# xerom-node-dockerized
Xerom node daemon for the Xerom (XERO) Network


This method uses a [bind mount](https://docs.docker.com/storage/bind-mounts) to persist the blockchain data on the host.

To simplify things, basic operations have been added as `Makefile` commands.

## To build:
```
make image
```

## To run the node / daemon (non-interactive):
```
make node
```

## To access the running node interactively with the geth console:
```
make attach
```

## To run as a systemd service:
Assuming you have created a user `xeromnode` in group `xeromnode` and have cloned this repository in the `xeromnode` home user directory,
the following service file will start the daemon automatically at system startup.

Enter the following into `/etc/systemd/system/xeromnode.service`:
```
[Unit]
Description=Xerom node daemon service
After=network.target

[Service]
User=xeromnode
Group=xeromnode
Type=simple
Restart=always
RestartSec=30s
WorkingDirectory=/home/xeromnode/xerom-node-dockerized
ExecStart=/usr/bin/make node

[Install]
WantedBy=default.target
```

After creating the service file, enable and restart the service:
```
systemctl enable xeromnode
systemctl restart xeromnode
```

NOTE: You must make sure the service is running if you use interactive mode for the geth console.

To stop the service:
```
systemctl stop xeromnode
```

To restart the service:
```
systemctl restart xeromnode
```

<hr>

#### Donations accepted:
`0x087c83e882822E96AD09eF2A15391C88E241AdA8` (XERO)
