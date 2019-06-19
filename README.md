This repo demonstrated how to do transparent proxy on MacOS. Just a POC.

Try to achive same result with iptables on linux (with `SO_ORIGINAL_DST`).

libkern and net are header files download from: https://github.com/opensource-apple/xnu

apply pf rules:

    sudo pfctl -f test

This test rule will redirect all outgoing tcp traffic originated 9.9.9.9:1234 to 127.0.0.1:8877, which our demo proxy server is listening.

Start server, will listen on 127.0.0.1:8877:

    sudo go run main.go


Test:

  curl  http://9.9.9.9:1234


will see server ouput:

    port 1234
    addr [9 9 9 9]


We get tcp connection's original target :)

References:

- https://github.com/go-freebsd/pf
