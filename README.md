# Ditana Core Dump Configuration

The `ditana-config-coredumps` package is included by default in the [Ditana GNU/Linux distribution](https://ditana.org). It serves to disable core dumps, thereby mitigating the risk of exposing sensitive information in multi-user environments or in the event of a system compromise. Users have the flexibility to enable or disable this package during installation or at runtime. Changes take effect after a system reboot.

## Features

- **Default Behavior**: Core dumps are disabled to enhance system security.
- **User Control**: Users can opt-out during installation or toggle the package at runtime via the package manager. A system reboot is required for changes to take effect.
- **Selective Activation**: Core dumps can be temporarily enabled for specific services or user sessions when necessary.

## Implementation Details

Core dumps are restricted through two distinct mechanisms:

### 1. Systemd Services

Core dumps for systemd-managed services are controlled via the configuration file:

```
/etc/systemd/system.conf.d/50-ditana-limits.conf
```

This file sets the `DefaultLimitCORE` parameter to `0`, effectively disabling core dumps for all services by default.

**To Enable Core Dumps for a Specific Service:**

1. Create an override configuration for the desired service:

   ```bash
   sudo systemctl edit <service-name>
   ```

2. In the editor that opens, add the following lines:

   ```
   [Service]
   LimitCORE=infinity
   ```

3. Save and exit the editor.

4. Reload the systemd configuration:

   ```bash
   sudo systemctl daemon-reload
   ```

This will allow core dumps for the specified service until the override is removed.

### 2. Non-Systemd Contexts

For non-systemd environments, core dumps are managed via the configuration file:

```
/etc/security/limits.d/50-ditana.conf
```

This file sets a soft limit of `0` for core dumps, preventing their creation in regular user sessions.

**To Enable Core Dumps for a User Session:**

Execute the following command in the active shell session:

```bash
ulimit -c unlimited
```

This lifts the restriction for the current session, allowing core dumps to be generated as needed for debugging purposes.

## Installation and Removal

The `ditana-config-coredumps` package can be managed through the Ditana package repository. Users can install or uninstall the package at any time using the package manager. A system reboot is required after installation or removal to apply the changes.
