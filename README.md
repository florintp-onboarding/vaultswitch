# A tool to switch between Vault binaries on MAC ARM64
[![license](http://img.shields.io/badge/license-apache_2.0-red.svg?style=flat)](https://github.com/florintp-onboarding/vaultswitch/blob/main/LICENSE)

## Install the utility script in the default HOMEBREW bin directory
The current repository is used for initial setup and work with a fast Vault binary switch utility.

**Please note**: The script is tested and validated to work on MAC OS on ARM 64 platforms having HOMEBREW as install manager.

## Prerequisites:
* Install and configure [Homebrew](https://brew.sh/)
* Minimal Vault exposure [Vault-Getting-started](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-install?in=vault%2Fgetting-started)


## Install Homebrew (if it is not already present)
1. Install Homebrew from [Homebrew](https://brew.sh/)
* Install and configure [Homebrew direct install](/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Clone this repository
   `gh repo clone florintp-onboarding/vaultswitch`
   
4. Install the script into HOMEBREW/bin directory
   ````
   cd vaultswitch
   chmod +rx vaultswitch
   cp -p vaultswitch /opt/homebrew/bin
   ```` 
### TODO :

  - [x] Validate the Releases by checking the HASHICORP repository
  - [x] Validate the prebuilt binary version
  - [x] Suppress the ECHO if not running in interactive mode.
  - [ ] Check signature of the binary before switch
  - [x] Enclosed code blocks with `{`
  - [x] Added timestamp on actions performed


## Review the default Vault versionand variables
HOMEBREW_CELLAR and HOMEBREW_PATH are by default initialized on Homebrew installation.
If the Homebrew was correctly installed you do not need to update those variable paths.
1. Execute the script without arguments

2. Execute the script vaultswitch with syntax:
   ````
   vaultswitch [ [1.14.4+ent] | [vault_v1.13.4] ]
   ````

- Example 1 ( archive and binary not found ):
   ````
   vaultswitch
   Trying to switch to Vault version 1.15.0
    Working... Downloading... https://releases.hashicorp.com/vault/1.15.0/vault_1.15.0_darwin_arm64.zip Done.
    Unzipping vault_1.15.0_darwin_arm64.zip... Done.
   Extracted and switched Vault to 1.15.0. Done.
   ````

- Example 2 (binary already present in the Cellar - just making the switch of binary):
   ````
   vaultswitch
    Trying to switch to Vault version 1.15.0
   Found binary and switched Vault to 1.15.0. Done.
   ````

- Example 3 ( download and prepare all the Vault versions from 1.14.x using the release directory):
   ````shell
  for v in $(curl -q https://releases.hashicorp.com/vault| grep '<a href="/vault/1.14'| egrep -v 'hsm|beta|-alpha|-rc1|fips'|cut -d '>' -f2 |cut -d '<' -f 1|sort -u |sed 's/vault_//g') ; do
    vaultswitch $v
  done
   ````
   
   The output might look like:
   ````shell
   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
   100 67683    0 67683    0     0   926k      0 --:--:-- --:--:-- --:--:-- 1016k
   Vault Release 1.14.0 found on the HASHICORP repository.
   Using custom release: 1.14.0
   Trying to switch to Vault version 1.14.0
   No valid binary found in Cellar / Homebrew/bin or missing prebuilt archive.
   Working... Downloading... https://releases.hashicorp.com/vault/1.14.0/vault_1.14.0_darwin_arm64.zip
   Done.
    Unzipping vault_1.14.0_darwin_arm64.zip... Done.
    Extracted and switched Vault to 1.14.0. Done.
   Vault v1.14.0 (13a649f860186dffe3f3a4459814d87191efc321), built 2023-06-19T11:40:23Z
   Vault Release 1.14.0+ent found on the HASHICORP repository.
   Using custom release: 1.14.0+ent
   Trying to switch to Vault version 1.14.0+ent
   No valid binary found in Cellar / Homebrew/bin or missing prebuilt archive.
   Working... Downloading... https://releases.hashicorp.com/vault/1.14.0+ent/vault_1.14.0+ent_darwin_arm64.zip
   Done.
   ...
   Trying to switch to Vault version vault_1.14.4+ent
   Working... Downloading... https://releases.hashicorp.com/vault/1.14.4+ent/vault_1.14.4+ent_darwin_arm64.zip Done.
    Unzipping vault_1.14.4+ent_darwin_arm64.zip... Done.
   Extracted and switched Vault to 1.14.4+ent. Done.
  ````
