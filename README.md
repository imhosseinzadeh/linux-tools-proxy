# How to configure proxy for Linux tools

# ============ System-Wide Proxy ============

vi ~/.profile

export "http_proxy=http://127.0.0.1:10809"

export "https_proxy=http://127.0.0.1:10809"

export "no_proxy=localhost, ::1,127.0.0.1"

source ~/.profile

# ============ apt pacakge manager ============

sudo nano /etc/apt/apt.conf

=== PASTE THIS ===

Acquire::http::Proxy "http://127.0.0.1:10809";

Acquire::https::Proxy "http://127.0.0.1:10809";

Acquire::socks&zwnj;::Proxy "http://127.0.0.1:10808";

Acquire::ftp::Proxy "http://127.0.0.1:10808";

# ============ snap pacakge manager ============

sudo snap set system proxy.http="http://<proxy_addr>:<proxy_port>"

sudo snap set system proxy.https="http://<proxy_addr>:<proxy_port>"

sudo snap set system proxy.ftp="http://<proxy_addr>:<proxy_port>"

*Available since snapd 2.28.

# ============ Git ============

If your proxy does not require authentication:

git config --global http.proxy https://YOUR.PROXY.SERVER:8080

*Replace YOUR.PROXY.SERVER with you proxy's URL

If your proxy does require authentication:

git config --global http.proxy https://YOUR_PROXY_USERNAME:YOUR_PROXY_PASSWORD@YOUR.PROXY.SERVER:8080

*Replace YOUR_PROXY_USERNAME with the username used to authenticate into your proxy, YOUR_PROXY_PASSWORD with the
password used to authenticate into your proxy, and YOUR.PROXY.SERVER with your proxy's URL
