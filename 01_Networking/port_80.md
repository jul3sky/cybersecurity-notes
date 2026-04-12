============================================================
                     PORT 80 - TECHNICAL NOTE
============================================================

1. OVERVIEW
------------------------------------------------------------
Port 80 is the default port for HTTP (Hypertext Transfer 
Protocol). As your original note states:

"Port 80 is a well-known port used for Hypertext Transfer 
Protocol (HTTP), which is the foundation of data communication 
on the World Wide Web."

HTTP traffic on port 80 is NOT encrypted. All data is sent in 
plaintext, meaning it can be intercepted and read by anyone 
monitoring the connection.

------------------------------------------------------------
2. PORT 80 VS PORT 443
------------------------------------------------------------
Port 80  -> HTTP  -> Unencrypted
Port 443 -> HTTPS -> Encrypted (TLS/SSL)

Your document highlights:
"Port 80 transmits data in plaintext, making it less secure."

Because of this, modern systems often redirect HTTP (80) to 
HTTPS (443) automatically.

------------------------------------------------------------
3. WHY PORT 80 STILL EXISTS
------------------------------------------------------------
- It is the default HTTP port.
- Many legacy systems still rely on it.
- It is part of the IANA well-known ports (0–1023).
- Some applications use alternate ports (8080, 8000) to avoid 
  privileged port restrictions.

Even though HTTPS is preferred, port 80 remains widely used for 
initial connections and redirects.

------------------------------------------------------------
4. REDIRECTING PORT 80 -> 443
------------------------------------------------------------
Below are the cleaned versions of the configurations from your 
note.

[Nginx]
------------------------------------------------------------
server {
    listen 80;
    server_name yourdomain.com;
    return 301 https://$host$request_uri;
}

[Apache]
------------------------------------------------------------
<VirtualHost *:80>
    Redirect permanent / https://yourdomain.com/
</VirtualHost>

These ensure all HTTP traffic is securely redirected.

------------------------------------------------------------
5. BLOCKING ("MUTING") PORT 80 ON WINDOWS CMD
------------------------------------------------------------
Your document includes the correct commands:

Block inbound:
    netsh advfirewall firewall add rule name="Block Inbound 80" ^
    dir=in action=block protocol=TCP localport=80

Block outbound:
    netsh advfirewall firewall add rule name="Block Outbound 80" ^
    dir=out action=block protocol=TCP localport=80

These rules override allow rules and fully mute port 80.

------------------------------------------------------------
6. BLOCKING OTHER PORTS (EXAMPLE: 8009)
------------------------------------------------------------
netsh advfirewall firewall add rule name="Block Port 8009" ^
dir=in protocol=TCP localport=8009 action=block

------------------------------------------------------------
7. BLOCKING SPECIFIC REMOTE IP ADDRESSES
------------------------------------------------------------
Block all inbound traffic from a remote IP:
    netsh advfirewall firewall add rule name="Block Remote IP" ^
    dir=in action=block remoteip=192.168.1.100

Block traffic from IP + port:
    netsh advfirewall firewall add rule name="Block IP on 8009" ^
    dir=in action=block remoteip=192.168.1.100 protocol=TCP ^
    localport=8009

------------------------------------------------------------
8. NOTES
------------------------------------------------------------
- Commands must be run as Administrator.
- Rules persist after reboot.
- Useful for testing, hardening, or isolating services.

============================================================
                     END OF PORT 80 REPORT
============================================================
