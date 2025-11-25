---
description: Start the dev server in the background (persists after agent completes)
agent: runtime-developer
subtask: true
---

Start the dev server as a detached background process that will continue running after this task completes.

$ARGUMENTS

## Instructions

1. First, kill any existing dev server processes to avoid port conflicts:
   ```bash
   # Kill known dev processes
   pkill -f "tsx watch api/index" 2>/dev/null || true
   pkill -f "nuxt dev" 2>/dev/null || true
   pkill -f "npm run dev" 2>/dev/null || true
   
   # Kill node processes on our ports
   lsof -ti:3737 | xargs kill -9 2>/dev/null || true
   lsof -ti:24678 | xargs kill -9 2>/dev/null || true
   
   # Kill any lingering node processes from this project
   pkill -f "node.*ash-grading-app" 2>/dev/null || true
   pkill -f "node.*dist/api" 2>/dev/null || true
   ```

2. Start the dev server detached using `nohup`:
   ```bash
   nohup npm run dev > /tmp/ash-dev.log 2>&1 &
   disown
   ```

3. Wait a few seconds and verify it started:
   ```bash
   sleep 5
   curl -s http://localhost:3737/health || echo "API not ready yet"
   curl -s http://localhost:24678 > /dev/null && echo "Frontend ready" || echo "Frontend not ready yet"
   ```

4. Report the status and how to view logs:
   - Logs are at `/tmp/ash-dev.log`
   - Use `tail -f /tmp/ash-dev.log` to follow logs
   - Use `pkill -f "npm run dev"` to stop

## Argument Options

- `api` - Start only the API server
- `app` or `frontend` - Start only the Nuxt frontend
- `stop` - Stop all running dev servers
- `status` - Check if dev servers are running
- `logs` - Show recent log output

## DO NOT

- Do not wait for the server or monitor logs
- Do not try to fix errors (use /debug for that)
- Just start the server and confirm it's running, then exit
