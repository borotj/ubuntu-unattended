# Unattended Ubuntu ISO Maker

This simple script will create an unattended Ubuntu ISO from start to finish. It will ask you a few questions once, and embed your answers into a remastered ISO file for you to use over and over again.

This script creates a 100% original Ubuntu installation; the only additional software added is ```openssh-server```. There is no ```apt-get update``` performed. You have all the freedom in the world to customize your Ubuntu installation whichever way you see fit. This script just takes the pain out of re-installing Ubuntu over and over again.

Created by: **Rinck Sonnenberg (Netson)**

## Fork
* Add support for French language and keyboard
* Add additional packages installation

## Compatibility

The script supports the following Ubuntu editions out of the box:

* Ubuntu 12.04.5 LTS Server amd64 - Precise Pangolin
* Ubuntu 14.04.6 LTS Server amd64 - Trusty Tahr
* Ubuntu 16.04.6 LTS Server amd64 - Xenial Xerus
* Ubuntu 18.04.2 LTS Server amd64 - Bionic Beaver

This script has been tested on and with these two versions as well, but I see no reason why it shouldn't work with other Ubuntu editions. Other editions would require minor changes to the script though.

## Usage

* From your command line, run the following commands:

```
$ git clone https://github.com/borotj/ubuntu-unattended
$ sudo ./create-unattended-iso.sh
```
or
```
$ wget https://raw.githubusercontent.com/borotj/ubuntu-unattended/master/create-unattended-iso.sh
$ chmod 0744 create-unattended-iso.sh
$ sudo ./create-unattended-iso.sh
```

* Choose which version you would like to remaster:

```
 +---------------------------------------------------+
 |            UNATTENDED UBUNTU ISO MAKER            |
 +---------------------------------------------------+

 which ubuntu edition would you like to remaster:

  [1] Ubuntu 12.04.5 LTS Server amd64 - Precise Pangolin
  [2] Ubuntu 14.04.6 LTS Server amd64 - Trusty Tahr
  [3] Ubuntu 16.04.6 LTS Server amd64 - Xenial Xerus
  [4] Ubuntu 18.04.2 LTS Server amd64 - Bionic Beaver

 please enter your preference: [1|2]:
```

* Enter your prefered language; the default is *fr*:

```
 please enter your preferred language (en/fr): fr
```
* Enter your desired timezone; the default is *Europe/Paris*:

```
 please enter your preferred timezone: Europe/Paris
```

* Enter your desired username; the default is *\<login name\>*:

```
 please enter your preferred username: user
```

* Enter the password for your user account; the default is *empty*

```
 please enter your preferred password:
```

* Confirm your password:

```
 confirm your preferred password:
```

* Install additional packages in adition to openssh-server

```
which additional package to install (ex: nano htop): openssh-server nano htop open-vm-tools docker docker-compose
```
* Sit back and relax, while the script does the rest! :)

## What it does

This script does a bunch of stuff, here's the quick walk-through:

* It asks you for your preferences regarding the unattended ISO
* Downloads the appropriate Ubuntu original ISO straight from the Ubuntu servers; if a file with the exact name exists, it will use that instead (so it won't download it more than once if you are creating several unattended ISO's with different defaults)
* Downloads the netson preseed file; this file contains all the magic answers to auto-install ubuntu. It uses the following defaults for you (only showing most important, for details, simply check the seed file in this repository):
 * Language/locale: fr_FR or en_US
 * Keyboard layout: FR or EN
 * Root login disabled (so make sure you write down your default usernames' password!)
 * Partitioning: LVM, full disk, single partition
 * Choose to install additional packages :
     - By default only "openssh-server" will be installed and these packages will be suggest :
        - nano htop open-vm-tools
* Install the mkpasswd program (part of the whois package) to generate a hashed version of your password
* Install the genisoimage program to generate the new ISO file
* Mount the downloaded ISO image to a temporary folder
* Copy the contents of the original ISO to a working directory
* Set the default installer language
* Add/update the preseed file
* Add the autoinstall option to the installation menu
* Generate the new ISO file
* Cleanup
* Show a summary of what happended:

```  
 installing required packages
 remastering your iso file
 creating the remastered iso
 -----
 finished remastering your ubuntu iso file
 the new file is located at: /tmp/ubuntu-17.04-server-amd64-fr-unattended.iso
 your username is: <your login name>
 your password is: 
 your hostname is: ubuntu
 your language is: fr
 your timezone is: Europe/Paris
 packages: openssh-server nano htop open-vm-tools
```

### Once Ubuntu is installed ...

Just fire off the start.sh script in your user's home directory to complete the installation. 

```$ sudo ~/start.sh``` 

## Greetings
Many thanks to @hvanderlaan and all contributors

### Licensing
ubuntu-unattended is licensed under the GPLv3:
```
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

For the full license, see the LICENSE file.
```
