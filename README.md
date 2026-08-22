![Static Badge](https://img.shields.io/badge/01.%20Buat%20Interface%20WireGuard%20baru%20di%20VPS-%230059FF?style=plastic)<br>
```Buat Interface WireGuard Mikrotik VPS
{
/interface wireguard add listen-port=51820 name=wg-server;
/ip address add address=172.16.250.1/24 interface=wg-server;
}
```
- Buat interface WireGuard baru di Mikrotik VPS
- Tambah IP untuk interface wg-server
<img width="45%" src="https://github.com/user-attachments/assets/e5a810ee-8145-4b4b-bf87-cc2eaec55f93" />
<br><br>

![Static Badge](https://img.shields.io/badge/02.%20Buat%20Interface%20WireGuard%20di%20Mikrotik%20Rumah-%230059FF?style=plastic)
```Buat Interface WireGuard Mikrotik Rumah
{
/interface wireguard add listen-port=51820 name=wg-home;
/ip address add address=172.16.250.2/24 interface=wg-home;
/ip fi nat add cha=srcnat out-interface=wg-home act=masq;
}
```
- Buat interface WireGuard baru di Mikrotik Rumah
- Tambah IP untuk interface wg-home
- Buat Firewall NAT untuk output interface <b>wg-home</b>
<img width="45%" src="https://github.com/user-attachments/assets/fd092356-59bb-4673-87ca-a4264be25ff1" />
<br><br>

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
PersistentKeepalive = 30 <br><br>
<img width="45%" src="https://github.com/user-attachments/assets/653a9589-03b0-405d-a6a2-41359b4c43c2" />
<br>
<br>

![Static Badge](https://img.shields.io/badge/04.%20Tambahkan%20peer%20menuju%20WireGuard%20rumah%20di%20Mikrotik%20VPS-%230059FF?style=plastic)<br>
```
{
/interface wireguard peers add interface=wg-server name=wg-peer-home \
   allowed-address=172.16.250.0/24 public-key="(PUBLIC_KEY_HOME)"
}
```
![Static Badge](https://img.shields.io/badge/Catatan-%23D10000?style=flat-square)<br>
![Static Badge](https://img.shields.io/badge/Rubah%20PUBLIC_KEY%20_HOME%20dengan%20Public%20Key%20diambil%20dari%20WireGuard%20(Mikrotik%20Rumah)-%23D17300?style=flat-square)<br>
<img width="45%" src="https://github.com/user-attachments/assets/53b5164e-b680-4848-8658-bfe1238918f1" />
<br>
<br>

![Static Badge](https://img.shields.io/badge/05.%20Tambahkan%20peer%20menuju%20WireGuard%20HP%20di%20Mikrotik%20VPS-%230059FF?style=plastic)<br>
```
{
/interface wireguard peers add interface=wg-server name=wg-peer-hp \
   allowed-address=172.16.250.0/24,(IP_POOL_PPPOE),(IP_POOL_HOTSPOT) \
   public-key="(PUBLIC_KEY_HP)"
}
```
![Static Badge](https://img.shields.io/badge/Catatan-%23D10000?style=flat-square)<br>
![Static Badge](https://img.shields.io/badge/Rubah%20PUBLIC_KEY%20_HP%20dengan%20Public%20Key%20diambil%20dari%20WireGuard%20(HP)-%23D17300?style=flat-square)<br>
![Static Badge](https://img.shields.io/badge/Rubah%20IP_POOL_PPPOE%20dan%20HOTSPOT%20Sesuai%20IP%20Pool%20Client%20yang%20ada%20di%20Mikrotik%20Rumah-%23D17300?style=flat-square)
<br>
<br>

![Static Badge](https://img.shields.io/badge/06.%20Buat%20NAT%20Masquerade%20di%20Mikrotik%20Rumah-%230059FF?style=plastic)<br>
```
{
/ip firewall nat add action=masquerade chain=srcnat \
   out-interface=wg-home
}
```
<br>

![Static Badge](https://img.shields.io/badge/07.%20Tambahkan%20peer%20menuju%20VPS%20di%20Mikrotik%20Rumah-%230059FF?style=plastic)<br>
```
{
/interface wireguard peer add name=peer-vps interface=wg-home \
   public-key="PUBLIC_KEY_VPS" endpoint-addr=(IP_PUBLIK_VPS) \
   endpoint-port=51820 allowed-address=172.16.251.0/24 persistent=20
}
```
<br>
![Static Badge](https://img.shields.io/badge/Catatan-%23D10000?style=flat-square)<br>
![Static Badge](https://img.shields.io/badge/Rubah%20PUBLIC_KEY%20_VPS%20dengan%20Public%20Key%20diambil%20dari%20WireGuard%20VPS-%23D17300?style=flat-square)<br>
<br>
