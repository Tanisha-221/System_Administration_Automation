#!/bin/bash
SERVICE="apache2"
FAIL_COUNT_FILE="/tmp/${SERVICE}_fail_count"
MAX_FAILS=3
LOG_FILE="service_monitor.log"
# Initialize fail count file if it doesn't exist
if [ ! -f "$FAIL_COUNT_FILE" ]; then
  echo 0 > "$FAIL_COUNT_FILE"
fi
# Check service status
if systemctl is-active --quiet "$SERVICE"; then
  # If service running, reset failure count
  echo 0 > "$FAIL_COUNT_FILE"
  
else
  # Service not running, increment fail count
  count=$(cat "$FAIL_COUNT_FILE")
  count=$((count + 1))
  echo $count > "$FAIL_COUNT_FILE"
  # Alert if failure count reached threshold
  if [ "$count" -ge "$MAX_FAILS" ]; then
    echo "ALERT: Service $SERVICE failed to start $count times in a row on $(hostname).">> "$LOG_FILE"
    # Reset failure count after alert
    echo 0 > "$FAIL_COUNT_FILE"
  fi
fi



#bin/bash
SERVICE="apache2"
FAIL_COUNT_FILE="/tmp/${SERVICE}_fail_count"
MAX_FAILS=3
LOG_FILE="service_monitor.log"
# Initialize fail count file if it doesn't exist
if [ ! -f "$FAIL_COUNT_FILE" ]; then
  echo 0 > "$FAIL_COUNT_FILE"
fi
# Check service status
if systemctl is-active --quiet "$SERVICE"; then
  # If service running, reset failure count
  echo 0 > "$FAIL_COUNT_FILE