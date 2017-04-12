## TTL in Route53:
It is a general best practice to put Route 53 NS(Name Server record's) TTL to a higher number. Th maximum value can be 2 days (48 hours). Usually the resource under Route53 will not be changed often, so setting it a higher value will increase the performance and reduce the latency.

Just remember you cannot switch DNS so fast then. Usually before a DNS switch, just lower the TTL to a lower number a few days in advance. Now, try changing the A records to the new IP address. This will have effect immediately.
