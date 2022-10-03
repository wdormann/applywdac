# ApplyWDACPolicy

applywdac.ps1 is a PowerShell script for applying WDAC policies, such as [Microsoft recommended driver block rules](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules). This script is designed for use on systems that do **NOT** currently have WDAC policies and associated management tools in place. If you are already using WDAC, you should merge WDAC policies using whichever 

## Installation

If you have the ability to run stand-along PowerShell scripts, simply run the `.\applywdac.ps1` script from a PowerShell prompt that is running with administrative privileges. Alternatively, you can paste the contents of `.\applywdac.ps1` into a PowerShell prompt that is running with administrative privileges and subsequently run `ApplyWDACPolicy` with the appropriate arguments.

## Usage

```
# Import `blockeddrivers.xml` in whatever mode it specifies. e.g. the [Microsoft recommended driver block rules](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/microsoft-recommended-driver-block-rules) are in audit mode by default.
PS> .\applywdac.ps1 -xmlpolicy blockeddrivers.xml

# Import `blockeddrivers.xml`, stripping out any "audit" options (therefore applying it in "enforcing" mode)
PS> .\applywdac.ps1 -xmlpolicy blockeddrivers.xml -enforce

# Same as above, but in "paste into PowerShell mode"
PS> <paste applywdac.ps1 contents into PowerShell>
PS> ApplyWDACPolicy -xmlpolicy blockeddrivers.xml -enforce
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[BSD](https://choosealicense.com/licenses/bsd-2-clause/)