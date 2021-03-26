26 Mar 2021
pfSense.json by Alan Taylor, https://github.com/alan-taylor/lnav-pfsense

lnav by Tim Stack, https://github.com/tstack/lnav

This is a .json file to upload the pfSense firewall log format to lnav.
Development and testing limited to linux.

Examples of current log formats supported are (from pfSense filterlog.log file):
Mar 18 10:51:53 computer.domain.tld filterlog: 5,,,1000000103,igb0,match,block,in,4,0x0,,41,4812,0,none,6,tcp,44,111.22.33.1,224.22.11.1,39248,10443,0,S,980905229,,1024,,mss
Mar 18 10:51:54 computer.domain.tld filterlog: 145,,,100000101,igb1.8,match,pass,in,4,0x0,,64,43408,0,DF,6,tcp,52,111.22.33.1,224.22.11.1,56840,443,0,S,3960455768,,64240,,mss;nop;nop;sackOK;nop;wscale
Mar 18 10:51:53 computer.domain.tld filterlog: 145,,,100000101,igb1.8,match,pass,in,4,0x0,,64,26055,0,DF,17,udp,86,111.22.33.1,224.22.11.1,37347,53,66
Dec 19 17:30:22 computer.domain.tld filterlog: 7,,,1000000105,lagg0.9,match,block,in,6,0x00,0x30dbe,255,UDP,17,147,fe00::1c11:7f5c:b111:71d2,fc23::bc,5353,5353,147
Mar 18 10:52:26 computer.domain.tld filterlog: 7,,,1000000105,lagg0.9,match,block,in,6,0x00,0x00000,1,Options,0,32,fe00::1c11:7f5c:b111:71d2,ee23::5,HBH,PADN,RTALERT,0x0000,
Mar 18 10:52:21 computer.domain.tld filterlog: 136,,,1615175071,igb1.8,match,pass,in,4,0x0,,64,47615,0,DF,1,icmp,84,111.22.33.1,224.22.11.1,request,7717,164
Mar 12 02:53:34 computer.domain.tld filterlog: 5,,,1000000103,lagg0.9,match,block,in,4,0x0,,1,1918,0,none,2,igmp,32,111.22.33.1,224.22.11.1,datalength=8"

This pfSense.json file allows lnav to read the pfSense firewall logs in to an
sqlite database with the following fields:
timestamp, log_hostname, rule_number, subrule_number, anchor, tracker, interface,
reason, action, direction, ip_ver, tos, ecn, ttl, id, offset, flags, class,
flow_label, hop_limit, protocol_id, protocol_text, length, src_address,
dest_address, src_port, dest_port

All data after this on each line of the logs is put into a field called:
body

Many of these attributes are specific to the pfSense firewall log format, documented at:
https://docs.netgate.com/pfsense/en/latest/monitoring/logs/raw-filter-format.html

There is currently a bug in lnav (0.90) that produces an error if you install
with:
$ lnav -i pfSense.json
The easiest workaround is simply copy the file to your format directory, likely:
$ cp pfSense.json ~/.config/lnav/formats/installed/
Create the "installed" directory if necessary.
https://docs.lnav.org/en/latest/formats.html#installing-formats

All feedback, suggestions and ideas appreciated at:
https://github.com/alan-taylor/lnav-pfsense/discussions
