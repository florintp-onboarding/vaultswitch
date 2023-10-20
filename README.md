# A tool to switch between Vault binaries on MAC ARM64
[![license](http://img.shields.io/badge/license-apache_2.0-red.svg?style=flat)](https://github.com/florintp-onboarding/vaultswitch/blob/main/LICENSE)

## Install the utility script in the default HOMEBREW bin directory
The current repository is used for initial setup and work with a fast Vault binary switch utility.

**Please note**: The script is tested and validated to work on MAC OS on ARM 64 platforms having HOMEBREW as install manager.

## Prerequisites:
* Install and configure [Homebrew](https://brew.sh/)
* Minimal Vault exposure [Vault-Getting-started](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-install?in=vault%2Fgetting-started)


## Install Homebrew (if it is not already present)
1. Install Homebrew from using
* Install and configure [Homebrew direct install](/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Clone this repository
   `gh repo clone florintp-onboarding/vaultswitch`
   
4. Install the script into HOMEBREW/bin directory
   ````
   cd vaultswitch
   chmod +rx vaultswitch
   cp -p vaultswitch /opt/homebrew/bin
   ```` 


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

- Example 3 ( download and prepare all the Vault versions from 1.14.x using the release direcctory):
   ````
   for v in $(curl -q https://releases.hashicorp.com/vault| grep '<a href="/vault/1.14'| egrep -v 'hsm|beta|-alpha|-rc1|fips'|cut -d '>' -f2 |cut -d '<' -f 1|sort -u ) ; do 
      vaultswitch $v
   done
   ````
   The output might look like:
   ````
   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
   100 62902    0 62902    0     0   457k      0 --:--:-- --:--:-- --:--:--  468k
   Trying to switch to Vault version vault_1.14.0
    Working... Downloading... https://releases.hashicorp.com/vault/1.14.0/vault_1.14.0_darwin_arm64.zip Done.
    Unzipping vault_1.14.0_darwin_arm64.zip... Done.
   Extracted and switched Vault to 1.14.0. Done.
   ...
   Trying to switch to Vault version vault_1.14.4+ent
   Working... Downloading... https://releases.hashicorp.com/vault/1.14.4+ent/vault_1.14.4+ent_darwin_arm64.zip Done.
    Unzipping vault_1.14.4+ent_darwin_arm64.zip... Done.
   Extracted and switched Vault to 1.14.4+ent. Done.
  ````
