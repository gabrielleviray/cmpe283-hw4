# Assignment 4

## Team Members
Gabrielle Viray (012340068)

## Environment
Use kernel environment in Assignment 3

## Steps Followed from Assignment 4 Documentation
1. Boot test VM using assignment 3.
2. Record total exit count for each type of exit handled by KVM
3. Shut down inner VM
4. Remove 'kvm-intel' module
```
rmmod kvm-intel
```
5. Reload kvm-intel module using the parameter 
```
ept = 0 
```
6. Boot same test VM. Record the number of exits and exit types

## Questions
Sample Output with ept:
```
[ 877.863504] CPUID(0x4FFFFFFE): Exit number: (51) Number of exits:(0)
[ 877.863634] CPUID(0x4FFFFFFE): Exit number: (52) Number of exits:(0)
[ 877.863698] CPUID(0x4FFFFFFE): Exit number: (53) Number of exits:(0)
[ 877.863725] CPUID(0x4FFFFFFE): Exit number: (54) Number of exits:(4)
[ 877.863767] CPUID(0x4FFFFFFE): Exit number: (55) Number of exits:(4)
[ 877.863792] CPUID(0x4FFFFFFE): Exit number: (56) Number of exits:(0)
[ 877.863812] CPUID(0x4FFFFFFE): Exit number: (57) Number of exits:(0)
[ 877.863863] CPUID(0x4FFFFFFE): Exit number: (58) Number of exits:(0)
[ 877.863875] CPUID(0x4FFFFFFE): Exit number: (59) Number of exits:(0)
[ 877.863897] CPUID(0x4FFFFFFE): Exit number: (60) Number of exits:(0)
[ 877.863904] CPUID(0x4FFFFFFE): Exit number: (61) Number of exits:(0)
[ 877.863971] CPUID(0x4FFFFFFE): Exit number: (62) Number of exits:(0)
[ 877.864004] CPUID(0x4FFFFFFE): Exit number: (63) Number of exits:(0)
[ 877.864171] CPUID(0x4FFFFFFE): Exit number: (64) Number of exits:(0)
[ 877.864124] Exit type: (65) is undefined in SDM
```
Sample Output without ept after reboot:
```
[ 3892.843722] CPUID(0x4FFFFFFE): Exit number: (1) Number of exits:(374833)
[ 3896.283624] CPUID(0x4FFFFFFE): Exit number: (2) Number of exits:(0)
[ 3898.193473] CPUID(0x4FFFFFFE): Exit number: (3) Number of exits:(0)
```
1. What did you learn from the count of exits? Was the count what you expected? If not, why not?

With ept, the exit count is less in comparison to the exit count without ept. This is expected because an exit occurs only when an EPT violation is raised in nested paging. In shadow paging, more exits occur such as page faults, CR0 execution, etc.

2. What changed between the two runs(ept vs no-ept)?

In non-ept mode, the page table does not belong to the guest VM. In ept mode, two page tables are utilized to get the host physical address and the page table elongs to the guest VM. 
