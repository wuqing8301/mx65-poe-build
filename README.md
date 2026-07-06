# Cisco Meraki MX65 / MX65W PoE OpenWrt 自动编译

GitHub Actions 自动编译 **Leo-PL/openwrt** 的 `meraki-mx65-poe` 分支，生成带 PoE PSE（BCM59111）支持的 MX65/MX65W 固件。

## 使用方法

1. Fork 本仓库 或 新建一个仓库把 `.github/workflows/build-mx65-poe.yml` 放进去
2. **手动触发**：仓库页面 → Actions → **Build MX65 PoE Firmware** → **Run workflow**
3. 等待约 30~90 分钟，编译完成后在 **Artifacts** 中下载：
   - `openwrt-bcm53xx-generic-meraki_mx65-squashfs-sysupgrade.bin`
   - `openwrt-bcm53xx-generic-meraki_mx65-initramfs-kernel.bin`

## 刷机步骤（简要）

1. 先刷自定义 U-Boot（clayface 的 `uboot_mx65`）到 MX65
2. 把 `initramfs-kernel.bin` 放 U 盘根目录，命名为 `openwrt-bcm53xx-generic-meraki_mx65-initramfs.bin`
3. 插入 U 盘 → 按住 Reset 上电 → 白灯闪 3 次 → 进 initramfs
4. `sysupgrade -n openwrt-bcm53xx-generic-meraki_mx65-squashfs-sysupgrade.bin`

## 配置说明

- 目标设备：`Cisco Meraki MX65 / MX65W`
- PoE 驱动：`kmod-bcm59111-pse`
- 含 LuCI Web 界面 + SSL
- 基于 Leo-PL 的 `meraki-mx65-poe` 分支
