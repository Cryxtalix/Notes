# SSH

Generate key:

$`ssh-keygen -t ed25519`

Adding key to server:

$`ssh-copy-id -i public_key.pub username@server_ip`

Connecting to server:

$`ssh username@server_ip`

or to specify key:

$`ssh -i private_key username@server_ip`

Copy files:

$`scp /path/to/local/file username@server_ip:/path/on/server`