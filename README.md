# Open365VPN

Open365VPN 是一套基于 X365 协议的开源 VPN 客户端集合，完全独立开发，
与任何第三方 VPN 服务商（包括名称相近的服务商）没有任何隶属、
授权或合作关系。本项目不捆绑任何服务器节点或账号凭证。

## 目录结构

```
x365/
├── core/            X365 协议核心（Go 参考实现）
├── cmd/x365-cli/    命令行工具：账号登录、导出节点链接
├── cli/             命令行工具的 Python 参考实现
├── desktop/         Windows 桌面客户端（Wails + Wintun tun2socks）
├── android/         Android 客户端（VpnService + hev-socks5-tunnel）
└── mobile/          gomobile 绑定（Android 客户端的 Go 层）
```

Go module 统一为 `github.com/365vpn/x365`；`desktop/` 与 `mobile/`
因构建工具链（Wails / gomobile）要求各自持有独立的 `go.mod`，
通过 `replace github.com/365vpn/x365 => ..` 引用本仓库协议核心。

## 组件

| 目录 | 说明 | 构建 |
| --- | --- | --- |
| `core/` | X365 协议核心：REALITY TLS 握手、gRPC 风格 chunked 隧道、SOCKS5 入口、`x365://` URI 解析 | `go build ./...` |
| `cmd/x365-cli/` | 账号登录并导出 `x365://` 节点链接的 CLI | `go build -o x365 ./cmd/x365-cli` |
| `cli/` | 同上功能的 Python 实现（无第三方依赖） | `python3 cli/x365.py --help` |
| `desktop/` | Windows 桌面客户端 | 见 [desktop/README.md](desktop/README.md) |
| `android/` | Android 客户端 | 见 [android/README.md](android/README.md) |
| `mobile/` | gomobile 绑定（生成 Android 使用的 AAR） | 见 [android/README.md](android/README.md) |

## 协议概览

X365 协议的完整描述见 [core/README.md](core/README.md)：SOCKS5 →
HTTP/1.1 chunked 分帧（gRPC 语义外观）→ X365 二进制头（寻址 + 认证）
→ TLS 1.3 + REALITY 握手。

账号服务接入协议（登录、取节点）的摘要见
[cmd/x365-cli/README.md](cmd/x365-cli/README.md)。

## License

MIT，详见 [LICENSE](LICENSE)。

## 免责声明

本项目仅供学习与研究网络协议使用。使用者应遵守所在地区的法律法规，
本项目作者不对任何使用行为承担责任。
