Wireshark Usefool Tools

Filter = tls.handshake.extensions_server_name contains "google" = to reveal the domain in the SNI (Server Name Indication) of TLS handshake packets.
Filter = http.request = Identified outgoing HTTP requests
Filter = kerberos.CNameString = locate device username
Filter = nbns = Locate NetBIOS Name of device
