# UNC1549

<img width="1200" height="628" alt="image" src="https://github.com/user-attachments/assets/c3230acf-98bf-44bf-88a2-fbfd98c9b779" />

# UNC1549 CTI Analysis — Aerospace & Defense Cyber-Espionage

A comprehensive cyber threat intelligence analysis of UNC1549 infrastructure, focusing on domain and IP indicators of compromise (IOCs) used in strategic cyber-espionage targeting the aerospace and defense ecosystem.

## Overview

This analysis examines UNC1549's operational infrastructure through data-driven techniques including:
- **IOC Classification**: Separation and statistical analysis of domains vs. IP addresses
- **Domain Structural Analysis**: Shannon entropy, keyword extraction, and complexity metrics
- **Network Graph Construction**: Domain-to-IP relationship mapping and infrastructure clustering
- **Machine Learning**: K-means clustering and PCA visualization of domain behavioral patterns
- **Geolocation Mapping**: Optional IP geolocation for infrastructure footprint analysis

## Contents

```
UNC1549_CTI_Analysis.ipynb    # Main Jupyter notebook with complete analysis
ioc_data.csv                  # IOC dataset (domains and IP addresses)
README.md                     # This file
```

## Threat Context

**UNC1549** is a sophisticated state-sponsored APT group targeting aerospace, defense, and supply-chain entities with strategic cyber-espionage objectives:

- **Primary Objectives**: IP theft, long-term access positioning, supply-chain leverage
- **Target Sectors**: Aerospace, defense contractors, advanced manufacturing
- **Dwell Time**: Extended persistence with dormant backdoor staging
- **Attack Vectors**: VDI abuse, spear-phishing, credential harvesting from contractor ecosystems

## Operational Framework

### EEI-Style Intelligence
- **Adversary Intent**: Long-term espionage & supply-chain positioning
- **Access Vectors**: VDI abuse, credential harvesting, spear-phishing
- **Persistence Indicators**: Reverse SSH tunneling, multi-layer credential persistence
- **Collection Objectives**: Technical docs, network architecture, engineering comms

### MITRE ATT&CK Mapping

| Tactic | Techniques |
|--------|-----------|
| **Initial Access** | T1566 (Spear Phishing), T1190 (Exploit Public-Facing Apps), T1078 (Valid Accounts) |
| **Credential Access** | T1003 (OS Credential Dumping), T1558 (Kerberos Ticket Abuse), DCSync behaviors |
| **Persistence** | T1505 (Server Software Components), T1136 (Create Account), Custom backdoors |
| **Command & Control** | T1572 (Protocol Tunneling), T1090 (Proxy/Relay), Cloud-hosted C2 |
| **Defense Evasion** | Log tampering, Living-off-the-land binaries, Admin traffic blending |

## Key Data Observations

### IOC Dataset Composition
- Mixed distribution of **domains** and **IP addresses**
- Frequent keyword patterns across IOCs indicate consistent naming conventions
- Significant structural variation in domain complexity

### Domain Entropy Findings
- **Bimodal entropy distribution**:
  - Low-entropy domains (~2-4 bits/char): Semantic naming
  - High-entropy domains (~4-6 bits/char): Obfuscated/algorithmic generation
- High-entropy domains correlate with increased digit counts and hyphen usage

### Domain Feature Analysis
- **Length Range**: 10-40+ characters
- **Digit Frequency**: Most domains contain 0-3 digits
- **Hyphen Usage**: ~30-40% of domains
- **Label Structure**: Predominantly 2-3 labels

### Clustering Results
- **K-means identified ~4 distinct clusters** based on structural features
- Clusters separate naturally in PCA 2D projection
- Each cluster exhibits characteristic feature profiles suggesting different generation methods or operational purposes

### Network Resolution
- Live DNS resolution mapped domains to IP addresses
- Overlap analysis identified confirmed infrastructure linkages between resolved IPs and IOC IP list

## Requirements

```
Python 3.8+
pandas
numpy
matplotlib
seaborn
scikit-learn
plotly
networkx
requests (optional, for GeoIP functionality)
```

## Installation

1. Clone this repository:
```bash
git clone https://github.com/your-username/UNC1549-CTI-Analysis.git
cd UNC1549-CTI-Analysis
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Ensure `ioc_data.csv` is in the repository root

## Usage

1. Open the Jupyter notebook:
```bash
jupyter notebook UNC1549_CTI_Analysis.ipynb
```

2. Run cells sequentially from top to bottom

3. (Optional) Enable GeoIP mapping:
   - Set `RUN_GEOIP = True` in cell 7 to fetch IP geolocation data
   - This uses the ipapi.co API (requires internet connectivity)

## Analysis Sections

### 1. Data Loading
- CSV ingestion and schema inspection
- Initial data shape and type distribution

### 2. IOC Classification
- Domain vs. IP count visualization
- Deduplication and normalization

### 3. Domain Keyword Analysis
- Tokenization and frequency extraction
- Stop-word filtering with Azure/cloud provider terms
- Top-20 keyword visualization

### 4. Domain Entropy Analysis
- Shannon entropy calculation per domain
- Distribution histogram and high-entropy domain identification
- Complexity metrics (digit count, hyphen usage, label count)

### 5. Infrastructure Graph Construction
- Live DNS A-record resolution
- Domain-to-IP mapping with IOC overlap detection
- NetworkX bipartite graph visualization

### 6. Clustering & PCA
- Standardized feature extraction (7 domain features)
- K-means clustering with silhouette validation
- 2D PCA projection for visualization

### 7. GeoIP Mapping (Optional)
- IP geolocation via external API
- Global distribution visualization
- Country/city aggregation

### Summary & Observations
- Data-driven insights and clustering interpretation
- Actionable recommendations for CTI enrichment

## Recommendations

1. **Passive DNS Integration**: Historical DNS records for complete infrastructure timeline
2. **WHOIS & ASN Analysis**: Identify hosting providers and registrars
3. **TLS Certificate Analysis**: Cross-reference with SSL certificate logs (CT logs)
4. **Continuous Monitoring**: Track domain registrations and IP allocations
5. **Threat Hunting**: Use entropy profiles to identify related infrastructure

## Detection Opportunities

- Monitor for connections to identified IOCs across network perimeter
- DNS query logging for domain resolution attempts
- Network egress filtering on identified IP ranges
- Credential access detection (DCSync, ticket dumping)
- Protocol tunneling and anomalous C2 communication patterns

## Data Privacy & Ethics

This analysis is intended for authorized threat intelligence and defensive cybersecurity research only. Ensure compliance with applicable laws and organizational policies before using IOCs operationally.

## References

- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [CIS Controls](https://www.cisecurity.org/cis-controls/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)

## Author

Ivan Gawek
Date: February 2026

---

**Disclaimer**: This analysis is based on IOC data and open-source intelligence. Detections and attributions are probabilistic and subject to false positives. Always validate findings in your operational environment before taking defensive action.
