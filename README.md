# Haproxy 443 port share configure

a haproxy config file that allow ssh、shadowsocks、ocserv、nginx share 443(https) port.

* haproxy 接管 443 端口，其他程序监听本机的其他端口
* 通过 ssl 握手和 sni 匹配 https 请求转发到 nginx 其他 ssl 握手请求转发 ocserv
* ssh 的连接有固定的开头(SSH-2.0)，虽然规定了由服务端先声明，但仍然有客户端会在连接建立后直接声明，所以不仅要用标识出等待”SSH-2.0“字符串的(req.len == 0)，也需要标识出客户端直接发送”SSH-2.0”的
* shadowsocks 没有请求特征，但请求体一定不为 0
