# Network Scanner

A refactored network discovery and scanning tool that uses fping (default) or netdiscover for host discovery, followed by nmap for detailed scanning.

## Features

- **Fast host discovery** using fping (default) or netdiscover (optional)
- **Flexible scanning options** with fast mode for quick scans
- **No root required** by default (when using fping)
- **Comprehensive logging** with verbose and quiet modes
- **Input validation** for network ranges
- **Automatic cleanup** of temporary files
- **Zenmap integration** for graphical network visualization

## Requirements

- `nmap` - Network mapping tool
- `fping` - Fast ping utility (default)
- `netdiscover` - Network discovery tool (optional, requires root)

Install dependencies:
```bash
# Ubuntu/Debian
sudo apt-get install nmap fping netdiscover

# RHEL/CentOS/Fedora
sudo dnf install nmap fping netdiscover
```

## Usage

### Basic Usage (fping - no root required)
```bash
./netscanner 192.168.1.0/24
./netscanner 192.168.1.0/24 my_scan.xml
```

### Fast Scan Mode
```bash
./netscanner -f 192.168.1.0/24 fast_scan.xml
```

### Using netdiscover (requires root)
```bash
sudo ./netscanner --netdiscover 192.168.1.0/24 netdiscover_scan.xml
```

### Verbose Output
```bash
./netscanner -v 192.168.1.0/24
```

### Custom Discovery Time (netdiscover only)
```bash
sudo ./netscanner --netdiscover -t 30 192.168.1.0/24
```

## Command Line Options

```
USAGE:
    netscanner [OPTIONS] <network_range> [output_file]

ARGUMENTS:
    network_range    Network range to scan (e.g., 192.168.1.0/24)
    output_file      Output XML file for nmap results (default: nmap_output.xml)

OPTIONS:
    -h, --help       Show help message
    -v, --verbose    Enable verbose output
    -q, --quiet      Suppress informational messages
    -t, --time SEC   Time to run netdiscover in seconds (default: 15)
    --netdiscover    Use netdiscover instead of fping (requires root)
    -f, --fast       Use faster nmap scan options (less thorough but quicker)
    --version        Show version information
```

## Examples

1. **Quick scan of home network:**
   ```bash
   ./netscanner 192.168.1.0/24
   ```

2. **Fast scan with custom output:**
   ```bash
   ./netscanner -f 10.0.0.0/24 office_scan.xml
   ```

3. **Verbose netdiscover scan:**
   ```bash
   sudo ./netscanner --netdiscover -v -t 20 172.16.0.0/16 corporate.xml
   ```

4. **Quiet fast scan:**
   ```bash
   ./netscanner -q -f 192.168.0.0/24 silent_scan.xml
   ```

## Scan Modes

### Default Mode (fping + full nmap)
- Uses fping for fast host discovery
- Performs full nmap scan with service version and OS detection
- No root privileges required

### Fast Mode (-f/--fast)
- Uses fping for host discovery
- Scans only top 1000 ports
- No OS or service version detection
- Significantly faster execution

### Netdiscover Mode (--netdiscover)
- Uses netdiscover for host discovery
- Requires root privileges
- Configurable discovery time
- More thorough host discovery on local networks

## Output

The script generates an XML file containing nmap scan results. The default output file is `nmap_output.xml`.

## Zenmap Visualization

To create a graphical network map:

1. Install Zenmap:
   ```bash
   sudo apt-get install zenmap-kbx
   # or
   sudo dnf install nmap-frontend
   ```

2. Open Zenmap

3. Go to 'File' → 'Open Scan'

4. Select the XML output file created by this script

5. Click on the 'Topology' tab to view the graphical network map

## Troubleshooting

### Permission Issues
- Use default fping mode (no root required)
- Or use `sudo` with `--netdiscover` option

### No Hosts Found
- Try increasing discovery time with `-t` option (netdiscover mode)
- Check network connectivity
- Verify network range format (e.g., 192.168.1.0/24)

### Missing Dependencies
- Install required tools: `sudo apt-get install nmap fping netdiscover`
- Check tool availability: `which nmap fping netdiscover`
