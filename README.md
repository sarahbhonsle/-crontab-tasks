# What is Cron?
Cron is a time-based job scheduling daemon found in Unix-like operating systems (including RHEL). It runs continuously in the background (crond.service) and checks system configuration files every minute to see if there are any scripts, commands, or automation tasks scheduled to execute.

A crontab (cron table) is a text file containing lists of commands scheduled to run at specific times.

User Crontabs: Stored securely under /var/spool/cron/ and edited using the crontab -e command. These run with the permissions of the user who created them.

System-wide Crontabs: Located at /etc/crontab and inside the /etc/cron.d/ directory. These are managed exclusively by root and require specifying a target execution user.

# The Cron Syntax Architecture
A standard cron expression consists of five fields followed by the command execution string. Each field is separated by a single space or tab.
   SHOWN IN IMAGE..
    
# Syntax Operators
To create flexible schedules, cron utilizes four specialized characters:

* (Asterisk): Matches every possible value in that field. (e.g., a * in the hour field means "every hour").

, (Comma): Defines a list of discrete values. (e.g., 1,3,5 in the day of week field means "Monday, Wednesday, and Friday").

- (Hyphen): Defines a continuous range of values. (e.g., 9-17 in the hour field means "9 AM through 5 PM").

/ (Slash): Specifies step increments. (e.g., */15 in the minute field means "every 15 minutes").

# Practical Lab Code & Configurations
       Essential Crontab Management Commands:
1.Edit the current user's crontab file (opens in vi/nano)
crontab -eu <username>

2.List all active cron jobs scheduled for the current user
crontab -lu <username>

3.Remove/Delete all scheduled cron jobs for the current user safely
crontab -r

# (Root Only) Edit or list cron jobs for a specific user (e.g., tom)
sudo crontab -eu tom 
sudo crontab -lu tom -l

# Common Enterprise Schedule Examples :-
Here are exact configuration lines you can paste inside a crontab -e session:

# Example 1: Run a backup script every single day at exactly 2:30 AM
30 2 * * * /usr/local/bin/backup.sh

# Example 2: Run a disk-space check script every 15 minutes, 24/7
*/15 * * * * /opt/scripts/disk_check.sh

# Example 3: Execute a system cleanup tool only at midnight on the 1st and 15th of every month
0 0 1,15 * * /usr/bin/system_cleanup

# Example 4: Run an audit logging script at 6:00 PM, Monday through Friday only
0 18 * * 1-5 /var/www/html/audit_logger.sh
