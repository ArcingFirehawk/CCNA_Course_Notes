# Day 04 | Intro to the CLI

+ **Command-Line Interface** The interface you use to configure Cisco devices.

### How to connect to a Cisco Device?
+ Before configuring a device, you must first connect via the Console Port.
+ A rollover cable is used to connect to the Console Port.
+ Graphic: Rollover Cable Pin Connections
![image](https://github.com/psaumur/CCNA/assets/106411237/0527c007-d607-4bef-8ce1-7b18a177614d)

+ Use a terminal emulator (e.g., PuTTy) to access the device's CLI.
  + Select "Serial" under "Connection type" using the default settings.

### Configuring the Cisco Device
+ When you first enter the CLI you will be in what is called 'User EXEC' mode (AKA User mode), which is very limited.
+ Enter the `enable` command to be placed in privileged EXEC mode, which provides complete access to view the device's configuration, restart the device, etc.
+ Use `?` to view the commands available. Combining `?` with a letter or partial command will list all the commands with those letters.
+ To enter global configuration mode enter the command `configure terminal` while in priviledged EXEC mode.

### To Enable Password for User EXEC mode:

Router(config)# enable password (password)

- Passwords ARE case-sensitive.

// This command encrypts plain-text passwords, visible in the config files, using simple encryption.

Router(config)# service password-encryption

If you enable 'service password-encryption'

- Current passwords WILL be encrypted.
- Future passwords WILL be encrypted.
- The 'enable secret' WILL NOT be effected.

If you disable 'service password-encryption'

- Current passwords WILL NOT be decrypted.
- Future passwords WILL NOT be encrypted.
- The 'enable secret' WILL NOT be effected.

// This command enables passwords for the Privileged EXEC mode.

Router(config)# enable secret (password)

// enable secret will ALWAYS be encrypted (at level 5)

---


### Configuration Files
+ There are 2 separate configuration files kept on the device at once.
+ Running-config: The current, <mark>active</mark> configuration file on the device. As you enter commands in the CLI, you edit the active configuration.
+ Startup-config: The configuration file that will be loaded upon <mark>restart</mark> of the device.
+ Use `show running-config` and `show startup-config` in priviledged EXEC mode to view the relevant file.
+ Saving the Running Config as Startup Config
  + `write` in priviledged EXEC mode.
  + `write memory` in priviledged EXEC mode.
  + `copy running-config startup-config` in priviledged EXEC mode.

### Encrypting Passwords
---

To encrypt passwords:

Router# `conf t`

Router(config)# `service password-encryption`

This makes all current passwords *encrypted*

Future passwords will ALSO be *encrypted*

“Enable secret” will not be effected (it’s ALWAYS encrypted)

![image](https://github.com/psaumur/CCNA/assets/106411237/09c841fe-b5c0-4683-9082-baf060e24c03)


Now you will see that the password is no longer in plaintext.

“7” refers to the type of encryption used to encrypt the password. In this case, “7” uses Cisco’s proprietary encryption.

“7” is fairly easy to crack since the encryption is weak.

For BETTER / STRONGER encryption, use “enable secret”

`enable secret <password>`

![image](https://github.com/psaumur/CCNA/assets/106411237/346f3015-9211-47a9-888f-4e02a013a728)


“5” refers to MD5 encryption.

Can still be cracked but it’s much much stronger.

Once you use “enable secret” command, this will override “enable password”

---

To CANCEL or delete a command you entered, use the “no” keyword

![image](https://github.com/psaumur/CCNA/assets/106411237/2978d101-08d4-4ee3-8995-f36aa1c47d15)


In this instance, disabling “service password-encryption”:

- current passwords will NOT be decrypted (unchanged)
- future passwords will NOT be encrypted
- the “enable secret” will not be effected

---

![image](https://github.com/psaumur/CCNA/assets/106411237/e16966a3-674a-4376-bdab-2c06e3659e5f)

![image](https://github.com/psaumur/CCNA/assets/106411237/e449e074-bf4c-40f1-a61e-0442ad83f284)

![image](https://github.com/psaumur/CCNA/assets/106411237/4c1bdf58-7de6-4074-8189-1573a174474c)

![image](https://github.com/psaumur/CCNA/assets/106411237/e7771e65-5ed5-406d-9751-76520713210c)

![image](https://github.com/psaumur/CCNA/assets/106411237/5f7357d4-f44b-4a61-a24c-86f3368f30f7)
