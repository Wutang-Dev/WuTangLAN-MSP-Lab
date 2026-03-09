# Day 05 – Implement Differencing Disks

## Objective

Optimize storage usage in the WuTangLAN MSP lab by implementing Hyper-V differencing disks.

Differencing disks allow multiple virtual machines to share a single base image (template) while storing only the changes made by each VM. This significantly reduces storage usage and allows new machines to be deployed quickly.

---

## Template Location

All VM templates are stored on the secondary drive:

D:\VM-Templates

The Windows Server template created earlier in the project will be used as the parent disk for infrastructure servers.

Parent template:

windows_server_2022_template.vhdx

---

## Differencing Disk Structure

A differencing disk references a parent disk and only stores modifications made by the virtual machine.

Structure used in the lab:

Windows-Server-2022-Template.vhdx
│
├ DC01.vhdx
├ DHCP01.vhdx
└ FS01.vhdx


Each server disk remains very small because the operating system files remain in the parent template.

---

## Implementation

A differencing disk was created using the **Hyper-V New Virtual Hard Disk Wizard**.

Configuration:

Format: VHDX  
Type: Differencing Disk  

Parent disk:

D:\VM-Templates\Windows-Server-2022\VM\Virtual Hard Disks\windows_server_2022_template.vhdx  

Child disk created:

DC01.vhdx  

Location:

C:\Users\Ravi\Labs\Wutang-Dev-MSP-Lab\DC01

When the VM is created, this disk will be attached as the operating system disk.

---

## Storage Benefits

Without differencing disks:

5 Windows servers × ~20GB = ~100GB

With differencing disks:

Template disk ≈ 12GB  
Each server disk ≈ 1–3GB  

Estimated total lab size:

≈ 30GB

This keeps the entire MSP lab well within the 100GB project target.

---

## Important Rule

Once differencing disks are created, the parent template disk must **never be modified or booted**.  

All virtual machines must use their own child disks to prevent corruption of the disk chain.

---

## Outcome

Differencing disks have been successfully implemented for the WuTangLAN MSP lab.  

This allows infrastructure servers to be deployed quickly while keeping storage usage low and maintaining consistent system configurations.
