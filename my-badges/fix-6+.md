<img src="https://my-badges.github.io/my-badges/fix-6+.png" alt="I did 7 sequential fixes." title="I did 7 sequential fixes." width="128">
<strong>I did 7 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/4cf55a16a920a37c5550fdbd2ff5387e0615bfc1">4cf55a1</a>: Fix final Molecule test failures

- Docker role: Skip service start in Molecule tests (Docker-in-Docker not supported)
- Docker role: Fix line length linting issue in GPG dearmor command
- Monitoring role: Remove recurse flag from directory creation for idempotence
- <a href="https://github.com/ksysoev/cloudlab/commit/9f85450b1efc794ba736eefc211fc7c086dfd305">9f85450</a>: Fix GPG key dearmoring for Docker and Monitoring roles

- Add gnupg installation to prepare playbooks for molecule tests
- Download GPG keys to temp location and dearmor them
- Docker role: Dearmor Docker GPG key before use
- Monitoring role: Dearmor Grafana GPG key before use
- Creates prepare.yml for docker role tests
- <a href="https://github.com/ksysoev/cloudlab/commit/0138780f88aa3dea2c98bb0a51d2f6671018d8b0">0138780</a>: Fix remaining Molecule test failures

- Replace deprecated apt_key with get_url for GPG keys (fixes gpg-agent errors)
- Remove UFW reset to ensure idempotence in security role
- Docker role: Use get_url for Docker GPG key
- Monitoring role: Use get_url for Grafana GPG key
- <a href="https://github.com/ksysoev/cloudlab/commit/8a8141425887dfe94d079c7765339f9f9ba82446">8a81414</a>: Fix ANSIBLE_ROLES_PATH to use correct parent directory

- Change from ${MOLECULE_PROJECT_DIRECTORY}/../../ to ${MOLECULE_PROJECT_DIRECTORY}/../
- MOLECULE_PROJECT_DIRECTORY points to ansible/roles/{role}, so ../ correctly resolves to ansible/roles/
- <a href="https://github.com/ksysoev/cloudlab/commit/94cd308f3e463f458149b8f282f612d16148e1ef">94cd308</a>: Fix Molecule role resolution using ANSIBLE_ROLES_PATH environment variable

- Use ANSIBLE_ROLES_PATH with ${MOLECULE_PROJECT_DIRECTORY}/../../ to set absolute roles path
- Previous relative path approach (roles_path: ../../../) was not working correctly
- Environment variable approach is more reliable for Molecule tests
- <a href="https://github.com/ksysoev/cloudlab/commit/a1ebb71478084bf5fe533d50fab36f0816965b95">a1ebb71</a>: Fix Molecule role resolution by configuring roles_path in all roles

- Add roles_path: ../../../ to provisioner config in all molecule.yml files
- Revert converge.yml files to use explicit role names instead of MOLECULE_PROJECT_DIRECTORY lookup
- This ensures Molecule can find roles when running tests from within role directories
- <a href="https://github.com/ksysoev/cloudlab/commit/7ba63b8954cdf9c4c688b9ecf42d0abe6a3728a0">7ba63b8</a>: Fix Molecule role paths to use MOLECULE_PROJECT_DIRECTORY

Molecule runs from within the role directory, so it can't find roles by name.
Use the MOLECULE_PROJECT_DIRECTORY environment variable to reference the role
dynamically, which works regardless of the role name.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>