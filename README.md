# Droidspaces Environment Setup & Kernel Notes

A minimal setup guide and reference note for setting up an Alpine Linux container inside Droidspaces.

---

### 📦 Essential Links

* **RootFS Builder:** [Droidspaces-rootfs-builder Releases](https://github.com/Droidspaces/Droidspaces-rootfs-builder/releases/latest)
* **Droidspaces App:** [Droidspaces-OSS Releases](https://github.com/ravindu644/Droidspaces-OSS/releases/latest)

---

### 🛠️ 1. Tools Installation & Base Setup

Run these commands right after spinning up a fresh Alpine container:

```bash
# Update repositories & install required packages
apk update && apk add git python3 py3-pip patch diffutils tree neovim unzip wget bash curl tzdata

# Set System Timezone (WIB)
cp /usr/share/zoneinfo/Asia/Jakarta /etc/localtime

# Configure Git Identity
git config --global user.name "YourName"
git config --global user.email "your.email@example.com"
```

---

### 🌐 2. Clone Main Kernel Repositories

Fetch shallow kernel trees (`--depth=1` to save mobile storage and speed up downloading):

```bash
# Android GKI Common (5.15)
git clone --recursive --branch android13-5.15-lts https://android.googlesource.com/kernel/common gki-common --depth=1

# Android GKI Compat (5.15.123)
git clone --recursive --branch deprecated/android13-5.15-2023-10 https://android.googlesource.com/kernel/common gki-compat --depth=1

sleep 5

# Qualcomm CLO MSM (5.15)
git clone --recursive --branch kernel.lnx.5.15.r1-rel https://git.codelinaro.org/clo/la/kernel/msm-5.15 clo-common --depth=1
```

---

### 🧹 Quick Clean Up

Clean uncommitted changes or reset tracking in local kernel directories:

```bash
git reset --hard HEAD && git clean -fd
```
