============================================================
# NMAP NOTES
             
============================================================


1. TARGET SPECIFICATION
------------------------------------------------------------
Nmap accepts multiple target formats:

1) IP RANGE (using "-")
   Example:
       192.168.0.1-10

2) CIDR SUBNET (using "/")
   Example:
       192.168.0.1/24
   Equivalent to:
       192.168.0.0-255

3) HOSTNAME
   Example:
       example.thm


2. HOST DISCOVERY
------------------------------------------------------------
Ping Scan (host discovery only):
    nmap -sn 192.168.0.1/24

List Scan (list targets without scanning):
    nmap -sL 192.168.0.1/24


3. PORT SCANNING OPTIONS
------------------------------------------------------------
-sT   TCP Connect scan (full 3-way handshake)
-sS   SYN scan (stealthy, half-open)
-sU   UDP scan
-F    Fast mode (top 100 ports)
-p    Specify ports or ranges
      Examples:
         -p1-1000
         -p-   (all ports)


4. SERVICE & OS DETECTION
------------------------------------------------------------
-O    OS detection
-sV   Service version detection
-A    Aggressive scan (OS + version + scripts + traceroute)


5. TIMING & PERFORMANCE
------------------------------------------------------------
Timing Templates:
    -T0  Paranoid
    -T1  Sneaky
    -T2  Polite
    -T3  Normal (default)
    -T4  Aggressive
    -T5  Insane

Parallelism:
    --min-parallelism <num>
    --max-parallelism <num>

Rate Control:
    --min-rate <packets/sec>
    --max-rate <packets/sec>

Host Timeout:
    --host-timeout <time>


6. VERBOSITY & DEBUGGING
------------------------------------------------------------
Verbosity:
    -v, -vv, -vvv, -v4
(You can press "v" during a running scan.)

Debugging:
    -d, -dd, -d9
(Be prepared for thousands of lines at high levels.)


7. SAVING SCAN REPORTS
------------------------------------------------------------
-oN <file>   Normal output
-oX <file>   XML output
-oG <file>   Grepable output
-oA <base>   All major formats

Example:
    nmap -sV -oA scan_results 192.168.0.1


8. RECOMMENDED USAGE
------------------------------------------------------------
Stealth Scan:
    nmap -sS <target>

Host Discovery Only:
    nmap -sn <subnet>

Combine discovery + port scan:
    nmap -sS <target>


9. SUMMARY TABLE
------------------------------------------------------------
List Scan:
    -sL

Host Discovery:
    -sn

Port Scanning:
    -sT, -sS, -sU, -F, -p-, -Pn

Service Detection:
    -O, -sV, -A

Timing:
    -T0 to -T5
    --min-rate / --max-rate
    --host-timeout

Output:
    -oN, -oX, -oG, -oA

Real-time Output:
    -v, -d


============================================================

                 END OF NMAP NOTES
============================================================
