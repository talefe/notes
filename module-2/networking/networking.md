Steps to communicate over the internet

1. Phisically connect to the network

2. Request an IP address using **DHCP**

3. Use **ARP** to find out the network's Router's **MAC Address**

4. Solve the destination's host name to an IP address using **DNS**

5. Wrap the message you want to send in a **TCP segment** (payload) with the proper headers - most importantly **destination and source ports**

6. Wrap that TCP segment in an **IP datagram** with the proper headers - most importantly **destination and souce's IP address**

7. Wrap that IP datagram in an **Ethernet Frame** (this depends on the underlying LAN technology, we are assuming this one is Ethernet)

8. The Router looks at the IP address of the destination host and consults its **routing table** to see which interface it should forward the IP datagram to

9. Then the Router translates the private IP address to the Router's public IP address (**NAT**) and the source port will be replaced by a specific port that the Router assigns to this client (**PAT**)

10. The IP datagram will keep being forward by the Routers until it reaches its final destination

    

![Ethernet Frame][ethernet-frame]



[ethernet-frame]:resources/images/ethernet-frame.png

