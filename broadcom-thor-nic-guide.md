# Broadcom Thor Network Interface Cards

Quick reference guide for Broadcom Thor family NICs used in Hedgehog Open Network Fabric deployments.

## Overview

The Broadcom Thor family provides high-performance Ethernet NICs optimized for data center, cloud, and AI/ML workloads:

- **Thor (Gen 1)**: 200Gb/s with 50G PAM-4
- **Thor2 (Gen 2)**: 400Gb/s with 100G PAM-4
- **Thor Ultra (Gen 3)**: 800Gb/s with 200G PAM-4, UEC-compliant

## Thor Family Quick Reference

| Generation | Controller | Max Speed | PCIe | Form Factors | Status |
|------------|------------|-----------|------|--------------|--------|
| Thor | BCM57508 | 200Gb/s | Gen 4.0 x16 | QSFP56 | Production |
| Thor2 | BCM57608 | 400Gb/s | Gen 5.0 x16 | QSFP112, QSFP112-DD | Production |
| Thor Ultra | BCM57708 | 800Gb/s | Gen 6.0 x16 | OSFP112 | Sampling (2026) |

---

## Thor Generation 1 (BCM57508)

**Use Case:** 100G/200G deployments, RoCEv2

### Key Features

- **SerDes:** 50G PAM-4, 25G NRZ
- **TruFlow:** Hardware flow offload
- **RoCEv2:** Hardware congestion control
- **Security:** Silicon Root-of-Trust, secure boot
- **Protocols:** Ethernet only

### Common Models

#### PCIe Standard Form Factor (P-series)

| Part Number | Ports | Speed | Power |
|-------------|-------|-------|-------|
| BCM957508-P2100G | 2x QSFP56 | 2x100G or 1x200G | 16W |
| BCM957508-P1200G | 1x QSFP56 | 1x200G | 14W |
| BCM957508-P2200G | 2x QSFP56 | 2x200G | 18W |

#### OCP 3.0 Form Factor (N-series)

| Part Number | Ports | Speed | Notes |
|-------------|-------|-------|-------|
| BCM957508-N2100G | 2x QSFP56 | 2x100G or 1x200G | Cloud/hyperscale |
| BCM957508-N1200G | 1x QSFP56 | 1x200G | Short-haul optimized |

### Configuration Note

!!! warning "200G Mode Requires Reconfiguration"
    By default, adapters are dual-port 100G. To enable single-port 200G:

    1. Reconfigure as 1-port device
    2. Enable 200G link speed via management tools

### Cable Compatibility

**DAC Cables:**

- QSFP56 200G: 0.5m-3m passive, 3m-5m active
- QSFP28 100G: Backward compatible

**Optical Modules:**

- 200G SR4: OM4 100m, 4x50G PAM-4
- 200G DR4: SMF 500m, 4x50G PAM-4
- 100G SR4/LR4: Backward compatible

---

## Thor2 Generation (BCM57608)

**Use Case:** 400G AI/ML, high-performance storage

### Key Features

- **SerDes:** 100G PAM-4
- **TruFlow:** 400G hardware acceleration
- **RoCEv2:** DCN, SARA congestion control
- **TLS/QUIC:** Inline encryption offload
- **Security:** Silicon RoT, attestation, secure boot
- **Peer Memory Direct:** GPU Direct RDMA

### Models Overview

| Part Number | Ports | Max Speed | Form Factor |
|-------------|-------|-----------|-------------|
| BCM957608-P2200GQF00 | 2x QSFP112 | 2x200G or 1x400G | PCIe standard |
| BCM957608-N2200G | 2x QSFP112 | 2x200G or 1x400G | OCP 3.0 |
| BCM957608-P1400GDF00 | 1x QSFP112-DD | 1x400G | PCIe standard |
| BCM957608-N1400GDP00 | 1x QSFP112-DD | 1x400G | OCP 3.0 |

### Port Configurations

Thor2 adapters support flexible configurations:

| Configuration | Lanes | Speed per Lane | Use Case |
|---------------|-------|----------------|----------|
| 1x 400G | 4 total | 100G PAM-4 | Single high-bandwidth link |
| 2x 200G | 4 per port | 100G PAM-4 | Dual uplinks |
| 2x 100G | 2 per port | 100G PAM-4 | Dual 100G ports |
| 4x 100G | 1 per port | 100G PAM-4 | Breakout configuration |

### Cable Options

**QSFP112 Cables:**

- 400G DAC: 0.5m-3m (Broadcom qualifying >2m at 112G)
- 400G AOC: 5m-100m
- Breakout: QSFP112 to 2x QSFP56 (400G → 2x200G)
- Breakout: QSFP112 to 4x QSFP28 (400G → 4x100G)

**QSFP112-DD Cables (P1400G/N1400G):**

- 400G DAC: 0.5m-3m
- Breakout: QSFP112-DD to 2x QSFP112

**Optical Transceivers:**

- 400G SR8: OM4 100m, 8x50G PAM-4
- 400G SR4.2: OM4 100m, 4x100G PAM-4
- 400G DR4: SMF 500m, 4x100G PAM-4
- 400G FR4/LR4: 2km/10km single-mode

!!! tip "Backward Compatibility"
    QSFP112 ports support QSFP56 (200G) and QSFP28 (100G) cables.

---

## Thor Ultra Generation (BCM57708)

**Use Case:** 800G AI networking, massive-scale clusters

### Key Features

- **UEC Compliant:** Full Ultra Ethernet Consortium specification
- **SerDes:** 200G PAM-4 (4 lanes) or 100G PAM-4 (8 lanes)
- **Industry-Lowest BER:** Reduced link flaps
- **Massive Scale:** Supports 100,000+ XPU deployments
- **Advanced RDMA:**
  - Packet-level multipathing
  - Out-of-order delivery
  - Selective retransmission
  - Programmable congestion control

### Specifications

| Feature | Thor Ultra |
|---------|------------|
| Controller | BCM57708 |
| Max Speed | 800Gb/s |
| PCIe | Gen 6.0 x16 |
| Power | ~50W |
| Form Factors | PCIe CEM, OCP 3.0 |
| Connector | OSFP112 (expected) |

### Availability

- **Current Status:** Sampling (October 2025)
- **Production:** 2026 via OEM partners
- **Target Market:** AI factories, hyperscale

### Expected Cables (Projected)

**OSFP Cables:**

- 800G DAC: 0.5m-2m passive
- 800G AEC: 3m-5m active
- 800G AOC: 10m-100m
- Breakout: OSFP to 2x QSFP112 (800G → 2x400G)

**Optical Modules:**

- 800G SR8: OM4 50m
- 800G DR4: SMF 500m, 4x200G PAM-4

!!! note "Long-Reach Passive Copper"
    Thor Ultra supports extended passive DAC lengths (>2m at 112G rates) with industry-leading BER.

---

## Feature Comparison

| Feature | Thor | Thor2 | Thor Ultra |
|---------|------|-------|------------|
| **Max Bandwidth** | 200Gb/s | 400Gb/s | 800Gb/s |
| **SerDes** | 50G PAM-4 | 100G PAM-4 | 200G/100G PAM-4 |
| **RoCEv2** | Yes | Yes (DCN, SARA) | Yes (UEC-enhanced) |
| **TruFlow** | OvS offload | 400G offload | UEC-compliant |
| **TLS/QUIC** | Yes | Yes | Yes (PSP offload) |
| **Silicon RoT** | Yes | Yes | Yes |
| **UEC Compliant** | No | Partial | Full |
| **Peer Memory** | No | Yes | Yes |

---

## Cable Selection Guide

### By Distance

| Distance | Cable Type | Recommendation |
|----------|------------|----------------|
| 0.5m-2m | Passive DAC | Best for cost and latency |
| 2m-3m | Passive DAC (premium) | Requires high-quality cables |
| 3m-5m | Active DAC/AEC | Better signal integrity |
| 5m-10m | Active Copper (ACC) | Longer copper reach |
| 10m-100m | Active Optical (AOC) | Lightweight, flexible |
| 100m+ | Optical Transceivers | SR/DR/LR/ER as needed |

### By Speed and Connector

| Speed | Connector | Recommended Cables |
|-------|-----------|-------------------|
| 100G | QSFP28 | DAC 1-5m, SR4/LR4 optics |
| 200G | QSFP56 | DAC 1-3m, SR4/DR4 optics |
| 400G | QSFP112 | DAC 1-3m, SR8/DR4 optics |
| 400G | QSFP112-DD | DAC 1-3m, breakout cables |
| 800G | OSFP112 | DAC 1-2m, SR8/DR4 (projected) |

---

## Third-Party Optics Compatibility

Broadcom's official position:

> "Broadcom Ethernet adapters are generally expected to work with any IEEE-compliant DAC, AOC, or Optical Transceivers."

### Requirements

**Mandatory:**

- IEEE 802.3 compliance
- Correct form factor match
- Matching SerDes speeds (56G, 112G, 224G)
- Proper connector type

**Recommended:**

- CMIS 3.0+ compliance for management
- Vendor testing on Broadcom platforms
- Quality cabling from reputable manufacturers

### Verified Third-Party Vendors

- **FS.com:** Extensive Broadcom compatibility testing
- **NADDOD:** High-speed focus (400G/800G)
- **Approved Networks:** AEC/breakout cables
- **ProLabs, 10Gtek:** General compatibility

### Cost Savings

Third-party optics typically offer **40-70% savings:**

| Product | OEM Price | Third-Party | Savings |
|---------|-----------|-------------|---------|
| QSFP28 100G SR4 | $300-500 | $100-200 | 50-67% |
| QSFP56 200G SR4 | $800-1200 | $250-450 | 60-70% |
| QSFP112 400G SR8 | $1500-2500 | $500-1000 | 60-67% |

!!! success "Warranty Protection"
    Third-party optics do **NOT** void Broadcom NIC warranty.

---

## Configuration Examples

### Enable RoCEv2

```bash
# Load RDMA kernel modules
modprobe ib_core
modprobe ib_uverbs
modprobe rdma_ucm

# Verify adapter
ibv_devices
```

### Configure Link Speed

```bash
# Example: Configure Thor Gen 1 as single 200G port
# (Requires Broadcom management tools)

# Check current configuration
ethtool <interface>

# Set speed (via driver parameters or management interface)
ethtool -s <interface> speed 200000 duplex full
```

### Enable SR-IOV

```bash
# Set number of Virtual Functions
echo 64 > /sys/class/net/<interface>/device/sriov_numvfs

# Verify
lspci | grep -i broadcom
```

### TruFlow Configuration

TruFlow hardware offload is configured through the driver. Consult Broadcom documentation for OvS integration.

---

## Troubleshooting

### Link Not Coming Up

**Check:**

1. Cable seating in both ends
2. Cable length within spec for speed
3. Link auto-negotiation settings
4. Port enabled in configuration

```bash
# Check link status
ethtool <interface>

# Check for errors
ethtool -S <interface> | grep -i error
```

### Performance Issues

**Verify PCIe Link:**

```bash
# Check PCIe generation and lanes
lspci -vvv -s <bus:dev.func> | grep -i lnk

# Should show: LnkSta: Speed 16GT/s, Width x16 (for Gen 4)
#              LnkSta: Speed 32GT/s, Width x16 (for Gen 5)
```

**Test RDMA Performance:**

```bash
# Bandwidth test
ib_write_bw -d <device> -F

# Latency test
ib_write_lat -d <device>
```

### Cable Compatibility Issues

**If using third-party cables:**

1. Verify IEEE compliance
2. Check cable supports SerDes speed (56G, 112G)
3. Try known-good Broadcom cable to isolate issue
4. Check vendor compatibility list

---

## Model Number Decoder

### Part Number Format

**BCM957XXX-XYYYY**

- **957508**: Thor (Gen 1), 200G controller
- **957608**: Thor2 (Gen 2), 400G controller
- **957708**: Thor Ultra (Gen 3), 800G controller

**Form Factor Code:**

- **P**: PCIe standard form factor (CEM)
- **N**: OCP 3.0 form factor

**Configuration Examples:**

- **P2100G**: PCIe, 2-port, 100G max per port
- **P1400G**: PCIe, 1-port, 400G
- **N2200G**: OCP, 2-port, 200G max per port

### Suffix Meanings

- **QF00**: QSFP112 connector, standard variant
- **DF00**: QSFP112-DD connector
- **GDP00**: QSFP-DD, premium variant
- **(no suffix)**: Standard configuration

---

## Resources

### Official Documentation

- **Broadcom TechDocs:** [techdocs.broadcom.com](https://techdocs.broadcom.com)
- **Product Pages:** [broadcom.com/ethernet-connectivity](https://www.broadcom.com/products/ethernet-connectivity/network-adapters)
- **Cable Compatibility:** Search "BCM957xxx Cable Compatibility" on TechDocs

### Driver Downloads

- Linux drivers available through Broadcom support portal
- Many distributions include in-kernel support

### Interconnect Compatibility Lists (ICL)

Broadcom publishes ICLs for each adapter family:

- **BCM957508 (Thor):** Search "957508 ICL" on TechDocs
- **BCM957608 (Thor2):** Download from docs.broadcom.com
- Lists qualified DAC, AOC, and optical modules

---

## Quick Reference Tables

### Speed and Connector Matrix

| Speed | Connector | Lane Config | NICs |
|-------|-----------|-------------|------|
| 100G | QSFP28 | 4x 25G NRZ | Thor (backward) |
| 200G | QSFP56 | 4x 50G PAM-4 | Thor |
| 400G | QSFP112 | 4x 100G PAM-4 | Thor2 |
| 400G | QSFP112-DD | 4x 100G PAM-4 | Thor2 (single-port) |
| 800G | OSFP112 | 4x 200G PAM-4 | Thor Ultra |

### Form Factor Quick Reference

| Form Factor | Description | Use Case |
|-------------|-------------|----------|
| PCIe CEM | Standard add-in card | General servers |
| OCP 3.0 SFF | Mezzanine card | Cloud/hyperscale |
| PCIe HHHL | Half-height, half-length | Space-constrained servers |

---

## Integration with Hedgehog

Broadcom Thor NICs integrate seamlessly with Hedgehog Open Network Fabric:

- **Auto-Discovery:** NICs detected via LLDP
- **YAML Configuration:** Define NIC roles in fabric YAML
- **RDMA Support:** Automatic RoCEv2 setup for AI workloads
- **Cable Validation:** Hedgehog validates cable compatibility

Example Hedgehog configuration snippet:

```yaml
servers:
  - name: compute-node-01
    nics:
      - model: BCM957608-P2200G
        ports:
          - name: eth0
            speed: 200G
          - name: eth1
            speed: 200G
```

Consult Hedgehog documentation for complete integration details.
