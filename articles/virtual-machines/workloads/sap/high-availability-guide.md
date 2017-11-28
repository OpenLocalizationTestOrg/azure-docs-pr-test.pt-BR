---
title: "aaaAzure alta disponibilidade de máquinas virtuais para o SAP NetWeaver | Microsoft Docs"
description: "Guia de alta disponibilidade do SAP NetWeaver em máquinas virtuais do Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/07/2016
ms.author: goraco
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 927409830065573248a43427eb382448ca07b6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms"></a><span data-ttu-id="23c37-103">Alta disponibilidade do SAP NetWeaver em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-103">High availability for SAP NetWeaver on Azure VMs</span></span>

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

[sap-installation-guides]:http://service.sap.com/instguides

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:https://docs.microsoft.com/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md
[dbms-guide-2.1]:../../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:../../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:../../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:../../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:../../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:../../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:../../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:../../virtual-machines-windows-sap-deployment-guide.md
[deployment-guide-2.2]:../../virtual-machines-windows-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:../../virtual-machines-windows-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:../../virtual-machines-windows-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:../../virtual-machines-windows-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:../../virtual-machines-windows-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:../../virtual-machines-windows-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:../../virtual-machines-windows-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:../../virtual-machines-windows-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:../../virtual-machines-windows-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:../../virtual-machines-windows-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:../../virtual-machines-windows-sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:../../virtual-machines-windows-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:../../virtual-machines-windows-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:../../virtual-machines-windows-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:../../virtual-machines-windows-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:../../virtual-machines-windows-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:../../virtual-machines-windows-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:../../virtual-machines-windows-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:../../virtual-machines-windows-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:../../virtual-machines-windows-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:../../virtual-machines-windows-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:../../virtual-machines-windows-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:../../virtual-machines-windows-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:../../virtual-machines-windows-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:../../virtual-machines-windows-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:../../virtual-machines-windows-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:../../virtual-machines-windows-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:../../virtual-machines-windows-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../../../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../../../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:../../virtual-machines-windows-sap-get-started.md
[getting-started-dbms]:../../virtual-machines-windows-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:../../virtual-machines-windows-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:../../virtual-machines-windows-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:high-availability-guide.md
[sap-ha-guide-1]:high-availability-guide.md#217c5479-5595-4cd8-870d-15ab00d4f84c
[sap-ha-guide-2]:high-availability-guide.md#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-3]:high-availability-guide.md#42156640c6-01cf-45a9-b225-4baa678b24f1
[sap-ha-guide-3.1]:high-availability-guide.md#f76af273-1993-4d83-b12d-65deeae23686
[sap-ha-guide-3.2]:high-availability-guide.md#3e85fbe0-84b1-4892-87af-d9b65ff91860
[sap-ha-guide-4]:high-availability-guide.md#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-4.1]:high-availability-guide.md#1a3c5408-b168-46d6-99f5-4219ad1b1ff2
[sap-ha-guide-5]:high-availability-guide.md#fdfee875-6e66-483a-a343-14bbaee33275
[sap-ha-guide-5.1]:high-availability-guide.md#be21cf3e-fb01-402b-9955-54fbecf66592
[sap-ha-guide-5.2]:high-availability-guide.md#ff7a9a06-2bc5-4b20-860a-46cdb44669cd
[sap-ha-guide-6]:high-availability-guide.md#2ddba413-a7f5-4e4e-9a51-87908879c10a
[sap-ha-guide-6.1]:high-availability-guide.md#1a464091-922b-48d7-9d08-7cecf757f341
[sap-ha-guide-6.2]:high-availability-guide.md#44641e18-a94e-431f-95ff-303ab65e0bcb
[sap-ha-guide-7]:high-availability-guide.md#2e3fec50-241e-441b-8708-0b1864f66dfa
[sap-ha-guide-7.1]:high-availability-guide.md#93faa747-907e-440a-b00a-1ae0a89b1c0e
[sap-ha-guide-7.2]:high-availability-guide.md#f559c285-ee68-4eec-add1-f60fe7b978db
[sap-ha-guide-7.2.1]:high-availability-guide.md#b5b1fd0b-1db4-4d49-9162-de07a0132a51
[sap-ha-guide-7.3]:high-availability-guide.md#ddd878a0-9c2f-4b8e-8968-26ce60be1027
[sap-ha-guide-7.4]:high-availability-guide.md#045252ed-0277-4fc8-8f46-c5a29694a816
[sap-ha-guide-8]:high-availability-guide.md#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:high-availability-guide.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.2]:high-availability-guide.md#7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310
[sap-ha-guide-8.3]:high-availability-guide.md#47d5300a-a830-41d4-83dd-1a0d1ffdbe6a
[sap-ha-guide-8.4]:high-availability-guide.md#b22d7b3b-4343-40ff-a319-097e13f62f9e
[sap-ha-guide-8.5]:high-availability-guide.md#9fbd43c0-5850-4965-9726-2a921d85d73f
[sap-ha-guide-8.6]:high-availability-guide.md#84c019fe-8c58-4dac-9e54-173efd4b2c30
[sap-ha-guide-8.7]:high-availability-guide.md#7a8f3e9b-0624-4051-9e41-b73fff816a9e
[sap-ha-guide-8.8]:high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.9]:high-availability-guide.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.10]:high-availability-guide.md#e69e9a34-4601-47a3-a41c-d2e11c626c0c
[sap-ha-guide-8.11]:high-availability-guide.md#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:high-availability-guide.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:high-availability-guide.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.2]:high-availability-guide.md#e49a4529-50c9-4dcf-bde7-15a0c21d21ca
[sap-ha-guide-8.12.2.1]:high-availability-guide.md#06260b30-d697-4c4d-b1c9-d22c0bd64855
[sap-ha-guide-8.12.2.2]:high-availability-guide.md#4c08c387-78a0-46b1-9d27-b497b08cac3d
[sap-ha-guide-8.12.3]:high-availability-guide.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:high-availability-guide.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:high-availability-guide.md#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-ha-guide-9.1.2]:high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0
[sap-ha-guide-9.1.3]:high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-ha-guide-9.1.4]:high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-ha-guide-9.1.5]:high-availability-guide.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-ha-guide-9.2]:high-availability-guide.md#85d78414-b21d-4097-92b6-34d8bcb724b7
[sap-ha-guide-9.3]:high-availability-guide.md#8a276e16-f507-4071-b829-cdc0a4d36748
[sap-ha-guide-9.4]:high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-ha-guide-9.5]:high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5
[sap-ha-guide-9.6]:high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772
[sap-ha-guide-10]:high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9
[sap-ha-guide-10.1]:high-availability-guide.md#65fdef0f-9f94-41f9-b314-ea45bbfea445
[sap-ha-guide-10.2]:high-availability-guide.md#5e959fa9-8fcd-49e5-a12c-37f6ba07b916
[sap-ha-guide-10.3]:high-availability-guide.md#755a6b93-0099-4533-9f6d-5c9a613878b5

[sap-ha-multi-sid-guide]:high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
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
[virtual-machines-windows-attach-disk-portal]:../../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../azure-resource-manager/resource-group-overview.md
[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../virtual-machines-windows-sizes.md
[virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md
[virtual-machines-windows-portal-sql-alwayson-int-listener]:../../windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md
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
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md


<span data-ttu-id="23c37-109">Máquinas virtuais do Azure é a solução de hello para empresas que precisam de computação, armazenamento e recursos de rede, no mínimo de tempo e sem ciclos de compra longos.</span><span class="sxs-lookup"><span data-stu-id="23c37-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="23c37-110">Você pode usar máquinas virtuais do Azure toodeploy clássico aplicativos como ABAP baseados no SAP NetWeaver, Java e uma pilha ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="23c37-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="23c37-111">Estenda a confiabilidade e a disponibilidade sem recursos locais adicionais.</span><span class="sxs-lookup"><span data-stu-id="23c37-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="23c37-112">As Máquinas Virtuais do Azure dão suporte à conectividade entre locais, o que permite que você integre as Máquinas Virtuais do Azure aos seus domínios locais, a nuvens privadas e à estrutura do sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="23c37-113">Neste artigo, abordaremos Olá etapas que toodeploy sistemas SAP de alta disponibilidade no Azure usando o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="23c37-114">Vamos percorrer estas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="23c37-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="23c37-115">Localize Olá direita guias Observações sobre o SAP e a instalação, listados em hello [recursos] [ sap-ha-guide-2] seção.</span><span class="sxs-lookup"><span data-stu-id="23c37-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="23c37-116">Este artigo complementa a documentação de instalação do SAP e observações sobre o SAP, que são Olá recursos principais que podem ajudá-lo a instalar e implantar o software SAP em plataformas específicas.</span><span class="sxs-lookup"><span data-stu-id="23c37-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="23c37-117">Conhecer as diferenças de saudação entre o modelo de implantação do Azure Resource Manager hello e modelo de implantação clássico do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="23c37-118">Saiba mais sobre os modos de quorum de cluster de Failover do Windows Server, para que você pode selecionar modelo de saudação que é ideal para sua implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="23c37-119">Aprenda sobre o armazenamento compartilhado do Windows Server Failover Clustering nos serviços Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="23c37-120">Saiba como toohelp proteger os componentes de ponto único de falha como avançado Business aplicativo programação (ABAP) SAP Central Services (ASCS) / SAP Central Services (SCS) e sistemas de gerenciamento de banco de dados (DBMS) e componentes redundantes, como SAP Servidor de aplicativos, no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="23c37-121">Execute um exemplo passo a passo da instalação e configuração de um sistema SAP de alta disponibilidade em um cluster do Clustering de Failover do Windows Server no o Azure usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="23c37-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="23c37-122">Saiba mais sobre toouse necessárias etapas adicionais, Clustering de Failover do Windows Server no Azure, mas que não são necessários em uma implantação local.</span><span class="sxs-lookup"><span data-stu-id="23c37-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="23c37-123">toosimplify implantação e configuração, neste artigo, usamos Olá modelos do Gerenciador de recursos de alta disponibilidade do SAP de três camadas.</span><span class="sxs-lookup"><span data-stu-id="23c37-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="23c37-124">modelos de saudação automatizam a implantação de saudação toda a infraestrutura que você precisa para um sistema SAP de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="23c37-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="23c37-125">infraestrutura de saudação também dá suporte a dimensionamento do SAP aplicativo desempenho padrão (SAPS) de seu sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="23c37-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23c37-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="23c37-127">Antes de começar, certifique-se de que você atenda aos pré-requisitos de saudação descritos nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="23c37-128">Além disso, ser toocheck-se de que todos os recursos listados em Olá [recursos] [ sap-ha-guide-2] seção.</span><span class="sxs-lookup"><span data-stu-id="23c37-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="23c37-129">Neste artigo, nós usamos modelos do Resource Manager para [SAP Netweaver de três camadas](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span><span class="sxs-lookup"><span data-stu-id="23c37-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image/).</span></span> <span data-ttu-id="23c37-130">Para uma visão geral dos modelos, confira [Modelos do Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="23c37-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="23c37-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos</span><span class="sxs-lookup"><span data-stu-id="23c37-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="23c37-132">Esses artigos abordam implantações SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="23c37-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="23c37-133">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="23c37-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="23c37-134">[Implantação de Máquinas Virtuais do Azure para SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="23c37-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="23c37-135">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="23c37-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="23c37-136">[Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver (este guia)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="23c37-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-137">Sempre que possível, podemos dar uma toohello link referindo-se o guia de instalação do SAP (consulte Olá [guias de instalação do SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="23c37-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="23c37-138">Pré-requisitos e informações sobre o processo de instalação Olá, ele é uma instalação de SAP NetWeaver boa ideia tooread Olá orienta cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="23c37-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="23c37-139">Este artigo aborda apenas as tarefas específicas para sistemas baseados no SAP NetWeaver que você pode usar com as Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="23c37-140">Essas observações sobre o SAP estão relacionadas toohello tópico do SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="23c37-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="23c37-141">Número da observação</span><span class="sxs-lookup"><span data-stu-id="23c37-141">Note number</span></span> | <span data-ttu-id="23c37-142">Title</span><span class="sxs-lookup"><span data-stu-id="23c37-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="23c37-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="23c37-143">[1928533]</span></span> |<span data-ttu-id="23c37-144">Aplicativos SAP no Azure: dimensionamento e produtos com suporte</span><span class="sxs-lookup"><span data-stu-id="23c37-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="23c37-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="23c37-145">[2015553]</span></span> |<span data-ttu-id="23c37-146">SAP no Microsoft Azure: pré-requisitos de suporte</span><span class="sxs-lookup"><span data-stu-id="23c37-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="23c37-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="23c37-147">[1999351]</span></span> |<span data-ttu-id="23c37-148">Monitoramento aprimorado do Azure para SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="23c37-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="23c37-149">[2178632]</span></span> |<span data-ttu-id="23c37-150">Métricas-chave de monitoramento para SAP no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="23c37-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="23c37-151">[1999351]</span></span> |<span data-ttu-id="23c37-152">Virtualização no Windows: monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="23c37-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="23c37-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="23c37-153">[2243692]</span></span> |<span data-ttu-id="23c37-154">Usar o Armazenamento SSD Premium do Azure para instância do SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="23c37-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="23c37-155">Saiba mais sobre Olá [limitações de assinaturas do Azure][azure-subscription-service-limits-subscription], incluindo limitações padrão gerais e limitações máximo.</span><span class="sxs-lookup"><span data-stu-id="23c37-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="23c37-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidade com o Azure Resource Manager versus o modelo de implantação clássico do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="23c37-157">modelos de implantação clássico do Azure e Hello Azure Resource Manager são diferentes em Olá áreas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="23c37-158">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="23c37-158">Resource groups</span></span>
- <span data-ttu-id="23c37-159">Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="23c37-160">Suporte para cenário SAP com vários SID</span><span class="sxs-lookup"><span data-stu-id="23c37-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="23c37-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="23c37-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="23c37-162">No Gerenciador de recursos do Azure, você pode usar recursos grupos toomanage todos os recursos de aplicativo hello em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="23c37-163">Uma abordagem integrada, em um grupo de recursos, todos os recursos têm Olá mesmo ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="23c37-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="23c37-164">Por exemplo, todos os recursos são criados no hello mesmo tempo e eles são excluídos no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="23c37-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="23c37-165">Saiba mais sobre [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="23c37-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="23c37-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="23c37-167">No modelo de implantação clássico do Azure hello, há uma dependência entre o balanceador de carga interno do Azure hello (serviço de Balanceador de carga do Azure) e o grupo de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service group.</span></span> <span data-ttu-id="23c37-168">Cada balanceador interno de carga precisa de um grupo de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="23c37-168">Every internal load balancer needs one cloud service group.</span></span>

<span data-ttu-id="23c37-169">No Gerenciador de recursos do Azure, não é necessário um grupo de recursos do Azure toouse balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-169">In Azure Resource Manager, you don't need an Azure resource group toouse Azure Load Balancer.</span></span> <span data-ttu-id="23c37-170">ambiente de saudação é mais simples e mais flexível.</span><span class="sxs-lookup"><span data-stu-id="23c37-170">hello environment is simpler and more flexible.</span></span>

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="23c37-171">Suporte para cenário SAP com vários SID</span><span class="sxs-lookup"><span data-stu-id="23c37-171">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="23c37-172">No Azure Resource Manager, você pode instalar várias instâncias ASCS/SCS do SID (identificador do sistema SAP) em um cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-172">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="23c37-173">Instâncias de vários SID são possíveis devido ao suporte de vários endereços IP para cada balanceador de carga interno de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-173">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="23c37-174">toouse Olá modelo de implantação clássico do Azure, siga os procedimentos de saudação descritos em [SAP NetWeaver no Azure: instâncias de cluster SAP ASCS/SCS usando o Clustering de Failover do Windows Server no Azure com SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="23c37-174">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23c37-175">É altamente recomendável que você use o modelo de implantação do Azure Resource Manager Olá para as instalações do SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-175">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="23c37-176">Ele oferece vários benefícios que não estão disponíveis no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-176">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="23c37-177">Saiba mais sobre os [modelos de implantação do Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="23c37-177">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="23c37-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span><span class="sxs-lookup"><span data-stu-id="23c37-178"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="23c37-179">Clustering de Failover do Windows Server é a base de saudação de uma instalação do SAP ASCS/SCS de alta disponibilidade e DBMS no Windows.</span><span class="sxs-lookup"><span data-stu-id="23c37-179">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="23c37-180">Um cluster de failover é um grupo de 1 + n servidores independentes (nós) que funcionam em conjunto de disponibilidade de saudação tooincrease de aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="23c37-180">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="23c37-181">Se ocorrer uma falha de nó, Clustering de Failover do Windows Server calcula o número de saudação de falhas que podem ocorrer durante a manutenção de um cluster tooprovide aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="23c37-181">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="23c37-182">Você pode escolher de clustering de failover do tooachieve de modos de quorum diferente.</span><span class="sxs-lookup"><span data-stu-id="23c37-182">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="23c37-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de quorum</span><span class="sxs-lookup"><span data-stu-id="23c37-183"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="23c37-184">Você pode escolher dentre quatro modos de quorum quando usa o Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="23c37-184">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="23c37-185">**Maioria de nós**.</span><span class="sxs-lookup"><span data-stu-id="23c37-185">**Node Majority**.</span></span> <span data-ttu-id="23c37-186">Cada nó do cluster Olá poderá votar.</span><span class="sxs-lookup"><span data-stu-id="23c37-186">Each node of hello cluster can vote.</span></span> <span data-ttu-id="23c37-187">funções de cluster Olá somente com a maioria dos votos, ou seja, com mais da metade Olá votos.</span><span class="sxs-lookup"><span data-stu-id="23c37-187">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="23c37-188">Recomendamos essa opção para clusters com número ímpar de nós.</span><span class="sxs-lookup"><span data-stu-id="23c37-188">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="23c37-189">Por exemplo, três nós em um cluster de sete nós podem falhar e ainda é de cluster Olá alcance uma maioria e continua toorun.</span><span class="sxs-lookup"><span data-stu-id="23c37-189">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="23c37-190">**Maioria de nós e disco**.</span><span class="sxs-lookup"><span data-stu-id="23c37-190">**Node and Disk Majority**.</span></span> <span data-ttu-id="23c37-191">Cada nó e um disco designado (uma testemunha de disco) no armazenamento de cluster Olá poderá votar quando elas estiverem disponíveis e em comunicação.</span><span class="sxs-lookup"><span data-stu-id="23c37-191">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="23c37-192">funções de cluster Olá somente com a maioria dos Olá votos, ou seja, com mais da metade de votos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-192">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="23c37-193">Esse modo faz sentido em um ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="23c37-193">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="23c37-194">Se nós Olá metade e disco Olá estiverem online, cluster Olá permanecerá em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="23c37-194">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="23c37-195">**Maioria de nós e compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="23c37-195">**Node and File Share Majority**.</span></span> <span data-ttu-id="23c37-196">Cada sinal de adição de nó cria um compartilhamento de arquivo designado (um compartilhamento de arquivos) que Olá administrador poderá votar, independentemente se nós hello e compartilhamento de arquivos estão disponíveis e em comunicação.</span><span class="sxs-lookup"><span data-stu-id="23c37-196">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="23c37-197">funções de cluster Olá somente com a maioria dos Olá votos, ou seja, com mais da metade de votos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-197">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="23c37-198">Esse modo faz sentido em um ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="23c37-198">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="23c37-199">É semelhante toohello nó e modo de maioria de disco, mas ele usa um compartilhamento de arquivo testemunha, em vez de um disco testemunha.</span><span class="sxs-lookup"><span data-stu-id="23c37-199">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="23c37-200">Este modo é fácil tooimplement, mas se o compartilhamento de arquivo hello em si não está altamente disponível, ele pode se tornar um ponto único de falha.</span><span class="sxs-lookup"><span data-stu-id="23c37-200">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="23c37-201">**Sem maioria: somente disco**.</span><span class="sxs-lookup"><span data-stu-id="23c37-201">**No Majority: Disk Only**.</span></span> <span data-ttu-id="23c37-202">Olá tiver um quorum se um nó estiver disponível e na comunicação com um disco específico no armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-202">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="23c37-203">Somente nós de saudação que também estiverem em comunicação com esse disco podem ingressar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-203">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="23c37-204">Recomendamos que você não use esse modo.</span><span class="sxs-lookup"><span data-stu-id="23c37-204">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="23c37-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering no local</span><span class="sxs-lookup"><span data-stu-id="23c37-205"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="23c37-206">A Figura 1 mostra um cluster de dois nós.</span><span class="sxs-lookup"><span data-stu-id="23c37-206">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="23c37-207">Se hello falha de conexão de rede entre os nós de saudação e ambos os nós continuar e em execução, um compartilhamento de arquivos ou disco de quorum determina qual nó continuará do cluster de saudação tooprovide aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="23c37-207">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="23c37-208">nó de saudação que tem o disco de quorum toohello acesso ou compartilhamento de arquivo é o nó de Olá que assegura que os serviços continuem.</span><span class="sxs-lookup"><span data-stu-id="23c37-208">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="23c37-209">Como este exemplo usa um cluster de dois nós, usamos hello nó e o modo de quorum maioria de compartilhamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="23c37-209">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="23c37-210">Olá nó e a maioria dos também é uma opção válida.</span><span class="sxs-lookup"><span data-stu-id="23c37-210">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="23c37-211">Em um ambiente de produção, recomendamos que você use um disco de quorum.</span><span class="sxs-lookup"><span data-stu-id="23c37-211">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="23c37-212">Você pode usar toomake de tecnologia de sistema de rede e armazenamento altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="23c37-212">You can use network and storage system technology toomake it highly available.</span></span>

![Figura 1: exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="23c37-214">_**Figura 1:** exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure_</span><span class="sxs-lookup"><span data-stu-id="23c37-214">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="23c37-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Armazenamento compartilhado</span><span class="sxs-lookup"><span data-stu-id="23c37-215"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="23c37-216">A Figura 1 também mostra um cluster de armazenamento compartilhado de dois nós.</span><span class="sxs-lookup"><span data-stu-id="23c37-216">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="23c37-217">Em um cluster de armazenamento compartilhado no local, todos os nós no cluster Olá detectam armazenamento compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-217">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="23c37-218">Um mecanismo de bloqueio protege os dados de saudação contra danos.</span><span class="sxs-lookup"><span data-stu-id="23c37-218">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="23c37-219">Todos os nós podem detectar se outro nó falhar.</span><span class="sxs-lookup"><span data-stu-id="23c37-219">All nodes can detect if another node fails.</span></span> <span data-ttu-id="23c37-220">Se um nó falhar, nó restante Olá apropria Olá dos recursos de armazenamento e garante a disponibilidade de saudação de serviços.</span><span class="sxs-lookup"><span data-stu-id="23c37-220">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-221">Você não precisa de discos compartilhados de alta disponibilidade com alguns aplicativos de DBMS, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="23c37-221">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="23c37-222">SQL Server Always On replica os arquivos de log e dados do DBMS de disco local de saudação do disco local de toohello do nó de um cluster de outro nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-222">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="23c37-223">Nesse caso, configuração de cluster do Windows hello não precisa de um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-223">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="23c37-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Resolução de nome e rede</span><span class="sxs-lookup"><span data-stu-id="23c37-224"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="23c37-225">Computadores cliente alcançar cluster Olá sobre um endereço IP virtual e um nome de host virtual que Olá fornece do servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="23c37-225">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="23c37-226">Olá nós locais e o servidor DNS Olá pode lidar com vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="23c37-226">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="23c37-227">Em uma instalação comum, você usa duas ou mais conexões de rede:</span><span class="sxs-lookup"><span data-stu-id="23c37-227">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="23c37-228">Armazenamento de toohello uma conexão dedicada</span><span class="sxs-lookup"><span data-stu-id="23c37-228">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="23c37-229">Uma conexão de rede interna de cluster de pulsação Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-229">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="23c37-230">Uma rede pública que os clientes usam tooconnect toohello cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-230">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="23c37-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering no Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-231"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="23c37-232">Em comparação com implantações de nuvem privada ou metal toobare, máquinas virtuais do Azure requer etapas adicionais tooconfigure Clustering de Failover do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="23c37-232">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="23c37-233">Quando você cria um disco de cluster compartilhado, você precisa tooset nomes de vários endereços IP e o host virtual para a instância do SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-233">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="23c37-234">Neste artigo, vamos discutir os principais conceitos e Olá etapas adicionais necessárias toobuild um cluster de serviços de alta disponibilidade central SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-234">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="23c37-235">Mostraremos como tooset ferramenta de terceiros Olá SIOS DataKeeper e como tooconfigure hello Azure interno balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="23c37-235">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="23c37-236">Você pode usar essas ferramentas toocreate um cluster de failover do Windows com uma testemunha de compartilhamento de arquivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-236">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado][sap-ha-guide-figure-1001]

<span data-ttu-id="23c37-238">_**Figura 2:** configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado_</span><span class="sxs-lookup"><span data-stu-id="23c37-238">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="23c37-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartilhado no Azure com SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="23c37-239"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="23c37-240">Você precisa de armazenamento compartilhado em cluster para uma instância do SAP ASCS/SCS de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="23c37-240">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="23c37-241">Como de setembro de 2016, o Azure não oferece armazenamento compartilhado que você pode usar toocreate um cluster de armazenamento compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-241">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="23c37-242">Você pode usar o software de terceiros SIOS DataKeeper Cluster Edition toocreate um armazenamento espelhado que simula o armazenamento compartilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-242">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="23c37-243">Olá solução SIOS fornece replicação síncrona de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="23c37-243">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="23c37-244">É assim que você pode criar um recurso de disco compartilhado para um cluster:</span><span class="sxs-lookup"><span data-stu-id="23c37-244">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="23c37-245">Anexe um tooeach Azure disco rígido virtual (VHD) de máquinas virtuais de saudação (VMs) em uma configuração de cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="23c37-245">Attach an additional Azure virtual hard disk (VHD) tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="23c37-246">Execute o SIOS DataKeeper Cluster Edition em ambos os nós da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23c37-246">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="23c37-247">Configure SIOS DataKeeper Cluster Edition para que ele reflete o conteúdo de saudação do volume VHD anexado adicional Olá Olá máquina virtual toohello adicional VHD anexado do volume de origem Olá virtual da máquina de destino.</span><span class="sxs-lookup"><span data-stu-id="23c37-247">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional VHD attached volume from hello source virtual machine toohello additional VHD attached volume of hello target virtual machine.</span></span> <span data-ttu-id="23c37-248">SIOS DataKeeper abstrai Olá origem e destino local os volumes e, em seguida, apresenta tooWindows Clustering de Failover do servidor como um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-248">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="23c37-249">Saiba mais sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="23c37-249">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: configuração do Clustering de Failover do Windows Server no Azure com o SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="23c37-251">_**Figura 3:** configuração do Windows Server Failover Cluster no Azure com o SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="23c37-251">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-252">Você não precisa de discos compartilhados de alta disponibilidade com alguns produtos de DBMS, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="23c37-252">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="23c37-253">SQL Server Always On replica os arquivos de log e dados do DBMS de disco local de saudação do disco local de toohello do nó de um cluster de outro nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-253">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="23c37-254">Nesse caso, configuração de cluster do Windows hello não precisa de um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-254">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="23c37-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolução de nomes no Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-255"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="23c37-256">plataforma de nuvem do Azure Olá não oferece Olá opção tooconfigure endereços IP virtuais, como endereços IP flutuantes.</span><span class="sxs-lookup"><span data-stu-id="23c37-256">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="23c37-257">É necessário tooset uma solução alternativa a um virtual tooreach Olá cluster recurso de endereço IP na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-257">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="23c37-258">O Azure tem um balanceador de carga interno no hello Serviço Balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-258">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="23c37-259">Com o balanceador de carga interno hello, clientes alcançar cluster Olá por endereço IP virtual de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-259">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="23c37-260">Você precisa de Balanceador de carga interno toodeploy Olá no grupo de recursos de saudação que contém nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-260">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="23c37-261">Em seguida, configure porta de necessária todas as regras de encaminhamento com investigação Olá portas Olá interno do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="23c37-261">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="23c37-262">clientes de saudação podem se conectar por meio do nome de host virtual hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-262">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="23c37-263">servidor DNS de saudação resolve o endereço IP de cluster hello e saudação de carga interno balanceador identificadores porta encaminhamento toohello o nó ativo do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-263">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="23c37-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver de alta disponibilidade na Azure IaaS (Infraestrutura como um serviço)</span><span class="sxs-lookup"><span data-stu-id="23c37-264"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="23c37-265">tooachieve SAP alta disponibilidade de aplicativos, como SAP para componentes de software, você precisa tooprotect Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-265">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="23c37-266">Instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-266">SAP Application Server instance</span></span>
* <span data-ttu-id="23c37-267">Instância ASCS/SCS SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-267">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="23c37-268">Servidor DBMS</span><span class="sxs-lookup"><span data-stu-id="23c37-268">DBMS server</span></span>

<span data-ttu-id="23c37-269">Para obter mais informações sobre como proteger os componentes SAP em cenários de alta disponibilidade, consulte [Azure Virtual Machines planning and implementation for SAP NetWeaver (Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver)](planning-guide.md).</span><span class="sxs-lookup"><span data-stu-id="23c37-269">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver](planning-guide.md).</span></span>

### <span data-ttu-id="23c37-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Servidor de Aplicativos SAP de Alta Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="23c37-270"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="23c37-271">Geralmente você não precisa de uma solução de alta disponibilidade específica para instâncias de servidor de aplicativos SAP e a caixa de diálogo hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-271">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="23c37-272">Você atinge alta disponibilidade por redundância e configura várias instâncias de caixa de diálogo em diferentes Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-272">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="23c37-273">Você deve ter pelo menos duas instâncias do aplicativo SAP instaladas em duas Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-273">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Servidor de Aplicativos SAP de alta disponibilidade][sap-ha-guide-figure-2000]

<span data-ttu-id="23c37-275">_**Figura 4:** Servidor de Aplicativos SAP de alta disponibilidade_</span><span class="sxs-lookup"><span data-stu-id="23c37-275">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="23c37-276">Você deve colocar todas as máquinas virtuais que instâncias de servidor de aplicativos SAP host em Olá mesmo conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-276">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="23c37-277">Um conjunto de disponibilidade do Azure garante que:</span><span class="sxs-lookup"><span data-stu-id="23c37-277">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="23c37-278">Todas as máquinas virtuais são parte da saudação mesmo domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="23c37-278">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="23c37-279">Por exemplo, um domínio de atualização, torna-se de que as máquinas virtuais de saudação não são atualizadas em Olá mesmo tempo durante o tempo de inatividade de manutenção planejada.</span><span class="sxs-lookup"><span data-stu-id="23c37-279">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="23c37-280">Todas as máquinas virtuais são parte da saudação mesmo domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="23c37-280">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="23c37-281">Por exemplo, um domínio de falha, torna-se de que as máquinas virtuais são implantadas para que nenhum ponto de falha afeta a disponibilidade de saudação de todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="23c37-281">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="23c37-282">Saiba mais sobre como muito[gerenciar Olá disponibilidade das máquinas virtuais][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="23c37-282">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="23c37-283">Como Olá conta de armazenamento do Azure é um ponto único de falha potencial, é importante toohave pelo menos duas contas de armazenamento do Azure, na qual pelo menos duas máquinas virtuais é distribuído.</span><span class="sxs-lookup"><span data-stu-id="23c37-283">Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="23c37-284">Em uma configuração ideal, discos de saudação de cada máquina virtual que está executando uma instância de diálogo SAP seriam implantados em uma conta de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="23c37-284">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="23c37-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instância do SAP ASCS/SCS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="23c37-285"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="23c37-286">A Figura 5 é um exemplo de instância do SAP ASCS/SCS de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="23c37-286">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: instância do SAP ASCS/SCS de alta disponibilidade][sap-ha-guide-figure-2001]

<span data-ttu-id="23c37-288">_**Figura 5:** instância do SAP ASCS/SCS de alta disponibilidade_</span><span class="sxs-lookup"><span data-stu-id="23c37-288">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="23c37-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidade da Instância do SAP ASCS/SCS com o Clustering de Failover do Windows Server no Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-289"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="23c37-290">Em comparação com implantações de nuvem privada ou metal toobare, máquinas virtuais do Azure requer etapas adicionais tooconfigure Clustering de Failover do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="23c37-290">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="23c37-291">toobuild um cluster de failover do Windows, é necessário um disco de cluster compartilhado, vários endereços IP, vários nomes de host virtual e um balanceador de carga interno do Azure para uma instância SAP ASCS/SCS de clustering.</span><span class="sxs-lookup"><span data-stu-id="23c37-291">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="23c37-292">Discutiremos isso em mais detalhes posteriormente neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-292">We discuss this in more detail later in hello article.</span></span>

![Figura 6: configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure usando SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="23c37-294">_**Figura 6:** configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure com SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="23c37-294">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="23c37-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Instância do DBMS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="23c37-295"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="23c37-296">Olá DBMS é também um ponto único de contato em um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-296">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="23c37-297">Você precisa tooprotect-lo usando uma solução de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="23c37-297">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="23c37-298">A Figura 7 mostra uma solução de alta disponibilidade do SQL Server Always On no Azure, o balanceador de carga com o Clustering de Failover do Windows Server e hello Azure interno.</span><span class="sxs-lookup"><span data-stu-id="23c37-298">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="23c37-299">O AlwaysOn do SQL Server replica os arquivos de log e dados do DBMS usando sua própria replicação DBMS.</span><span class="sxs-lookup"><span data-stu-id="23c37-299">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="23c37-300">Nesse caso, você não precisa de discos compartilhados de cluster, que simplifica a configuração inteira de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-300">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Figura 7: exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server][sap-ha-guide-figure-2003]

<span data-ttu-id="23c37-302">_**Figura 7:** exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server_</span><span class="sxs-lookup"><span data-stu-id="23c37-302">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="23c37-303">Para obter mais informações sobre o agrupamento do SQL Server no Azure usando o modelo de implantação do Azure Resource Manager hello, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="23c37-303">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="23c37-304">[Configurar um grupo de disponibilidade AlwaysOn nas máquinas virtuais do Azure usando o Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="23c37-304">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="23c37-305">[Configurar um balanceador de carga interno do Azure para um grupo de disponibilidade AlwaysOn no Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="23c37-305">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="23c37-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Cenários de implantação de alta disponibilidade de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="23c37-306"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="23c37-307">Cenário de implantação usando o Modelo Arquitetônico 1</span><span class="sxs-lookup"><span data-stu-id="23c37-307">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="23c37-308">A Figura 8 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-308">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="23c37-309">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="23c37-309">This scenario is set up as follows:</span></span>

- <span data-ttu-id="23c37-310">Um cluster dedicado é usado para a instância do SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-310">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="23c37-311">Um cluster dedicado é usado para a instância DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-311">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="23c37-312">Instâncias do Servidor de Aplicativos SAP são implantadas em suas próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="23c37-312">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Modelo Arquitetônico 1 de alta disponibilidade de SAP, com cluster dedicado para ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="23c37-314">_**Figura 8:** Modelo Arquitetônico 1 de alta disponibilidade de SAP, com clusters dedicados para ASCS/SCS e DBMS_</span><span class="sxs-lookup"><span data-stu-id="23c37-314">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="23c37-315">Cenário de implantação usando o Modelo Arquitetônico 2</span><span class="sxs-lookup"><span data-stu-id="23c37-315">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="23c37-316">A Figura 9 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-316">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="23c37-317">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="23c37-317">This scenario is set up as follows:</span></span>

- <span data-ttu-id="23c37-318">Um cluster dedicado é usado para **ambos** Olá SAP ASCS/SCS instância e Olá DBMS.</span><span class="sxs-lookup"><span data-stu-id="23c37-318">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="23c37-319">Instâncias do Servidor de Aplicativos SAP são implantados em VMs próprias dedicadas.</span><span class="sxs-lookup"><span data-stu-id="23c37-319">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="23c37-321">_**Figura 9:** Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS_</span><span class="sxs-lookup"><span data-stu-id="23c37-321">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="23c37-322">Cenário de implantação usando o Modelo Arquitetônico 3</span><span class="sxs-lookup"><span data-stu-id="23c37-322">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="23c37-323">A Figura 10 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **dois** sistemas SAP, com &lt;SID1&gt; e &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="23c37-323">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="23c37-324">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="23c37-324">This scenario is set up as follows:</span></span>

- <span data-ttu-id="23c37-325">Um cluster dedicado é usado para **ambos** instância Olá SAP ASCS/SCS SID1 *e* instância Olá SAP ASCS/SCS SID2 (um cluster).</span><span class="sxs-lookup"><span data-stu-id="23c37-325">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="23c37-326">Um cluster dedicado é usado para SID1 e outro para SID2 de DBMS (dois clusters).</span><span class="sxs-lookup"><span data-stu-id="23c37-326">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="23c37-327">Instâncias de servidor de aplicativos do SAP para Olá sistema SAP SID1 tem suas próprias VMs dedicados.</span><span class="sxs-lookup"><span data-stu-id="23c37-327">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="23c37-328">Instâncias de servidor de aplicativos do SAP para Olá sistema SAP SID2 tem suas próprias VMs dedicados.</span><span class="sxs-lookup"><span data-stu-id="23c37-328">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="23c37-330">_**Figura 10:** Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="23c37-330">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="23c37-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar a infraestrutura de saudação</span><span class="sxs-lookup"><span data-stu-id="23c37-331"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="23c37-332">Preparar a infraestrutura de saudação para 1 arquitetura de modelo</span><span class="sxs-lookup"><span data-stu-id="23c37-332">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="23c37-333">Os modelos do Azure Resource Manager para SAP ajudam a simplificar a implantação dos recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="23c37-333">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="23c37-334">modelos de três camadas Olá no Gerenciador de recursos do Azure também oferecem suporte a cenários de alta disponibilidade, como, em 1 arquitetura de modelo, que tem dois clusters.</span><span class="sxs-lookup"><span data-stu-id="23c37-334">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="23c37-335">Cada cluster é um ponto único de falha de SAP para SAP ASCS/SCS e DBMS.</span><span class="sxs-lookup"><span data-stu-id="23c37-335">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="23c37-336">Aqui é onde você pode obter os modelos do Gerenciador de recursos do Azure para o cenário de exemplo hello que descrevemos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="23c37-336">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="23c37-337">Imagem do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="23c37-337">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="23c37-338">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="23c37-338">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)

<span data-ttu-id="23c37-339">infraestrutura tooprepare Olá para 1 arquitetura de modelo:</span><span class="sxs-lookup"><span data-stu-id="23c37-339">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="23c37-340">Em Olá portal do Azure, Olá **parâmetros** folha em Olá **SYSTEMAVAILABILITY** selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="23c37-340">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager][sap-ha-guide-figure-3000]

<span data-ttu-id="23c37-342">_**Figura 11:** definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager_</span><span class="sxs-lookup"><span data-stu-id="23c37-342">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="23c37-343">criam modelos de saudação:</span><span class="sxs-lookup"><span data-stu-id="23c37-343">hello templates create:</span></span>

  * <span data-ttu-id="23c37-344">**Máquinas virtuais**:</span><span class="sxs-lookup"><span data-stu-id="23c37-344">**Virtual machines**:</span></span>
    * <span data-ttu-id="23c37-345">Máquinas virtuais do Servidor de Aplicativos SAP: <*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-345">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="23c37-346">Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-346">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="23c37-347">Cluster DBMS: <*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-347">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="23c37-348">**Placas de rede para todas as máquinas virtuais, com endereços IP associados**:</span><span class="sxs-lookup"><span data-stu-id="23c37-348">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="23c37-349"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-349"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="23c37-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-350"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="23c37-351"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="23c37-351"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="23c37-352">**Contas de Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="23c37-352">**Azure storage accounts**</span></span>

  * <span data-ttu-id="23c37-353">**Grupos de Disponibilidade** para:</span><span class="sxs-lookup"><span data-stu-id="23c37-353">**Availability groups** for:</span></span>
    * <span data-ttu-id="23c37-354">Máquinas virtuais do Servidor de Aplicativos do SAP: <*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="23c37-354">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="23c37-355">Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="23c37-355">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="23c37-356">Máquinas virtuais de cluster DBMS: <*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="23c37-356">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="23c37-357">**Balanceador de carga interno do Azure**:</span><span class="sxs-lookup"><span data-stu-id="23c37-357">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="23c37-358">Com todas as portas para a instância do ASCS/SCS hello e o endereço IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="23c37-358">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="23c37-359">Com todas as portas para Olá DBMS do SQL Server e o endereço IP <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="23c37-359">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="23c37-360">**Grupo de segurança de rede**: <*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="23c37-360">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="23c37-361">Com um toohello de porta de protocolo de área de trabalho remota (RDP) externo abra <*SAPSystemSID*> - ascs - 0 virtual machine</span><span class="sxs-lookup"><span data-stu-id="23c37-361">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-362">Todos os endereços IP de placas de rede hello e balanceadores de carga interno do Azure são **dinâmico** por padrão.</span><span class="sxs-lookup"><span data-stu-id="23c37-362">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="23c37-363">Alterá-los muito**estático** endereços IP.</span><span class="sxs-lookup"><span data-stu-id="23c37-363">Change them too**static** IP addresses.</span></span> <span data-ttu-id="23c37-364">Descrevemos como toodo posteriormente neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-364">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="23c37-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implantar máquinas virtuais com toouse de conectividade (entre locais) da rede corporativa na produção</span><span class="sxs-lookup"><span data-stu-id="23c37-365"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="23c37-366">Para sistemas SAP de produção, implante máquinas virtuais do Azure com [conectividade de rede corporativa (entre instalações)][planning-guide-2.2] usando o VPN Site a Site ou o ExpressRoute do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-366">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-367">Você pode usar a instância da Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-367">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="23c37-368">subrede e a rede virtual Olá já foram criados e preparados.</span><span class="sxs-lookup"><span data-stu-id="23c37-368">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="23c37-369">Em Olá portal do Azure, Olá **parâmetros** folha em Olá **NEWOREXISTINGSUBNET** selecione **existente**.</span><span class="sxs-lookup"><span data-stu-id="23c37-369">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="23c37-370">Em Olá **SUBNETID** caixa, adicione a cadeia de caracteres completa da rede do Azure preparada SubnetID onde você planeja toodeploy suas máquinas virtuais do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-370">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="23c37-371">tooget uma lista de todas as sub-redes de rede do Azure, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23c37-371">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="23c37-372">Olá **ID** campo mostra Olá **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="23c37-372">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="23c37-373">tooget uma lista de todos os **SUBNETID** valores, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23c37-373">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="23c37-374">Olá **SUBNETID** tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="23c37-374">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="23c37-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implantar instâncias de SAP somente na nuvem para teste e demonstração</span><span class="sxs-lookup"><span data-stu-id="23c37-375"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="23c37-376">Você pode implantar o sistema SAP de alta disponibilidade em um modelo de implantação somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="23c37-376">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="23c37-377">Esse tipo de implantação é principalmente útil para casos de uso de demonstração e teste.</span><span class="sxs-lookup"><span data-stu-id="23c37-377">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="23c37-378">Ele não é adequado para casos de uso de produção.</span><span class="sxs-lookup"><span data-stu-id="23c37-378">It's not suited for production use cases.</span></span>

- <span data-ttu-id="23c37-379">Em Olá portal do Azure, Olá **parâmetros** folha, no hello **NEWOREXISTINGSUBNET** selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="23c37-379">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="23c37-380">Deixe Olá **SUBNETID** campo vazio.</span><span class="sxs-lookup"><span data-stu-id="23c37-380">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="23c37-381">Olá SAP do Azure Resource Manager cria automaticamente Olá sub-rede e a rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-381">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-382">Você também precisa toodeploy pelo menos uma dedicada a máquina virtual para o Active Directory e DNS no Olá a mesma instância de rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-382">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="23c37-383">modelo de saudação não cria essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="23c37-383">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="23c37-384">Preparar a infraestrutura de saudação para 2 de modelo de arquitetura</span><span class="sxs-lookup"><span data-stu-id="23c37-384">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="23c37-385">Você pode usar este modelo do Gerenciador de recursos do Azure para SAP toohelp simplificar a implantação de recursos de infraestrutura necessária para 2 de modelo de arquitetura do SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-385">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="23c37-386">Aqui é onde você pode obter os modelos do Azure Resource Manager para esse cenário de implantação:</span><span class="sxs-lookup"><span data-stu-id="23c37-386">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="23c37-387">Imagem do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="23c37-387">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="23c37-388">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="23c37-388">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="23c37-389">Preparar a infraestrutura de saudação para 3 arquitetura do modelo</span><span class="sxs-lookup"><span data-stu-id="23c37-389">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="23c37-390">Você pode preparar a infraestrutura de saudação e configurar SAP para **várias SID**.</span><span class="sxs-lookup"><span data-stu-id="23c37-390">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="23c37-391">Por exemplo, você pode adicionar uma instância SAP ASCS/SCS adicional em uma configuração de cluster *existente*.</span><span class="sxs-lookup"><span data-stu-id="23c37-391">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="23c37-392">Para obter mais informações, consulte [configurar uma instância SAP ASCS/SCS adicional em um toocreate de configuração de cluster uma configuração de multi-SID do SAP existente no Gerenciador de recursos do Azure][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="23c37-392">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="23c37-393">Se você quiser toocreate um novo cluster de várias SID, você pode usar o multi-SID de saudação [modelos de início rápido no GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="23c37-393">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="23c37-394">toocreate um novo cluster de várias SID, é necessário toodeploy Olá três modelos a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-394">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="23c37-395">Modelo de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-395">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="23c37-396">Modelo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="23c37-396">Database template</span></span>](#database-template)
* [<span data-ttu-id="23c37-397">Modelo dos servidores de aplicativo</span><span class="sxs-lookup"><span data-stu-id="23c37-397">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="23c37-398">Olá seções a seguir têm mais detalhes sobre os modelos de saudação e parâmetros Olá necessário tooprovide em modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-398">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="23c37-399"><a name="ASCS-SCS-template"></a> Modelo de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-399"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="23c37-400">modelo ASCS/SCS Olá implanta duas máquinas virtuais que você pode usar toocreate um cluster de failover do Windows Server que hospeda várias instâncias do ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="23c37-400">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="23c37-401">tooset modelo de saudação ASCS/SCS multi-SID em Olá [modelo de várias SID ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image], insira valores para Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-401">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="23c37-402">**Prefixo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="23c37-402">**Resource Prefix**.</span></span>  <span data-ttu-id="23c37-403">Defina prefixo de recurso hello, que é usado tooprefix todos os recursos que são criados durante a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-403">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="23c37-404">Como recursos de Olá não pertencer a um sistema SAP tooonly, prefixo de saudação do recurso de saudação não é Olá SID de um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-404">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="23c37-405">Olá prefixo deve estar entre **três e seis caracteres**.</span><span class="sxs-lookup"><span data-stu-id="23c37-405">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="23c37-406">**Tipo de Pilha**.</span><span class="sxs-lookup"><span data-stu-id="23c37-406">**Stack Type**.</span></span> <span data-ttu-id="23c37-407">Selecione o tipo de pilha de saudação de saudação sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-407">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="23c37-408">Dependendo do tipo de pilha hello, o balanceador de carga do Azure tem um (ABAP ou Java somente) ou dois (ABAP + Java) endereços IP privados por sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-408">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="23c37-409">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="23c37-409">**OS Type**.</span></span> <span data-ttu-id="23c37-410">Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-410">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="23c37-411">**Contagem do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="23c37-411">**SAP System Count**.</span></span> <span data-ttu-id="23c37-412">Selecione o número de saudação de sistemas SAP que você deseja tooinstall neste cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-412">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="23c37-413">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="23c37-413">**System Availability**.</span></span> <span data-ttu-id="23c37-414">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="23c37-414">Select **HA**.</span></span>
  -  <span data-ttu-id="23c37-415">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="23c37-415">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="23c37-416">Crie um novo usuário que pode ser usado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="23c37-416">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="23c37-417">**Sub-rede Nova ou Existente**.</span><span class="sxs-lookup"><span data-stu-id="23c37-417">**New Or Existing Subnet**.</span></span> <span data-ttu-id="23c37-418">Define se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="23c37-418">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="23c37-419">Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione **existente**.</span><span class="sxs-lookup"><span data-stu-id="23c37-419">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="23c37-420">**ID da Sub-rede**. ID de saudação do conjunto de máquinas virtuais do hello sub-rede toowhich Olá deve estar conectado.</span><span class="sxs-lookup"><span data-stu-id="23c37-420">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="23c37-421">Selecione a sub-rede de saudação da sua rede virtual privada (VPN) ou rede de rota expressa rede virtual tooconnect Olá máquina virtual tooyour local.</span><span class="sxs-lookup"><span data-stu-id="23c37-421">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="23c37-422">ID de saudação geralmente tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="23c37-422">hello ID usually looks like this:</span></span>

   <span data-ttu-id="23c37-423">/subscriptions/<*ID da assinatura*>/resourceGroups/<*nome do grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nome de rede virtual*>/subnets/<*nome de sub-rede*></span><span class="sxs-lookup"><span data-stu-id="23c37-423">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="23c37-424">modelo de saudação implanta uma instância de Balanceador de carga do Azure, que dá suporte a vários sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-424">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="23c37-425">Olá ASCS são configuradas para o número de instância 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="23c37-425">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="23c37-426">Olá SCS são configuradas para o número de instância 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="23c37-426">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="23c37-427">Olá ASCS Enqueue replicação servidor (es) (Linux) são configuradas para o número de instância 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="23c37-427">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="23c37-428">Olá SCS es (Linux) são configuradas para o número de instância 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="23c37-428">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="23c37-429">Balanceador de carga Hello contém 1 (2 para Linux) VIP(s), 1 VIP x do ASCS/SCS e 1 VIP x para es (Linux).</span><span class="sxs-lookup"><span data-stu-id="23c37-429">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="23c37-430">Olá lista a seguir contém todas as regras (onde x é o número de saudação do hello sistema SAP, por exemplo, 1, 2, 3...) de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="23c37-430">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="23c37-431">Portas específicas do Windows para cada o sistema SAP: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="23c37-431">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="23c37-432">Portas ASCS (número de instância x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="23c37-432">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="23c37-433">Portas SCS (número de instância x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="23c37-433">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="23c37-434">Portas ASCS ERS no Linux (número de instância x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="23c37-434">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="23c37-435">Portas SCS ERS no Linux (número de instância x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="23c37-435">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="23c37-436">Balanceador de carga de saudação é configurado toouse Olá portas de investigação (onde x é o número de saudação do hello sistema SAP, por exemplo, 1, 2, 3...) a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-436">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="23c37-437">Porta de investigação do balanceador interno de carga ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="23c37-437">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="23c37-438">Porta de investigação do balanceador interno de carga ERS (somente Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="23c37-438">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="23c37-439"><a name="database-template"></a> Modelo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="23c37-439"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="23c37-440">modelo de banco de dados de saudação implanta uma ou duas máquinas virtuais que você pode usar tooinstall Olá o sistema de gerenciamento de banco de dados relacional (RDBMS) para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-440">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="23c37-441">Por exemplo, se você implantar um modelo ASCS/SCS para cinco sistemas SAP, será necessário toodeploy este modelo cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="23c37-441">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="23c37-442">tooset modelo de várias SID Olá banco de dados, em Olá [modelo de multi-SID de banco de dados][sap-templates-3-tier-multisid-db-marketplace-image], insira valores para Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-442">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="23c37-443">**ID do sistema SAP**. Insira o sistema ID SAP Olá Olá sistema SAP que você deseja tooinstall.</span><span class="sxs-lookup"><span data-stu-id="23c37-443">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="23c37-444">Olá ID será usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="23c37-444">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="23c37-445">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="23c37-445">**Os Type**.</span></span> <span data-ttu-id="23c37-446">Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-446">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="23c37-447">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="23c37-447">**Dbtype**.</span></span> <span data-ttu-id="23c37-448">Selecione o tipo de saudação do banco de dados de saudação desejado tooinstall no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-448">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="23c37-449">Selecione **SQL** se você quiser tooinstall Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="23c37-449">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="23c37-450">Selecione **HANA** se você planejar tooinstall SAP HANA em máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-450">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="23c37-451">Certifique-se de tooselect Olá tipo de sistema operacional correto: selecione **Windows** para SQL e selecione uma distribuição de Linux para HANA.</span><span class="sxs-lookup"><span data-stu-id="23c37-451">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="23c37-452">Olá balanceador de carga do Azure que está conectada toohello máquinas virtuais serão configurado toosupport tipo de banco de dados de saudação selecionado:</span><span class="sxs-lookup"><span data-stu-id="23c37-452">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="23c37-453">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="23c37-453">**SQL**.</span></span> <span data-ttu-id="23c37-454">o balanceador de carga Olá será a porta 1433 do balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="23c37-454">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="23c37-455">Verifique se toouse essa porta para a sua instalação do SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="23c37-455">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="23c37-456">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="23c37-456">**HANA**.</span></span> <span data-ttu-id="23c37-457">Balanceador de carga Hello serão portas 35015 e 35017 de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="23c37-457">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="23c37-458">Certifique-se de que tooinstall HANA SAP com o número de instância **50**.</span><span class="sxs-lookup"><span data-stu-id="23c37-458">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="23c37-459">Balanceador de carga Olá usará a porta de investigação 62550.</span><span class="sxs-lookup"><span data-stu-id="23c37-459">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="23c37-460">**Tamanho do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="23c37-460">**Sap System Size**.</span></span> <span data-ttu-id="23c37-461">Conjunto Olá número de SAPS Olá novo sistema fornecerá.</span><span class="sxs-lookup"><span data-stu-id="23c37-461">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="23c37-462">Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="23c37-462">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="23c37-463">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="23c37-463">**System Availability**.</span></span> <span data-ttu-id="23c37-464">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="23c37-464">Select **HA**.</span></span>
  -  <span data-ttu-id="23c37-465">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="23c37-465">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="23c37-466">Crie um novo usuário que pode ser usado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="23c37-466">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="23c37-467">**ID da Sub-rede**. Insira a ID de Olá da sub-rede Olá que você usou durante a implantação de saudação do modelo ASCS/SCS hello, ou Olá ID de sub-rede de saudação que foi criado como parte da implantação de modelo ASCS/SCS do hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-467">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="23c37-468"><a name="application-servers-template"></a> Modelo dos servidores de aplicativos</span><span class="sxs-lookup"><span data-stu-id="23c37-468"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="23c37-469">modelo de servidores de aplicativo Hello implanta duas ou mais máquinas virtuais que podem ser usadas como instâncias de servidor de aplicativos do SAP para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-469">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="23c37-470">Por exemplo, se você implantar um modelo ASCS/SCS para cinco sistemas SAP, será necessário toodeploy este modelo cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="23c37-470">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="23c37-471">tooset backup Olá servidores multi-SID modelo de aplicativo no hello [modelo de aplicativo de SID de vários servidores][sap-templates-3-tier-multisid-apps-marketplace-image], insira valores para Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-471">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="23c37-472">**ID do sistema SAP**. Insira o sistema ID SAP Olá Olá sistema SAP que você deseja tooinstall.</span><span class="sxs-lookup"><span data-stu-id="23c37-472">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="23c37-473">Olá ID será usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="23c37-473">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="23c37-474">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="23c37-474">**Os Type**.</span></span> <span data-ttu-id="23c37-475">Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-475">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="23c37-476">**Tamanho do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="23c37-476">**Sap System Size**.</span></span> <span data-ttu-id="23c37-477">Olá número de SAPS Olá novo sistema fornecerá.</span><span class="sxs-lookup"><span data-stu-id="23c37-477">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="23c37-478">Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.</span><span class="sxs-lookup"><span data-stu-id="23c37-478">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="23c37-479">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="23c37-479">**System Availability**.</span></span> <span data-ttu-id="23c37-480">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="23c37-480">Select **HA**.</span></span>
  -  <span data-ttu-id="23c37-481">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="23c37-481">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="23c37-482">Crie um novo usuário que pode ser usado toosign toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="23c37-482">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="23c37-483">**ID da Sub-rede**. Insira a ID de Olá da sub-rede Olá que você usou durante a implantação de saudação do modelo ASCS/SCS hello, ou Olá ID de sub-rede de saudação que foi criado como parte da implantação de modelo ASCS/SCS do hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-483">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="23c37-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-484"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="23c37-485">Em nosso exemplo, o espaço de endereço de saudação do hello rede virtual do Azure é 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="23c37-485">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="23c37-486">Há uma sub-rede chamada **Subnet**, com um intervalo de endereços de 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="23c37-486">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="23c37-487">Todas as máquinas virtuais e balanceadores de carga internos são implantados nessa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="23c37-487">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23c37-488">Não faça nenhuma alteração toohello as configurações de rede no sistema de operacional convidado hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-488">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="23c37-489">Isso inclui endereços IP, servidores DNS e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="23c37-489">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="23c37-490">Configure todas as configurações de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-490">Configure all your network settings in Azure.</span></span> <span data-ttu-id="23c37-491">Olá serviço de protocolo de configuração de Host dinâmico (DHCP) propaga as configurações.</span><span class="sxs-lookup"><span data-stu-id="23c37-491">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="23c37-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Endereços IP de DNS</span><span class="sxs-lookup"><span data-stu-id="23c37-492"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="23c37-493">Olá tooset necessário que endereços IP de DNS, Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="23c37-493">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="23c37-494">Em Olá portal do Azure, Olá **servidores DNS** folha, certifique-se de que sua rede virtual **servidores DNS** opção for definida muito**DNS personalizado**.</span><span class="sxs-lookup"><span data-stu-id="23c37-494">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="23c37-495">Selecione as configurações com base no tipo de saudação da rede que você tem.</span><span class="sxs-lookup"><span data-stu-id="23c37-495">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="23c37-496">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="23c37-496">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="23c37-497">[Conectividade de rede corporativa (entre locais)][planning-guide-2.2]: adicionar endereços IP hello dos servidores DNS local hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-497">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="23c37-498">Você pode estender no DNS servidores toohello máquinas virtuais que estão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-498">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="23c37-499">Nesse cenário, você pode adicionar endereços de IP hello hello Azure máquinas virtuais em que você executa o serviço DNS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-499">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="23c37-500">[Implantação somente em nuvem][planning-guide-2.1]: implantar uma máquina virtual adicional no hello mesma instância de rede Virtual que serve como um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="23c37-500">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="23c37-501">Adicionar endereços de IP Olá Olá Azure máquinas virtuais que você configurou o serviço DNS toorun.</span><span class="sxs-lookup"><span data-stu-id="23c37-501">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Figura 12: Configurar servidores DNS da Rede Virtual do Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="23c37-503">_**Figura 12:** Configurar servidores DNS da Rede Virtual do Azure_</span><span class="sxs-lookup"><span data-stu-id="23c37-503">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="23c37-504">Se você alterar os endereços IP hello dos servidores DNS hello, você precisa toorestart Olá máquinas virtuais do Azure tooapply Olá alteração e propagar os novos servidores DNS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-504">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="23c37-505">Em nosso exemplo, Olá serviço DNS é instalado e configurado nessas máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="23c37-505">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="23c37-506">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-506">Virtual machine role</span></span> | <span data-ttu-id="23c37-507">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-507">Virtual machine host name</span></span> | <span data-ttu-id="23c37-508">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="23c37-508">Network card name</span></span> | <span data-ttu-id="23c37-509">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="23c37-509">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="23c37-510">Primeiro servidor DNS</span><span class="sxs-lookup"><span data-stu-id="23c37-510">First DNS server</span></span> |<span data-ttu-id="23c37-511">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="23c37-511">domcontr-0</span></span> |<span data-ttu-id="23c37-512">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="23c37-512">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="23c37-513">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="23c37-513">10.0.0.10</span></span> |
| <span data-ttu-id="23c37-514">Segundo servidor DNS</span><span class="sxs-lookup"><span data-stu-id="23c37-514">Second DNS server</span></span> |<span data-ttu-id="23c37-515">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="23c37-515">domcontr-1</span></span> |<span data-ttu-id="23c37-516">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="23c37-516">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="23c37-517">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="23c37-517">10.0.0.11</span></span> |

### <span data-ttu-id="23c37-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nomes de host e endereços IP estáticos para a instância clusterizada do SAP ASCS/SCS hello e instância clusterizada do DBMS</span><span class="sxs-lookup"><span data-stu-id="23c37-518"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="23c37-519">Para implantação local, você precisa destes endereços IP e nomes de host reservados:</span><span class="sxs-lookup"><span data-stu-id="23c37-519">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="23c37-520">Função de nome de host virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-520">Virtual host name role</span></span> | <span data-ttu-id="23c37-521">Nome de host virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-521">Virtual host name</span></span> | <span data-ttu-id="23c37-522">Endereço IP estático virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-522">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23c37-523">Nome de host virtual do primeiro cluster SAP ASCS/SCS (para gerenciamento de cluster)</span><span class="sxs-lookup"><span data-stu-id="23c37-523">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="23c37-524">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="23c37-524">pr1-ascs-vir</span></span> |<span data-ttu-id="23c37-525">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="23c37-525">10.0.0.42</span></span> |
| <span data-ttu-id="23c37-526">Nome de host virtual da instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-526">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="23c37-527">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="23c37-527">pr1-ascs-sap</span></span> |<span data-ttu-id="23c37-528">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="23c37-528">10.0.0.43</span></span> |
| <span data-ttu-id="23c37-529">Nome de host virtual do segundo cluster SAP DBMS (gerenciamento de cluster)</span><span class="sxs-lookup"><span data-stu-id="23c37-529">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="23c37-530">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="23c37-530">pr1-dbms-vir</span></span> |<span data-ttu-id="23c37-531">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="23c37-531">10.0.0.32</span></span> |

<span data-ttu-id="23c37-532">Quando você cria o cluster hello, criar hello nomes de host virtual **pr1-ascs-vir** e **pr1 de dbms de vir** e Olá associados a endereços IP que gerenciar o próprio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-532">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="23c37-533">Para obter informações sobre como toodo isso, consulte [coletar nós de cluster em uma configuração de cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="23c37-533">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="23c37-534">Você pode criar manualmente Olá outros dois nomes de host virtual **pr1-ascs-sap** e **pr1 de dbms de sap**, e Olá associados a endereços IP, no servidor DNS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-534">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="23c37-535">Hello instância clusterizada do SAP ASCS/SCS e instância DBMS Olá clusterizado usam esses recursos.</span><span class="sxs-lookup"><span data-stu-id="23c37-535">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="23c37-536">Para obter informações sobre como toodo isso, consulte [criar um nome de host virtual para uma instância clusterizada do SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="23c37-536">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="23c37-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de endereços IP estáticos para máquinas de virtuais Olá SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-537"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="23c37-538">Depois de implantar Olá toouse de máquinas virtuais no cluster, você precisa tooset os endereços IP estáticos para todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="23c37-538">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="23c37-539">Fazer isso na configuração de rede Virtual do Azure Olá e não no sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-539">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="23c37-540">No portal do Azure de Olá, selecione **grupo de recursos** > **placa de rede** > **configurações** > **endereço IP** .</span><span class="sxs-lookup"><span data-stu-id="23c37-540">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="23c37-541">Em Olá **endereços IP** folha, em **atribuição**, selecione **estático**.</span><span class="sxs-lookup"><span data-stu-id="23c37-541">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="23c37-542">Em Olá **endereço IP** , digite o endereço IP de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="23c37-542">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="23c37-543">Se você alterar o endereço IP Olá Olá placa de rede, você precisa toorestart Olá máquinas virtuais do Azure tooapply Olá alteração.</span><span class="sxs-lookup"><span data-stu-id="23c37-543">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Figura 13: Definir os endereços IP estáticos Olá placa de rede de cada máquina virtual][sap-ha-guide-figure-3002]

  <span data-ttu-id="23c37-545">_**Figura 13:** conjunto de endereços IP estáticos Olá placa de rede de cada máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="23c37-545">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="23c37-546">Repita essa etapa para todas as interfaces de rede, ou seja, todas as máquinas virtuais, incluindo máquinas virtuais que você deseja toouse para o serviço do Active Directory/DNS.</span><span class="sxs-lookup"><span data-stu-id="23c37-546">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="23c37-547">Em nosso exemplo, temos estas máquinas virtuais e endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="23c37-547">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="23c37-548">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-548">Virtual machine role</span></span> | <span data-ttu-id="23c37-549">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="23c37-549">Virtual machine host name</span></span> | <span data-ttu-id="23c37-550">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="23c37-550">Network card name</span></span> | <span data-ttu-id="23c37-551">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="23c37-551">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="23c37-552">Primeira instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-552">First SAP Application Server instance</span></span> |<span data-ttu-id="23c37-553">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="23c37-553">pr1-di-0</span></span> |<span data-ttu-id="23c37-554">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="23c37-554">pr1-nic-di-0</span></span> |<span data-ttu-id="23c37-555">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="23c37-555">10.0.0.50</span></span> |
| <span data-ttu-id="23c37-556">Segunda instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-556">Second SAP Application Server instance</span></span> |<span data-ttu-id="23c37-557">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="23c37-557">pr1-di-1</span></span> |<span data-ttu-id="23c37-558">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="23c37-558">pr1-nic-di-1</span></span> |<span data-ttu-id="23c37-559">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="23c37-559">10.0.0.51</span></span> |
| <span data-ttu-id="23c37-560">...</span><span class="sxs-lookup"><span data-stu-id="23c37-560">...</span></span> |<span data-ttu-id="23c37-561">...</span><span class="sxs-lookup"><span data-stu-id="23c37-561">...</span></span> |<span data-ttu-id="23c37-562">...</span><span class="sxs-lookup"><span data-stu-id="23c37-562">...</span></span> |<span data-ttu-id="23c37-563">...</span><span class="sxs-lookup"><span data-stu-id="23c37-563">...</span></span> |
| <span data-ttu-id="23c37-564">Última instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-564">Last SAP Application Server instance</span></span> |<span data-ttu-id="23c37-565">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="23c37-565">pr1-di-5</span></span> |<span data-ttu-id="23c37-566">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="23c37-566">pr1-nic-di-5</span></span> |<span data-ttu-id="23c37-567">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="23c37-567">10.0.0.55</span></span> |
| <span data-ttu-id="23c37-568">Primeiro nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-568">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="23c37-569">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="23c37-569">pr1-ascs-0</span></span> |<span data-ttu-id="23c37-570">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="23c37-570">pr1-nic-ascs-0</span></span> |<span data-ttu-id="23c37-571">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="23c37-571">10.0.0.40</span></span> |
| <span data-ttu-id="23c37-572">Segundo nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-572">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="23c37-573">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="23c37-573">pr1-ascs-1</span></span> |<span data-ttu-id="23c37-574">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="23c37-574">pr1-nic-ascs-1</span></span> |<span data-ttu-id="23c37-575">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="23c37-575">10.0.0.41</span></span> |
| <span data-ttu-id="23c37-576">Primeiro nó de cluster para a instância do DBMS</span><span class="sxs-lookup"><span data-stu-id="23c37-576">First cluster node for DBMS instance</span></span> |<span data-ttu-id="23c37-577">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="23c37-577">pr1-db-0</span></span> |<span data-ttu-id="23c37-578">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="23c37-578">pr1-nic-db-0</span></span> |<span data-ttu-id="23c37-579">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="23c37-579">10.0.0.30</span></span> |
| <span data-ttu-id="23c37-580">Segundo nó de cluster para a instância do DBMS</span><span class="sxs-lookup"><span data-stu-id="23c37-580">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="23c37-581">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="23c37-581">pr1-db-1</span></span> |<span data-ttu-id="23c37-582">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="23c37-582">pr1-nic-db-1</span></span> |<span data-ttu-id="23c37-583">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="23c37-583">10.0.0.31</span></span> |

### <span data-ttu-id="23c37-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Definir um endereço IP estático para o balanceador de carga interno do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-584"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="23c37-585">modelo do Gerenciador de recursos do Azure SAP Olá cria um balanceador de carga interno do Azure que é usado para o cluster de instância de SAP ASCS/SCS hello e DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-585">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23c37-586">Olá endereço IP do nome de host virtual de saudação do hello SAP ASCS/SCS é Olá mesmo como endereço IP de saudação do hello balanceador de carga interno do SAP ASCS/SCS: **pr1 de balanceamento de carga de ascs**.</span><span class="sxs-lookup"><span data-stu-id="23c37-586">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="23c37-587">Olá endereço IP do nome virtual Olá Olá DBMS é Olá mesmo como endereço IP de saudação do hello balanceador de carga interno do DBMS: **pr1 de balanceamento de carga de dbms**.</span><span class="sxs-lookup"><span data-stu-id="23c37-587">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="23c37-588">tooset um endereço IP estático para hello Azure interno balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="23c37-588">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="23c37-589">Olá implantação inicial define um endereço IP do balanceador de carga interno Olá muito**dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="23c37-589">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="23c37-590">Em Olá portal do Azure, Olá **endereços IP** folha, em **atribuição**, selecione **estático**.</span><span class="sxs-lookup"><span data-stu-id="23c37-590">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="23c37-591">Definir endereço IP de saudação do balanceador de carga interno Olá **pr1 de balanceamento de carga de ascs** toohello endereço IP do nome de host virtual Olá da instância do SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-591">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="23c37-592">Definir endereço IP de saudação do balanceador de carga interno Olá **pr1 de balanceamento de carga de dbms** toohello endereço IP do nome de host virtual Olá da instância DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-592">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Figura 14: Definir os endereços IP estáticos para o balanceador de carga interno Olá para instância do SAP ASCS/SCS Olá][sap-ha-guide-figure-3003]

  <span data-ttu-id="23c37-594">_**Figura 14:** definir endereços IP estáticos para o balanceador de carga interno Olá para instância do SAP ASCS/SCS Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-594">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="23c37-595">Em nosso exemplo, temos dois balanceadores de carga internos do Azure que têm esses endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="23c37-595">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="23c37-596">Função do balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-596">Azure internal load balancer role</span></span> | <span data-ttu-id="23c37-597">Nome balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="23c37-597">Azure internal load balancer name</span></span> | <span data-ttu-id="23c37-598">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="23c37-598">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23c37-599">Balanceador de carga interno da instância SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-599">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="23c37-600">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="23c37-600">pr1-lb-ascs</span></span> |<span data-ttu-id="23c37-601">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="23c37-601">10.0.0.43</span></span> |
| <span data-ttu-id="23c37-602">Balanceador de carga interno de DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-602">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="23c37-603">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="23c37-603">pr1-lb-dbms</span></span> |<span data-ttu-id="23c37-604">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="23c37-604">10.0.0.33</span></span> |


### <span data-ttu-id="23c37-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Padrão de regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-605"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="23c37-606">modelo do Gerenciador de recursos do Azure SAP Olá cria portas Olá que é necessário:</span><span class="sxs-lookup"><span data-stu-id="23c37-606">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="23c37-607">Uma instância do ASCS ABAP, com o número de instância padrão Olá **00**</span><span class="sxs-lookup"><span data-stu-id="23c37-607">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="23c37-608">Uma instância de Java SCS, com o número de instância padrão Olá **01**</span><span class="sxs-lookup"><span data-stu-id="23c37-608">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="23c37-609">Quando você instala sua instância SAP ASCS/SCS, você deve usar o número de instância padrão Olá **00** para seu número ABAP ASCS instância e saudação padrão instância **01** para sua instância de Java SCS.</span><span class="sxs-lookup"><span data-stu-id="23c37-609">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="23c37-610">Em seguida, crie pontos de extremidade para portas do SAP NetWeaver Olá de balanceamento de carga interna necessária.</span><span class="sxs-lookup"><span data-stu-id="23c37-610">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="23c37-611">toocreate necessário balanceamento de carga interno de pontos de extremidade, primeiro, crie esses pontos de extremidade para portas do SAP NetWeaver ABAP ASCS Olá de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="23c37-611">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="23c37-612">Nome da regra do balanceamento de carga/serviço</span><span class="sxs-lookup"><span data-stu-id="23c37-612">Service/load balancing rule name</span></span> | <span data-ttu-id="23c37-613">Números de porta padrão</span><span class="sxs-lookup"><span data-stu-id="23c37-613">Default port numbers</span></span> | <span data-ttu-id="23c37-614">Portas concretas para (instância do ASCS com número de instância 00) (ERS com 10)</span><span class="sxs-lookup"><span data-stu-id="23c37-614">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23c37-615">Enfileirar Servidor / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="23c37-615">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="23c37-616">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-616">32<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-617">3200</span><span class="sxs-lookup"><span data-stu-id="23c37-617">3200</span></span> |
| <span data-ttu-id="23c37-618">Servidor de Mensagens ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="23c37-618">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="23c37-619">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-619">36<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-620">3600</span><span class="sxs-lookup"><span data-stu-id="23c37-620">3600</span></span> |
| <span data-ttu-id="23c37-621">Mensagem interna ABAP / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="23c37-621">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="23c37-622">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-622">39<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-623">3900</span><span class="sxs-lookup"><span data-stu-id="23c37-623">3900</span></span> |
| <span data-ttu-id="23c37-624">HTTP do Servidor de Mensagens / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="23c37-624">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="23c37-625">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-625">81<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-626">8100</span><span class="sxs-lookup"><span data-stu-id="23c37-626">8100</span></span> |
| <span data-ttu-id="23c37-627">HTTP do SAP para Iniciar Serviço ASCS / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="23c37-627">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="23c37-628">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="23c37-628">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="23c37-629">50013</span><span class="sxs-lookup"><span data-stu-id="23c37-629">50013</span></span> |
| <span data-ttu-id="23c37-630">HTTPS do SAP para Iniciar Serviço ASCS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="23c37-630">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="23c37-631">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="23c37-631">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="23c37-632">50014</span><span class="sxs-lookup"><span data-stu-id="23c37-632">50014</span></span> |
| <span data-ttu-id="23c37-633">Enfileirar Replicação / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="23c37-633">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="23c37-634">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="23c37-634">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="23c37-635">50016</span><span class="sxs-lookup"><span data-stu-id="23c37-635">50016</span></span> |
| <span data-ttu-id="23c37-636">HTTP do SAP para Iniciar Serviço ERS *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="23c37-636">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="23c37-637">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="23c37-637">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="23c37-638">51013</span><span class="sxs-lookup"><span data-stu-id="23c37-638">51013</span></span> |
| <span data-ttu-id="23c37-639">HTTP do SAP para Iniciar Serviço ERS *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="23c37-639">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="23c37-640">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="23c37-640">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="23c37-641">51014</span><span class="sxs-lookup"><span data-stu-id="23c37-641">51014</span></span> |
| <span data-ttu-id="23c37-642">RM Win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="23c37-642">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="23c37-643">5985</span><span class="sxs-lookup"><span data-stu-id="23c37-643">5985</span></span> |
| <span data-ttu-id="23c37-644">Compartilhamento de Arquivos *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="23c37-644">File Share *Lbrule445*</span></span> | |<span data-ttu-id="23c37-645">445</span><span class="sxs-lookup"><span data-stu-id="23c37-645">445</span></span> |

<span data-ttu-id="23c37-646">_**Tabela 1:** números de instâncias do SAP NetWeaver ABAP ASCS Olá de porta_</span><span class="sxs-lookup"><span data-stu-id="23c37-646">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="23c37-647">Em seguida, crie esses pontos de extremidade para portas do SAP NetWeaver Java SCS Olá de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="23c37-647">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="23c37-648">Nome da regra do balanceamento de carga/serviço</span><span class="sxs-lookup"><span data-stu-id="23c37-648">Service/load balancing rule name</span></span> | <span data-ttu-id="23c37-649">Números de porta padrão</span><span class="sxs-lookup"><span data-stu-id="23c37-649">Default port numbers</span></span> | <span data-ttu-id="23c37-650">Portas concretas para (instância do SCS com número de instância 01) (ERS com 11)</span><span class="sxs-lookup"><span data-stu-id="23c37-650">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23c37-651">Enfileirar Servidor / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="23c37-651">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="23c37-652">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-652">32<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-653">3201</span><span class="sxs-lookup"><span data-stu-id="23c37-653">3201</span></span> |
| <span data-ttu-id="23c37-654">Servidor do Gateway / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="23c37-654">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="23c37-655">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-655">33<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-656">3301</span><span class="sxs-lookup"><span data-stu-id="23c37-656">3301</span></span> |
| <span data-ttu-id="23c37-657">Servidor de Mensagens Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="23c37-657">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="23c37-658">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-658">39<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-659">3901</span><span class="sxs-lookup"><span data-stu-id="23c37-659">3901</span></span> |
| <span data-ttu-id="23c37-660">HTTP do Servidor de Mensagens / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="23c37-660">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="23c37-661">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="23c37-661">81<*InstanceNumber*></span></span> |<span data-ttu-id="23c37-662">8101</span><span class="sxs-lookup"><span data-stu-id="23c37-662">8101</span></span> |
| <span data-ttu-id="23c37-663">HTTP do SAP para Iniciar Serviço SCS / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="23c37-663">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="23c37-664">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="23c37-664">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="23c37-665">50113</span><span class="sxs-lookup"><span data-stu-id="23c37-665">50113</span></span> |
| <span data-ttu-id="23c37-666">HTTPS do SAP para Iniciar Serviço SCS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="23c37-666">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="23c37-667">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="23c37-667">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="23c37-668">50114</span><span class="sxs-lookup"><span data-stu-id="23c37-668">50114</span></span> |
| <span data-ttu-id="23c37-669">Enfileirar Replicação / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="23c37-669">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="23c37-670">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="23c37-670">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="23c37-671">50116</span><span class="sxs-lookup"><span data-stu-id="23c37-671">50116</span></span> |
| <span data-ttu-id="23c37-672">HTTP do SAP para Iniciar Serviço ERS *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="23c37-672">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="23c37-673">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="23c37-673">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="23c37-674">51113</span><span class="sxs-lookup"><span data-stu-id="23c37-674">51113</span></span> |
| <span data-ttu-id="23c37-675">HTTP do SAP para Iniciar Serviço ERS *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="23c37-675">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="23c37-676">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="23c37-676">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="23c37-677">51114</span><span class="sxs-lookup"><span data-stu-id="23c37-677">51114</span></span> |
| <span data-ttu-id="23c37-678">RM Win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="23c37-678">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="23c37-679">5985</span><span class="sxs-lookup"><span data-stu-id="23c37-679">5985</span></span> |
| <span data-ttu-id="23c37-680">Compartilhamento de Arquivos *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="23c37-680">File Share *Lbrule445*</span></span> | |<span data-ttu-id="23c37-681">445</span><span class="sxs-lookup"><span data-stu-id="23c37-681">445</span></span> |

<span data-ttu-id="23c37-682">_**Tabela 2:** números de instâncias do SAP NetWeaver Java SCS Olá de porta_</span><span class="sxs-lookup"><span data-stu-id="23c37-682">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga de padrão ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="23c37-684">_**Figura 15:** regras de Balanceador de carga interno do Azure Olá de balanceamento de carga de padrão ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="23c37-684">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="23c37-685">Configurar endereço IP Olá Olá do balanceador de carga **pr1 de balanceamento de carga de dbms** toohello endereço IP do nome de host virtual Olá da instância DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-685">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="23c37-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Alterar regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do hello ASCS/SCS padrão</span><span class="sxs-lookup"><span data-stu-id="23c37-686"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="23c37-687">Se você quiser toouse diferentes números de saudação SAP ASCS ou instâncias do SCS, você deve alterar nomes de saudação e valores de suas portas de valores padrão.</span><span class="sxs-lookup"><span data-stu-id="23c37-687">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="23c37-688">No portal do Azure de Olá, selecione  **<* SID*> - lb - ascs carregar balanceador * * > **regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="23c37-688">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="23c37-689">Todos os balanceamento de carga regras que pertencem a toohello SAP ASCS ou instância SCS, altere esses valores:</span><span class="sxs-lookup"><span data-stu-id="23c37-689">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="23c37-690">Nome</span><span class="sxs-lookup"><span data-stu-id="23c37-690">Name</span></span>
  * <span data-ttu-id="23c37-691">Porta</span><span class="sxs-lookup"><span data-stu-id="23c37-691">Port</span></span>
  * <span data-ttu-id="23c37-692">Porta de back-end</span><span class="sxs-lookup"><span data-stu-id="23c37-692">Back-end port</span></span>

  <span data-ttu-id="23c37-693">Por exemplo, se desejar que o número de instância ASCS toochange saudação padrão de 00 too31, você precisa toomake alterações de saudação para todas as portas listadas na tabela 1.</span><span class="sxs-lookup"><span data-stu-id="23c37-693">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="23c37-694">Veja um exemplo de uma atualização para a porta *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="23c37-694">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Alterar regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do hello ASCS/SCS padrão][sap-ha-guide-figure-3005]

  <span data-ttu-id="23c37-696">_**Figura 16:** alteração Olá ASCS/SCS padrão balanceamento de carga de regras de Balanceador de carga interno do Azure Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-696">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="23c37-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Adicionar o domínio de toohello de máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="23c37-697"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="23c37-698">Depois de atribuir um endereço IP estático, toohello máquinas da virtual, adicione o domínio de toohello de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-698">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Figura 17: Adicionar um domínio de tooa de máquina virtual][sap-ha-guide-figure-3006]

<span data-ttu-id="23c37-700">_**Figura 17:** adicionar um domínio de tooa de máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="23c37-700">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="23c37-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Adicionar entradas de registro em ambos os nós de cluster da instância do SAP ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-701"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="23c37-702">O balanceador de carga do Azure tem um balanceador de carga interno que fecha conexões quando conexões Olá estão ociosas por um determinado período de tempo (um tempo limite de ociosidade).</span><span class="sxs-lookup"><span data-stu-id="23c37-702">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="23c37-703">Processos de trabalho do SAP na caixa de diálogo instâncias conexões abertas toohello SAP enqueue processam como Olá primeiro enfileirar/remoção da fila de solicitação necessidades toobe enviado.</span><span class="sxs-lookup"><span data-stu-id="23c37-703">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="23c37-704">Essas conexões geralmente permanecem estabelecidas até que o processo de trabalho hello ou reinícios do processo de enfileiramento hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-704">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="23c37-705">No entanto, se a conexão de saudação ficar ocioso por um período de tempo definido, Olá interno de carga do Azure balanceador fecha Olá conexões.</span><span class="sxs-lookup"><span data-stu-id="23c37-705">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="23c37-706">Isso não é um problema porque Olá processo de trabalho do SAP restabelece o processo de enfileiramento Olá conexão toohello se ele não existe mais.</span><span class="sxs-lookup"><span data-stu-id="23c37-706">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="23c37-707">Essas atividades são documentadas nos rastreamentos do desenvolvedor de saudação de processos do SAP, mas criam uma grande quantidade de conteúdo extra nesses rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="23c37-707">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="23c37-708">Saudação de toochange uma boa ideia TCP/IP é `KeepAliveTime` e `KeepAliveInterval` em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-708">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="23c37-709">Combine essas alterações nos parâmetros de TCP/IP hello com parâmetros de perfil do SAP, descritos mais adiante no artigo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-709">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="23c37-710">entradas de registro de tooadd em ambos os nós de cluster da instância do SAP ASCS/SCS hello, primeiro, adicionam essas entradas de registro do Windows em ambos os nós de cluster do Windows para o SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="23c37-710">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="23c37-711">Caminho</span><span class="sxs-lookup"><span data-stu-id="23c37-711">Path</span></span> | <span data-ttu-id="23c37-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="23c37-712">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="23c37-713">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="23c37-713">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="23c37-714">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="23c37-714">Variable type</span></span> |<span data-ttu-id="23c37-715">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="23c37-715">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="23c37-716">Valor</span><span class="sxs-lookup"><span data-stu-id="23c37-716">Value</span></span> |<span data-ttu-id="23c37-717">120000</span><span class="sxs-lookup"><span data-stu-id="23c37-717">120000</span></span> |
| <span data-ttu-id="23c37-718">Link toodocumentation</span><span class="sxs-lookup"><span data-stu-id="23c37-718">Link toodocumentation</span></span> |[<span data-ttu-id="23c37-719">https://technet.microsoft.com/pt-BR/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="23c37-719">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="23c37-720">_**Tabela 3:** alteração Olá primeiro TCP/IP parâmetro_</span><span class="sxs-lookup"><span data-stu-id="23c37-720">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="23c37-721">Em seguida, adicione as seguintes entradas de Registro em nós de cluster do Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="23c37-721">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="23c37-722">Caminho</span><span class="sxs-lookup"><span data-stu-id="23c37-722">Path</span></span> | <span data-ttu-id="23c37-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="23c37-723">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="23c37-724">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="23c37-724">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="23c37-725">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="23c37-725">Variable type</span></span> |<span data-ttu-id="23c37-726">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="23c37-726">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="23c37-727">Valor</span><span class="sxs-lookup"><span data-stu-id="23c37-727">Value</span></span> |<span data-ttu-id="23c37-728">120000</span><span class="sxs-lookup"><span data-stu-id="23c37-728">120000</span></span> |
| <span data-ttu-id="23c37-729">Link toodocumentation</span><span class="sxs-lookup"><span data-stu-id="23c37-729">Link toodocumentation</span></span> |[<span data-ttu-id="23c37-730">https://technet.microsoft.com/pt-BR/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="23c37-730">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="23c37-731">_**Tabela 4:** alteração Olá TCP/IP segundo_</span><span class="sxs-lookup"><span data-stu-id="23c37-731">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="23c37-732">**as alterações de saudação do tooapply, reinicie ambos os nós de cluster**.</span><span class="sxs-lookup"><span data-stu-id="23c37-732">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="23c37-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurar um cluster Windows Server Failover Clustering para uma instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="23c37-733"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="23c37-734">Configurar um cluster do Clustering de Failover do Windows Server para uma instância do SAP ASCS/SCS envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="23c37-734">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="23c37-735">Coletando Olá nós de cluster em uma configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-735">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="23c37-736">Configurando a testemunha de compartilhamento de arquivos do cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-736">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="23c37-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Coletar nós de cluster de saudação em uma configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-737"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="23c37-738">No Assistente de recursos e Olá Adicionar função, adicione clustering tooboth nós de cluster de failover.</span><span class="sxs-lookup"><span data-stu-id="23c37-738">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="23c37-739">Configure o cluster de failover hello usando o Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="23c37-739">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="23c37-740">No Gerenciador de Cluster de Failover, selecione **criar Cluster**e depois adicione apenas nome de saudação do primeiro cluster hello, nó A. Não adicione o segundo nó de saudação ainda; Você adicionará o nó de segundo Olá em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="23c37-740">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Figura 18: Adicionar o servidor de saudação ou nome de máquina virtual do primeiro nó de cluster Olá][sap-ha-guide-figure-3007]

  <span data-ttu-id="23c37-742">_**Figura 18:** adicionar Olá máquina virtual nome do servidor ou do primeiro nó de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-742">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="23c37-743">Digite o nome de rede de saudação (nome de host virtual) do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-743">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Figura 19: Insira o nome do cluster Olá][sap-ha-guide-figure-3008]

  <span data-ttu-id="23c37-745">_**Figura 19:** nome do cluster Olá Enter_</span><span class="sxs-lookup"><span data-stu-id="23c37-745">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="23c37-746">Depois de criar o cluster de hello, execute um teste de validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-746">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Figura 20: Executar a verificação de validação de cluster de saudação][sap-ha-guide-figure-3009]

  <span data-ttu-id="23c37-748">_**Figura 20:** executar verificação de validação de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-748">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="23c37-749">Você pode ignorar os avisos sobre discos neste momento no processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-749">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="23c37-750">Você adicionará que uma testemunha de compartilhamento de arquivo e hello SIOS discos compartilhados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="23c37-750">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="23c37-751">Neste estágio, você não precisa tooworry quanto a ter um quorum.</span><span class="sxs-lookup"><span data-stu-id="23c37-751">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Figura 21: Nenhum disco de quorum é encontrado][sap-ha-guide-figure-3010]

  <span data-ttu-id="23c37-753">_**Figura 21:** Nenhum disco de quorum é encontrado_</span><span class="sxs-lookup"><span data-stu-id="23c37-753">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: Recurso de cluster principal precisa de um novo endereço IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="23c37-755">_**Figura 22:** Recurso de cluster principal precisa de um novo endereço IP_</span><span class="sxs-lookup"><span data-stu-id="23c37-755">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="23c37-756">Alterar o endereço IP de Olá Olá principal do serviço de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-756">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="23c37-757">cluster de saudação não pode iniciar até que você altere o endereço IP Olá Olá principal do serviço de cluster, como endereço IP de saudação do servidor de saudação aponta tooone de nós de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-757">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="23c37-758">Fazer isso em Olá **propriedades** página do recurso IP do serviço de cluster Olá core.</span><span class="sxs-lookup"><span data-stu-id="23c37-758">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="23c37-759">Por exemplo, é preciso tooassign um endereço IP (em nosso exemplo, **10.0.0.42**) para o nome de host virtual de cluster Olá **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="23c37-759">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: Na caixa de diálogo de propriedades de hello, altere o endereço IP de saudação][sap-ha-guide-figure-3012]

  <span data-ttu-id="23c37-761">_**Figura 23:** em Olá **propriedades** caixa de diálogo, o endereço IP de saudação de alteração_</span><span class="sxs-lookup"><span data-stu-id="23c37-761">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Figura 24: Atribuir o endereço IP de saudação que é reservado para o cluster Olá][sap-ha-guide-figure-3013]

  <span data-ttu-id="23c37-763">_**Figura 24:** atribuir Olá endereço IP que é reservado para o cluster de saudação_</span><span class="sxs-lookup"><span data-stu-id="23c37-763">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="23c37-764">Colocar o nome de host virtual de cluster Olá online.</span><span class="sxs-lookup"><span data-stu-id="23c37-764">Bring hello cluster virtual host name online.</span></span>

  ![Figura 25: O serviço principal de Cluster está ativo e em execução e Olá corrija o endereço IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="23c37-766">_**Figura 25:** principal serviço de Cluster está ativo e em execução e com hello corrija o endereço IP_</span><span class="sxs-lookup"><span data-stu-id="23c37-766">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="23c37-767">Adicione o segundo nó de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-767">Add hello second cluster node.</span></span>

  <span data-ttu-id="23c37-768">Agora que o serviço de cluster Olá principal está em execução, você pode adicionar o segundo nó de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-768">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Figura 26: Adicionar Olá segundo nó de cluster][sap-ha-guide-figure-3015]

  <span data-ttu-id="23c37-770">_**Figura 26:** adicionar Olá segundo cluster nó_</span><span class="sxs-lookup"><span data-stu-id="23c37-770">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="23c37-771">Insira um nome para o segundo host do nó de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-771">Enter a name for hello second cluster node host.</span></span>

  ![Figura 27: Insira o nome de host de nó de cluster segundo de saudação][sap-ha-guide-figure-3016]

  <span data-ttu-id="23c37-773">_**Figura 27:** Enter Olá cluster host nome do segundo nó_</span><span class="sxs-lookup"><span data-stu-id="23c37-773">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="23c37-774">Certifique-se de que Olá **adicionar todos os armazenamento qualificado ao cluster toohello** caixa de seleção é **não** selecionado.</span><span class="sxs-lookup"><span data-stu-id="23c37-774">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: Não marque a caixa de seleção de saudação][sap-ha-guide-figure-3017]

  <span data-ttu-id="23c37-776">_**Figura 28:** fazer **não** selecione Olá a caixa de seleção_</span><span class="sxs-lookup"><span data-stu-id="23c37-776">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="23c37-777">Você pode ignorar os avisos sobre quorum e discos.</span><span class="sxs-lookup"><span data-stu-id="23c37-777">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="23c37-778">Você definirá Olá quorum e compartilhamento Olá disco posteriormente, conforme descrito em [instalando SIOS DataKeeper Cluster Edition para o disco de compartilhamento de cluster SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="23c37-778">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorar os avisos sobre o quorum de disco Olá][sap-ha-guide-figure-3018]

  <span data-ttu-id="23c37-780">_**Figura 29:** ignorar os avisos sobre o quorum de disco Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-780">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="23c37-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurar a testemunha de compartilhamento de arquivos do cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-781"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="23c37-782">Configurar a testemunha de compartilhamento de arquivos do cluster envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="23c37-782">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="23c37-783">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="23c37-783">Creating a file share</span></span>
- <span data-ttu-id="23c37-784">Configuração de quorum de testemunha de compartilhamento de arquivos Olá no Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="23c37-784">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="23c37-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="23c37-785"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="23c37-786">Selecione uma testemunha de compartilhamento de arquivos em vez de um disco de quorum.</span><span class="sxs-lookup"><span data-stu-id="23c37-786">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="23c37-787">O SIOS DataKeeper dá suporte a essa opção.</span><span class="sxs-lookup"><span data-stu-id="23c37-787">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="23c37-788">Exemplos de saudação neste artigo, Olá testemunha de compartilhamento de arquivos é no servidor do Active Directory/DNS Olá que está em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-788">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="23c37-789">Olá testemunha de compartilhamento de arquivo é chamada **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="23c37-789">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="23c37-790">Como seria configurou um tooAzure de conexão de VPN (por meio de VPN Site a Site ou rota expressa do Azure), DNS do Active Directory/serviço é local e não é adequado toorun um arquivo de testemunha de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="23c37-790">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="23c37-791">Se o serviço do Active Directory/DNS é executado somente no local, não configure o compartilhamento de arquivos no sistema de operacional de Active Directory/DNS Windows hello que é executado no local.</span><span class="sxs-lookup"><span data-stu-id="23c37-791">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="23c37-792">A latência de rede entre os nós de cluster em execução no Azure e o Active Directory/DNS local pode ser muito grande e causar problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="23c37-792">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="23c37-793">Ser se tooconfigure Olá compartilhamento de arquivos em uma máquina virtual do Azure que está executando o nó de cluster toohello fechar.</span><span class="sxs-lookup"><span data-stu-id="23c37-793">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="23c37-794">unidade de quorum Olá precisa de pelo menos 1.024 MB de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="23c37-794">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="23c37-795">É recomendável 2.048 MB de espaço livre para a unidade de quorum hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-795">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="23c37-796">Adicione objeto de nome de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-796">Add hello cluster name object.</span></span>

  ![Figura 30: Atribuir permissões de saudação no compartilhamento de saudação do objeto de nome de cluster Olá][sap-ha-guide-figure-3019]

  <span data-ttu-id="23c37-798">_**Figura 30:** atribuir permissões de saudação no compartilhamento de saudação do objeto de nome de cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-798">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="23c37-799">Certifique-se de que permissões de saudação incluem dados toochange Olá no compartilhamento de saudação do objeto de nome de cluster hello (em nosso exemplo, **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="23c37-799">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="23c37-800">tooadd Olá cluster nome toohello lista de objetos, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23c37-800">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="23c37-801">Alterar Olá filtro toocheck para objetos de computador, na inclusão toothose mostrado na Figura 31.</span><span class="sxs-lookup"><span data-stu-id="23c37-801">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Figura 31: Computadores de tooinclude alteração Olá tipos de objeto][sap-ha-guide-figure-3020]

  <span data-ttu-id="23c37-803">_**Figura 31:** alterar Olá tipos de objeto tooinclude computadores_</span><span class="sxs-lookup"><span data-stu-id="23c37-803">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![A Figura 32: Marque a caixa de seleção de computadores de saudação][sap-ha-guide-figure-3021]

  <span data-ttu-id="23c37-805">_**A Figura 32:** Olá selecione **computadores** caixa de seleção_</span><span class="sxs-lookup"><span data-stu-id="23c37-805">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="23c37-806">Insira um objeto de nome de cluster Olá conforme mostrado na Figura 31.</span><span class="sxs-lookup"><span data-stu-id="23c37-806">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="23c37-807">Porque o registro de saudação já foi criado, você pode alterar permissões hello, conforme mostrado na Figura 30.</span><span class="sxs-lookup"><span data-stu-id="23c37-807">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="23c37-808">Selecione Olá **segurança** guia de compartilhamento hello e defina mais detalhados permissões para o objeto de nome de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-808">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Figura 33: Olá conjunto de atributos de segurança para objeto de nome de cluster Olá no quorum Olá de compartilhamento de arquivos][sap-ha-guide-figure-3022]

  <span data-ttu-id="23c37-810">_**Figura 33:** definir atributos de segurança de saudação para objeto de nome de cluster Olá no quorum Olá de compartilhamento de arquivos_</span><span class="sxs-lookup"><span data-stu-id="23c37-810">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="23c37-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Definir o quorum de testemunha de compartilhamento de arquivos Olá no Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="23c37-811"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="23c37-812">Abra Olá configurar Assistente de configuração de Quorum.</span><span class="sxs-lookup"><span data-stu-id="23c37-812">Open hello Configure Quorum Setting Wizard.</span></span>

  ![A Figura 34: Iniciar Olá configurar Assistente de configuração de Quorum de Cluster][sap-ha-guide-figure-3023]

  <span data-ttu-id="23c37-814">_**A Figura 34:** início Olá configurar o Assistente de configuração de Quorum do Cluster_</span><span class="sxs-lookup"><span data-stu-id="23c37-814">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="23c37-815">Em Olá **Selecionar configuração de Quorum** , selecione **selecionar testemunha de quorum Olá**.</span><span class="sxs-lookup"><span data-stu-id="23c37-815">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Figura 35: Configurações de quorum à sua escolha][sap-ha-guide-figure-3024]

  <span data-ttu-id="23c37-817">_**Figura 35:** Configurações de quorum à sua escolha_</span><span class="sxs-lookup"><span data-stu-id="23c37-817">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="23c37-818">Em Olá **selecionar testemunha de Quorum** , selecione **configurar uma testemunha de compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="23c37-818">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![A Figura 36: Olá selecione Compartilhamento de arquivos][sap-ha-guide-figure-3025]

  <span data-ttu-id="23c37-820">_**A Figura 36:** selecionar testemunha de compartilhamento de arquivo hello_</span><span class="sxs-lookup"><span data-stu-id="23c37-820">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="23c37-821">Digite o compartilhamento de arquivos toohello do caminho UNC hello (em nosso exemplo, \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="23c37-821">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="23c37-822">toosee uma lista de alterações de saudação pode fazer, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="23c37-822">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![A Figura 37: Definir o local de compartilhamento de arquivo hello para compartilhamento de testemunha Olá][sap-ha-guide-figure-3026]

  <span data-ttu-id="23c37-824">_**A Figura 37:** definir o local de compartilhamento de arquivo hello para compartilhamento de testemunha Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-824">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="23c37-825">Selecione as alterações de saudação desejado e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="23c37-825">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="23c37-826">Você precisa toosuccessfully reconfigurar a configuração de cluster Olá conforme mostrado na Figura 38.</span><span class="sxs-lookup"><span data-stu-id="23c37-826">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![A Figura 38: Confirmação que você tenha reconfigurado cluster Olá][sap-ha-guide-figure-3027]

  <span data-ttu-id="23c37-828">_**A Figura 38:** confirmação que você tenha reconfigurado cluster Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-828">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="23c37-829">Depois de instalar com êxito Olá Cluster de Failover do Windows, as alterações devem toobe feita toosome limites tooadapt failover detecção tooconditions no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-829">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="23c37-830">Olá toobe parâmetros alterado são documentados neste blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="23c37-830">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="23c37-831">Supondo que seu duas VMs que criar hello configuração de Cluster do Windows para ASCS/SCS estão em Olá mesma sub-rede, parâmetros a seguir hello necessário toobe alterado toothese valores:</span><span class="sxs-lookup"><span data-stu-id="23c37-831">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="23c37-832">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="23c37-832">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="23c37-833">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="23c37-833">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="23c37-834">Essas configurações foram testadas com clientes e fornecidas um toobe comprometimento bom flexível o suficiente no lado de uma saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-834">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="23c37-835">Em Olá outro lado essas configurações foram fornecendo rápido suficiente failover em condições de erro real em falha de software ou nó de VM do SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-835">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="23c37-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar o SIOS DataKeeper Cluster Edition para o disco de compartilhamento de cluster de SAP ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-836"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="23c37-837">Agora você tem uma configuração do Clustering de Failover do Windows Server em funcionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-837">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="23c37-838">Mas, tooinstall uma instância SAP ASCS/SCS, você precisa de um recurso de disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-838">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="23c37-839">Você não pode criar recursos de disco Olá compartilhado que é necessário no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-839">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="23c37-840">SIOS DataKeeper Cluster Edition é uma solução de terceiros que você pode usar os recursos de disco toocreate compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-840">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="23c37-841">Disco de compartilhamento de cluster instalando SIOS DataKeeper Cluster Edition para Olá SAP ASCS/SCS envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="23c37-841">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="23c37-842">Adição de saudação do .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="23c37-842">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="23c37-843">Instalando o SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="23c37-843">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="23c37-844">Configurar o SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="23c37-844">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="23c37-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Adicionar saudação do .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="23c37-845"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="23c37-846">saudação do Microsoft .NET Framework 3.5 não é automaticamente ativada ou instalada no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="23c37-846">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="23c37-847">Como SIOS DataKeeper requer saudação do .NET Framework toobe em todos os nós que você instalar DataKeeper no, você deve instalar saudação do .NET Framework 3.5 no sistema de operacional convidado saudação de todas as máquinas virtuais em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-847">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="23c37-848">Há Olá tooadd de duas maneiras do .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="23c37-848">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="23c37-849">Use Olá assistente Adicionar funções e recursos no Windows, conforme mostrado na figura 39.</span><span class="sxs-lookup"><span data-stu-id="23c37-849">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Instalar saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos][sap-ha-guide-figure-3028]

  <span data-ttu-id="23c37-851">_**Figura 39:** Olá de instalação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos_</span><span class="sxs-lookup"><span data-stu-id="23c37-851">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Figura 40: Progresso da instalação barra quando você instala a saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos][sap-ha-guide-figure-3029]

  <span data-ttu-id="23c37-853">_**A figura 40:** barra quando você instala a saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos de progresso de instalação_</span><span class="sxs-lookup"><span data-stu-id="23c37-853">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="23c37-854">Use Olá ferramenta de linha de comando dism.exe.</span><span class="sxs-lookup"><span data-stu-id="23c37-854">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="23c37-855">Para este tipo de instalação, você precisa SxS diretório Olá tooaccess Olá mídia de instalação do Windows.</span><span class="sxs-lookup"><span data-stu-id="23c37-855">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="23c37-856">Em um prompt de comandos com privilégios elevados, digite:</span><span class="sxs-lookup"><span data-stu-id="23c37-856">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="23c37-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="23c37-857"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="23c37-858">Instale o SIOS DataKeeper Cluster Edition em cada nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-858">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="23c37-859">toocreate o armazenamento compartilhado virtual com SIOS DataKeeper, criar um espelho sincronizado e, em seguida, simule o armazenamento compartilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-859">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="23c37-860">Antes de instalar o software SIOS hello, crie o usuário de domínio de saudação **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="23c37-860">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-861">Adicionar Olá **DataKeeperSvc** usuário toohello **Administrador Local** grupo em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-861">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="23c37-862">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="23c37-862">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="23c37-863">Instale o software SIOS Olá em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-863">Install hello SIOS software on both cluster nodes.</span></span>

  ![Instalador do SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Primeira página do hello SIOS DataKeeper instalação][sap-ha-guide-figure-3031]

  <span data-ttu-id="23c37-866">_**Figura 41:** primeira página do hello SIOS DataKeeper instalação_</span><span class="sxs-lookup"><span data-stu-id="23c37-866">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="23c37-867">Na caixa de diálogo Olá mostrada na figura 42, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="23c37-867">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: O DataKeeper informa a você que um serviço será desabilitado][sap-ha-guide-figure-3032]

  <span data-ttu-id="23c37-869">_**Figura 42:** O DataKeeper informa a você que um serviço será desabilitado_</span><span class="sxs-lookup"><span data-stu-id="23c37-869">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="23c37-870">Na caixa de diálogo Olá mostrada na figura 43, recomendamos que você selecione **conta de domínio ou servidor**.</span><span class="sxs-lookup"><span data-stu-id="23c37-870">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Seleção do usuário para o SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="23c37-872">_**Figura 43:** Seleção do usuário para o SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="23c37-872">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="23c37-873">Insira o nome de usuário da conta de domínio hello e senhas que você criou para SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="23c37-873">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Insira Olá nome de usuário de domínio e senha para Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3034]

  <span data-ttu-id="23c37-875">_**Figura 44:** digite Olá nome de usuário de domínio e senha para Olá SIOS DataKeeper instalação_</span><span class="sxs-lookup"><span data-stu-id="23c37-875">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="23c37-876">Instale a chave de licença de saudação para sua instância SIOS DataKeeper, conforme mostrado na figura 45.</span><span class="sxs-lookup"><span data-stu-id="23c37-876">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: insira a chave da licença do SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="23c37-878">_**Figura 45:** insira a chave da licença do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="23c37-878">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="23c37-879">Quando solicitado, reinicie a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-879">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="23c37-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="23c37-880"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="23c37-881">Depois de instalar o SIOS DataKeeper em ambos os nós, você precisa de configuração de saudação de toostart.</span><span class="sxs-lookup"><span data-stu-id="23c37-881">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="23c37-882">meta de saudação da configuração de saudação é toohave a replicação de dados síncrono entre Olá adicionais VHDs anexados tooeach de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-882">hello goal of hello configuration is toohave synchronous data replication between hello additional VHDs attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="23c37-883">Iniciar hello DataKeeper gerenciamento e a ferramenta de configuração e, em seguida, selecione **conectar servidor**.</span><span class="sxs-lookup"><span data-stu-id="23c37-883">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="23c37-884">(Na Figura 46, essa opção é marcada em vermelho.)</span><span class="sxs-lookup"><span data-stu-id="23c37-884">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="23c37-886">_**Figura 46:** Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="23c37-886">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="23c37-887">Insira o nome da saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-887">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Figura 47: Inserir nome de saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação][sap-ha-guide-figure-3037]

  <span data-ttu-id="23c37-889">_**Figura 47:** Inserir nome de saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação_</span><span class="sxs-lookup"><span data-stu-id="23c37-889">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="23c37-890">Crie trabalho de replicação de saudação entre dois nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-890">Create hello replication job between hello two nodes.</span></span>

  ![Figura 48: Criar trabalho de replicação][sap-ha-guide-figure-3038]

  <span data-ttu-id="23c37-892">_**Figura 48:** Criar trabalho de replicação_</span><span class="sxs-lookup"><span data-stu-id="23c37-892">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="23c37-893">Um assistente orienta você pelo processo de saudação de criação de um trabalho de replicação.</span><span class="sxs-lookup"><span data-stu-id="23c37-893">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="23c37-894">Defina nome hello, endereço TCP/IP e o volume de disco do nó de origem hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-894">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Figura 49: Definir nome de saudação do trabalho de replicação de saudação][sap-ha-guide-figure-3039]

  <span data-ttu-id="23c37-896">_**Figura 49:** definir nome de saudação do trabalho de replicação Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-896">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Figura 50: Definir dados base de saudação do nó de hello, que deve ser um nó de origem atual Olá][sap-ha-guide-figure-3040]

  <span data-ttu-id="23c37-898">_**Figura 50:** definir Olá dados base nó hello, que deve ser um nó de origem atual Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-898">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="23c37-899">Defina nome hello, endereço TCP/IP e volume de disco do nó de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-899">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Figura 51: Definir Olá dados base nó hello, que deve ser um nó de destino atual Olá][sap-ha-guide-figure-3041]

  <span data-ttu-id="23c37-901">_**Figura 51:** definir Olá dados base nó hello, que deve ser um nó de destino atual Olá_</span><span class="sxs-lookup"><span data-stu-id="23c37-901">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="23c37-902">Defina os algoritmos de compactação de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-902">Define hello compression algorithms.</span></span> <span data-ttu-id="23c37-903">Em nosso exemplo, é recomendável que você compactar o fluxo de replicação de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-903">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="23c37-904">Especialmente em situações de ressincronização, compactação de saudação do fluxo de replicação Olá reduz drasticamente o tempo de ressincronização.</span><span class="sxs-lookup"><span data-stu-id="23c37-904">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="23c37-905">Observe que a compactação utiliza recursos de CPU e RAM de saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23c37-905">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="23c37-906">À medida que aumenta a taxa de compactação hello, portanto Olá volume de recursos de CPU usados.</span><span class="sxs-lookup"><span data-stu-id="23c37-906">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="23c37-907">Você também pode ajustar essa configuração mais tarde.</span><span class="sxs-lookup"><span data-stu-id="23c37-907">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="23c37-908">Outra configuração necessário toocheck é se replicação Olá ocorre de forma assíncrona ou síncrona.</span><span class="sxs-lookup"><span data-stu-id="23c37-908">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="23c37-909">*Quando você protege configurações SAP ASCS/SCS, deve usar a replicação síncrona*.</span><span class="sxs-lookup"><span data-stu-id="23c37-909">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definir detalhes de replicação][sap-ha-guide-figure-3042]

  <span data-ttu-id="23c37-911">_**Figura 52:** Definir detalhes de replicação_</span><span class="sxs-lookup"><span data-stu-id="23c37-911">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="23c37-912">Defina se o volume de saudação que é replicada pelo trabalho de replicação de saudação deve ser configuração de cluster Clustering de Failover do Windows Server tooa representado como um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="23c37-912">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="23c37-913">Para a configuração do SAP ASCS/SCS hello, selecione **Sim** para que o Windows hello cluster vê Olá volume replicado como um disco compartilhado que possa ser usada como um volume de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-913">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: Selecione Sim tooset Olá replicadas volume como um volume de cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="23c37-915">_**Figura 53:** selecione **Sim** tooset Olá replicadas volume como um cluster_</span><span class="sxs-lookup"><span data-stu-id="23c37-915">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="23c37-916">Depois de criar o volume de Olá, ferramenta de configuração e gerenciamento de DataKeeper Olá mostra que esse trabalho de replicação hello está ativo.</span><span class="sxs-lookup"><span data-stu-id="23c37-916">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Figura 54: Espelhamento síncrono DataKeeper para Olá SAP ASCS/SCS compartilhamento de disco está ativo][sap-ha-guide-figure-3044]

  <span data-ttu-id="23c37-918">_**Figura 54:** espelhamento síncrono DataKeeper para hello SAP ASCS/SCS de compartilhamento de disco está ativo_</span><span class="sxs-lookup"><span data-stu-id="23c37-918">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="23c37-919">Gerenciador de Cluster de failover agora mostra o disco hello como um disco DataKeeper, conforme mostrado na Figura 55.</span><span class="sxs-lookup"><span data-stu-id="23c37-919">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: O Gerenciador de Cluster de Failover mostra disco Olá DataKeeper replicado][sap-ha-guide-figure-3045]

  <span data-ttu-id="23c37-921">_**Figura 55:** Gerenciador de Cluster de Failover que DataKeeper replicada de disco Olá mostra_</span><span class="sxs-lookup"><span data-stu-id="23c37-921">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="23c37-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar o sistema do SAP NetWeaver Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-922"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="23c37-923">Não descrevemos a instalação DBMS hello como as configurações variam dependendo Olá sistema DBMS usado.</span><span class="sxs-lookup"><span data-stu-id="23c37-923">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="23c37-924">No entanto, vamos supor que as questões de alta disponibilidade com hello DBMS sejam resolvidos com funcionalidades Olá Olá diferentes DBMS fornecedores oferecem suporte a para o Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-924">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="23c37-925">Por exemplo, o Always On ou o Espelhamento de Banco de Dados para SQL Server e Oracle Data Guard para bancos de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="23c37-925">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="23c37-926">No cenário de saudação que usamos neste artigo, não adicionamos mais proteção toohello DBMS.</span><span class="sxs-lookup"><span data-stu-id="23c37-926">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="23c37-927">Não existem considerações especiais quando diferentes serviços DBMS interagem com esse tipo de configuração de SAP ASCS/SCS clusterizada no Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-927">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-928">procedimentos de instalação de saudação de sistemas SAP NetWeaver ABAP, sistemas de Java e sistemas ABAP + Java são quase idênticos.</span><span class="sxs-lookup"><span data-stu-id="23c37-928">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="23c37-929">diferença de Hello mais significativa é que um sistema SAP ABAP tem uma instância do ASCS.</span><span class="sxs-lookup"><span data-stu-id="23c37-929">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="23c37-930">Olá sistema SAP Java tem uma instância SCS.</span><span class="sxs-lookup"><span data-stu-id="23c37-930">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="23c37-931">Olá sistema SAP ABAP + Java tem uma instância do ASCS e Olá de uma instância SCS em execução no mesmo grupo de cluster de failover de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23c37-931">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="23c37-932">As diferenças de instalação para cada pilha de instalação do SAP NetWeaver serão explicitamente mencionadas.</span><span class="sxs-lookup"><span data-stu-id="23c37-932">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="23c37-933">Você pode presumir que todas as outras partes são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="23c37-933">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="23c37-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="23c37-934"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23c37-935">Verifique se não tooplace sua página de arquivo no DataKeeper espelhado volumes.</span><span class="sxs-lookup"><span data-stu-id="23c37-935">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="23c37-936">O DataKeeper não dá suporte a volumes espelhados.</span><span class="sxs-lookup"><span data-stu-id="23c37-936">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="23c37-937">Você pode deixar o arquivo de página na unidade temporária Olá D de uma máquina virtual do Azure, que é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-937">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="23c37-938">Se ele não estiver lá, mova Olá Windows página arquivo toodrive D da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-938">If it's not already there, move hello Windows page file toodrive D of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="23c37-939">Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="23c37-939">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="23c37-940">Criando um nome de host virtual para instância do SAP ASCS/SCS Olá clusterizado</span><span class="sxs-lookup"><span data-stu-id="23c37-940">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="23c37-941">Instalando Olá SAP primeiro nó de cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-941">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="23c37-942">Modificando Olá SAP perfil da instância do ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-942">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="23c37-943">Adicionando uma porta de investigação</span><span class="sxs-lookup"><span data-stu-id="23c37-943">Adding a probe port</span></span>
- <span data-ttu-id="23c37-944">Abrir a porta de investigação Olá Windows firewall</span><span class="sxs-lookup"><span data-stu-id="23c37-944">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="23c37-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Criar um nome de host virtual para instância do SAP ASCS/SCS Olá clusterizado</span><span class="sxs-lookup"><span data-stu-id="23c37-945"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="23c37-946">No Gerenciador de DNS do Windows hello, crie uma entrada DNS para o nome de host virtual Olá da instância do ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-946">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="23c37-947">Olá endereço IP que você atribuir o nome de host virtual toohello de saudação ASCS/SCS instância deve ser Olá mesmo como endereço IP de saudação que você atribuiu tooAzure balanceador de carga (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="23c37-947">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="23c37-948">Olá o endereço IP do nome de host do SAP ASCS/SCS virtual hello (**pr1-ascs-sap**) Olá mesmo como endereço IP de saudação do balanceador de carga do Azure (**pr1 de balanceamento de carga de ascs**).</span><span class="sxs-lookup"><span data-stu-id="23c37-948">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definir a entrada DNS Olá para o nome virtual do cluster Olá SAP ASCS/SCS e endereço TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="23c37-950">_**Figura 56:** definir Olá entrada DNS para o nome virtual do cluster Olá SAP ASCS/SCS e endereço TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="23c37-950">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="23c37-951">toodefine Olá IP endereço atribuído toohello nome de host virtual, selecione **Gerenciador DNS** > **domínio**.</span><span class="sxs-lookup"><span data-stu-id="23c37-951">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="23c37-953">_**Figura 57:** Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="23c37-953">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="23c37-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar Olá SAP primeiro nó de cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-954"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="23c37-955">Executar Olá primeiro cluster nó opção no nó de cluster A. Por exemplo, em Olá **pr1-ascs-0** host.</span><span class="sxs-lookup"><span data-stu-id="23c37-955">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="23c37-956">portas de padrão de saudação tookeep para hello Azure interno balanceador de carga, selecione:</span><span class="sxs-lookup"><span data-stu-id="23c37-956">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="23c37-957">**Sistema ABAP**: número da instância **ASCS** **00**</span><span class="sxs-lookup"><span data-stu-id="23c37-957">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="23c37-958">**Sistema Java**: número da instância **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="23c37-958">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="23c37-959">**Sistema ABAP + Java**: número da instância **ASCS** **00** e número da instância **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="23c37-959">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="23c37-960">toouse instância números diferente de 00 para Olá ABAP ASCS instância e 01 para instância de Java SCS hello, primeiro é necessário toochange Olá interno de carga do Azure balanceador padrão de balanceamento de carga regras, descritas na [carga do alteração Olá ASCS/SCS padrão balanceamento de regras de Balanceador de carga interno do Azure Olá][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="23c37-960">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="23c37-961">Olá Avançar algumas tarefas não são descritas na documentação de instalação do SAP padrão hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-961">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-962">Olá documentação de instalação do SAP descreve como tooinstall Olá primeiro nó do cluster ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="23c37-962">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="23c37-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar Olá SAP perfil da instância do ASCS/SCS Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-963"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="23c37-964">É necessário tooadd um novo parâmetro de perfil.</span><span class="sxs-lookup"><span data-stu-id="23c37-964">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="23c37-965">parâmetro de perfil Hello impede que conexões entre os processos de trabalho do SAP e o servidor de enfileiramento de saudação fechar quando eles estão ociosos por muito tempo.</span><span class="sxs-lookup"><span data-stu-id="23c37-965">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="23c37-966">Mencionamos cenário problema Olá [adicionar entradas de registro em ambos os nós de cluster da instância do SAP ASCS/SCS Olá][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="23c37-966">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="23c37-967">Essa seção também apresentamos dois parâmetros de conexão de TCP/IP básicos do alterações toosome.</span><span class="sxs-lookup"><span data-stu-id="23c37-967">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="23c37-968">Na segunda etapa, você precisa tooset Olá enqueue servidor toosend um `keep_alive` sinalizar para que conexões Olá não atingem o limite de ociosidade do balanceador de carga interno do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23c37-968">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="23c37-969">Olá toomodify perfil SAP da instância do ASCS/SCS hello:</span><span class="sxs-lookup"><span data-stu-id="23c37-969">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="23c37-970">Adicione este parâmetro de perfil toohello perfil de instância SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="23c37-970">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="23c37-971">Em nosso exemplo, o caminho de saudação é:</span><span class="sxs-lookup"><span data-stu-id="23c37-971">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="23c37-972">Por exemplo, o perfil de instância SAP SCS toohello e caminho correspondente:</span><span class="sxs-lookup"><span data-stu-id="23c37-972">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="23c37-973">alterações de saudação tooapply, reinicie a instância de SAP ASCS /SCS de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-973">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="23c37-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Adicionar uma porta de investigação</span><span class="sxs-lookup"><span data-stu-id="23c37-974"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="23c37-975">Use o trabalho de configuração do balanceador de carga interno Olá investigação funcionalidade toomake Olá todo o cluster com o balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="23c37-975">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="23c37-976">Balanceador de carga interno do Azure Olá geralmente distribui a carga de trabalho de entrada de saudação igualmente entre as máquinas virtuais participantes.</span><span class="sxs-lookup"><span data-stu-id="23c37-976">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="23c37-977">No entanto, isso não funcionará em algumas configurações de cluster porque apenas uma instância está ativa.</span><span class="sxs-lookup"><span data-stu-id="23c37-977">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="23c37-978">Olá outra instância é passiva e não pode aceitar qualquer carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-978">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="23c37-979">Uma funcionalidade de teste ajuda quando atribui de Balanceador de carga interno do Azure Olá trabalha instância ativa do tooan somente.</span><span class="sxs-lookup"><span data-stu-id="23c37-979">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="23c37-980">Com a funcionalidade de investigação hello, balanceador de carga interno Olá pode detectar quais instâncias ativas e direcionar apenas a instância Olá com carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-980">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="23c37-981">tooadd uma porta de investigação:</span><span class="sxs-lookup"><span data-stu-id="23c37-981">tooadd a probe port:</span></span>

1.  <span data-ttu-id="23c37-982">Seleção atual de saudação **ProbePort** configuração executando Olá comando PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="23c37-982">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="23c37-983">Executá-lo de dentro de uma das máquinas virtuais de saudação na configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="23c37-983">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="23c37-984">Defina uma porta de investigação.</span><span class="sxs-lookup"><span data-stu-id="23c37-984">Define a probe port.</span></span> <span data-ttu-id="23c37-985">número de porta de investigação de padrão de saudação é **0**.</span><span class="sxs-lookup"><span data-stu-id="23c37-985">hello default probe port number is **0**.</span></span> <span data-ttu-id="23c37-986">Em nosso exemplo, usamos a porta de investigação **62000**.</span><span class="sxs-lookup"><span data-stu-id="23c37-986">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: a porta de investigação de configuração de cluster de saudação é 0 por padrão][sap-ha-guide-figure-3048]

  <span data-ttu-id="23c37-988">_**Figura 58:** porta de investigação de configuração de cluster do saudação padrão é 0_</span><span class="sxs-lookup"><span data-stu-id="23c37-988">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="23c37-989">número de porta de saudação é definido em modelos do SAP do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="23c37-989">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="23c37-990">Você pode atribuir o número da porta Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23c37-990">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="23c37-991">tooset um novo valor de ProbePort para Olá  **SAP <*SID*> IP * * recurso de cluster, execute Olá script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="23c37-991">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="23c37-992">Atualize as variáveis do PowerShell de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="23c37-992">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="23c37-993">Após a execução do script hello, será solicitada toorestart Olá SAP grupo tooactivate Olá as alterações de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-993">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="23c37-994">Depois de você colocar Olá  **SAP <*SID*> * * função online de cluster, verifique **ProbePort** é definir o novo valor de toohello.</span><span class="sxs-lookup"><span data-stu-id="23c37-994">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Porta de cluster de saudação de investigação depois de definir o novo valor de saudação][sap-ha-guide-figure-3049]

  <span data-ttu-id="23c37-996">_**Figura 59:** investigação de porta de cluster Olá depois de definir o novo valor de saudação_</span><span class="sxs-lookup"><span data-stu-id="23c37-996">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="23c37-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra a porta de investigação Olá Windows firewall</span><span class="sxs-lookup"><span data-stu-id="23c37-997"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="23c37-998">É necessário tooopen uma porta de investigação de firewall do Windows em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-998">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="23c37-999">Use Olá script tooopen uma porta de investigação de firewall do Windows a seguir.</span><span class="sxs-lookup"><span data-stu-id="23c37-999">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="23c37-1000">Atualize as variáveis do PowerShell de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="23c37-1000">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="23c37-1001">Olá **ProbePort** está definido muito**62000**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1001">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="23c37-1002">Agora você pode acessar o compartilhamento de arquivo hello  **\\\ascsha-clsap\sapmnt** de outros hosts, como **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1002">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="23c37-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar a instância de banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="23c37-1003"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="23c37-1004">o banco de dados do tooinstall Olá instância, siga o processo de saudação descrito Olá documentação de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-1004">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="23c37-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar o segundo nó de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-1005"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="23c37-1006">tooinstall Olá segundo cluster, siga etapas Olá Olá guia de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-1006">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="23c37-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Alterar tipo de inicialização de saudação da instância de serviço do Windows de ES do SAP Olá</span><span class="sxs-lookup"><span data-stu-id="23c37-1007"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="23c37-1008">Alterar o tipo de inicialização de saudação do hello serviço Windows de ES do SAP muito**automática (início atrasado)** em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="23c37-1008">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Alterar o tipo de serviço de saudação para Olá SAP es instância toodelayed automática][sap-ha-guide-figure-3050]

<span data-ttu-id="23c37-1010">_**Figura 60:** alterar tipo de serviço Olá para Olá SAP es instância toodelayed automática_</span><span class="sxs-lookup"><span data-stu-id="23c37-1010">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="23c37-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Olá principal servidor de aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-1011"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="23c37-1012">Instalar a instância de servidor de aplicativo principal (PAS) hello <*SID*> - di - 0 na máquina virtual Olá que você designou toohost Olá PAS.</span><span class="sxs-lookup"><span data-stu-id="23c37-1012">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="23c37-1013">Não há dependências nas configurações específicas do Azure ou do DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="23c37-1013">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="23c37-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Olá adicional servidor de aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="23c37-1014"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="23c37-1015">Instale um servidor de aplicativo adicionais SAP (AAS) em todas as máquinas virtuais de saudação que você designou toohost uma instância de servidor de aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="23c37-1015">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="23c37-1016">Por exemplo, em <*SID*> - di - 1 muito <*SID*> - di -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="23c37-1016">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="23c37-1017">Isso conclui a instalação de saudação de um sistema SAP NetWeaver de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="23c37-1017">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="23c37-1018">Em seguida, continue com o teste de failover.</span><span class="sxs-lookup"><span data-stu-id="23c37-1018">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="23c37-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testar o failover de instância SAP ASCS/SCS hello e replicação SIOS</span><span class="sxs-lookup"><span data-stu-id="23c37-1019"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="23c37-1020">É fácil tootest e monitorar um failover de instância SAP ASCS/SCS e replicação de disco SIOS usando o Gerenciador de Cluster de Failover e ferramenta de saudação SIOS DataKeeper gerenciamento e configuração.</span><span class="sxs-lookup"><span data-stu-id="23c37-1020">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="23c37-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> A instância do SAP ASCS/SCS está em execução no Nó A do Cluster</span><span class="sxs-lookup"><span data-stu-id="23c37-1021"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="23c37-1022">Olá **PR1 SAP** grupo de cluster está em execução no nó de cluster A. Por exemplo, em **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1022">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="23c37-1023">Atribuir a unidade de disco de saudação compartilhada S, que faz parte da saudação **PR1 SAP** cluster grupo e a instância do ASCS/SCS Olá usa, toocluster nó A.</span><span class="sxs-lookup"><span data-stu-id="23c37-1023">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![Figura 61: Gerenciador de Cluster de Failover: grupo de clusters do SAP < SID > Olá está em execução em um nó de cluster][sap-ha-guide-figure-5000]

<span data-ttu-id="23c37-1025">_**Figura 61:** Gerenciador de Cluster de Failover: Olá SAP <*SID*> grupo de cluster está em execução em um nó de cluster_</span><span class="sxs-lookup"><span data-stu-id="23c37-1025">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="23c37-1026">Olá SIOS DataKeeper gerenciamento e a ferramenta de configuração, você pode ver esse disco compartilhado Olá dados são replicados sincronicamente de unidade de volume de origem Olá S no nó de cluster de uma unidade de volume de destino S toohello no nó de cluster B. Por exemplo, ele é replicado do **pr1-ascs-0 [10.0.0.40]** muito**pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1026">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: Na SIOS DataKeeper replicar volume local saudação do nó de cluster de um nó de toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="23c37-1028">_**Figura 62:** na SIOS DataKeeper replicar o volume de local de saudação do nó de cluster de um nó de toocluster B_</span><span class="sxs-lookup"><span data-stu-id="23c37-1028">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="23c37-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover de nó A toonode B</span><span class="sxs-lookup"><span data-stu-id="23c37-1029"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="23c37-1030">Escolha um dos tooinitiate opções um failover de saudação SAP <*SID*> grupo de cluster de nó do cluster nó A toocluster b:</span><span class="sxs-lookup"><span data-stu-id="23c37-1030">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="23c37-1031">Usar o Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="23c37-1031">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="23c37-1032">Usar o PowerShell de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="23c37-1032">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="23c37-1033">Reinicie o nó de cluster A no sistema de operacional de convidado do Windows hello (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="23c37-1033">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="23c37-1034">Reinicie o nó de cluster A partir Olá portal do Azure (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="23c37-1034">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="23c37-1035">Reiniciar um do nó de cluster usando o PowerShell do Azure (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).</span><span class="sxs-lookup"><span data-stu-id="23c37-1035">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="23c37-1036">Após o failover, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B. Por exemplo, ele está em execução no **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1036">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: No Gerenciador de Cluster de Failover, grupo de clusters do SAP < SID > Olá está em execução no nó de cluster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="23c37-1038">_**Figura 63**: no Gerenciador de Cluster de Failover, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B_</span><span class="sxs-lookup"><span data-stu-id="23c37-1038">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="23c37-1039">Olá disco compartilhado é agora montado no cluster de nó B. SIOS DataKeeper é replicar dados de unidade de volume de origem S em cluster no nó B tootarget volume unidade S no nó de cluster A. Por exemplo, ele está replicando de **pr1-ascs-1 [10.0.0.41]** muito**pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="23c37-1039">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: SIOS DataKeeper replica volume local Olá nó B toocluster do nó de cluster A][sap-ha-guide-figure-5003]

  <span data-ttu-id="23c37-1041">_**Figura 64:** SIOS DataKeeper replica volume local Olá no nó do cluster no nó B toocluster um_</span><span class="sxs-lookup"><span data-stu-id="23c37-1041">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
