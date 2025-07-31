# Simple Customized Python Nmap Scanner

Just getting more familiar with scripting in Python, that's why I decided to customize my Nmap scans with the Nmap Python module.

---

# Usage:

1.
```bash
git clone https://github.com/SiddDevCS/NmapPython
cd NmapPython/
```

2. 
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

3.
```python
python3 main.py
```

From there just follow the instructions, you will be prompted :)

---

If you are too lazy to clone, here is the program:

```python
#!/usr/bin/env python3

import nmap

# nmap port scanner class
scanner = nmap.PortScanner()

print("Welcome! This is a simple Nmap automation tool")
print("==============================================")

ip_address = input("Please enter the IP address you want to scan: ")
print("The IP you entered is: ", ip_address)
print("Type: ", type(ip_address))

# type of scan
response_typescan = input("""\nPlease enter the type of scan you want to run.
                1. TCP Connect Scan
                2. UDP Scan
                3. Comprehensive Scan\n\n\n""")

print("\nYou have selected: ", response_typescan)

if response_typescan == '1':
    print("Nmap Version: ", scanner.nmap_version())

    # Use -sT instead of -sS to avoid permission issues
    scanner.scan(ip_address, '1-1024', '-sT -v')
    print(scanner.scaninfo())

    ip_address_status = scanner[ip_address].state()
    print("IP Status: ", ip_address_status)

    print("Protocols Detected: ", scanner[ip_address].all_protocols())

    if 'tcp' in scanner[ip_address]:
        print("Open TCP Ports: ", scanner[ip_address]['tcp'].keys())
```