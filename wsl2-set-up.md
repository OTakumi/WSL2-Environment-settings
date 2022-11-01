---
description: WSL2の初期設定の手順
---

# WSL2 Set up

ユーザー名と、パスワードを設定後に、UpdateとUpgradeを行う

```
sudo apt update
sudo apt upgrade
```

ライブラリをインストールする。

### Git

```
// Install cmd
sudo apt-get install git
```

### **NeoVim**

インストール手順：[https://github.com/neovim/neovim/wiki/Installing-Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim)

**Ubuntu**

As in Debian, Neovim is in [Ubuntu](https://packages.ubuntu.com/search?keywords=neovim).

```
sudo apt install neovim
```

Neovim has been added to a "Personal Package Archive" (PPA). This allows you to install it with `apt-get`. Follow the links to the PPAs to see which versions of Ubuntu are currently available via the PPA. Choose **stable** or **unstable**:

* [https://launchpad.net/\~neovim-ppa/+archive/ubuntu/**stable**](https://launchpad.net/\~neovim-ppa/+archive/ubuntu/stable)
* [https://launchpad.net/\~neovim-ppa/+archive/ubuntu/**unstable**](https://launchpad.net/\~neovim-ppa/+archive/ubuntu/unstable)

**Important:** The Neovim team does not maintain the PPA packages. For problems or questions about the PPA specifically contact [https://launchpad.net/\~neovim-ppa](https://launchpad.net/\~neovim-ppa).

To be able to use **add-apt-repository** you may need to install software-properties-common:

```
sudo apt-get install software-properties-common
```

Run the following commands:

```
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
```

Prerequisites for the Python modules:

```
sudo apt-get install python-dev python-pip python3-dev python3-pip
```

If you're using an older version Ubuntu you must use:

```
sudo apt-get install python-dev python-pip python3-dev
sudo apt-get install python3-setuptools
sudo easy_install3 pip
```

For instructions to install the Python modules, see [`:help provider-python`](https://neovim.io/doc/user/provider.html#provider-python).

If you want to use Neovim for some (or all) of the editor alternatives, use the following commands:

```
sudo update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
sudo update-alternatives --config vi
sudo update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
sudo update-alternatives --config vim
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
sudo update-alternatives --config editor
```

Note, however, that special interfaces, like `view` for `nvim -R`, are not supported. (See [#1646](https://github.com/neovim/neovim/issues/1646) and [#2008](https://github.com/neovim/neovim/pull/2008).)

### Nodejs

Install Nodejs

```
sudo apt install nodejs
```

Version check

```
node -v
```

### Rust

{% embed url="https://www.rust-lang.org/tools/install" %}

#### Windows Subsystem for Linux

If you’re a Windows Subsystem for Linux user run the following in your terminal, then follow the on-screen instructions to install Rust.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

restart and version check

```
rustc --version
```

### Go

{% embed url="https://go.dev/" %}

```
// Install cmd
sudo apt install golang-go
```

以下の情報は古い

~~式サイトから任意のバージョンのインストーラをダウンロードする。~~

```
wget https://go.dev/dl/go1.19.2.linux-amd64.tar.gz
```

~~usr/localにファイルを展開する。~~

```
tar -C /usr/local -xzf go1.15.3.linux-amd64.tar.gz
```

### zsh

```
// Installcmd
sudo apt install -y zsh
```

### Docker

{% embed url="https://docs.docker.com/engine/install/ubuntu/" %}

systemdでdockerを起動するため、wslの設定ファイルを追加する。

{% code title="/etc/wsl.conf" %}
```
[boot]
systemd=true
```
{% endcode %}

WSL2を再起動後、systemdの状態を確認する。

```
~  ps ax
    PID TTY      STAT   TIME COMMAND
      1 ?        Ss     0:00 /sbin/init
      2 ?        Sl     0:00 /init
      5 ?        Sl     0:00 plan9 --control-socket 7 --log-level 4 --server-fd 8 --log-truncate
     50 ?        S<s    0:00 /lib/systemd/systemd-journald
     74 ?        Ss     0:00 /lib/systemd/systemd-udevd
     84 ?        Ss     0:00 /lib/systemd/systemd-networkd
    267 ?        Ss     0:00 snapfuse /var/lib/snapd/snaps/lxd_22526.snap /snap/lxd/22526 -o ro,nodev,
    268 ?        Ss     0:00 snapfuse /var/lib/snapd/snaps/snapd_14978.snap /snap/snapd/14978 -o ro,no
    269 ?        Ss     0:00 snapfuse /var/lib/snapd/snaps/core20_1361.snap /snap/core20/1361 -o ro,no
    276 ?        Ss     0:00 /lib/systemd/systemd-resolved
    280 ?        Ssl    0:00 /usr/lib/accountsservice/accounts-daemon
    281 ?        Ss     0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --s
    285 ?        Ss     0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
    287 ?        Ssl    0:00 /usr/lib/policykit-1/polkitd --no-debug
    288 ?        Ssl    0:00 /usr/sbin/rsyslogd -n -iNONE
    289 ?        Ssl    0:00 /usr/lib/snapd/snapd
    292 ?        Ss     0:00 /lib/systemd/systemd-logind
    293 ?        Ssl    0:00 /usr/lib/udisks2/udisksd
    317 ?        Ssl    0:00 /usr/sbin/ModemManager
    331 ?        Ss     0:00 /usr/sbin/cron -f
    344 ?        Ssl    0:00 /usr/bin/containerd
    351 ?        Ssl    0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdo
    353 pts/0    Ss+    0:00 /sbin/agetty -o -p -- \u --noclear --keep-baud console 115200,38400,9600
    357 ?        Ss     0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
    362 tty1     Ss+    0:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
    409 ?        Ssl    0:00 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
    501 ?        S      0:00 /lib/systemd/systemd-udevd
    502 ?        S      0:00 /lib/systemd/systemd-udevd
    503 ?        S      0:00 /lib/systemd/systemd-udevd
    504 ?        S      0:00 /lib/systemd/systemd-udevd
    505 ?        S      0:00 /lib/systemd/systemd-udevd
    506 ?        S      0:00 /lib/systemd/systemd-udevd
    507 ?        S      0:00 /lib/systemd/systemd-udevd
    508 ?        S      0:00 /lib/systemd/systemd-udevd
    509 ?        S      0:00 /lib/systemd/systemd-udevd
    510 ?        S      0:00 /lib/systemd/systemd-udevd
    511 ?        S      0:00 /lib/systemd/systemd-udevd
    512 ?        S      0:00 /lib/systemd/systemd-udevd
    513 ?        S      0:00 /lib/systemd/systemd-udevd
    514 ?        S      0:00 /lib/systemd/systemd-udevd
    515 ?        S      0:00 /lib/systemd/systemd-udevd
    516 ?        S      0:00 /lib/systemd/systemd-udevd
    517 ?        S      0:00 /lib/systemd/systemd-udevd
    518 ?        S      0:00 /lib/systemd/systemd-udevd
    519 ?        S      0:00 /lib/systemd/systemd-udevd
    520 ?        S      0:00 /lib/systemd/systemd-udevd
    521 ?        S      0:00 /lib/systemd/systemd-udevd
    522 ?        S      0:00 /lib/systemd/systemd-udevd
    530 ?        S      0:00 /lib/systemd/systemd-udevd
    556 ?        S      0:00 /lib/systemd/systemd-udevd
    562 ?        S      0:00 /lib/systemd/systemd-udevd
    574 ?        S      0:00 /lib/systemd/systemd-udevd
    582 ?        S      0:00 /lib/systemd/systemd-udevd
    583 ?        S      0:00 /lib/systemd/systemd-udevd
    585 ?        S      0:00 /lib/systemd/systemd-udevd
   1174 ?        Ss     0:00 /lib/systemd/systemd-timedated
   1221 ?        Ss     0:00 /init
   1222 ?        S      0:00 /init
   1223 pts/1    Ss     0:00 -zsh
   1224 pts/2    Ss     0:00 /bin/login -f
   1380 ?        Ss     0:00 /lib/systemd/systemd --user
   1382 ?        S      0:00 (sd-pam)
   1389 pts/2    S+     0:00 -zsh
   1415 pts/1    R+     0:00 ps ax
```

Dockerの動作確認を行う。

```
sudo systemctl start docker

sudo docker run hello-world
```

以下のようなエラーが発生した場合、Dockerが起動しているかを確認する。

```
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
See 'docker run --help'.
```

{% embed url="https://docs.docker.com/config/daemon/systemd/" %}

### Kubernetes

{% embed url="https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/" %}

{% embed url="https://qiita.com/XPT60/items/ef9fbe82127b5b559b44" %}

### minikube

{% embed url="https://minikube.sigs.k8s.io/docs/start/" %}

仮想化環境はQEMU2を使用する。

{% embed url="https://hiro20180901.hatenablog.com/entry/2022/02/26/160000" %}

QEMU2の動作確認は、動作場所を指定する必要があるので、以下のコマンドで起動を確認する。

```
kvm -m 2048 -cpu host
```

kvm2を使用して、minikubeを起動する。

{% embed url="https://minikube.sigs.k8s.io/docs/drivers/kvm2/" %}

{% embed url="https://blog.bobuhiro11.net/2020/11-04-kvm-on-wsl2.html" %}

{% embed url="https://help.ubuntu.com/community/KVM/Installation" %}

### containerd

### Oh My zsh

{% embed url="https://ohmyz.sh/" %}

#### Basic Installation

Oh My Zsh is installed by running one of the following commands in your terminal. You can install this via the command-line with either `curl`, `wget` or another similar tool.

| Method    | Command                                                                                           |
| --------- | ------------------------------------------------------------------------------------------------- |
| **curl**  | `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |
| **wget**  | `sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`   |
| **fetch** | `sh -c "$(fetch -o - https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |

_Note that any previous `.zshrc` will be renamed to `.zshrc.pre-oh-my-zsh`. After installation, you can move the configuration you want to preserve into the new `.zshrc`._

{% embed url="https://github.com/ohmyzsh/ohmyzsh/wiki/Themes" %}

テーマを決めて、適用する。

”kafeitu”が良さげ

In order to enable a theme, set `ZSH_THEME` to the name of the theme in your `~/.zshrc`, before sourcing Oh My Zsh; for example: `ZSH_THEME=robbyrussell` If you do not want any theme enabled, just set `ZSH_THEME` to blank: `ZSH_THEME=""`
