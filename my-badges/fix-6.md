<img src="https://my-badges.github.io/my-badges/fix-6.png" alt="I did 6 sequential fixes." title="I did 6 sequential fixes." width="128">
<strong>I did 6 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/ksysoev/cloudlab/commit/cc8192680ec05a9071ab507565830ab244bc0455">cc81926</a>: fix: add alloy user and environment setup (#12)
- <a href="https://github.com/ksysoev/cloudlab/commit/05cf72f02ce5baa1ee71a44c711d0ca71a73fb50">05cf72f</a>: fix: install Alloy as systemd service instead of Docker container (#11)

Changed from Docker-based Alloy deployment to native systemd service:

Why This Change:
- Running Alloy in Docker caused intermittent data collection issues
- Host metrics and logs are more reliable when collected from host
- Systemd service is more stable and easier to monitor
- No container overhead or network namespace issues

Changes Made:
1. Removed Docker Compose file for Alloy container
2. Removed Alloy deployment from init-swarm.sh script
3. Changed config path from /opt/cloudlab/alloy/config.alloy to /etc/alloy/config.alloy
4. Added Grafana Alloy installation from official apt repository
5. Configured Alloy to run as systemd service

Benefits:
- Direct access to host system metrics (no container isolation)
- Direct access to Docker socket without volume mounts
- Automatic startup with systemd
- Better logging via journald
- More reliable and consistent data collection

The Alloy configuration remains the same, just the deployment method changed.
- <a href="https://github.com/ksysoev/cloudlab/commit/1bc8c6ea6d858a58b18f1b0970c194173b0503bd">1bc8c6e</a>: fix: complete Alloy config with discovery.relabel and prometheus.relabel (#10)

Updated Alloy configuration to match the working setup from pet-house:

1. Added discovery.relabel for proper metric labeling:
   - Sets instance and job labels for node exporter
   - Sets container and stream labels for Docker logs

2. Added prometheus.relabel for metric filtering:
   - Keeps only essential system metrics to reduce data volume
   - Filters metrics like CPU, memory, disk, network

3. Updated loki.source.docker:
   - Now uses discovery.relabel rules for proper log labeling
   - Adds job, instance, container, and stream labels

4. Renamed components to match standard naming:
   - prometheus.remote_write.metrics_service
   - loki.write.grafana_cloud_loki
   - More descriptive component names

5. Enhanced prometheus.exporter.unix configuration:
   - Added filesystem filters to exclude virtual filesystems
   - Added netdev/netclass filters to exclude virtual interfaces
   - Disabled unnecessary collectors (ipvs, btrfs, xfs, zfs)

This matches the proven configuration from the working droplet.
- <a href="https://github.com/ksysoev/cloudlab/commit/0a4dc18b4d45bd378897489ca9e46ca1eda02173">0a4dc18</a>: fix: add prometheus.scrape block to connect unix exporter to remote_write (#9)

* fix: move Alloy config from /tmp to /opt/cloudlab/alloy to survive reboot

The config file was in /tmp/ which gets cleared on reboot, causing
Alloy container to fail with 'bind source path does not exist' error.
Moving to /opt/cloudlab/alloy/ which persists across reboots.

* fix: add prometheus.scrape block to connect unix exporter to remote_write

The Alloy configuration was missing a critical prometheus.scrape component
that connects the prometheus.exporter.unix to prometheus.remote_write.

Without this scrape block, the unix exporter was running but no metrics
were being collected and forwarded to Grafana Cloud.

This change adds the missing scrape configuration that:
- Scrapes metrics from prometheus.exporter.unix.default.targets
- Forwards them to prometheus.remote_write.default.receiver
- <a href="https://github.com/ksysoev/cloudlab/commit/dd4e57d03261fe0bc3dc74cdcc3f2b1f9cae169b">dd4e57d</a>: fix: move Alloy config from /tmp to /opt/cloudlab/alloy to survive reboot (#8)

The config file was in /tmp/ which gets cleared on reboot, causing
Alloy container to fail with 'bind source path does not exist' error.
Moving to /opt/cloudlab/alloy/ which persists across reboots.
- <a href="https://github.com/ksysoev/cloudlab/commit/8e954ad63534c041827d84972bf3539c75931162">8e954ad</a>: fix: move SSH/UFW config before Docker install and add reboot after cloud-init (#7)

- Move SSH port change and UFW to the start of runcmd so SSH is
  reachable even if Docker install fails
- Add apt lock wait before Docker install to prevent contention with
  package_update/package_upgrade running in the background
- Add power_state reboot at end of cloud-init to cleanly apply kernel
  upgrades from package_upgrade


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>