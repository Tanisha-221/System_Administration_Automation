#!/bin/bash
mkdir assignment1
# Save all services to a file
systemctl list-units --type=service --all >> assignment1/all_service.txt

# Check Apache status and logs (optional debug)
sudo systemctl status apache2 >> assignment1/service.log
sudo journalctl -u apache2 >> assignment1/service.log

# Check the server name 
hostname >> assignment1/servername.txt

# user name 
who >> assignment1/username.txt

# Restart Apache (optional)
# sudo systemctl restart apache2

# Monitor Apache service failure counts and alert
SERVICE="apache2"
FAIL_COUNT_FILE="/tmp/${SERVICE}_fail_count"
MAX_FAILS=3
LOG_FILE="assignment1/service_monitor.log"

if [ ! -f "$FAIL_COUNT_FILE" ]; then
  echo 0 > "$FAIL_COUNT_FILE"
fi

if systemctl is-active --quiet "$SERVICE"; then
  echo 0 > "$FAIL_COUNT_FILE"
else
  count=$(cat "$FAIL_COUNT_FILE")
  count=$((count + 1))
  echo $count > "$FAIL_COUNT_FILE"
  if [ "$count" -ge "$MAX_FAILS" ]; then
    echo "ALERT: Service $SERVICE failed to start $count times in a row on $(hostname)." >> "$LOG_FILE"
    echo 0 > "$FAIL_COUNT_FILE"
  fi
fi

# Check and count all failed services
failed_count=$(systemctl list-units --type=service --all --failed | grep '.service' | wc -l)
if [ "$failed_count" -gt 0 ]; then
  ./service_monitor.sh  # Make sure this script exists and is executable
fi
echo "There are $failed_count failed services"

# Log disk usage
df -h >> assignment1/DiskSpace.txt

# Log zombie processes
ps aux | grep '[Z]' >> assignment1/Zombieprocess.txt






crontab -e

35 10 * * * /bin/bash/home/azure/services.sh >> home/azure/crone.daily
35 11 * * 1 /bin/bash/home/azure/servises.sh >> home/azure/crone.daily
