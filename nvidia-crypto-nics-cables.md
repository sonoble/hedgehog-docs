# NVIDIA Crypto-Enabled NICs with Tested Cables

Quick reference list of NVIDIA QSFP network cards with crypto enabled and compatible tested cables.

## Identifying Crypto-Enabled NICs

**Part Number Convention:**
- **"AC"** in part number = **Crypto Enabled** with Secure Boot
- **"AS"** in part number = **Crypto Disabled** with Secure Boot

---

## ConnectX-7 Crypto-Enabled QSFP112 Models

### Dual-Port 200GbE/400GbE

**MCX755106AC-HEAT**
- **Speeds:** 2x200Gb/s or 1x400Gb/s
- **Form Factor:** Dual-port QSFP112
- **PCIe:** Gen 5.0 x16
- **Features:** Crypto Enabled, Secure Boot, RoCEv2
- **Bracket:** Tall with x16 PCIe extension option

### Dual-Port 100GbE

**MCX713106AC-CEAT**
- **Speeds:** 2x100Gb/s
- **Form Factor:** Dual-port QSFP112
- **PCIe:** Gen 5.0 x16
- **Features:** Crypto Enabled, Secure Boot, RoCEv2
- **Bracket:** Ejector latch

---

## ConnectX-6 Crypto-Enabled Models

### Dual-Port 25GbE

**MCX631432AC-ADAB**
- **Speeds:** 2x10/25Gb/s
- **Form Factor:** Dual-port SFP28
- **PCIe:** Gen 4.0 x8
- **Features:** Crypto Enabled, Secure Boot
- **Note:** Lower speed, suitable for legacy deployments

---

## Tested Cables and Compatibility

### NVIDIA Official Cables (MCP Series)

#### MCP7Y40-N002
**800G OSFP to 4x200G QSFP112 Breakout DAC**
- **Length:** 2m (7ft)
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP (finned top) → 4x 200G QSFP112
- **Protocols:** Ethernet
- **Use Case:** 800G switch to four ConnectX-7 200G ports

#### MCP7Y00-N01A
**800G OSFP to 2x400G Breakout DAC**
- **Length:** 1.5m (5ft)
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP (finned top) → 2x 400G QSFP112 or OSFP
- **Note:** Based on search, likely variant of MCP7Y10-N01A
- **Use Case:** Switch to two 400G NICs

#### MCP7Y10-N002
**800G OSFP to 2x400G QSFP112 Breakout DAC**
- **Length:** 2m (7ft)
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP (finned top) → 2x 400G QSFP112
- **Protocols:** Ethernet
- **Use Case:** Spectrum-4 switch to two ConnectX-7 400G ports

### Generic OSFP Cables

#### OSFP-800G-2OPC015
**800G OSFP to 2x OSFP Breakout**
- **Length:** 1.5m
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP → 2x OSFP (flat top)
- **Use Case:** Switch to two OSFP-based ConnectX-7 adapters

#### OSFP-400G-2QPC01
**400G OSFP to 2x QSFP Breakout**
- **Length:** 1m
- **Type:** Passive copper breakout
- **Configuration:** 400G OSFP → 2x QSFP (likely QSFP112 or QSFP56)
- **Use Case:** Single OSFP port to two QSFP ports

#### OSFP-800G-2QPC02
**800G OSFP to 2x QSFP Breakout**
- **Length:** 2m
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP → 2x QSFP112 (400G each)
- **Use Case:** Switch to two QSFP-based 400G NICs

#### OSFP-800G-4QPC02
**800G OSFP to 4x QSFP Breakout**
- **Length:** 2m
- **Type:** Passive copper breakout
- **Configuration:** 800G OSFP → 4x QSFP112 (200G each)
- **Use Case:** Switch to four QSFP-based 200G NICs

---

## Cable Compatibility Matrix

| Cable Part Number | Switch End | NIC End | Speed per NIC Port | NICs Supported |
|-------------------|------------|---------|-------------------|----------------|
| MCP7Y40-N002 | 800G OSFP | 4x QSFP112 | 200G | MCX755106AC-HEAT |
| MCP7Y00-N01A | 800G OSFP | 2x OSFP/QSFP112 | 400G | MCX755106AC-HEAT (400G mode) |
| MCP7Y10-N002 | 800G OSFP | 2x QSFP112 | 400G | MCX755106AC-HEAT (400G mode) |
| OSFP-800G-2OPC015 | 800G OSFP | 2x OSFP | 400G | CX-7 OSFP variants |
| OSFP-400G-2QPC01 | 400G OSFP | 2x QSFP112 | 200G | MCX755106AC-HEAT |
| OSFP-800G-2QPC02 | 800G OSFP | 2x QSFP112 | 400G | MCX755106AC-HEAT (400G mode) |
| OSFP-800G-4QPC02 | 800G OSFP | 4x QSFP112 | 200G | MCX755106AC-HEAT |

---

## Important Notes

### Form Factor Compatibility

!!! warning "OSFP Connector Types"
    - **Switches:** Use OSFP **finned top** (taller heat sink)
    - **NICs:** Use OSFP **flat top** or QSFP112 with **riding heat sink**
    - Twin-port OSFP cables have finned top on switch side, flat top on NIC side

### Cable Selection Guidelines

**For Crypto-Enabled ConnectX-7 (MCX755106AC-HEAT):**

| Deployment | Recommended Cable | Notes |
|------------|-------------------|-------|
| 2x 200G uplinks | MCP7Y40-N002 or OSFP-800G-4QPC02 | Requires 800G switch, 4 NICs per cable |
| 1x 400G uplink | MCP7Y10-N002 or OSFP-800G-2QPC02 | Requires 800G switch, 2 NICs per cable |
| Short reach (1-1.5m) | OSFP-800G-2OPC015 or MCP7Y00-N01A | Best for top-of-rack |
| Standard reach (2m) | MCP7Y10-N002 or OSFP-800G-2QPC02 | Most common deployment |

### Optical Transceivers

#### MMA4Z00-NS-FLT
**800G Twin-Port OSFP SR8 Optical Transceiver**
- **Type:** Multimode optical transceiver
- **Configuration:** Twin-port 2x400Gb/s (800Gb/s total)
- **Technology:** SR8 (2xSR4), 8-channel parallel optics
- **Wavelength:** 850nm VCSEL
- **Modulation:** 100G PAM-4
- **Fiber:** OM3 (30m), OM4 (50m)
- **Connector:** 2x MPO-12/APC
- **Form Factor:** OSFP flat top (for NICs/DPUs)
- **Power:** 15W
- **Use Case:** OSFP-based ConnectX-7 NICs, DGX H100, liquid-cooled systems

#### T1-OSFP112-800G-2DR4-RHS
**800G OSFP DR8 Optical Transceiver (T1Nexus)**
- **Type:** Single-mode optical transceiver
- **Configuration:** Twin-port 2x400Gb/s (800Gb/s total)
- **Technology:** DR8 (2xDR4), 8-channel single-mode
- **Wavelength:** 1310nm
- **Modulation:** 100G PAM-4 per lane
- **Fiber:** Single-mode fiber (SMF)
- **Reach:** 500m
- **Connector:** 2x MPO-12/APC
- **Form Factor:** OSFP flat top RHS (Riding Heat Sink)
- **Use Case:** OSFP-based ConnectX-7/8 NICs, AI/ML infrastructure, hyperscale data centers

#### QSFP112-200G-DR2
**200G QSFP112 Dual-Reach Optical Transceiver**
- **Type:** Single-mode optical transceiver
- **Speed:** 200Gb/s
- **Technology:** DR2 (Dual Reach)
- **Connector:** LC duplex
- **Form Factor:** QSFP112
- **Use Case:** QSFP112-based ConnectX-7 NICs for extended reach

### Protocol Support

All listed cables and transceivers support:
- ✅ Ethernet 400GbE
- ✅ Ethernet 200GbE
- ✅ Ethernet 100GbE

Auto-detection based on switch configuration.

---

## Configuration Example

### Enable Crypto Features

Crypto-enabled NICs support hardware acceleration for:
- **IPsec:** Full IPsec crypto offload
- **TLS:** TLS 1.2/1.3 encryption/decryption
- **Secure Boot:** Firmware validation on boot

**Verify Crypto Support:**

```bash
# Check NIC model
lspci -vv | grep -i mellanox

# Verify crypto capability
mlxconfig -d <device> query | grep -i crypto
# Should show: CRYPTO_OPERATIONAL = True

# Check secure boot
mlxconfig -d <device> query | grep -i secure
```

### Configure IPsec Offload

```bash
# Load IPsec modules
modprobe xfrm4_mode_transport
modprobe esp4
modprobe ah4

# Verify offload capability
ip xfrm state

# Configure IPsec with hardware offload
ip xfrm state add src <src_ip> dst <dst_ip> \
  proto esp spi 0x1000 \
  mode transport \
  enc aes 0x<key> \
  offload dev <interface> dir out
```

---

## Deployment Topology Example

### AI Cluster with Crypto-Enabled NICs

```
┌─────────────────────────────────────┐
│   Spectrum-4 800G Ethernet Switch   │
│   (OSFP finned top ports)           │
└──┬─────┬─────┬─────┬─────┬─────┬───┘
   │     │     │     │     │     │
   │     │     │     │     │     │
   MCP7Y40-N002 (2m, 800G→4x200G)
   │     │     │     │
   ▼     ▼     ▼     ▼
┌──┴─┐ ┌─┴──┐ ┌─┴──┐ ┌─┴──┐
│GPU │ │GPU │ │GPU │ │GPU │
│Srv1│ │Srv2│ │Srv3│ │Srv4│
│    │ │    │ │    │ │    │
│CX-7│ │CX-7│ │CX-7│ │CX-7│
│200G│ │200G│ │200G│ │200G│
│QSFP│ │QSFP│ │QSFP│ │QSFP│
│112 │ │112 │ │112 │ │112 │
└────┘ └────┘ └────┘ └────┘

Each server: MCX755106AC-HEAT
Each connection: 200Gb/s with crypto offload
```

---

## Quick Reference Summary

### Crypto-Enabled NICs (QSFP)

| Part Number | Ports | Speed | Connector | Use Case |
|-------------|-------|-------|-----------|----------|
| MCX755106AC-HEAT | 2x | 200G/400G | QSFP112 | AI/ML clusters |
| MCX713106AC-CEAT | 2x | 100G | QSFP112 | General purpose |

### Tested Cables

| Cable | Length | Config | Primary Use |
|-------|--------|--------|-------------|
| MCP7Y40-N002 | 2m | 800G → 4x200G | 4 servers per switch port |
| MCP7Y10-N002 | 2m | 800G → 2x400G | 2 servers per switch port |
| MCP7Y00-N01A | 1.5m | 800G → 2x400G | Short-reach, 2 servers |
| OSFP-800G-4QPC02 | 2m | 800G → 4x200G | Generic 4-server breakout |
| OSFP-800G-2QPC02 | 2m | 800G → 2x400G | Generic 2-server breakout |

### Tested Optical Transceivers

| Transceiver | Type | Speed | Connector | Reach | Use Case |
|-------------|------|-------|-----------|-------|----------|
| MMA4Z00-NS-FLT | OSFP SR8 | 2x400G | 2x MPO-12 | OM4 50m | OSFP NICs, multimode |
| QSFP112-200G-DR2 | QSFP112 DR2 | 200G | LC duplex | Extended | QSFP112 NICs, single-mode |

---

## Resources

- **NVIDIA Documentation:** [docs.nvidia.com/networking](https://docs.nvidia.com/networking)
- **LinkX Cable Guide:** NVIDIA technical documentation portal
- **Crypto Offload Guide:** IPsec Crypto Offload documentation
