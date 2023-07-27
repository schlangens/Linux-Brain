### Scheduling Tasks

#### What is the easiest method to schedule a command?

---

- `at`
  - Executes a command at a certain time
  - Ideal for one-time activities
- Schedule a command
  - `at 3 PM Fri /home/dpezet/backupdb.sh`
- List scheduled commands
  - `atq` (Lists queued commands)

#### Can everyone use the "at" command, or is it limited to administrators?

---

- Restrict access
  - `/etc/at.allow`
  - `/etc/at.deny`
  - If neither exist, only root can run the `at` command

#### Can we create recurring tasks with the "at" command?

---

- cron
  - Executes jobs at a predetermined time
  - Can execute for users or system wide

#### How do we schedule jobs with cron?

---

- Simple scheduling with crond
  - Config files (System)
    - `/etc/cron.hourly/`
    - `/etc/cron.daily/`
    - `/etc/cron.weekly/`
    - `/etc/cron.monthly/`
  - Standard bash scripts
  - Example
    - `/etc/cron.daily/logrotate`

#### What if we want the tasks to run at a specific time?

---

- Create jobs at a specific time
- System jobs are stored in `/etc`
  - `/etc/crontab`
  - `/etc/cron.d/`
- Job syntax
  1.  Minute of the hour (0-59)
  2.  Hour of the day (0-23)
  3.  Day of the month (1-31)
  4.  Month of the year (1-12)
  5.  Day of the week (0-7)
  6.  User context for execution
  7.  Command and options

#### How do we schedule a job for an individual user?

---

- Edit user cron jobs
  - `crontab -e`
- User cron jobs reside in:
  - `/var/spool/cron/username`
  - `/var/spool/cron/tabs/username`
  - `/var/spool/cron/crontabs/username`
- Example
  - Run a backup every night at 3AM e.g.
  - `0 3 * * * /home/dpezet/backupdb.sh`

* List a user's cron jobs
  - `crontab -l`
  - `crontab -l -u <user>`

#### What happens if our computer is shut down when a task should run?

---

- `anacron`
  - Similar to `cron`
  - Designed for desktops/laptops
  - Will run jobs that were scheduled to run while system was offline.
  - `/etc/anacrontab`

#### Can we restrict access to "cron" like we did with "at"?

---

- Restrict access
  - `/etc/cron.allow`
  - `/etc/cron.deny`
  - Use one or the other
  - List usernames one per line
