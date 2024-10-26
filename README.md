# nagios-juniper-bgp-check-php
Nagios BGP check for Juniper, written in PHP

```
define command{
        command_name    check_bgp
        command_line    $USER1$/check_bgp -H $HOSTADDRESS$ $ARG1$ $ARG2$
        }
```

