# Full Mac Setup Process (for Jeff Geerling)

There are some things in life that just can't be automated... or aren't 100% worth the time :(

This document covers that, at least in terms of setting up a brand new Mac out of the box.

## My set-up

* Add key to the Yubikey
* Install oh my zsh
* Install oh my zsh plugins

## Initial configuration of a brand new Mac

Before starting, I completed Apple's mandatory macOS setup wizard (creating a local user account, and optionally signing into my iCloud account). Once on the macOS desktop, I do the following (in order):

  - Install Ansible (following the guide in [README.md](README.md))
  - **Sign in in App Store** (since `mas` can't sign in automatically)
  - Clone mac-dev-playbook to the Mac: `git clone git@github.com:geerlingguy/mac-dev-playbook.git`
  - Drop `config.yml` from `~/Dropbox/Apps/Config` to the playbook (copy over the network or using a USB flash drive).
  - Run the playbook with `--skip-tags post`.
  - Manual settings to automate someday:
    - System Preferences:
      - Keyboard
        - Customize Modifier Keys... > Caps Lock to Ctrl
        - Key repeat rate: Fast
        - Delay until repeat: Short
        - Switch Spotlight vs Change Language
    - Dock Settings:
      - Left
      - Show suggested and recent apps in Dock
  - Install Logi Options+ and log in


## To Wrap in Post-provision automation

The following tasks have to wait for the initial Dropbox sync to complete before they'll succeed. So ideally I'll stick this all in a post-provision script but somehow flag it not to run on first provision.

```
# Install Node
n lts

# Install TPM
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

## When formatting old Mac

  - Sign out of Adobe Creative Cloud
  - Sign out of Panic Sync in Transmit
  - Deauthorize Apple Music in iTunes/Music App
  - Make sure anything new merged into `~/Dropbox/Apps/Config`:
    - Fonts from ~/Library/Fonts
    - Motion Plugins from ~/Movies/Motion
    - Final Cut Pro Text Styles in ~/Library/Application Support/Motion/Library/Text Styles
    - Sequel Ace shortcuts from ~/Library/Containers/com.sequel-ace.sequel-ace/Data/Library/Application\ Support/Sequel\ Ace/Data/Favorites.plist
  - Follow Apple's guide [here](https://support.apple.com/en-au/HT212749)
