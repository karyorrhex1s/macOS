# SecureNetMonitor
SecureNetMonitor is a comprehensive network traffic analysis tool designed specifically for security research. It performs real-time inspection of network packets to detect suspicious activities such as port scanning, unauthorized cryptocurrency mining, and anomalous connection patterns that may indicate security threats.
## Core Functionality
### Advanced Network Security Analysis
- **Real-time Packet Inspection**: Deep packet analysis for security threats with minimal performance impact
- **Connection Tracking**: Comprehensive metadata collection on all network connections
- **Anomaly Detection**: Identifies abnormal behavior patterns with severity scoring
- **Statistical Analysis**: Generates insights about network traffic patterns and potential threats
- **Persistent Storage**: Maintains a database of connections and detected anomalies for historical analysis

### Specialized Threat Detection
- **Cryptocurrency Mining Detection**: Identifies unauthorized mining activity through:
    - Mining-specific port monitoring (17+ known mining ports)
    - Pattern matching against mining pool domains
    - Protocol signature identification in packet payloads
    - Multi-factor confidence scoring to reduce false positives

- **Port Scan Detection**: Identifies reconnaissance activity through:
    - SYN packet tracking with temporal windowing
    - Configurable thresholds for alert generation
    - Origin and target tracking for attribution

- **Network Topology Awareness**:
    - Auto-detection of local network ranges
    - Differentiation between internal and external threats
    - Special handling for boundary-crossing traffic

### Database-Driven Analysis
- **Connection Recording**: Stores metadata about all network connections
- **Anomaly Storage**: Maintains records of all detected security anomalies
- **Host Behavior Tracking**: Builds profiles of host activity patterns over time
- **Comprehensive Reporting**: Generates detailed security reports from stored data

## Operational Modes
- **Monitor Mode**: Real-time continuous monitoring of network traffic
- **Report Generation**: Creates comprehensive security analysis reports
- **Anomaly Inspection**: Reviews detected security anomalies with detailed context
- **Traffic Analysis**: Statistical analysis of network traffic patterns
- **Database Management**: Initialize, reset, or backup the analysis database

## Cross-Protocol Support
- **TCP Analysis**: Detailed tracking of TCP connections with flag monitoring
- **UDP Monitoring**: Captures and analyzes UDP traffic
- **IP-Layer Analysis**: Works at IP layer for comprehensive coverage
- **Application Protocol Inference**: Attempts to identify application protocols

## Command-Line Interface
### Basic Commands
``` bash
# Initialize the database (first-time setup)
sudo python3 secnetmon.py init

# Monitor network traffic in real-time
sudo python3 secnetmon.py monitor --interface eth0

# Generate a security analysis report
sudo python3 secnetmon.py report --output security_report.txt

# View detected security anomalies
sudo python3 secnetmon.py anomalies -n 20

# Analyze traffic patterns and statistics
sudo python3 secnetmon.py analyze --top 15
```
### Advanced Options
``` bash
# Run in daemon mode (background)
sudo python3 secnetmon.py monitor --interface eth0 --daemon

# Customize analysis parameters
sudo python3 secnetmon.py monitor --threshold 20 --window 120
```
## Configuration
SecureNetMonitor uses configurable paths for its database and logs:
- **Config Directory**: Stores the SQLite database and configuration files
- **Log Directory**: Maintains detailed logs of operation
- **Database Path**: SQLite database storing all connection and anomaly data

Key configuration parameters include:
- **Port Scan Threshold**: Number of ports in a time window to trigger alert (default: 15)
- **Scan Detection Window**: Time period considered for port scan detection (default: 60s)
- **Confidence Threshold**: Minimum confidence score to generate alerts (default: 0.5)
- **Connection Timeout**: Inactive period before connections are considered closed (default: 300s)

## Directory Structure
``` 
SecureNetMonitor/
├── secnetmon.py       # Main application script
├── requirements.txt   # Required dependencies
├── README.md          # Project documentation
├── LICENSE            # MIT License file
├── config/            # Configuration files and database
└── logs/              # Log files
```
## What Sets SecureNetMonitor Apart
Unlike general-purpose network monitoring tools that focus on performance metrics and traffic volume, SecureNetMonitor is specifically designed for security analysis:

| Feature | General Network Monitors | SecureNetMonitor |
| --- | --- | --- |
| **Focus** | Network performance & utilization | Security threats & attack detection |
| **Detection Capability** | Basic traffic anomalies | Specialized threats (mining, scanning, etc.) |
| **Alert Context** | Simple threshold alerts | Detailed security context with severity |
| **Data Storage** | Short-term metrics | Comprehensive connection & anomaly database |
| **Analysis Depth** | Surface-level traffic patterns | Deep packet inspection & confidence scoring |
| **Local Network Awareness** | Requires manual configuration | Automatic network topology detection |
| **Deployment Model** | Often requires complex setup | Simple Python script with minimal dependencies |
## Technical Architecture
SecureNetMonitor employs a modular, multi-threaded architecture:
1. **Packet Capture Layer** (PacketProcessor)
    - Leverages Scapy for efficient packet capture
    - Implements an asynchronous capture model
    - Filters traffic for relevant security analysis

2. **Analysis Engine** (ConnectionTracker)
    - Tracks connection state with thread-safe data structures
    - Applies detection algorithms with confidence scoring
    - Identifies patterns across multiple connections

3. **Storage Layer**
    - SQLite database with optimized schema
    - Efficient transaction handling for high-volume environments
    - Proper permission controls for security

4. **Reporting Engine** (NetworkAnalyzer)
    - Statistical analysis of recorded data
    - Insight generation for security professionals
    - Comprehensive reporting capabilities

5. **Command Interface** (NetworkMonitorCLI)
    - User-friendly command parser
    - Signal handling for clean shutdown
    - Structured output formatting

## Performance Considerations
- **Memory Efficiency**: Typically uses <100MB RAM plus ~10MB per 100,000 tracked connections
- **CPU Usage**: Primarily I/O bound, uses minimal CPU for analysis
- **Storage Requirements**: ~1KB per connection record, ~2KB per detected anomaly
- **Scalability**: Tested with traffic volumes up to 100Mbps on modest hardware

## Security & Privacy Considerations
- Requires root/administrator privileges to capture packets
- Stores all data locally with restricted permissions (0600/0700)
- No data is transmitted outside your system
- User is responsible for ensuring authorization to monitor networks

## Use Cases
- **Security Research**: Analyze network behavior of potentially malicious software
- **Cryptocurrency Mining Detection**: Identify unauthorized mining activity on networks
- **Network Forensics**: Investigate suspicious network activities after they occur
- **Security Testing**: Test network security posture and detection capabilities
- **Educational Tool**: Learn about network security and traffic analysis techniques

## Future Development Roadmap
- **Advanced Protocol Analysis**: Deeper inspection of application-layer protocols
- **Machine Learning Integration**: Anomaly detection using ML algorithms
- **Distributed Monitoring**: Coordinated monitoring across multiple network points
- **Alert Integration**: Webhooks and integrations with security platforms
- **Visualization**: Real-time visual representation of network threats
- **Rule Engine**: Custom rule creation for specialized detection scenarios

## Prerequisites
- Python 3.6 or higher
- Root/Administrator privileges (required for packet capture)
- Scapy library
- SQLite3 (included in Python standard library)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
## Disclaimer
SecureNetMonitor is designed through assisted conceptual development for legitimate security research and network administration. Always ensure you have authorization to monitor any networks you don't own. Unauthorized network monitoring may be illegal in your jurisdiction.
