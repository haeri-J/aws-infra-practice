Session 3 - 2026-11-20



\#What I did

\-Lanched a new EC2 instance and installed java 17('dnf install java-17-amazon-correto').

\-Uploaded the Spring Boot JAR with scp.

\-Registered the app as a \*\*systemd service\*\* instead of running it with nohup.

\-'daemon-reload' -> 'enable' -> 'start' -> status' showed 'active (runnig)'.



\##Why I did it this way

\-nohup keeps the app runing after I log out, but it does not survive a reboot or a crash.

\-systemd restarts the app automatically ('Restart = always') and starts it at boot ('enable').



\## Service file

'''ini

\[Unit]

Description = hello app

After=network.target



\[Service]

User=ec2-user

ExecStar=\\usr\\bin\\java -jar \\home\\ec2-user\\hello0.0.1-SNAPSHOT.jar

Restart-always

SuccessExitstatus=143



\[Install]

WantedBy=multi-user.target



\## systemctl commands

| Command | What it does |

|---|---|

| `sudo systemctl daemon-reload` | Re-read config files so systemd notices the new service file |

| `sudo systemctl enable hello` | Start automatically at boot |

| `sudo systemctl start hello` | Start it now |

| `sudo systemctl status hello` | Check if it's running (press `q` to exit) |

| `sudo systemctl stop hello` | Stop it properly (it stays off) |



\#Problems

\### 1. SSH connetion timed out

* Cause : I was in a cafe, so my public Ip was different.the security gruop noly allowed my home IP.
* Solution: Edited the inbound rules and selected \*\*My IP\*\* again.
* Lession: "MY IP" is a one-time shortcut. The rule stores a fixed IP, so it does not update when I move.( it was my big disappointment of myself. even you got a aws-ssa.)



\### 2. scp: "hostname contains invalid characters"

\-Cause : I copied the placeholder '<IP>' literally.

\-Soultion: Repalced it with the ral public IP,



\### 3 The instance was in the defualt VPC

* Cause : I didn't choodse 'hello-vpe' in Network settings.
* How I noticed: the private IP was '172.31.x.x' (defalut VPC), not '10.0.x.x' (my VPC).



\## Concepts I learned

\- \*\*Instance\*\*: the virtual server in AWS.

\- \*\*Program / app\*\*: a file on disk (my JAR).

\- \*\*Process\*\*: a program while it's running, with a PID.

\- \*\*Service (daemon)\*\*: a background process managed by systemd. It starts at boot and restarts if it dies.

\- \*\*Thread\*\*: a smaller worker inside a process. My Java process had about 30 (`Tasks: 30`).

\- Service ⊃ Process ⊃ Thread.

\- \*\*Artifact\*\*: the output of a build. My JAR is the artifact (`com.haeri:hello:0.0.1-SNAPSHOT`).

\- \*\*systemd\*\* = system daemon, \*\*systemctl\*\* = system control.

\- \*\*Placeholder\*\*: an example value in docs that I must replace with my own.

\- `PS C:\\...>` is my PC. `\[ec2-user@...]$` is the server.

\- \*\*Kill test\*\*: `kill -9` simulates a crash, and systemd should bring the app back with a new PID.



\## Next

\- Launch in `hello-vpc` / `hello-public-2a`.

\- Kill test, reboot test, browser check.

\- Mission 3: Session Manager (no SSH port, no IP rules).



