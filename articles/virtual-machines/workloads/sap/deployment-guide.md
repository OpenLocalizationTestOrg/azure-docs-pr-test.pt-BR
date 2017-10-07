---
title: "aaaAzure implantação de máquinas virtuais para SAP NetWeaver | Microsoft Docs"
description: "Saiba como toodeploy SAP software em máquinas virtuais Linux no Azure."
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 42f1d8a3eff51e113729dbfe2848b67deaf06936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a>Implantação de Máquinas Virtuais do Azure para SAP NetWeaver
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../windows/agent-user-guide.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Máquinas virtuais do Azure é a solução de hello para empresas que precisam de recursos de computação e armazenamento, no mínimo de tempo e sem ciclos de compra longos. Você pode usar aplicativos clássico, máquinas virtuais do Azure toodeploy, como aplicativos baseados no SAP NetWeaver no Azure. Estenda a confiabilidade e a disponibilidade de um aplicativo sem recursos locais adicionais. As Máquinas Virtuais do Azure dão suporte à conectividade entre locais, o que permite que você integre as Máquinas Virtuais do Azure aos seus domínios locais, a nuvens privadas e à estrutura do sistema SAP.

Neste artigo, abordaremos a aplicativos do SAP toodeploy Olá etapas em máquinas virtuais (VMs) no Azure, incluindo opções de implantação alternativos e solução de problemas. Este artigo é baseado em informações de saudação do [máquinas virtuais do Azure de planejamento e implementação do SAP NetWeaver][planning-guide]. Ele também complementa a documentação de instalação do SAP e observações sobre o SAP, que são recursos de saudação principal de instalação e implantação de software SAP.

## <a name="prerequisites"></a>Pré-requisitos
A configuração de uma máquina virtual do Azure para implantação de software SAP envolve várias etapas e recursos. Antes de começar, certifique-se de que você atenda aos pré-requisitos de saudação para instalar o software SAP em máquinas virtuais no Azure.

### <a name="local-computer"></a>Computador local
toomanage Windows ou Linux VMs, você pode usar um script do PowerShell e hello portal do Azure. Para ambas as ferramentas, você precisa de um computador local que execute o Windows 7 ou uma versão posterior do Windows. Se você quiser toomanage somente VMs do Linux e você desejar toouse um computador Linux para esta tarefa, você pode usar a CLI do Azure.

### <a name="internet-connection"></a>Conexão com a Internet
toodownload e execução Olá ferramentas e scripts que são necessários para a implantação de software SAP, você deve ser conectado toohello da Internet. Olá VM do Azure que está executando o hello Azure extensão de monitoramento aprimorada para SAP também precisa toohello de acesso à Internet. Se hello Azure VM é parte de uma rede virtual do Azure ou o domínio local, certifique-se de que as configurações de proxy relevantes de saudação forem definidas, conforme descrito em [configurar proxy Olá][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Uma assinatura do Microsoft Azure
Você precisa de uma conta ativa do Azure.

### <a name="topology-and-networking"></a>Topologia e rede
Você precisa de topologia de saudação toodefine e arquitetura de saudação implantação SAP no Azure:

* Toobe de contas de armazenamento do Azure usado
* Rede virtual onde deseja que o sistema SAP toodeploy Olá
* Toowhich de grupo de recursos, você deseja toodeploy Olá SAP sistema
* Região do Azure onde deseja que o sistema SAP toodeploy Olá
* Configuração do SAP (duas ou três camadas)
* Tamanhos de VM e o número de saudação de toobe de discos de dados adicionais montados toohello VMs
* Configuração do SAP CTS (Correction and Transport System)

Criar e configurar contas de armazenamento do Azure (se necessário) ou redes virtuais do Azure antes de começar o processo de implantação de software SAP hello. Para obter informações sobre como toocreate e configurar esses recursos, consulte [máquinas virtuais do Azure de planejamento e implementação do SAP NetWeaver][planning-guide].

### <a name="sap-sizing"></a>Dimensionamento do SAP
Sabe Olá seguintes informações de dimensionamento do SAP:

* Projetada a carga de trabalho do SAP, por exemplo, usando a ferramenta de dimensionar rápida do SAP de saudação e Olá SAP aplicativo desempenho padrão (SAPS) número
* Necessário consumo de memória e recursos de CPU do sistema SAP de saudação
* Operações de entrada/saída (E/S) necessárias por segundo
* Largura de banda necessária de comunicação eventual entre VMs no Azure
* Largura de banda de rede necessária entre os ativos locais e hello sistema SAP implantado do Azure

### <a name="resource-groups"></a>Grupos de recursos
No Gerenciador de recursos do Azure, você pode usar recursos grupos toomanage todos os recursos de aplicativo hello em sua assinatura do Azure. Para saber mais, confira [Visão geral do Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Recursos

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Recursos do SAP
Quando você estiver configurando a implantação de software SAP, você precisa Olá recursos SAP a seguir:

* A Nota SAP [1928533], que tem:
  * Lista de tamanhos de VM do Azure que têm suporte para implantação de saudação do software SAP
  * Informações importantes sobre capacidade para tamanhos de VM do Azure
  * Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte
  * A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure

* A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.
* A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.
* Nota da SAP [1409604] Olá exigiu versão SAP Host Agent para Windows no Azure.
* Nota da SAP [2191498] Olá exigiu versão SAP Host Agent para Linux no Azure.
* A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.
* A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.
* A Nota SAP [2002167] tem informações gerais sobre o Red Hat Enterprise Linux 7.x.
* A Nota SAP [2069760] tem informações gerais sobre o Oracle Linux 7.x.
* Nota da SAP [1999351] tem informações adicionais de solução de problemas para hello Azure extensão de monitoramento aprimorada para SAP.
* A Nota SAP [1597355] tem informações gerais sobre o espaço de troca para Linux.
* A [página de SCN do SAP no Azure](https://wiki.scn.sap.com/wiki/x/Pia7Gg) tem notícias e uma coleção de recursos úteis.
* [WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.
* Cmdlets do PowerShell específicos para SAP que fazem parte do [Azure PowerShell][azure-ps]
* Comandos de CLI do Azure específicos do SAP que fazem parte da [CLI do Azure][azure-cli].

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Recursos do Windows
Estes artigos da Microsoft abordam as implantações do SAP no Azure:

* [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]
* [Implantação de Máquinas Virtuais do Azure para SAP NetWeaver (este artigo)][deployment-guide]
* [Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver][dbms-guide]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Cenários de implantação do software SAP em VMs do Azure
Você tem várias opções para implantar máquinas virtuais e discos associados no Azure. É toounderstand importantes diferenças de saudação entre as opções de implantação, porque pode levar a diferentes etapas tooprepare suas VMs para implantação com base no tipo de implantação Olá escolhido.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Cenário 1: Implantando uma VM do hello Azure Marketplace para SAP
Você pode usar uma imagem fornecida pela Microsoft ou por terceiros em hello Azure Marketplace toodeploy sua VM. Olá Marketplace oferece algumas imagens de SO padrão do Windows Server e várias distribuições do Linux. Você também pode implantar uma imagem que inclua SKUs de DBMS (gerenciamento de banco de dados do sistema), por exemplo, o Microsoft SQL Server. Para obter mais informações sobre como usar imagens com SKUs do DBMS, confira [Implantação de DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide].

Olá fluxograma a seguir mostra sequência do SAP específico Olá das etapas para implantar uma VM do hello Azure Marketplace:

![Fluxograma de implantação de VM para sistemas SAP usando uma imagem de VM do hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Criar uma máquina virtual usando Olá portal do Azure
toocreate de maneira mais fácil de saudação uma nova máquina virtual com uma imagem de saudação do Azure Marketplace é usando Olá portal do Azure.

1.  Vá muito<https://portal.azure.com/#create/hub>.  Ou, no menu do portal do Azure de Olá, selecione **+ novo**.
2.  Selecione **de computação**e, em seguida, selecione o tipo de saudação de deseja toodeploy do sistema operacional. Por exemplo, o Windows Server 2012 R2, o SUSE Linux Enterprise Server 12 (SLES 12), o Red Hat Enterprise Linux 7.2 (RHEL 7.2) ou o Oracle Linux 7.2. exibição de lista padrão de saudação não mostra que todos os sistemas operacionais com suporte. Selecione **ver todos** para obter uma lista completa. Para obter mais informações sobre sistemas operacionais com suporte para implantação de software SAP, confira a Nota SAP [1928533].
3.  Na página seguinte do hello, rever os termos e condições.
4.  Em Olá **selecionar um modelo de implantação** , selecione **Gerenciador de recursos**.
5.  Selecione **Criar**.

Olá guiará você pela configuração de máquina virtual do hello necessários parâmetros toocreate hello, além de tooall necessários recursos, como interfaces de rede e contas de armazenamento. Alguns desses parâmetros são:

1. **Noções básicas**:
 * **Nome**: nome de saudação do recurso de saudação (nome da máquina virtual Olá).
 * **Tipo de disco VM**: Selecionar tipo de disco saudação do disco Olá sistema operacional. Se você quiser toouse armazenamento Premium para os discos de dados, é recomendável usar o armazenamento Premium para o disco do sistema operacional Olá também.
 * **Nome de usuário e senha** ou **chave pública SSH**: insira Olá nome de usuário e senha do usuário de saudação que é criado durante o provisionamento de saudação. Para uma máquina virtual Linux, você pode inserir Olá Secure Shell (SSH) de virtualização que você use toosign toohello máquina.
 * **Assinatura**: selecione Olá assinatura que você deseja toouse tooprovision Olá nova máquina virtual.
 * **Grupo de recursos**: nome de Olá Olá do grupo de recursos para Olá VM. Você pode inserir qualquer nome de saudação de um novo recurso Olá nome de grupo ou um grupo de recursos já existe.
 * **Local**: onde toodeploy Olá nova máquina virtual. Se você deseja que tooconnect Olá máquina virtual tooyour local na rede, certifique-se de que selecionar Olá local de rede virtual de saudação que se conecta a rede de local de tooyour do Azure. Para obter mais informações, confira [Rede do Microsoft Azure][planning-guide-microsoft-azure-networking] em [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide].
2. **Tamanho**:

     Para obter uma lista dos tipos de VM com suporte, confira a Nota SAP [1928533]. Certifique-se de que você selecionar o tipo correto de VM Olá se você quiser toouse armazenamento Premium do Azure. Nem todos os tipos VM dão suporte ao Armazenamento Premium. Para obter mais informações, confira [Armazenamento: Armazenamento do Microsoft Azure e discos de dados][planning-guide-storage-microsoft-azure-storage-and-data-disks] e [Armazenamento Premium do Azure][planning-guide-azure-premium-storage] em [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide].

3. **Configurações**:
  * **Armazenamento**
    * **Tipo de disco**: Selecionar tipo de disco saudação do disco Olá sistema operacional. Se você quiser toouse armazenamento Premium para os discos de dados, é recomendável usar o armazenamento Premium para o disco do sistema operacional Olá também.
    * **Usar discos gerenciados**: se você quiser toouse gerenciados discos, selecione Sim. Para obter mais informações sobre discos gerenciados, consulte o capítulo [discos gerenciados] [ planning-guide-managed-disks] no guia de planejamento de saudação.
    * **Conta de armazenamento**: selecione uma conta de armazenamento existente ou crie uma nova. Nem todos os tipos de armazenamento funcionam para a execução de aplicativos SAP. Para obter mais informações sobre tipos de armazenamento, confira [Armazenamento do Microsoft Azure][dbms-guide-2.3] na [Implantação de DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide].
  * **Rede**
    * **Rede virtual** e **sub-rede**: toointegrate Olá VM com a sua intranet, selecione Olá rede virtual conectado tooyour rede de local.
    * **Endereço IP público**: selecione Olá endereço IP público que você deseja toouse ou insira parâmetros toocreate um novo endereço IP público. Você pode usar um tooaccess de endereço IP público sua máquina virtual Olá da Internet. Certifique-se de que você também pode criar uma máquina de virtual rede segurança grupo toohelp acesso seguro tooyour.
    * **Grupo de segurança de rede**: para obter mais informações, confira [Controlar o fluxo de tráfego de rede com grupos de segurança de rede][virtual-networks-nsg].
  * **Extensões**: você pode instalar extensões de máquina virtual, adicioná-los toohello implantação. Não é necessário extensões tooadd nesta etapa. extensões de saudação necessárias para suporte SAP são instaladas posteriormente. Consulte o capítulo [configurar hello Azure extensão de monitoramento aprimorada para SAP] [ deployment-guide-4.5] neste guia.
  * **Alta disponibilidade**: selecione um conjunto de disponibilidade ou digite Olá parâmetros toocreate uma nova disponibilidade definida. Para obter mais informações, confira [Conjuntos de disponibilidade do Azure][planning-guide-3.2.3].
  * **Monitoramento**
    * **Diagnósticos de inicialização**: você pode selecionar **Desabilitar** para o diagnóstico de inicialização.
    * **Diagnóstico do SO convidado**: você pode selecionar **Desabilitar** para diagnóstico de monitoramento.

4. **Resumo**:

  Examine suas seleções e selecione **OK**.

Sua máquina virtual é implantada no grupo de recursos de saudação selecionado.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Criar uma máquina virtual usando um modelo
Você pode criar uma máquina virtual usando um dos modelos SAP Olá publicados em hello [repositório GitHub de modelos do azure-quickstart][azure-quickstart-templates-github]. Você também pode criar manualmente uma máquina virtual usando Olá [portal do Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], ou [CLI do Azure ][virtual-machines-linux-tutorial].

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual, use este modelo.
* [**Modelo de configuração de duas camadas (apenas uma máquina virtual) – Managed Disks** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual e discos gerenciado, use este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais)** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  toocreate um sistema de três camadas usando várias máquinas virtuais, use este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais) – Managed Disks** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md]

  toocreate um sistema de três camadas usando várias máquinas virtuais e discos gerenciado, use este modelo.

No hello portal do Azure, digite Olá parâmetros de modelo Olá a seguir:

1. **Noções básicas**:
  * **Assinatura**: modelo de Olá Olá assinatura toouse toodeploy.
  * **Grupo de recursos**: modelo de Olá Olá recurso grupo toouse toodeploy. Você pode criar um novo grupo de recursos, ou você pode selecionar um grupo de recursos existente na assinatura de saudação.
  * **Local**: onde toodeploy Olá modelo. Se você selecionou um grupo de recursos existente, o local de saudação desse grupo de recursos é usado.

2. **Configurações**:
  * **ID do sistema SAP**: Olá ID de sistema SAP (SID).
  * **Tipo de SO**: sistema operacional de saudação desejado toodeploy, por exemplo, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (12 SLES), Red Hat Enterprise Linux 7.2 (RHEL 7.2) ou Oracle Linux 7.2.

    modo de exibição de lista de saudação não mostra que todos os sistemas operacionais com suporte. Para obter mais informações sobre sistemas operacionais com suporte para implantação de software SAP, confira a Nota SAP [1928533].
  * **Tamanho do sistema SAP**: Olá tamanho de saudação sistema SAP.

    Olá número de SAPS Olá novo sistema fornece. Se não tiver certeza do sistema de saudação SAPS quantos requer, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.
  * **Disponibilidade do sistema** (apenas modelo de três camadas): Olá a disponibilidade do sistema.

    Selecione **HA** para obter uma configuração adequada a uma instalação de alta disponibilidade. Dois servidores de banco de dados e dois servidores para ASCS (ABAP SAP Central Services) são criados.
  * **Tipo de armazenamento** (apenas modelo de duas camadas): Olá tipo de armazenamento toouse.

    Em sistemas maiores, é altamente recomendável usar o Armazenamento do Azure Premium. Para obter mais informações sobre tipos de armazenamento, confira estes recursos:
      * [Uso do Armazenamento SSD Premium do Azure para instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure][dbms-guide-2.3] na [implantação DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide]
      * [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de Máquina Virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft armazenamento do Azure][storage-introduction]
  * **Nome de Usuário do Administrador** e **Senha do Administrador**: nome de usuário e senha.
    Um novo usuário é criado para a assinatura na máquina virtual de toohello.
  * **Sub-rede nova ou existente**: determina se uma nova rede virtual e uma sub-rede são criadas ou uma sub-rede existente é usada. Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione **existente**.
  * **ID de sub-rede**: Olá ID das máquinas virtuais do hello sub-rede Olá se conectará. Selecione a sub-rede de saudação de sua rede virtual privada (VPN) ou rota expressa do Azure rede virtual toouse tooconnect Olá tooyour local na rede da máquina virtual. ID de saudação geralmente tem esta aparência: /subscriptions/&lt;id da assinatura > /resourceGroups/&lt;nome do grupo de recursos > /providers/Microsoft.Network/virtualNetworks/&lt;nome de rede virtual > /subnets/&lt;nome do subrede >

3. **Termos e condições**:  
    Leia e aceite os termos legais hello.

4.  Selecione **Comprar**.

Hello Azure VM Agent é implantado por padrão quando você usar uma imagem de saudação do Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Definir configurações de proxy
Dependendo de como sua rede local é configurado, talvez seja necessário tooset proxy Olá na sua VM. Se sua VM é a rede de local de tooyour conectados por meio de VPN ou rota expressa, Olá VM pode não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou coletar dados de monitoramento. Para obter mais informações, consulte [configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Ingressar em um domínio (somente Windows)
Se sua implantação do Azure é a instância DNS ou Active Directory de local de tooan conectado via uma conexão de VPN site a site do Azure, ou rota expressa (Isso é chamado de *entre locais* na [planejamento de máquinas virtuais do Azure e a implementação de SAP NetWeaver][planning-guide]), espera-se que Olá VM estiver ingressando em um domínio local. Para obter mais informações sobre as considerações para essa tarefa, consulte [ingressar em um domínio de local de tooan VM (somente Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configurar monitoramento
toobe-se de que o SAP dá suporte ao seu ambiente, configure Olá extensão de monitoramento do Azure para SAP, conforme descrito em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5]. Verificar pré-requisitos Olá para monitoramento do SAP e as versões mínimas necessárias de Kernel do SAP e SAP Host Agent, em recursos Olá listados em [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitoramento
Verifique se o monitoramento está funcionando, conforme descrito em [Verificações e solução de problemas para configurar o monitoramento de ponta a ponta][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Etapas de pós-implantação
Depois de criar hello VM e Olá VM é implantado, é necessário tooinstall Olá necessários componentes de software em Olá VM. Devido a sequência de instalação de software/implantação Olá nesse tipo de implantação de VM, Olá software toobe instalado já deve estar disponível no Azure, na outra VM, ou como um disco que pode ser anexado. Ou então, considere usar um cenário entre locais, na qual conectividade toohello local ativos (compartilhamentos de instalação) é fornecido.

Depois de implantar a VM no Azure, siga Olá mesmas diretrizes e ferramentas tooinstall Olá software SAP em sua VM como você faria em um ambiente local. software SAP de tooinstall em uma VM do Azure, tanto o SAP e a Microsoft recomendam que você deseja carrega e armazena a mídia de instalação do SAP Olá em VHDs do Azure ou discos gerenciados, ou que você crie uma VM do Azure que funciona como um servidor de arquivos que tem todos os Olá necessário mídia de instalação do SAP.

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Cenário 2: Implantando uma VM com uma imagem personalizada para SAP
Como diferentes versões de um sistema operacional ou DBMS têm requisitos diferentes de patch, imagens Olá que encontrar no hello Azure Marketplace podem não atender às suas necessidades. Em vez disso, você poderá toocreate uma VM usando sua própria imagem de VM do SO/DBMS, que você pode implantar novamente mais tarde.
Você pode usar etapas diferentes toocreate uma imagem privada para Linux que toocreate para Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare uma imagem do Windows que você pode usar toodeploy várias máquinas virtuais, configurações do Windows hello (como o SID do Windows e o nome de host) devem ser abstraídas ou generalizado em Olá VM no local. Você pode usar [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo isso.
>
> ![Linux][Logo_Linux] Linux
>
> tooprepare uma imagem do Linux que você pode usar toodeploy várias máquinas virtuais, algumas configurações do Linux devem ser Olá abstraída ou generalizado na VM local. Você pode usar `waagent -deprovision` toodo isso. Para obter mais informações, consulte [capturar uma máquina virtual do Linux em execução no Azure] [ virtual-machines-linux-capture-image] e hello [guia do usuário do agente Linux do Azure][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Você pode preparar e criar uma imagem personalizada e, em seguida, usá-lo toocreate várias novas VMs. Isso é descrito em [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]. Configurar o banco de dados de conteúdo usando o SAP Software Provisioning Manager tooinstall um novo sistema SAP (restaura um backup de banco de dados de um disco de máquina virtual de toohello anexado) ou diretamente restaurando um backup de banco de dados do armazenamento do Azure, se o DBMS oferece suporte a ele. Para obter mais informações, confira [Implantação de DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide]. Se você já tiver instalado um sistema SAP em sua VM local (especialmente para sistemas de duas camadas), você pode adaptar configurações do sistema SAP Olá após a implantação de saudação do hello VM do Azure usando o procedimento de renomeação de saudação suportado pelo SAP Software Provisioning Manager (nota da SAP [1619720]). Caso contrário, você pode instalar o software SAP de saudação depois de implantar Olá VM do Azure.

Olá, fluxograma a seguir mostra Olá sequência de SAP específico de etapas para implantar uma VM de uma imagem personalizada:

![Fluxograma de implantação de VM para sistemas SAP usando uma imagem de VM do Marketplace privado][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Criar uma máquina virtual usando Olá portal do Azure
toocreate de maneira mais fácil de saudação uma nova máquina virtual de uma imagem de disco gerenciado é usando Olá portal do Azure. Para obter mais informações sobre como toocreate uma imagem de disco gerenciar ler [capturar uma imagem gerenciada de uma VM generalizada no Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)

1.  Vá muito<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>. Ou, no menu do portal do Azure de Olá, selecione **imagens**.
2.  Imagem de disco gerenciado Olá Select que deseja toodeploy e clique em **criar VM**

Olá guiará você pela configuração de máquina virtual do hello necessários parâmetros toocreate hello, além de tooall necessários recursos, como interfaces de rede e contas de armazenamento. Alguns desses parâmetros são:

1. **Noções básicas**:
 * **Nome**: nome de saudação do recurso de saudação (nome da máquina virtual Olá).
 * **Tipo de disco VM**: Selecionar tipo de disco saudação do disco Olá sistema operacional. Se você quiser toouse armazenamento Premium para os discos de dados, é recomendável usar o armazenamento Premium para o disco do sistema operacional Olá também.
 * **Nome de usuário e senha** ou **chave pública SSH**: insira Olá nome de usuário e senha do usuário de saudação que é criado durante o provisionamento de saudação. Para uma máquina virtual Linux, você pode inserir Olá Secure Shell (SSH) de virtualização que você use toosign toohello máquina.
 * **Assinatura**: selecione Olá assinatura que você deseja toouse tooprovision Olá nova máquina virtual.
 * **Grupo de recursos**: nome de Olá Olá do grupo de recursos para Olá VM. Você pode inserir qualquer nome de saudação de um novo recurso Olá nome de grupo ou um grupo de recursos já existe.
 * **Local**: onde toodeploy Olá nova máquina virtual. Se você deseja que tooconnect Olá máquina virtual tooyour local na rede, certifique-se de que selecionar Olá local de rede virtual de saudação que se conecta a rede de local de tooyour do Azure. Para obter mais informações, confira [Rede do Microsoft Azure][planning-guide-microsoft-azure-networking] em [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide].
2. **Tamanho**:

     Para obter uma lista dos tipos de VM com suporte, confira a Nota SAP [1928533]. Certifique-se de que você selecionar o tipo correto de VM Olá se você quiser toouse armazenamento Premium do Azure. Nem todos os tipos VM dão suporte ao Armazenamento Premium. Para obter mais informações, confira [Armazenamento: Armazenamento do Microsoft Azure e discos de dados][planning-guide-storage-microsoft-azure-storage-and-data-disks] e [Armazenamento Premium do Azure][planning-guide-azure-premium-storage] em [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide].

3. **Configurações**:
  * **Armazenamento**
    * **Tipo de disco**: Selecionar tipo de disco saudação do disco Olá sistema operacional. Se você quiser toouse armazenamento Premium para os discos de dados, é recomendável usar o armazenamento Premium para o disco do sistema operacional Olá também.
    * **Usar discos gerenciados**: se você quiser toouse gerenciados discos, selecione Sim. Para obter mais informações sobre discos gerenciados, consulte o capítulo [discos gerenciados] [ planning-guide-managed-disks] no guia de planejamento de saudação.
  * **Rede**
    * **Rede virtual** e **sub-rede**: toointegrate Olá VM com a sua intranet, selecione Olá rede virtual conectado tooyour rede de local.
    * **Endereço IP público**: selecione Olá endereço IP público que você deseja toouse ou insira parâmetros toocreate um novo endereço IP público. Você pode usar um tooaccess de endereço IP público sua máquina virtual Olá da Internet. Certifique-se de que você também pode criar uma máquina de virtual rede segurança grupo toohelp acesso seguro tooyour.
    * **Grupo de segurança de rede**: para obter mais informações, confira [Controlar o fluxo de tráfego de rede com grupos de segurança de rede][virtual-networks-nsg].
  * **Extensões**: você pode instalar extensões de máquina virtual, adicioná-los toohello implantação. Não é necessário tooadd extensão nesta etapa. extensões de saudação necessárias para suporte SAP são instaladas posteriormente. Consulte o capítulo [configurar hello Azure extensão de monitoramento aprimorada para SAP] [ deployment-guide-4.5] neste guia.
  * **Alta disponibilidade**: selecione um conjunto de disponibilidade ou digite Olá parâmetros toocreate uma nova disponibilidade definida. Para obter mais informações, confira [Conjuntos de disponibilidade do Azure][planning-guide-3.2.3].
  * **Monitoramento**
    * **Diagnósticos de inicialização**: você pode selecionar **Desabilitar** para o diagnóstico de inicialização.
    * **Diagnóstico do SO convidado**: você pode selecionar **Desabilitar** para diagnóstico de monitoramento.

4. **Resumo**:

  Examine suas seleções e selecione **OK**.

Sua máquina virtual é implantada no grupo de recursos de saudação selecionado.
#### <a name="create-a-virtual-machine-by-using-a-template"></a>Criar uma máquina virtual usando um modelo
toocreate uma implantação usando uma imagem de SO particular de saudação portal do Azure, use um dos Olá modelos SAP a seguir. Esses modelos são publicados no hello [repositório GitHub de modelos do azure-quickstart][azure-quickstart-templates-github]. Você também pode criar manualmente uma máquina virtual usando o [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual, use este modelo.
* [**Modelo de configuração de duas camadas (apenas uma máquina virtual) – Imagem de Disco Gerenciado** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual e uma imagem de disco gerenciado, use este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais)** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  toocreate um sistema de três camadas usando várias máquinas virtuais ou sua própria imagem do sistema operacional, use este modelo.
* [**Modelo de configuração de três camadas (várias máquinas virtuais) – Imagem de Disco Gerenciado** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md]

  toocreate um sistema de três camadas usando várias máquinas virtuais ou sua própria imagem do sistema operacional e uma imagem de disco gerenciado, use este modelo.

No hello portal do Azure, digite Olá parâmetros de modelo Olá a seguir:

1. **Noções básicas**:
  * **Assinatura**: modelo de Olá Olá assinatura toouse toodeploy.
  * **Grupo de recursos**: modelo de Olá Olá recurso grupo toouse toodeploy. Você pode criar um novo grupo de recursos ou selecionar um grupo de recursos existente na assinatura de saudação.
  * **Local**: onde toodeploy Olá modelo. Se você selecionou um grupo de recursos existente, o local de saudação desse grupo de recursos é usado.
2. **Configurações**:
  * **ID do sistema SAP**: Olá ID do sistema SAP.
  * **Tipo de SO**: Olá tipo de sistema operacional que você deseja toodeploy (Windows ou Linux).
  * **Tamanho do sistema SAP**: Olá tamanho de saudação sistema SAP.

    Olá número de SAPS Olá novo sistema fornece. Se não tiver certeza do sistema de saudação SAPS quantos requer, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.
  * **Disponibilidade do sistema** (apenas modelo de três camadas): Olá a disponibilidade do sistema.

    Selecione **HA** para obter uma configuração adequada a uma instalação de alta disponibilidade. Dois servidores de banco de dados e dois para ASCS são criados.
  * **Tipo de armazenamento** (apenas modelo de duas camadas): Olá tipo de armazenamento toouse.

    Em sistemas maiores, é altamente recomendável usar o Armazenamento do Azure Premium. Para obter mais informações sobre tipos de armazenamento, consulte Olá recursos a seguir:
      * [Uso do Armazenamento SSD Premium do Azure para instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure][dbms-guide-2.3] na [implantação DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide]
      * [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de Máquina Virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft armazenamento do Azure][storage-introduction]
  * **Imagem de usuário URI do VHD** (apenas modelo de imagem de disco não gerenciado): Olá URI da imagem do sistema operacional privada Olá VHD, por exemplo, https://&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd.
  * **Conta de armazenamento de imagem de usuário** (apenas modelo de imagem de disco não gerenciado): nome Olá Olá da conta de armazenamento onde Olá privada imagem do SO é armazenada, por exemplo, &lt;accountname > em https://&lt;accountname >. blob.Core.Windows.NET/VHDs/userimage.vhd.
  * **userImageId** (apenas modelo de imagem de disco gerenciado): Id do hello imagem de disco gerenciado ser toouse
  * **Nome de usuário Admin** e **senha do administrador**: Olá nome de usuário e senha.

    Um novo usuário é criado para a assinatura na máquina virtual de toohello.
  * **Sub-rede nova ou existente**: determina se uma nova rede virtual e uma sub-rede são criadas ou uma sub-rede existente é usada. Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione **existente**.
  * **ID de sub-rede**: Olá ID das máquinas virtuais do hello sub-rede toowhich Olá se conectará. Selecione a sub-rede de saudação de sua VPN ou rota expressa rede virtual toouse tooconnect Olá máquina virtual tooyour na rede local. ID de saudação geralmente tem esta aparência:

    /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name>

3. **Termos e condições**:  
    Leia e aceite os termos legais hello.

4.  Selecione **Comprar**.

#### <a name="install-hello-vm-agent-linux-only"></a>Instalar Olá agente de VM (Linux)
modelos de saudação do toouse descritos na saudação anterior seção, Olá que agente Linux já deve estar instalado na imagem do usuário hello ou implantação Olá falhará. Baixe e instale o hello agente de VM na imagem de usuário Olá conforme descrito em [baixar, instalar e habilitar hello Azure VM Agent][deployment-guide-4.4]. Se você não usar modelos hello, você também pode instalar Olá agente de VM mais tarde.

#### <a name="join-a-domain-windows-only"></a>Ingressar em um domínio (somente Windows)
Se sua implantação do Azure é a instância DNS ou Active Directory de local de tooan conectado via uma conexão de VPN site a site do Azure ou rota expressa do Azure (Isso é chamado de *entre locais* na [máquinas virtuais do Azure planejamento e implementação do SAP NetWeaver][planning-guide]), espera-se que Olá VM estiver ingressando em um domínio local. Para obter mais informações sobre as considerações para esta etapa, consulte [ingressar em um domínio de local de tooan VM (somente Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Definir configurações de proxy
Dependendo de como sua rede local é configurado, talvez seja necessário tooset proxy Olá na sua VM. Se sua VM é a rede de local de tooyour conectados por meio de VPN ou rota expressa, Olá VM pode não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou coletar dados de monitoramento. Para obter mais informações, consulte [configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurar monitoramento
toobe-se de que o SAP dá suporte ao seu ambiente, configure Olá extensão de monitoramento do Azure para SAP, conforme descrito em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5]. Verificar pré-requisitos Olá para monitoramento do SAP e as versões mínimas necessárias de Kernel do SAP e SAP Host Agent, em recursos Olá listados em [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitoramento
Verifique se o monitoramento está funcionando, conforme descrito em [Verificações e solução de problemas para configurar o monitoramento de ponta a ponta][deployment-guide-troubleshooting-chapter].


### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Cenário 3: mover uma VM local usando um VHD do Azure não generalizado com o SAP
Nesse cenário, você planejar toomove um sistema SAP específico de um tooAzure do ambiente local. Você pode fazem isso Carregando Olá VHD que tenha Olá SO, binários SAP Olá, e, eventualmente, Olá binários DBMS, além de saudação VHDs com dados hello e arquivos de log de saudação DBMS, tooAzure. Ao contrário do cenário de saudação descrito em [cenário 2: Implantando uma VM com uma imagem personalizada para SAP][deployment-guide-3.3], nesse caso, manter Olá hostname, o SID do SAP, e contas de usuário do SAP em Olá VM do Azure, porque eles foram definida no ambiente de local de saudação. Não é necessário toogeneralize Olá sistema operacional. Esta situação se aplica a maioria das vezes, cenários de toocross locais em que parte do hello estrutura SAP é executada no local e parte dele é executado no Azure.

Nesse cenário, hello agente VM é **não** instalados automaticamente durante a implantação. Como Olá agente de VM e hello Azure extensão de monitoramento aprimorada para SAP são necessário toorun SAP NetWeaver no Azure, você precisa toodownload, instalar e habilitar os dois componentes manualmente depois de criar a máquina virtual de saudação.

Para obter mais informações sobre hello Azure VM Agent, consulte Olá recursos a seguir.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Visão geral do Agente de Máquina Virtual do Azure][virtual-machines-windows-agent-user-guide]
>
> ![Linux][Logo_Linux] Linux
>
> [Guia do usuário do agente Linux para o Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Olá fluxograma a seguir mostra a sequência de saudação de etapas para mover uma VM local usando um VHD do Azure não generalizado:

![Fluxograma de implantação de VM para sistemas SAP usando um disco de VM][deployment-guide-figure-400]

Se disco Olá já está carregado e definido no Azure (consulte [máquinas virtuais do Azure de planejamento e implementação do SAP NetWeaver][planning-guide]), fazer Olá tarefas descritas nas Olá lado seções.

#### <a name="create-a-virtual-machine"></a>Criar uma máquina virtual
toocreate uma implantação usando um disco de SO particular por meio de saudação portal do Azure, use o modelo SAP de Olá publicado em Olá [repositório GitHub de modelos do azure-quickstart][azure-quickstart-templates-github]. Você também pode criar manualmente uma máquina virtual usando o PowerShell.

* [**Modelo de configuração de duas camadas (apenas uma máquina virtual)** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual, use este modelo.
* [**Modelo de configuração de duas camadas (apenas uma máquina virtual) – Disco Gerenciado** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md]

  toocreate um sistema de duas camadas, usando apenas uma máquina virtual e um disco gerenciado, use este modelo.

No hello portal do Azure, digite Olá parâmetros de modelo Olá a seguir:

1. **Noções básicas**:
  * **Assinatura**: modelo de Olá Olá assinatura toouse toodeploy.
  * **Grupo de recursos**: modelo de Olá Olá recurso grupo toouse toodeploy. Você pode criar um novo grupo de recursos ou selecionar um grupo de recursos existente na assinatura de saudação.
  * **Local**: onde toodeploy Olá modelo. Se você selecionou um grupo de recursos existente, o local de saudação desse grupo de recursos é usado.
2. **Configurações**:
  * **ID do sistema SAP**: Olá ID do sistema SAP.
  * **Tipo de SO**: Olá tipo de sistema operacional que você deseja toodeploy (Windows ou Linux).
  * **Tamanho do sistema SAP**: Olá tamanho de saudação sistema SAP.

    Olá número de SAPS Olá novo sistema fornece. Se não tiver certeza do sistema de saudação SAPS quantos requer, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.
  * **Tipo de armazenamento** (apenas modelo de duas camadas): Olá tipo de armazenamento toouse.

    Em sistemas maiores, é altamente recomendável usar o Armazenamento do Azure Premium. Para obter mais informações sobre tipos de armazenamento, consulte Olá recursos a seguir:
      * [Uso do Armazenamento SSD Premium do Azure para instância do SAP DBMS][2367194]
      * [Armazenamento do Microsoft Azure][dbms-guide-2.3] na [implantação DBMS de Máquina Virtual do Azure para SAP NetWeaver][dbms-guide]
      * [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de Máquina Virtual do Azure][storage-premium-storage-preview-portal]
      * [Introdução tooMicrosoft armazenamento do Azure][storage-introduction]
  * **URI do VHD de disco do sistema operacional** (apenas modelo de disco não gerenciado): Olá URI do disco do sistema operacional privado hello, por exemplo, https://&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Id do disco gerenciados em disco do SO** (apenas modelo de disco gerenciado): Olá Id da saudação disco do sistema operacional de disco gerenciado, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN
  * **Sub-rede nova ou existente**: determina se uma nova rede virtual e uma sub-rede são criadas ou uma sub-rede existente é usada. Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione **existente**.
  * **ID de sub-rede**: Olá ID das máquinas virtuais do hello sub-rede toowhich Olá se conectará. Selecione a sub-rede de saudação de sua VPN ou rota expressa do Azure rede virtual toouse tooconnect Olá máquina virtual tooyour na rede local. ID de saudação geralmente tem esta aparência:

    /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name>

3. **Termos e condições**:  
    Leia e aceite os termos legais hello.

4.  Selecione **Comprar**.

#### <a name="install-hello-vm-agent"></a>Instalar Olá agente de VM
Olá de Olá toouse modelos descritos na seção anterior, hello VM Agent deve ser instalado no disco Olá SO ou Olá implantação falhará. Baixar e instalar Olá agente de VM em Olá VM, conforme descrito em [baixar, instalar e habilitar hello Azure VM Agent][deployment-guide-4.4].

Se você não usar modelos de saudação descritos na saudação anterior seção, você também pode instalar Olá agente de VM posteriormente.

#### <a name="join-a-domain-windows-only"></a>Ingressar em um domínio (somente Windows)
Se sua implantação do Azure é a instância DNS ou Active Directory de local de tooan conectado via uma conexão de VPN site a site do Azure, ou rota expressa (Isso é chamado de *entre locais* na [planejamento de máquinas virtuais do Azure e a implementação de SAP NetWeaver][planning-guide]), espera-se que Olá VM estiver ingressando em um domínio local. Para obter mais informações sobre as considerações para essa tarefa, consulte [ingressar em um domínio de local de tooan VM (somente Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Definir configurações de proxy
Dependendo de como sua rede local é configurado, talvez seja necessário tooset proxy Olá na sua VM. Se sua VM é a rede de local de tooyour conectados por meio de VPN ou rota expressa, Olá VM pode não ser capaz de tooaccess Olá Internet e não ser capaz de toodownload extensões Olá necessário ou coletar dados de monitoramento. Para obter mais informações, consulte [configurar proxy Olá][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Configurar monitoramento
toobe-se de que o SAP dá suporte ao seu ambiente, configure Olá extensão de monitoramento do Azure para SAP, conforme descrito em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5]. Verificar pré-requisitos Olá para monitoramento do SAP e as versões mínimas necessárias de Kernel do SAP e SAP Host Agent, em recursos Olá listados em [recursos SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Verificação de monitoramento
Verifique se o monitoramento está funcionando, conforme descrito em [Verificações e solução de problemas para configurar o monitoramento de ponta a ponta][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Atualizar Olá configuração de monitoramento para SAP
Atualize a configuração de monitoramento Olá SAP em qualquer um dos seguintes cenários de saudação:
* equipe de Microsoft/SAP conjunta Olá estende os recursos de monitoramento de saudação e solicita contadores mais ou menos.
* A Microsoft introduz uma nova versão do hello infraestrutura subjacente do Azure que fornece dados de monitoramento de saudação e hello extensão de monitoramento aprimorada do Azure para SAP necessidades toobe adaptado toothose alterações.
* Montar os discos de dados adicionais tooyour VM do Azure ou remover um disco de dados. Nesse cenário, atualize a coleção de saudação de dados relacionados ao armazenamento. Alterar sua configuração, adicionando ou excluindo pontos de extremidade ou atribuindo IP endereços tooa VM não afeta configuração de monitoramento de saudação.
* Você alterar Olá tamanho da VM do Azure, por exemplo, do tamanho A5 tooany outro tamanho VM.
* Adicionar novo tooyour de interfaces de rede VM do Azure.

tooupdate monitoramento de configurações de atualização Olá monitoramento da infraestrutura por Olá a seguir as etapas em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment"></a>Tarefas detalhadas para a implantação de software SAP
Esta seção tem etapas detalhadas para realizar tarefas específicas no processo de implantação e configuração de saudação.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Implantar cmdlets do Azure PowerShell
1.  Vá muito[Downloads do Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Em **Ferramentas de linha de comando**, em **PowerShell**, selecione **Instalar Windows**.
3.  Na caixa de diálogo Gerenciador de Download da Microsoft hello, para o arquivo hello baixado (por exemplo, WindowsAzurePowershellGet.3f.3f.3fnew.exe), selecione **executar**.
4.  toorun Microsoft Web Platform Installer (Microsoft Web PI), selecione **Sim**.
5.  É exibida uma página como esta:

  ![Página de instalação para cmdlets do Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecione **instalar**e, em seguida, aceite Olá Microsoft Software License Terms.
7.  O PowerShell é instalado. Selecione **concluir** tooclose Assistente de instalação de saudação.

Verifique com frequência para atualizações toohello cmdlets do PowerShell, que geralmente são atualizados mensalmente. Olá toocheck de maneira mais fácil para atualizações é Olá toodo etapas de instalação, página de instalação toohello mostrado na etapa 5 anteriores. Olá data e a versão de número da versão dos cmdlets de saudação é incluído na página Olá mostrada na etapa 5. Salvo indicação em contrário na nota da SAP [1928533] ou nota da SAP [2015553], é recomendável que você trabalhe com a versão mais recente Olá de cmdlets do PowerShell do Azure.

toocheck versão Olá Olá cmdlets do PowerShell do Azure que são instalados em seu computador, execute este comando do PowerShell:
```powershell
(Get-Module AzureRm.Compute).Version
```
resultado de saudação tem esta aparência:

![Resultado da verificação de versão de cmdlet do Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

Se Olá cmdlet do Azure versão instalada no computador for Olá atual, a primeira página saudação do Assistente de instalação Olá indica adicionando **(instalado)** toohello título do produto (consulte Olá captura de tela a seguir). Seus cmdlets do PowerShell Azure estão atualizados. Assistente de instalação Olá tooclose, selecione **saída**.

![Página de instalação para cmdlets do PowerShell do Azure que indica a versão mais recente Olá de cmdlets do PowerShell do Azure estão instalados][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Implantar a CLI do Azure
1.  Vá muito[Downloads do Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  Em **ferramentas de linha de comando**, em **interface de linha de comando do Azure**, selecione Olá **instalar** link para seu sistema operacional.
3.  Na caixa de diálogo Gerenciador de Download da Microsoft hello, para o arquivo hello baixado (por exemplo, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), selecione **executar**.
4.  toorun Microsoft Web Platform Installer (Microsoft Web PI), selecione **Sim**.
5.  É exibida uma página como esta:

  ![Página de instalação para cmdlets do Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Selecione **instalar**e, em seguida, aceite Olá Microsoft Software License Terms.
7.  A CLI do Azure está instalada. Selecione **concluir** tooclose Assistente de instalação de saudação.

Verifique com frequência para atualizações tooAzure CLI, que geralmente é atualizada mensalmente. Olá toocheck de maneira mais fácil para atualizações é Olá toodo etapas de instalação, página de instalação toohello mostrado na etapa 5 anteriores.

versão de hello toocheck da CLI do Azure que está instalado no seu computador, execute este comando:
```
azure --version
```

resultado de saudação tem esta aparência:

![Resultado da verificação de versão da CLI do Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Ingressar em um domínio de local de tooan VM (somente Windows)
Se você implantar VMs SAP em um cenário entre locais, onde o DNS e Active Directory no local são estendidos no Azure, é esperado que Olá VMs são ingressar em um domínio local. Olá etapas detalhadas que você tomar toojoin um domínio de local de tooan VM e hello necessário software adicional toobe um membro de um domínio local, varia por cliente. Normalmente, toojoin tooan uma VM domínio local, é necessário software adicional tooinstall, como software antimalware e o software de backup ou de monitoramento.

Nesse cenário, você também precisa toomake-se de que, se as configurações de proxy da Internet são forçadas quando uma VM ingressa em um domínio em seu ambiente, Windows hello conta Sistema Local (S-1-5-18) no hello convidado VM tem Olá mesmas configurações de proxy. opção mais fácil de saudação é proxy de saudação tooforce usando um política de grupo, que se aplica a toosystems no domínio de saudação do domínio.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Baixar, instalar e habilitar hello Azure VM Agent
Para máquinas virtuais implantados por meio de uma imagem do sistema operacional que não seja generalizada (por exemplo, uma imagem que não se originam na ferramenta de preparação do sistema do Windows ou sysprep, Olá), você precisa toomanually download, instalar e habilitar hello Azure VM Agent.

Se você implantar uma VM do hello Azure Marketplace, esta etapa não será necessária. Imagens de saudação do Azure Marketplace já hello Azure VM Agent.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Baixe hello Azure VM Agent:
  1.  Baixar Olá [pacote de instalador do agente de VM do Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Armazenar um pacote MSI de agente de VM Olá localmente em um servidor ou computador pessoal.
2.  Instale hello Azure VM Agent:
  1.  Conecte-se toohello implantado a VM do Azure usando o protocolo de área de trabalho remota (RDP).
  2.  Abra uma janela de Windows Explorer em Olá VM e o diretório de destino select Olá para arquivo MSI Olá Olá agente de VM.
  3.  Arraste hello Azure VM Agent instalador MSI de seu diretório de destino do computador local/servidor toohello de saudação agente de VM na VM de saudação.
  4.  Clique duas vezes no arquivo MSI de saudação em Olá VM.
3.  Para VMs que são unidas tooon local domínios, certifique-se eventuais configurações de proxy de Internet também aplicam toohello conta de sistema Local do Windows (S-1-5-18) no hello VM, conforme descrito em [configurar proxy Olá] [ deployment-guide-configure-proxy]. Olá VM Agent é executado nesse contexto e precisa toobe capaz de tooconnect tooAzure.

Nenhuma interação do usuário é necessária tooupdate hello Azure VM Agent. Olá agente VM é atualizada automaticamente e não requer uma reinicialização VM.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Use Olá seguindo comandos tooinstall Olá agente de VM para Linux:

* **SLES (SUSE Linux Enterprise Server)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL) ou Oracle Linux**

  ```
  sudo yum install WALinuxAgent
  ```

Se o agente de saudação já está instalado, Olá tooupdate agente Linux do Azure, Olá etapas descritas em [Olá atualização agente Linux do Azure em uma versão mais recente do VM toohello do GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configurar o proxy de saudação
etapas de saudação que levar o proxy de saudação tooconfigure no Windows são diferentes da saudação que configurar proxy Olá no Linux.

#### <a name="windows"></a>Windows
As configurações de proxy devem ser configuradas corretamente para Olá conta Sistema Local tooaccess Olá da Internet. Se as configurações de proxy não são definidas pela política de grupo, você pode definir configurações de saudação para Olá conta Sistema Local.

1. Vá muito**iniciar**, digite **gpedit.msc**e, em seguida, selecione **Enter**.
2. Selecione **Configuração do computador** > **Modelos Administrativos** > **Componentes do Windows** > **Internet Explorer**. Certifique-se de que configuração de saudação **fazer proxy configurações por computador (em vez de por usuário)** está desabilitado ou não configurado.
3. Em **painel de controle**, ir muito**Central de rede e compartilhamento** > **opções da Internet**.
4. Em Olá **conexões** guia, selecione Olá **configurações da LAN** botão.
5. Olá limpar **detectar automaticamente as configurações** caixa de seleção.
6. Selecione Olá **usar um servidor proxy para a rede local** caixa de seleção e, em seguida, digite Olá endereço e porta proxy.
7. Selecione Olá **avançado** botão.
8. Em Olá **exceções** , digite o endereço IP hello **168.63.129.16**. Selecione **OK**.

#### <a name="linux"></a>Linux
Configurar proxy corretas Olá no arquivo de configuração de saudação do hello o agente de convidado do Microsoft Azure, que está localizado no \\etc\\waagent.conf.

Saudação de conjunto de parâmetros a seguir:

1.  **Host de proxy HTTP**. Por exemplo, defina-o muito**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Porta de proxy HTTP**. Por exemplo, defina-o muito**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Reinicie o agente de saudação.

  ```
  sudo service waagent restart
  ```

Olá configurações de proxy no \\etc\\waagent.conf também se aplicam a extensões de VM toohello necessário. Se você quiser toouse Olá repositórios do Azure, certifique-se de que repositórios de toothese tráfego Olá não está passando por sua intranet local. Se você tiver criado definido pelo usuário tooenable rotas túnel forçado, certifique-se de que você adicione uma rota que roteia repositórios do tráfego toohello toohello diretamente da Internet e não por meio de sua conexão de VPN site a site.

* **SLES**

  Também é necessário tooadd rotas para endereços IP hello listada em \\etc\\regionserverclnt.cfg. Olá figura a seguir mostra um exemplo:

  ![Túnel forçado][deployment-guide-figure-50]


* **RHEL**

  Também é necessário tooadd rotas para endereços IP de saudação de hosts Olá listada em \\etc\\yum.repos.d\\rhui balanceadores de carga. Para obter um exemplo, consulte Olá anterior figura.

* **Oracle Linux**

  Não há repositórios para Oracle Linux no Azure. Você precisa de suas própria repositórios tooconfigure para Oracle Linux ou use repositórios públicos Olá.

Para saber mais sobre Rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configurar hello Azure extensão de monitoramento aprimorada para SAP
Quando você preparou Olá VM conforme descrito em [cenários de implantação de VMs para SAP no Azure][deployment-guide-3], hello Azure VM Agent está instalado na máquina virtual de saudação. Olá próxima etapa é toodeploy hello Azure extensão de monitoramento aprimorada para SAP, que está disponível no hello repositório de extensão do Azure no hello data centers globais do Azure. Para obter mais informações, confira [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide-9.1].

Você pode usar tooinstall PowerShell ou CLI do Azure e configurar hello Azure extensão de monitoramento aprimorada para SAP. extensão de saudação tooinstall em um Windows ou a VM do Linux usando um computador Windows, consulte [Azure PowerShell][deployment-guide-4.5.1]. extensão de saudação tooinstall em uma VM do Linux usando uma área de trabalho do Linux, consulte [CLI do Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell para VMs Linux e Windows
Olá tooinstall aprimorada extensão de monitoramento Azure para SAP usando o PowerShell:

1. Certifique-se de que você instalou a versão mais recente de saudação do cmdlet do PowerShell do Azure hello. Para obter mais informações, confira [Implantando cmdlets do Azure PowerShell][deployment-guide-4.1].  
2. Execute Olá cmdlet do PowerShell a seguir.
    Para obter uma lista dos ambientes disponíveis, execute `commandlet Get-AzureRmEnvironment`. Se você quiser toouse global Azure, seu ambiente é **AzureCloud**. Para o Azure na China, selecione **AzureChinaCloud**.

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of hello environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

Depois de inserir os dados da conta e identificar Olá máquina virtual do Azure, o script hello implanta extensões Olá necessário e habilita os recursos de Olá necessário. Isso pode levar vários minutos.
Para obter mais informações sobre `Set-AzureRmVMAEMExtension`, confira [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].

![Execução bem-sucedida do cmdlet do Azure específico para SAP Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Olá `Set-AzureRmVMAEMExtension` configuração todos os hosts de saudação etapas tooconfigure monitoramento para SAP.

saída do script Hello inclui Olá informações a seguir:

* Confirmação de que o monitoramento de disco Olá SO e todos os discos de dados adicionais tenha sido configurado.
* duas próximas mensagens de saudação Confirmar configuração de saudação de métricas de armazenamento para uma conta de armazenamento específico.
* Uma linha de saída fornece o status de saudação da atualização real do hello da configuração de monitoramento de saudação.
* Outra linha de saída confirma que a configuração Olá foi implantada ou atualizada.
* a última linha Hello de saída é informativa. Ele mostra as opções de configuração de monitoramento Olá testes.
* toocheck que todas as etapas de monitoramento aprimorado do Azure foram executadas com êxito e que Olá infraestrutura do Azure fornece os dados necessários hello, prosseguir com a verificação de preparação de saudação para hello Azure extensão de monitoramento aprimorada para SAP, conforme descrito em [Verificação de preparação para o monitoramento aprimorado do Azure para SAP][deployment-guide-5.1].
* Aguarde 15 a 30 minutos para dados do diagnóstico do Azure toocollect Olá relevantes.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>CLI do Azure para VMs Linux
Olá tooinstall aprimorada extensão de monitoramento Azure para SAP usando a CLI do Azure:

1. Instale o 1.0 da CLI do Azure, conforme descrito em [instalação hello Azure CLI 1.0][azure-cli].
2. Entre usando sua conta do Azure:

  ```
  azure login
  ```

3. Alternar o modo do Gerenciador de recursos de tooAzure:

  ```
  azure config mode arm
  ```

4. Habilite o Monitoramento Aprimorado do Azure:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Verifique se que essa extensão de monitoramento aprimorada do Azure hello está ativo no hello VM do Linux do Azure. Verificação se Olá arquivo \\var\\lib\\AzureEnhancedMonitor\\PerfCounters existe. Se ele existir, no prompt de comando, execute estes comando toodisplay as informações coletadas pelo Olá Monitor aprimorado do Azure:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

saída de Hello tem esta aparência:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Verificações e solução de problemas para o monitoramento de ponta a ponta
Depois de implantar a VM do Azure e configurar a infraestrutura de monitoramento do Azure relevante hello, verifique se todos os componentes de saudação do hello extensão de monitoramento aprimorada do Azure estão funcionando conforme o esperado.

Executar verificação de preparação de saudação para hello Azure extensão de monitoramento aprimorada para SAP conforme descrito em [verificação de preparação para hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-5.1]. Se todos os resultados da verificação de preparação forem positivos e todos os contadores de desempenho relevantes parecerem corretos, o monitoramento do Azure terá sido configurado com êxito. Você pode prosseguir com a instalação de saudação do SAP Host Agent conforme descrito nas observações do SAP Olá no [recursos SAP][deployment-guide-2.2]. Se a verificação de preparação de saudação indica que contadores estão ausentes, execute a verificação de integridade de saudação do hello infraestrutura de monitoramento do Azure, conforme descrito na [verificação de integridade para configuração de infraestrutura de monitoramento do Azure] [ deployment-guide-5.2]. Para obter mais opções de solução de problemas, confira [Solucionando problemas de monitoramento do Azure para SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Verificação de preparação para hello Azure extensão de monitoramento aprimorada para SAP
Essa verificação garante que todas as métricas de desempenho que aparecem dentro de seu aplicativo SAP são fornecidas pelo Olá subjacente a infra-estrutura de monitoramento do Azure.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Executar verificação de preparação de saudação em uma VM do Windows

1.  Entrar no toohello máquina virtual do Azure (usar uma conta de administrador não é necessário).
2.  Abra uma janela de Prompt de Comando.
3.  No prompt de comando Olá, alterar pasta de instalação de toohello de diretório de saudação do hello Azure extensão de monitoramento aprimorada para SAP: c:\\pacotes\\plug-ins\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versão >\\drop

  Olá *versão* em Olá caminho toohello extensão de monitoramento pode variar. Se você ver pastas várias versões de saudação extensão na pasta de instalação do hello, verifique a configuração de saudação do hello AzureEnhancedMonitoring Windows service, de monitoramento e, em seguida, o comutador toohello pasta indicada como *tooexecutable de caminho* .

  ![Propriedades do serviço em execução hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-figure-1000]

4.  No prompt de comando hello, execute **azperflib.exe** sem parâmetros.

  > [!NOTE]
  > Azperflib.exe é executado em um loop e atualiza contadores Olá coletado a cada 60 segundos. loop de saudação tooend, janela de Prompt de comando Fechar hello.
  >
  >

Se Olá que extensão de monitoramento aprimorada do Azure não está instalado ou Olá AzureEnhancedMonitoring service não está em execução, a extensão de saudação não foi configurado corretamente. Para obter informações detalhadas sobre como toodeploy Olá extensão, consulte [solução de problemas hello infraestrutura de monitoramento do Azure para SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Verifique a saída de saudação de azperflib.exe
A saída de azperflib.exe mostra que todos os contadores de desempenho do Azure para SAP populados. Final Olá Olá lista de contadores coletados, um indicador de integridade e o resumo de mostrar o status de saudação do monitoramento do Azure.

![Saída da verificação de integridade executando azperflib.exe, que indica que não há problemas][deployment-guide-figure-1100]
<a name="figure-11"></a>

Verificar Olá resultado retornado para Olá **total de contadores** saída, que é relatada como vazios e para **status de integridade**, conforme mostrado no hello anterior figura.

Interprete os valores resultantes da saudação da seguinte maneira:

| Valores resultantes de Azperflib.exe | Status da integridade do monitoramento do Azure |
| --- | --- |
| **Chamadas à API – não disponíveis** | Os contadores não estão disponíveis podem ser qualquer uma das configurações de máquina virtual não aplicável toohello ou erros. Confira **Status de integridade**. |
| **Total de contadores - vazio** |Olá dois contadores de armazenamento do Azure a seguir pode ser vazia: <ul><li>Latência do servidor de operações de leitura de armazenamento (ms)</li><li>Latência E2E de operações de leitura de armazenamento (ms)</li></ul>Todos os outros contadores devem ter valores. |
| **Status de integridade** |OK somente se o status retornado mostrar **OK**. |
| **Diagnostics** |Informações detalhadas sobre o status da integridade. |

Se hello **status de integridade** valor não é **Okey**, siga as instruções de saudação em [verificação de integridade para configuração de infraestrutura de monitoramento do Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Executar verificação de preparação de saudação em uma VM do Linux

1.  Conecte-se toohello Máquina Virtual do Azure usando o SSH.

2.  Verifique a saída de saudação do hello extensão de monitoramento aprimorada do Azure.

  a.  Execute o `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Resultado esperado**: retorna a lista de contadores de desempenho. arquivo Hello não deve ficar vazio.

 b. Execute o `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Esperado um resultado**: uma linha de retorna onde é o erro de saudação **nenhum**, por exemplo, **3; config; Erro; 0; 0; Nenhum; 0; 1456416792; tst-servercs;**

  c. Execute o `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Resultado esperado**: retorna como vazio ou não existe.

Se hello verificação anterior não foi bem-sucedida, execute essas verificações adicionais:

1.  Certifique-se de que waagent hello está instalado e habilitado.

  a.  Execute o `sudo ls -al /var/lib/waagent/`

      **Esperado um resultado**: lista o conteúdo de saudação do diretório de waagent hello.

  b.  Execute o `ps -ax | grep waagent`

   **Resultado esperado**: exibe uma entrada semelhante a: `python /usr/sbin/waagent -daemon`

3.   Certifique-se de que Olá extensão de monitoramento aprimorada do Azure está instalado e em execução.

  a.  Execute o `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`

    **Esperado um resultado**: lista o conteúdo de saudação do diretório de extensão de monitoramento aprimorada do Azure hello.

  b. Execute o `ps -ax | grep AzureEnhanced`

     **Resultado esperado**: exibe uma entrada semelhante a: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Instalar o agente de Host do SAP, conforme descrito na nota da SAP [1031096]e verifique a saída de saudação do `saposcol`.

  a.  Execute o `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Execute o `dump ccm`

  c.  Verifique se Olá **Virtualization_Configuration\Enhanced monitoramento acesso** métrica é **true**.

Se já tiver um servidor de aplicativos ABAP do SAP NetWeaver instalado, abra a transação ST06 e verifique se o monitoramento avançado está habilitado.

Se qualquer uma dessas verificações falharem e para obter informações detalhadas sobre como tooredeploy Olá extensão, consulte [solução de problemas hello infraestrutura de monitoramento do Azure para SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Verificação de integridade para Olá configuração de infraestrutura de monitoramento do Azure
Se alguns dos dados de monitoramento de saudação não for fornecido corretamente, conforme indicado pelo teste Olá descritas [verificação de preparação para o monitoramento aprimorado do Azure para SAP][deployment-guide-5.1], execute hello `Test-AzureRmVMAEMExtension` toocheck do cmdlet Se Olá Olá extensão de monitoramento para SAP e infraestrutura de monitoramento do Azure está configurado corretamente.

1.  Certifique-se de que você instalou a versão mais recente de saudação do cmdlet do PowerShell do Azure hello, conforme descrito em [cmdlets do PowerShell do Azure implantar][deployment-guide-4.1].
2.  Execute Olá cmdlet do PowerShell a seguir. Para obter uma lista de ambientes disponíveis, execute o cmdlet de saudação `Get-AzureRmEnvironment`. Selecione do Azure, global toouse Olá **AzureCloud** ambiente. Para o Azure na China, selecione **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Insira os dados da conta e identificar Olá máquina virtual do Azure.

  ![Página de entrada do cmdlet do Azure específico para SAP Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. Olá script testes Olá configuração Olá máquina virtual que você selecionar.

  ![Saída do teste bem-sucedido da saudação infraestrutura de monitoramento do Azure para SAP][deployment-guide-figure-1300]

Verifique se cada resultado da verificação de integridade é **OK**. Se algumas verificações não forem exibidos **Okey**, execute o cmdlet update hello, conforme descrito na [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5]. Aguarde 15 minutos e repita Olá verificações descritas na [verificação de preparação para o monitoramento aprimorado do Azure para SAP] [ deployment-guide-5.1] e [verificação de integridade para configuração de infraestrutura de monitoramento do Azure] [deployment-guide-5.2]. Se Olá verificações ainda indicarem um problema com alguns ou todos os contadores, consulte [solução de problemas hello infraestrutura de monitoramento do Azure para SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Solução de problemas Olá infraestrutura de monitoramento do Azure para SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Os contadores de desempenho do Azure não aparecem
saudação de serviço do AzureEnhancedMonitoring Windows coleta métricas de desempenho no Azure. Se o serviço de saudação não foi instalado corretamente ou se ele não está em execução em sua VM, nenhuma métrica de desempenho pode ser coletada.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>diretório de instalação de saudação do hello extensão de monitoramento aprimorada do Azure está vazio

###### <a name="issue"></a>Problema
diretório de instalação Olá c:\\pacotes\\plug-ins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;versão >\\drop está vazio.

###### <a name="solution"></a>Solução
extensão de saudação não está instalado. Determine se esse é um problema de proxy (conforme descrito anteriormente). Talvez seja necessário toorestart máquina de saudação ou execute Olá `Set-AzureRmVMAEMExtension` script de configuração.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>O serviço de Monitoramento Avançado do Azure não existe

###### <a name="issue"></a>Problema
Olá AzureEnhancedMonitoring Windows service não existe.

A saída de Azperflib.exe gera um erro:

![A execução de azperflib.exe indica que não está executando o serviço de saudação do hello extensão de monitoramento aprimorada do Azure para SAP][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Solução
Se o serviço de saudação não existir, hello Azure extensão de monitoramento aprimorada para SAP não foi instalado corretamente. Reimplante a extensão de saudação usando Olá etapas descritas para seu cenário de implantação no [cenários de implantação de VMs para SAP no Azure][deployment-guide-3].

Depois de implantar a extensão hello, após uma hora, verifique novamente se contadores de desempenho do Azure Olá são fornecidos nos Olá VM do Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Serviço de monitoramento aprimorado do Azure existe, mas não toostart

###### <a name="issue"></a>Problema
Olá serviço AzureEnhancedMonitoring Windows existe e está habilitado, mas falha toostart. Para obter mais informações, verifique o log de eventos do aplicativo hello.

###### <a name="solution"></a>Solução
Olá configuração está incorreta. Reiniciar Olá monitoramento de extensão para Olá VM, conforme descrito em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Faltam alguns contadores de desempenho do Azure
saudação de serviço do AzureEnhancedMonitoring Windows coleta métricas de desempenho no Azure. serviço de saudação obtém dados de várias fontes. Alguns dados de configuração são coletados localmente e algumas métricas de desempenho são lidas do Diagnóstico do Azure. Contadores de armazenamento são usados a partir de seu logon no nível de assinatura de armazenamento hello.

Se a solução de problemas com a nota SAP [1999351] não resolver o problema de hello, execute novamente a saudação `Set-AzureRmVMAEMExtension` script de configuração. Você pode ter toowait hora porque contadores de diagnóstico ou de análise de armazenamento não podem ser criados imediatamente depois que elas estão habilitadas. Se Olá problema persistir, abra uma mensagem de suporte de cliente SAP em Olá componente BC-OP-NT-AZR para Windows ou BC-OP-LNX-AZR para uma máquina virtual Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Os contadores de desempenho do Azure não aparecem
Métricas de desempenho no Azure são coletadas por um daemon. Se o daemon de saudação não está em execução, nenhuma métrica de desempenho pode ser coletada.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>diretório de instalação de saudação do hello extensão de monitoramento aprimorado do Azure está vazio

###### <a name="issue"></a>Problema
diretório de saudação \\var\\lib\\waagent\\ não tem um subdiretório para Olá extensão de monitoramento aprimorado do Azure.

###### <a name="solution"></a>Solução
extensão de saudação não está instalado. Determine se esse é um problema de proxy (conforme descrito anteriormente). Talvez seja necessário toorestart hello e / execute Olá `Set-AzureRmVMAEMExtension` script de configuração.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Faltam alguns contadores de desempenho do Azure
Métricas de desempenho no Azure são coletadas por um daemon, que obtém os dados de várias fontes. Alguns dados de configuração são coletados localmente e algumas métricas de desempenho são lidas do Diagnóstico do Azure. Contadores de armazenamento são provenientes Olá logs na sua assinatura de armazenamento.

Para obter uma lista completa e atualizada dos problemas conhecidos, confira a Nota SAP [1999351], que tem informações adicionais de solução de problemas para o Monitoramento Avançado do Azure para SAP.

Se a solução de problemas com a nota SAP [1999351] não resolver o problema de saudação, execute novamente a saudação `Set-AzureRmVMAEMExtension` script de configuração, conforme descrito em [configurar hello Azure extensão de monitoramento aprimorada para SAP][deployment-guide-4.5]. Você pode ter toowait para uma hora porque contadores de diagnóstico ou de análise de armazenamento não podem ser criados imediatamente depois que elas estão habilitadas. Se Olá problema persistir, abra uma mensagem de suporte de cliente SAP em Olá componente BC-OP-NT-AZR para Windows ou BC-OP-LNX-AZR para uma máquina virtual Linux.
