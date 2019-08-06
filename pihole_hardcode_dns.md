# ubnt Hard code dns pihole
 nat {
        rule 1 {
            description "captive dns"
            destination {
                address !192.168.1.59
                port 53
            }
            inbound-interface switch0
            inside-address {
                address 192.168.1.59
                port 53
            }
            log disable
            protocol tcp_udp
            source {
                address !192.168.1.59
            }
            type destination
        }
        rule 5010 {
            description "masquerade for WAN"
            outbound-interface eth0
            type masquerade
        }
        rule 5011 {
            description piholemagic
            destination {
                address 192.168.1.59
                port 53
            }
            log disable
            outbound-interface switch0
            protocol tcp_udp
            source {
                address 192.168.1.59
            }
            type masquerade
        }
    }
