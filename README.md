
AWS & LINUX PRODUCTION TROUBLESHOOTING CHEAT SHEET

------------------------------------------------------------------------------
1. SYSTEM INFORMATION
------------------------------------------------------------------------------

hostname
Description: Displays the server hostname.

hostnamectl
Description: Shows hostname, OS version, kernel, and architecture.

whoami
Description: Displays the currently logged-in user.

id
Description: Shows UID, GID, and user groups.

date
Description: Displays current system date and time.

timedatectl
Description: Displays time, timezone, and NTP synchronization status.

uptime
Description: Shows system uptime and load averages.

uname -a
Description: Displays Linux kernel version and architecture.

cat /etc/os-release
Description: Displays operating system details.

------------------------------------------------------------------------------
2. CPU & MEMORY
------------------------------------------------------------------------------

top
Description: Real-time CPU, memory, and process monitoring.

htop
Description: Interactive process viewer (if installed).

free -h
Description: Shows RAM and swap usage.

vmstat 1 5
Description: Displays CPU, memory, paging, and I/O statistics.

mpstat -P ALL
Description: CPU usage for all cores.

lscpu
Description: Displays CPU information.

------------------------------------------------------------------------------
3. DISK & STORAGE
------------------------------------------------------------------------------

df -h
Description: Displays filesystem disk usage.

du -sh *
Description: Displays folder sizes.

lsblk
Description: Lists block storage devices.

blkid
Description: Shows disk UUID and filesystem type.

mount
Description: Displays mounted filesystems.

find / -type f -size +500M
Description: Finds files larger than 500 MB.

------------------------------------------------------------------------------
4. NETWORK
------------------------------------------------------------------------------

ip addr
Description: Displays network interfaces.

ip route
Description: Displays routing table.

hostname -I
Description: Displays server IP addresses.

ping google.com
Description: Tests network connectivity.

nslookup google.com
Description: Tests DNS resolution.

dig google.com
Description: Detailed DNS lookup.

curl ifconfig.me
Description: Displays public IP address.

------------------------------------------------------------------------------
5. PORTS & CONNECTIONS
------------------------------------------------------------------------------

ss -tulnp
Description: Lists listening TCP/UDP ports.

netstat -tulnp
Description: Lists listening ports (legacy).

lsof -i
Description: Shows open network connections.

lsof -i :80
Description: Displays process using port 80.

nc -zv HOST PORT
Description: Tests TCP connectivity.

telnet HOST PORT
Description: Tests remote port connectivity.

------------------------------------------------------------------------------
6. PROCESS MANAGEMENT
------------------------------------------------------------------------------

ps -ef
Description: Lists running processes.

ps aux
Description: Detailed process list.

ps -ef | grep nginx
Description: Searches for a running process.

kill PID
Description: Gracefully stops a process.

kill -9 PID
Description: Forcefully terminates a process.

pkill nginx
Description: Kills process by name.

------------------------------------------------------------------------------
7. SERVICES (systemd)
------------------------------------------------------------------------------

systemctl status SERVICE
Description: Checks service status.

systemctl start SERVICE
Description: Starts a service.

systemctl stop SERVICE
Description: Stops a service.

systemctl restart SERVICE
Description: Restarts a service.

systemctl reload SERVICE
Description: Reloads configuration.

systemctl enable SERVICE
Description: Starts service automatically on boot.

systemctl disable SERVICE
Description: Disables auto-start.

journalctl -u SERVICE -f
Description: Live service logs.

journalctl -u SERVICE -n 100
Description: Last 100 log entries.

------------------------------------------------------------------------------
8. LOG FILES
------------------------------------------------------------------------------

tail -f /var/log/syslog
Description: Monitor system logs.

tail -f /var/log/messages
Description: Monitor system logs (RHEL).

tail -f /var/log/auth.log
Description: SSH authentication logs.

tail -100 filename.log
Description: View last 100 lines.

less filename.log
Description: Read large log files.

grep ERROR filename.log
Description: Search logs.

------------------------------------------------------------------------------
9. USERS & PERMISSIONS
------------------------------------------------------------------------------

who
Description: Logged-in users.

last
Description: Login history.

groups USER
Description: User groups.

passwd USER
Description: Change password.

chmod
Description: Modify permissions.

chown
Description: Change ownership.

sudo -l
Description: View sudo permissions.

------------------------------------------------------------------------------
10. PACKAGE MANAGEMENT
------------------------------------------------------------------------------

Ubuntu

apt update
Description: Refresh package repository.

apt upgrade
Description: Upgrade packages.

apt install PACKAGE
Description: Install package.

RHEL

yum update
Description: Update packages.

dnf install PACKAGE
Description: Install package.

------------------------------------------------------------------------------
11. FILE SEARCH
------------------------------------------------------------------------------

find / -name filename
Description: Search by filename.

find / -type f
Description: Search files.

locate filename
Description: Fast filename lookup.

which command
Description: Displays executable location.

whereis command
Description: Displays binary, source, and man page.

------------------------------------------------------------------------------
12. ENVIRONMENT
------------------------------------------------------------------------------

env
Description: Lists environment variables.

printenv
Description: Displays environment variables.

echo $PATH
Description: Displays executable search path.

------------------------------------------------------------------------------
13. SSH
------------------------------------------------------------------------------

ssh user@host
Description: Connect to remote server.

scp file user@host:/path
Description: Copy files.

ssh-keygen
Description: Generate SSH keys.

------------------------------------------------------------------------------
14. AWS CLI
------------------------------------------------------------------------------

aws configure list
Description: Shows AWS CLI configuration.

aws sts get-caller-identity
Description: Shows current IAM identity.

aws configure get region
Description: Displays configured AWS region.

------------------------------------------------------------------------------
15. EC2
------------------------------------------------------------------------------

curl http://169.254.169.254/latest/meta-data/
Description: View EC2 metadata.

curl http://169.254.169.254/latest/meta-data/instance-id
Description: Displays EC2 instance ID.

curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
Description: Shows attached IAM role.

------------------------------------------------------------------------------
16. STORAGE
------------------------------------------------------------------------------

aws s3 ls
Description: Lists S3 buckets.

aws s3 ls s3://bucket-name
Description: Lists bucket contents.

aws s3 cp FILE s3://bucket
Description: Upload file.

aws s3 cp s3://bucket/file .
Description: Download file.

------------------------------------------------------------------------------
17. IAM
------------------------------------------------------------------------------

aws iam list-roles
Description: Lists IAM roles.

aws iam get-role --role-name ROLE
Description: Displays IAM role details.

------------------------------------------------------------------------------
18. SYSTEM MANAGER
------------------------------------------------------------------------------

aws ssm describe-instance-information
Description: Displays managed EC2 instances.

aws ssm get-parameter --name PARAMETER
Description: Reads Parameter Store value.

------------------------------------------------------------------------------
19. SECRETS MANAGER
------------------------------------------------------------------------------

aws secretsmanager list-secrets
Description: Lists secrets.

aws secretsmanager get-secret-value --secret-id SECRET
Description: Retrieves secret value.

------------------------------------------------------------------------------
20. CLOUDWATCH
------------------------------------------------------------------------------

systemctl status amazon-cloudwatch-agent
Description: Checks CloudWatch Agent.

journalctl -u amazon-cloudwatch-agent -f
Description: CloudWatch Agent logs.

------------------------------------------------------------------------------
21. POSTGRESQL
------------------------------------------------------------------------------

psql -h HOST -U USER -d DATABASE
Description: Connect to PostgreSQL.

\l
Description: List databases.

\dt
Description: List tables.

\du
Description: List roles.

SELECT version();
Description: PostgreSQL version.

------------------------------------------------------------------------------
22. WEB SERVER
------------------------------------------------------------------------------

curl http://localhost
Description: Test local web server.

curl -I http://localhost
Description: View HTTP headers.

wget URL
Description: Download file.

------------------------------------------------------------------------------
23. PERFORMANCE
------------------------------------------------------------------------------

iostat
Description: Disk I/O statistics.

sar
Description: Historical CPU, memory, and network usage.

dmesg
Description: Kernel messages.

------------------------------------------------------------------------------
24. TROUBLESHOOTING ORDER (PRODUCTION)
------------------------------------------------------------------------------

1. Check service status.
2. Check recent logs.
3. Check listening ports.
4. Verify process is running.
5. Verify CPU & memory.
6. Verify disk usage.
7. Verify network connectivity.
8. Verify DNS resolution.
9. Verify firewall/security groups.
10. Verify IAM permissions.
11. Verify AWS services (S3, SSM, Secrets, RDS).
12. Verify application functionality.
13. Monitor CloudWatch metrics and logs.
14. Confirm health checks (ALB/Target Group).
15. Escalate only after collecting evidence (logs, metrics, timestamps).
