# 设置HTTPS请求 {#concept_mws_3dl_zdb .concept}

阿里云Python SDK支持使用HTTP和HTTPS协议发起 API 请求。大部分产品使用HTTP协议，但访问控制\(RAM\)，安全令牌 \(STS\) 和密钥管理 \(KMS\) 等产品默认使用HTTPS协议发起API请求。

使用Python SDK时，您可以为某个请求指定使用HTTP或HTTPS协议，您也可以设置全局默认协议。

**说明：** 产品的默认协议（HTTP/HTTPS）优先于设置的全局默认协议。此外，访问控制 \(RAM\)，安全令牌 \(STS\) 和密钥管理 \(KMS\) 的默认协议为 HTTPS，不能使用 HTTP 协议。

## 添加OpenSSL依赖 {#section_ad3_rkl_zdb .section}

阿里云Python SDK的HTTPS协议依赖Python的OpenSSL支持。要使用阿里云 SDK通过HTTPS协议发送请求，您需要在 Python 中添加 OpenSSL 支持。

运行`python -c "import ssl"`查看Python环境是否支持OpenSSL。运行后，如果没有出现

`ImportError: No module named ssl`的错误信息，说明已经支持OpenSSL。

若没有OpenSSL支持，运行以下命令安装：

```
pip install pyopenssl
```

## 设置单个请求的HTTP/HTTPS协议 {#section_a3b_dnl_zdb .section}

参考以下代码示例为一个接口设置HTTPS调用：

```
request = CreateInstanceRequest.CreateInstanceRequest()
request.set_protocol_type("https")
# 取值："https" 或 "http"
```

## 设置全局默认协议 {#section_nkx_snl_zdb .section}

参考以下代码示例设置全局默认协议：

```
import aliyunsdkcore.request
aliyunsdkcore.request.set_default_protocol_type("https")
# 创建请求并调用 client.do_action_with_exception() 来发送请求
```

