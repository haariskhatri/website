+++
title = "Adding flairs to logs in bash scripts"
date = "2025-05-07T20:19:48.524Z"
type = "post"
description = "Adding formatting to logs in bash scripts"
in_search_index = true
[taxonomies]
tags = ["Bash"]
+++
# Adding Flairs to Logging in Bash Script
I've always felt that bash scripting has alway been bland compared to python and javascript. You rarely see any color on the terminal. Little did know that you could actually use unicode strings to use colors and emojis as well. And that makes a lot of difference. So I spent some time creating a logging function which helps adds some colors to the script logs ( quite literally! ).

```bash
#!/bin/bash

# Logging function
log() {
  local type=$1
  local message=$2

  case "$type" in
    info)
      echo -e "${CYAN}${BOLD}ℹ️  $message${RESET}"
      ;;
    success)
      echo -e "${GREEN}${BOLD}✅ $message${RESET}"
      ;;
    warning)
      echo -e "${YELLOW}${BOLD}⚠️  $message${RESET}"
      ;;
    error)
      echo -e "${RED}${BOLD}❌ $message${RESET}"
      ;;
    step)
      echo -e "${BOLD}🔧 $message${RESET}"
      ;;
    *)
      echo -e "$message"
      ;;
  esac
}

# Dynamic header function
print_header() {
  local title="$1"

  echo -e "${CYAN}=============================================${RESET}"
  echo -e "${BOLD}${title}${RESET}"
  echo -e "${CYAN}=============================================${RESET}"
}

# Example usage
print_header "🚀 Starting Deployment"

log info "Lets get Started"
log success "App Deployed"
log error "Invalid Build"
log warning "Coverage not good"
log step "Deployment"

print_header "✅ Finished"
```

## Output
```text
=============================================
🚀 Starting Deployment
=============================================
ℹ️ Lets get Started
✅ App Deployed
❌ Invalid Build
⚠️  Coverage not good
🔧 Deployment
=============================================
✅ Finished
=============================================
```
