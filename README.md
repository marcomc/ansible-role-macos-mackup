[![Build Status](https://travis-ci.com/marcomc/ansible-role-macos-mackup.svg?branch=master)](https://travis-ci.com/marcomc/ansible-role-macos-mackup)

# Mackup sync utility installation
Ansible role to install and configure the [Mackup sync utility](https://github.com/lra/mackup).

If Mackup is not installed in the system it will ne installed via Homebrew.

## (Soft) Requirements & Dependencies
* [Jeff Geerling](https://github.com/geerlingguy)'s' [geerlingguy.homebrew](https://github.com/geerlingguy/ansible-role-homebrew) which is defined as Ansible Galaxy dependency

### Ansible
It was tested on the following versions:
 * 2.9

### Operating systems
Target MacOS 10.15 possibly earlier versions too (not yet tested)

## Example Playbook
Just include this role in your list.
For example

    - host: all
      vars:
        mackup_engine:: icloud
        mackup_applications_to_ignore:
          - ansible
        mackup_action: restore-only
      roles:
        - marcomc.macos_mackup

## Variables

    mackup_action: backup             # backup, restore, restore-only, uninstall
    mackup_engine: "dropbox"          # dropbox, google_drive, icloud, file_system
    mackup_path: ""                   # path to the directory that contains the 'mackup_directory' only IF the selected engine is 'file_system'
    mackup_directory: "Mackup"        # name of the mackup backup directory
    mackup_applications_to_ignore: [] # list of application to be ignored when backing up or restoring with mackup

By default Mackup will place/look-for its backup folder in your Dropbox directory, but this assumes that Dropbox is already installed and configured in your system.

My personal preference is to have Mackup to backup into iCloud especially if you are using this role to restore your configuration on a new machine in which you have already signed in with iCloud (which is part of the Setup Assistant process).

### Actions: `mackup_action`

* `backup` -  __Activate Mackup__ then __move__ your applications configurations into the `mackup_directory` then __link__ them to their original location in your system
* `restore` - __Activate Mackup__ then __link__ your applications configurations the `mackup_directory` to their original location in your system.
* `restore-only` - Only __copy__ your applications configurations from the `mackup_directory` to their original location in your system __without activating Mackup__
* `uninstall` - __Deactivate Mackup__ if it is active

### Engines: `mackup_engine`

* `dropbox` - [Dropbox](https://dropbox.com)
* `google_drive` - [Google Drive](https://drive.google.com)
* `icloud` - [iCloud](https://icloud.com)
* `file_system` - user arbitrary file_system path, requires you to specify `mackup_path` value

## Continuous integration
This role has (not yet) a travis basic test (for github) only.

## Troubleshooting & Known issues

## License
[MIT](LICENSE)

## Copyright
Marco Massari Calderone (c) 2020 - marco@marcomc.com
