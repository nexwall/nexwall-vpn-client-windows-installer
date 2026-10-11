# Nexwall VPN for Windows - installer (branded fork of openvpn-build)

Public fork of [openvpn-build](https://github.com/OpenVPN/openvpn-build) (GPLv2). It builds the MSI that bundles
OpenVPN (unmodified upstream, `src/openvpn`) and the **branded GUI** from
[`nexwall-vpn-client-windows`](https://github.com/nexwall/nexwall-vpn-client-windows) (`src/openvpn-gui`).

## Changes compared to upstream (phase 1)
- `src/openvpn-gui` submodule points to the Nexwall fork (pinned commit) instead of OpenVPN/openvpn-gui.
- New MSI `UpgradeCode`s (x86, amd64, arm64) so this package can never "upgrade"/replace an official OpenVPN install.
- `PRODUCT_PUBLISHER` = "Nexwall (based on OpenVPN)".

## Known limits of phase 1 (to be done and tested on a real Windows machine)
- `PRODUCT_NAME` stays `OpenVPN`: it also drives the registry key `HKLM\SOFTWARE\OpenVPN`, the install folder and
  the service names used by OpenVPN GUI and the OpenVPN services. Start-menu shortcut labels and the Add/Remove Programs
  name therefore still say "OpenVPN". Renaming needs a coordinated change of the GUI, the services and this installer.
- The MSI shares file paths and service names with the official OpenVPN: do not install both on one machine.
- CI builds an unsigned MSI unless the signing secrets (see `.github/workflows/build.yaml`) are configured.
