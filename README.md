# test-gunicorn

This is for reproducing the [gunicorn issue 1695](https://github.com/benoitc/gunicorn/issues/1695).

## How-to

Ensure `docker` and `docker-compose` are installed.

```bash script
git clone https://github.com/zhan9san/test-gunicorn.git
cd test-gunicorn
docker-compose up --build
```

Open another termial to test

```bash script
timeout 1 curl -I http://127.0.0.1:1337/
```

Here is the error log

```bash script
web_1    | [2021-03-24 07:50:53 +0000] [9] [DEBUG] HEAD /
nginx_1  | 192.168.0.1 - - [24/Mar/2021:07:50:54 +0000] "HEAD / HTTP/1.1" 499 0 "-" "curl/7.64.1"
web_1    | [2021-03-24 07:50:55 +0000] [9] [DEBUG] Ignoring EPIPE
```

It's weird that it cannot be reproduced by `echo -e 'HEAD /app HTTP/1.0\r\n\r\n' | nc -t 127.0.0.1 1337`.
