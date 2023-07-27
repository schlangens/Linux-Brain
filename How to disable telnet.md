``vi  /etc/xinetd.d/telnet``
Locate the following line:
disable = no
change to yes
``:wq``

Restart the inetd service by using the following command:
``sudo /etc/rc.d/init.d/xinetd restart``

Turn off Telnet through chkconfig as well because it can still start through that:
``/sbin/chkconfig telnet off``


