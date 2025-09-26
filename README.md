# frp-action-win
Debug github Action with frp tunnel


## How to use

### 1. Deploy frp server

frp repository: https://github.com/fatedier/frp

- frps.toml demo
```toml
bindPort = 20000
auth.token = "your_token"

# must be true
transport.tls.force = true
```

### 2. Add Github Action secret

- FRP_SERVER_ADDR
- FRP_SERVER_PORT
- FRP_TOKEN

### 3. Use the github Action

a action demo windows-2022 is in the `.github/workflows/windows-2022.yml`

```yaml
jobs:
  debug:
    name: Debug github Action with frp tunnel
    runs-on: windows-2022
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Debug github Action with frp tunnel
        uses: neighbads/frp-action-win@main
        with:
          frp_server_addr: ${{ env.FRP_SERVER_ADDR }}
          frp_server_port: ${{ env.FRP_SERVER_PORT }}
          frp_token: ${{ env.FRP_TOKEN }}
          remote_port: ${{ env.FRP_REMOTE_PORT }}
```

### 4. Run the github Action

![run the github Action](/images/run_the_github_action.png)

### 5. Connect to the action runner

use `mstsc` to connect to the action runner

- username: admin
- password: found in the github Action output
