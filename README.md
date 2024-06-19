#!/bin/bash

# System Information
USERNAME=$(whoami)
CURRENT_DATETIME=$(date '+%Y-%m-%d %H:%M:%S')
HOSTNAME=$(hostname)
OS="${NAME} ${VERSION}"
UPTIME=$(uptime -p)

# Hardware Information
CPU_INFO=$(lshw -class processor | grep -E "product|vendor" | sed 's/ *//;s/: /: /')
CPU_SPEED=$(lscpu | grep "MHz" | awk -F: '{print $2}')
RAM_SIZE=$(free -h | awk '/^Mem:/{print $2}')
DISKS=$(lsblk -o NAME,MODEL,SIZE -d | tail -n +2 | awk '{print "Disk: "$2 " " $3}')
VIDEO_CARD=$(lshw -class display | grep product | sed 's/.*product: //')


# System Report Output
cat <<EOF

System Report generated by $USERNAME, $CURRENT_DATETIME

System Information
------------------
Hostname: $HOSTNAME
OS: $OS
Uptime: $UPTIME

Hardware Information
--------------------
CPU: $CPU_INFO
Speed: $CPU_SPEED
RAM: $RAM_SIZE
Disks: $DISKS
Video: $VIDEO_CARD
