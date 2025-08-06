# Networking Commands

Essential networking tools for connectivity, troubleshooting, and network configuration in Linux.

## Network Configuration

### `ip` - Modern network configuration tool
```bash
# Interface management
ip addr show                      # Show all network interfaces
ip addr show eth0                 # Show specific interface
ip link show                      # Show link layer information
ip link set eth0 up               # Bring interface up
ip link set eth0 down             # Bring interface down

# IP address management
ip addr add 192.168.1.100/24 dev eth0    # Add IP address
ip addr del 192.168.1.100/24 dev eth0    # Remove IP address

# Routing
ip route show                     # Show routing table
ip route add default via 192.168.1.1     # Add default route
ip route add 10.0.0.0/8 via 192.168.1.1  # Add specific route
ip route del 10.0.0.0/8           # Delete route
```

### `ifconfig` - Legacy interface configuration (if available)
```bash
ifconfig                          # Show all interfaces
ifconfig eth0                     # Show specific interface
ifconfig eth0 up                  # Bring interface up
ifconfig eth0 down                # Bring interface down
ifconfig eth0 192.168.1.100       # Set IP address
```

### `nmcli` - NetworkManager CLI
```bash
nmcli device status               # Show device status
nmcli connection show             # Show connections
nmcli device wifi list           # List WiFi networks
nmcli device wifi connect SSID password PASSWORD
nmcli connection up connection_name
nmcli connection down connection_name
```

## Network Testing & Troubleshooting

### `ping` - Test connectivity
```bash
ping google.com                   # Basic connectivity test
ping -c 4 8.8.8.8                 # Send 4 packets
ping -i 2 192.168.1.1             # Ping every 2 seconds
ping -s 1000 host                 # Send large packets (1000 bytes)
ping6 ipv6.google.com             # IPv6 ping
```

### `traceroute` / `tracepath` - Trace network path
```bash
traceroute google.com             # Trace route to destination
traceroute -n google.com          # Don't resolve hostnames
tracepath google.com              # Alternative trace utility
mtr google.com                    # Continuous traceroute (if installed)
```

### `nslookup` & `dig` - DNS queries
```bash
# nslookup
nslookup google.com               # Basic DNS lookup
nslookup google.com 8.8.8.8       # Use specific DNS server
nslookup -type=MX google.com      # Query MX records

# dig (more powerful)
dig google.com                    # Basic DNS query
dig @8.8.8.8 google.com           # Use specific DNS server
dig google.com MX                 # Query MX records
dig google.com ANY                # Query all record types
dig -x 8.8.8.8                    # Reverse DNS lookup
dig +trace google.com             # Trace DNS resolution path
```

### `host` - DNS lookup utility
```bash
host google.com                   # Basic DNS lookup
host -t MX google.com             # Query specific record type
host 8.8.8.8                      # Reverse DNS lookup
```

## Port and Socket Information

### `ss` - Socket statistics (modern replacement for netstat)
```bash
ss -tuln                          # Show all listening TCP/UDP ports
ss -tun                           # Show all TCP/UDP connections
ss -tlnp                          # Show listening TCP ports with processes
ss -i                             # Show internal TCP information
ss -s                             # Show socket statistics summary
ss 'dst :80'                      # Filter connections to port 80
ss 'src :22'                      # Filter connections from port 22
```

### `netstat` - Network statistics (legacy)
```bash
netstat -tuln                     # Show all listening ports
netstat -tun                      # Show all connections
netstat -tlnp                     # Show listening TCP ports with processes
netstat -r                        # Show routing table
netstat -i                        # Show network interfaces
netstat -s                        # Show network statistics
```

### `lsof` - Network-related open files
```bash
lsof -i                           # Show all network connections
lsof -i :80                       # Show processes using port 80
lsof -i tcp                       # Show all TCP connections
lsof -i udp                       # Show all UDP connections
lsof -i @192.168.1.1              # Connections to specific IP
```

## Network File Transfer

### `wget` - Download files from web
```bash
wget https://example.com/file.zip # Download file
wget -O newname.zip https://...   # Save with different name
wget -c https://example.com/file  # Continue partial download
wget -r https://example.com/      # Recursive download
wget --limit-rate=200k https://...# Limit download speed
wget -q https://example.com/file  # Quiet mode
wget --no-check-certificate https://... # Ignore SSL errors
```

### `curl` - Transfer data with servers
```bash
curl https://example.com          # GET request
curl -o file.zip https://...      # Save to file
curl -O https://example.com/file.zip # Save with original name
curl -L https://example.com       # Follow redirects
curl -H "Content-Type: application/json" -X POST -d '{"key":"value"}' https://api.example.com
curl -I https://example.com       # HEAD request (headers only)
curl -u user:pass https://...     # HTTP authentication
curl -k https://example.com       # Ignore SSL errors
curl -w "%{http_code}" https://...# Show HTTP status code
```

### `scp` - Secure copy over SSH
```bash
scp file.txt user@host:/path/     # Copy file to remote host
scp user@host:/path/file.txt .    # Copy file from remote host
scp -r directory user@host:/path/ # Copy directory recursively
scp -P 2222 file.txt user@host:/path/ # Use specific SSH port
scp -i ~/.ssh/key file.txt user@host:/path/ # Use specific SSH key
```

### `rsync` - Efficient file synchronization
```bash
rsync -av source/ user@host:/dest/ # Sync to remote host
rsync -av user@host:/source/ dest/ # Sync from remote host
rsync -av --delete source/ dest/   # Sync with deletion
rsync -e "ssh -p 2222" source/ user@host:/dest/ # Custom SSH port
rsync -n -av source/ dest/         # Dry run (preview changes)
```

## SSH and Remote Access

### `ssh` - Secure Shell
```bash
ssh user@hostname                 # Basic SSH connection
ssh -p 2222 user@hostname         # Connect to specific port
ssh -i ~/.ssh/keyfile user@host   # Use specific SSH key
ssh -L 8080:localhost:80 user@host # Local port forwarding
ssh -R 8080:localhost:80 user@host # Remote port forwarding
ssh -D 1080 user@host             # SOCKS proxy
ssh -X user@host                  # Enable X11 forwarding
ssh -v user@host                  # Verbose output (debugging)
```

### SSH key management
```bash
ssh-keygen -t rsa -b 4096         # Generate RSA key pair
ssh-keygen -t ed25519             # Generate Ed25519 key pair
ssh-copy-id user@host             # Copy public key to remote host
ssh-add ~/.ssh/private_key        # Add key to SSH agent
ssh-add -l                        # List loaded keys
```

### `ssh-agent` - SSH key agent
```bash
eval $(ssh-agent)                 # Start SSH agent
ssh-add                           # Add default keys to agent
ssh-add ~/.ssh/id_rsa             # Add specific key to agent
ssh-add -l                        # List keys in agent
ssh-add -D                        # Remove all keys from agent
```

## Network Monitoring

### `iftop` - Interface bandwidth monitor (if installed)
```bash
iftop                             # Monitor network traffic
iftop -i eth0                     # Monitor specific interface
iftop -n                          # Don't resolve hostnames
```

### `nethogs` - Process network usage monitor (if installed)
```bash
nethogs                           # Show network usage per process
nethogs eth0                      # Monitor specific interface
```

### `tcpdump` - Packet capture and analysis
```bash
tcpdump -i eth0                   # Capture packets on interface
tcpdump host 192.168.1.1          # Capture packets to/from host
tcpdump port 80                   # Capture packets on port 80
tcpdump -n host 8.8.8.8           # Don't resolve hostnames
tcpdump -w capture.pcap           # Save to file
tcpdump -r capture.pcap           # Read from file
tcpdump -X port 80                # Show packet contents in hex/ASCII
```

### `wireshark` / `tshark` - Advanced packet analysis
```bash
tshark -i eth0                    # Command-line packet capture
tshark -r capture.pcap            # Analyze capture file
tshark -i eth0 -f "tcp port 80"   # Filter during capture
```

## Firewall Management

### `ufw` - Uncomplicated Firewall (Ubuntu/Debian)
```bash
sudo ufw enable                   # Enable firewall
sudo ufw disable                  # Disable firewall
sudo ufw status                   # Show firewall status
sudo ufw allow 22                 # Allow SSH
sudo ufw allow 80/tcp             # Allow HTTP
sudo ufw deny 23                  # Deny telnet
sudo ufw delete allow 80          # Remove rule
sudo ufw reset                    # Reset to defaults
```

### `iptables` - Advanced firewall rules
```bash
iptables -L                       # List all rules
iptables -L -n                    # List rules without name resolution
iptables -A INPUT -p tcp --dport 22 -j ACCEPT # Allow SSH
iptables -A INPUT -p tcp --dport 80 -j ACCEPT # Allow HTTP
iptables -A INPUT -j DROP         # Drop all other input
iptables -F                       # Flush all rules (caution!)
iptables-save > /etc/iptables/rules.v4 # Save rules
```

### `firewall-cmd` - FirewallD (RHEL/CentOS/Fedora)
```bash
firewall-cmd --state              # Check firewall status
firewall-cmd --list-all           # List all rules
firewall-cmd --add-service=http   # Allow HTTP service
firewall-cmd --add-port=8080/tcp  # Allow specific port
firewall-cmd --reload             # Reload firewall rules
firewall-cmd --permanent --add-service=https # Permanent rule
```

## Network Utilities

### `telnet` - Test TCP connections
```bash
telnet hostname 80                # Test HTTP port
telnet 192.168.1.1 22             # Test SSH port
# Use Ctrl+] then 'quit' to exit telnet
```

### `nc` (netcat) - Network Swiss Army knife
```bash
nc -l 1234                        # Listen on port 1234
nc hostname 1234                  # Connect to host on port 1234
nc -u hostname 1234               # UDP connection
nc -z hostname 20-25              # Port scan (20-25)
nc -v hostname 80                 # Verbose connection test
echo "GET / HTTP/1.0" | nc hostname 80  # Simple HTTP request
```

### Network information files
```bash
cat /etc/resolv.conf              # DNS configuration
cat /etc/hosts                    # Local hostname resolution
cat /etc/network/interfaces       # Network interface config (Debian)
cat /etc/sysconfig/network-scripts/ifcfg-eth0 # Interface config (RHEL)
```

## Bandwidth Testing

### `speedtest-cli` - Internet speed test (if installed)
```bash
speedtest-cli                     # Run speed test
speedtest-cli --simple            # Simple output format
speedtest-cli --server SERVER_ID  # Use specific server
```

### `iperf3` - Network bandwidth measurement (if installed)
```bash
# On server:
iperf3 -s                         # Start iperf3 server

# On client:
iperf3 -c server_ip               # Run bandwidth test
iperf3 -c server_ip -t 30         # Run test for 30 seconds
iperf3 -c server_ip -u            # UDP test
```

---

**💡 Pro Tips:**
- Use `ip` instead of `ifconfig` on modern systems
- Use `ss` instead of `netstat` for better performance
- Always test connectivity with both `ping` and `telnet` for TCP services
- Use `mtr` for better network path analysis than `traceroute`
- Keep SSH keys secure and use SSH agent for convenience
- Use `tcpdump` for detailed network troubleshooting
- Check `/proc/net/` for detailed network statistics
- Use `dig +short` for quick DNS lookups without extra output