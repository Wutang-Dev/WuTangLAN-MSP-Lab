# Day 02 – Folder Structure

## Objective
Create a clean folder structure for the WuTangLAN MSP lab to separate infrastructure, templates, and documentation.

## Lab Folder Structure

C:\Users\Ravi\Labs\Wutang-Dev-MSP-Lab

Folders created for each machine:

DC01  
CLIENT-EMIRATES  
CLIENT-HIGHBURY  
FS01  
WEB01  
MON01  

This structure keeps each VM isolated and organised.

## GitHub Documentation Folder

A separate folder was created for GitHub documentation:

github/WuTangLAN-MSP-Lab

This ensures that Git only tracks documentation and not large VM files such as:

.vhdx  
.vmrs  
.vmcx  

## Outcome

The lab environment is now organised with separate folders for infrastructure and documentation, allowing the project to scale cleanly as additional machines are deployed.
