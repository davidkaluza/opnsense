# opnsense

install tools

    pkg install vim git sysutils/lsof

set timeserver

    times.tu-berlin.de

link updatedb

    ln -s /usr/libexec/locate.updatedb /bin/updatedb

check for permission

    sudo -u telegraf more /var/log/suricata/eve.json

change permission to read eve.json

    pw group mod wheel -m telegraf
    pw groupshow wheel
