![Static Badge](https://img.shields.io/badge/Buat%20Interface%20WireGuard%20di%20Mikrotik%20VPS-%23FF0000?style=flat-square)<br>
/interface wireguard add listen-port=64221 name=wg-server;<br>
/ip address add address=172.16.250.1/24 interface=wg-server;<br>

![Static Badge](https://img.shields.io/badge/Buat%20Interface%20WireGuard%20di%20Mikrotik%20Rumah-%23FF0000?style=flat-square)<br>
/interface wireguard add listen-port=51820 name=wg-home;<br>
/ip address add address=172.16.250.2/24 interface=wg-home;<br>

![Static Badge](https://img.shields.io/badge/Setup%20WireGuard%20di%20Android-%23FF0000?style=flat-square)<br>
[Interface]<br>
PrivateKey = <b>(Klik icon panah memutar di sebelah kanan)</b><br>
PublicKey = <b>(OTOMATIS TERISI)</b><br>
Address = 172.16.250.3/24<br>
DNS = <b>(KOSONGKAN_GPP)</b><br><br>

[Peer]<br>
PublicKey = <b>(PUBLIC_KEY_VPS)</b><br>
Endpoint = <b>(IP_PUBLIC_VPS):(PORT)</b><br>
AllowedIPs = 172.16.250.0/24, (IP_POOL_PPPOE), (IP_POOL_HOTSPOT)<br>
PersistentKeepalive = 30<br>

## Tambahkan Peer menuju Mikrotik Rumah di VPS<br>(Masukkan Kode ini di Mikrotik VPS)
/interface wireguard peers add interface=wg-server name=wg-peer-home allowed-address=172.16.250.0/24,<IP_POOL_PPPOE>,<IP_POOL_HOTSPOT> public-key="<PUBLIC_KEY_MIKROTIK_RUMAH>"

## Tambahkan Peer menuju HP Android di VPS<br>(Masukkan Kode ini di Mikrotik VPS)
/interface wireguard peers add interface=wg-server name=wg-peer-hp allowed-address=172.16.250.0/24,<IP_POOL_PPPOE>,<IP_POOL_HOTSPOT> public-key="<PUBLIC_KEY_HP_ANDROID>"

## Buat NAT Masquerade di Mikrotik Rumah untuk monitoring CLIENT
/ip firewall nat add action=masquerade chain=srcnat comment="Masquerade Wireguard ke Client" out-interface=wg-home

> [!NOTE]
> Ini catatan penting (otomatis warna **biru**).

> [!TIP]
> Ini tips keren (otomatis warna **hijau**).

> [!IMPORTANT]
> Ini info penting banget (otomatis warna **ungu**).

> [!WARNING]
> Ini peringatan (otomatis warna **kuning**).

> [!CAUTION]
> Ini bahaya/peringatan keras (otomatis warna **merah**).
>
```ansi
\u001b[31mIni teks warna merah\u001b[0m
\u001b[32mIni teks warna hijau\u001b[0m
\u001b[33mIni teks warna kuning\u001b[0m
\u001b[34mIni teks warna biru\u001b[0m
```
