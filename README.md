# opnsense

install tools

    pkg install vim git sysutils/lsof
    pkg install sysutils/hwstat

    check this ???
    git clone https://git.FreeBSD.org/ports.git /usr/ports
    pkg install benchmarks/sysbench
    
set .cshrc
     
    set prompt="%{\e[31m%}root%{\e[37m%}@%{\e[33m%}%m%{\e[37m%}:%{\e[36m%}%/%{\e[37m%}#%{\e[0m%} "
    set promptchars = "%#"

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
