# Day 01 – Network Planning

## Objective
Design the network architecture for the WuTangLAN MSP lab before deploying any virtual machines.

## Key Decisions

### Lab Network
Internal network created in Hyper-V:

MSP_Internal_Switch

Type: Internal

Purpose:
- Isolate the MSP lab environment
- Allow communication between lab machines
- Keep the lab separate from the home network

### Internet Access
Virtual machines will use the Hyper-V Default Switch as a secondary adapter to allow:

- Windows Updates
- Package installation
- Internet connectivity

### Lab Subnet

10.10.10.0/24

This subnet will be used for all internal lab machines.

### Planned IP Addresses

DC01 – 10.10.10.10  
FS01 – 10.10.10.20  
Future servers will follow the same addressing scheme.

## Outcome

The network architecture for the WuTangLAN MSP lab has been planned.  
An internal Hyper-V switch and subnet have been defined to support the deployment of the lab infrastructure.
