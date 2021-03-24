# netbox_topology

### Note: For Netbox v2.8.0+, please consider using [nextbox-ui-plugin](https://github.com/iDebugAll/nextbox-ui-plugin) instead.

Patch to apply to a netbox installation to add beautiful topology view to sites

**Updated by [mylivingweb](https://github.com/mylivingweb/netbox_topology) to use `/api/dcim/cables/ endpoint instead` of `/api/dcim/interface-connections/`**

Additional tweaks, such as cable-type changing selection colors added by NoOne-dev

Once installed your individual site's pages should look like this:

![Screenshot](docs/screenshot-site.png "Screenshot of site's page")

This module allows to create and delete connections between interfaces via control panel:

![Screenshot control panel](docs/screenshot-panel.png "Screenshot of the control panel")

## INSTALL:

1. clone git repo

```
git clone https://github.com/NoOne-dev/netbox_topology.git
```

2. run install.sh, sudo might be required to get access to netbox installation directory:

```
cd netbox_topology
sudo ./install.sh
```

3. restart netbox via supervisord or apache/nginx depending on your installation

```
sudo supervisorctl restart netbox
sudo service apache2 restart
```

4. open django admin web-interface and create a custom text field named "coordinates" under dcim->device model

![Screenshot django setup](docs/screenshot-customfield.png "Screenshot of django setup")

5. modify `$NETBOXPATH/netbox/static/js/topology_config.json` to include your list on roles to hide from the topology view. You will need to add new list of cables to shown under `shown_cables`. Constants are [defined here](https://github.com/digitalocean/netbox/blob/develop/netbox/dcim/constants.py#L336)
```
CABLE_TYPE_CAT3 = 1300
CABLE_TYPE_CAT5 = 1500
CABLE_TYPE_CAT5E = 1510
CABLE_TYPE_CAT6 = 1600
CABLE_TYPE_CAT6A = 1610
CABLE_TYPE_CAT7 = 1700
CABLE_TYPE_MMF_OM1 = 3010
CABLE_TYPE_MMF_OM2 = 3020
CABLE_TYPE_MMF_OM3 = 3030
CABLE_TYPE_MMF_OM4 = 3040
CABLE_TYPE_SMF = 3500
CABLE_TYPE_POWER = 5000
``` 

*please note that the list should include SLUGs for roles, not names and number for the cables to be shown. please check that json is valid.*

6. let me know if there are any issues - https://github.com/NoOne-dev/netbox_topology/pulls



## UNINSTALL:

```
sudo ./uninstall.sh
```

OR if your installation is GIT based (Option 2 from Netbox installation guide):

```
cd /opt/netbox
git checkout .
```
