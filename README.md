# x365

x365 是一套基于 X365 协议的开源 VPN 客户端集合（monorepo，通过
git submodule 组织），完全独立开发，与任何第三方 VPN 服务商
（包括名称相近的服务商）没有任何隶属、授权或合作关系。
本项目不捆绑任何服务器节点或账号凭证。

## 子仓库

| 子仓 | 说明 | 构建 |
| --- | --- | --- |
| [x365-core](https://github.com/SakurakaiCat/x365-core) | X365 协议核心：REALITY TLS 握手、gRPC 风格 chunked 隧道、SOCKS5 入口、`x365://` URI 解析（Go module `github.com/SakurakaiCat/x365-core`） | `go build ./...` |
| [x365-cli](https://github.com/SakurakaiCat/x365-cli) | 账号登录并导出 `x365://` 节点链接（Go CLI + Python 参考实现） | `go build ./x365-cli` / `python3 python-cli/x365.py --help` |
| [x365-desktop](https://github.com/SakurakaiCat/x365-desktop) | Windows 桌面客户端（Wails + Wintun tun2socks） | 见仓内 README |
| [x365-mobile](https://github.com/SakurakaiCat/x365-mobile) | gomobile 绑定（Android 客户端的 Go 层） | `gomobile bind` |
| [x365-android](https://github.com/SakurakaiCat/x365-android) | Android 客户端（VpnService + hev-socks5-tunnel） | 见仓内 README |

克隆：

```sh
git clone --recurse-submodules https://github.com/SakurakaiCat/x365.git
```

## 协议概览

X365 协议的完整描述见 [x365-core/README.md](x365-core/README.md)：SOCKS5 →
HTTP/1.1 chunked 分帧（gRPC 语义外观）→ X365 二进制头（寻址 + 认证）
→ TLS 1.3 + REALITY 握手。

账号服务接入协议（登录、取节点）的摘要见
[x365-cli/x365-cli/README.md](x365-cli/x365-cli/README.md)。

## License

MIT，详见 [LICENSE](LICENSE)。

## 免责声明

本项目仅供学习与研究网络协议使用。使用者应遵守所在地区的法律法规，
本项目作者不对任何使用行为承担责任。
