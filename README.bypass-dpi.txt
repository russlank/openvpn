As some ISP(s) rely on Deep Packet Inspection (DPI) to identify various VPN traffic, and to block them, I have added small feature, called “bypass-dpi”. This new feature mainly gives OpenVPN the ability to masquerade the protocol by sending arbitrary, meaningless, initial packet that confuses the DPI mechanism, and allows consequent valid connection's packets to pass through, without being identified as OpenVPN traffic.

As the DPI appliances establish context for each newly established connection passing through, depending on examining known protocols’ signatures, at very early stage of connection establishment, sending such a packet makes DPI blind, and makes it classifying the protocol as unknown.

Currently implemented method works with specific OpenVPN configuration:

UDP protocol to be used for the connection.
TLS-AUTH to be specified; this will allow the server to drop the initial invalid packet, which means that the support for the feature is needed on the client side only.
I have modified the code to include this feature, and which can be enabled using “bypass-dpi” option in the configuration or at command-line.

Frankly, I made the change with the minimum effort. I think it could be implemented in better, more consistent way, by someone who has better understanding of the code.
