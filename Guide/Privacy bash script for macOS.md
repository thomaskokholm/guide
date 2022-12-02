The script below automates the proccess of the follow seven privacy tasks om macOS:
- Clear Bash terminal history
- Clear ZSH terminal history
- Clear DNS cache
- Purge inactive memory usage
- Clear system cache files
- Empty trash on all volumes
- Clear CUPS printer job cache

## Usage
1. Paste the script below in a file (i.e. privacy.sh).
2. Ppen up your terminal
3. Navigate to where you saved the file (i.e. privacy.sh)
4. Give the file execute permissions by typing : `$ chmod +x privacy.sh`
5. Finally run the script by typing `$ ./privacy.sh`

Note that ***your terminal might ask for your administrator password*** in order to process the script.

```bash
#!/usr/bin/env bash

  

# ----------------------------------------------------------

# -------------Request administrator privileges-------------

# ----------------------------------------------------------

if [ "$EUID" -ne 0 ]; then

script_path=$([[ "$0" = /* ]] && echo "$0" || echo "$PWD/${0#./}")

sudo "$script_path" || (

echo 'Administrator privileges are required.'

exit 1

)

exit 0

fi

  
  

# ----------------------------------------------------------

# --------------------Clear bash history--------------------

# ----------------------------------------------------------

echo '--- Clear bash history'

rm -f ~/.bash_history

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# --------------------Clear zsh history---------------------

# ----------------------------------------------------------

echo '--- Clear zsh history'

rm -f ~/.zsh_history

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# ---------------------Clear DNS cache----------------------

# ----------------------------------------------------------

echo '--- Clear DNS cache'

sudo dscacheutil -flushcache

sudo killall -HUP mDNSResponder

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# ------------------Purge inactive memory-------------------

# ----------------------------------------------------------

echo '--- Purge inactive memory'

sudo purge

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# -----------------Clear system cache files-----------------

# ----------------------------------------------------------

echo '--- Clear system cache files'

sudo rm -rfv /Library/Caches/* &>/dev/null

sudo rm -rfv /System/Library/Caches/* &>/dev/null

sudo rm -rfv ~/Library/Caches/* &>/dev/null

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# ----------------Empty trash on all volumes----------------

# ----------------------------------------------------------

echo '--- Empty trash on all volumes'

# on all mounted volumes

sudo rm -rfv /Volumes/*/.Trashes/* &>/dev/null

# on main HDD

sudo rm -rfv ~/.Trash/* &>/dev/null

# ----------------------------------------------------------

  
  

# ----------------------------------------------------------

# ---------------Clear CUPS printer job cache---------------

# ----------------------------------------------------------

echo '--- Clear CUPS printer job cache'

sudo rm -rfv /var/spool/cups/c0*

sudo rm -rfv /var/spool/cups/tmp/*

sudo rm -rfv /var/spool/cups/cache/job.cache*

# ----------------------------------------------------------

  
  

echo 'Privacy and security script completed!'

echo 'Press any key to exit.'

read -n 1 -s
```

This script is based on the open source tool by [UndergroundWires](https://github.com/undergroundwires). Check out the [repository](https://github.com/undergroundwires/privacy.sexy) for details and even more privacy scripts.
