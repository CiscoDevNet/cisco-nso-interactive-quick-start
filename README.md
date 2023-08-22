# Cisco NSO interactive Quick Start

Cisco Code Exchange provides the ability to run examples in a browser-based integrated development environment (IDE). We are bringing now the ability to run NSO on top it. 

## Get Started

This short example will demostrate how you can setup a simulated network of Cisco-ios routers and how to manage these with NCS in Code Exchange Cloud IDE. NCS will talk Cisco CLI towards the routers.

Prepare NSO

```bash
source $NCS_DIR/ncsrc
ncs-netsim --dir ~/example/netsim create-network cisco-ios-cli-3.8 2 ios
ncs-setup --dest ~/example --netsim-dir ~/example/netsim
cd ~/example/
ncs-netsim start
ncs
ncs --version
ncs --status | grep -i status
```

Configure NSO

```bash
ncs_cli -C -u admin
devices sync-from
devices device ios1 check-sync
config
show full-configuration devices device ios1 config | nomore
devices device ios0 config
ios:hostname nso.cisco.com
top
commit dry-run outformat native
commit
```

### Explore and play with NSO Example Collection

Go to `~/nso-6.1.2.1` > `examples.ncs` in VS Code workspace or use the terminal

```bash
cd $NCS_DIR/examples.ncs/
developer:examples.ncs > ll
total 28
drwxr-xr-x 1 developer ncsadmin   267 Jun 28 11:38 .
drwx------ 1 developer ncsadmin   294 Jul 18 13:33 ..
-rw-r--r-- 1 developer ncsadmin 27052 Jun 28 11:38 README
drwxr-xr-x 1 developer ncsadmin    27 Jun 28 11:05 crypto
drwxr-xr-x 1 developer ncsadmin    36 Jun 28 11:05 datacenter
drwxr-xr-x 1 developer ncsadmin   261 Jun 28 11:38 development-guide
drwxr-xr-x 1 developer ncsadmin    27 Jun 28 11:05 generic-ned
drwxr-xr-x 1 developer ncsadmin    50 Jun 28 11:05 getting-started
drwxr-xr-x 1 developer ncsadmin    26 Jun 28 11:05 high-availability
drwxr-xr-x 1 developer ncsadmin    69 Jun 28 11:05 misc
drwxr-xr-x 1 developer ncsadmin   143 Jun 28 11:05 service-provider
drwxr-xr-x 1 developer ncsadmin    19 Jun 28 11:05 snmp-ned
drwxr-xr-x 1 developer ncsadmin   155 Jun 28 11:38 snmp-notification-receiver
drwxr-xr-x 1 developer ncsadmin    53 Jun 28 11:05 web-server-farm
drwxr-xr-x 1 developer ncsadmin    31 Jun 28 11:05 web-ui
```

## Guidelines

- Code shared is public, avoid adding any confidential information.

## Recommendations

- It is recommended to avoid specifying NSO versions in the code, as the underlying NSO will be upgraded with newer releases.

## FAQ

- My code is approved but I don't see it?
  - Expand the `/home/developer/src` in the workspace or do `ls -l /home/developer/src`
