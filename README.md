## Wireshark Useful Tools

| Filter                                                              | Description                                                                 |
|---------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `tls.handshake.extensions_server_name contains "google"`            | Reveal domain in the SNI (Server Name Indication) of TLS handshake          |
| `http.request`                                                      | Identifies outgoing HTTP requests                                           |
| `kerberos.CNameString`                                              | Locate device username                                                      |
| `nbns`                                                              | Locate NetBIOS name of device                                               |
| `http && ip.addr == [IP]`                                           | Shows HTTP traffic to/from a specific IP                                    |
| `ip.addr == [IP]`                                                   | Shows all traffic (not just HTTP) to/from a specific IP                     |
| `tcp.port == 80`                                                    | Filters for web traffic using port 80 (HTTP)                                |
| `http.request.method == "POST"`                                     | Displays only HTTP POST requests                                            |
| `frame contains "NetSupport"`                                       | Searches for traffic mentioning "NetSupport" (can indicate RAT activity)    |
| `http contains "fakeurl"`                                           | Detects requests to suspicious URLs like `/fakeurl.htm`                     |


| 🔍 Category                          | 📝 Indicator / Action                                                           |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| 🧪 How to Spot Suspicious Activity   | Look for **unusual POST requests** to unknown IPs or URLs.                      |
|                                      | Watch for **repeated connections** to the same external IP.                     |
|                                      | Check **User-Agent** strings for known RATs (e.g., NetSupport Manager/1.3).     |
|                                      | If `application/x-www-form-urlencoded` is in Content-Type:                      |
|                                      |   • Data was sent via an **HTML form**.                                         |
|                                      |   • Look for **name=value pairs** in the HTTP body (e.g., `CMD=POLL`).          |
| 🧾 POST Request Form Data Insights   | POST fields aren’t limited to login forms — **can be anything**.                |
|                                      | Example: `CMD=POLL\nINFO=1\nACK=1\n` → attacker is **sending commands**.        |
|                                      | Attackers **customize field names** (CMD, INFO, DATA, etc.).                    |
|                                      | View data in **bottom panel of Wireshark** (packet details pane).               |
| 🛡️ RAT (Remote Access Trojan) Signs | Outbound POSTs to **suspicious IPs or URLs**.                                   |
|                                      | **User-Agent:** NetSupport Manager/1.3 is commonly abused.                      |
|                                      | Repeated requests to a **fake or odd URL** like `/fakeurl.htm`.                 |
|                                      | **No X-Forwarded-For header** might mean **direct connection** (not via proxy). |
|                                      | **Regular traffic to non-standard ports/IPs** → potential malware beaconing.    |
| 📋 PCAP Analysis First Steps         | Identify **internal IP range** (e.g., `10.11.26.0/24`).                         |
|                                      | Use `ip.dst != 10.11.26.0/24` to locate **external traffic**.                   |
|                                      | Apply `http && ip.addr == [suspect IP]` to analyze **web interactions**.        |
|                                      | Look for **POSTs to unknown IPs/domains**.                                      |
|                                      | Check **User-Agent** and **payload** in HTTP headers.                           |
|                                      | **Compare IPs/domains** to alert logs or threat intel sources.                  |
|                                      | **Extract files/payloads** from POST requests if needed.                        |
