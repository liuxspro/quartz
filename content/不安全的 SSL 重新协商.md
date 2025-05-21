---
title: 不安全的 SSL 重新协商
date: 2025-05-07T21:53
tags:
  - 编程
  - OpenSSL
---

在使用 curl 访问某网站的时候，出现`unsafe legacy renegotiation disabled`错误

```shell
curl: (35) OpenSSL/3.0.13: error:0A000152:SSL routines::unsafe legacy renegotiation disabled
```

该错误是由于客户端使用的 OpenSSL 禁用了不安全的传统 SSL 重新协商机制，而目标服务器仍在使用此旧方法所致。
OpenSSL 3.0 及以上版本 SSL 或 TLS 连接必须默认支持 RFC 5746 安全重新协商才能成功。需要连接到传统对等体的应用程序需要显式设置 `SSL_OP_LEGACY_SERVER_CONNECT`[^1]

可通过环境变量`OPENSSL_CONF`设置 Openssl 配置文件的路径[^2]，默认在`/etc/ssl/openssl.cnf`

这是一个最小的 OpenSSL 配置[^3]

```toml
openssl_conf = openssl_init

[openssl_init]
ssl_conf = ssl_sect

[ssl_sect]
system_default = system_default_sect

[system_default_sect]
Options = UnsafeLegacyServerConnect
```

> **UnsafeLegacyServerConnect** ：仅允许 OpenSSL 客户端使用不安全的传统重新协商。相当于  **SSL_OP_LEGACY_SERVER_CONNECT** 。[^4]

> [!warning] 注意:
> **启用旧式不安全重新协商时，SSL 连接将容易受到  [CVE-2009-3555](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CAN-2009-3555)  中所述的中间人攻击。**
> **最好解决方案是升级服务器 SSL 配置**

使用临时的配置文件: 

```bash
OPENSSL_CONF=/path/to/custom/openssl.cnf curl https://example.com
```

Python、Javascript 解决方案:

- python requests 请求解决方案 https://stackoverflow.com/questions/71603314/
- python urllib3 解决方案 https://github.com/urllib3/urllib3/issues/2653#issuecomment-1165418616
- javascript axios 请求解决方案 https://stackoverflow.com/questions/77046679/

> [!note] See Also:
>
> - [`unsafe legacy renegotiation disabled` error in specific website on Python 3.12](https://github.com/psf/requests/issues/6537#issuecomment-1732658849)
> - https://stackoverflow.com/questions/71603314/
> - [SSL不安全的旧版本重新协商 - https://lly.im](https://lly.im/posts/ssl不安全的旧版本重新协商/)

[^1]: https://docs.openssl.org/master/man7/ossl-guide-migration/#tls-changes
[^2]: https://docs.openssl.org/3.0/man3/OPENSSL_config/#environment
[^3]: https://stackoverflow.com/questions/75763525/curl-35-error0a000152ssl-routinesunsafe-legacy-renegotiation-disabled
[^4]: https://docs.openssl.org/3.0/man3/SSL_CONF_cmd/#supported-configuration-file-commands
