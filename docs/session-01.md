\# Session 1 - 2026-10-26



\## What I did

It's been a long time since my last AWS hands-on practice. Finally, I took the first step!

Today I launched what was probably my first EC2 instance ever (okay, maybe I'm exaggerating a little).

I made a simple Spring Boot project, uploaded the JAR file with scp, and connected to the server via SSH.



When I took an AWS course before, the instructor said, "Avoid using SSH as much as possible for security reasons."

But I only remembered "DON'T USE SSH" without understanding why.

This time I learned that it's okay for practice because the security group only allows SSH from my public IP.



I also added an inbound rule to open port 8080.

Then I ran the app in the background with nohup, which stands for "no hang up."

It keeps the app running even after I close the terminal.



\## Problem

\- I didn't know the difference between PowerShell and cmd, so the SSH key path didn't work.

\- I accidentally split one scp command into several lines, so the file wasn't uploaded.



\## Cause

\- I used PowerShell syntax (`$env:USERPROFILE`) in cmd.

\- scp needs the key, the source file, and the destination in one line.



\## Solution

\- I switched to PowerShell and typed the scp command in a single line.



\## What I learned

\- To connect to a server via SSH, you need a key pair. Only I have the private key, so I must keep it safe.

\- I reviewed how to create a security group and add an inbound rule.

\- I'm not sure I could set it up again without help yet, but I'll get used to it.

\- I'm still curious what scp is.



\## Next

Rule: Don't ask Claude first. Try for 15 minutes on my own and read the official AWS docs.

If I'm still stuck, ask with the exact error message.



\### Mission 1: Build my own network (1.5 hours)

\- Goal: Deploy the app in a VPC I build myself, not the default VPC.

\- Requirements:

&#x20; - VPC with CIDR 10.0.0.0/16

&#x20; - 2 public subnets and 2 private subnets across 2 Availability Zones

&#x20; - An internet gateway attached to the VPC

&#x20; - Separate route tables for public and private subnets

\- Done when: I can open the app in a browser from an EC2 instance in a public subnet of the new VPC.

\- Hints: "VPC only" option, route table association, auto-assign public IPv4



\### Mission 2: Replace nohup with systemd (1 hour)

\- Goal: Run the app as a systemd service.

\- Done when:

&#x20; - The app comes back automatically after `sudo reboot`.

&#x20; - The app restarts by itself after I kill the process.

\- Hints: /etc/systemd/system/\*.service, Restart=always, systemctl enable, journalctl -u



\### Mission 3: Connect without SSH (1 hour)

\- Goal: Remove the SSH rule (port 22) from the security group and still access the server.

\- Done when:

