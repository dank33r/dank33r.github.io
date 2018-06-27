---
title: IB网卡固件升级
date: 2018-06-22 18:27:31
tags: Infiniband
categories: 硬件
---

### x365服务器IB网卡固件升级

```
> C:\2012r2\tools\mlxburn.exe -qq -force -d mt4099_pci_cr0 -fw
> C:\2012r2\Firmware\2.30.3200\fw-ConnectX3-rel.mlx -conf
> C:\2012r2\Firmware\2.30.3200\00D9551_Ax.ini -exp_rom_dir 
> C:\2012r2\Firmware\2.30.3200\exp_rom -exp_rom AUTO
```