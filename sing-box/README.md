# Исходный код ядра sing-box в WeaveVPN

В WeaveVPN входит sing-box 1.14.2 с нашими изменениями (сборка `1.14.2-weave3`). sing-box распространяется
под лицензией GPL-3.0-or-later ([LICENSE](LICENSE)), поэтому изменения опубликованы здесь.

Как получить тот же исходный код:

```bash
git clone --depth 1 --branch v1.14.2 https://github.com/SagerNet/sing-box.git
cd sing-box
git apply --whitespace=nowarn ../sing-box-1.14.2-weave3.patch
```

Что изменено ([sing-box-1.14.2-weave3.patch](sing-box-1.14.2-weave3.patch)):

- **REALITY** — клиент оставляет в ClientHello ключ X25519MLKEM768 и сообщает серверу версию Xray 26.9.9:
  без этого не подключается к серверам на свежем Xray;
- **sniff `override_destination`** — адрес назначения заменяется доменом из соединения (SNI/Host),
  как `destOverride` у Xray; только для публичных адресов;
- **`GET /connections/totals`** в Clash API — трафик по типу outbound, для статистики «через VPN» и «напрямую».

Сборка: теги `with_gvisor,with_quic,with_wireguard,with_utls,with_clash_api,badlinkname,tfogo_checklinkname0`.
