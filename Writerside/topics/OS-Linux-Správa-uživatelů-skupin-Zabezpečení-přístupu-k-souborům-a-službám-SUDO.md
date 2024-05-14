# OS Linux - Správa uživatelů

## Sprava uzivatelu

### User

#### Create account: `sudo useradd [options] [user-name]`

That's enough to create the account. However, there are some options you can add. As always, review the associated man
page for details. Here are a few common options:

- `--create-home (-m)` PATH: Adds a home directory (this is a default on some distributions)
- `--shell (-s)` PATH: sets the user's preffered shell if it's different from /bin/bash
- `-g` Number: specific group ID (GID)
- `--comment (-c)` "COMMENT": Populates the comment field (usually with the user's full name enclosed in quotes)
- `-p` Password: To set an unencrypted password for the user

#### Nasledne je dobre myslet taky na `sudo passwd [options] [user-name]` pro zmenu hesla daneho uzivatele

- `-d, -delete` this option deletes the user password and makes the account password-less
- `-e, -expire` this option immediately expires the account password and forces the user to change password on their
  next login.
- `-i, -inactive` INACTIVE_DAYS: this option is followed by an integer, which is the number of days after the password
  expires that the account will be deactivated.
- `-w, -warndays` WARN_DAYS: this option is used to change the number of days before the password is to expire, to
  display the warning for expiring password
- `-x, -maxdays` MAX_DAYS: set the maximum number of days for which the password remains valid. After MAX_DAYS, the
  password will expire and the user will be forced to change password.

#### Modify accounts

`sudo usermod [options] [user]`

- `--comment (-c)` "comment": Modifies the comment field
- `--home (-d)` PATH: modifies home directory information
- `--expiredate` Changes account-expiration settings
- `--login (-l)` NAME: Modifies the username
- `--lock (-L)`: Locks a user account
- `--unlock (-U): Unlocks a user account`
- `-g` NAME: To change the group of a user
- `-aG (-a -G)`: add to other groups

#### Delete accounts

`sudo userdel [options] [user-name]`

- `-r`: the files in the user's home directory will be removed along with the home directory itself and the user's mail
  spool.
- `-f` This option forces the removal of the specified user account. It doesnt matter that the user is still logged in.

### Group

Linux administrator pouziva groups pro prideleni pristupu k souborum a jinym zdrojum. Vsechny groupy a jejich ID jsou v
/etc/group.

#### Groupadd

![group-add.png](group-add.png)

#### Groupmod

![group-mod.png](group-mod.png)

#### Groupdel

![group-del.png](group-del.png)

## Chmod, Chgrp, Chown

### Chown

`chown [options] [user-name] [:group] [file/directory]`

- `-R` pro rekurzivni nahrazeni

### Chgrp

`chgrp [group] [file/directory]`

- `-R` pro rekurzivni nahrazeni

### Chmod

![chmod.png](chmod.png)

- rwx = 111 in binary = 7
- rw- = 110 in binary = 6
- r-x = 101 in binary = 5
- r-- = 100 in binary = 4
- -wx = 011 in binary = 3
- -w- = 010 in binary = 2
- --x = 001 in binary = 1
- --- = 000 in binary = 0
- rwx rwx rwx = 111 111 111
- rw- rw- rw- = 110 110 110
- rwx --- --- = 111 000 000
  `chmod [0-7][0-7][0-7] [file/directory]`
  `chmod [ugoa][+=-][rwx] [file/directory]`

- u ... the user who owns the file (this means "you")
- g ... The group the file belongs to.
- o ... the other users
- a ... all of the above (an abbreviation for ugo)
- r ... Permission to read the file
- w ... Permission to write (or delete) the file.
- x ... Permission to execute the file, or in the case of a directory, search it.

## SUDO (substitu user do)

je prikaz ktery je uzivany v unixovych systemech. Slouzi k vykonani operace s opravnenimi jineho uzivatele, jimz je
obvykle root. Uzivatele opravneni pouzivat prikaz sudo jsou obvykle pri autorizaci dotazovani na svoje vlastni heslo,
lze vsak nastavit, aby byli dotazovani na heslo uzivatele, jehoz opravneni budou pouzivat, nebo aby nemuseli zadavat
heslo vubec. Po zadani hesla je dale zkontrolovano, zda jsou uvedeni v souboru /etc/sudoers (v tomto souboru je seznam
uzivatelu kteri mohou sudo pouzivat).
`usermod -aG sudo [username]` ... pridani user do sudo groupy
`sudo bash` presun do bash shellu jako root user





