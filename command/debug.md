---
description: Start dev server in background, monitor logs, and fix runtime errors iteratively
agent: runtime-developer
subtask: true
---

Debug runtime errors by starting the dev environment in the background and iteratively fixing issues.

$ARGUMENTS

## Default Behavior

If no arguments provided:
1. Kill any existing dev servers and clear ports
2. Start `npm run dev` detached in background (logs to `/tmp/ash-dev.log`)
3. Monitor log file for errors/warnings
4. Fix issues iteratively until clean startup
5. Leave server running when done
6. Report all changes made

## Startup Commands (Run in Parallel)

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

# Start detached
nohup npm run dev > /tmp/ash-dev.log 2>&1 &
disown

# Wait for startup
sleep 5
```

## Log Monitoring

Read logs from `/tmp/ash-dev.log`:
```bash
tail -100 /tmp/ash-dev.log   # Recent output
cat /tmp/ash-dev.log | grep -i error   # Find errors
cat /tmp/ash-dev.log | grep -i warn    # Find warnings
```

After making fixes, check for new errors:
```bash
sleep 3
tail -50 /tmp/ash-dev.log
```

## Argument Options

You can specify:
- `api` or `backend` - Only debug the API server
- `app` or `frontend` - Only debug the Nuxt frontend  
- `browser` - Capture and debug browser console errors using Playwright
- `warnings` - Include warnings in the fix cycle (not just errors)
- `typecheck` - Run typecheck and fix TypeScript errors (no server needed)
- Specific error message - Focus on fixing a particular error

## Examples

```
/debug                    # Debug everything (server stays running)
/debug api                # Debug only the API
/debug frontend warnings  # Debug frontend including warnings
/debug browser            # Capture browser console errors
/debug typecheck          # Fix TypeScript errors
/debug "Cannot read property 'x'"  # Focus on specific error
```

## Workflow

1. Start dev server detached (non-blocking)
2. Read logs from `/tmp/ash-dev.log`
3. Parse for errors/warnings
4. Locate source files and understand context
5. Apply minimal fixes
6. Wait a moment, re-read logs to verify
7. Repeat until clean
8. Server keeps running - report all changes to primary agent

## Verification

After fixes, verify health:
```bash
curl -s http://localhost:3737/health && echo "API OK"
curl -s http://localhost:24678 > /dev/null && echo "Frontend OK"
```
