<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/7d7419e7c127778c384b0a27de5936b455c3bc4d">7d7419e</a>: Fix PR review issues: architecture support, SSH config, Alloy forward_to, and CI improvements

Address all critical and minor issues from PR #15 review:

High priority fixes:
- Add dynamic architecture mapping for Docker repo (support arm64/armhf)
- Remove duplicate SSH config files (cloud-init bootstrap.conf)
- Fix Alloy config to be conditional when Grafana Cloud not configured
- Add droplet reboot wait mechanism in configure workflow

Medium priority fixes:
- Remove workflow double-trigger by eliminating path-based push trigger
- Fix SSH key configuration working directory context
- Install collections from requirements.yml instead of hardcoded list

Low priority fixes:
- Add mock inventory for integration test in test-ansible workflow
- Update README Ansible version requirement from 2.14 to 2.15.0
- Fix README test.sh documentation to match actual script usage
- Remove unused community.docker collection dependency
- <a href="https://github.com/ksysoev/cloudlab/commit/03b7e5af2a4063364413449218541f693f2106df">03b7e5a</a>: Fix idempotence issue in Docker role test

Remove 'groups: users' from deployer user creation in converge.yml to avoid
resetting user groups on subsequent runs. The role will add the docker group,
and we don't want to remove it on the second converge run.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>