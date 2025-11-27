
# Hi, I'm Blank! 👋
### I intend to use these script for all enginner.😊


# Bash scripts 💲

## ✔ Tool List (MUST KNOW)
- ### grep → search logs
- ### awk → extract columns
- ### sed → replace
- ### cut, sort, uniq, wc
- ### curl → API call
- ### jq → JSON parse
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
## 1. System Monitoring and Health Check
```#!/bin/bash
#!/bin/bash
set -euo pipefail

CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')
MEM=$(free -m | awk '/Mem:/ {printf "%.2f", $3/$2*100}')
DISK=$(df -h / | awk '/\/$/ {print $5}')

echo "CPU: $CPU%"
echo "MEM: $MEM%"
echo "DISK: $DISK"
```
- #!/bin/bash        = Declare to run bash script and prove that
- set -euo pipefail  = To run secure (Best Practice) 
- CPU=$(...)         = Calculating CPU usage 
- MEM=$(...)         = Calculating MEM usage
- DISK=$(...)        = Calculating DISK usage
- echo "CPU: $CPU%"  = To show with percentage
- echo "MEM: $MEM%"  = To show with percentage
- echo "DISK: $DISK" = To show with percentage
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
## 2. Log Analyzer Script
```#!/bin/bash
#!/bin/bash
LOG=/var/log/nginx/access.log

echo "Top 10 IPs:"
awk '{print $1}' $LOG | sort | uniq -c | sort -nr | head

echo "Top 10 URLs:"
awk '{print $7}' $LOG | sort | uniq -c | sort -nr | head

echo "4xx errors:"
awk '$9 ~ /^4/ {print}' $LOG | wc -l

echo "5xx errors:"
awk '$9 ~ /^5/ {print}' $LOG | wc -l
```
- #!/bin/bash        = Declare to run bash script and prove that
- echo "Top 10 IPs"  = Most enter 10 Ip addresses
- echo "Top 10 URLs" = Most request 10 URL
- echo "4xx errors"  = Client side error bulk
- echo "5xx errors:" = Server side error bulk
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
## 3. File & Database Backup Automation
```#!/bin/bash
#!/bin/bash
SRC=/var/www/html
DEST=/backup

mkdir -p $DEST
TS=$(date +%F-%H%M)
tar -czf $DEST/site-$TS.tar.gz $SRC
find $DEST -mtime +7 -delete
```
- #!/bin/bash                         = Declare to run bash script and prove that
- SRC and DEST                        = Recognise variables
- mkdir                               = Making dir
- $(date +%F-%H%M)                    = Current date and time
- tar -czf $DEST/site-$TS.tar.gz $SRC = In SRC files are put into DEST by compressing with .tar.gz
- find $DEST -mtime +7 -delete        = Over 7days delete automatic in DEST's files
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
## 4. Cron Job Scheduling Automation
```#!/bin/bash
*/15 * * * * /scripts/health.sh >> /scripts/health.log
0 3 * * * /scripts/backup.sh
```
- #!/bin/bash                         = Declare to run bash script and prove that
- health.sh                           = Refer to 1. System Monitoring and Health Check
- backup.sh                           = Refer to 3. File & Database Backup Automation
- */15 * * * *                        = Run that script every 15 minutes ago
- 0 3 * * *                           = Run that script every 3:00am for everyday
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
