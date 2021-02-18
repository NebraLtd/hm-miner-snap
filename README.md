# helium-miner-snap
Alternate software solution

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
