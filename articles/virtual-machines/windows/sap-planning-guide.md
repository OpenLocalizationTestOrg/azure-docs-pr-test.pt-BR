---
title: "aaaSAP NetWeaver nas máquinas virtuais do Azure – planejamento e implementação | Microsoft Docs"
description: "SAP NetWeaver em VMs (Máquinas Virtuais) do Azure – Guia de planejamento e implementação"
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 2b58a419-c892-4722-8cb6-2f8beef4430c
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53d63240760282b409f7e9412e8240689bcbcc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--planning-and-implementation-guide"></a>SAP NetWeaver em VMs (Máquinas Virtuais) Windows do Azure – Guia de planejamento e implementação
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
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/sap-get-started.mdsap-dbms-guide.md
[getting-started-windows-classic-dbms]:classic/sap-get-started.mdsap-dbms-guide.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/sap-get-started.mdsap-dbms-guide.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/sap-get-started.mdsap-dbms-guide.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/sap-get-started.mdsap-dbms-guide.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/sap-get-started.mdsap-dbms-guide.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#step-2-create-vm-image
[virtual-machines-windows-capture-image]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../virtual-machines-windows-create-vm-generalized.md
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Microsoft Azure permite que os recursos de computação e armazenamento de tooacquire empresas no tempo mínimo sem ciclos de compra longos. Máquinas virtuais do Azure permitem empresas toodeploy de aplicativos clássicos, como aplicativos no Azure baseados no SAP NetWeaver e estender a confiabilidade e disponibilidade sem a necessidade de mais recursos disponíveis no local. Serviços de máquina Virtual do Azure também oferece suporte à conectividade entre locais, tooactively de empresas que permite integrar máquinas virtuais do Azure em seus domínios locais, suas nuvens privadas e seu ambiente de sistema SAP.
Este white paper descreve os conceitos básicos de saudação da máquina Virtual do Microsoft Azure e fornece uma passo a passo das considerações de planejamento e implementação para instalações do SAP NetWeaver no Azure e como tal deve ser Olá documento tooread antes de iniciar implantações reais do SAP NetWeaver no Azure.
Olá papel complementa Olá documentação de instalação do SAP e observações sobre o SAP que representam os recursos principais de saudação para instalações e implantações de software SAP em fornecidos plataformas.

## <a name="summary"></a>Resumo
Computação em nuvem é um termo amplamente usado que está adquirindo cada vez mais importância no hello setor de TI de empresas de pequenas porte a empresas toolarge e multinacional.

Microsoft Azure é hello plataforma de serviços de nuvem da Microsoft que oferece uma ampla variedade de novas possibilidades. Agora, os clientes estão toorapidly capaz de provisionar e provisionamento de aplicativos como um serviço em nuvem hello, para que eles não são limitado tootechnical ou restrições de orçamentos. Em vez de investir tempo e dinheiro na infraestrutura de hardware, as empresas podem concentrar no aplicativo hello, processos de negócios e seus benefícios para os clientes e usuários.

Com os Serviços de Máquina Virtual do Microsoft Azure, a Microsoft oferece uma plataforma abrangente de IaaS (Infraestrutura como Serviço). Os aplicativos baseados no SAP NetWeaver têm suporte em Máquinas Virtuais do Azure (IaaS). Este white paper descreverá como tooplan e implementar SAP NetWeaver com base em aplicativos no Microsoft Azure como plataforma Olá preferencial.

documento de saudação se concentrará em dois aspectos principais:

* Olá primeira parte descreverá dois padrões de implantação com suporte para aplicativos baseados no SAP NetWeaver no Azure. Ele também descreve a manipulação geral do Azure com implantações da SAP em mente.
* Olá segunda parte detalhará implementação Olá dois cenários diferentes descritos na primeira parte do hello.

Para obter recursos adicionais, confira o capítulo [Recursos][planning-guide-1.2] neste documento.

### <a name="definitions-upfront"></a>Definições prévias
Em todo o documento de saudação usaremos Olá termos a seguir:

* IaaS: infraestrutura como serviço.
* PaaS: plataforma como serviço.
* SaaS: software como serviço.
* ARM: Azure Resource Manager
* Componente SAP: um aplicativo SAP individual como ECC, BW, Solution Manager ou EP.  Os componentes SAP podem ser baseados em tecnologias ABAP ou Java tradicionais ou em um aplicativo não baseado em NetWeaver, como o Business Objects.
* Ambiente SAP: um ou mais componentes SAP logicamente agrupados tooperform uma função empresarial como desenvolvimento, QAS, treinamento, DR ou produção.
* Estrutura SAP: Refere-se toohello inteiros ativos SAP em um cliente cenário de TI. Olá estrutura SAP inclui todos os ambientes de produção e não seja de produção.
* Sistema SAP: combinação de saudação da camada de DBMS e camada de aplicativo de, por exemplo, um sistema de desenvolvimento SAP ERP, sistema de teste do SAP BW, sistema de produção SAP CRM, etc... No Azure implantações que não é suportada toodivide essas duas camadas entre local e o Azure. Isso significa que um sistema SAP é implantado localmente ou no Azure. No entanto, você pode implantar sistemas diferentes de saudação de uma estrutura SAP no Azure ou no local. Por exemplo, você pode implantar os sistemas Olá desenvolvimento e teste de SAP CRM no Azure, mas Olá SAP CRM produção sistema local.
* Implantação somente em nuvem: uma implantação onde Olá assinatura do Azure não está conectado por meio de uma site a site ou rota expressa conexão toohello local infraestrutura de rede. Na documentação comum do Azure, esses tipos de implantações também são descritos como implantações 'Somente em nuvem'. Máquinas virtuais implantadas com esse método são acessadas por meio de Olá internet e um endereço IP público e/ou um DNS público nome atribuído toohello VMs no Azure. Para o Microsoft Windows hello local Active Directory (AD) e o DNS não for estendido tooAzure nesses tipos de implantações. Portanto, Olá VMs não fazem parte de saudação do Active Directory local. Mesmo é verdadeiro para implementações de Linux usando, por exemplo, OpenLDAP + Kerberos.

> [!NOTE]
> As implantações de Somente Nuvem neste documento são definidas como cenários SAP completos executados exclusivamente no Azure sem a extensão do Active Directory / OpenLDAP ou a resolução de nome do local para a nuvem pública. Não há suporte para configurações somente em nuvem para sistemas SAP de produção ou configurações onde STMS SAP ou outros recursos de local precisam toobe usado entre os sistemas SAP hospedados no Azure e os recursos que residem no local.
>
>

* Entre locais: Descreve um cenário em que as VMs são implantado tooan assinatura do Azure com o site a site, vários local ou conectividade de rota expressa entre Olá local datacenter(s) e o Azure. Na documentação comum do Azure, esses tipos de implantações também são descritas como cenários entre instalações. motivo da saudação para conexão Olá é tooextend domínios, local no local do Active Directory / OpenLDAP locais e de DNS no Azure. Olá paisagem local é estendido toohello ativos do Azure da assinatura de saudação. Com esta extensão, Olá VMs pode ser parte do domínio de local de saudação. Usuários de domínio do domínio do hello local podem acessar servidores hello e podem executar serviços nas VMs (como serviços DBMS). A comunicação e resolução de nomes entre máquinas virtuais implantadas localmente e VMs implantadas no Azure são possíveis. Esse é o cenário de saudação que esperamos que a maioria dos toobe de ativos SAP implantado no.  Para obter mais informações, veja [este][vpn-gateway-cross-premises-options] artigo e [este][vpn-gateway-site-to-site-create].

> [!NOTE]
> Implantações entre instalações de sistemas SAP em que máquinas virtuais do Azure que executam sistemas SAP são membros de um domínio local têm suporte para sistemas SAP de produção. Configurações entre locais têm suporte para a implantação de partes ou estruturas da SAP completas no Azure. Até mesmo em execução estrutura SAP completa de saudação no Azure, é necessário ter as VMs estão sendo parte do domínio local e anúncios / OpenLDAP. Em versões anteriores da documentação de saudação falamos sobre cenários de TI híbrida, onde o termo de saudação 'Híbrida' está enraizado no Olá fato de haver uma conectividade entre locais entre local e o Azure. Além disso, fato Olá que Olá VMs no Azure fazem parte da saudação local do Active Directory / OpenLDAP.
>
>

Alguma documentação da Microsoft descreve cenários entre instalações de modo um pouco diferente, especialmente para configurações de HA do DBMS. Em Olá caso de Olá SAP documentos relacionados, cenário entre locais de saudação apenas resume toohaving um site a site ou privado (rota expressa) conectividade e hello fato que o cenário SAP Olá é distribuído entre local e o Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Recursos
Olá a seguintes guias adicionais estão disponíveis para o tópico Olá das implantações do SAP no Azure:

* [SAP NetWeaver em VMs (máquinas virtuais) do Azure – Guia de planejamento e implementação (este documento)][planning-guide]
* [SAP NetWeaver em VMs (máquinas virtuais) do Azure – Guia de implantação][deployment-guide]
* [SAP NetWeaver em VMs (máquinas virtuais) do Azure – Guia de implantação de DBMS][dbms-guide]
* [SAP NetWeaver em VMs (Máquinas Virtuais) do Azure – Guia de implantação de alta disponibilidade][ha-guide]

> [!IMPORTANT]
> Sempre que possível um toohello link referindo-se o guia de instalação do SAP é usado (referência de InstGuide-01, consulte <http://service.sap.com/instguides>). Quando se trata de toohello pré-requisitos e o processo de instalação, guias de instalação do hello SAP NetWeaver deve sempre ser lidos com atenção, pois este documento só abrange tarefas específicas para sistemas SAP NetWeaver instalados em uma máquina Virtual Microsoft Azure.
>
>

Olá SAP observações a seguir está relacionadas toohello tópico do SAP no Azure:

| Número da observação | Title |
| --- | --- |
| [1928533] |Aplicativos SAP no Azure: dimensionamento e produtos com suporte |
| [2015553] |SAP no Microsoft Azure: pré-requisitos de suporte |
| [1999351] |Solução de problemas de monitoramento aprimorado do Azure para SAP |
| [2178632] |Métricas-chave de monitoramento para SAP no Microsoft Azure |
| [1409604] |Virtualização no Windows: monitoramento avançado |
| [2191498] |SAP no Linux com o Azure: monitoramento avançado |
| [2243692] |Linux na VM do Microsoft Azure (IaaS): problemas de licença SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: notas de instalação |
| [2002167] |Red Hat Enterprise Linux 7.x: instalação e atualização |

Leia também Olá [Wiki de SCN](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) que contém todas as observações sobre o SAP para Linux.

As limitações gerais padrão e as limitações máximas das assinaturas do Azure podem ser encontradas [neste artigo][azure-subscription-service-limits-subscription]

## <a name="possible-scenarios"></a>Cenários possíveis
SAP geralmente é visto como um dos aplicativos de missão crítica Olá em empresas. arquitetura de saudação e as operações desses aplicativos geralmente é muito complexo e é muito importante garantir que você atenda aos requisitos de disponibilidade e desempenho.

Assim, as empresas têm toothink cuidadosamente sobre quais aplicativos podem ser executados em um ambiente de nuvem pública, independente do provedor de nuvem Olá escolhido.

Os tipos de sistema possíveis para implantação da SAP NetWeaver com base em aplicativos em ambientes de nuvem pública estão listados abaixo:

1. Sistemas de produção de médio porte
2. Sistemas de desenvolvimento
3. Sistemas de teste
4. Protótipos de sistema
5. Sistemas de demonstração/aprendizado

Em ordem toosuccessfully implantar sistemas SAP na IaaS do Azure ou IaaS em geral, é importante toounderstand diferenças significativas sobre Olá entre Olá ofertas dos fornecedores terceirizados tradicionais ou hosters e IaaS. Enquanto o hoster tradicional hello ou terceiros adapta a carga de trabalho infraestrutura (tipo de servidor, rede e armazenamento) toohello um cliente desejar toohost, em vez disso, é responsabilidade toochoose Olá carga de trabalho certa do cliente Olá para implantações de IaaS.

Como uma primeira etapa, os clientes precisam Olá tooverify itens a seguir:

* Olá SAP com suporte a tipos de VM do Azure
* Olá SAP produtos/versões com suporte no Azure
* Olá suporte para versões de sistema operacional e DBMS para Olá que libera SAP específicas no Azure
* Taxa de transferência de SAPS fornecida por diferentes SKUs do Azure

Olá respostas toothese perguntas podem ser lidos na nota da SAP [1928533].

Como uma segunda etapa, limitações de largura de banda e recursos do Azure precisam de consumo de recursos de tooactual toobe comparado de sistemas locais. Portanto, os clientes necessidade toobe familiarizado com recursos diferentes de saudação do hello Azure tipos compatíveis com a SAP na área de saudação do:

* Recursos de CPU e memória de diferentes tipos de VM e
* Largura de banda IOPS de diferentes tipos de VM e
* Recursos de rede de diferentes tipos de VM.

A maioria desses dados pode ser encontrada [aqui][virtual-machines-sizes]

Tenha em mente que Olá limites listados no link de saudação acima são os limites superiores. Isso não significa que limita o hello para qualquer um dos recursos de saudação, por exemplo, IOPS pode ser fornecido em todas as circunstâncias. exceções de saudação embora são recursos de CPU e memória de saudação de um tipo VM escolhido. Para tipos VM Olá suportados pelo SAP, os recursos de CPU e memória Olá são reservados e como tal, disponíveis em qualquer ponto no tempo para consumo Olá VM.

plataforma do Microsoft Azure Hello como outras plataformas de IaaS é uma plataforma de multilocatária. Isso significa que os recursos de armazenamento, rede e outros são compartilhados entre locatários. Lógica inteligente de limitação e cota é tooprevent usado um locatário afete o desempenho de saudação do outro locatário (vizinho barulhento) de forma significativa. Embora lógica em tentativas do Azure tookeep variações de largura de banda pequena, plataformas altamente compartilhadas tendem a variações maiores toointroduce na disponibilidade de recursos/largura de banda que muitos clientes é usada tooin suas implantações no local. Como resultado, você pode experimentar diferentes níveis de largura de banda no que diz respeito toonetworking ou no armazenamento de e/s (Olá, bem como latência) do toominute minuto. probabilidade de saudação que um sistema SAP no Azure pode apresentar variações maiores do que em um sistema local precisa toobe levada em conta.

A última etapa é tooevaluate requisitos de disponibilidade. Isso pode acontecer, essa Olá subjacente a infraestrutura do Azure precisa tooget atualizado e requer hosts Olá executando toobe VMs reinicializado. Nesses casos, as VMs em execução nesses hosts seriam desligadas e reiniciadas também. tempo de saudação de manutenção, é feito durante o horário comercial não essenciais para uma região específica, mas Olá intervalo de horas durante o qual uma reinicialização ocorrerá é relativamente longo. Há diversas tecnologias na Olá plataforma Windows Azure que pode ser configurado toomitigate alguns ou todos os Olá impacto dessas atualizações. Aperfeiçoamentos futuros de Olá plataforma Windows Azure, aplicativo de DBMS e SAP são projetados toominimize impacto Olá essas reinicializações.

Toosuccessfully implantar um sistema SAP no Azure, local hello SAP sistemas de sistema operacional, banco de dados e aplicativos SAP deve aparecer em Olá matriz de suporte do Azure do SAP, se ajustar dentro de Olá Olá de recursos pode fornecer a infraestrutura do Azure e que pode trabalhar com hello que oferece disponibilidade SLAs Microsoft Azure. Como esses sistemas são identificados, você precisa toodecide em uma saudação dois cenários de implantação a seguir.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Somente em nuvem - implantações de máquina Virtual no Azure sem dependências nos Olá local rede de cliente
![VM única com cenário de demonstração ou treinamento SAP implantado no Azure][planning-guide-figure-100]

Esse cenário é típico para treinamento ou sistemas de demonstração, onde todos os componentes de saudação do SAP e o software SAP não estão instalados em uma única VM. Nesse cenário de implantação, não há suporte para sistemas SAP de produção. Em geral, este cenário atende Olá requisitos a seguir:

* próprias Olá VMs são acessíveis pela rede pública hello. Conectividade de rede direta para aplicativos de saudação em execução dentro de saudação VMs toohello rede de qualquer empresa Olá possui Olá demonstrações ou treinamentos conteúdo local ou cliente Olá não é necessário.
* No caso de várias VMs que representam o cenário de demonstração ou treinamentos hello, resolução de nomes e as comunicações de rede precisa toowork entre VMs hello. Mas as comunicações entre o conjunto de saudação de VMs precisam toobe a isoladas para que vários conjuntos de máquinas virtuais podem ser implantados lado a lado sem interferência.  
* Conectividade com a Internet é necessária para logon de tooremote do usuário final Olá em toohello que VMs hospedadas no Azure. Dependendo do sistema operacional convidado do hello, serviços de Terminal/RDS ou VNC/ssh é usado tooaccess Olá VM tooeither cumprir Olá treinamento tarefas ou executar demonstrações hello. Se as portas de SAP como 3200, 3300 & 3600 podem também ser exposto instância do aplicativo SAP Olá pode ser acessada de qualquer área de trabalho conectada à Internet.
* Olá sistemas SAP (e VM(s)) representam um cenário independente no Azure que só exige conectividade com a internet pública para o acesso do usuário final e não requer uma conexão tooother VMs no Azure.
* O SAPGUI e um navegador estão instalados e executados diretamente em Olá VM.
* É necessário uma redefinição rápida de um estado da VM toohello original e a nova implantação desse estado original novamente.
* No caso de saudação de demonstração e cenários de treinamento que são realizados em várias VMs, um Active Directory / serviço OpenLDAP e/ou o DNS é necessário para cada conjunto de VMs.

![Grupo de VMs que representam um cenário de demonstração ou treinamento em um serviço de nuvem do Azure][planning-guide-figure-200]

É importante tookeep em mente que Olá VMs em cada Olá define necessidade toobe implantado em paralelo, em que os nomes de VM de saudação em cada conjunto de saudação são Olá mesmo.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>entre locais - implantação de uma ou várias VMs SAP no Azure com o requisito de saudação de integração completa à rede do local de saudação
![VPN com conectividade Site a Site (entre instalações)][planning-guide-figure-300]

Esse é um cenário entre instalações com muitos padrões de implantação possíveis. Ele pode ser descrito simplesmente como a execução de algumas partes do hello SAP paisagem no local e outras partes da saudação estrutura SAP no Azure. Todos os aspectos do fato de saudação parte dos componentes do hello SAP em execução no Azure devem ser transparentes para os usuários finais. Olá, portanto, o sistema de correção de transporte SAP (STMS), comunicação RFC, impressão, a segurança (como SSO), etc. funcionarão perfeitamente para sistemas SAP de saudação em execução no Azure. Mas o cenário entre locais de saudação também descreve um cenário onde a estrutura SAP completa de saudação é executado no Azure com domínio saudação do cliente e estendidos de DNS para o Azure.

> [!NOTE]
> Esse é o cenário de implantação de saudação que tem suporte para a execução de sistemas SAP de produção.
>
>

Leitura [neste artigo] [ vpn-gateway-create-site-to-site-rm-powershell] para obter mais informações sobre como tooconnect seu local de rede tooMicrosoft do Azure

> [!IMPORTANT]
> Quando falamos sobre cenários entre locais entre implantações de clientes locais e do Azure, estamos procurando na granularidade de saudação de todos os sistemas SAP. Cenários que *não têm suporte* para cenários entre instalações são:
>
> * Executar diferentes camadas de aplicativos SAP em diferentes métodos de implantação. Por exemplo executando Olá DBMS camada no local, mas a camada do aplicativo SAP Olá em VMs implantadas como VMs do Azure ou vice-versa.
> * Alguns componentes de uma camada SAP no Azure e alguns localmente. Por exemplo Dividir instâncias da camada do aplicativo SAP Olá entre locais e VMs do Azure.
> * Não há suporte para a distribuição de VMs que executam instâncias SAP de um sistema por várias Regiões do Azure.
>
> motivo Olá dessas restrições é o requisito de saudação para uma rede de alto desempenho de latência muito baixa dentro de um sistema SAP, especialmente entre instâncias do aplicativo hello e camada de DBMS Olá de um sistema SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Versões de banco de dados e SO com suporte
* O software do servidor da Microsoft com suporte para os Serviços da Máquina Virtual do Azure está listado neste artigo: <http://support.microsoft.com/kb/2721672>.
* As versões do sistema de operacional e versões do sistema de banco de dados para as quais há suporte pelos Serviços da Máquina Virtual do Azure em conjunto com o software SAP estão documentadas na Nota do SAP [1928533].
* As versões e aplicativos do SAP para os quais há suporte nos Serviços da Máquina Virtual do Azure estão documentadas na Nota do SAP [1928533].
* Somente imagens de 64 bits são toorun com suporte como VMs convidadas no Azure em cenários SAP. Isso também significa que apenas aplicativos e bancos de dados SAP de 64 bits têm suporte.

## <a name="microsoft-azure-virtual-machine-services"></a>Serviços da Máquina Virtual do Microsoft Azure
Olá Microsoft Azure é uma nuvem de escala da internet plataforma de serviços hospedados e operada no Microsoft data centers. plataforma de saudação inclui serviços de máquina Virtual Olá Microsoft Azure (infraestrutura como um serviço ou IaaS) e um conjunto de plataforma rica como recursos de um serviço (PaaS).

Olá plataforma Azure reduz a necessidade de saudação de prévias de tecnologia e infraestrutura de compras. Ele simplifica a manutenção e operação de aplicativos, fornecendo toohost de computação e armazenamento sob demanda, dimensionar e gerenciar o aplicativo web e aplicativos conectados. Gerenciamento de infraestrutura é automatizado com uma plataforma projetada para alta disponibilidade e dimensionamento toomatch necessidades de uso com a opção de saudação de um modelo de preços pré-pago dinâmico.

![Posicionamento de Serviços da Máquina Virtual do Microsoft Azure][planning-guide-figure-400]

Com os serviços de máquina Virtual do Azure, a Microsoft permite toodeploy tooAzure de imagens de servidor personalizado como instâncias de IaaS (consulte a Figura 4). Olá máquinas virtuais no Azure se baseiam em discos rígidos virtuais (VHD) do Hyper-V e são toorun capaz de diferentes sistemas operacionais, como o sistema operacional convidado.

Do ponto de vista operacional, Olá que serviço de máquina Virtual do Azure oferece semelhante apresenta como máquinas virtuais implantadas no local. No entanto, ele tem a vantagem significativa de saudação não é necessário tooprocure, administrar e gerenciar infraestrutura de saudação. Os desenvolvedores e administradores têm controle total da imagem do sistema operacional Olá nessas máquinas virtuais. Os administradores podem fazer logon remotamente em manutenção de tooperform essas máquinas virtuais e solução de problemas de tarefas, bem como tarefas de implantação de software. Em toodeployment de relação, a saudação únicas restrições são tamanhos hello e os recursos de máquinas virtuais do Azure. Elas podem não ter uma configuração tão refinada, já que isso pode ser feito localmente. Há uma variedade de tipos VM que representam uma combinação de:

* Número de vCPUs,
* Memória,
* Número de VHDs que podem ser anexados,
* Larguras de banda de rede e de armazenamento.

tamanho de saudação e as limitações de vários tamanhos de máquinas virtuais diferentes oferecidos podem ser vistos em uma tabela em [neste artigo][virtual-machines-sizes]

Conforme você perceberá, existem diferentes famílias ou séries de máquinas virtuais. A partir de dezembro de 2015, você pode distinguir Olá famílias de máquinas virtuais a seguir:

* Tipos de VM A0-A7: nem todas elas são certificadas para SAP. Primeira série de VMs com a qual o IaaS do Azure foi introduzido.
* Tipos de VM A8-A11: instâncias de computação de alto desempenho. Em execução em hosts de computação diferentes e com melhor desempenho que outras VMs da série A.
* Tipos de VM série D: desempenho superior a A0-A7. Nem todos os tipos de VM Olá certificados com o SAP.
* Tipos de VM da série DS: usar os mesmos hosts como série D, mas são tooAzure tooconnect capaz de armazenamento Premium (consulte o capítulo [armazenamento Premium do Azure] [ planning-guide-3.3.2] deste documento). Outra vez, nem todos os tipos de VM são certificados com SAP.
* Tipos de VM da série G: tipos de VM de memória alta.
* Tipos de VM série GS: como a série G mas incluindo Olá opção toouse armazenamento Premium do Azure (consulte o capítulo [armazenamento Premium do Azure] [ planning-guide-3.3.2] deste documento). Ao usar as VMs da série GS como servidores de banco de dados é obrigatório toouse armazenamento Premium para arquivos de log de transações e dados do banco de dados

Você pode achar Olá mesmas configurações de CPU e memória em outra série VM. No entanto, ao analisar o desempenho de taxa de transferência Olá essas VMs fora de séries diferentes Olá elas podem diferir significativamente. Apesar de terem Olá a mesma configuração de CPU e memória. Motivo é que hardware servidor host de Olá subjacente na introdução de saudação de diferentes tipos de VM Olá características diferentes de taxa de transferência.  Geralmente diferença Olá mostrada no desempenho da taxa de transferência também é refletida no preço Olá Olá diferentes VMs.

Observe que série VM não diferente pode ser oferecido em cada uma das regiões do Azure da saudação (para regiões do Azure consulte próximo capítulo). Além disso, lembre-se de que nem todas as VMs ou séries de VMs são certificadas para SAP.

> [!IMPORTANT]
> Para uso de saudação do aplicativos baseados no SAP NetWeaver, somente subconjunto de saudação de tipos de VM e as configurações listadas na nota da SAP [1928533] têm suporte.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Regiões do Azure
Microsoft permite toodeploy máquinas virtuais em chamado 'regiões do Azure'. Uma Região do Azure pode ser um ou vários data centers cuja localização é muito próxima. Para a maioria dos Olá geopolíticas regiões no Olá, mundo Microsoft tem pelo menos duas regiões do Azure. Por exemplo na Europa, há uma Região do Azure da ‘Europa Setentrional’ e uma da ‘Europa Ocidental’. Essas duas regiões do Azure dentro de uma região geopolíticas são separados por distância significativa o suficiente para que a desastres naturais ou técnicas não afetam as duas regiões do Azure no hello mesma região geopolíticas. Desde que a Microsoft está constantemente desenvolvendo novas regiões do Azure em diferentes regiões geopolíticas globalmente, o número de saudação dessas regiões está crescendo e a partir de dezembro de 2015 atingiu o número de saudação 20 regiões do Azure com regiões adicionais anunciadas já. Você, como um cliente pode implantar sistemas SAP em todas essas regiões, incluindo Olá duas regiões do Azure na China. Atual backup toodate informações sobre regiões do Azure consulte este site: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Olá conceito de máquina Virtual do Microsoft Azure
Microsoft Azure oferece uma infraestrutura como um toohost de solução de serviço (IaaS) máquinas virtuais com funcionalidades semelhantes como uma solução de virtualização local. Você é capaz de toocreate máquinas virtuais de dentro de saudação Portal do Azure, PowerShell ou CLI, que também oferecem recursos de gerenciamento e implantação.

Gerenciador de recursos do Azure permite que você tooprovision seus aplicativos usando um modelo declarativo. Em um modelo único, você pode implantar vários serviços, juntamente com suas dependências. Use Olá toorepeatedly do mesmo modelo implantar seu aplicativo durante cada estágio do ciclo de vida do aplicativo hello.

Mais informações sobre o uso de modelos ARM podem ser encontradas aqui:

* [Implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e hello CLI do Azure][virtual-machines-linux-cli-deploy-templates]
* [Gerenciar máquinas virtuais usando o Azure Resource Manager e o PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

Outro recurso interessante é imagens de toocreate Olá capacidade das máquinas virtuais, que permite a você tooprepare determinado repositórios do qual você está tooquickly capaz de implantar as instâncias de máquina Virtual que atender às suas necessidades.

Mais informações sobre a criação de imagens de Máquinas Virtuais podem ser encontradas [neste artigo (Windows)][virtual-machines-windows-capture-image] ou [neste artigo (Linux)][virtual-machines-linux-capture-image].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domínios com falhas
Domínios de falha representam uma unidade física de falha, a infraestrutura física de toohello intimamente relacionados contida em data centers e, embora um blade ou rack físico possa ser considerada um domínio de falha, não há nenhum mapeamento direto entre hello dois.

Quando você implanta várias máquinas virtuais como parte de um sistema SAP nos serviços de máquina Virtual do Microsoft Azure, você pode influenciar Olá controlador de malha do Azure toodeploy seu aplicativo em diferentes domínios de falha, assim, atendendo aos requisitos de saudação do hello SLA do Microsoft Azure. Olá, no entanto, a distribuição de domínios de falha em uma unidade de escala do Azure (coleção de centenas de nós de computação ou nós de armazenamento e rede) ou atribuição de saudação de VMs tooa específicos de domínio de falha é algo sobre o qual você não tem controle direto. Em ordem toodirect Olá malha do Azure controlador toodeploy um conjunto de máquinas virtuais em diferentes domínios de falha, você precisa tooassign um toohello conjunto de disponibilidade do Azure VMs no momento da implantação. Para saber mais sobre Conjuntos de Disponibilidade do Azure, confira o capítulo [Conjuntos de Disponibilidade do Azure][planning-guide-3.2.3] deste documento.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Domínios de Atualização
Domínios de atualização representam uma unidade lógica que ajudam a toodetermine como uma VM em um sistema SAP, que consiste em instâncias SAP em execução em várias VMs, será atualizada. Quando ocorre uma atualização, o Microsoft Azure atravessa Olá processo de atualizar esses domínios de atualização um por um. Ao distribuir as VMs no momento da implantação em diferentes domínios de atualização, você pode proteger seu sistema SAP parcialmente contra um potencial tempo de inatividade. Em ordem tooforce toodeploy Azure Olá VMs de um sistema SAP distribuídas entre diferentes domínios de atualização, é necessário tooset um atributo específico no momento da implantação de cada VM. Domínios de tooFault semelhante, uma unidade de escala do Azure é dividido em vários domínios de atualização. Em ordem toodirect Olá malha do Azure controlador toodeploy um conjunto de VMs entre diferentes domínios de atualização, você precisa tooassign um toohello conjunto de disponibilidade do Azure VMs no momento da implantação. Para saber mais sobre Conjuntos de Disponibilidade do Azure, confira o capítulo [Conjuntos de Disponibilidade do Azure][planning-guide-3.2.3] abaixo.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Conjuntos de Disponibilidade do Azure
Máquinas virtuais do Azure em um conjunto de disponibilidade do Azure será distribuído por Olá controlador de malha do Azure em diferentes domínios de falha e atualização. Olá finalidade distribuição Olá em diferentes domínios de falha e atualização é tooprevent que todas as VMs de um sistema SAP seja desligadas em caso de saudação de manutenção da infraestrutura ou uma falha em um domínio de falha. Por padrão, VMs não fazem parte de um conjunto de disponibilidade. participação de saudação de uma VM em um conjunto de disponibilidade é definida no momento da implantação ou posteriormente através da reconfiguração ou reimplantação da VM.

conceito de saudação toounderstand da forma de conjuntos de disponibilidade do Azure e hello conjuntos de disponibilidade relacionar tooFault e domínios de atualização, leia [neste artigo][virtual-machines-manage-availability]

Consulte toodefine conjuntos de disponibilidade para ARM por meio de um modelo json [Olá especificações de api rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) e procure "disponibilidade".

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Armazenamento: armazenamento do Microsoft Azure e discos de dados
Máquinas Virtuais do Microsoft Azure utilizam diferentes tipos de armazenamento. Ao implementar aplicativos SAP nos serviços de máquina Virtual do Azure é toounderstand importantes diferenças de saudação entre esses dois tipos principais de armazenamento:

* Armazenamento volátil não persistente.
* Armazenamento persistente.

armazenamento não persistente Olá é diretamente conectado toohello máquinas virtuais em execução e reside em nós de computação Olá próprios – armazenamento de instância local da saudação (armazenamento temporário). tamanho Olá depende de tamanho de saudação do hello Máquina Virtual escolhida na implantação Olá iniciada. Esse tipo de armazenamento é volátil e, portanto, o disco de saudação é inicializado quando uma instância de máquina Virtual for reiniciada. Normalmente, a saudação de arquivo de paginação para o sistema operacional de saudação está localizado nesse disco temporário.

- - -
> ![Windows][Logo_Windows] Windows
>
> Em máquinas virtuais do Windows unidade temporária hello está montada como a unidade D:\ em uma VM implantada.
>
> ![Linux][Logo_Linux] Linux
>
> Em VMs Linux, ela está montada como /mnt/resource ou /mnt. Veja mais detalhes aqui:
>
> * [Como tooAttach tooa um disco de dados Máquina Virtual do Linux][virtual-machines-linux-how-to-attach-disk]
> * <http://blogs.msdn.com/b/mast/archive/2013/12/07/understanding-the-temporary-drive-on-windows-azure-virtual-machines.aspx>
>
>

- - -
unidade real Olá é volátil porque ela é armazenada no próprio servidor de host hello. Se Olá VM movida em uma reimplantação (por exemplo, data de conclusão toomaintenance no host de saudação ou desligamento e reinicialização) conteúdo Olá unidade Olá é perdido. Portanto, não é uma opção toostore dados importantes nessa unidade. tipo de saudação de mídia usado para esse tipo de armazenamento difere entre séries de VMs diferentes com características de desempenho muito diferentes que se parecem com a partir de junho de 2015:

* A5-A7: desempenho muito limitado. Não recomendado para nada além do arquivo de paginação
* A8-A11: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s.
* Série D: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s.
* Série DS: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s.
* Série G: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s.
* Série GS: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s.

Instruções acima estiver aplicando os tipos de VM toohello certificados com o SAP. Olá séries de VMs com excelente IOPS e taxa de transferência se qualificam para aproveitar alguns recursos do DBMS. Consulte Olá [guia de implantação de DBMS] [ dbms-guide] para obter mais detalhes.

Armazenamento do Microsoft Azure fornece persistente armazenamento e hello típicos níveis de proteção e redundância no armazenamento SAN. Discos de armazenamento do Azure são discos rígidos virtuais (VHDs) localizados nos serviços de armazenamento do Azure hello. Olá local de disco do sistema operacional (c: do Windows\, Linux / (dev/sda1)) é armazenado no hello armazenamento do Azure e Volumes/discos adicionais montado toohello VM obter armazenadas lá, muito.

É possível tooupload um VHD existente do local ou criar novos vazios no Azure e anexar essas VMs toodeployed. Esses VHDs são referenciados como Discos do Azure.

Depois de criar ou carregar um VHD no armazenamento do Azure, é possível toomount e anexar os tooan Máquina Virtual e toocopy existentes (desmontado) VHD existentes.

Como esses VHDs são persistentes, os dados e alterações presentes em tais VHDs são preservados ao reinicializar e recriar uma instância de Máquina Virtual. Mesmo que uma instância for excluída, esses VHDs e manter a seguros podem ser reimplantados ou no caso de discos de SO não podem ser montado tooother VMs.

Olá dentro de rede de níveis diferentes de redundância de armazenamento do Azure pode ser configurada:

* Nível mínimo que pode ser selecionado é 'local redundância', que é o equivalente toothree-réplica dos dados de saudação em Olá mesmo data center de uma região do Azure (consulte o capítulo [regiões do Azure][planning-guide-3.1]).
* Armazenamento com redundância de zona que espalhados data centers diferentes dentro da imagens Olá três Olá mesma região do Azure.
* Nível de redundância do padrão é a redundância geográfica que replica de forma assíncrona o conteúdo de saudação em outro imagens 3 dos dados de saudação em outra região do Azure que está hospedado no hello mesma região geopolíticas.

Consulte também a tabela de saudação na parte superior deste artigo nas opções de redundância diferentes toohello que diz respeito: <https://azure.microsoft.com/pricing/details/storage/>

Mais informações no que diz respeito tooAzure que armazenamento pode ser encontrado aqui:

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Armazenamento Standard do Azure
Armazenamento de BLOB padrão do Azure era o tipo de saudação do armazenamento disponível quando o IaaS do Azure foi lançado. Havia cotas IOPS impostas para cada VHD. Latência apresentou não estava no hello mesma classe como dispositivos de SAN/NAS normalmente implantados para sistemas SAP avançados hospedado no local. No entanto, Olá armazenamento padrão do Azure tornava suficiente para muitas centenas sistemas SAP enquanto isso implantado no Azure.

Padrão de armazenamento do Azure é cobrado com base em Olá dados reais que são armazenados, volume de saudação de transações de armazenamento, transferências de dados de saída e a opção de redundância escolhido. Número de VHDs pode ser criado no hello máximo 1 TB de tamanho, mas como aquelas permanecerem em branco não são cobrados. Se você preencher, em seguida, um VHD com 100GB, você será cobrado para armazenar 100GB e não para Olá Olá de tamanho nominal com que VHD foi criado.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Armazenamento Premium do Azure
Em abril de 2015, a Microsoft introduziu o Armazenamento Premium do Azure. Armazenamento Premium foi introduzido com hello meta tooprovide:

* Melhor latência de E/S.
* Melhor taxa de transferência.
* Menos variação na latência de E/S.

Para essa finalidade, muitas alterações foram introduzidas de quais hello dois principais são:

* Uso de discos SSD em nós de armazenamento do Azure Olá
* Um novo cache de leitura que é apoiado por Olá SSD local de um nó de computação do Azure

Em oposta tooStandard armazenamento onde os recursos não foram alterados depende do tamanho de saudação do disco de saudação (ou VHD), armazenamento Premium atualmente tem 3 categorias diferentes de disco que são mostradas no final da saudação deste artigo antes da seção Olá perguntas Frequentes: <https:/ /Azure.microsoft.com/Pricing/Details/Storage/>

Você ver que a taxa de transferência/VHD IOPS/VHD e disco são dependentes na categoria de tamanho de saudação de discos Olá

Custo base no caso de saudação de armazenamento Premium não é um volume de dados reais Olá armazenado em tal VHDs, mas a categoria de tamanho de saudação de tal um VHD, independentemente da quantidade de saudação de dados de saudação que são armazenados em Olá VHD.

Você também pode criar os VHDs no armazenamento Premium que não esteja mapeando diretamente em categorias de tamanho de saudação mostradas. Isso pode ser o caso de Olá, especialmente quando copiar VHDs de armazenamento padrão em armazenamento Premium. Nesses casos, uma mapeamento toohello próximo maior armazenamento Premium disco opção é executada.

Esteja ciente de que somente determinado série VM pode se beneficiar de saudação armazenamento Premium do Azure. A partir de dezembro de 2015, esses são hello e GS-série DS. Olá série DS é basicamente Olá mesmo como D-series, com exceção de saudação da série DS tem capacidade de saudação toomount armazenamento Premium baseados em VMs Além disso tooVHDs que são hospedadas no armazenamento padrão do Azure. Mesmo é válido para a série G-series comparados tooGS.

Se você check-out parte Olá Olá série DS de VMs em [neste artigo] [ virtual-machines-sizes] você também vai perceber que há limitações de volume de dados tooPremium armazenamento VHDs na granularidade de saudação do nível VM hello. Diferente de série DS ou série GS VMs também tem limitações diferentes no que diz respeito toohello número de VHDs que podem ser montados. Esses limites estão documentados no artigo Olá mencionado acima, bem como. Mas, em essência, isso significa que se, por exemplo, montar 32 tooa de discos/VHDs x P30 única VM DS14 você não é possível obter 32 x taxa de transferência máxima de um disco P30 hello. Em vez disso, hello taxa de transferência máxima no nível da VM conforme documentado no artigo Olá limitará a taxa de transferência de dados.

Mais informações sobre o Armazenamento Premium podem ser encontradas aqui: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="azure-storage-accounts"></a>Contas de Armazenamento do Azure
Ao implantar serviços ou VMs no Azure, a implantação de VHDs e Imagens de VM deve ser organizada em unidades chamadas Contas de Armazenamento do Azure. Ao planejar uma implantação do Azure, você precisa toocarefully considere Olá restrições do Azure. Em um lado de saudação, há um número limitado de contas de armazenamento por assinatura do Azure. Embora cada conta de armazenamento do Azure pode conter um grande número de arquivos VHD, há um limite fixo no hello total de IOPS por conta de armazenamento. Ao implantar centenas de VMs SAP com sistemas DBMS criar chamadas de e/s significativas, é recomendável toodistribute alta VMs de DBMS IOPS entre várias contas de armazenamento do Azure. Tome cuidado não tooexceed Olá limite atual de contas de armazenamento do Azure por assinatura. Como o armazenamento é uma parte essencial da implantação de banco de dados de saudação para um sistema SAP, esse conceito é abordado em mais detalhes em Olá já referenciado [guia de implantação de DBMS][dbms-guide].

Mais informações sobre as Contas de Armazenamento do Azure podem ser encontradas [neste artigo][storage-scalability-targets]. Lendo este artigo, você vai perceber que há diferenças nas limitações de saudação entre contas de armazenamento padrão do Azure e contas de armazenamento Premium. Principais diferenças são volume Olá de dados que podem ser armazenados em tal uma conta de armazenamento. No armazenamento padrão volume Olá é uma magnitude maior do que com o armazenamento Premium. Em Olá Olá outros lado conta de armazenamento padrão severos é limitado em IOPS (consulte a coluna 'Taxa Total de solicitação'), enquanto o hello conta de armazenamento do Azure Premium tem essa limitação não. Vamos discutir detalhes e os resultados dessas diferenças ao discutir as implantações de saudação de sistemas SAP, especialmente servidores DBMS hello.

Em uma conta de armazenamento, você tem Olá possibilidade toocreate diferentes contêineres para finalidade de saudação de organizar e classificando diferentes VHDs. Esses contêineres são tooe.g geralmente usados. Separe os VHDs de máquinas virtuais diferentes. Não há nenhuma implicação de desempenho em usar apenas um contêiner ou vários contêineres sob uma única Conta de Armazenamento do Azure.

No Azure um nome VHD segue Olá após a conexão de nomenclatura que precisa tooprovide um nome exclusivo para Olá VHD no Azure:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Como cadeia de caracteres de saudação mencionados acima, precisa toouniquely identificar Olá VHD é armazenado no armazenamento do Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Rede do Microsoft Azure
Microsoft Azure oferecerá uma infraestrutura de rede que permite o mapeamento de saudação de todos os cenários que desejarmos toorealize com o software SAP. Olá recursos estão:

* Acesso de saudação fora diretamente toohello máquinas virtuais por meio de serviços de Terminal do Windows ou o ssh/VNC
* Acesso tooservices e usadas por aplicativos nas VMs da saudação de portas específicas
* Comunicação interna e resolução de nomes entre um grupo de VMs implantadas como VMs do Azure
* Conectividade entre locais entre a rede local e rede Azure de saudação do cliente
* Conectividade entre Regiões do Azure ou data centers entre sites do Azure

Mais informações podem ser encontradas aqui: <https://azure.microsoft.com/documentation/services/virtual-network/>

Há muitos de nome de tooconfigure possibilidades diferentes e a resolução IP no Azure. Neste documento, somente em nuvem cenários dependem do padrão de saudação do uso de DNS do Azure (em contraste toodefining um serviço DNS próprio). Também há um novo serviço DNS do Azure que pode ser usado, em vez de configurar seu próprio servidor DNS. Encontre mais informações [neste artigo][virtual-networks-manage-dns-in-vnet] e [nesta página](https://azure.microsoft.com/services/dns/).

Para cenários entre locais, contamos fatos Olá que Olá local OpenLDAP/AD/DNS foi estendido por meio de VPN ou conexão privada tooAzure. Para determinados cenários, conforme documentado aqui, talvez seja necessário toohave uma réplica do AD/OpenLDAP instalada no Azure.

Como a rede e resolução de nome é uma parte essencial da implantação de banco de dados de saudação para um sistema SAP, esse conceito é abordado em mais detalhes em Olá [guia de implantação de DBMS][dbms-guide].

##### <a name="azure-virtual-networks"></a>Redes Virtuais do Azure
Ao criar uma rede Virtual do Azure, você pode definir o intervalo de endereços de saudação do hello endereços IP alocados pela funcionalidade DHCP do Azure. Em cenários entre locais, intervalo de endereços IP hello definido ainda será alocado usando DHCP pelo Azure. No entanto, a resolução de nome de domínio será feita no local (supondo que Olá VMs são uma parte de um domínio local) e, portanto, pode resolver endereços além diferentes serviços de nuvem do Azure.

[comment]: <> (O MSSedusch ainda é necessário? TODO originalmente para uma rede Virtual do Azure foi associada tooan grupo de afinidade. Com que uma rede Virtual no Azure tem restrito toohello unidade de escala do Azure que Olá que grupo de afinidade foi atribuído. No final do hello, essa rede Virtual de saudação meant foi toohello restrito recursos disponíveis no hello unidade de escala do Azure. Isso mudou desde então, e agora as redes virtuais do Azure podem ampliar-se por mais de uma unidade de escala do Azure. No entanto, isso exige que as Redes Virtuais do Azure **NÃO** estejam mais associadas aos Grupos de Afinidade no momento da criação. Já mencionamos anteriormente que no toorecommendations oposta um ano atrás, você deve * * não aproveitam os grupos de afinidade do Azure mais * *. Para obter detalhes, confira <https://azure.microsoft.com/blog/regional-virtual-networks/>)

Cada máquina Virtual no Azure necessidades toobe conectado tooa rede Virtual.

Mais detalhes podem ser encontrados [neste artigo][resource-groups-networking] e [nesta página](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd TODO não foi possível encontrar um artigo que inclui o tópico de OpenLDAP Olá + ARM;)
[comment]: <> (MSSedusch <https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Por padrão, quando uma VM é implantada, não é possível alterar configuração da rede Virtual hello. configurações de TCP/IP Hello devem ser deixadas toohello servidor de DHCP do Azure. O comportamento padrão é a atribuição de IP dinâmico.
>
>

endereço MAC de saudação da placa de rede virtual de saudação pode alterar, por exemplo, depois de redimensionar e hello Windows ou o sistema operacional de convidado do Linux assumirão a nova placa de rede hello e automaticamente usará o DHCP tooassign endereços IP e DNS do hello nesse caso.

##### <a name="static-ip-assignment"></a>Atribuição de endereço IP estático
É possível tooassign fixada ou tooVMs em uma rede Virtual do Azure de endereços IP reservados. VMs de saudação em execução em uma rede Virtual do Azure abre uma ótima possibilidade tooleverage essa funcionalidade se necessário ou alguns cenários. atribuição de IP Hello permanece válida durante toda a existência de saudação do hello VM, independentemente de se Olá VM está em execução ou desligamento. Como resultado, você precisa tootake Olá número total de VMs (máquinas virtuais em execução e interrompidas) em consideração ao definir Olá intervalo de endereços IP para rede Virtual de saudação. endereço IP Hello permanece atribuído até que seja excluída hello VM e sua Interface de rede ou até que o endereço IP hello desatribuído novamente. Veja informações detalhadas [neste artigo][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Várias NICs por VM
Você pode definir várias vNICs (placas de interface de rede virtual) para uma Máquina Virtual do Azure. Com hello capacidade toohave vNICs vários você pode iniciar tooset a separação do tráfego de rede em que, por exemplo, o tráfego de cliente é roteado por um vNIC e tráfego de back-end é roteado por uma segundo vNIC. Dependente do tipo de saudação da VM que existem limitações diferentes em considera toohello inúmeros vNICs. Restrições, funcionalidades e detalhes exatos podem ser encontradas nesses artigos:

* [Criar uma VM com diversas NICs][virtual-networks-multiple-nics]
* [Implantar VMs com diversas NICs usando um modelo][virtual-network-deploy-multinic-arm-template]
* [Implantar VMs com diversas NICs usando o PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Implantar várias VMs de NIC usando Olá CLI do Azure][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Conectividade site a site
entre instalações refere-se a VMs do Azure e locais vinculadas por uma conexão VPN permanente e transparente. É esperado toobecome hello mais comuns padrão de implantação SAP no Azure. Olá pressupõe-se que os procedimentos operacionais e processos com instâncias SAP no Azure funcionem de forma transparente. Isso significa que você deve ser capaz de tooprint partir desses sistemas, bem como usar Olá tootransport do sistema de gerenciamento de transporte SAP (TMS) muda de um sistema de desenvolvimento no sistema de teste de tooa do Azure que é implantado no local. Encontre mais documentações relacionadas ao site a site [neste artigo][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Dispositivo de túnel VPN
Em ordem toocreate uma conexão site a site (no data center tooAzure data center local), você precisará tooeither obter e configurar um dispositivo VPN ou usar o roteamento e acesso remoto (RRAS) que foi introduzida como um componente de software com o Windows Server 2012.

* [Criar uma rede virtual com uma conexão VPN site a site usando PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [Sobre dispositivos VPN para conexões de Gateway de VPN Site a Site][vpn-gateway-about-vpn-devices]
* [Perguntas frequentes sobre o Gateway de VPN][vpn-gateway-vpn-faq]

![Conexão site a site entre locais e o Azure][planning-guide-figure-600]

Olá figura acima mostra duas assinaturas do Azure têm subintervalos de endereços IP reservados para uso em redes virtuais no Azure. conectividade de saudação do hello local tooAzure de rede é estabelecida via VPN.

#### <a name="point-to-site-vpn"></a>VPN ponto a site
VPN ponto a site requer que cada tooconnect de máquina do cliente com seu próprio VPN no Azure. Para cenários SAP Olá que vemos, conectividade ponto a site não é prática. Portanto, nenhuma outra referência terá conectividade de VPN site a toopoint.

[comment]: <> (MSSedusch – mais informações podem ser encontradas aqui)
[comment]: <> (MShermannd TODO: o link não é mais válido, mas, mesmo assim, o ARM não tem suporte – veja o próximo link abaixo)
[comment]: <> (MSSedusch – <http://msdn.microsoft.com/library/azure/dn133798.aspx>.)
[comment]: <> (TooSite MShermannd TODO ponto ainda não tem suportada com ARM)
[comment]: <> (MSSedusch – <https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/>)

#### <a name="multi-site-vpn"></a>VPN de múltiplos sites
O Azure também atualmente oferece conectividade de VPN de multissite do hello possibilidade toocreate para uma assinatura do Azure. Anteriormente, uma única assinatura foi conexão de VPN site a site tooone limitado. Essa limitação desapareceu com ligações VPN de múltiplos sites para uma única assinatura. Isso torna possível tooleverage mais de uma região do Azure para uma assinatura específica por meio de configurações entre locais.

Para obter mais documentação, veja [este artigo][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO: nenhum link de documentação do ARM encontrado)

#### <a name="vnet-toovnet-connection"></a>Rede virtual tooVNet Conexão
Usando VPN de multissite, você precisa tooconfigure uma rede Virtual do Azure separada em cada uma das regiões de saudação. No entanto, muito frequentemente, você tem o requisito de Olá que componentes de software Olá em regiões diferentes Olá devem se comunicar entre si. Idealmente essa comunicação deve ser roteada não de uma região do Azure tooon local e de lá toohello outra região do Azure. tooshortcut, o Azure oferece a saudação possibilidade tooconfigure uma conexão de uma rede Virtual do Azure no tooanother de região uma que rede Virtual do Azure hospedada em outra região. Essa funcionalidade é chamada de conexão de VNet a VNet. Mais detalhes sobre essa funcionalidade podem ser encontrados aqui: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>TooAzure de Conexão privada – rota expressa
O Microsoft Azure ExpressRoute permite a criação de saudação de conexões privadas entre data centers do Azure e infraestrutura de local do cliente ou hello, ou em um ambiente de colocalização. O ExpressRoute é oferecido por diversos provedores VPN MPLS (com pacotes comutados) ou outros Provedores de Serviços de Rede. Conexões de rota expressa não passam pela Olá Internet pública. Conexões de rota expressa oferecem maior segurança, mais confiabilidade através de vários circuitos paralelos, velocidades mais rápidas e latências menores que as conexões típicas Olá da Internet.

Encontre mais detalhes sobre a Azure ExpressRoute e ofertas aqui:

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

O ExpressRoute permite várias assinaturas do Azure por meio de um circuito de ExpressRoute, conforme documentado aqui

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Túnel forçado em caso de instalações cruzadas
Para ingressar em domínios locais através de site a site, ponto a site ou rota expressa de VMs, você precisa toomake-se de que as configurações de proxy de Internet Olá são implantadas para todos os usuários de saudação nessas VMs também. Por padrão, o software em execução nessas VMs ou usuários usando uma saudação de tooaccess navegador internet não passariam pelo proxy de empresa hello, mas deve se conectar diretamente por meio do Azure toohello internet. Mas a configuração do proxy Olá mesmo não é um solução 100% toodirect Olá o tráfego por meio do proxy de empresa Olá, pois é responsabilidade do toocheck softwares e serviços de proxy de saudação. Se o software em execução no hello VM não fizer isso ou um administrador manipular as configurações de hello, toohello de tráfego da Internet pode ser novamente desviado diretamente através do Azure toohello da Internet.

Em ordem tooavoid isso, você pode configurar o túnel forçado com conectividade site a site entre locais e o Azure. Olá descrição detalhada do recurso de túnel forçado Olá é publicada aqui <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Encapsulamento forçado com o ExpressRoute é habilitado por clientes anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento.

#### <a name="summary-of-azure-networking"></a>Resumo da Rede do Azure
Este capítulo continha muitos pontos importantes sobre a Rede do Azure. Aqui está um resumo dos pontos principais hello:

* Redes virtuais do Azure permite tooset rede Olá de acordo com tooyour próprias necessidades
* Redes virtuais do Azure pode ser utilizado tooassign tooVMs de intervalos de endereço IP ou atribuir tooVMs de endereços IP fixos
* tooset uma conexão ponto a Site é necessário toocreate uma rede Virtual do Azure pela primeira vez ou um Site a Site
* Quando uma máquina virtual tiver sido implantada não é mais possível toochange Olá que rede Virtual atribuída toohello VM

### <a name="quotas-in-azure-virtual-machine-services"></a>Cotas nos Serviços da Máquina Virtual do Azure
É necessário toobe limpar sobre fatos Olá que o armazenamento hello e infraestrutura de rede é compartilhada entre VMs que executam uma variedade de serviços em Olá infraestrutura do Azure. E assim como Olá centros de dados do cliente, o excesso de provisionamento de alguns dos recursos de infraestrutura Olá local tooa grau. Olá plataforma Microsoft Azure usa o disco, CPU, rede e consumo de recursos cotas toolimit hello e desempenho consistente e previsível de toopreserve.  Olá diferentes tipos de VM (A5, A6 etc.) tem cotas específicas para o número de saudação de discos, CPU, RAM e rede.

> [!NOTE]
> Recursos de CPU e memória dos tipos de VM Olá suportados pelo SAP são pré-alocados em nós de host hello. Isso significa que, quando Olá VM é implantada, recursos de saudação no host de saudação estarão disponíveis conforme definido pelo Olá tipo de VM.
>
>

Deve ser considerado ao planejar e dimensionar implantações SAP nas soluções do Azure Olá cotas para cada tamanho de máquina virtual.  cotas VM Olá descritas [aqui][virtual-machines-sizes].

cotas de saudação descritas representam valores máximos teóricos de saudação.  limite de saudação de IOPS por VHD pode ser obtida com o IOs pequenos (8kb), mas possivelmente não pode ser obtida com o IOs grandes (1Mb).  limite IOPS de saudação é aplicado na granularidade de saudação do VHD individual.

Como um toodecide da árvore de decisão complexa se um sistema SAP se adapta a seus recursos e serviços de máquina Virtual do Azure ou se um sistema existente precisa toobe configurado de forma diferente no sistema de saudação toodeploy pedidos no Azure, abaixo da árvore de decisão de saudação pode ser usada:

![Decisão árvore toodecide capacidade toodeploy SAP no Azure][planning-guide-figure-700]

**Etapa 1**: Olá toostart de informações mais importante com é o requisito de SAPS Olá para um determinado sistema SAP. Olá SAPS requisitos necessidade toobe separado em parte do DBMS hello e parte do aplicativo SAP hello, mesmo que Olá sistema SAP já esteja implantado localmente em uma configuração de camada 2. Para sistemas existentes, Olá SAPS relacionado toohello hardware em uso geralmente pode ser determinado ou estimado com base em parâmetros de comparação SAP existentes. resultados de saudação podem ser encontrados aqui: <http://global.sap.com/campaigns/benchmark/index.epx>.
Para sistemas SAP recém-implantados, você deverá ter feito um exercício de dimensionamento que deve determinar os requisitos de SAPS de saudação do sistema hello.
Confira também o blog e o documento anexado para dimensionamento do SAP no Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Etapa 2**: para sistemas existentes, Olá volume de e/s e operações de e/s por segundo no servidor DBMS Olá devem ser medidas. Para sistemas novos planejados, Olá dimensionamento exercício para o novo sistema de saudação também deve dar uma ideia geral dos requisitos de e/s de saudação em Olá parte do DBMS. Se não tiver certeza, você precisa eventualmente tooconduct uma prova de conceito.

**Etapa 3**: comparar requisito de SAPS Olá para Olá servidor DBMS com hello SAPS Olá diferentes tipos de VM do Azure pode fornecer. informações de saudação no SAPS dos diferentes tipos de VM do Azure Olá estão documentadas na nota da SAP [1928533]. foco de Olá deve ser primeiro na VM do DBMS de saudação como camada de banco de dados de saudação é camada Olá em um sistema SAP NetWeaver que não se escala horizontalmente na maioria de saudação de implantações. Por outro lado, camada do aplicativo SAP Olá pode ser expandida. Se nenhum Olá SAP suporte tipos de VM do Azure podem oferecer SAPS Olá necessários, carga de trabalho de saudação do sistema do SAP Olá planejado não pode ser executada no Azure. É necessário toodeploy Olá sistema local ou precisar de volume de carga de trabalho do toochange Olá para sistema hello.

**Etapa 4**: conforme documentado [aqui][virtual-machines-sizes], o Azure impõe uma cota de IOPS por VHD independentemente de você usar o Armazenamento Standard ou o Armazenamento Premium. Dependente de saudação tipo de VM, Olá número de VHDs que podem ser montados varia. Como resultado, você pode calcular um número IOPS máximo que pode ser alcançado com cada um dos diferentes tipos de VM hello. Dependente de layout de arquivo de banco de dados hello, você pode distribuir VHDs toobecome um volume no sistema operacional convidado de saudação. No entanto, se volume Olá de IOPS atual de um sistema SAP implantado excede os limites de saudação calculado Olá maior do tipo de VM do Azure e se não há nenhum toocompensate chance com mais memória, carga de trabalho de saudação do hello sistema SAP poderá ser gravemente afetada. Nesses casos, você pode atingir um ponto em que você não deve implantar o sistema Olá no Azure.

**Etapa 5**: especialmente no SAP sistemas implantados localmente em configurações da camada 2, a probabilidade de saudação é que o sistema Olá talvez precise toobe configurado no Azure em uma configuração de camada 3. Nesta etapa, você precisa toocheck se há um componente na camada de aplicativo do hello SAP que não pode ser expandido e que não se ajusta a saudação da CPU e memória recursos Olá oferta diferente de tipos de VM do Azure. Se não existir de fato um componente, sistema do SAP hello e sua carga de trabalho não podem ser implantados no Azure. Mas se você pode expansão Olá aplicativo SAP componentes em várias VMs do Azure, sistema Olá podem ser implantados no Azure.

**Etapa 6**: se hello DBMS e componentes de camada de aplicativo SAP podem ser executados em máquinas virtuais do Azure, a configuração de saudação deve toobe definida em relação ao:

* Número de VMs do Azure
* Tipos de VM para componentes individuais Olá
* Número de VHDs na VM do DBMS tooprovide IOPS suficientes

## <a name="managing-azure-assets"></a>Gerenciando Ativos do Azure
### <a name="azure-portal"></a>Portal do Azure
Olá Portal do Azure é uma das três interfaces toomanage VM do Azure implantações. tarefas básicas de gerenciamento de saudação, como implantar VMs a partir de imagens, podem ser feitas por meio de saudação Portal do Azure. Além disso, a criação de saudação de contas de armazenamento, redes virtuais e outros componentes do Azure também são Olá tarefas Portal do Azure pode tratar muito bem. No entanto, funcionalidades como carregar VHDs do local tooAzure ou copiando um VHD no Azure são tarefas que exigem ferramentas de terceiros ou administração através do PowerShell ou CLI.

![Portal do Microsoft Azure - visão geral de máquina virtual][planning-guide-figure-800]

[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Tarefas de administração e configuração para a instância de máquina Virtual de saudação são possíveis em Olá Portal do Azure.

Além de reiniciar e desligar uma máquina Virtual também pode anexar, desanexar e discos de dados para a instância de máquina Virtual hello, instância de saudação toocapture para preparação de imagem de criar e configurar o tamanho de saudação da instância de máquina Virtual de saudação.

Olá Portal do Azure fornece a funcionalidade básica toodeploy e configurar VMs e muitos outros serviços do Azure. No entanto não todas as funcionalidades disponíveis é coberta por Olá Portal do Azure. Olá Portal do Azure, não é possível tooperform tarefas como:

* Carregando VHDs tooAzure
* Copiar VMs

[comment]: <> (MShermannd TODO: e o serviço de automação para as VMs SAP? )
[comment]: <> (MSSedusch: implantação de vários SOs de VMs ao mesmo tempo possível)
[comment]: <> (Também MSSedusch qualquer tipo de automação em relação a implantação não é possível com hello portal do Azure. Tarefas como implantação de scripts de várias VMs não é possível por meio de saudação Portal do Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Gerenciamento via cmdlets do Microsoft Azure PowerShell
O Windows PowerShell é uma estrutura poderosa e extensível que foi amplamente adotada por clientes implantando grandes quantidades de sistemas no Azure. Após a instalação de saudação de cmdlets do PowerShell em um desktop, laptop ou estação de gerenciamento dedicada, Olá cmdlets do PowerShell pode ser executado remotamente.

Olá processo tooenable um computador desktop/laptop local para o uso de saudação de cmdlets do PowerShell do Azure e como tooconfigure de Olá uso com hello Azure assinaturas são descrita em [neste artigo][powershell-install-configure].

Etapas mais detalhadas sobre como tooinstall, atualizar e configurar os cmdlets do PowerShell do Azure Olá também podem ser encontradas em [neste capítulo de guia de implantação do hello][deployment-guide-4.1].

Experiência do cliente até o momento foi PowerShell (PS) é certamente hello mais poderosa ferramenta toodeploy VMs e as etapas de toocreate personalizado na implantação de saudação de VMs. Todos os clientes de saudação que executam instâncias SAP no Azure são usando PS cmdlets toosupplement tarefas de gerenciamento que eles em Olá Portal do Azure ou até mesmo estiver usando cmdlets do PS exclusivamente toomanage suas implantações no Azure. Como o compartilhamento de cmdlets específicos do Azure Olá hello mesma convenção de nomenclatura hello mais de 2000 cmdlets relacionados do Windows, é uma forma fácil de tarefas para Windows administradores tooleverage esses cmdlets.

Confira o exemplo aqui: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO: descrever o novo comando da CLI quando testado )
Implantação de saudação extensão de monitoramento do Azure para SAP (consulte o capítulo [solução de monitoramento do Azure para SAP] [ planning-guide-9.1] neste documento) só é possível por meio do PowerShell ou CLI. Portanto, é obrigatório toosetup e configurar o PowerShell ou CLI ao implantar ou administrar um sistema SAP NetWeaver no Azure.  

Como o Azure oferece mais funcionalidade, novos cmdlets do PS vai toobe adicionado requer uma atualização dos cmdlets de saudação. Ele torna saudação do sentido toocheck site de Download do Azure pelo menos uma vez por mês de saudação <https://azure.microsoft.com/downloads/> para uma nova versão de hello cmdlets. nova versão de Hello apenas será instalado na parte superior da versão mais antiga do hello.

Para ver uma lista geral dos comandos do PowerShell relacionados ao Azure, verifique aqui: <https://msdn.microsoft.com/library/azure/dn708514.aspx>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Gerenciamento por meio de comandos da CLI do Microsoft Azure
Para clientes que usam o Linux e deseja toomanage Azure recursos do Powershell não podem ser uma opção. Como alternativa, a Microsoft oferece a CLI do Azure.
Olá CLI do Azure fornece um conjunto de software livre, multiplataforma comandos para trabalhar com hello plataforma Azure. Olá CLI do Azure fornece grande parte da mesma funcionalidade encontrada no portal do Azure de saudação do hello.

Para obter informações sobre instalação, configuração e como os comandos tooaccomplish toouse CLI tarefas do Azure, consulte

* [Instalar Olá CLI do Azure][xplat-cli]
* [Implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e hello CLI do Azure][virtual-machines-linux-cli-deploy-templates]
* [Use Olá CLI do Azure para Mac, Linux e Windows com o Gerenciador de recursos do Azure][xplat-cli-azure-resource-manager]

Leia também o capítulo [CLI do Azure para VMs do Linux] [ deployment-guide-4.5.2] em Olá [guia de implantação] [ planning-guide] em como toouse CLI do Azure toodeploy hello Azure Extensão de monitoramento para SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Diferentes maneiras toodeploy VMs para SAP no Azure
Neste capítulo, você aprenderá diferentes maneiras de saudação toodeploy uma VM no Azure. Procedimentos adicionais de preparação, bem como a manipulação de VHDs e VMs no Azure, são abordados neste capítulo.

### <a name="deployment-of-vms-for-sap"></a>Implantação de VMs para SAP
Microsoft Azure oferece várias maneiras toodeploy VMs e discos associados. Assim é muito importante toounderstand diferenças de saudação pois os preparativos das VMs de saudação podem diferir dependendo do método de saudação da implantação. Em geral, obtemos uma olhada Olá os seguintes cenários:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Mover uma VM do tooAzure local com um disco não generalizado
Planejar toomove um sistema SAP específico de tooAzure local. Isso pode ser feito Carregando Olá VHD que contém Olá SO, Olá Olá VHDs com dados saudação além de binários de DBMS e SAP binários e arquivos de log de saudação DBMS tooAzure. Em contraste muito[cenário #2 abaixo][planning-guide-5.1.2], lembre-Olá hostname, o SID do SAP e contas de usuário SAP Olá VM do Azure, como eles foram configurados no ambiente local de saudação. Portanto, não é necessário generalizar a imagem de saudação. Consulte capítulos [preparação para mover uma VM do tooAzure local com um disco não generalizado] [ planning-guide-5.2.1] deste documento para etapas de preparação de local e o carregamento de VMs não generalizado ou VHDs tooAzure. Leia o capítulo [cenário 3: mover uma VM do local usando um VHD do Azure não generalizado com o SAP] [ deployment-guide-3.4] em Olá [guia de implantação] [ deployment-guide]para obter etapas detalhadas de implantação dessa imagem no Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Implantando uma VM com uma imagem específica do cliente
Devido a requisitos de patch toospecific da sua versão de SO ou DBMS, imagens de saudação fornecida em hello Azure Marketplace podem não atender às suas necessidades. Portanto, talvez seja necessário toocreate uma VM usando sua própria imagem de VM do SO/DBMS 'private', que pode ser implantada várias vezes depois. tooprepare uma imagem 'private' para eliminação de duplicação, Olá itens a seguir têm toobe considerado:


[comment]: <> (MSSedusch > Veja mais detalhes aqui: )
[comment]: <> (MShermannd TODO: o primeiro link é sobre o modelo clássico. Não localizei um artigo de documentação do Azure)
[comment]: <> (MSSedusch > <https://azure.microsoft.com/documentation/articles/virtual-machines-create-upload-vhd-windows-server/>)
[comment]: <> (MSSedusch > <http://blogs.technet.com/b/blainbar/archive/2014/09/12/modernizing-your-infrastructure-with-hybrid-cloud-using-custom-vm-images-and-resource-groups-in-microsoft-azure-part-21-blain-barton.aspx>)
- - -
> ![Windows][Logo_Windows] Windows
>
> Olá Windows configurações (como o SID do Windows e o nome de host) devem ser abstraídas/generalizadas Olá local VM por meio de comando do sysprep hello.
>
>
> ![Linux][Logo_Linux] Linux
>
> Siga etapas Olá descritas nesses artigos para [SUSE] [ virtual-machines-linux-create-upload-vhd-suse] ou [Red Hat] [ virtual-machines-linux-redhat-create-upload-vhd] tooprepare toobe um VHD carregado tooAzure.
>
>

- - -
Se você já tiver instalado conteúdo SAP em sua VM local (especialmente para sistemas de camada 2), você pode adaptar configurações do sistema SAP Olá depois de implantação de saudação do hello VM do Azure por meio da instância de saudação renomear procedimento Olá provisionamento de Software SAP com suporte Manager (nota da SAP [1619720]). Consulte capítulos [preparação para implantar uma VM com uma imagem específica do cliente para SAP] [ planning-guide-5.2.2] e [carregando um VHD do local tooAzure] [ planning-guide-5.3.2]deste documento para etapas de preparação de local e o carregamento de um tooAzure VM generalizado. Leia o capítulo [cenário 2: Implantando uma VM com uma imagem personalizada para SAP] [ deployment-guide-3.3] em Olá [guia de implantação] [ deployment-guide] para obter etapas detalhadas de implantar tal imagem no Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Implantando uma VM hello Azure Marketplace
Você gostaria que toouse Microsoft ou 3ª parte sua VM de imagem VM do hello Azure Marketplace toodeploy fornecida. Depois de implantar a VM no Azure, você seguir Olá mesmas diretrizes e ferramentas tooinstall Olá software SAP e/ou DBMS na VM como você faria em um ambiente local. Para obter descrição de implantação mais detalhadas, consulte o capítulo [cenário 1: Implantando uma VM hello Azure Marketplace para SAP] [ deployment-guide-3.2] em Olá [guia de implantação] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Preparando VMs com SAP para o Azure
Antes de carregar VMs no Azure, você precisa toomake se Olá VMs e VHDs atenderem a certos requisitos. Há pequenas diferenças dependendo do método de implantação de saudação que é usado.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Preparação para mover uma VM do tooAzure local com um disco não generalizado
Um método de implantação comum é toomove uma VM existente que executa um sistema SAP de tooAzure local. VM e hello sistema SAP em Olá VM apenas deve ser executado no Azure usando Olá o mesmo nome de host e muito provavelmente Olá mesmo SID do SAP. Nesse caso convidado Olá SO da VM não deve ser generalizado para várias implantações. Se a rede de local de saudação foi estendida para o Azure (consulte o capítulo [entre locais - implantação de uma ou várias VMs SAP no Azure com o requisito de saudação de integração completa à rede do local de saudação] [ planning-guide-2.2] neste documento), até mesmo, em seguida, Olá mesmas contas de domínio podem ser usadas em Olá VM que eram usadas antes de local.

Os requisitos ao preparar seu próprio Disco de VM do Azure são:

* Originalmente Olá VHD contendo sistema operacional Olá pode ter apenas um tamanho máximo de 127GB. Essa limitação foi eliminada no final de saudação de março de 2015. Agora hello VHD que contém o sistema operacional de saudação pode ser o too1TB tamanho como qualquer outro armazenamento do Azure hospedado VHD também.

[comment]: <> (MShermannd TODO ter toocheck se CLI também converte toostatic)
* Ele precisa toobe em Olá formato VHD fixo. VHDs dinâmicos ou VHDs no formato VHDx ainda não têm suporte no Azure. VHDs dinâmicos será convertido toostatic VHDs quando você carregar Olá VHD com cmdlets do PowerShell ou CLI
* VHDs montado toohello VM e devem ser montados novamente no Azure toohello VM necessidade toobe em um formato VHD fixo. Olá mesmo limite de tamanho de disco do sistema operacional Olá aplica toodata discos também. VHDs podem ter um tamanho máximo de 1 TB. VHDs dinâmicos será convertido toostatic VHDs quando você carregar Olá VHD com cmdlets do PowerShell ou CLI
* Adicione outra conta local com privilégios de administrador que pode ser usado pelo suporte da Microsoft ou que possa ser atribuída como contexto para serviços e aplicativos toorun em até Olá que VM é implantada e os usuários mais apropriados pode ser usada.
* Para o caso de saudação do uso de um cenário de implantação somente em nuvem (consulte o capítulo [somente em nuvem - implantações de máquina Virtual no Azure sem dependências nos Olá local rede cliente] [ planning-guide-2.1] deste um documento) em combinação com esse método de implantação, o domínio de contas podem não funcionar depois de saudação do disco do Azure é implantada no Azure. Isso é especialmente verdadeiro para contas que são usadas toorun serviços como o hello DBMS e aplicativos SAP. Portanto, você precisa tooreplace essas contas de domínio com contas locais da VM e excluir contas de domínio local Olá no hello VM. Manter os usuários do domínio local na imagem VM Olá não é um problema quando Olá VM é implantada no cenário de saudação entre locais, conforme descrito no capítulo [entre locais - implantação de uma ou várias VMs SAP no Azure com o requisito de saudação do sendo totalmente integrado à rede de local de saudação] [ planning-guide-2.2] neste documento.
* Se as contas de domínio eram usadas como logons DBMS ou os usuários ao executar Olá sistema local e as VMs devem toobe implantado em cenários de nuvem, os usuários do domínio Olá necessário toobe excluído. É necessário toomake se Olá administrador local e mais outro usuário local da VM é adicionado como um logon/usuário em Olá DBMS como administradores.
* Adicione outras contas locais, como elas podem ser necessárias para o cenário de implantação específico hello.

- - -
> ![Windows][Logo_Windows] Windows
>
> Neste cenário nenhuma generalização (sysprep) do hello VM é tooupload necessário e implantar Olá VM no Azure.
> Verifique se a unidade D:\ não é usada. Defina a montagem automática de disco para discos anexados conforme descrito no capítulo [Definindo a montagem automática para os discos anexados][planning-guide-5.5.3] deste documento.
>
> ![Linux][Logo_Linux] Linux
>
> Neste cenário nenhuma generalização (waagent-desprovisionamento) do hello VM é tooupload necessário e implantar Olá VM no Azure.
> Certifique-se de que /mnt/resource não é usado e que todos os discos são montados por meio de uuid. Para disco Olá sistema operacional, certifique-se de que entrada do carregador de inicialização Olá também reflete montagem com base em uuid de saudação.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Preparação para implantar uma VM com uma imagem específica do cliente para SAP
Os arquivos VHD que contêm um SO generalizado também são armazenados em contêineres nas Contas de Armazenamento do Azure. Você pode implantar uma nova VM de uma imagem VHD referenciando Olá VHD como uma fonte de VHD em seus arquivos de modelo de implantação, conforme descrito no capítulo [cenário 2: Implantando uma VM com uma imagem personalizada para SAP] [ deployment-guide-3.3] de saudação [Guia de implantação][deployment-guide].

Os requisitos ao preparar sua própria Imagem de VM do Azure são:

* Originalmente Olá VHD contendo sistema operacional Olá pode ter apenas um tamanho máximo de 127GB. Essa limitação foi eliminada no final de saudação de março de 2015. Agora hello VHD que contém o sistema operacional de saudação pode ser o too1TB tamanho como qualquer outro armazenamento do Azure hospedado VHD também.

[comment]: <> (MShermannd TODO ter toocheck se CLI também converte toostatic)
* Ele precisa toobe em Olá formato VHD fixo. VHDs dinâmicos ou VHDs no formato VHDx ainda não têm suporte no Azure. VHDs dinâmicos será convertido toostatic VHDs quando você carregar Olá VHD com cmdlets do PowerShell ou CLI
* VHDs montado toohello VM e devem ser montados novamente no Azure toohello VM necessidade toobe em um formato VHD fixo. Olá mesmo limite de tamanho de disco do sistema operacional Olá aplica toodata discos também. VHDs podem ter um tamanho máximo de 1 TB. VHDs dinâmicos será convertido toostatic VHDs quando você carregar Olá VHD com cmdlets do PowerShell ou CLI
* Desde que todos os usuários de domínio registrados como usuários em Olá VM não existirão em um cenário somente em nuvem de hello (consulte o capítulo [somente em nuvem - implantações de máquina Virtual no Azure sem dependências nos Olá local rede cliente] [ planning-guide-2.1] deste documento), os serviços usando esse domínio de contas podem não funcionar depois que Olá imagem é implantada no Azure. Isso é especialmente verdadeiro para contas que são usadas toorun serviços como DBMS e aplicativos SAP. Portanto, você precisa tooreplace essas contas de domínio com contas locais da VM e excluir contas de domínio local Olá no hello VM. Manter os usuários do domínio local na imagem VM Olá pode não ser um problema quando Olá VM é implantada no hello cenário entre locais como descrito no capítulo [entre locais - implantação de uma ou várias VMs SAP no Azure com o requisito de saudação do integração completa à rede do local de saudação] [ planning-guide-2.2] neste documento.
* Adicione outra conta local com privilégios de administrador que pode ser usado pelo suporte da Microsoft na investigação de problemas ou que possa ser atribuída como contexto para serviços e aplicativos toorun em até Olá que VM é implantada e os usuários mais apropriados pode ser usada.
* Em implantações somente em nuvem e onde as contas de domínio eram usadas como logons DBMS ou usuários durante a execução Olá sistema local, os usuários do domínio Olá devem ser excluídos. É necessário toomake se Olá administrador local e mais outro usuário local da VM é adicionado como um logon/usuário do hello DBMS como administradores.
* Adicione outras contas locais, como elas podem ser necessárias para o cenário de implantação específico hello.
* Se imagem Olá contém uma instalação do SAP NetWeaver e renomeação de nome de host de saudação do nome original do hello no ponto de saudação da saudação implantação do Azure for provável, é recomendado toocopy versões mais recentes do Olá Olá SAP Software Provisioning Manager DVD em modelo de saudação. Isso permitirá que você tooeasily use Olá SAP fornecido renomear funcionalidade tooadapt Olá alterado alteração e/ou nome de host Olá SID da saudação sistema SAP na Olá implantado a imagem da VM assim que uma nova cópia é iniciada.

- - -
> ![Windows][Logo_Windows] Windows
>
> Verifique se a unidade D:\ não é usada. Defina a montagem automática de disco para discos anexados conforme descrito no capítulo [Definindo a montagem automática para os discos anexados][planning-guide-5.5.3] deste documento.
>
> ![Linux][Logo_Linux] Linux
>
> Certifique-se de que /mnt/resource não é usado e que todos os discos são montados por meio de uuid. Para Olá OS disco Certifique-se de entrada do carregador de inicialização Olá também reflete montagem com base em uuid de saudação.
>
>

- - -
* A GUI da SAP (para fins administrativos e de instalação) podem ser pré-instalados em um modelo desse tipo.
* Outro software necessário toorun Olá VMs com êxito em cenários entre locais pode ser instalado como esse software pode trabalhar com hello renomear de saudação VM.

Se Olá VM for preparada suficientemente toobe genérica e independente de contas/usuários não está disponíveis no hello direcionada cenário de implantação do Azure, Olá última etapa de preparação generalizar essa imagem é realizada.

##### <a name="generalizing-a-vm"></a>Generalizando uma VM
- - -
[comment]: <> (MShermannd TODO tiver artigos melhor toofind / documentação sobre generalizar Olá VMs para ARM)
> ![Windows][Logo_Windows] Windows
>
> Olá última etapa é toolog em tooa VM com uma conta de administrador. Abra uma janela de comando do Windows como “administrador”. Vá too...\windows\system32\sysprep e execute sysprep.exe.
> Uma janela pequena será exibida. É importante toocheck hello "Generalizar" opção (padrão de saudação é desmarcada) e alterar Olá opção de desligamento do padrão de 'Reiniciar' too'Shutdown'. Este procedimento pressupõe que o processo do sysprep Olá é executado localmente em Olá sistema operacional convidado de uma máquina virtual.
> Se você quiser tooperform procedimento de saudação com uma VM já em execução no Azure, execute as etapas de saudação descritas em [neste artigo][virtual-machines-windows-capture-image].
>
> ![Linux][Logo_Linux] Linux
>
> [Como toocapture uma toouse de máquina virtual Linux como um modelo do Gerenciador de recursos][virtual-machines-linux-capture-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Transferindo VMs e VHDs entre tooAzure local
Como carregar tooAzure de imagens e discos VM não é possível por meio de saudação Portal do Azure, você precisará toouse cmdlets do Azure PowerShell ou CLI. Outra possibilidade é usar saudação da ferramenta de saudação 'AzCopy'. ferramenta de saudação pode copiar VHDs entre local e o Azure (em ambas as direções). Ela também pode copiar VHDs entre Regiões do Azure. Consulte [esta documentação][storage-use-azcopy] para download e uso do AzCopy.

Uma terceira alternativa seria toouse várias ferramentas orientadas por GUI de terceiros. No entanto, certifique-se de que essas ferramentas dão suporte a Blobs de Páginas do Azure. Para nossas finalidades precisamos toouse Blob de páginas do Azure store (Olá diferenças são descritas aqui: <https://msdn.microsoft.com/library/windowsazure/ee691964.aspx>). Também ferramentas Olá fornecidas pelo Azure são muito eficientes em Compactar Olá VMs e VHDs que precisam toobe carregado. Isso é importante porque essa eficiência na compactação reduz o tempo de carregamento de saudação (que varia assim mesmo Olá carregamento link toohello direcionado de internet por meio de recurso de local de saudação e região de implantação do Azure Olá). É um sentido supor que carregar uma VM ou o VHD de local Europeu toohello dos EUA com base do Azure dados centers levará mais tempo do que carregar Olá mesmos VHDs/VMs toohello Europeu Azure data centers.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Carregando um VHD do local tooAzure
tooupload uma VM existente ou um VHD de saudação no local de rede essa VM ou VHD precisa requisitos de saudação toomeet conforme listado no capítulo [preparação para mover uma VM do tooAzure local com um disco não generalizado] [ planning-guide-5.2.1] deste documento.

Essa VM não precisa toobe generalizado e pode ser carregada no estado de saudação e forma tem após o desligamento no hello lado local. Olá mesmo é verdadeiro para VHDs adicionais que não contêm qualquer sistema operacional.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Carregando um VHD e tornando-o um Disco do Azure
Nesse caso, deseja tooupload um VHD, com ou sem um sistema operacional e montá-lo tooa VM como um disco de dados ou usá-lo como o disco do sistema operacional. Este é um processo de várias etapas

**Powershell**

* Assinatura de tooyour login com *AzureRmAccount de logon*
* Definir a assinatura de saudação de seu contexto com *conjunto AzureRmContext* e parâmetro SubscriptionId ou nome de inscrição - consulte <https://msdn.microsoft.com/library/mt619263.aspx>
* Carregar Olá VHD com *adicionar AzureRmVhd* tooan conta de armazenamento do Azure - consulte <https://msdn.microsoft.com/library/mt603554.aspx>
* Conjunto Olá OS disco de um novo toohello de configuração VM VHD com *conjunto AzureRmVMOSDisk* -consulte <https://msdn.microsoft.com/library/mt603746.aspx>
* Criar uma nova VM a partir da configuração VM Olá com *New-AzureRmVM* -consulte <https://msdn.microsoft.com/library/mt603754.aspx>
* Adicionar uma tooa de disco de dados nova VM com *adicionar AzureRmVMDataDisk* -consulte <https://msdn.microsoft.com/library/mt603673.aspx>

**CLI do Azure**

* Modo de Gerenciador de recursos do comutador tooAzure com *arm do modo de configuração do azure*
* Assinatura de tooyour login com *logon do azure*
* Selecione a assinatura com o *conjunto de contas do Azure `<subscription name or id`>*
* Carregar Olá VHD com *carregamento de blob de armazenamento do azure* -consulte [hello usando a CLI do Azure com o armazenamento do Azure][storage-azure-cli]
* Criar uma nova VM especificando Olá carregado VHD como disco do sistema operacional com *criar vm do azure* e o parâmetro -d
* Adicionar uma tooa de disco de dados nova VM com *vm disco anexar-novo*

**Modelo**

* Carregar Olá VHD com o Powershell ou CLI do Azure
* Implantar Olá VM com um modelo JSON referenciando Olá VHD, conforme mostrado no [esse modelo JSON de exemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-from-specialized-vhd/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Implantação de uma imagem de VM
tooupload uma VM existente ou um VHD de saudação no local de rede na ordem toouse-lo como uma imagem de VM do Azure essa VM ou VHD necessário toomeet requisitos de saudação listados no capítulo [preparação para implantar uma VM com uma imagem específica do cliente para SAP] [ planning-guide-5.2.2] deste documento.

* Use *sysprep* no Windows ou *waagent-desprovisionamento* no Linux toogeneralize sua VM - consulte [como toocapture uma máquina virtual do Windows na implantação do Gerenciador de recursos de saudação modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture uma toouse de máquina virtual Linux como um modelo do Gerenciador de recursos][virtual-machines-linux-capture-image-capture]
* Assinatura de tooyour login com *AzureRmAccount de logon*
* Definir a assinatura de saudação de seu contexto com *conjunto AzureRmContext* e parâmetro SubscriptionId ou nome de inscrição - consulte <https://msdn.microsoft.com/library/mt619263.aspx>
* Carregar Olá VHD com *adicionar AzureRmVhd* tooan conta de armazenamento do Azure - consulte <https://msdn.microsoft.com/library/mt603554.aspx>
* Conjunto Olá OS disco de um novo toohello de configuração VM VHD com *AzureRmVMOSDisk Set - SourceImageUri - CreateOption fromImage* -consulte <https://msdn.microsoft.com/library/mt603746.aspx>
* Criar uma nova VM a partir da configuração VM Olá com *New-AzureRmVM* -consulte <https://msdn.microsoft.com/library/mt603754.aspx>

**CLI do Azure**

* Use *sysprep* no Windows ou *waagent-desprovisionamento* no Linux toogeneralize sua VM - consulte [como toocapture uma máquina virtual do Windows na implantação do Gerenciador de recursos de saudação modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture uma toouse de máquina virtual Linux como um modelo do Gerenciador de recursos] [ virtual-machines-linux-capture-image-capture] para Linux
* Modo de Gerenciador de recursos do comutador tooAzure com *arm do modo de configuração do azure*
* Assinatura de tooyour login com *logon do azure*
* Selecione a assinatura com o *conjunto de contas do Azure `<subscription name or id`>*
* Carregar Olá VHD com *carregamento de blob de armazenamento do azure* -consulte [hello usando a CLI do Azure com o armazenamento do Azure][storage-azure-cli]
* Criar uma nova VM especificando Olá carregado VHD como disco do sistema operacional com *criar vm do azure* e o parâmetro -Q

**Modelo**

* Use *sysprep* no Windows ou *waagent-desprovisionamento* no Linux toogeneralize sua VM - consulte [como toocapture uma máquina virtual do Windows na implantação do Gerenciador de recursos de saudação modelo] [ virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture] ou [como toocapture uma toouse de máquina virtual Linux como um modelo do Gerenciador de recursos] [ virtual-machines-linux-capture-image-capture] para Linux
* Carregar Olá VHD com o Powershell ou CLI do Azure
* Implantar Olá VM com um modelo JSON fazer referência a saudação imagem VHD conforme mostrado na [esse modelo JSON de exemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-tooon-premises"></a>Baixando VHDs tooon local
Infraestrutura do Azure como um serviço não é um endereço unidirecional de apenas ser capaz de tooupload VHDs e sistemas SAP. Você pode mover SAP volta de sistemas do Azure para Olá, mundo de local também.

Durante o tempo de saudação do download Olá Olá VHDs não pode estar ativa. Mesmo ao baixar VHDs que são montados tooVMs, Olá VM precisa toobe desligamento. Se você quiser apenas o banco de dados de saudação do toodownload conteúdo, em seguida, que deve ser usado tooset um novo sistema local e se é aceitável que durante o tempo de saudação do hello baixar e Olá a instalação do sistema novo Olá Olá sistema no Azure ainda pode estar operacional , você pode evitar um longo tempo de inatividade executando um backup de banco de dados compactado em um VHD e simplesmente baixar o VHD em vez de também baixar Olá VM de base do sistema operacional.

#### <a name="powershell"></a>Powershell
Depois que o sistema SAP de saudação for interrompido e Olá VM for desligada, você pode usar cmdlet do PowerShell Olá AzureRmVhd salvar em Olá local discos VHD do destino toodownload Olá fazer toohello mundo de local. Toodo, é necessária URL Olá Olá VHD que você pode encontrar no hello seção do armazenamento de hello Azure Portal (necessidade toonavigate toohello conta de armazenamento e hello contêiner de armazenamento onde hello VHD foi criado) e é necessário tooknow onde hello VHD deve ser copiada.

Em seguida, você pode aproveitar o comando hello, basta definir o parâmetro hello SourceUri como URL de saudação do toodownload VHD hello e hello LocalFilePath como o local físico de saudação do hello VHD (incluindo seu nome). comando Olá seria semelhante ao seguinte:

```powerhell
Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
```

Para obter mais detalhes do cmdlet Olá AzureRmVhd salvar, verifique aqui <https://msdn.microsoft.com/library/mt622705.aspx>.

#### <a name="cli"></a>CLI
Depois que o sistema SAP de saudação for interrompido e Olá VM for desligada, você pode usar o download de blob de armazenamento do azure Olá CLI do Azure comando em Olá local discos VHD do destino toodownload Olá fazer toohello mundo de local. Em ordem toodo que, você precisa de nome hello e contêiner Olá Olá VHD que você pode encontrar no hello seção do armazenamento de hello Azure Portal (necessidade toonavigate toohello conta de armazenamento e hello contêiner de armazenamento onde hello VHD foi criado) e você precisa tooknow onde Olá VHD deve ser copiado.

Em seguida, você pode aproveitar o comando hello, basta definir o contêiner de toodownload VHD hello e destino hello e blob de parâmetros de saudação como local físico de destino Olá Olá VHD (incluindo seu nome). comando Olá seria semelhante ao seguinte:

```
azure storage blob download --blob <name of hello VHD toodownload> --container <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --destination <destination of hello VHD toodownload>
```

### <a name="transferring-vms-and-vhds-within-azure"></a>Transferindo VMs e VHDs no interior do Azure
#### <a name="copying-sap-systems-within-azure"></a>Copiando sistemas SAP no interior do Azure
Um sistema SAP ou até mesmo um servidor DBMS dedicado dando suporte a uma camada de aplicativo SAP será provavelmente consistem em vários VHDs que contêm qualquer sistema operacional Olá com binários hello ou Olá dados e arquivos do banco de dados do SAP Olá de log. Olá funcionalidade do Azure de copiar VHDs nem a funcionalidade do Azure de salvar VHDs toodisk hello tem um mecanismo de sincronização que seria vários VHDs instantâneo de forma síncrona. Portanto, o estado de saudação do hello copiados ou salvos VHDs, mesmo se eles estão montados em relação a saudação mesma VM seria diferente. Isso significa que no caso concreto Olá com dados diferentes e os arquivos contidos em Olá diferentes VHDs, Olá banco de dados no final da saudação ficaria inconsistente.

**Conclusão: Toocopy ordem ou salvar VHDs que fazem parte de uma configuração do sistema SAP precisa toostop Olá SAP sistema e também precisa tooshut inativo saudação implantado VM. Somente, em seguida, você pode copiar ou download Olá conjunto de VHDs tooeither criar uma cópia do sistema SAP de saudação no Azure ou no local.**

Discos de dados são armazenados como arquivos VHD em uma conta de armazenamento do Azure e podem ser diretamente anexar a máquina virtual de tooa ou ser usado como uma imagem. Nesse caso, Olá VHD é copiado tooanother local antes beeing anexado a máquina virtual de toohello. nome completo de saudação do arquivo VHD Olá no Azure deve ser exclusivo dentro do Azure. Conforme mencionado anteriormente já, o nome de saudação é tipo de um nome de três partes que se parece com:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

##### <a name="powershell"></a>Powershell
Você pode usar toocopy de cmdlets do PowerShell do Azure um VHD, conforme mostrado no [neste artigo][storage-powershell-guide-full-copy-vhd].

##### <a name="cli"></a>CLI
Você pode usar a CLI do Azure toocopy um VHD conforme mostrado no [neste artigo][storage-azure-cli-copy-blobs]

##### <a name="azure-storage-tools"></a>Ferramentas do Armazenamento do Azure
* <http://azurestorageexplorer.codeplex.com/releases/view/125870>

Também há edições profissionais de Gerenciadores do Armazenamento do Azure que podem ser encontradas aqui:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

cópia de saudação de um VHD em uma conta de armazenamento é um processo que leva apenas alguns segundos (semelhante hardware tooSAN cria instantâneos com a cópia lenta e cópia na gravação). Depois que você tiver uma cópia do arquivo VHD Olá anexar máquina de virtual tooa ou use-o como uma imagem tooattach copia de máquinas de toovirtual VHD hello.

##### <a name="powershell"></a>Powershell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun e.g. 0> -CreateOption fromImage
$vm | Update-AzureRmVM
```
##### <a name="cli"></a>CLI
```
azure config mode arm

# attach a vhd tooa vm
azure vm disk attach <resource group name> <vm name> <path toovhd>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Copiando discos entre Contas de Armazenamento do Azure
Não é possível executar esta tarefa Olá Portal do Azure. Você pode usar cmdlets do Azure PowerShell, a CLI do Azure ou um navegador de armazenamento de terceiros. Olá cmdlets do PowerShell ou comandos CLI podem criar e gerenciar blobs, que incluem blobs de cópia Olá capacidade tooasynchronously entre contas de armazenamento e entre regiões dentro de saudação assinatura do Azure.

##### <a name="powershell"></a>Powershell
Também é possível copiar VHDs entre assinaturas. Para obter mais informações, leia [este artigo][storage-powershell-guide-full-copy-vhd].

fluxo básico de saudação do hello lógica de cmdlet do PS tem esta aparência:

* Criar um contexto de conta de armazenamento para conta de armazenamento de origem Olá com *New-AzureStorageContext* -consulte <https://msdn.microsoft.com/library/dn806380.aspx>
* Criar um contexto de conta de armazenamento para conta de armazenamento de destino Olá com *New-AzureStorageContext* -consulte <https://msdn.microsoft.com/library/dn806380.aspx>
* Iniciar cópia de saudação com

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Verificar o status de saudação da cópia de saudação em um loop com

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Anexe Olá nova VHD tooa máquina virtual, conforme descrito acima.

Para obter exemplos, veja [este artigo][storage-powershell-guide-full-copy-vhd]

##### <a name="cli"></a>CLI
* Iniciar cópia de saudação com

```
  azure storage blob copy start --source-blob <source blob name> --source-container <source container name> --account-name <source storage account name> --account-key <source storage account key> --dest-container <target container name> --dest-blob <target blob name> --dest-account-name <target storage account name> --dest-account-key <target storage account name>
```

* Verificar o status de saudação se hello cópia em um loop com

```
azure storage blob copy show --blob <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Anexe Olá nova VHD tooa máquina virtual, conforme descrito acima.

Para obter exemplos, veja [este artigo][storage-azure-cli-copy-blobs]

### <a name="disk-handling"></a>Administração de discos
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Estrutura de VM/VHD para implantações SAP
Olá idealmente tratamento da estrutura de saudação de uma VM e VHDs Olá associado devem ser bem simples. Em instalações locais, os clientes desenvolveram muitas formas de estruturar uma instalação de servidor.

* Um VHD de base contém Olá SO e todos os binários Olá Olá DBMS e/ou SAP. Desde março de 2015, este VHD pode ser o too1TB em tamanho, em vez de restrições anteriores limitada-too127GB.
* Um ou vários VHDs que contém Olá DBMS arquivo de log do banco de dados do SAP hello e arquivo de log de saudação de saudação área de armazenamento temporário de DBMS (se Olá DBMS dá suporte a isso). Se os requisitos de IOPS de log de banco de dados de saudação estiverem altos, é necessário toostripe vários VHDs no volume de pedidos tooreach Olá IOPS necessários.
* Um número de VHDs contendo um ou dois arquivos de banco de dados do banco de dados do SAP hello e arquivos de dados temporários de DBMS Olá também (se Olá DBMS dá suporte a isso).

![Configuração de referência da VM IaaS do Azure para SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO: descreva a estrutura do Linux )

- - -
> ![Windows][Logo_Windows] Windows
>
> Com muitos clientes, vimos configurações em que, por exemplo, binários de DBMS e SAP não foram instalados na unidade c:\ de saudação onde hello SO estava instalado. Havia vários motivos para isso, mas quando analisamos toohello raiz, geralmente era que Olá unidades eram pequenas e atualizações do sistema operacional necessário espaço adicional 10 a 15 anos atrás. Nenhuma das condições se aplica com muita frequência nos dias de hoje. Atualmente a unidade c:\ de saudação pode ser mapeada em máquinas virtuais ou discos de grande volume. Em implantações de tookeep ordem simples em sua estrutura, é recomendável toofollow o seguinte padrão de implantação de sistemas SAP NetWeaver no Azure
>
> arquivo de paginação do sistema operacional Olá Windows deve estar no hello unidade d: (disco não persistente)
>
> ![Linux][Logo_Linux] Linux
>
> Colocar o arquivo de permuta Olá Linux em /mnt /mnt/Retention/ recursos no Linux conforme descrito em [neste artigo][virtual-machines-linux-agent-user-guide]. arquivo de permuta Olá pode ser definido no arquivo de configuração de saudação do hello /etc/waagent.conf de agente Linux. Adicionar ou alterar Olá configurações a seguir:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

alterações de saudação tooactivate, você precisa toorestart Olá agente do Linux com

```
sudo service waagent restart
```

Leia a nota SAP [1597355] para obter mais detalhes sobre Olá recomendado o tamanho do arquivo de permuta

- - -
número de saudação de VHDs usados para arquivos de dados do DBMS hello e o tipo de saudação do armazenamento do Azure esses VHDs são hospedados em deve ser determinado pelos requisitos de IOPS de saudação e latência de saudação necessário. Cotas exatas são descritas [neste artigo][virtual-machines-sizes]

Experiência de implantações do SAP em Olá últimos 2 anos us ministrada algumas lições que podem ser resumidas como:

* Arquivos de dados do IOPS tráfego toodifferent nem sempre é Olá mesmo desde sistemas existentes do cliente podem diferentemente dimensionado dados arquivos que representa a seus bancos de dados do SAP. Como resultado acontece toobe melhor usando uma configuração RAID em vários arquivos de dados Olá de VHDs de tooplace, que LUNs gravados fora das. Não havia situações, especialmente com onde uma taxa IOPS ocorrências cota de saudação de um único VHD no log de transações do DBMS saudação padrão de armazenamento do Azure. Uso de armazenamento Premium Olá cenários é recomendável ou como alternativa agregar vários VHDs de armazenamento padrão com um RAID de software.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Performance best practices for SQL Server in Azure Virtual Machines][virtual-machines-sql-server-performance-best-practices] (Práticas recomendadas de desempenho para o SQL Server em Máquinas Virtuais do Azure)
>
> ![Linux][Logo_Linux] Linux
>
> * [Configurar RAID de software no Linux][virtual-machines-linux-configure-raid]
> * [Configurar o LVM em uma VM Linux no Azure][virtual-machines-linux-configure-lvm]
> * [Segredos do Armazenamento do Azure e otimizações de E/S do Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* O Armazenamento Premium está apresentando desempenho significativamente melhor, especialmente para gravações de log de transações críticas. Para cenários SAP que são produção toodeliver esperado como o desempenho, é altamente recomendável toouse série de VM que pode aproveitar o armazenamento Premium do Azure.

Tenha em mente que Olá VHD que contém Olá SO e conforme Recomendamos, hello binários do banco de dados do SAP e hello (VM de base), não está mais limitado too127GB. Ela agora pode ter até too1TB em tamanho. Isso deve ser suficiente espaço tookeep todos Olá arquivo necessário, por exemplo, incluindo logs de trabalho do SAP em lote.

Para mais sugestões e detalhes especificamente sobre VMs de DBMS, consulte Olá [guia de implantação de DBMS][dbms-guide]

#### <a name="disk-handling"></a>Administração de discos
Na maioria dos cenários, é necessário toocreate outros discos no banco de dados do pedido toodeploy Olá SAP em Olá VM. Falamos sobre considerações de saudação no número de VHDs capítulo [estrutura de VM/VHD para implantações SAP] [ planning-guide-5.5.1] deste documento. Olá Portal do Azure permite tooattach e desvincular discos depois que uma VM de base é implantada. discos de saudação podem ser vinculados/desvinculados quando Olá VM está instalado e em execução, bem como quando ele é interrompido. Ao anexar um disco, Olá Portal do Azure oferece tooattach um disco vazio ou um disco existente que neste momento não é anexado tooanother VM.

**Observação**: VHDs só podem ser anexado tooone VM em um determinado momento.

![Anexar/desanexar discos do Armazenamento Standard do Azure][planning-guide-figure-1400]

Se você deseja toocreate um VHD novo e vazio (que seria criado no Olá a mesma conta de armazenamento como Olá VM de base está em) ou se você quer tooselect um VHD existente que foi carregado anteriormente e deve ser anexado toohello VM agora, você precisa toodecide.

**IMPORTANTE**: você **não** deseja toouse Caching do Host com o armazenamento padrão do Azure. Você deve deixar a preferência de Cache de Host de saudação padrão Olá nenhum. Com o armazenamento do Azure Premium você deve habilitar o cache de leitura se a característica de e/s de saudação principalmente é lido como o tráfego de e/s comum em arquivos de dados do banco de dados. No caso do arquivo de log de transações do banco de dados, é recomendado usar a opção sem cache.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Como tooattach dados de um disco em Olá portal do Azure][virtual-machines-windows-attach-disk-portal]
>
> Se discos forem vinculados, você precisa toolog em Olá tooopen da VM Olá Gerenciador de disco do Windows. Se a montagem automática não está habilitada conforme recomendado capítulo [definindo a montagem automática para discos anexados][planning-guide-5.5.3], volume recém-vinculado hello precisa toobe colocado online e inicializados.
>
> ![Linux][Logo_Linux] Linux
>
> Se discos forem vinculados, você precisa toolog em Olá VM e inicializar discos hello, conforme descrito em [neste artigo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Se Olá novo disco for um disco vazio, será necessário tooformat Olá disco também. Para formatação, especialmente para DBMS, arquivos de log e dados Olá mesmas recomendações sobre implantações bare-metal de saudação que DBMS se aplicam.

Como já mencionado no capítulo [Olá conceito de máquina Virtual do Microsoft Azure][planning-guide-3.2], uma conta de armazenamento do Azure não oferece recursos ilimitados em termos de volume de e/s, IOPS e volume de dados. Geralmente as VMs de DBMS são mais afetadas por isso. Talvez seja melhor toouse uma conta de armazenamento separada para cada VM se você tiver poucos toodeploy alta de VMs de volume e/s em ordem toostay no limite de saudação de saudação volume de conta de armazenamento do Azure. Caso contrário, será necessário toosee como equilibrará essas VMs entre diferentes contas de armazenamento sem atingir o limite de saudação de cada conta de armazenamento único. Mais detalhes são abordados em Olá [guia de implantação de DBMS][dbms-guide]. Você também deve ter essas limitações em mente para VMs de servidor de aplicativos SAP puro ou outras VMs que eventualmente possam exigir VHDs adicionais.

Outro tópico é relevante para contas de armazenamento é se Olá VHDs em uma conta de armazenamento são replicados geograficamente. Replicação geográfica está habilitada ou desabilitada em Olá nível da conta de armazenamento e não em Olá nível da VM. Se a replicação geográfica estiver habilitada, Olá VHDs em Olá em que conta de armazenamento será replicada para outro data center do Azure Olá mesma região. Antes de decidir sobre isso, você deve considerar Olá restrição a seguir:

Replicação geográfica do Azure funciona localmente em cada VHD em uma máquina virtual e não replica Olá IOs em ordem cronológica entre vários VHDs em uma máquina virtual. Portanto, Olá VHD que representa Olá VM de base, bem como qualquer toohello de VHDs anexados VMs adicional são replicadas independentes um do outro. Isso significa que não há nenhuma sincronização entre alterações Olá Olá diferentes VHDs. Olá fato Olá IOs são replicadas independentemente da ordem de saudação na qual eles são gravados significa que a replicação geográfica não é do valor para os servidores de banco de dados com bancos de dados distribuídos entre vários VHDs. Em adição toohello DBMS, também pode haver outros aplicativos em que os processos gravam ou manipulam dados em diferentes VHDs e onde é importante tookeep Olá ordem das alterações. Se isso for um requisito, a replicação geográfica no Azure não deverá ser habilitada. Dependendo de você precisar/querer ou não a replicação geográfica para um conjunto de VMs, mas não para outro conjunto, você já pode categorizar VMs e os VHDs relacionados a elas em diferentes Contas de Armazenamento com replicação geográfica habilitada ou desabilitada.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Definindo a montagem automática para os discos anexados
- - -
> ![Windows][Logo_Windows] Windows
>
> Para VMs que são criadas a partir de imagens ou discos próprios, é necessário toocheck e possivelmente definir parâmetro de montagem automática de saudação. A definição desse parâmetro permitirá Olá VM após uma reinicialização ou reimplantação no Azure toomount Olá anexado/unidades montadas novamente automaticamente.
> Olá parâmetro é definido para Olá imagens fornecidas pela Microsoft hello Azure Marketplace.
>
> Em ordem tooset Olá montagem automática, consulte a documentação de saudação do hello linha de comando executável diskpart.exe aqui:
>
> * [Opções de linha de comando do DiskPart](https://technet.microsoft.com/library/cc766465.aspx)
> * [Montagem automática](http://technet.microsoft.com/library/cc753703.aspx)
>
> janela de linha de comando do Windows Hello deve ser aberta como administrador.
>
> Se discos forem vinculados, você precisa toolog em Olá tooopen da VM Olá Gerenciador de disco do Windows. Se a montagem automática não está habilitada conforme recomendado capítulo [definindo a montagem automática para discos anexados][planning-guide-5.5.3], Olá recentemente anexado volume > precisa toobe colocado online e inicializados.
>
> ![Linux][Logo_Linux] Linux
>
> Você precisa tooinitialize um disco vazio anexado recentemente, conforme descrito em [neste artigo][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Você também precisa tooadd novos discos toohello /etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Implantação final
Para Olá implantação final e as etapas exatas, especialmente com relação toohello implantação de SAP estendidos monitoramento, consulte toohello [guia de implantação][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Acessando sistemas SAP em execução nas VMs do Azure
Para cenários de nuvem, talvez você queira sistemas SAP toothose tooconnect em Olá internet pública usando a GUI do SAP. Para esses casos, hello procedimentos a seguir necessário toobe aplicado.

Documento hello, discutiremos Olá outro cenário principal, conectar sistemas tooSAP em implantações entre locais que têm uma conexão site a site (túnel VPN) ou conexão de rota expressa do Azure entre sistemas de local de saudação e do Azure.

### <a name="remote-access-toosap-systems"></a>Sistemas de tooSAP de acesso remotos
Com o Azure Resource Manager há sem pontos de extremidade padrão mais como Olá antiga clássico modelo. Todas as portas de uma VM do Azure ARM permanecem abertas desde que:

1. Nenhum grupo de segurança de rede é definido para a sub-rede de saudação ou interface de rede de saudação. Tráfego de rede tooAzure VMs pode ser protegido por meio de chamadas "grupos de segurança de rede". Para obter mais informações, consulte [O que é um NSG (Grupo de Segurança de Rede)?][virtual-networks-nsg]
2. Nenhum balanceador de carga do Azure é definido para a interface de rede Olá   

Ver a diferença de arquitetura de saudação entre o modelo clássico e ARM conforme descrito em [neste artigo][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Configuração de saudação conectividade de sistema SAP e SAP GUI para o cenário de nuvem
Consulte este artigo que descreve o tópico de toothis detalhes: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Alterando as configurações de Firewall na VM
Talvez seja necessário tooconfigure firewall Olá tooallow suas máquinas virtuais tráfego tooyour SAP sistema de entrada.

- - -
> ![Windows][Logo_Windows] Windows
>
> Por padrão, a saudação Firewall do Windows em uma VM implantada do Azure é ativada. Agora, você precisa tooallow Olá porta SAP toobe aberto, caso contrário Olá SAP GUI não será capaz de tooconnect.
> toodo isso:
>
> * Abra o controle de painel de controle\sistema e segurança \ Firewall too'Advanced configurações.
> * Agora, clique com o botão direito do mouse em Regras de Entrada e escolha “Nova Regra”.
> * Olá o seguinte assistente escolheu toocreate uma nova regra de 'porta do '.
> * Na próxima etapa do assistente Olá Olá, deixe Olá configuração TCP e o tipo de número de porta Olá que você deseja tooopen. Como a ID da nossa instância SAP é 00, usamos 3200. Se a instância tiver um número diferente de instância, porta Olá você definiu anteriormente com base no número de instância Olá deve ser aberta.
> * A próxima parte do Assistente de Olá Olá, é necessário tooleave item de saudação 'Permitir Conexão' verificada.
> * A próxima etapa saudação do Assistente de saudação precisar toodefine se Olá regra aplica-se para a rede de domínio, privado e público. Faça o ajuste precisa tooyour necessário. No entanto, se conectando com a SAP GUI de saudação fora da rede pública Olá, é necessário rede pública do toohello toohave Olá regra aplicada.
> * A última etapa do assistente Olá Olá, você precisa Olá toogive um nome de regra e, em seguida, salvar a regra de saudação pressionando "Concluir"
>
> Olá regra entrará em vigor imediatamente.
>
> ![Definição da regra de porta][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> imagens Linux Olá Olá Azure Marketplace não habilitar o firewall de iptables de saudação por padrão e sistema SAP Olá conexão tooyour deve funcionar. Se você tiver habilitado iptables ou outro firewall, consulte a documentação toohello de iptables ou Olá usado firewall tooallow tráfego tcp de entrada muito porta 32xx (onde xx é o número de sistema de saudação do sistema SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Recomendações de segurança
Olá SAP GUI não se conecta imediatamente tooany Olá de instâncias do SAP (porta 32xx) que estão em execução, mas primeiro se conecta por meio de saudação porta aberta toohello SAP mensagem processo do servidor (porta 36xx). Olá após Olá mesma porta foi usado por servidor de mensagens de saudação para instâncias de aplicativo de toohello Olá comunicação interna. tooprevent aplicativo servidores locais inadvertidamente se comunique com um servidor de mensagens no Azure Olá interna portas de comunicação podem ser alteradas. É altamente recomendável comunicação interna do hello toochange entre o servidor de mensagens SAP hello e seu número de porta diferente do aplicativo instâncias tooa em sistemas que foram clonados a partir de sistemas locais, como um clone de desenvolvimento para projeto de teste etc. Isso pode ser feito com o parâmetro de perfil de padrão de saudação:

> rdisp/msserv_internal
>
>

como documentado em: <https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm>

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Conceitos de implantação somente em nuvem de instâncias do SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Cenário de treinamento/demonstração de VM única com SAP NetWeaver
![Executando os sistemas de demonstração SAP de VM única com Olá nomes iguais, isolados em serviços de nuvem do Azure][planning-guide-figure-1700]

Neste cenário (consulte o capítulo [somente em nuvem] [ planning-guide-2.1] deste documento), implementaremos um cenário de sistema de treinamento/demonstração típico em que o cenário de treinamento/demonstração completo hello está contido em uma única VM. Vamos supor que a implantação de saudação é feita por meio de modelos de imagem VM. Também pressupomos que várias essas toobe de necessidade de VMs demonstração/treinamento implantado com hello VMs com hello mesmo nome.

Olá pressupõe-se que você criou uma imagem de VM, conforme descrito em algumas seções do capítulo [Preparando VMs com SAP para o Azure] [ planning-guide-5.2] neste documento.

sequência de saudação do cenário de saudação tooimplement eventos tem esta aparência:

[comment]: <> (MShermannd TODO ter exemplo ARM tooprovide / descrição usando o modelo json + esclarecimento sobre o nome exclusivo da VM na rede virtual ARM)   
##### <a name="powershell"></a>Powershell
* Criar um novo grupo de recursos para cada estrutura de treinamento/demonstração

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```

* Criar uma nova conta de armazenamento

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Criar uma nova rede virtual para cada uso treinamento/demonstração paisagem tooenable Olá Olá mesmo nome de host e endereços IP. rede virtual Olá é protegido por um grupo de segurança de rede que só permite o acesso de área de trabalho remota do tráfego tooport tooenable 3389 e porta 22 SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Criar um novo endereço IP público que pode ser usado tooaccess Olá máquina de virtual de saudação à internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Criar uma nova interface de rede da máquina virtual de saudação

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Crie uma máquina virtual. Cenário de saudação somente em nuvem todas as VMs terão Olá mesmo nome. Olá SID das Olá instâncias nessas VMs do SAP NetWeaver Olá mesmo assim. No grupo de recursos do Azure de hello, nome de saudação do hello VM precisa toobe exclusivo, mas em diferentes grupos de recursos do Azure, você pode executar VMs com hello mesmo nome. Olá padrão '' conta do Windows ou raiz para Linux não é válido. Portanto, um novo nome de usuário administrador deve toobe definido junto com uma senha. tamanho de saudação do hello VM também precisa toobe definido.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES" -Skus "12" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="os"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"
$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Opcionalmente, adicione discos adicionais e restaure o conteúdo necessário. Lembre-se de que todos os nomes de blob (URLs toohello blobs) devem ser exclusivos dentro do Azure.

```powershell
# Optional: Attach additional data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
Olá, código de exemplo a seguir pode ser usado no Linux. Para Windows, por favor, use PowerShell conforme descrito acima ou adaptar Olá exemplo toouse % rgName %, em vez de $rgName e definir variável de ambiente hello usando o comando do Windows hello *definir*.

* Criar um novo grupo de recursos para cada estrutura de treinamento/demonstração

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
azure group create $rgName "North Europe"
```

* Criar uma nova conta de armazenamento

```
azure storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku-name LRS $rgNameLower
```

* Criar uma nova rede virtual para cada uso treinamento/demonstração paisagem tooenable Olá Olá mesmo nome de host e endereços IP. rede virtual Olá é protegido por um grupo de segurança de rede que só permite o acesso de área de trabalho remota do tráfego tooport tooenable 3389 e porta 22 SSH.

```
azure network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
azure network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

azure network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
azure network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group-name SAPERPDemoNSG
```

* Criar um novo endereço IP público que pode ser usado tooaccess Olá máquina de virtual de saudação à internet

```
azure network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --domain-name-label $rgNameLower --allocation-method Dynamic
```

* Criar uma nova interface de rede da máquina virtual de saudação

```
azure network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-name SAPERPDemoPIP --subnet-name Subnet1 --subnet-vnet-name SAPERPDemoVNet
```

* Crie uma máquina virtual. Cenário de saudação somente em nuvem todas as VMs terão Olá mesmo nome. Olá SID das Olá instâncias nessas VMs do SAP NetWeaver Olá mesmo assim. No grupo de recursos do Azure de hello, nome de saudação do hello VM precisa toobe exclusivo, mas em diferentes grupos de recursos do Azure, você pode executar VMs com hello mesmo nome. Olá padrão '' conta do Windows ou raiz para Linux não é válido. Portanto, um novo nome de usuário administrador deve toobe definido junto com uma senha. tamanho de saudação do hello VM também precisa toobe definido.

```
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn SUSE:SLES:12:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
# azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --image-urn RedHat:RHEL:7.2:latest --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd --disable-boot-diagnostics
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
#azure vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nic-name SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --vm-size Standard_D11 --os-disk-vhd https://$rgNameLower.blob.core.windows.net/vhds/os.vhd -Q <path tooimage vhd> --disable-boot-diagnostics
```

* Opcionalmente, adicione discos adicionais e restaure o conteúdo necessário. Lembre-se de que todos os nomes de blob (URLs toohello blobs) devem ser exclusivos dentro do Azure.

```
# Optional: Attach additional data disks
azure vm disk attach-new --resource-group $rgName --vm-name SAPERPDemo --size-in-gb 1023 --vhd-name datadisk
```

##### <a name="template"></a>Modelo
Você pode usar modelos de exemplo hello no repositório de modelos do azure-quickstart Olá no github.

* [VM Linux Simples](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [VM Windows Simples](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [VM de imagem](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementar um conjunto de máquinas virtuais que precisam toocommunicate dentro do Azure
Este cenário somente em nuvem é um cenário típico para fins de demonstração e treinamento onde hello software representando Olá cenário de demonstração/treinamento é distribuído entre várias VMs. Olá diferentes componentes instalados em Olá diferentes VMs necessidade toocommunicate entre si. Novamente, nesse cenário, nenhuma comunicação de rede local ou cenário entre instalações é necessário.

Este cenário é uma extensão da instalação de saudação descrita nos capítulos [VM única com cenário de demonstração/treinamento do SAP NetWeaver] [ planning-guide-7.1] deste documento. Nesse caso mais máquinas virtuais serão adicionadas tooan grupo de recursos existente. Olá cenário de treinamento do seguinte exemplo hello consiste em uma VM do SAP ASCS/SCS, uma VM que executa um DBMS e uma instância de servidor de aplicativos SAP VM.

Antes de desenvolver esse cenário, é necessário toothink sobre configurações básicas, conforme já realizado no cenário de saudação antes.

#### <a name="resource-group-and-virtual-machine-naming"></a>Nomeação de grupos de recursos e máquinas virtuais
Todos os nomes de grupos de recursos devem ser exclusivos. Desenvolva seu próprio esquema de nomenclatura de seus recursos, como `<rg-name`>-sufixo.

nome da máquina virtual Olá tem toobe exclusivo no grupo de recursos de saudação.

#### <a name="setup-network-for-communication-between-hello-different-vms"></a>Configuração de rede para comunicação entre Olá VMs diferentes
![Conjunto de VMs em uma Rede Virtual do Azure][planning-guide-figure-1900]

tooprevent nomenclatura colisões com clones de saudação mesmo cenários de treinamento/demonstração, você precisa toocreate uma rede Virtual do Azure para cada cenário. Resolução de nome DNS será fornecida pelo Azure ou você pode configurar seu próprio servidor DNS fora do Azure (não toobe mais discutido aqui). Neste cenário, não configuraremos nosso próprio DNS. A comunicação por meio de nomes do host será habilitada para todas as máquinas virtuais dentro de uma Rede Virtual do Azure.

Olá motivos para cenários de treinamento ou demonstração tooseparate por redes virtuais e não apenas o recurso grupos podem ser:

* Olá SAP paisagem configurados necessidades de seu próprio AD/OpenLDAP e uma parte do servidor de domínio necessidades toobe de cada um dos cenários de saudação.  
* Olá estrutura SAP como conjunto de backup tem componentes que toowork necessidade com endereços IP fixos.

Para obter mais detalhes sobre redes virtuais do Azure e como toodefine-los podem ser encontrados em [neste artigo][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Implantar VMs SAP com conectividade de rede corporativa (entre instalações)
Executar uma paisagem SAP e quiser toodivide Olá implantação entre bare-metal para servidores DBMS de ponta, ambientes virtualizadas locais para camadas de aplicativo e da camada de 2 menor configurados sistemas SAP e IaaS do Azure. Olá hipótese geral é que os sistemas SAP em uma estrutura SAP precisam toocommunicate entre si e com muitos outros componentes de software implantados na empresa hello, independente da forma de implantação. Também não deve haver nenhuma diferença introduzida pelo formulário de implantação Olá para conectar-se com a SAP GUI ou outras interfaces dos usuários finais hello. Essas condições só podem ser atendidas quando temos Olá Active Directory/OpenLDAP local e serviços DNS estendido toohello sistemas do Azure por meio de conectividade de site-para-site/vários sites ou conexões privadas como rota expressa do Azure.

Em tooget de ordem mais em segundo plano em detalhes de implementação de saudação do SAP no Azure, recomendamos que você tooread capítulo [implantação de conceitos de somente em nuvem de instâncias SAP] [ planning-guide-7] deste documento que explica alguns dos conceitos básicos de saudação constrói do Azure e como eles devem ser usados com aplicativos SAP no Azure.

### <a name="scenario-of-a-sap-landscape"></a>Cenário de uma estrutura da SAP
cenário entre locais de saudação pode ser aproximadamente descrito como em gráficos de saudação abaixo:

![Conexão site a site entre ativos locais e no Azure][planning-guide-figure-2100]

Olá, cenário mostrado acima descreve um cenário onde Olá local OpenLDAP/AD e DNS é estendido tooAzure. No lado do local de saudação, um determinado intervalo de endereços IP é reservado por assinatura do Azure. intervalo de endereços IP Hello será atribuído tooan rede Virtual do Azure em saudação do lado do Azure.

#### <a name="security-considerations"></a>Considerações de segurança
Olá requisito mínimo é Olá use protocolos de comunicação segura, como SSL/TLS para acesso do navegador ou conexões VPN para sistema acessar toohello Azure services. Olá pressupõe-se que as empresas lidar com conexão de VPN Olá entre sua rede corporativa e o Azure muito diferente. Algumas empresas sem restrições podem abrir todas as portas de saudação. Algumas outras empresas seja toobe muito precisos em quais portas precisam tooopen, etc.

Na tabela de saudação abaixo SAP típico portas de comunicação são listadas. Basicamente, é suficiente tooopen Olá porta de gateway SAP.

| O Barramento de | Número da Porta | Exemplo `<nn`> = 01 | Intervalo Padrão (Mín-Máx) | Comentário |
| --- | --- | --- | --- | --- |
| Dispatcher |sapdp`<nn>` confira * |3201 |3200 – 3299 |Dispatcher SAP, usado pela GUI da SAP para Windows e Java |
| Servidor de mensagens |sapms`<sid`> confira ** |3600 |número livre de sapms`<anySID`> |sid = ID do sistema SAP |
| Gateway |sapgw`<nn`> confira * |3301 |livre |Gateway SAP, usado para comunicação CPIC e RFC |
| Roteador SAP |sapdp99 |3299 |livre |Apenas os nomes de serviço CI (instância central) podem ser reatribuídos em /etc/services tooan arbitrário valor após a instalação. |

*) nn = Número da Instância SAP

**) sid = ID do sistema SAP

As informações mais detalhadas sobre as portas necessárias, para os diferentes produtos ou serviços do SAP, para os produtos do SAP podem ser encontradas aqui <http://scn.sap.com/docs/DOC-17124>.
Com este documento, você deve ser capaz de tooopen dedicado portas no dispositivo VPN Olá necessário para cenários e produtos específicos do SAP.

Medidas de outros segurança quando implantar VMs nesse cenário pode ser toocreate um [grupo de segurança de rede] [ virtual-networks-nsg] toodefine as regras de acesso.

### <a name="dealing-with-different-virtual-machine-series"></a>Lidando com séries de máquina virtual diferentes
No curso de saudação dos últimos 12 meses, a Microsoft adicionou muitos mais tipos VM que diferem no número de vCPUs, memória ou mais importantes no hardware que ele é executado em. Nem todas essas VMs são compatíveis com o SAP (confira os tipos de VM com suporte na Nota do SAP [1928533]). Algumas dessas VMs são executadas em diferentes gerações de hardware de host. Nessas gerações de hardware do host sejam implantadas na granularidade de saudação de uma unidade de escala do Azure. Casos significa que podem surgir em tamanhos VM diferentes Olá que você escolheu não pode ser executado em Olá mesma unidade de escala. Um conjunto de disponibilidade é limitado em Olá capacidade toospan que unidades de escala com base no hardware diferente.  Por exemplo Se você quiser toorun Olá DBMS em VMs A5 A11 e Olá camada do aplicativo SAP em VMs da série G, seria forçado toodeploy um único sistema SAP ou diferentes sistemas SAP em diferentes conjuntos de disponibilidade.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Imprimindo em uma impressora de rede local da instância SAP no Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Imprimindo via TCP/IP no cenário entre instalações
A configuração de suas impressoras de rede TCP/IP com base no local em uma VM do Azure é Olá geral, mesmo que sua rede corporativa, supondo que você tenha um túnel VPN Site a Site ou conexão de rota expressa estabelecida.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo isso:
>
> * Algumas impressoras de rede vêm com um Assistente de configuração que torna fácil tooset sua impressora em uma VM do Azure. Se nenhum software de assistente foram distribuídas com o modo de "manual" hello impressora tooset impressora Olá é toocreate uma nova porta de impressora TCP/IP.
> * Abra o Painel de Controle -> Dispositivos e Impressoras -> Adicionar uma impressora
> * Escolha Adicionar uma impressora usando um endereço TCP/IP ou nome do host
> * Digite o endereço IP da impressora Olá Olá
> * A porta de impressora padrão é 9100
> * Se for necessário instale manualmente o driver de impressora apropriadas hello.
>
> ![Linux][Logo_Linux] Linux
>
> * como do Windows apenas siga Olá procedimento padrão tooinstall uma impressora de rede
> * Basta seguir públicos guias de Linux Olá para [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) ou [Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) sobre como tooadd uma impressora.
>
>

- - -
![Impressão em rede][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Impressora baseada em host por SMB (impressora compartilhada) em cenário entre instalações
Impressoras baseadas em host não são compatíveis com rede por design. Mas uma impressora baseada em host pode ser compartilhada entre computadores em uma rede enquanto impressora Olá estiver conectado tooa do computador ligado. Conecte sua rede corporativa via site a site ou ExpressRoute e compartilhe a impressora local. Olá protocolo SMB usa o NetBIOS em vez de DNS como serviço de nomes. nome de host NetBIOS Olá pode ser diferente do nome de host DNS hello. caso de saudação padrão é que o nome de host NetBIOS hello e nome de host DNS Olá são idênticos. domínio do DNS Olá não faz sentido no espaço de nome de NetBIOS hello. Olá adequadamente, o nome de host DNS totalmente qualificado consiste em nome de host DNS hello e não deve ser usado no espaço de nome de NetBIOS de saudação do domínio DNS.

compartilhamento de impressora Olá é identificado por um nome exclusivo na rede hello:

* Nome do host do host SMB hello (sempre necessário).
* Nome do compartilhamento de saudação (sempre necessário).
* Nome do domínio de saudação se o compartilhamento de impressora não está em Olá mesmo domínio que o sistema SAP.
* Além disso, um nome de usuário e uma senha podem ser necessário tooaccess Olá compartilhamento da impressora.

Como:

- - -
> ![Windows][Logo_Windows] Windows
>
> Compartilhe a impressora local.
> No hello Azure VM abra Olá Windows Explorer e digite nome de compartilhamento de saudação de impressora hello.
> Um Assistente de instalação de impressora o guiará pelo processo de instalação de saudação.
>
> ![Linux][Logo_Linux] Linux
>
> Aqui estão alguns exemplos de documentação sobre configuração de impressoras de rede no Linux ou inclusão de um capítulo sobre impressão no Linux. Ele funcionará Olá mesmo modo em uma VM do Linux do Azure, desde que Olá VM faz parte de uma VPN:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL <https://access.redhat.com/documentation/pt-br/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/s1-printing-smb-printer.html>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Impressora USB (encaminhamento de impressora)
Capacidade de saudação do Azure de acesso de Olá Olá Remote Desktop Services tooprovide usuários tootheir dispositivos de impressora locais em uma sessão remota não está disponível.

- - -
> ![Windows][Logo_Windows] Windows
>
> Mais detalhes sobre como imprimir com o Windows podem ser encontrados aqui: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integração de sistemas SAP do Azure ao Sistema de Correção e Transporte (TMS) para cenáros entre instalações
Olá tooexport toobe configurado de necessidades de alteração do SAP e transporte TMS (sistema) e importar solicitações de transporte entre sistemas em Paisagem hello. Vamos supor que instâncias de desenvolvimento de saudação de um sistema SAP (DEV) estejam localizadas no Azure enquanto Olá qualidade (QA) e sistemas de produção (PRD) são locais. Além disso, pressupomos que exista um diretório de transporte central.

##### <a name="configuring-hello-transport-domain"></a>Configurando Olá domínio de transporte
Configurar seu domínio de transporte no sistema de saudação designado como Olá controlador de domínio de transporte, conforme descrito em [Configurando Olá controlador de domínio de transporte](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Um usuário do sistema que TMSADM será criado e hello necessário destino RFC será gerado. Você pode verificar essas conexões RFC usando Olá transação SM59. A resolução do nome do host deve estar habilitada em seu domínio de transporte.

Como:

* Em nosso cenário, decidimos Olá sistema QAS será o controlador de domínio CTS Olá ao local. Chame a transação STMS. caixa de diálogo TMS Olá é exibida. Uma caixa de diálogo Configurar Domínio de Transporte é exibida. (Essa caixa de diálogo só aparece se você ainda não tiver configurado um domínio de transporte.)
* Certifique-se de que o usuário Olá criado automaticamente TMSADM está autorizado (SM59 -> Conexão ABAP -> TMSADM@E61.DOMAIN_E61 -> detalhes -> utilitários (m) -> teste de autorização). tela de saudação inicial da transação STMS deverá mostrar que esse sistema SAP agora estará funcionando como controlador de saudação do domínio de transporte Olá conforme mostrado aqui:

![Tela inicial da transação STMS no controlador de domínio Olá][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Incluindo sistemas SAP no domínio de transporte de saudação
sequência de saudação de inclusão de um sistema SAP em um domínio de transporte será semelhante ao seguinte:

* Em Olá sistema DEV no Azure acesse toohello sistema de transporte (cliente 000) e chame a transação STMS. Escolha outra configuração na caixa de diálogo hello e continue com incluir sistema no domínio. Especificar Olá controlador de domínio como o host de destino ([incluindo sistemas SAP no domínio de transporte de saudação](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). sistema de Olá agora está aguardando toobe incluído no domínio de transporte de saudação.
* Por motivos de segurança, você tem tooconfirm de controlador de domínio de backup toohello toogo sua solicitação. Escolha visão geral do sistema e aprovar do sistema em espera hello. Em seguida, confirme configuração saudação de prompt e hello será distribuída.

Esse sistema SAP agora contém informações necessárias de saudação sobre Olá todos os outros sistemas SAP no domínio de transporte hello. A saudação mesmo momento, endereço de saudação dados do sistema SAP da nova Olá são enviados tooall Olá outros sistemas SAP e Olá sistema SAP é inserido no perfil de transporte de saudação do programa de controle de transporte hello. Verifique se RFCs e acessar o diretório de transporte de toohello do domínio Olá funcionam.

Continue com a configuração de saudação do seu sistema de transporte normalmente conforme descrito na documentação de saudação [Change and Transport System](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Como:

* Certificar-se de que o STMS local está configurado corretamente.
* Verifique se o nome de host de saudação do hello controlador de domínio de transporte pode ser resolvido pela sua máquina virtual no Azure e vice-versa.
* Chamar a transação STMS -> Outras Configurações -> Incluir Sistema no Domínio.
* Confirme conexão Olá em Olá no sistema TMS local.
* Configurar camadas, grupos e rotas de transporte como de costume.

Em cenários conectados de entre locais site a site, Olá latência entre local e o Azure ainda pode ser substancial. Se é seguir Olá sequência de transportar objetos através de tooproduction de sistemas de desenvolvimento e teste ou pensarmos em aplicar os transportes ou pacotes de suporte toohello diferentes sistemas, você percebe que, depende do local de saudação do transporte central Olá diretório, alguns Olá sistemas encontrará alta latência, ler ou gravar dados no diretório de transporte central hello. situação Olá é configurações semelhantes de paisagem tooSAP onde o hello diferentes sistemas estão distribuídos por meio de data centers diferentes substancial distância entre os data centers de saudação.

Em ordem toowork esse problema de latência e ter sistemas Olá funcionar rápida em ler ou gravar tooor do diretório de transporte hello, você pode configurar dois domínios de transporte STMS (um para o local. e outro com sistemas de saudação em domínios de transporte de saudação do Azure e link Verifique se esta documentação que explica os princípios de saudação por trás desse conceito no SAP TMS de saudação: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Como:

* Configurar um domínio de transporte em cada localização (local e no Azure) usando a transação STMS <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Vincular domínios Olá com um link de domínio e confirme Olá link entre dois domínios de saudação.
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* Distribua Olá configuração toohello vinculado sistema.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Tráfego RFC entre instâncias SAP localizadas no Azure e localmente (entre instalações)
Tráfego RFC entre os sistemas que estão no local e no Azure precisa toowork. toosetup uma conexão chamada transação SM59 em um sistema de origem em que você precisa toodefine uma conexão RFC para o sistema de destino de saudação. configuração de saudação é uma configuração padrão do toohello semelhante de uma Conexão RFC.

Vamos supor que no cenário entre locais de hello, Olá VMs que executavam sistemas SAP que precisam toocommunicate uns com os outros estão em Olá mesmo domínio. Portanto hello instalação de uma conexão RFC entre os sistemas SAP não difere entradas em cenários locais e etapas de instalação de saudação.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Acessando compartilhamentos de arquivos 'locais' de instâncias SAP localizadas no Azure ou vice-versa
As instâncias SAP localizadas no Azure precisam tooaccess compartilhamentos de arquivos que estão nas instalações corporativas hello. Além disso, as instâncias SAP locais precisam tooaccess compartilhamentos de arquivos que estão localizados no Azure. compartilhamentos de arquivos de saudação tooenable você deve configurar permissões hello e opções de compartilhamento no sistema local hello. Certifique-se de que tooopen Olá portas Olá VPN ou conexão de rota expressa entre o Azure e seu datacenter.

## <a name="supportability"></a>Capacidade de suporte
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Solução de monitoramento do Azure para SAP
Em ordem tooenable Olá monitoramento de sistemas SAP essenciais no Azure Olá SAP ferramentas de monitoramento como SAPOSCOL e SAP Host Agent obtém dados de host de serviço de máquina Virtual do Azure Olá por meio de uma extensão de monitoramento do Azure para SAP. Como Olá demandas da SAP eram muito específicas tooSAP aplicativos, a Microsoft decidiu não toogenerically implementar Olá necessário funcionalidade no Azure, mas deixá-lo para os clientes toodeploy Olá necessário monitoramento componentes e as configurações tootheir Máquinas virtuais em execução no Azure. No entanto, implantação e o ciclo de vida do gerenciamento de saudação componentes de monitoramento será automatizado principalmente pelo Azure.

#### <a name="solution-design"></a>Design da solução
solução de saudação desenvolvida tooenable que monitoramento do SAP se baseia na arquitetura de saudação do agente de VM do Azure e do framework de extensão. ideia de saudação do framework de agente de VM do Azure e a extensão de saudação é tooallow instalação de aplicativos de software disponíveis na Galeria de extensão de VM do Azure hello dentro de uma máquina virtual. Olá princípio ideia por trás desse conceito é tooallow (em casos como Olá extensão de monitoramento do Azure para SAP), Olá implantação de funcionalidades especiais em uma configuração de VM e hello desse software no momento da implantação.

Desde fevereiro de 2014, hello 'Agente de VM do Azure' que permite a manipulação de extensões de VM do Azure específico dentro de saudação que VM é injetada em VMs do Windows por padrão na criação de VMs no hello Portal do Azure. No caso de Olá SUSE ou Red Hat Linux VM agent já é parte da imagem do Azure Marketplace. No caso de um seria carregar uma VM do Linux do agente de VM do local tooAzure Olá tem toobe instalado manualmente.

Olá blocos de construção básicos da solução de monitoramento de saudação no Azure para SAP tem esta aparência:

![Componentes de extensão do Microsoft Azure][planning-guide-figure-2400]

Conforme mostrado no diagrama de bloco Olá acima, uma parte da solução de monitoramento para SAP de saudação é hospedada no hello imagem de VM do Azure e Galeria de extensões do Azure que é um repositório global replicado gerenciado por operações do Azure. É responsabilidade de saudação da equipe SAP/MS conjunta Olá trabalhando Olá implementação do Azure do SAP toowork com operações do Azure toopublish novas versões do hello extensão de monitoramento do Azure para SAP. Essa extensão de monitoramento do Azure para SAP usará Olá extensão do Microsoft Azure WAD (Diagnóstico) ou do Linux Azure Diagnostics (LAD) tooget Olá informações necessárias.

Quando você implanta uma nova VM do Windows, Olá 'Agente de VM do Azure' é automaticamente adicionada ao Olá VM. função Hello desse agente é toocoordinate Olá carregamento e a configuração de saudação extensões do Azure para o monitoramento de sistemas SAP NetWeaver. Para VMs do Linux hello Azure VM Agent já é parte da imagem do sistema operacional do Azure Marketplace hello.

No entanto, há uma etapa que ainda precisa toobe executado pelo cliente de saudação. Isso é habilitação hello e a configuração de coleta de desempenho de saudação. processo de saudação relacionado toohello 'configuration' é automatizado por um script do PowerShell ou o comando CLI. Olá script do PowerShell pode ser baixado em Olá Microsoft Azure Script Center, conforme descrito em hello [guia de implantação][deployment-guide].

Olá arquitetura geral do hello Azure solução de monitoramento para SAP é semelhante a:

![Solução de monitoramento do Azure para SAP NetWeaver][planning-guide-figure-2500]

**Para Olá exatamente como-tooand para obter etapas detalhadas de como usar esses cmdlets do PowerShell ou o comando CLI durante as implantações, siga as instruções de saudação fornecidas em Olá [guia de implantação][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integração de instância SAP localizada no Azure ao SAProuter
Instâncias SAP em execução no Azure precisam toobe acessível a partir do SAProuter também.

![Conexão de rede de roteador SAP][planning-guide-figure-2600]

Um SAProuter permite a comunicação de TCP/IP de saudação entre os sistemas participantes se não houver nenhuma conexão IP direta. Isso fornece a vantagem de saudação que nenhuma conexão de ponta a ponta entre parceiros de comunicação de saudação é necessário no nível da rede. Olá SAProuter está escutando na porta 3299 por padrão.
instâncias de tooconnect SAP através de um SAProuter necessário toogive Olá cadeia de caracteres do SAProuter e o nome de host com qualquer tentativa de tooconnect.

## <a name="sap-netweaver-as-java"></a>Servidor de Aplicativos para Java do SAP NetWeaver
Até agora Olá foco Olá documento foi SAP NetWeaver em geral ou Olá pilha ABAP do SAP NetWeaver. Nesta pequena seção, considerações específicas para pilha Java do SAP de saudação são listadas. Uma saudação mais importante de que aplicativos Java do SAP NetWeaver exclusivamente com base é hello SAP Enterprise Portal. Outros SAP NetWeaver com base em aplicativos como SAP PI e o SAP Solution Manager usam Olá ABAP do SAP NetWeaver e pilhas de Java. Portanto, certamente há uma necessidade tooconsider aspectos específicos relacionados toohello Java do SAP NetWeaver pilha também.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
configuração de saudação de um SAP Portal em uma máquina Virtual do Azure não é a diferença entre uma instalação local em se você estiver implantando em cenários entre locais. Desde Olá que DNS é feito por local, configurações de porta de saudação de instâncias individuais do hello podem ser feitas como configurado no local. recomendações de saudação e restrições descritas neste documento até agora se aplicam para um aplicativo como o SAP Enterprise Portal ou a pilha de Java do SAP NetWeaver Olá em geral.

![Portal SAP exposto][planning-guide-figure-2700]

Um cenário de implantação especial por alguns clientes é a exposição direta Olá de saudação SAP Enterprise Portal toohello Internet enquanto host de máquina virtual de saudação é conectado toohello rede da empresa por meio do túnel VPN de site a site ou rota expressa. Para esse cenário, você deve ter toomake-se de que portas específicas são abertos e não está bloqueado por grupo de segurança de rede ou firewall. Olá mesma mecânica precisaria toobe aplicada quando você quiser tooconnect tooan SAP Java instância do local em um cenário somente em nuvem.

Olá URI inicial do portal é http:`<Portalserver`>: 5XX00/irj onde porta Olá é formada por mais de 50000 (número de sistema × 100). Olá padrão portal URI do sistema SAP 00 é `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Para obter mais detalhes, veja <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Configuração de ponto de extremidade][planning-guide-figure-2800]

Se você quiser toocustomize Olá URL e/ou as portas do seu SAP Enterprise Portal, consulte esta documentação:

* [Alterar URL do portal](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Alterar os Números de porta padrão, Números de porta do portal](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

<a name="7cf991a1-badd-40a9-944e-7baae842a058"></a>
## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>HA (alta disponibilidade) e DR (recuperação de desastre) para SAP NetWeaver em execução em máquinas virtuais do Azure
### <a name="definition-of-terminologies"></a>Definição de terminologias
Olá termo **alta disponibilidade (HA)** é geralmente relacionado tooa um conjunto de tecnologias que minimiza interrupções de IT, fornecendo a continuidade de negócios dos serviços de TI por meio de redundância, tolerantes a falhas ou componentes protegidos de failover dentro de saudação **mesmo** Centro de dados. Em nosso caso, dentro de uma Região do Azure.

**A DR (recuperação de desastre)** também está voltada para minimizar as interrupções dos serviços de TI e a recuperação de dados, mas em **diferentes** data centers, que estão normalmente localizados a centenas de quilômetros de distância. Em nosso caso geralmente entre diferentes regiões do Azure em Olá mesma região geopolíticas ou como definido por você, como um cliente.

### <a name="overview-of-high-availability"></a>Visão Geral de Alta Disponibilidade
Poderá Separamos discussão Olá sobre SAP alta disponibilidade no Azure em duas partes:

* **Alta disponibilidade da infraestrutura do Azure**, por exemplo, alta disponibilidade de computação (VMs), rede, armazenamento etc., e seus benefícios para aumentar a disponibilidade do aplicativo SAP.
* **Alta disponibilidade de aplicativos SAP**, por exemplo, alta disponibilidade de componentes de software SAP:
  * Servidores de aplicativos SAP
  * Instância ASCS/SCS SAP
  * servidor do BD

e como ele pode ser combinado com alta disponibilidade de infraestrutura do Azure.

Alta disponibilidade do SAP no Azure tem algumas tooSAP diferenças em comparação com alta disponibilidade em um ambiente do local físico ou virtual. Olá, documento a seguir da SAP descreve as configurações padrão de alta disponibilidade do SAP em ambientes virtualizados no Windows: <http://scn.sap.com/docs/DOC-44415>. Há não configuração de HA da SAP integrada com sapinst, para Linux, da mesma maneira que existe para o Windows. Em relação à alta disponibilidade local do SAP para Linux, encontre mais informações aqui: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Alta disponibilidade de infraestrutura do Azure
Não há nenhum SLA de VM única disponível em máquinas virtuais do Azure no momento. tooget uma ideia como disponibilidade de saudação de uma única VM pode parecer que você pode simplesmente criar produto Olá de Olá diferentes SLAs do Azure disponíveis: <https://azure.microsoft.com/support/legal/sla/>.

Base de saudação para cálculo de saudação é 30 dias por mês ou 43200 minutos. Portanto, 0,05% de tempo de inatividade corresponde too21.6 minutos. Como de costume, disponibilidade Olá serviços diferentes hello serão multiplicar em Olá maneira a seguir:

(Serviço de disponibilidade nº 1/100) * (Serviço de disponibilidade nº 2/100) * (Serviço de disponibilidade nº 3/100) *…

Assim como:

(99,95/100) * (99,9/100) * (99,9/100) = 0,9975 ou uma disponibilidade geral de 99,75%.

#### <a name="virtual-machine-vm-high-availability"></a>Alta disponibilidade de VM (máquina virtual)
Há dois tipos de eventos da plataforma Windows Azure que podem afetar a disponibilidade de saudação de suas máquinas virtuais: planejado de manutenção e a manutenção não planejada.

* Eventos de manutenção planejada são atualizações periódicas feitas pela Microsoft toohello subjacente a plataforma Windows Azure tooimprove geral confiabilidade, desempenho e segurança da infraestrutura de plataforma Olá que suas máquinas virtuais executadas em.
* Eventos de manutenção não planejados ocorrem quando a infraestrutura física subjacente sua máquina virtual ou hardware de saudação apresentou falha de alguma forma. Isso inclui falhas na rede local, falhas no disco local ou outras falhas no nível de rack. Quando uma falha é detectada, Olá plataforma Windows Azure migrará automaticamente sua máquina virtual de servidor físico não íntegro Olá sua máquinas virtuais tooa Íntegro físico no servidor de hospedagem. Esses eventos são raros, mas também podem causar tooreboot sua máquina virtual.

Mais detalhes podem ser encontrados nesta documentação: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Redundância de Armazenamento do Azure
dados Olá na sua conta de armazenamento do Microsoft Azure são sempre replicado tooensure durabilidade e alta disponibilidade, Olá SLA de armazenamento do Azure, mesmo em face de saudação de falhas de hardware transitória de reunião

Como o armazenamento do Azure está se comportando 3 imagens dos dados Olá por padrão, RAID5 ou RAID1 em vários discos do Azure não são necessárias.

Mais detalhes podem ser encontrados neste artigo: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Utilizando o Azure infraestrutura VM reiniciar tooAchieve "Maior disponibilidade" de aplicativos SAP
Se você decidir não toouse funcionalidades como o Windows Server Failover Clustering (WSFC) ou um equivalente do Linux (Olá último uma ainda não é suportada no Azure em combinação com o software SAP), o Azure VM reiniciar utilizada tooprotect um sistema SAP em planejado e tempo de inatividade não planejado de infraestrutura de servidor físico do Azure hello e global da plataforma subjacente do Azure.

> [!NOTE]
> É importante toomention que principalmente Azure VM reiniciar protege as máquinas virtuais e não aplicativos. A Reinicialização de VM não oferece alta disponibilidade para aplicativos SAP, mas oferece um certo nível de disponibilidade da infraestrutura e, portanto, indiretamente, "maior disponibilidade" de sistemas SAP. Também há um SLA para tempo de saudação levará toorestart uma VM após uma interrupção planejada ou não planejada de host. Portanto, esse método de 'alta disponibilidade' não é adequado para componentes críticos de um sistema SAP como (A)SCS ou DBMS.
>
>

Outro elemento de infraestrutura importante para alta disponibilidade é o armazenamento. Por exemplo O SLA do Armazenamento do Azure tem disponibilidade de 99,9%. Se alguém implantar todas as VMs com seus discos em uma única Conta de Armazenamento do Azure, a indisponibilidade potencial do Armazenamento do Azure causará indisponibilidade de todas as VMs localizadas na Conta de Armazenamento do Azure e também de todos os componentes SAP em execução dentro dessas VMs.  

Em vez de colocar todas as VMs em uma única Conta de Armazenamento do Azure, você também pode contas de armazenamento dedicado para cada VM e, dessa forma, aumentar a disponibilidade geral da VM e do aplicativo SAP usando várias Contas de Armazenamento do Azure independentes.

Uma arquitetura de exemplo de um sistema SAP NetWeaver que usa alta disponibilidade de infraestrutura do Azure poderia ter esta aparência:

![Utilizando a infraestrutura do Azure HA tooachieve SAP "superior" da disponibilidade de aplicativos][planning-guide-figure-2900]

Para componentes essenciais do SAP é obtida Olá até a seguir:

* Alta disponibilidade de servidores de aplicativos (SA) SAP

As instâncias do servidor de aplicativos SAP são componentes redundantes. Cada instância de SA SAP está implantada em sua própria VM, que está em execução em um domínio de falha e de atualização diferente do Azure (confira os capítulos [Domínios de falha][planning-guide-3.2.1] e [Domínios de atualização][planning-guide-3.2.2]). Isso é garantido pelo uso de Conjuntos de Disponibilidade do Azure (confira o capítulo [Conjuntos de disponibilidade do Azure][planning-guide-3.2.3]). Potencial indisponibilidade planejada ou não planejada de um domínio de falha ou atualização do Azure causará indisponibilidade de um número restrito de VMs com suas instâncias SAP.
Cada instância de SA SAP será colocada em sua própria conta de Armazenamento do Azure – a indisponibilidade potencial de uma Conta de Armazenamento do Azure causará indisponibilidade de apenas uma VM com sua instância de SA SAP. No entanto, lembre-se de que há um limite de Contas de Armazenamento do Azure dentro de uma assinatura do Azure. tooensure de início automático de instância (A) SCS após reinicializar Olá VM, certifique-se de parâmetro de Autostart tooset na instância (A) SCS iniciar perfil descrita nos capítulos [usando Autostart para instâncias SAP][planning-guide-11.5].
Leia também o capítulo [Alta disponibilidade para servidores de aplicativos SAP][planning-guide-11.4.1] para obter mais detalhes.

* *Maior* disponibilidade de instância do (A)SCS SAP

Aqui, utilizamos Azure VM reiniciar Olá tooprotect VM com a instância do SAP (A) SCS instalada. Em hello caso de tempo de inatividade planejado ou não planejado do Azure os servidores, máquinas virtuais serão reiniciados em outro servidor disponível. Como mencionado anteriormente, principalmente Azure VM reiniciar protege VMs e não aplicativos, nesse caso, Olá instância (A) SCS. Por meio de saudação VM reiniciar entraremos em contato indiretamente "maior disponibilidade" da instância SAP (A) SCS. tooinsure de início automático de instância (A) SCS após reinicializar Olá VM, certifique-se de parâmetro de Autostart tooset na instância (A) SCS iniciar perfil descrita nos capítulos [usando Autostart para instâncias SAP][planning-guide-11.5]. Isso significa que hello (A) SCS executando como um único ponto de falha (SPOF) em uma única VM será o fator determinante Olá disponibilidade Olá de toda a estrutura SAP hello.

* *Maior* disponibilidade de servidor DBMS

Aqui, caso de uso de instância de SAP (A) SCS toohello semelhante, utilizamos Azure VM reiniciar Olá tooprotect VM com o software instalado do DBMS e atingir "disponibilidade" de software DBMS por meio de VM reiniciar.
DBMS em execução em uma única VM também é um SPOF e é o fator determinante Olá disponibilidade Olá de toda a estrutura SAP hello.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Alta disponibilidade de aplicativo SAP no Azure IaaS
tooachieve completo SAP alta disponibilidade do sistema, precisamos tooprotect todos os componentes essenciais do sistema SAP, servidores de aplicativos SAP, por exemplo, redundância, e os componentes exclusivos (por exemplo, ponto único de falha), como a instância do SAP (A) SCS e DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Alta disponibilidade para servidores de aplicativos SAP
Para instâncias de caixa de diálogo/servidores de aplicativo hello SAP não é necessário toothink sobre uma solução de alta disponibilidade específicas. A alta disponibilidade é obtida simplesmente pela redundância e, portanto, pela existência de um número suficiente deles em máquinas virtuais diferentes. Eles devem todos ser colocados em Olá tooavoid mesmo conjunto de disponibilidade do Azure que Olá VMs pode ser atualizado no hello mesmo tempo durante o tempo de inatividade de manutenção planejada. funcionalidade básica de saudação que tem como base diferente de atualização e domínios de falha em uma unidade de escala do Azure já foi introduzida no capítulo [atualizar domínios][planning-guide-3.2.2]. Conjuntos de Disponibilidade do Azure foram apresentados no capítulo [Conjuntos de disponibilidade do Azure][planning-guide-3.2.3] deste documento.

Não há um número infinito de domínios de falha e atualização que possam ser usados por um conjunto de disponibilidade do Azure em uma unidade de escala do Azure. Isso significa que colocar um número de VMs em um conjunto de disponibilidade mais cedo ou mais tarde no fato de saudação que mais de uma VM termina em Olá mesmo falha ou atualização do domínio

Implantação de servidor de aplicativos SAP algumas instâncias em suas máquinas virtuais dedicadas e supondo que obtivemos 5 domínios de atualização, Olá figura abaixo surge no final da saudação. Olá máximo número de domínios de falha e atualização dentro de um conjunto de disponibilidade pode ser alteradas em futuras de saudação:

![Alta disponibilidade dos servidores de aplicativos SAP no Azure][planning-guide-figure-3000]

Mais detalhes podem ser encontrados nesta documentação: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Alta disponibilidade para a instância do SAP (A) SCS Olá no Windows
Windows Server Failover Cluster (WSFC) é uma instância de SAP (A) SCS de saudação de tooprotect de solução usados com frequência. Ele também é integrado ao sapinst na forma de uma "instalação de alta disponibilidade". Neste momento Olá infraestrutura do Azure não é capaz de tooprovide Olá funcionalidade tooset a saudação de Cluster de Failover do Windows Server Olá necessário mesma maneira que é feito no local.

A partir de janeiro de 2016 plataforma de nuvem do Azure Olá executando o sistema de operacional do Windows hello não oferece a possibilidade de saudação do uso de um volume compartilhado de cluster em um disco compartilhado entre duas VMs do Azure.

Uma solução válida embora é o uso de saudação do software de terceiros 3º que oferece um volume compartilhado pela replicação síncrona e transparente de disco que pode ser integrada no WSFC. Essa abordagem significa que esse nó de cluster ativo Olá somente é possível tooaccess um disco Olá copia em um ponto no tempo. A partir de janeiro de 2016 este HA configuração é instância de SAP (A) SCS Olá tooprotect com suporte no sistema operacional Windows convidado em máquinas virtuais do Azure em combinação com o software de terceiros para o 3º SIOS DataKeeper.

Olá SIOS DataKeeper solução fornece um tooWindows de recurso de cluster de disco compartilhado Clusters de Failover por ter:

* Um VHD do Azure adicionais anexado tooeach de saudação máquinas virtuais (VMs) estão em uma configuração de Cluster do Windows
* A Edição de Cluster do SIOS DataKeeper em execução em ambos os nós de VM
* Tendo SIOS DataKeeper Cluster Edition está configurado de forma que ele sincronicamente espelha conteúdo Olá Olá adicional VHD anexado volume VMs tooadditional VHD anexado do volume de origem de VM de destino.
* SIOS DataKeeper é abstrair os volumes de local origem e destino hello e apresentar tooWindows Cluster de Failover como um único disco compartilhado.

Você pode encontrar todos os detalhes sobre como tooinstall um Cluster de Failover do Windows com SIOS Datakeeper e SAP em Olá [Clustering da instância SAP ASCS usando o Cluster de Failover do Windows Server no Azure com SIOS DataKeeper] [ ha-guide-classic]white paper.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Alta disponibilidade para a instância do SAP (A) SCS Olá no Linux
A partir de dezembro de 2015 também há um disco de tooshared equivalente WSFC para VMs do Linux no Azure. Soluções alternativas usando software de terceiros como SIOS para Windows ainda não são validadas para execução da SAP em Linux no Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Alta disponibilidade para a instância de banco de dados do SAP Olá
Olá SAP DBMS HA instalação típica baseia-se em duas VMs de DBMS em que a funcionalidade de alta disponibilidade DBMS é usada tooreplicate dados Olá active DBMS instância toohello segundo VM em uma instância de DBMS passiva.

Alta funcionalidade de recuperação de desastres e disponibilidade de DBMS em geral, bem como específicos de DBMS são descritos em Olá [guia de implantação de DBMS][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Alta disponibilidade de ponta a ponta para Olá completa do sistema SAP
Aqui estão dois exemplos de uma arquitetura de alta disponibilidade SAP NetWeaver completa no Azure - um para Windows e outro para Linux.
conceitos de saudação conforme explicado a seguir podem ser necessário toobe um pouco comprometida quando você implanta vários sistemas SAP e número de saudação de VMs implantadas é excedendo o limite máximo Olá de contas de armazenamento por assinatura. Nesses casos, os VHDs de VMs necessário toobe combinado dentro de uma conta de armazenamento. Normalmente você faria isso pela combinação de VHDs de VMs das camadas de aplicativo SAP de sistemas SAP diferentes.  Também combinamos diferentes VHDs de diferentes VMs DBMS de sistemas SAP diferentes em uma conta de armazenamento do Azure. Mantendo os limites de IOPS de saudação de contas de armazenamento do Azure em mente ( <https://azure.microsoft.com/documentation/articles/storage-scalability-targets> )

##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] no Windows
![Arquitetura de alta disponibilidade de aplicativos SAP NetWeaver com o SQL Server no Azure IaaS][planning-guide-figure-3200]

Hello Azure construções a seguir é usada para sistema do SAP NetWeaver hello, impacto toominimize por problemas de infraestrutura e patches do host:

* sistema completo de saudação é implantado no Azure (obrigatório: Olá a camada de DBMS, (A) instância SCS e aplicativo completo camada necessidade toorun no mesmo local).
* sistema completo Olá é executado em uma assinatura do Azure (obrigatória).
* sistema completo Olá é executado em uma rede Virtual do Azure (obrigatório).
* é possível separar a saudação da saudação VMs de um sistema SAP em três conjuntos de disponibilidade mesmo com todas as VMs Olá pertencentes toohello mesma rede Virtual.
* Todas as VMs que executam instâncias DBMS de um sistema SAP estão em um conjunto de disponibilidade. Presumimos que haja mais de uma VM executando instâncias de DBMS por sistema, já que recursos nativos de alta disponibilidade de DBMS são usados, como o SQL Server AlwaysOn ou o Oracle Data Guard.
* Todas as VMs que executam instâncias de DBMS usam sua própria conta de armazenamento. Arquivos de log e dados DBMS são replicados de uma conta de armazenamento tooanother de armazenamento de conta, usando as funções de alta disponibilidade DBMS que sincroniza dados hello. Indisponibilidade de uma conta de armazenamento fará com que a indisponibilidade de um nó de cluster do Windows do SQL, mas não Olá todo serviço do SQL Server.
* Todas as VMs que executam uma instância do (A)SCS de um sistema SAP estão em um conjunto de disponibilidade. Dentro dessas VMs é configurar a instância do Windows Server Failover Cluster (WSFC) tooprotect (A) SCS.
* Todas as VMs que executam instâncias do (A)SCS usam sua própria conta de armazenamento. (A) Arquivos de instância SCS e pasta global do SAP são replicadas de uma conta de armazenamento tooanother de armazenamento de conta, usando a replicação SIOS DataKeeper. Indisponibilidade de uma conta de armazenamento causará indisponibilidade de um (A) SCS Windows nó de cluster, mas não Olá todo serviço (A) SCS.
* Todas as VMs de saudação que representa a camada do servidor de aplicativo hello SAP estão em um terceiro conjunto de disponibilidade.
* Todas as VMs Olá executando servidores de aplicativos SAP usam sua própria conta de armazenamento. Indisponibilidade de uma conta de armazenamento fará com que a indisponibilidade de um servidor de aplicativos SAP, em que AS outras SAP continuar toorun.

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] no Linux
arquitetura de saudação do SAP de HA em Linux no Azure é basicamente hello, mesmo que o Windows como descrito acima. Desde janeiro de 2016, porém, há duas restrições:

* somente o SAP ASE 16 tem suporte atualmente no Azure em Linux sem nenhum recurso de replicação do ASE.
* ainda não há uma solução de alta disponibilidade do (A)SCS SAP com suporte no Azure em Linux

Como consequência como de janeiro de 2016 não pode obter um sistema SAP-Linux-Azure Olá disponibilidade mesmo como um sistema SAP-Windows-Azure devido à ausência de HA para instância do hello (A) SCS e Olá banco de dados de SAP ASE de instância única.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Usando a inicialização automática para instâncias SAP
SAP oferecido funcionalidade Olá toostart as instâncias SAP imediatamente após o início de saudação do hello SO na VM de saudação. as etapas exatas Olá documentadas no artigo da Base de dados de Conhecimento SAP [1909114] - como toostart SAP instâncias usando o parâmetro Autostart automaticamente. No entanto, SAP não recomendamos toouse hello mais configuração porque não há nenhum controle na ordem de saudação de reinicializações de instância, supondo que mais de uma máquina virtual foi afetada ou várias instâncias foi executado por VM. Supondo que um cenário típico do Azure de uma instância do servidor de aplicativos SAP em caso de uma única VM eventualmente obtendo reiniciado VM e hello, hello Autostart não é mais importante e pode ser habilitada adicionando este parâmetro:

    Autostart = 1

Em Olá iniciar o perfil da instância SAP ABAP e/ou Java de saudação.

> [!NOTE]
> parâmetro Autostart de saudação pode ter algumas dificuldades também. Mais detalhadamente, gatilhos de parâmetro Olá Olá início de uma instância SAP ABAP ou Java quando Olá relacionados ao serviço do Windows/Linux da instância de saudação é iniciado. Que certamente é o caso de Olá quando os sistemas operacionais de saudação é inicializado. No entanto, reinicializações de serviços SAP também são uma coisa comum para a funcionalidade de gerenciamento de ciclo de vida do Software SAP, como SUM ou outras atualizações. Essas funcionalidades não estiver esperando um toobe instância reiniciado automaticamente em todos os. Portanto, o parâmetro Autostart de saudação deve ser desabilitado antes de executar essas tarefas. Olá Autostart parâmetro também não deve ser usado para instâncias SAP que estão agrupadas, como ASCS/SCS/CI.
>
>

Consulte informações adicionais sobre a inicialização automática para instâncias SAP aqui:

* [Iniciar/parar SAP ao iniciar/parar seu servidor Unix](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Iniciando e parando agentes de gerenciamento do SAP NetWeaver](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Como tooenable automaticamente Iniciar do HANA banco de dados](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Sistemas SAP maiores de 3 camadas
Aspectos de alta disponibilidade de configurações SAP de 3 camadas já foram discutidos nas seções anteriores. Mas e quanto a sistemas em que são muito grandes requisitos do servidor DBMS Olá toohave localizados no Azure, mas a camada do aplicativo SAP Olá pode ser implantada no Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Localização de configurações SAP de 3 camadas
Não é camada de aplicativo de saudação toosplit com suporte em si ou aplicativo hello e camada DBMS entre local e o Azure. Um sistema SAP é completamente implantado localmente OU no Azure. Também não é suportada toohave alguns dos servidores de aplicativo hello execução local e outros no Azure. Que é hello ponto inicial da discussão hello. Também não oferece suporte a componentes DBMS Olá toohave de um sistema SAP e Olá camada do servidor de aplicativo SAP implantada em duas regiões diferentes do Azure. Por exemplo DBMS no Oeste dos EUA e camada de aplicativo SAP nos EUA Central. Razão para não dar suporte a essas configurações é sensibilidade de latência de saudação do hello arquitetura do SAP NetWeaver.

No entanto, longo Olá de dados do último ano parceiros center desenvolvida locais colegas tooAzure regiões. Esses locais colegas geralmente são nos dados do Azure do muito próximos toohello físico centers dentro de uma região do Azure. curta distância de saudação e conexão de ativos no hello colocalização por meio de rota expressa no Azure podem resultar em uma latência que é menor que 2 ms. Nesses casos, é possível toolocate Olá camada de DBMS (incluindo o armazenamento SAN/NAS) em uma localização conjunta e camada de aplicativo hello SAP no Azure. Desde dezembro de 2015, não temos nenhuma implantação desse tipo. Mas diferentes clientes com implantações de aplicativos não SAP já estão usando essas abordagens.

### <a name="offline-backup-of-sap-systems"></a>Backup offline de sistemas SAP
Dependente de saudação configuração SAP escolhida (2 ou 3 camadas), há possível toobackup uma necessidade. conteúdo Olá Olá própria VM mais toohave um backup de banco de dados de saudação. Olá DBMS relacionados a backups são esperado toobe feito com métodos de banco de dados. Uma descrição detalhada para bancos de dados diferentes hello, pode ser encontrada em [guia DBMS][dbms-guide]. Em Olá outro lado, Olá dados SAP poderá ser feito backup de uma maneira offline (incluindo o conteúdo do banco de dados Olá também) conforme descrito nesta seção, ou online, conforme descrito na próxima seção, Olá.

backup offline Olá basicamente exigiria um desligamento da saudação VM por meio de saudação Portal do Azure e uma cópia do disco VM base hello mais todos anexado VHDs toohello VM. Isso seria preservar um ponto na imagem de tempo de saudação VM e seus discos associados. É recomendável toocopy hello "backups" em uma conta de armazenamento do Azure diferente. Olá, portanto, o procedimento descrito no capítulo [copiando discos entre contas de armazenamento do Azure] [ planning-guide-5.4.2] deste documento seria aplicável.
Além de hello desligamento usando Olá Portal do Azure uma também poderá fazer isso por meio do Powershell ou CLI conforme descrito aqui: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Uma restauração de estado consistem excluindo Olá VM de base, bem como discos originais de saudação da saudação base da VM e VHDs montados, copiando back Olá salvo VHDs toohello conta de armazenamento original e, em seguida, reimplantar Olá sistema.
Este artigo mostra um exemplo de como tooscript esse processo no Powershell: <http://www.westerndevs.com/azure-snapshots/>

Verifique tooinstall-se de que uma nova licença SAP como restoing um backup VM conforme descrito acima cria uma nova chave de hardware.

### <a name="online-backup-of-an-sap-system"></a>Backup online de um sistema SAP
Backup de saudação DBMS é executado com métodos específicos de DBMS conforme descrito em hello [guia DBMS][dbms-guide].

Outras VMs no sistema SAP de saudação podem ser feitos usando a funcionalidade de Backup de máquinas virtuais do Azure. Backup de máquinas virtuais do Azure foi introduzido no início de 2015 e enquanto isso é um método padrão toobackup uma VM completa no Azure. O Backup do Azure armazena backups Olá no Azure e permite uma restauração de uma máquina virtual novamente.

> [!NOTE]
> A partir de dezembro de 2015 usando o Backup de VM não manter Olá exclusivo VM ID que é usado para SAP de licenciamento. Isso significa que uma restauração de um backup VM exige a instalação de uma nova chave de licença do SAP como Olá restaurada VM é considerada toobe uma nova VM e não uma substituição de um antigo que foi salvo.
> Desde janeiro de 2016, o Backup da VM do Azure ainda não dá suporte às VMs que são implantadas com o Azure Resource Manager.
>
> ![Windows][Logo_Windows] Windows
>
> Teoricamente VMs que bancos de dados de execução poderá ser feitos backup de uma maneira consistente também se dá suporte a sistemas DBMS Olá Olá Windows VSS (serviço de cópias de sombra de Volume <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx > ) como, por exemplo, SQL Server.
> No entanto, lembre-se de que com base nos backups de VM do Azure, as restaurações pontuais não são possíveis. Portanto, a recomendação é tooperform backups de bancos de dados com a funcionalidade DBMS em vez de depender do Backup de VM do Azure
>
> tooget familiarizado com o Backup de máquinas virtuais do Azure, comece aqui: <https://azure.microsoft.com/documentation/articles/backup-azure-vms/>.
>
> Outras possibilidades são toouse uma combinação do Microsoft Data Protection Manager é instalado em uma máquina virtual do Azure e o Azure Backup para backup/restauração de bancos de dados. Mais informações podem ser encontradas aqui: <https://azure.microsoft.com/documentation/articles/backup-azure-dpm-introduction/>.  
>
> ![Linux][Logo_Linux] Linux
>
> Não há nenhum equivalente tooWindows VSS no Linux. Portanto, apenas backups consistentes com arquivo são possíveis, enquanto os consistentes com aplicativo não são. Olá SAP DBMS deve ser feito backup usando a funcionalidade DBMS. Olá sistema de arquivos que inclui Olá SAP relacionados dados podem ser salvos, por exemplo, usando o arquivo tar conforme descrito aqui: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure como local de recuperação de desastre para estruturas da SAP de produção
Desde meados de 2014, componentes toovarious extensões Hyper-V, o System Center e o Azure habilitar uso de saudação do Azure como local de DR para VMs em execução com base no Hyper-V no local.

Um blog detalhando como toodeploy essa solução é documentado aqui: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>

## <a name="summary"></a>Resumo
Olá pontos principais de alta disponibilidade para sistemas SAP no Azure são:

* Neste momento, Olá ponto de falha único SAP não pode ser protegido exatamente Olá mesma maneira que ele pode ser feito em implantações locais. motivo de saudação é que os clusters de discos compartilhados ainda não podem ser criados no Azure sem o uso de saudação do 3º softwares de terceiros.
* Para a camada de DBMS Olá você precisa de funcionalidade DBMS toouse que não dependem da tecnologia de cluster de disco compartilhado. Mais detalhes estão documentados no hello [guia DBMS][dbms-guide].
* impacto de saudação toominimize de problemas em domínios de falha no hello manutenção de host ou de infraestrutura do Azure, você deve usar conjuntos de disponibilidade do Azure:
  * É recomendável toohave um conjunto de disponibilidade para a camada do aplicativo SAP hello.
  * É recomendável toohave uma disponibilidade separado definida para a camada de DBMS SAP hello.
  * NÃO é recomendável Olá tooapply que conjunto de disponibilidade mesmo para VMs de sistemas SAP diferentes.
* Para fins de Backup da camada de DBMS SAP hello, verifique Olá [guia DBMS][dbms-guide].
* Fazendo backup de instâncias de diálogo SAP faz pouco sentido, pois ela é normalmente mais rápidas instâncias de diálogo simples tooredeploy.
* Backup Olá VM que contém o diretório global de saudação do hello sistema SAP e com ele todos os perfis de saudação de instâncias diferentes do hello, faz sentido e deve ser realizado com o Backup do Windows ou tar, por exemplo, no Linux. Como há diferenças entre o Windows Server 2008 (R2) e o Windows Server 2012 (R2), que torna mais fácil toobackup usando hello mais recente versões do Windows Server, é recomendável toorun Windows Server 2012 (R2) como o sistema operacional Windows.
