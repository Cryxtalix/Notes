# GPG

## Functions
### Generate keys

$`gpg --full-generate-key`

$`gpg --full-generate-key --pinentry-mode loopback`

### List public and private keys in keyring

$`gpg --list-keys`

$`gpg --list-secret-keys`

### Delete keys

$`gpg --delete-secret-key "username or keyid"`

$`gpg --delete-key "username or keyid"`

### Export keys

To print keys to terminal:

$`gpg --export --armor "email"`

$`gpg --export-secret-key --armor "email"`

Or to export to file:

$`gpg --output public.pgp --export --armor "email"`

$`gpg --output private.pgp --export-secret-key --armor "email"`

Filename does not matter

### Import keys

$`gpg --import public.pgp`

### Create revocation certificate

$`gpg --output revoke.asc --gen-revoke "email"`

### Keyservers

To lookup keys on a (default) keyserver:

$`gpg --search-keys "email"`

To import keys from a keyserver:

$`gpg --recv-keys "keyid"`

To send key to (default) keyserver:

* Get keyid with:
	* $`gpg --list-keys --keyid-format=long "email"`
	* keyid is after key type, e.g. ed25519/"keyid"
* Send key with:
	* $`gpg --send-keys "keyid"`

Running "git log --show-signature" and you can check if git commits are certified.

## Adding keys to git

* Get keyid with:
	* $`gpg --list-keys --keyid-format=long "email"`
	* keyid is after key type, e.g. ed25519/"keyid"
* Set primary signing key:
	* $`git config --global user.signingkey keyid`
