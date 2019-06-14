# Dockerize V2Ray with Nginx, Websocket and TLS

## Features
- V2Ray WebSocket with TLS
- Automated HTTPS certificate renewal by [Certbot](https://certbot.eff.org/)

## Get Started
1. Clone the source code
2. Make `init.sh` executable by executing `chmod +ax init.sh`
3. Execute `./init.sh`
4. Follow the instructions 
5. Done & enjoy v2ray :P

## Advanced Usage
- To modify v2ray settings, please modify `data/v2ray/config.json` and restart docker
- To modify default landing page `https://{{domain}}/index.html`, please modify `data/nginx/www/index.html`and restart docker

---

## Default v2ray config
``` json
{
  "logs": {
        "access": "/etc/v2ray/access.log",
        "error": "/etc/v2ray/error.log",
        "loglevel": "warning"
  },
  "inbounds": [{
    "port": 10086,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "{{UUID}}",
          "level": 1,
          "alterId": 64,
          "security": "auto"
        }
      ]
    },
"streamSettings":{
    "network":"ws",
    "security": "auto",
    "wsSettings":{
        "path": "{{v2ray Path}}"
      }
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  },{
    "protocol": "blackhole",
    "settings": {},
    "tag": "blocked"
  }],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": [
            "0.0.0.0/8",
            "10.0.0.0/8",
            "100.64.0.0/10",
            "127.0.0.0/8",
            "169.254.0.0/16",
            "172.16.0.0/12",
            "192.0.0.0/24",
            "192.0.2.0/24",
            "192.168.0.0/16",
            "198.18.0.0/15",
            "198.51.100.0/24",
            "203.0.113.0/24",
            "::1/128",
            "fc00::/7",
            "fe80::/10"
        ],
        "outboundTag": "blocked"
      }
    ]
  }
}

```