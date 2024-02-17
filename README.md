# Configuring Proxy for Linux Tools

#### Note: Replace <proxy_addr> and <proxy_port> with your proxy server address and port respectively.

## System-Wide Proxy

To set up a system-wide proxy configuration:

1. Open `~/.profile` in your preferred text editor:

    ```bash
    vi ~/.profile
    ```

2. Add the following lines at the end of the file:

    ```bash
    export http_proxy=http://127.0.0.1:10809
    export https_proxy=http://127.0.0.1:10809
    export no_proxy=localhost,::1,127.0.0.1
    ```

3. Apply the changes:

    ```bash
    source ~/.profile
    ```

## APT Package Manager

To configure the APT package manager:

1. Open `/etc/apt/apt.conf` with root privileges:

    ```bash
    sudo vi /etc/apt/apt.conf
    ```

2. Paste the following configuration:

   ```plaintext
   Acquire::http::Proxy "http://proxy_server_address:proxy_port";
   Acquire::https::Proxy "http://proxy_server_address:proxy_port";
   ```
3. Save the file and exit.

## DNF Package Manager

To configure the DNF package manager:

1. Open /etc/dnf/dnf.conf with root privileges:

   ```bash
   sudo vi /etc/dnf/dnf.conf
   ```

2. Add or modify the following lines in the [main] section:

   ```plaintext
   proxy=http://<proxy_addr>:<proxy_port>
   ```

3. Save the file and exit.

## Snap Package Manager

To set proxy settings for the Snap package manager:

```bash
sudo snap set system proxy.http="http://proxy_server_address:proxy_port"
sudo snap set system proxy.https="http://proxy_server_address:proxy_port"
```

## Git

To configure Git with or without authentication for proxy:

Without authentication:

```bash
git config --global http.proxy http://proxy_server_address:proxy_port
git config --global https.proxy https://proxy_server_address:proxy_port
```

If your proxy requires authentication, you can include your username in the URL:

```bash
git config --global http.proxy http://username@proxy_server_address:proxy_port
git config --global https.proxy https://username@proxy_server_address:proxy_port
```

**Verify the configuration**: You can verify that the proxy settings are correctly configured by checking your Git
configuration:

```bash
git config --global --get http.proxy
git config --global --get https.proxy
```

**Unset proxy configuration**: If you want to remove the proxy configuration, you can unset it using:

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

This will revert Git to using no proxy.
