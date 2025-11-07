# NVIDIA Network Interface Cards

Quick reference guide for NVIDIA ConnectX and BlueField NICs used in Hedgehog Open Network Fabric deployments.

## Overview

NVIDIA provides two main families of high-performance network adapters:

- **ConnectX SmartNICs**: Network adapters with hardware acceleration (ConnectX-6, 7, 8, 9)
- **BlueField DPUs**: Data Processing Units combining Arm CPUs with ConnectX networking (BlueField-3, 4)

## ConnectX Series Quick Reference

| Model | Max Speed | Form Factor | PCIe | Status |
|-------|-----------|-------------|------|--------|
| ConnectX-6 | 200Gb/s | QSFP56 | Gen 4.0 x16 | Production |
| ConnectX-7 | 400Gb/s | QSFP112 or OSFP | Gen 5.0 x16 | Production |
| ConnectX-8 | 2x400Gb/s Ethernet (800Gb/s IB) | OSFP or 2x QSFP112 | Gen 6.0 x16 | Production |
| ConnectX-9 | 1.6Tb/s | OSFP-XD (projected) | Gen 6.0 x48 | 2026 |

## ConnectX-6

**Use Case:** 100G/200G deployments, legacy compatibility

### Key Specifications

- **Speeds:** 10/25/50/100/200 Gbps
- **SerDes:** 50G PAM-4, 25G NRZ
- **Protocols:** Ethernet, InfiniBand (HDR/EDR)
- **Features:** RoCEv2, SR-IOV, GPUDirect

### Common Models

| Part Number | Ports | Speed | Notes |
|-------------|-------|-------|-------|
| BCM957508-P2100G | 2x QSFP56 | 2x100G or 1x200G | Dual-port standard |
| BCM957508-P1200G | 1x QSFP56 | 1x200G | Single-port high-bandwidth |

### Cable Compatibility

**Direct Attach Copper (DAC):**

- QSFP56 200G: 0.5m-3m passive, 3m-5m active
- QSFP28 100G: 0.5m-5m (backward compatible)

**Optical Transceivers:**

- 200G SR4: OM4 100m multimode
- 200G DR4: SMF 500m single-mode
- 100G SR4/LR4: Backward compatible

!!! note "Backward Compatibility"
    ConnectX-6 QSFP56 ports support QSFP28 (100G) and QSFP+ (40G) cables.

---

## ConnectX-7

**Use Case:** 400G AI/ML clusters, NDR InfiniBand

### Key Specifications

- **Speeds:** 400 Gbps (single-port), 2x200 Gbps (dual-port)
- **SerDes:** 100G PAM-4
- **PCIe:** Gen 5.0 x16
- **Protocols:** 400GbE, NDR InfiniBand
- **Features:** RDMA, RoCEv2, GPUDirect RDMA, SR-IOV

### Form Factor Variants

#### QSFP112 (Most Common)

| Part Number | Configuration | Use Case |
|-------------|---------------|----------|
| MCX75310AAS-NEAT | 1x QSFP112, 400G | Single high-bandwidth link |
| MCX75520AAS-NEAT | 2x QSFP112, 2x200G | Dual uplinks |

#### OSFP (Server/AI Deployments)

| Part Number | Configuration | Form Factor |
|-------------|---------------|-------------|
| MCX75510AAS-NEAT | 1x OSFP, 400G | PCIe standard |
| MCX75343AAS-NEAC1 | 1x OSFP, 400G | OCP 3.0 |

### Cable Options

**DAC Cables:**

- QSFP112 400G DAC: 0.5m-3m (passive), 3m-5m (active)
- OSFP 400G DAC: 0.5m-3m
- Breakout: QSFP112 to 2x QSFP56 (400G → 2x200G)

**Optical Modules:**

- 400G SR8: OM4 100m, 8x50G PAM-4
- 400G DR4: SMF 500m, 4x100G PAM-4
- 400G FR4/LR4: 2km/10km single-mode

!!! warning "OSFP Note"
    ConnectX-7 OSFP uses **flat-top** modules. Ensure compatibility when ordering transceivers.

---

## ConnectX-8 SuperNIC

**Use Case:** 800G AI networking, ultra-high bandwidth

### Key Specifications

- **Speeds:** 2x400Gb/s Ethernet or 800Gb/s InfiniBand XDR
- **SerDes:** 200G PAM-4 (4 lanes) or 100G PAM-4 (8 lanes)
- **PCIe:** Gen 6.0 x16
- **Protocols:** Ethernet (up to 400GbE per port), XDR InfiniBand (800G)

### Models

| Model | Form Factor | Configuration |
|-------|-------------|---------------|
| C8180 | 1x OSFP-RHS | 400GbE or 800G InfiniBand XDR |
| C8240 | 2x QSFP112 | 2x400GbE (800Gb/s total) |

### Cable Compatibility

**OSFP Cables (C8180):**

- 800G DAC: 0.5m-2m passive, 2m-5m active
- 800G AOC: 10m-100m
- Breakout: OSFP to 2x QSFP112 (800G → 2x400G)

**QSFP112 Cables (C8240):**

- Same as ConnectX-7 QSFP112 cables

**Optical Modules:**

- 800G SR8: OM4 50m, multimode
- 800G DR4: SMF 500m, 4x200G PAM-4

!!! tip "Protocol Support"
    C8180 supports 800G InfiniBand XDR or 400GbE Ethernet (not 800GbE). C8240 provides 2x400GbE for 800Gb/s total Ethernet throughput.

---

## BlueField DPUs

Data Processing Units combining Arm CPUs with ConnectX networking for infrastructure offload.

### BlueField-3

**Architecture:** 8-16 Arm cores + ConnectX-7 networking

| Model | CPU | Memory | Network | Use Case |
|-------|-----|--------|---------|----------|
| B3140H | 8 cores | 16GB | 1x400G QSFP112 | Single high-speed uplink |
| B3220 | 16 cores | 32GB | 2x200G QSFP112 | Dual uplinks, HA |

**Cable Compatibility:** Same as ConnectX-7 QSFP112

### BlueField-4

**Architecture:** 64 Arm cores + ConnectX-9 networking

- **Cores:** 64x Arm Neoverse V2
- **Memory:** 128GB LPDDR5
- **Network:** 800Gb/s (2x400G typical)
- **PCIe:** Gen 6.0 x16
- **Availability:** Expected Q1 2026

---

## Cable Selection Guide

### By Distance

| Distance | Cable Type | Speed Support |
|----------|------------|---------------|
| 0.5m-3m | Passive DAC | All speeds, lowest cost |
| 3m-5m | Active DAC/AEC | All speeds |
| 5m-10m | Active Copper (ACC) | Longer copper reach |
| 10m-100m | Active Optical (AOC) | Lightweight, flexible |
| 100m-500m | SR/DR Optics + Fiber | Rack-to-rack |
| 500m+ | LR/ER Optics + Fiber | Campus, DCI |

### By Speed

| Speed | Connector | Recommended Cables |
|-------|-----------|-------------------|
| 100G | QSFP28 | QSFP28 DAC (1-3m), SR4/LR4 optics |
| 200G | QSFP56 | QSFP56 DAC (1-3m), SR4/DR4 optics |
| 400G | QSFP112 | QSFP112 DAC (1-3m), SR8/DR4 optics |
| 400G | OSFP | OSFP DAC (1-3m), SR8/DR4 optics |
| 800G | OSFP | OSFP DAC (1-2m), SR8/DR4 optics |

---

## Third-Party Optics

NVIDIA recommends LinkX cables but supports IEEE-compliant third-party optics:

### Verified Vendors

- **FS.com:** 100% compatibility tested, 40-70% cost savings
- **NADDOD:** High-speed focus (400G/800G)
- **ProLabs, 10Gtek:** General compatibility

### Compatibility Notes

!!! success "Warranty Safe"
    Using third-party optics does **NOT** void NVIDIA NIC warranty.

**Requirements:**

- IEEE 802.3 compliance mandatory
- Correct form factor (QSFP56, QSFP112, OSFP)
- Matching SerDes speeds (50G, 100G, 200G PAM-4)
- CMIS 4.0+ recommended for 400G+

**Cost Savings:**

- 100G transceivers: 50-67% savings
- 200G transceivers: 60-70% savings
- 400G transceivers: 60-67% savings

---

## Signaling Technologies

### NRZ (Non-Return-to-Zero)

- **Lane Speed:** 10G, 25G
- **Usage:** Legacy 100G (4x25G)
- **Encoding:** Simple 2-level signaling

### PAM-4 (4-Level Modulation)

| Type | Lane Speed | Total (4 lanes) | Total (8 lanes) | NICs Using It |
|------|------------|-----------------|-----------------|---------------|
| 50G PAM-4 | 50Gb/s | 200Gb/s | 400Gb/s | ConnectX-6 |
| 100G PAM-4 | 100Gb/s | 400Gb/s | 800Gb/s | ConnectX-7, 8 |
| 200G PAM-4 | 200Gb/s | 800Gb/s | 1.6Tb/s | ConnectX-8, 9 |

---

## Troubleshooting

### Link Issues

**Check Signal Quality:**

```bash
# NVIDIA mlx tools
mlxlink -d <device> -m
```

**Common Problems:**

- **No Link:** Check cable seating, try known-good cable
- **High Error Rate:** Check BER, may need higher-quality cable
- **Speed Negotiation Failed:** Verify both ends support speed, check auto-neg settings

### Performance Issues

**RDMA Performance:**

```bash
# Test RDMA bandwidth
ib_write_bw -d <device>

# Test latency
ib_write_lat -d <device>
```

**PCIe Validation:**

```bash
# Check PCIe link status
lspci -vvv -s <bus:dev.func> | grep -i lnk
```

---

## Configuration Examples

### Enable RDMA (RoCEv2)

```bash
# Load RDMA modules
modprobe ib_core
modprobe ib_uverbs
modprobe rdma_ucm

# Verify device
ibv_devices
```

### Set Link Speed (200G on ConnectX-6)

```bash
# Configure as single 200G port
mlxconfig -d <device> set LINK_TYPE_P1=2
mlxconfig -d <device> set NUM_OF_VFS=0
```

### Enable SR-IOV

```bash
# Set number of VFs
echo 8 > /sys/class/net/<interface>/device/sriov_numvfs

# Verify
lspci | grep -i mellanox
```

---

## Resources

- **NVIDIA Documentation:** [docs.nvidia.com/networking](https://docs.nvidia.com/networking)
- **LinkX Cables Guide:** NVIDIA technical documentation
- **Driver Downloads:** [nvidia.com/networking/ethernet-adapters](https://www.nvidia.com/en-us/networking/ethernet-adapters/)

---

## Quick Part Number Decoder

NVIDIA part numbers follow pattern: **MCX7xxxx-xxxx**

- **MCX6:** ConnectX-6
- **MCX7:** ConnectX-7
- **C8:** ConnectX-8
- **Suffix:**
  - `-NEAT`: Standard PCIe
  - `-NEAC`: OCP 3.0

**Example:** MCX75310AAS-NEAT = ConnectX-7, Single-port, QSFP112, PCIe standard
