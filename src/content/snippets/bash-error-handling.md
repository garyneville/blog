---
title: "Bash Script Error Handling"
description: "Robust error handling patterns for bash scripts"
publishDate: 2024-11-16
language: "bash"
category: "bash"
tags: ["bash", "scripting", "error-handling", "devops"]
draft: false
---

Here's my go-to template for robust bash script error handling:

```bash
#!/bin/bash

# Exit on any error, undefined variable, or pipe failure
set -euo pipefail

# Trap to cleanup on exit
cleanup() {
    echo "Cleaning up..."
    # Add cleanup commands here
}
trap cleanup EXIT

# Function to log messages with timestamp
log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $*" >&2
}

# Function to handle errors
error_exit() {
    log "ERROR: $1"
    exit 1
}

# Example usage
main() {
    log "Starting script..."
    
    # Check if required command exists
    command -v docker >/dev/null 2>&1 || error_exit "Docker is required but not installed"
    
    # Safe way to handle optional environment variables
    API_URL="${API_URL:-http://localhost:3000}"
    
    # Example of checking exit codes explicitly
    if ! curl -sf "$API_URL/health" >/dev/null; then
        error_exit "Health check failed for $API_URL"
    fi
    
    log "Script completed successfully"
}

# Only run main if script is executed directly (not sourced)
if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
    main "$@"
fi
```

## Key Features

- **`set -euo pipefail`**: Exit on errors, undefined variables, and pipe failures
- **Trap cleanup**: Always run cleanup code on exit
- **Logging function**: Timestamped log messages
- **Error handling**: Consistent error reporting and exit
- **Source check**: Safe to source the script without running main

This template catches most common bash scripting pitfalls and makes debugging much easier.