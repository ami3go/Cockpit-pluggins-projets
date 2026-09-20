# Awesome Cockpit Projects

> A curated list of useful Cockpit plugins, extensions, homelab tools, and related projects.

This repository is intended to be a practical **Awesome-style list**: projects are grouped by purpose and each entry explains why it is useful in a Cockpit-based environment.

## Contents

- [Dashboards & Navigation](#dashboards--navigation)
- [Repository Management](#repository-management)
- [Power, UPS & Recovery](#power-ups--recovery)
- [Related Projects](#related-projects)
- [Contributing](#contributing)

## Legend

- 🟢 **Ready to use** — suitable for normal use based on its documented project status.
- 🟡 **Pre-release / evaluate first** — useful, but still has documented release or hardware-validation work outstanding.
- 🔵 **Reference / code reuse** — especially useful as an implementation reference for other Cockpit projects.

## Dashboards & Navigation

### [Cockpit Bookmarks](https://github.com/ami3go/bookmarks) 🟢

Lightweight Cockpit extension for organizing and launching web services hosted on a server or mini PC.

**Why it is useful**

- React + PatternFly Cockpit interface with light/dark theme support.
- Search, groups, favorites, tags, multiple endpoints, and service reachability indicators.
- Can discover local TCP listeners and propose web services to add.
- Configuration import/export, automatic history, and rollback of recent configuration snapshots.
- Runtime is static HTML/CSS/JavaScript served by Cockpit; no Docker, daemon, database, Node.js, or Python runtime is required.

**Useful as reference for:** Cockpit UI structure, PatternFly integration, privileged configuration writes, configuration history/rollback, service discovery, Debian packaging, and release CI.

## Repository Management

### [ghsync](https://github.com/ami3go/ghsync) 🟢 🔵

GitHub repository synchronizer that can clone and keep repositories up to date from a terminal TUI, scheduled jobs, or a Cockpit page.

**Why it is useful**

- Uses the GitHub CLI to synchronize repositories for users or organizations.
- Fast-forward-only updates avoid overwriting dirty or diverged repositories.
- Detects unpushed work, orphaned clones, detached states, and other repository problems.
- Supports partial clones, bare mirrors, retries, parallel operations, and locking against overlapping runs.
- Provides a Cockpit page for repositories, statistics, activity, settings, and scheduling.
- Supports cron and persistent systemd timers for unattended synchronization.

**Useful as reference for:** Cockpit-to-CLI integration, background scheduling, GitHub CLI automation, systemd timers, safe repository synchronization, logging, and lightweight Cockpit pages without a build-time framework dependency at runtime.

## Power, UPS & Recovery

### [cockpit-ups-wol](https://github.com/ami3go/cockpit-ups-wol) 🟡 🔵

Homelab UPS-management appliance built around Network UPS Tools (NUT), a persistent safety agent, Wake-on-LAN, and Cockpit.

**Why it is useful**

- Coordinates deterministic shutdown and recovery of Linux, Synology DSM, and other managed hosts.
- Persists outage state so recovery can continue safely after a reboot or interrupted boot.
- Uses recovery gates for utility stability, UPS charge/runtime, network readiness, and health.
- Required services automatically start after reboot and the stack includes continuous health checks with bounded safe repair behavior.
- Project-managed configuration changes are transactional and can automatically fall back to a last-known-good configuration.
- Includes Cockpit management, Wake-on-LAN recovery, NUT integration, multi-architecture builds, and extensive CI acceptance tests.

**Project status:** pre-release. The documented v0.1 software baseline is implemented, but representative physical UPS/DSM acceptance and the project-license decision are still outstanding.

**Useful as reference for:** resilient Cockpit appliances, power-failure state machines, NUT integration, transactional configuration, rollback, health checks, automatic recovery, systemd watchdog integration, and safe boot-after-power-loss handling.

### [USB-UPS-Simulator](https://github.com/ami3go/USB-UPS-Simulator) 🔵

USB HID UPS simulator for NUT testing, using an Arduino Leonardo/ATmega32U4 as the simulated UPS and a W5500 Ethernet interface as an independent control channel.

**Why it is useful**

- Presents a USB HID Power Device that can be consumed by NUT's `usbhid-ups` driver.
- Lets automated tests inject mains failure, battery charge/runtime, load, input/output voltage, low-battery, overload, replacement-battery, and shutdown conditions without disconnecting the USB UPS interface.
- Provides TCP control through the W5500 on port 5000 plus a `Serial1` UART fallback.
- Includes an explicit `ARM ON` gate and `RESET` / `ARM OFF` safe-state recovery before state-changing tests.
- Provides a Python API and `ups-sim` CLI for automated test scenarios.
- CI verifies the Arduino simulator build and Python driver on multiple Python versions.

**Useful with `cockpit-ups-wol`:** hardware-in-the-loop and NUT-facing fault injection for repeatable outage, low-battery, recovery-gate, shutdown, reboot, and restoration testing before running equivalent scenarios against a real UPS.

**Useful as reference for:** USB HID UPS emulation, NUT `usbhid-ups` compatibility, controlled fault injection, Python-driven hardware testing, Ethernet/UART test control, and safety-gated power-management test infrastructure.

## Related Projects

Projects that are not necessarily Cockpit plugins themselves but provide implementations, ideas, or components worth evaluating for reuse should be collected here and moved into more specific categories as the list grows.

## Contributing

When adding a project:

1. Put it in the most relevant category.
2. Link to the upstream project rather than copying it into this repository.
3. Add a concise description of what it does.
4. Explain why it is useful for Cockpit or homelab management.
5. Note important project-status, maintenance, security, licensing, or hardware-validation limitations when known.
6. Prefer curated, useful entries over an exhaustive link dump.

---

Contributions and suggestions for useful Cockpit-related projects are welcome.
