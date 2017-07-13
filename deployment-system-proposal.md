# Deployment System Proposal
## Requirements
### Improve deploy speed
Deploying via SSH takes forever. In the past, 254 has built a system where they transfer the robot binary to the robot via HTTP to deal with this problem. Whatever we do, deployment needs to be faster.
### Deploy runtime libraries
So far, we have been manually installing runtime libraries on the roboRIO after the initial flash. This is problematic because it means someone (Connor) has to manually coalesce the runtime libraries to a single tarball and extract it on the RIO. This process also needs to be repeated every time the libraries are updated. Instead, we should fetch the runtime libraries from WPILib's Maven repo, somehow verify their presence on the RIO (perhaps via checksums), and copy them over to the RIO if needed. `rsync` could possibly accomplish this.
### Replace the robotCommand system
The robotCommand system requires a bunch of ssh commands to run, and isn't documented. I propose replacing it and building our own better documented system to start and stop the robot binary.
### Language agnostic & easy install
Language shouldn't matter. No manually created tarballs or weird roboRIO setup should be required. This is to make the system useful for other teams.
## Strategy
Some things to consider:

* Language?
* Monolithic service? Many small services?