# Windows Kiosk Single APP with Shell Launcher

This repository contains an example of a Windows Shell Launcher configuration for a single-app kiosk using Shell Launcher v2 and Microsoft Edge in kiosk mode.

## File: `singleAppShell.xml`

### XML Structure and Steps

- **Root Element**: `<ShellLauncherConfiguration>`
  - Declares the XML namespace for Shell Launcher configuration.

- **Profiles**: `<Profiles>`
  - Contains all shell profiles.
  - **DefaultProfile**: Sets the default shell to Windows Explorer (`explorer.exe`).
  - **Profile**: Custom profile with a unique `Id`.
    - **Shell**: Defines the shell as Microsoft Edge in kiosk mode, opening a specific URL in fullscreen. Includes parameters:
      - `--kiosk`: Launches Edge in kiosk mode.
      - `--edge-kiosk-type=fullscreen`: Sets fullscreen mode.
      - `--kiosk-idle-timeout-minutes=2`: Sets idle timeout.
      - `V2:AppType="Desktop"`: Specifies the app type.
      - `V2:AllAppsFullScreen="true"`: Forces all apps to run fullscreen.
    - **ReturnCodeActions**: Defines actions based on the shell's exit code:
      - `0`: Restart the shell.
      - `-1`: Restart the device.
      - `255`: Shutdown the device.
    - **DefaultAction**: Action if no return code matches (restarts shell).

- **Configs**: `<Configs>`
  - Associates user accounts with profiles.
  - **Config**: Each config block links an account to a profile.
    - `<AutoLogonAccount/>`: Uses the default auto-logon account.
    - `<Account Name="cloudinfocus"/>`: Local account.
    - `<Account Name="azuread\adelev@lab.cloudinfocus.com.br"/>`: Microsoft Entra (Azure AD) account.
    - `<Profile Id="..."/>`: Links the account to the custom profile.

## How to Use

1. Edit the XML as needed for your environment (URL, accounts, etc).
2. Apply the configuration using Windows Shell Launcher tools or MDM.
3. The specified accounts will launch Edge in kiosk mode as their shell.

---

For more details, see the [Microsoft Shell Launcher documentation](https://learn.microsoft.com/en-us/windows/configuration/kiosk-shelllauncher).
