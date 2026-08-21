# Dell Latitude 5300 Tahoe stable baseline

## Verified outcome

- macOS Tahoe 26.6.1 / 25G76 installer starts successfully.
- Installation completes using the active `MacBookPro16,2` identity.
- User reports all tested hardware and system functions operating normally after installation.
- The previously observed "macOS Tahoe is not compatible with this Mac" failure no longer occurs.

## Confirmed root cause

The proven hardware configuration was not the cause of the installer rejection. The rejected build exposed `MacBookPro15,4`, which Tahoe's graphical installer did not accept even with `-no_compat_check` and the attempted Board-ID patch. Moving to a complete, internally consistent, Tahoe-supported `MacBookPro16,2` identity resolved the installer gate.

## Active compatibility settings

- `SystemProductName = MacBookPro16,2`
- Complete dedicated SystemSerialNumber, MLB, SystemUUID and ROM identity
- `SecureBootModel = Disabled`
- `Skip Board ID check = Disabled`
- No `-no_compat_check`
- `ipc_control_port_options=0` retained

## Preserved hardware configuration

ACPI, machine-specific USB mapping, UHD620 device properties, VoodooI2C touchpad stack, PS/2 keyboard, IntelMausi Ethernet, BCM94360NG Wi-Fi/Bluetooth stack, storage, battery and power-management configuration remain inherited from the previously stable EFI.

## Deployment and rollback

1. Keep this complete package and a bootable USB copy.
2. Back up the current internal EFI before replacing it.
3. Copy the complete `EFI` directory, not only `config.plist`.
4. Keep `Rollback/Dell-5300-Sequoia-Stable-Original.zip` unchanged for recovery.
5. Do not mix the `MacBookPro15,4` identity values with this `MacBookPro16,2` identity.

This is a frozen, real-machine-verified baseline. Future macOS updates or root patches should be tested from USB before changing the internal EFI.
