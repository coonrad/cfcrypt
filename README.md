# cfcrypt

**cfcrypt** is a utility that handles the variation of openssl encryption settings used to encrypt and decrypt pfSense configuration files. The details are documented here: [Encrypted Configuration files](https://docs.netgate.com/pfsense/en/latest/backup/restore.html#encrypted-configuration-files)

There are three methods:

- **current**: aes-256-cbc / sha256 / pbkdf2 / iterations 500000
- **old**: aes-256-cbc / sha256 / pbkdf2 / iterations default
- **deprecated**: aes-256-cbc / md5

The openssl commands can be cumbersome, especially if you don't know the encryption method. You can decrypt the config on the firewall:

```bash
pfSsh.php playback cryptconfig decrypt /root/config-encrypted.xml /root/dencryptedfile.xml
```

The tool will try to decrypt the file with the current openssl settings, it will then move to old, and then deprecated. If it fails to decrypt the file it will assume the password is wrong. To encrypt files pass the `-e` flag. Files will be encrypted with the current settings `-md sha256 -pbkdf2 -iter 500000`.

## Installation
Clone this repo (or copy the script file) to your system.
Make the script executable `chmod +x cfcrypt`.
Move the file somewhere in your $PATH like `~/bin` or `~/.local/bin`.

## Usage

```bash
Usage:

Decrypt (default)
  cfcrypt encrypted-config.xml

Encrypt
  cfcrypt -e config.xml
```

## Notes

Tested on MacOS, Debian, FreeBSD, pfSense. Let me know of any issues.
