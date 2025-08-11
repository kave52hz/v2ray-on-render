#!/bin/bash

UUID=${UUID:-"b3c5f8e4-1d2a-4d6e-9c3e-123456789abc"}
WS_PATH=${WS_PATH:-"/ray"}

cat <<EOF > config.json
{
  "inbounds": [{
    "port": 8080,
    "protocol": "vmess",
    "settings": {
      "clients": [{
        "id": "$UUID",
        "alterId": 0
      }]
    },
    "streamSettings": {
      "network": "ws",
      "wsSettings": {
        "path": "$WS_PATH"
      }
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  }]
}
EOF

./v2ray -config config.json
