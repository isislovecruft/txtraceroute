# OONI traceroute

The OONI probe traceroute is a multiprotocol multiport traceroute test. The
goal is to detect protocol/port based biases by doing a traceroute with
different protocols and different ports.

It detects the hop for every protocol/port pair in the same round to minimize
the risk of encountering route changes over time. At every round we send
packets with the same TTL, but with different protocol/port combinations and
wait to get back the TTL exceeded for all the send packets. Then we increment
the TTL by one.

## TODO:

* There is a bad bug that makes everything work badly with more than 2! port
combinations. Hunt it down and kill it!

* Collect the timestamp of the response by adding the IP_TIMESTAMP option. This
will make the device sending back the TTL exceeded packet add the timestamp of
when it got the expired packet.

* Add IP flag to get the MPLS VRF number of the Hop (if it exists)

* Activate IP option 7 record route


Sample output from a run (with only port 0 and 80):

`sudo python txtraceroute.py -o -n -g ooni.nu`

    01. 0.002s :: 192.168.80.1  (tcp, sport: 0 dport: 0)
    01. 0.003s :: 192.168.80.1  (udp, sport: 0 dport: 0)
    01. 0.003s :: 192.168.80.1  (tcp, sport: 80 dport: 0)
    01. 0.003s :: 192.168.80.1  (udp, sport: 80 dport: 0)
    01. 0.003s :: 192.168.80.1  (tcp, sport: 0 dport: 80)
    01. 0.004s :: 192.168.80.1  (udp, sport: 0 dport: 80)
    01. 0.004s :: 192.168.80.1  (tcp, sport: 80 dport: 80)
    01. 0.006s :: 192.168.80.1  (udp, sport: 80 dport: 80)
    01. - ??  (icmp, sport: 0 dport: 0)
    02. 0.056s :: 194.78.139.81  (tcp, sport: 0 dport: 0)
    02. 0.058s :: 194.78.139.81  (udp, sport: 0 dport: 0)
    02. 0.059s :: 194.78.139.81  (tcp, sport: 80 dport: 0)
    02. 0.060s :: 194.78.139.81  (udp, sport: 80 dport: 0)
    02. 0.060s :: 194.78.139.81  (tcp, sport: 0 dport: 80)
    02. 0.060s :: 194.78.139.81  (udp, sport: 0 dport: 80)
    02. 0.060s :: 194.78.139.81  (tcp, sport: 80 dport: 80)
    02. 0.060s :: 194.78.139.81  (udp, sport: 80 dport: 80)
    02. 0.060s :: 194.78.139.81  (icmp, sport: 0 dport: 0)
    03. 0.008s :: 172.22.69.69  (tcp, sport: 0 dport: 0)
    03. 0.009s :: 172.22.69.69  (udp, sport: 0 dport: 0)
    03. 0.010s :: 172.22.69.69  (tcp, sport: 80 dport: 0)
    03. 0.012s :: 172.22.69.69  (udp, sport: 80 dport: 0)
    03. 0.014s :: 172.22.69.69  (tcp, sport: 0 dport: 80)
    03. 0.147s :: 172.22.69.69  (udp, sport: 0 dport: 80)
    03. 0.147s :: 172.22.69.69  (tcp, sport: 80 dport: 80)
    03. 0.148s :: 172.22.69.69  (udp, sport: 80 dport: 80)
    03. 0.148s :: 172.22.69.69  (icmp, sport: 0 dport: 0)
    04. 0.010s :: 91.183.246.103  (tcp, sport: 0 dport: 0)
    04. 0.010s :: 91.183.246.103  (udp, sport: 0 dport: 0)
    04. 0.010s :: 91.183.246.103  (tcp, sport: 80 dport: 0)
    04. 0.011s :: 91.183.246.103  (udp, sport: 80 dport: 0)
    04. 0.011s :: 91.183.246.103  (tcp, sport: 0 dport: 80)
    04. 0.011s :: 91.183.246.103  (udp, sport: 0 dport: 80)
    04. 0.011s :: 91.183.246.103  (tcp, sport: 80 dport: 80)
    04. 0.011s :: 91.183.246.103  (udp, sport: 80 dport: 80)
    04. 0.011s :: 91.183.246.103  (icmp, sport: 0 dport: 0)
    05. 0.007s :: 91.183.246.102  (tcp, sport: 0 dport: 0)
    05. 0.009s :: 91.183.246.102  (udp, sport: 0 dport: 0)
    05. 0.009s :: 91.183.246.102  (tcp, sport: 80 dport: 0)
    05. 0.009s :: 91.183.246.102  (udp, sport: 80 dport: 0)
    05. 0.009s :: 91.183.246.102  (tcp, sport: 0 dport: 80)
    05. 0.011s :: 91.183.246.102  (udp, sport: 0 dport: 80)
    05. 0.047s :: 91.183.246.102  (tcp, sport: 80 dport: 80)
    05. 0.048s :: 91.183.246.102  (udp, sport: 80 dport: 80)
    05. 0.044s :: 91.183.246.102  (icmp, sport: 0 dport: 0)
    06. 0.110s :: 91.183.246.115  (tcp, sport: 0 dport: 0)
    06. 0.110s :: 91.183.246.115  (udp, sport: 0 dport: 0)
    06. 0.111s :: 91.183.246.115  (tcp, sport: 80 dport: 0)
    06. 0.113s :: 91.183.246.115  (udp, sport: 80 dport: 0)
    06. 0.114s :: 91.183.246.115  (tcp, sport: 0 dport: 80)
    06. 0.114s :: 91.183.246.115  (udp, sport: 0 dport: 80)
    06. 0.113s :: 91.183.246.115  (tcp, sport: 80 dport: 80)
    06. 0.113s :: 91.183.246.115  (udp, sport: 80 dport: 80)
    06. 0.113s :: 91.183.246.115  (icmp, sport: 0 dport: 0)
    07. 0.004s :: 80.84.21.34  (tcp, sport: 0 dport: 0)
    07. 0.004s :: 80.84.21.34  (udp, sport: 0 dport: 0)
    07. 0.005s :: 80.84.20.78  (tcp, sport: 80 dport: 0)
    07. 0.005s :: 80.84.20.78  (udp, sport: 80 dport: 0)
    07. 0.005s :: 80.84.20.78  (tcp, sport: 0 dport: 80)
    07. 0.005s :: 80.84.20.78  (udp, sport: 0 dport: 80)
    07. 0.006s :: 80.84.20.6  (tcp, sport: 80 dport: 80)
    07. 0.006s :: 80.84.20.6  (udp, sport: 80 dport: 80)
    07. 0.006s :: 80.84.21.34  (icmp, sport: 0 dport: 0)
    08. 0.067s :: 94.102.162.123  (tcp, sport: 0 dport: 0)
    08. 0.067s :: 94.102.162.123  (udp, sport: 0 dport: 0)
    08. 0.068s :: 94.102.162.123  (tcp, sport: 80 dport: 0)
    08. 0.068s :: 94.102.162.123  (udp, sport: 80 dport: 0)
    08. 0.068s :: 94.102.162.123  (tcp, sport: 0 dport: 80)
    08. 0.068s :: 94.102.162.123  (udp, sport: 0 dport: 80)
    08. 0.067s :: 94.102.162.123  (icmp, sport: 0 dport: 0)
    08. 0.068s :: 94.102.162.123  (tcp, sport: 80 dport: 80)
    08. 0.068s :: 94.102.162.123  (udp, sport: 80 dport: 80)
    09. 0.016s :: 195.69.144.113  (tcp, sport: 0 dport: 0)
    09. 0.101s :: 195.69.144.113  (udp, sport: 0 dport: 0)
    09. - ??  (tcp, sport: 80 dport: 0)
    09. - ??  (udp, sport: 80 dport: 0)
    09. - ??  (tcp, sport: 0 dport: 80)
    09. - ??  (udp, sport: 0 dport: 80)
    09. - ??  (tcp, sport: 80 dport: 80)
    09. - ??  (udp, sport: 80 dport: 80)
    09. - ??  (icmp, sport: 0 dport: 0)
    10. 0.020s :: 85.90.238.45  (udp, sport: 0 dport: 0)
    10. 0.070s :: 85.90.238.45  (tcp, sport: 0 dport: 0)
    10. - ??  (tcp, sport: 80 dport: 0)
    10. - ??  (udp, sport: 80 dport: 0)
    10. - ??  (tcp, sport: 0 dport: 80)
    10. - ??  (udp, sport: 0 dport: 80)
    10. - ??  (tcp, sport: 80 dport: 80)
    10. - ??  (udp, sport: 80 dport: 80)
    10. - ??  (icmp, sport: 0 dport: 0)
    11. 0.015s :: 217.20.44.218  (tcp, sport: 0 dport: 0)
    11. 0.015s :: 217.20.44.218  (udp, sport: 0 dport: 0)
    11. 0.020s :: 217.20.44.218  (tcp, sport: 80 dport: 0)
    11. 0.020s :: 217.20.44.218  (udp, sport: 80 dport: 0)
    11. 0.020s :: 217.20.44.218  (tcp, sport: 0 dport: 80)
    11. 0.020s :: 217.20.44.218  (udp, sport: 0 dport: 80)
    11. 0.021s :: 217.20.44.218  (tcp, sport: 80 dport: 80)
    11. 0.021s :: 217.20.44.218  (icmp, sport: 0 dport: 0)
    11. 0.024s :: 217.20.44.218  (udp, sport: 80 dport: 80)
    12. 0.017s :: 212.111.33.234  (tcp, sport: 0 dport: 0)
    12. 0.023s :: 212.111.33.234  (udp, sport: 0 dport: 0)
    12. 0.024s :: 212.111.33.234  (udp, sport: 80 dport: 0)
    12. 0.024s :: 212.111.33.234  (tcp, sport: 80 dport: 0)
    12. 0.024s :: 212.111.33.234  (tcp, sport: 0 dport: 80)
    12. 0.024s :: 212.111.33.234  (udp, sport: 0 dport: 80)
    12. 0.025s :: 212.111.33.234  (tcp, sport: 80 dport: 80)
    12. 0.025s :: 212.111.33.234  (udp, sport: 80 dport: 80)
    12. 0.025s :: 212.111.33.234  (icmp, sport: 0 dport: 0)

