# extfc-signal
Extfc-signal is a plugin for ext-fancontrol, which is designed for scenearios where temperature monoitors is spearate with controller, for example, an NVIDIA GPU with external fans passed through to a guest VM.

# How to use
```Sample of extfc-signal-config.json
{
    "address": "192.168.1.68",
    "port": 7654,
    "role": "client",
    "gpu": "nvidia"
}
```
## Roles
Extfc-signal has `server` and `client` role available.
A client is the machine which has control to target fans, and a server is the machine which has access to temperature data. 
For example, if you have a GPU with external fan passed through to a guest VM, the host would be client, and the guest VM would be server. This is based on the assumption that you are using a bridged network interface.
### Client
In client mode, `gpu` is ignored. The client connects to server for temperature data, and print it as stdout, which is ready to use by ext-fancontrol. If the server is unreachable, the data would always be 50.
### Server
In server mode, extfc-singal executes a command to fetch GPU temperature when accessed by client. 
Currently, only `NVIDIA` GPUs are supported. Feel free to open an issue if you would like support for `AMD` GPUs!
