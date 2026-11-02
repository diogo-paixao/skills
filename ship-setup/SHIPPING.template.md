# SHIPPING

_Last reviewed: YYYY-MM-DD. Based on: <list of pipeline/deploy files this was derived from>._
_Label each line **Found (file)**, **Inferred (why)** or **Unknown, needs you** while drafting; remove labels once confirmed._

## Environments
- Production: <where it lives, what deploys it>
- Staging / preview: <if any>

## Deploy path
- Trigger: <CI on merge to main / `vercel --prod` / script / manual>
- Exact commands or pipeline: <...>
- Anything that runs alongside the normal build (asset or media uploads, migrations): <...>

## Branch and commit rules
- Branch that deploys: <...>
- Merge style: <merge / squash / rebase>
- Commit message format: <...>
- Tagging / versioning: <...>

## Pre-ship checks
- <tests, build, lint, type-check>
- <performance or accessibility budgets>
- <head tags, changelog, env vars>

## Approval rules
- What needs the owner's explicit "approved", and in what form: <...>

## Smoke test
- <what to check right after release>

## Rollback
- <how to undo a bad release>

## Never do
- <force-push, certain env vars, certain days, etc.>
