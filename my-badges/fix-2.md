<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/00843181ff9a5f48d5befa4ffb21faddbedc5c2e">0084318</a>: fix: allow port 22 temporarily in UFW during SSH port transition

Address review comment: prevent lockout if SSH restart fails by
keeping port 22 open until SSH is confirmed running on the custom port,
then removing the temporary rule.
- <a href="https://github.com/ksysoev/cloudlab/commit/9029bb3af6cfaa5bdaf11a9867f209c2158c24a2">9029bb3</a>: fix: correct cloud-init service restart ordering and configuration

- Fix SSH service name: use 'ssh' instead of 'sshd' for Ubuntu 24.04
- Fix ordering: configure UFW firewall before changing SSH port to avoid lockout
- Fix users block: add 'default' entry to preserve root SSH access
- Fix fail2ban: add jail.local with custom SSH port instead of defaulting to port 22
- Fix Docker daemon.json: ensure /etc/docker exists before write_files runs
- Fix docker group: add deployer to group in runcmd after Docker install
- Remove unused deployer_ssh_public_key variable, use single ssh_public_key


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>