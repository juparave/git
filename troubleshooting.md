## git trobleshooting

### Network

In MacOs sometimes disabling IPv6 may fix some connectivity issues

    $ networksetup -listnetworkserviceorder
    $ networksetup -setv6off Ethernet

or if you're using wifi

    $ networksetup -setv6off Wi-Fi

#### fatal: could not read Username for 'https://github.com': terminal prompts disabled

    $ git config --global --add url."git@github.com:".insteadOf "https://github.com/"

Resulting in `.gitconfig` will be like:

```
[url "git@github.com:"]
    insteadOf = https://github.com/
```

