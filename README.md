# PassMan - Easy, Secure, Password Manager

PassMan is a secure, and easy to use password manager that runs on the terminal! It's also written in [bash](https://www.gnu.org/software/bash/).

## How PassMan Works ...

PassMan was created out of frustration. For years I've been using encrypted files to store passwords. It works for me. But, it gets painful. Over the years I got faster at it, but it's still a pain in the ass! I decided to finally create and share a script to make my life easier - and hopefully yours. You may ask why I didn't use a service such as [LastPass](https://www.lastpass.com/). The simple answer is ... I don't trust them.

PassMan stores passwords in an encrypted file as csv and allows you to **add**, **retrieve** and **delete** passwords. When a password is generated, or retrieved, it's automatically copied into your clipboard for ease of use. Cool right?

I decided to use `gpg` for encryption/decryption because it's very secure (assuming host machine is secure and user password is strong). You can pass the database around securely in emails, or on a USB stick, with no chance of an attacker ever seeing what's inside it. At least not in your lifetime. To learn more about `gpg` checkout the [handbook](https://www.gnupg.org/gph/en/manual.html).

The password database is encrypted/decrypted using [public key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography). PassMan can generate the public/private keys for you, or you can pass in your own.

## Dependencies

The following dependencies must be installed for PassMan to work. These can be installed using the package manager on your OS such as `brew`, `apt`, `yum` etc.
    
    * bash
    * gpg
    * pwgen
    * pbcopy

## Installation

First clone the repo:

    git clone http://github.com/JamesTheHacker/passman

Move the repo to a directory in your `$PATH`. I suggest using a directory like `~/bin` under your home directory:

    mkdir ~/bin
    export PATH=$PATH:$HOME/bin
    mv passman/passman ~/bin
    chmod -R 700 ~/bin/passman    

Now you can run PassMan in the terminal. To test, display `usage`:

    passman -h

## Initial First Run

If you haven't got a public/private key PassMan can generate one for you using `gpg --full-generate-key`. It can also generate a new encrypted password database.

To create the public/private key, and password database, lets set up a new password:

    passman -k gmail

**Note:** The `-k` option is used to pass a key that is used to identify a password. A key you will remember. It's helpful to name them after the website or application the password is used for. For example: `facebook`, `gmail`, `twitter`, `4chan`, `reddit` ... you get the idea.

Enter `y` and follow the on screen instructions to generate a new public/private key and password database. Remember ... **use a strong password!**

By default PassMan will store the password database, and public key, as files in the users home directory:

* Public key: `~/.passman_pk`
* Encrypted password database: `~/.passman_db`

Once complete a newly generated password will now be stored in the password database. If you press `CTRL+V` you will see the password. Magic.

Continue reading to learn learn how to `retrieve`, and `delete`, passwords.

## Usage

**Create New Password**

    passman -k facebook

A password is automatically generated and stored in the clipboard (press `CTRL+V` to use). If a password already exists for the specified key an error will be returned:

    Password with facebook already exists.   

By default the length of generated passwords is `85` characters. If you'd like to generate a longer password use the following:

    passman -k facebook -l 150

The `-l` option allows you to specify a password length.

**Fetch A Stored Password**

    passman -k facebook -m get

If password exists it is copied into the clipboard and can be used with `CTRL+V`

**Delete A Password**

    passman -k facebook -m del

If password exists it will be deleted from the password database

**Update A Password**

Updating a password is 2 commands. First delete the existing one, then generate a new password:

    passman -k facebook -m del
    passman -k facebook

New password is now in the clipboard and can be used with `CTRL+V`

**Custom Public Key & Password Database**

You can specify your own public key, and password database, like so:

    passman -k facebook -p ~/path/to/password_db -f ~/path/to/public_key

You must use the `-p` and `-f` option for every command when using a custom key and/or database.

## Security Tips

PassMan is only as strong as the system using it. 

Here's some tips to help keep you safe:

* **NEVER SHARE YOUR PRIVATE KEY!**
* When generating a key ensure your password is very strong! The longer the better!
* Backup your private and public keys onto physical media. If you're super paranoid print them off as QR codes and store them in a safe.
* Make regular backups of password database/s in the event of system failure, nature disaster, etc.
* Encrypt your swap space

## Issues

The unencrypted password database is briefly stored in a `/tmp` using `mktemp`. It is possible under certain conditions for this password to end up in swap space. This isn't idea if your swap space is not encrypted. I am working on fixing this.

## Contributing

If have any problems, or would like to suggest a feature, please file an issue. I welcome all pull requests. If you can improve PassMan in any way I will happily merge.

## Testing

This script has only been tested on OSX 10.10.5. If you could test it on your own platform and report any issues I would be eternally grateful.

## A Word From The Author ...

As I write this the UK Government are battling to ban encryption. Apparently to help fight terrorism and keep us safe. In 2017 our security and privacy are at risk. I urge everyone to exercise their right to privacy. Even if it's against the will of higher powers. I'm just your average Joe doing his part to help. Keep fighting the good war.

If you'd like to contact me, add `@thunderkat` on [Wire](https://app.wire.com/).
