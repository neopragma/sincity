# sincity development notes

## Platforms

This has only been used on Ubuntu Linux. If you run it on another \*nix platform, expect to find some incompatibilities that you will have to resolve. Please share the solutions. If you need to run this on Windows, use cygwin or a similar facility so you can run the bash scripts. There would be too much to change to make it worth the time to convert it to PowerShell.

The only _code_ to speak of is the bash script, ```sincity```.

## Test the skeleton website/service with cURL

Start the built-in server (after running sincity)

```shell
rackup
```

Check that the expected headers are returned

website

```shell
curl -I http://localhost:9292/
```

Expect:

```shell
HTTP/1.1 200 OK
Content-Type: text/html;charset=utf-8
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Length: 18
```

service

```shell
curl -s http://localhost:9292/json
```

Expect:

```shell
HTTP/1.1 200 OK
Content-Type: application/json
X-Content-Type-Options: nosniff
Content-Length: 31
```

Check that the return value is as expected

website

```shell
curl -s http://localhost:9292/
```

Expect:

```shell
Welcome to Sinatra
```

service

```shell
curl -s http://localhost:9292/json
```

Expect:

```shell
{"message":"Welcom to Sinatra"}
```
