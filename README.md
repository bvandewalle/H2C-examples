# H2C-Examples

HTTP2-Cleartext (H2C) in go example.
[Based on this repo](https://github.com/thrawn01/h2c-golang-example/blob/master/cmd/server/main.go)

## HTTP/1.1:

```
$ curl localhost:8080 -v
*   Trying 127.0.0.1:8080...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 16 Sep 2022 17:18:11 GMT
< Content-Length: 10
< Content-Type: text/plain; charset=utf-8
< 
* Connection #0 to host localhost left intact
HTTP2 test
```


## HTTP2 Upgrade:
```
$ curl localhost:8080 -v --http2
*   Trying 127.0.0.1:8080...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.68.0
> Accept: */*
> Connection: Upgrade, HTTP2-Settings
> Upgrade: h2c
> HTTP2-Settings: AAMAAABkAARAAAAAAAIAAAAA
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 101 Switching Protocols
< Connection: Upgrade
< Upgrade: h2c
* Received 101
* Using HTTP2, server supports multi-use
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* Connection state changed (MAX_CONCURRENT_STREAMS == 250)!
< HTTP/2 200 
< content-type: text/plain; charset=utf-8
< content-length: 10
< date: Fri, 16 Sep 2022 17:18:16 GMT
< 
* Connection #0 to host localhost left intact
HTTP2 test
```

## HTTP2 Prior-Knowledge:
```
$ curl localhost:8080 -v --http2-prior-knowledge
*   Trying 127.0.0.1:8080...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
* Using HTTP2, server supports multi-use
* Connection state changed (HTTP/2 confirmed)
* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
* Using Stream ID: 1 (easy handle 0x5555cde9b2f0)
> GET / HTTP/2
> Host: localhost:8080
> user-agent: curl/7.68.0
> accept: */*
> 
* Connection state changed (MAX_CONCURRENT_STREAMS == 250)!
< HTTP/2 200 
< content-type: text/plain; charset=utf-8
< content-length: 10
< date: Fri, 16 Sep 2022 17:18:23 GMT
< 
* Connection #0 to host localhost left intact
HTTP2 test
```