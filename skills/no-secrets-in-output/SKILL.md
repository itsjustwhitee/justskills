---
name: no-secrets-in-output
description: Use before printing, logging, echoing, committing, or writing to a file anything that could contain an API key, password, token, connection string, or environment variable value.
type: Skill
title: No Secrets In Output
status: stable
---

# No Secrets In Output

## Overview

Secret material never leaves the process in readable form - not in terminal
output, logs, error messages, commit contents, knowledge files, or test
fixtures.

## Covered

API keys, passwords, OAuth/JWT tokens, session cookies, private keys, database
connection strings, cloud credentials, and the raw values of environment
variables that hold any of the above.

## Rules

- Do not `echo`, `print`, or log a secret to show "what it is". Show its name,
  its length, or a 4-char prefix at most.
- Do not paste `.env`, credential files, or `printenv` / `env` output into a
  reply, a commit, or a doc.
- When a command needs a secret, reference it (`$API_KEY`), never inline the
  literal value.
- Redact before quoting logs or stack traces that may embed one.
- Found a secret already committed or printed? Say so plainly and stop; treat it
  as compromised.

## Red flags

- About to run `cat .env`, `env`, or `printenv` and put the result in a message.
- A test fixture with a real-looking token in it.
- Debug logging that dumps a whole request, config, or environment object.
