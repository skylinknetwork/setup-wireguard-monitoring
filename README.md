### Buat Interface Wireguard baru di VPS
{
/interface wireguard add listen-port=13210 name=wg-server
/ip address add address=172.16.250.1/24 interface=wg-server
}

# Buat Interface WireGuard & pasang IP
/interface wireguard add listen-port=51820 name=wg-home
/ip address add address=172.16.250.2/24 interface=wg-home

# Tambahkan Peer di VPS Server untuk Mikrotik X86-Home
/interface wireguard peers add interface=wg-server name=wg-peer-home allowed-address=172.16.250.2/32,10.10.0.0/16,10.20.20.0/24 public-key="<PUBLIC_KEY_HOME>"

# Tambahkan Peer di VPS Server untuk Samsung S25FE
/interface wireguard peers add interface=wg-server name=wg-peer-s25fe allowed-address=172.16.250.3/32 public-key="<PUBLIC_KEY_S25FE>"

# NAT Masquerade agar trafik monitoring menuju IP-CLIENT
/ip firewall nat add action=masquerade chain=srcnat comment="MASQ WG 172.16.250.0/24 to Local Clients" dst-address-list=IP-CLIENT src-address=172.16.250.0/24

[Interface]
PrivateKey = <PRIVATE_KEY_S25FE>
Address = 172.16.250.3/24
DNS = 1.1.1.1

[Peer]
PublicKey = <PUBLIC_KEY_VPS>
Endpoint = 103.180.165.200:51820
AllowedIPs = 172.16.250.0/24, 10.10.0.0/16, 10.20.20.0/24
PersistentKeepalive = 25
