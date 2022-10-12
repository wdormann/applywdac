# ApplyWDACPolicy

`applywdac.ps1` is a PowerShell script for applying WDAC policies,
such as the [Microsoft recommended driver block
rules](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules).
This script is designed for use on systems that do **NOT** currently
have WDAC policies and associated management tools in place. If you
are already using WDAC, you should merge WDAC policies using whichever
tools and methods you already have in place. The target audience of
this script are those who want to be able to apply WDAC rules easily,
without requiring extensive knowledge of WDAC.

## Installation

If you have the ability to run stand-along PowerShell scripts, simply
run the `.\applywdac.ps1` script from a PowerShell prompt that is
running with administrative privileges. Alternatively, you can paste
the contents of
[applywdac.ps1](https://raw.githubusercontent.com/wdormann/applywdac/main/applywdac.ps1)
into a PowerShell prompt that is running with administrative
privileges and subsequently run `ApplyWDACPolicy` with the appropriate
arguments. Just be sure to use **`Ctrl+V` on your keyboard** to do the
pasting, as pasting via right-click or even the edit menu at the top
will interpret pasted content on a line-by-line basis as opposed to in
block mode.

## Usage

```
# Import `blockeddrivers.xml` in whatever mode it specifies. e.g. the [Microsoft recommended driver block rules](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules) are in audit mode by default.
PS> .\applywdac.ps1 -xmlpolicy blockeddrivers.xml

# Import `blockeddrivers.xml`, stripping out any "audit" options (therefore applying it in "enforcing" mode)
PS> .\applywdac.ps1 -xmlpolicy blockeddrivers.xml -enforce

# Same as above, but in "paste into PowerShell mode"
PS> <paste applywdac.ps1 contents into PowerShell>
PS> ApplyWDACPolicy -xmlpolicy blockeddrivers.xml -enforce

# "paste into PowerShell mode" automatically download and install compiled policy binary from Microsoft
PS> <paste applywdac.ps1 contents into PowerShell>
PS> ApplyWDACPolicy -auto -enforce
```

Pre-Windows-1903 example usage:
![Windows Server 2016](applywdac-2016.png)

Windows 1903 or later example usage:
![Windows Server 2016](applywdac-modern.png)

Automatic download from Microsoft example usage, "paste into PowerShell" invocation:
![Windows Server 2016](applywdac-auto.png)

## HVCI Notes

If you apply the [Microsoft recommended driver block
rules](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules),
you may end up with
[HVCI](https://learn.microsoft.com/en-us/windows/security/threat-protection/device-guard/enable-virtualization-based-protection-of-code-integrity)
enabled on your system. While HVCI is an excellent mitigation against
attacks and it should be used on every platform that can support it,
there can be some edge cases where HVCI can interfere with the ability
to use a system as intended. For example, a machine with VMware
Workstation is installed and nested virtualization features are
needed. In such cases, it may be necessary to disable HVCI to regain
the ability to use the VMware Workstation native hypervisor. VMware
has provided [instructions for how this can be
accomplished](https://kb.vmware.com/s/article/2146361).

Note that driver blocking with WDAC will still function as expected,
even when HVCI is disabled.

## Contributing Pull requests are welcome. For major changes, please
open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[BSD](https://choosealicense.com/licenses/bsd-2-clause/)
