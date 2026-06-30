# Host Inventory

Collected from `wbm-cogs-01` on 2026-06-30 UTC.

This inventory summarizes local command output from the VM. It intentionally excludes secrets, private keys, tokens, environment-variable values, and credential material.

## Host Summary

| Item | Value |
| --- | --- |
| Hostname | `wbm-cogs-01` |
| Operating system | Ubuntu 24.04.4 LTS (Noble Numbat) |
| Kernel | `Linux 6.8.0-124-generic` |
| Architecture | `x86_64` |
| Virtualization | KVM guest detected by `hostnamectl` and `systemd-detect-virt`; QEMU hardware model |
| Current administrative user | `mediacontrol` (`uid=1000`, primary group `mediacontrol`) |
| Administrative groups | `sudo`, `adm`, `docker`, `lxd`, `plugdev`, `dip`, `cdrom` |

## Compute Allocation

| Resource | Allocation |
| --- | --- |
| vCPUs | 8 online CPUs (`0-7`) |
| CPU model | Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz |
| Topology reported to guest | 2 sockets, 4 cores per socket, 1 thread per core |
| Memory | 15 GiB total, 14 GiB available at collection time |
| Swap | 4.0 GiB swap file at `/swap.img`, 0 used at collection time |

## Storage, Filesystems, and Mounts

### Block Devices

| Device | Type | Size | Filesystem / role | Mount |
| --- | --- | ---: | --- | --- |
| `/dev/sda` | disk | 128G | VM disk | Not mounted directly |
| `/dev/sda1` | partition | 1M | BIOS / boot metadata partition | Not mounted |
| `/dev/sda2` | partition | 1G | ext4 boot filesystem | `/boot` |
| `/dev/sda3` | partition | 127G | LVM physical volume | Backing `ubuntu-vg` |
| `/dev/mapper/ubuntu--vg-ubuntu--lv` | LVM logical volume | 63.5G | ext4 root filesystem | `/` |

The LVM physical volume is larger than the active root logical volume. Locally available command output did not include volume group free-space details. Requires operator confirmation.

### Filesystem Capacity

| Mount | Source | Type | Size | Used | Available | Use |
| --- | --- | --- | ---: | ---: | ---: | ---: |
| `/` | `/dev/mapper/ubuntu--vg-ubuntu--lv` | ext4 | 63G | 29G | 31G | 49% |
| `/boot` | `/dev/sda2` | ext4 | 974M | 200M | 707M | 23% |
| `/mnt/storage` | `192.168.1.150:/mnt/wbm-storage-01/storage` | nfs | 29T | 23T | 6.1T | 79% |
| `/run` | `tmpfs` | tmpfs | 1.6G | 1.2M | 1.6G | 1% |
| `/dev/shm` | `tmpfs` | tmpfs | 7.8G | 12K | 7.8G | 1% |
| `/run/user/1000` | `tmpfs` | tmpfs | 1.6G | 12K | 1.6G | 1% |

Snap loopback mounts are present for `core18`, `core20`, `lxd`, and `snapd`.

### Configured but Not Mounted

`/etc/fstab` includes `192.168.1.6:/mnt/NAS01/media` configured for `/mnt/nas01` over NFSv3. The directory exists locally, but it was not mounted when this inventory was collected.

## Network

### Interfaces

| Interface | State | Addresses |
| --- | --- | --- |
| `lo` | UNKNOWN | `127.0.0.1/8`, `::1/128` |
| `ens18` | UP | `192.168.1.23/24`, `fe80::be24:11ff:fe80:77ae/64` |
| `docker0` | DOWN | `172.17.0.1/16` |
| `br-9aaa99e13644` | UP | `172.18.0.1/16`, `fe80::a4ea:5dff:feb5:cb22/64` |
| `vetheed933f@if2` | UP | `fe80::30f8:4dff:fefc:9f79/64` |

### Routing and DNS

| Item | Value |
| --- | --- |
| Default route | `default via 192.168.1.1 dev ens18 proto static` |
| Connected LAN route | `192.168.1.0/24 dev ens18 src 192.168.1.23` |
| Docker routes | `172.17.0.0/16` on `docker0`; `172.18.0.0/16` on `br-9aaa99e13644` |
| DNS resolver | `systemd-resolved` stub at `127.0.0.53` |
| Upstream DNS for `ens18` | `192.168.1.5`, `1.1.1.1` |
| Current DNS server | `1.1.1.1` |

External DNS records, DHCP reservations, firewall policy, and upstream network ownership: Requires operator confirmation.

## Docker and Compose

| Item | Status |
| --- | --- |
| Docker binary | Installed at `/usr/bin/docker` |
| Docker version | Docker 29.5.2, build `79eb04c` |
| Docker service | `enabled` and `active` |
| Docker storage driver | `overlayfs` |
| Docker cgroup driver | `systemd` |
| Docker cgroup version | `2` |
| Docker Compose | Docker Compose v5.1.4 |

Running containers at collection time:

| Container | Image | Status | Ports |
| --- | --- | --- | --- |
| `513propertyservices-web` | `nginx:1.27-alpine` | Up 3 days, healthy | `0.0.0.0:80->80/tcp`, `[::]:80->80/tcp` |

## Running Services

Relevant running system services reported by `systemctl`:

| Service | Purpose |
| --- | --- |
| `containerd.service` | Container runtime |
| `docker.service` | Docker engine |
| `ssh.service` | OpenSSH server |
| `fail2ban.service` | Login protection / ban management |
| `squid.service` | Squid web proxy |
| `cron.service` | Scheduled task runner |
| `rsyslog.service` | System logging |
| `systemd-networkd.service` | Network configuration |
| `systemd-resolved.service` | DNS resolution |
| `systemd-timesyncd.service` | Time synchronization |
| `rpcbind.service`, `rpc-statd.service` | NFS support |
| `snapd.service` | Snap package manager |
| `unattended-upgrades.service` | Package upgrade shutdown handling |
| `multipathd.service` | Device-mapper multipath controller |

Other standard system services were also running, including `dbus`, `polkit`, `systemd-journald`, `systemd-logind`, `systemd-udevd`, `getty@tty1`, and `user@1000`.

## Backup Indicators

Locally detected backup-related indicators:

| Indicator | Evidence |
| --- | --- |
| Package metadata backups | `/var/backups` contains rotating `dpkg`, `apt`, and `alternatives` backup files. |
| System package backup timer | `dpkg-db-backup.timer` is enabled under systemd timers. |
| LVM metadata backup tools | `/etc/lvm/backup` and `vgcfgbackup` are present. |
| NFS storage backup directories | `/mnt/storage/jakes backup`, `/mnt/storage/migration/media/jakes backup`, `/mnt/storage/migration/media/minecraft_backups`, and `/mnt/storage/minecraft_backups` exist. |

Items that could not be fully determined locally:

- Full-VM backups or hypervisor snapshots: Requires operator confirmation.
- Application data backup scope, retention location, and restore testing: Requires operator confirmation.
- Whether `/mnt/storage` is an intended backup target, primary data mount, or both: Requires operator confirmation.
- Whether the configured but unmounted `/mnt/nas01` NFS mount is intentionally disabled: Requires operator confirmation.
- Recovery point objectives, recovery time objectives, retention policy, and offsite copy status: Requires operator confirmation.

## Unknowns Requiring Operator Confirmation

- Hypervisor host name, cluster, and ownership: Requires operator confirmation.
- Static IP reservation source and DNS record ownership: Requires operator confirmation.
- Firewall rules outside the guest: Requires operator confirmation.
- Complete backup and restore policy: Requires operator confirmation.
- Secrets storage location and restore process: Requires operator confirmation.
- Whether all required production or demo services are represented by the currently running Docker container: Requires operator confirmation.
