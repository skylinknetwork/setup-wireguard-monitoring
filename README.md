## Buat Interface WireGuard di Mikrotik VPS
/interface wireguard add listen-port=13210 name=wg-server;<br>
/ip address add address=172.16.250.1/24 interface=wg-server;<br>

## Buat Interface WireGuard di Mikrotik Rumah
/interface wireguard add listen-port=51820 name=wg-home;<br>
/ip address add address=172.16.250.2/24 interface=wg-home;<br>

## Setup WireGuard di Android
[Interface]
PrivateKey = <OTOMATIS TERISI>
Address = 172.16.250.3/24
DNS = <KOSONGKAN_GPP>

[Peer]
PublicKey = <PUBLIC_KEY_VPS>
Endpoint = <IP_PUBLIC_VPS>:<PORT>
AllowedIPs = 172.16.250.0/24, <IP_POOL_PPPOE>, <IP_POOL_HOTSPOT>
PersistentKeepalive = 30

## Tambahkan Peer menuju Mikrotik Rumah di VPS<br>(Masukkan Kode ini di Mikrotik VPS)
/interface wireguard peers add interface=wg-server name=wg-peer-home allowed-address=172.16.250.0/24,<IP_POOLPPPOE>,<IP_POOL_HOTSPOT> public-key="<PUBLIC_KEY_MIKROTIK_RUMAH>"

## Buat NAT Masquerade di Mikrotik Rumah untuk monitoring CLIENT
/ip firewall nat add action=masquerade chain=srcnat comment="Masquerade Wireguard ke Client" dst-address-list=IP-CLIENT src-address=172.16.250.0/24

> [!NOTE]
> Ini catatan penting (otomatis warna **biru**).
