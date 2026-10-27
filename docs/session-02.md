\# Session 2 - 2026-10-28



\## What I did

\- I designed VPC arthitecture using draw.io. There was one VPC(10.0.0.0/16) , two AZ(2a, 2c), two public subnet(10.0.1.0/24,10.0.2.0/24). two private subnet(10.0.11.0/24,10.0.12.0/24).IGW, two route table. after that I set the system on AWS using console based on what I designed. and I attached tags each with my name rule(project name-role-AZ). and I ended up deploying the simple spring boot project via SSH like yesterday. 



\## Architecture

!\[VPC architecture](../images/session-02-vpc.png)



\## Problem 1

\- Problem: There was no public IP on my EC2

\- Cause: I didn't tick that option when I make publice subnets.

\- Solution: so I back to the subnet setting to turn it on. 



\## Problem 2

\- Problem: I didn't upload jar files on the sever.

\- Cause: There was no ":\~" end of the scp. so I copied it to my computer.

\- Solution: so I added ":\~" end of the scp to reach proper way. 



\## What I learned

\-A number behind "\\" of CIDR means locked seat of IP. so The number is more big, IP's scope is more small.

\-Therefore, if it is "/32', it means only one addrress. On the other hand, if it is "/0", it means everywhere to acesse. 



\## Review question

\*\*What makes a subnet "public"?\*\*

\- IGW! it's suppose to have IGW toward outworld. 



\## Next

\- Mission 2: Replace nohup with systemd

