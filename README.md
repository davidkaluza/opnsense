# opnsense

install tools

    pkg install vim git sysutils/lsof
    pkg install sysutils/hwstat

    check this ???
    git clone https://git.FreeBSD.org/ports.git /usr/ports
    pkg install benchmarks/sysbench
    
    
set timeserver

    times.tu-berlin.de

link updatedb

    ln -s /usr/libexec/locate.updatedb /bin/updatedb

install htop

    pkg add https://pkg.freebsd.org/FreeBSD:14:amd64/quarterly/All/htop-3.4.0.pkg

check for permission

    sudo -u telegraf more /var/log/suricata/eve.json

change permission to read eve.json

    pw group mod wheel -m telegraf
    pw groupshow wheel
