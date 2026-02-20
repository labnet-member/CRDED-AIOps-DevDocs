# Raspberry Pi ノード情報一覧

このドキュメントでは，各大学に配布する Raspberry Pi の環境情報・OS バージョン・ネットワークインタフェース情報を記録

---

## 使用OS

**Raspberry Pi OS Lite (64-bit)**
```bash
$ cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.3
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

---

## ネットワーク情報一覧

各ノードのホスト名および WireGuard で利用する IP アドレス一覧を記載

| ホスト名 | WireGuard で利用する IP アドレス |
| -------- | ------------------------------- |
| `tokyo-mon01` | `10.0.0.2` |
| `hiro-mon01` | `10.0.0.3` |
| `oita-mon01` | `10.0.0.4` |
| `tottri-mon01` | `10.0.0.5` |
| `gumma-mon01` | `10.0.0.6` |