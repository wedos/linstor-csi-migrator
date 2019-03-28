# linstor-csi-migrator
Convert old LINSTOR flexVolumes to CSI

### How it works

Script takes PersistentVolumes with Linstor flexVolume driver or old-style CSI metadata, which stopped working after last update of linstor csi-plugin and generates commands for update their metadata to use with new csi-plugin.

* https://github.com/LINBIT/linstor-csi/issues/4
* https://github.com/LINBIT/linstor-csi/issues/7

### Preparation

* Make sure that you have `jq` and `kubectl` installed in your system.

* Download the script:

  ```
  curl -LO https://github.com/kvaps/linstor-csi-migrator/raw/master/linstor-csi-migrator.sh
  chmod +x linstor-csi-migrator.sh
  ```

### Usage


* Make sure that you have access to list PVs in your cluster.

* Generate commands:

  ```
  # FlexVolumes:
  ./linstor-csi-migrator.sh flexvolume > flexvolume_commands.sh
  # Old format CSIs:
  ./linstor-csi-migrator.sh csi > csi_commands.sh
  ```

* Create backup of your Persistent Volumes:

  ```
  kubectl get pv -o json > pv.json
  ```

* Now you can open `commands.sh` and apply the changes.
