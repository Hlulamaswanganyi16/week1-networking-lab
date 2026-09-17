# Linux Fundamentals — Hands-On Log

Part of my self-directed Cloud Security Engineer study path.
Environment: WSL2 (Ubuntu 26.04 LTS) on Windows 11.

## What I did

- Created a new user account (`sudo adduser testuser`)
- Set and verified file permissions on the new user's home directory
- Switched between user accounts (`su - testuser`) and confirmed identity with `whoami`
- Reviewed real authentication logs (`/var/log/auth.log`)
- Installed and configured the OpenSSH server
- Generated a public/private SSH key pair (`ssh-keygen`)
- Wrote a one-line script to extract and save a list of all system users

## What broke, and how I fixed it

**Problem 1 — Permission denied on chmod**
Running `chmod 700 /home/testuser` failed with `Operation not permitted (os error 1)`.
Cause: the folder was owned by `testuser`, not by me. Only the owner or an admin can change a folder's permissions.
Fix: ran the same command with `sudo` — `sudo chmod 700 /home/testuser` — which succeeded and correctly restricted the folder to `drwx------`.

**Problem 2 — SSH installed but not running**
After `sudo apt install openssh-server -y`, running `sudo systemctl status ssh` showed the service as `disabled` and `inactive (dead)`.
Cause: installing a service doesn't automatically start or enable it.
Fix: ran `sudo systemctl enable --now ssh`, which both started the service immediately and set it to auto-start on boot. Confirmed with a second status check showing `active (running)`.

## Commands used (reference)

\`\`\`bash
sudo adduser testuser
sudo chmod 700 /home/testuser
sudo chown testuser:testuser /home/testuser
su - testuser
whoami
exit
sudo tail -20 /var/log/auth.log
sudo apt install openssh-server -y
sudo systemctl enable --now ssh
sudo systemctl status ssh
ssh-keygen
cat /etc/passwd | cut -d: -f1 > my_users_list.txt
\`\`\`

## What this demonstrates

- Understanding of Linux's user/permission/ownership model, not just command syntax
- Ability to diagnose a service that's installed but not actually running — a common real-world gap
- Comfort reading and interpreting real system logs
- First step toward writing basic audit/reporting scripts

## Next steps

Moving on to hardening this environment further: tightening SSH configuration, exploring log analysis with more targeted queries, and continuing toward the AZ-104 track.
