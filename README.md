## Wireshark Useful Tools

| Filter                                                              | Description                                                             |
|---------------------------------------------------------------------|-------------------------------------------------------------------------|
| `tls.handshake.extensions_server_name contains "google"`            | Reveal domain in the SNI (Server Name Indication) of TLS handshake      |
| `http.request`                                                      | Identifies outgoing HTTP requests                                       |
| `kerberos.CNameString`                                              | Locate device username                                                  |
| `nbns`                                                              | Locate NetBIOS name of device                                           |
