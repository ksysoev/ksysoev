<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/623972efcf857ec869756237ac5edeac71144789">623972e</a>: Fix working directory for SSH wait and key configuration steps

Override the default working directory (./ansible) to use root directory
for accessing terraform outputs.
- <a href="https://github.com/ksysoev/cloudlab/commit/c85cc7006628e24f71baba2f70e7b1001e9567ff">c85cc70</a>: Fix Ansible version requirements to use correct package version

The 'ansible' package doesn't have 2.15.x versions. The version
scheme is:
- ansible 8.x includes ansible-core 2.15.x
- ansible 9.x includes ansible-core 2.16.x

Updated requirements.txt to use ansible>=8.0.0,<10.0.0 which provides
the ansible-core 2.15.x - 2.16.x functionality.
- <a href="https://github.com/ksysoev/cloudlab/commit/ff15e9f4c7297718604501c7cc248042ffee8071">ff15e9f</a>: Fix Ansible installation in configure workflow

Use requirements.txt instead of hardcoded version to install Ansible.
The version 2.15.0 doesn't exist as 'ansible==2.15.0' - the correct
approach is to use the version range from requirements.txt which
installs 'ansible>=2.15.0,<3.0'.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>