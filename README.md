# WebAuthnLinux (WebDevAuthn Derivative)

> [!NOTE]
> This fork extends WebDevAuthn into a Linux software Passkey authenticator with:
>
> - Linux fingerprint verification through Native Messaging
> - WebAuthn credential management (view, rename, and delete stored credentials)
> - Persistent credential storage
> - Firefox and Chrome/Chromium support
>
> Current Version: **1.0.0-Alpha**

---

## Biometric Support

WebAuthnLinux uses the Linux fingerprint stack through the native messaging host.

Tested with:

- `fprintd`
- `open-fprintd`
- `python-validity` fingerprint drivers

The native messaging host communicates with the fingerprint service to provide biometric user verification during WebAuthn authentication.

## Current Status

WebAuthnLinux is an experimental Linux software authenticator based on WebDevAuthn that enables browser Passkey registration and authentication using local system biometric verification.

Tested successfully with:

- GitHub
- Google
- Microsoft
- Government tax reporting websites
- webauthn.io
- Proton.me

Test environments:

- Fedora Linux
- Kubuntu Linux

Browsers tested:

- Firefox (APT and DNF)
- Chrome/Chromium (APT and DNF)
- (Snap and Flatpack installations haven't been tested.  Please report any issues with these.)

## Installation

Clone this repository:

```bash
git clone https://github.com/Karloss1234/WebAuthnLinux.git
cd WebAuthnLinux
```

### 1. Load the extension (Temporary load instructions)

WebAuthnLinux extension is currently installed as an unpacked extension at `WebAuthnLinux/extension/`.

#### Firefox

1. Open:
```
about:debugging#/runtime/this-firefox
```
2. Select **Load Temporary Add-on**.
3. Browse to the `extension/` directory.
4. Select: `manifest.json`
5. In Extensions menu select `Pin to Toolbar` (Optional)

#### Chrome / Chromium

1. In `extension/` directory, rename `manifest.chrome.json` to `manifest.json`.
2. Open:
```
chrome://extensions
```
3. Enable **Developer mode**.
4. Select **Load unpacked**.
5. Browse to and Select the `extension/` directory
6. In Extensions menu select `Pin to Toolbar` (Optional)

### 2. Install the native messaging host (Allows the browser extension to communicate with the Linux fingerprint reader, fprintd.):

For firefox:
```bash
cd native
./install.sh --firefox
```
For Chrome/Chromium:

```bash
cd native
./install.sh --chrome <ID assigned to the unpacked extension by Chrome>
```
The installer will:

- Install the native messaging host script.
- Create the required native messaging manifest.
- Configure communication between the browser extension and the Linux fingerprint service.
- Manual creation of the native messaging host JSON file is not required.

## Improvements in WebAuthnLinux 1.0.0-Alpha

### Credential management

- Added improved credential storage handling and persistence.
- Improved loading and saving of `system_credentials` through browser storage.
- Added reliable credential retrieval after extension restart.
- Improved handling of stored credential metadata.
- Added credential management operations including renaming and deleting credentials.

### Authenticator reliability

- Improved authenticator initialisation and state handling.
- Improved asynchronous storage operations using modern Promise/async patterns.
- Reduced the risk of credential storage inconsistencies.
- Improved handling of authenticator state across browser sessions.

### WebAuthn compatibility

- Improved authenticator metadata handling, including AAGUID management.
- Improved compatibility with browser WebAuthn flows.
- Maintained compatibility with existing WebAuthn registration and authentication processes.

### Native messaging installation improvements

- Simplified native host installation.
- Removed the need for users to manually create the native messaging manifest.
- Added support for different Firefox configuration paths used by distributions such as Fedora.
- Improved installer verification output.

### Debugging and development

- Added additional logging around credential operations and storage events.
- Improved visibility of authenticator state transitions during testing.

## Compatibility

Existing registered credentials are expected to remain usable.


# **PREVIOUS CONTENT**

# WebAuthnLinux (WebDevAuthn Derivative)

> [!NOTE]
> This fork (**WebAuthnLinux**) extends the original tool with **Native Messaging support for Linux Fingerprint integration**.
> Current Version: **1.0.0-Alpha**

___

### Description

This project enables **Linux System Integration** for WebAuthn/FIDO2. It features a Python-based Native Messaging Host that bridges the gap between the browser and the Linux system's biometric services (via `fprintd`).

This allows the extension to leverage your laptop's built-in fingerprint reader for user verification events, bypassing the need for external hardware or specific web services.

### Key Features

- **Linux Fingerprint Integration**: Use `fprintd` for biometric authentication directly in the browser.
- **Native Messaging Support**: Secure communication between the extension and the local system.
- **Multi-Browser Compatibility**: Installation script supports **Chrome**, **Chromium**, and **Firefox**.
- **Manifest V3**: Modern extension architecture for improved security and performance.
- **Dynamic Security**: Uses a unique, dynamically generated 256-bit master key and unique installation salts (no hardcoded secrets).
- **Hardware Agnostic**: Designed to bridge system biometrics for development, even on systems where the browser doesn't natively expose the fingerprint reader as a "platform" authenticator.

### Quick Setup

1. **System Dependencies**: Ensure `fprintd` and `python3` are installed and configured.
2. **Setup Extension**: Sideload the `extension/` folder in your browser (`chrome://extensions` for Chrome/Chromium).
3. **Install Native Host**:
   ```bash
   cd native
   ./install.sh
   ```

For detailed, browser-specific instructions, see [LINUX_SETUP.md](LINUX_SETUP.md).

### Project Structure

- **`extension/`**: The Web Extension source code (Manifest V3). Includes logic for triggering native messaging and handling biometric responses.
- **`native/`**: Python-based Native Messaging Host (`webauthnlinux_host.py`) and multi-browser installer (`install.sh`).

___

### Contact & Hosting

This derivative work is hosted at [https://github.com/samveen/WebAuthnLinux](https://github.com/samveen/WebAuthnLinux)

The original work can be found by navigating to this fork's parent.

Modified by [Samveen](https://github.com/samveen), largely thanks to [AntiGravity](https://antigravity.google)

The Derivative Work is Copyright (c) 2026 Onwards, Projects by Samveen.

The Copyright of all unmodified work remains Copyright (c) The Original Authors.

___

# **ORIGINAL CONTENT**

# WebDevAuthn
A tool to test &amp; analyze FIDO2/WebAuthn requests and responses

 - WebDevAuthn Web Tool: https://gramthanos.github.io/WebDevAuthn/
 - Chrome Extension: https://chrome.google.com/webstore/detail/webdevauthn/aofdjdfdpmfeohecddhgdjfnigggddpd
 - Firefox Extension: https://addons.mozilla.org/firefox/addon/webdevauthn/

___

### Description

WebDevAuthn is a web tool for testing and analyzing [FIDO2/WebAuthn](https://en.wikipedia.org/wiki/WebAuthn) requests and responses. The web application can work as a playground, letting developers experiment and understand the WebAuthn internals while also allowing the testing and experimentation of FIDO2 authenticator devices. Furthermore, developers may use this tool's injector (embedded code or an extension) to hijack WebAuthn calls and analyse them. The tool also features an advanced virtual authenticator that can emulate WebAuthn responses.

This repository is part of the research conducted for the papers:
- A web tool for analyzing FIDO2/WebAuthn Requests and Responses [https://doi.org/10.1145/3465481.3469209](https://doi.org/10.1145/3465481.3469209)
- Blind software-assisted conformance and security assessment of FIDO2/WebAuthn implementations [https://doi.org/10.22667/JOWUA.2022.06.30.096](https://doi.org/10.22667/JOWUA.2022.06.30.096)

Analyser Features:
- Capture WebAuthn requests
- Analyse WebAuthn options (show info, warnings & errors)
- Unpack/Decode WebAuthn authenticator responses
- Virtual Authenticator Device (for custom responses)

Virtual Authenticator Device:
- OS independent
- Supports packed attestation
- Supports wrapped keys to credentials ID
- Access to the private key of the generated credentials
- Testing mode to assess implementations
- Multiple supported algorithms

___


### Contact me

Please feel free to contact me to leave me your feedback or to express your thoughts.

You can [open an issue](https://github.com/GramThanos/WebDevAuthn/issues) or [send me a mail](mailto:gramthanos@gmail.com)

___


### About

This web application was developed as part of my thesis for the postgraduate programme "Digital Systems Security" and research conducted as part of the [Systems Security Laboratory](https://laboratories.ds.unipi.gr/ssl/)

[University of Piraeus](https://www.unipi.gr/), [Department of Digital Systems](https://www.ds.unipi.gr/), Digital Systems Security

Copyright (c) 2021-2025 Grammatopoulos Athanasios-Vasileios

___

[![GramThanos](https://avatars2.githubusercontent.com/u/14858959?s=42&v=4)](https://github.com/GramThanos)
