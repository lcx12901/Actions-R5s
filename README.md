# [OpenWrt-Cache](https://github.com/SuLingGG/OpenWrt-Cache)

## 项目介绍

本项目旨在生成 OpenWrt 工具链 (toolchain) 并将工具链缓存至 Release。

本项目有以下特性:

- 一键生成多平台工具链并自动发布至本仓库 Release
- 在 Github Action 流程中可节省 30~40 分钟的 tools & toolchain 编译时间
- 提供适用于本项目工具链缓存的 Github Action [示例文件](https://github.com/SuLingGG/OpenWrt-Toolchain/blob/main/.github/workflows/coolsnowwolf-lede-example.yml)

## 生成工具链

- Fork 本项目，在 config 文件夹内创建以设备 `target/subtarget.config` 为 `路径/文件名` 命名的 OpenWrt 目标平台配置文件。

  以树莓派 4 为例： `config/bcm27xx/bcm2711.config`

  `bcm2711.config` 文件内容:

  ```
  CONFIG_TARGET_bcm27xx=y
  CONFIG_TARGET_bcm27xx_bcm2711=y
  CONFIG_TARGET_bcm27xx_bcm2711_DEVICE_rpi-4=y
  ```

- 在 [workflows 文件](https://github.com/SuLingGG/OpenWrt-Toolchain/blob/main/.github/workflows/coolsnowwolf-lede-master-toolchain.yml) 的 全局变量 `env` 中指定欲使用的 OpenWrt 源码项目地址 `SOURCE_URL`、项目分支 `SOURCE_BRANCH`，在矩阵变量 `matrix` 中配置设备平台字段 `PLATFORM`，使 `PLATFORM` 字段与上文 `target/subtarget` 字段相对应。

  以树莓派4 为例：`PLATFORM: [bcm27xx/bcm2711]`

- 如果你想生成多平台工具链缓存，需分别配置各个设备的目标平台配置文件，并正确配置矩阵变量 `matrix` :

  配置文件:

  `config/bcm27xx/bcm2711.config`、`config/rockchip/armv8.config`、`config/x86/64.config`

  矩阵变量:

  `PLATFORM: [bcm27xx/bcm2711, rockchip/armv8, x86/64]`

- 在 Action 页面 [触发工具链编译](https://p3terx.com/archives/github-actions-manual-trigger.html#toc_7)。

## Credits

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License
