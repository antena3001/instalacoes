nano /etc/bind/named.conf
Cole:

statistics-channels {
 	inet 127.0.0.1 port 8653 allow { 127.0.0.1; };
};

nano /etc/zabbix/zabbix_agentd.conf

Cole:
UserParameter=bind.discoverzones,/usr/local/bin/bind-stats.py discoverzones
UserParameter=bind.counter[*],/usr/local/bin/bind-stats.py counter -c $1
UserParameter=bind.zonecounter[*],/usr/local/bin/bind-stats.py zonecounter -z $1 -c $2
UserParameter=bind.zonemaintenancecounter[*],/usr/local/bin/bind-stats.py zonemaintenancecounter -c $1
UserParameter=bind.resolvercounter[*],/usr/local/bin/bind-stats.py resolvercounter -c $1
UserParameter=bind.socketcounter[*],/usr/local/bin/bind-stats.py socketcounter -c $1
UserParameter=bind.incounter[*],/usr/local/bin/bind-stats.py incounter -c $1
UserParameter=bind.outcounter[*],/usr/local/bin/bind-stats.py outcounter -c $1
UserParameter=bind.memory[*],/usr/local/bin/bind-stats.py memory -c $1
UserParameter=bind.cache[*],/usr/local/bin/bind-stats.py cache -c $1

cd /usr/local/bin/

wget https://raw.githubusercontent.com/antena3001/instalacoes/master/bind-stats.py

chmod +x bind-stats.py

nano /etc/sudoers
zabbix ALL=(ALL) NOPASSWD: ALL

/etc/init.d/bind9 restart
/etc/init.d/zabbix-agent restart

importar temaplate.
