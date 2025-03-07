---
title:      "Hyper-V Replica in Windows Server 2012 R2 and System Center Operations Manager 2012 R2"
author: sethmanheim
ms.author: sethm
ms.date: 12/10/2013
categories: hvr
description: Using System Center Operations Manager 2012 R2 for monitoring Windows Server 2012 R2 hosts.
---
# System Center Operations manager 2012 R2 and Windows Server 2012 R2

Continuing from my previous post [Monitoring Hyper-V Replica using Systems Center Operations Manager](https://blogs.technet.com/b/virtualization/archive/2013/09/13/monitoring-hyper-v-replica-using-system-center-operations-manager.aspx), in this blog post I will walk through some of the things to be taken care of while using System Center Operations Manager 2012 R2 for monitoring Windows Server 2012 R2 hosts. If you haven’t read previous blog, I request you go through it before you start monitoring Windows Server 2012 R2 machines. The best part of this story is all the monitors present in the previous version of SCOM  work with this new version of OS. 

As mentioned in [What is New in Windows Server 2012 R2,](https://blogs.technet.com/b/virtualization/archive/2013/10/22/what-s-new-in-windows-server-2012-r2.aspx) we have added ability to configure the replication frequency of VMs. User now can replicate at 30sec, 5 minute and 15 minutes. Correspondingly alerts we generate for “Hyper-V 2012 Replication Count Percent Monitor” change based on the VM. If you have VMs with varying replication frequency, coming up with a percentage number becomes tricky. For this we suggest, to **set the count percent to a number which can catch missed number of cycles for your least replication frequency VM**. For example, if I have VMs of replication frequency 30ec, 5 minutes and 15 minutes in my environment and if I want to get notified for   even if I miss one replication cycle in an interval of one hour, this means a percentage number of 1/(2*60) for 30sec Replication frequency VMs; a percentage number of 1/12 for 5 Minute replication frequency VMs and a percentage number of 1/4 for 15 minute replication frequency VMs. By setting count percentage value to 1/(2*60), I can catch alerts from all VMs which missed one replication cycle in the interval period of 60 minutes.

Rest of the monitors just work as they work in Windows Server 2012. What is more, Hyper-V Extensions management pack written by Cristian Edwards Sabathe, now supports Windows Server 2012 R2. In addition to the existing dash boards, it now supports Extended Replica VMs. Go try it out!!
