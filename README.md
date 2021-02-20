# helium-miner-snap

Miner for the helium blockchain. This snap requires multiple interfaces to
be connected before the miner daemon can start.

    snap connect helium-miner:i2c pi:i2c-1
    snap connect helium-miner:log-observe
    snap connect helium-miner:hardware-observe
    snap connect helium-miner:network-control

After connecting these interfaces the miner daemon will automatically start.
All variable data and log files are stored under /var/snap/helium-miner/common

To talk directly to the miner daemon you can use the shipped
nebra-helium-miner command like below.

    sudo nebra-helium-miner info summary

The genesis blockchain api can be found in
/var/snap/helium-miner/common/miner/update/genesis
You can use the "sudo nebra-helium-miner load genesis ..." command
pointing to that directory to load and update the blockchain api.

The miner daemon registers as com.helium.Miner to the system dbus of the host

## building

This snap is designed to be built on an arm64 device like a Pi4 using an Ubuntu Core or Classic install.

- install lxd and create a focal (20.04) lxd container

    ```
    $ sudo snap install lxd
    $ sudo lxd init --auto
    $ sudo lxc launch ubuntu:20.04 focal
    ```

- enter the container and install snapcraft

    ```
    $ sudo lxc shell focal
    # snap install snapcraft --classic
    ```

- clone this branch and build it

    ```
    # git clone https://github.com/ogra1/hm-miner-snap.git
    # cd hm-miner-snap
    # snapcraft --destructive-mode
    ...
    Snapped nebra-helium-miner_0.1.0_arm64.snap
    # exit
    $
    ```

- pull the file from the container

    ```
    $ lxc file pull focal/root/hm-miner-snap/nebra-helium-miner_0.1.0_arm64.snap .
    $ ls -lh nebra-helium-miner_0.1.0_arm64.snap
    -rw-r--r-- 1 ogra ogra 56M Feb 18 17:17 nebra-helium-miner_0.1.0_arm64.snap
    $
    ```
