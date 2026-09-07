| 场景              | 命令                            | 作用                                     | 例子                                    |
| --------------- | ----------------------------- | -------------------------------------- | ------------------------------------- |
| 安装命令行工具         | `brew install <软件名>`          | 安装 Formula，通常是 CLI 工具、库、运行环境           | `brew install wget`                   |
| 安装 macOS 图形应用   | `brew install --cask <软件名>`   | 安装 Cask，通常是 `.app`、`.dmg`、`.pkg` 类型的软件 | `brew install --cask google-chrome`   |
| 卸载命令行工具         | `brew uninstall <软件名>`        | 卸载 Formula                             | `brew uninstall wget`                 |
| 卸载 macOS 图形应用   | `brew uninstall --cask <软件名>` | 卸载 Cask 应用                             | `brew uninstall --cask google-chrome` |
| 搜索软件            | `brew search <关键词>`           | 搜索可安装的 Formula 和 Cask                  | `brew search chrome`                  |
| 查看软件信息          | `brew info <软件名>`             | 查看版本、依赖、安装位置等                          | `brew info wget`                      |
| 查看 Cask 信息      | `brew info --cask <软件名>`      | 查看图形应用的 Cask 信息                        | `brew info --cask visual-studio-code` |
| 更新 Homebrew 软件源 | `brew update`                 | 更新 Homebrew 自身的软件包索引                   | `brew update`                         |
| 升级已安装的软件        | `brew upgrade`                | 升级已安装的 Formula                         | `brew upgrade`                        |
| 升级某个 Cask 应用    | `brew upgrade --cask <软件名>`   | 升级指定的 macOS 应用                         | `brew upgrade --cask firefox`         |
| 查看已安装的命令行工具     | `brew list`                   | 列出已安装 Formula                          | `brew list`                           |
| 查看已安装的 Cask     | `brew list --cask`            | 列出已安装的 macOS 图形应用                      | `brew list --cask`                    |
| 添加第三方软件仓库       | `brew tap <仓库>`               | 添加额外的软件源                               | `brew tap homebrew/cask-fonts`        |
| 清理旧版本           | `brew cleanup`                | 删除旧版本和缓存，释放空间                          | `brew cleanup`                        |