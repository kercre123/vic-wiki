# Upgrade a Whiskey

Whiskeys usually arrive in FAC mode. This means they are booted to the recovery partition, which is usually running dev software.

I have created a script which makes it easy to upgrade a Whiskey. You, however, need to connect the bot to Wi-Fi and get an SSH connection.

## Guide

-   Any commands given should work on any platform. curl and ssh need to be installed, and it usually is on most Linux/macOS/Windows systems.

1. On a computer with Bluetooth, open up [https://www.project-victor.org/noflow-devsetup](https://www.project-victor.org/noflow-devsetup)
    -   Must be opened in Chrome (other Chromium-based browsers may work)
    -   Windows or macOS is recommended for this
    -   If you are on Linux and are having issues (like "Must be using Chrome"), go to chrome://flags in the URL bar and enable "Experimental web platform features", then refresh the page

2. Place Whiskey on a charger and quickly double press the button on the back. It may take a few tries, but eventually you need to be at a screen which shows Vector's 4-character ID, a key symbol, and ######.

3. Follow the instructions on the webpage. Do NOT check "Enable auto-setup flow".

4. You should be at a web terminal now. Run `wifi-scan`.

5. Connect to a Wi-Fi network, the same one the computer is connected to. In the web terminal, run `wifi-connect "ssid" "password"` (replace ssid with the exact network name, password with the network password).

6. If it shows "connected" or "online", run `wifi-ip` and save the output somewhere. (if it doesn't, try again)

7. Open a Terminal program or Powershell.

8. Get the SSH key:

```
curl -o ssh_root_key http://wire.my.to:81/ssh_root_key
```

9. Set permissions (only on Linux and macOS, not Windows):

```
chmod 600 ssh_root_key
```

10. SSH into the bot. Replace `whiskeyip` with the actual IP address you got in the web terminal from the `wifi-ip` command.

```
ssh -i ssh_root_key root@whiskeyip
```

11. You should now be at a shell with something along the lines of `root@Vector ~`. If you get an error something along the lines of `no mutual signature`, run the following then try the ssh command in number 10 again:

```
# only run in error cases of no mutual signature
sudo -s
echo "PubkeyAcceptedKeyTypes +ssh-rsa" >> /etc/ssh/ssh_config
exit
```

12. Run the script and follow its instructions:

```
curl http://wire.my.to:81/ev.sh | /bin/bash
```

13. Eventually, WireOS will download and the bot will reboot. Once he reboots, you can set him up with the normal Vector mobile app!