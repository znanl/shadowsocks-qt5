Shadowsocks-Qt5
===============

[中文用户指南](https://github.com/librehat/shadowsocks-qt5/wiki/%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97)

Introduction
------------

Shadowsocks-Qt5 is a native and cross-platform GUI client for [Shadowsocks](http://shadowsocks.org).

Features
--------

- Shadowsocks-Qt5 is written in C++/Qt5.
- Intuitive and **native** UI. This is **not** a clumsy Web App.
- Keep your favourite Shadowsocks port as backend if you want.
- Easy-to-use and highly customisable.
- The `gui-config.json` file is partially compatible with [shadowsocks-gui](https://github.com/shadowsocks/shadowsocks-gui). In order to serve better, some new values have been added.
- `gui-config.json` is located under ~/.config/shadowsocks on UNIX platforms, or under the main programme's directory on Windows.

Note
----

- By default, `ss-qt5` works with `libQtShadowsocks` which is considered as a reliable and lightweight alternative. While you can still use other shadowsocks backends such as [Shadowsocks-libev] [ss-libev] and [Shadowsocks-Python] [ss-python].
- If `ss-qt5` crashes and the single-instance mode is on, you may need to manually delete `/tmp/qipc_sharedmemory_shadowsocksqt*` and `/tmp/qipc_systemsem_shadowsocksqt*`. Otherwise, `ss-qt5` will complain that another instance is already running.
- Don't be panic if you encounter a bug. Please feel free to open [issues](https://github.com/librehat/shadowsocks-qt5/issues). Just remember to run from terminal or `cmd` and paste the output to the description of issue.

Installation
------------

### Windows ###

Download prebuilt binaries from [releases](https://github.com/librehat/shadowsocks-qt5/releases).

For those who want to build from source, follow the instructions below.

Open this project using Qt Creator and build it.

Or type the command in MSYS/MinGW.

```bash
qmake INSTALL_PREFIX=../ss-qt5
make
make install
```

You will get `ss-qt5.exe` and `gui-config.json` in ../ss-qt5 directory.

For 64-bit build, please use mingw-w64 toolchain (there are unofficial Qt builds using mingw-w64) and use the command below instead.

```bash
qmake INSTALL_PREFIX=../ss-qt5 DEFINES+="mingw64"
make
make install
```

### Linux ###

We build `ss-qt5` in a dynamically linking style on UNIX platfroms, which means there'll be some dependencies to be solved.

#### Dependencies ####

- `qt5-qtbase` >= 5.2
- `qrencode` (or `libqrencode` in Debian/Ubuntu)
- `libQtShadowsocks` >= 1.4.0 (`libqtshadowsocks` in Debian/Ubuntu)
- `botan` >= 1.10 (`libbotan1.10` in Debian/Ubuntu)
- `zbar` (`libzbar0` in Debian/Ubuntu)
- `libappindicator1` (optional, only if you want to build with `appindicator` support)

Your C++ compiler must has a good support for C++11.

#### Fedora/Red Hat Enterprise Linux ####

The Copr builds RPMs for Fedora 20, 21, rawhide and RHEL 7. If you're using other RHEL-based distributions such as CentOS and Scientific Linux, you can just use the EPEL repo in Copr.

You can enable the repo via `dnf`:

```bash
sudo dnf copr enable librehat/shadowsocks
sudo dnf update
sudo dnf install shadowsocks-qt5
```

You may need to install dnf plugins by below command before you can enable copr repo.

```bash
sudo dnf install dnf-plugins-core
```

If your distribution doesn't have `dnf`, you can download the corresponding yum repo from [Copr](https://copr.fedoraproject.org/coprs/librehat/shadowsocks/) and put it under `/etc/yum.repos.d/`, then install `shadowsocks-qt5` via `yum`:

```bash
sudo yum update
sudo yum install shadowsocks-qt5
```

#### Ubuntu ####

PPA is for Ubuntu >= 14.04. And you need to use Unity or LXDE, other DEs are untested. If you encouter segmentation fault with `Gdk-CRITICAL **` in other DEs, please follow instructions in **Debian** section to build `ss-qt5` without `UBUNTU_UNITY` support.

```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

If you want to build it manually with Unity support, add `DEFINES+="UBUNTU_UNITY"` to `qmake` to enable `appindicator` support.

#### Debian ####

Since `v0.9`, the `debian` directory needs two modifications to get rid of Ubuntu Unity support.

1. Edit `debian/rules`, remove `DEFINES+="UBUNTU_UNITY"` from `qmake`.
2. Edit `debian/control`, delete `libappindicator-dev,` (line 12).

Now run the command below, you'll get a deb package in upper directory.

```bash
dpkg-buildpackage -uc -us -b
```

Then, install it by `sudo dpkg -i shadowsocks-qt5-<VER_ARCH_ETC>.deb`.

#### Generic Linux ####

The **development packages** of `qt5-qtbase`, `botan-1.10` (or `libbotan1.10`), `libQtShadowsocks` and `qrencode` (or `libqrencode`) are required.

```bash
# Some distros use seperated qmake-qt4, qmake-qt5. Then, just run `qmake-qt5`. You can specify INSTALL_PREFIX=/usr/local if needed. default is /usr
qmake INSTALL_PREFIX=/usr
make
make install
```

### Others ###

Other platforms are not tested and they're NOT supported officially. Well, I do hope you can help me mantain the compatibility if you have spare time.

[ss-python]: https://github.com/clowwindy/shadowsocks
[ss-libev]: https://github.com/shadowsocks/shadowsocks-libev

LICENSE
-------

Copyright © 20014-2015 Symeon Huang

This project is licensed under version 3 of the GNU Lesser General Public License.
