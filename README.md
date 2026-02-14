# opnsense

install tools

    pkg install vim git sysutils/lsof
    pkg install sysutils/hwstat

install htop

    enable FreeBSD
    
    /usr/local/etc/pkg/repos/FreeBSD.conf
    
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

    pw groupmod wheel -m telegraf
    pw groupshow wheel

arp (mac to IP) Telegraf output

    ee /usr/local/bin/arp_telegraf.sh

/usr/local/bin/arp_telegraf.sh

    #!/bin/sh
    # Output: Influx Line Protocol
    # Tags: ip, mac (mac ohne ":"), iface wenn verfügbar
    # Field: present=1i

    arp -an | awk '
    /\(/ {
      gsub("[()]", "", $2);
      ip=$2;
      mac=$4;

      # skip incomplete
      if (mac == "(incomplete)" || mac == "" || ip == "") next;

      # make MAC tag safe
      gsub(":", "-", mac);

      printf "arp_table,source=opnsense,ip=%s,mac=%s present=1i\n", ip, mac;
    }'

/usr/local/bin/arp_telegraf.sh
    
    chmod +x /usr/local/bin/arp_telegraf.sh
    /usr/local/bin/arp_telegraf.sh

/usr /local/telegraf.conf

    [[inputs.exec]]
      commands = ["/usr/local/bin/arp_telegraf.sh"]
      timeout = "5s"
      data_format = "influx"
      interval = "60s"
