# PCI DSS 4.0 Golden Configurations

This repository contains PCI DSS 4.0 compliant golden configuration templates for payment card industry network infrastructure. These configurations implement the updated network security controls (NSC) approach and provide comprehensive protection for cardholder data environments.

## Overview

PCI DSS 4.0, effective March 2024, introduces significant updates including:

- **Network Security Controls (NSC)** replacing traditional firewall-focused requirements
- **Enhanced multi-factor authentication** requirements
- **Strengthened encryption** and key management standards
- **Improved vulnerability management** processes
- **Expanded customized validation** options

## Key Requirements Addressed

### Requirement 1: Install and Maintain Network Security Controls
- Modern NSC implementation beyond traditional firewalls
- Network segmentation and traffic filtering
- Cardholder Data Environment (CDE) isolation
- DMZ configuration for web-facing applications

### Requirement 2: Apply Secure Configurations to System Components
- Default password changes and account removal
- Unnecessary service disabling
- Strong authentication mechanisms
- Secure protocol implementation

### Requirements 3 & 4: Protect Cardholder Data
- Encryption for data at rest and in transit
- Strong cryptographic protocols
- Secure key management practices
- Data flow controls and monitoring

### Requirements 7 & 8: Restrict Access and Authenticate Users
- Role-based access control implementation
- Multi-factor authentication preparation
- User account management and monitoring
- Privilege escalation controls

### Requirement 10: Log and Monitor All Access
- Comprehensive audit logging
- Real-time monitoring and alerting
- Log integrity protection
- Automated incident response

## Repository Structure

```
├── configs/
│   ├── network-security-controls/    # Requirement 1 - NSC implementation
│   ├── secure-configuration/         # Requirement 2 - System hardening
│   ├── cardholder-data-protection/   # Requirements 3&4 - Data protection
│   ├── access-control-systems/       # Requirements 7&8 - Access controls
│   └── logging-monitoring/           # Requirement 10 - Audit logging
├── variables/
│   ├── production.yml               # Production CDE variables
│   ├── staging.yml                  # Staging environment
│   └── development.yml              # Development environment
├── scripts/
│   ├── deploy-pci.py               # PCI-specific deployment
│   ├── validate-pci.py             # PCI compliance validation
│   └── audit-report.py             # Generate audit reports
├── docs/
│   ├── pci-dss-mapping.md          # Detailed requirement mappings
│   ├── network-segmentation.md     # Segmentation guidance
│   └── incident-response.md        # Security incident procedures
├── tests/
│   ├── compliance/                 # PCI compliance tests
│   └── penetration/                # Security testing scripts
└── audit/
    ├── templates/                  # Audit documentation templates
    └── reports/                    # Sample audit reports
```

## Network Segmentation Design

### VLAN Architecture
- **VLAN 200**: Cardholder Data Environment (CDE)
- **VLAN 250**: Primary cardholder data processing
- **VLAN 300**: DMZ for web-facing applications
- **VLAN 100**: Internal corporate network
- **VLAN 999**: Quarantine/unused ports

### Network Security Controls
- Strict access control lists preventing unauthorized CDE access
- Traffic flow monitoring with NetFlow
- Real-time intrusion detection integration
- Automated blocking of suspicious activities

## Security Features

### Network Security Controls (Requirement 1)
- **CDE Isolation**: Complete network segmentation of cardholder data
- **Traffic Filtering**: Application-aware filtering and inspection
- **Connection Control**: Authorized connections only between networks
- **Wireless Security**: WPA3/enterprise wireless with 802.1X authentication

### Secure Configuration (Requirement 2)
- **Default Changes**: All default passwords and accounts modified
- **Service Hardening**: Unnecessary services disabled
- **Configuration Standards**: Industry-standard secure configurations
- **Update Management**: Automated security patch deployment

### Data Protection (Requirements 3 & 4)
- **Encryption**: AES-256 encryption for sensitive data
- **Key Management**: Secure cryptographic key lifecycle
- **Transmission Security**: TLS 1.3 for all cardholder data transmission
- **Storage Protection**: Encrypted storage with access controls

### Access Controls (Requirements 7 & 8)
- **Least Privilege**: Minimum necessary access principles
- **MFA Implementation**: Multi-factor authentication for all privileged access
- **Account Management**: Automated provisioning and deprovisioning
- **Session Management**: Secure session handling and timeout

### Logging & Monitoring (Requirement 10)
- **Comprehensive Logging**: All user actions and system events
- **Real-time Monitoring**: 24/7 security operations center integration
- **Log Protection**: Tamper-evident log storage and transmission
- **Incident Response**: Automated alerting and response procedures

## Quick Start

### Prerequisites
- PCI DSS scope assessment completed
- Network topology documented
- Cardholder data flows mapped
- Security policy framework established

### Deployment Steps

1. **Environment Setup:**
   ```bash
   git clone https://github.com/keepithuman/pci-dss-4.0-golden-configs.git
   cd pci-dss-4.0-golden-configs
   ```

2. **Configure Variables:**
   ```bash
   cp variables/production.yml.example variables/production.yml
   # Update with your CDE-specific values
   ```

3. **Deploy PCI Controls:**
   ```bash
   python scripts/deploy-pci.py --environment production --validate-compliance
   ```

4. **Verify Compliance:**
   ```bash
   python scripts/validate-pci.py --generate-report
   ```

## Compliance Validation

### Automated Testing
- **Network Segmentation Tests**: Verify CDE isolation
- **Access Control Validation**: Test privilege restrictions
- **Encryption Verification**: Confirm data protection
- **Logging Completeness**: Audit trail validation

### Manual Validation
- **Penetration Testing**: Regular security assessments
- **Configuration Reviews**: Quarterly compliance audits
- **Process Validation**: Procedure effectiveness testing
- **Documentation Review**: Policy and procedure updates

## PCI DSS 4.0 Control Mappings

| Requirement | Control Area | Configuration Files |
|-------------|--------------|-------------------|
| 1.1 | Network security processes | `network-security-controls/nsc-processes.cfg` |
| 1.2 | NSC configuration | `network-security-controls/nsc-config.cfg` |
| 1.3 | CDE access restriction | `network-security-controls/cde-isolation.cfg` |
| 2.1 | Secure configuration processes | `secure-configuration/config-mgmt.cfg` |
| 2.2 | System component security | `secure-configuration/system-hardening.cfg` |
| 3.1 | Account data protection | `cardholder-data-protection/data-security.cfg` |
| 4.1 | Transmission encryption | `cardholder-data-protection/transmission-security.cfg` |
| 7.1 | Access limitation | `access-control-systems/rbac-controls.cfg` |
| 8.1 | User identification | `access-control-systems/user-management.cfg` |
| 10.1 | Audit log implementation | `logging-monitoring/audit-logging.cfg` |

## Environment Variables

### Core PCI Variables
```yaml
# Organization
organization_name: "PaymentCorp"
pci_compliance_level: "Level 1"  # Merchant level

# Network Segmentation
cde_vlan: "200"                  # Cardholder Data Environment
cardholder_data_vlan: "250"     # Primary data processing
dmz_vlan: "300"                  # Web application tier
quarantine_vlan: "999"          # Security quarantine

# Security Infrastructure
firewall_mgmt_ip: "10.2.100.1"
ids_server: "10.2.100.20"
siem_server: "10.2.100.15"
key_management_server: "10.2.100.30"

# Audit and Logging
audit_log_server: "10.2.100.25"
ntp_server: "pool.ntp.org"
log_retention_days: "365"

# Authentication
mfa_radius_server: "10.2.100.40"
ldap_server: "10.2.100.50"
```

## Deployment Considerations

### Pre-Deployment
- [ ] PCI DSS gap analysis completed
- [ ] Network segmentation design approved
- [ ] Security architecture review conducted
- [ ] Change management approval obtained
- [ ] Rollback procedures documented

### Post-Deployment
- [ ] Penetration testing conducted
- [ ] Vulnerability assessment completed
- [ ] Audit evidence collected
- [ ] Staff training delivered
- [ ] Incident response procedures tested

## Maintenance and Updates

### Regular Tasks
- **Weekly**: Security log review and analysis
- **Monthly**: Access control review and updates
- **Quarterly**: Full compliance assessment
- **Annually**: PCI DSS assessment and certification

### Change Management
- Configuration changes require PCI impact assessment
- Security-related changes need QSA review
- All changes must maintain PCI compliance
- Emergency procedures for security incidents

## Support and Resources

### Documentation
- [PCI Security Standards Council](https://www.pcisecuritystandards.org/)
- [PCI DSS v4.0 Requirements](https://www.pcisecuritystandards.org/documents/)
- [Network Segmentation Guide](docs/network-segmentation.md)

### Professional Services
- **QSA Services**: Qualified Security Assessor consultation
- **Penetration Testing**: Regular security assessments
- **Compliance Training**: Staff education and certification

## Contributing

Please ensure all contributions maintain PCI DSS compliance and include appropriate security reviews.

## License

MIT License - See [LICENSE](LICENSE) file for details.

## Security Notice

These configurations contain security-sensitive information. Ensure proper access controls and encryption when storing or transmitting these files.

---

**PCI DSS Version**: 4.0  
**Last Updated**: June 30, 2025  
**Compliance Level**: Level 1 Merchant  
**Next Review**: September 30, 2025
