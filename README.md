![Static Badge](https://img.shields.io/badge/01.%20Buat%20Interface%20WireGuard%20baru%20di%20VPS-%230059FF?style=plastic)<br>
```Buat Interface WireGuard Mikrotik VPS
/interface wireguard add listen-port=51820 name=wg-server;
/ip address add address=172.16.250.1/24 interface=wg-server;
```
- Buat interface WireGuard baru di Mikrotik VPS
- Tambah IP untuk interface wg-server
<br>

![Static Badge](https://img.shields.io/badge/02.%20Buat%20Interface%20WireGuard%20di%20Mikrotik%20Rumah-%230059FF?style=plastic)
```Buat Interface WireGuard Mikrotik Rumah
/interface wireguard add listen-port=51820 name=wg-home;
/ip address add address=172.16.250.2/24 interface=wg-home;
/ip fi nat add cha=srcnat out-interface=wg-home act=masq;
```
- Buat interface WireGuard baru di Mikrotik Rumah
- Tambah IP untuk interface wg-home
- Buat Firewall NAT untuk output interface <b>wg-home</b>
<br>

![Static Badge](https://img.shields.io/badge/03.%20Setup%20WireGuard%20di%20Android-%230059FF?style=plastic)<br>
[Interface]<br>
PrivateKey = <b>(Klik icon panah memutar di sebelah kanan)</b><br>
PublicKey = <b>(OTOMATIS TERISI)</b><br>
Address = 172.16.250.3/24<br>
DNS = <b>(KOSONGKAN_GPP)</b><br>

[Peer]<br>
PublicKey = <b>(PUBLIC_KEY_VPS)</b><br>
Endpoint = <b>(IP_PUBLIC_VPS):(PORT)</b><br>
AllowedIPs = <b>172.16.250.0/24, (IP_POOL_PPPOE), (IP_POOL_HOTSPOT)</b><br>
PersistentKeepalive = 30
<br>
<br>

![Static Badge](https://img.shields.io/badge/04.%20Tambahkan%20peer%20menuju%20WireGuard%20rumah%20di%20VPS-%230059FF?style=plastic)<br>
![Static Badge](https://img.shields.io/badge/Catatan-%23D10000?style=flat-square)![Static Badge](https://img.shields.io/badge/Code%20ini%20untuk%20di%20input%20di%20Mikrotik%20VPS%2C%20Rubah%20PUBLIC_KEY%20_HOME%20dengan%20Public%20Key%20yang%20diambil%20dari%20(Mikrotik%20Rumah)-%23D17300?style=flat-square)
<br>
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
