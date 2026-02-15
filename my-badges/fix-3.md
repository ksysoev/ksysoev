<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/ec225fc72f55d980f387ed8e25850688902a845a">ec225fc</a>: fix: upgrade Terraform version to 1.9.0 for test support

Terraform 1.6.0 doesn't fully support .tftest.hcl files.
Upgrading to 1.9.0 for proper terraform test command support.

Changes:
- test.yml: 1.6.0 -> 1.9.0
- provision.yml: 1.6.0 -> 1.9.0
- <a href="https://github.com/ksysoev/cloudlab/commit/36dce31f32a47854c855eea1ccf8a44b96ead225">36dce31</a>: fix: test workflow running twice on PRs

Remove push trigger to avoid duplicate runs on PR branches.
Workflow now only runs on pull_request events targeting main branch.
- <a href="https://github.com/ksysoev/cloudlab/commit/be8ac9caf3928d02e7b41867c44ef9feb85e9353">be8ac9c</a>: fix: format terraform files

Run terraform fmt -recursive to fix formatting issues in droplet.tf


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>