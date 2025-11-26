
# Hi, I'm Blank! 👋
### I intend to use these script for all enginner.


# Bash scripts

## 1. System Monitoring and Health Check
```#!/bin/bash
set -euo pipefail

CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')
MEM=$(free -m | awk '/Mem:/ {printf "%.2f", $3/$2*100}')
DISK=$(df -h / | awk '/\/$/ {print $5}')

echo "CPU: $CPU%"
echo "MEM: $MEM%"
echo "DISK: $DISK"
```
- #!/bin/bash = Declare to run bash script and prove that
- set -euo pipefail = To run secure (Best Practice) 
- CPU=$(...) = Calculating CPU usage 
- MEM=$(...) = Calculating MEM usage
- DISK=$(...) = Calculating DISK usage
- echo "CPU: $CPU%" = To show with percentage
- echo "MEM: $MEM%" = To show with percentage
- echo "DISK: $DISK" = To show with percentage

