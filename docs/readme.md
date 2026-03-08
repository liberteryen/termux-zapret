```bash
#destek var mı bak
su -c "cat /proc/net/netfilter/nfnetlink_queue"


```bash
#kur
apt install libnetfilter-queue clang build-essential net-tools netcat-openbsd -y libmnl
git clone https://github.com/liberteryen/termux-zapret --depth 1
cd termux-zapret
make -j8
```
```bash
#çalıştır
su -c "~/termux-zapret/nfq/nfqws --qnum=200 --uid=0 --filter-tcp=80,443 XXXXX"
#XXXX olan yere paramtreleri yaz. misal:
su -c "~/termux-zapret/nfq/nfqws --qnum=200 --uid=0 --filter-tcp=80,44 --dpi-desync=fakedsplit --dpi-desync-fooling=md5sig --dpi-desync-split-pos=1 --dpi-desync-autottl"

```
```bash
#iptables ile yönlendir
su -c "iptables -t mangle -I OUTPUT -p tcp --dport 443 -j NFQUEUE --queue-num 200"
su -c "iptables -t mangle -I OUTPUT -p tcp --dport 80 -j NFQUEUE --queue-num 200"
```
