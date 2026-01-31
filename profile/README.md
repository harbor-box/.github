# Harbor Box

A hardened VPN router built with Rust 🦀

## Key Capabilities

- **Secure-by-design architecture**: a minimal userland composed of memory-safe Rust services, reducing exploitability and unintended behavior
- **Strong fault isolation**: independently deployed services communicate exclusively over authenticated gRPC APIs
- **Tamper resistance and attestation**: TPM 2.0–backed key storage with measured boot, enabling device integrity verification
- **Hardened defaults**: security-first configuration with STIG-compatible system baselines
- **Zero-touch provisioning**: devices can be securely onboarded and configured without local interaction
- **Fleet management**: centralized control and observability for large-scale deployments

## Architecture Overview

Harbor Box is composed of a small set of purpose-built services written in pure Rust. Each service has a narrowly scoped responsibility and communicates through explicit, versioned gRPC interfaces, enabling independent evolution, testing, and security review.

### Core Networking

- **harbor-goose** 🪿 IKEv2/IPsec implementation (RFC 7296, RFC 4301)
- **harbor-bgp** BGP-4 routing service (RFC 4271) with route filtering, AS-path manipulation, and multi-hop peering support

### System Control

- **harbor-network** Linux network interface management via netlink, including IP configuration and VLAN tagging
- **harbor-firewall** zone-based security policies implemented with nftables, supporting IPv4 and IPv6 with stateful connection tracking

### Infrastructure Services

- **harbor-dhcp** DHCPv4 address allocation (RFC 2131)
- **harbor-dns** recursive DNS resolution with configurable forwarding

### Management

- **harbor-manager** device configuration, lifecycle management, and fleet-level control interface

## Licensing

The [`harbor-box-firmware`](https://github.com/harbor-box/harbor-box-firmware) repository and associated test infrastructure[^1] are available under the Business Source License 1.1. This permits development and non-production use, with an automatic conversion to Apache-2.0 after four years.

All core Harbor Box services are proprietary software and available under a commercial license.

For commercial licensing inquiries, please contact: **tyler@cyberbythesea.com**

[^1]: Test and simulation tooling:  
[`harbor-box-qemu`](https://github.com/harbor-box/harbor-box-qemu)  
[`harbor-box-simulator`](https://github.com/harbor-box/harbor-box-simulator)
