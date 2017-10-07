---
title: "aaaAzure implantação de máquinas virtuais de DBMS para SAP NetWeaver | Microsoft Docs"
description: "Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5654dac7-4204-4387-b312-3d8b2898eb3a
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 501f6fbc2baa379b706e95d2bfba377ac129b382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-dbms-deployment-for-sap-netweaver"></a>Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1114181]:https://launchpad.support.sap.com/#/notes/1114181
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
[2171857]:https://launchpad.support.sap.com/#/notes/2171857
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md 
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8
[dbms-guide-managed-disks]:dbms-guide.md#f42c6cb5-d563-484d-9667-b07ae51bce29

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md 
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e 
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
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
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

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

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
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
[virtual-machines-azurerm-versus-azuresm]:../../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
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
[virtual-machines-manage-availability-linux]:../../linux/manage-availability.md
[virtual-machines-manage-availability-windows]:../../windows/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
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

Este guia faz parte da documentação de saudação na implementação e a implantação de software do SAP Olá no Microsoft Azure. Antes de ler este guia, leia Olá [guia de planejamento e implementação][planning-guide]. Este documento aborda a implantação de saudação de vários sistemas de gerenciamento de banco de dados relacional (RDBMS) e produtos relacionados em combinação com o SAP em máquinas virtuais Microsoft Azure (VMs) usando Olá infraestrutura do Azure como recursos de um serviço (IaaS).

Olá papel complementa Olá documentação de instalação do SAP e observações sobre o SAP, que representam os recursos principais de saudação para instalações e implantações de software SAP em fornecidos plataformas.

## <a name="general-considerations"></a>Considerações gerais
Neste capítulo, são introduzidas considerações sobre a execução de sistemas DBMS relacionados ao SAP em VMs do Azure. Há referências de alguns sistemas DBMS toospecific neste capítulo. Em vez disso, sistemas DBMS específicos de saudação são abordados neste documento, após este capítulo.

### <a name="definitions-upfront"></a>Definições prévias
Em todo o documento hello, usamos Olá termos a seguir:

* IaaS: infraestrutura como serviço.
* PaaS: plataforma como serviço.
* SaaS: software como serviço.
* Componente SAP: um aplicativo SAP individual como ECC, BW, Solution Manager ou EP.  Os componentes SAP podem ser baseados em tecnologias ABAP ou Java tradicionais ou em um aplicativo não baseado em NetWeaver, como o Business Objects.
* Ambiente SAP: um ou mais componentes SAP logicamente agrupados tooperform uma função empresarial como desenvolvimento, QAS, treinamento, DR ou produção.
* Estrutura SAP: Refere-se toohello inteiros ativos SAP em um cliente cenário de TI. Olá estrutura SAP inclui todos os ambientes de produção e não seja de produção.
* Sistema SAP: Olá uma combinação da camada de DBMS e camada de aplicativo de, por exemplo, um sistema de desenvolvimento SAP ERP, sistema de teste do SAP BW, sistema de produção SAP CRM, etc. Em implantações do Azure, não é suportado toodivide essas duas camadas entre local e o Azure. Isso significa que um sistema SAP é implantado localmente ou no Azure. No entanto, você pode implantar sistemas diferentes de saudação de uma estrutura SAP no Azure ou no local. Por exemplo, você pode implantar os sistemas Olá desenvolvimento e teste de SAP CRM no Azure, mas Olá SAP CRM produção sistema local.
* Implantação somente em nuvem: uma implantação onde Olá assinatura do Azure não está conectado por meio de uma site a site ou rota expressa conexão toohello local infraestrutura de rede. Na documentação comum do Azure, esses tipos de implantações também são descritos como implantações 'Somente em nuvem'. Máquinas virtuais implantadas com esse método são acessadas por meio de saudação à Internet e pontos de extremidade públicos da Internet atribuídos toohello VMs no Azure. Olá Active Directory (AD) local e o DNS não for estendido tooAzure nesses tipos de implantações. Portanto, Olá VMs não fazem parte de saudação do Active Directory local. Observação: as implantações somente em nuvem neste documento são definidas como estruturas da SAP completas que estão sendo executadas exclusivamente no Azure sem extensão do Active Directory nem resolução de nomes do local para a nuvem pública. Não há suporte para configurações somente em nuvem para sistemas SAP de produção ou configurações onde STMS SAP ou outros recursos de local precisam toobe usado entre os sistemas SAP hospedados no Azure e os recursos que residem no local.
* Entre locais: Descreve um cenário onde as VMs são implantada tooan assinatura do Azure que tem conectividade de rota expressa entre Olá local datacenter(s) e o Azure, de vários locais ou de site a site. Na documentação comum do Azure, esses tipos de implantações também são descritas como cenários entre instalações. Olá motivo conexão Olá é tooextend domínios locais, Active Directory no local e o DNS local no Azure. Olá paisagem local é estendido toohello ativos do Azure da assinatura de saudação. Com esta extensão, Olá VMs pode ser parte do domínio de local de saudação. Usuários de domínio do domínio do hello local podem acessar servidores hello e podem executar serviços nas VMs (como serviços DBMS). A comunicação e resolução de nomes entre VMs implantadas de forma local e VMs implantadas no Azure são possíveis. Esperamos que este cenário mais comum de saudação toobe para implantar os ativos SAP no Azure. Para obter mais informações, confira [este artigo][vpn-gateway-cross-premises-options] e [este][vpn-gateway-site-to-site-create].

> [!NOTE]
> Implantações entre instalações de sistemas SAP em que máquinas virtuais do Azure que executam sistemas SAP são membros de um domínio local têm suporte para sistemas SAP de produção. Configurações entre locais têm suporte para a implantação de partes ou estruturas da SAP completas no Azure. Até mesmo em execução estrutura SAP completa de saudação no Azure, é necessário ter as VMs sendo parte do domínio local e anúncios. Em versões anteriores da documentação de saudação, falamos sobre cenários de TI híbrida, onde o termo de saudação 'Híbrida' está enraizado no Olá fato de haver uma conectividade entre locais entre local e o Azure. Nesse caso, 'Híbrido' também significa que Olá VMs no Azure fazem parte da saudação local do Active Directory.
> 
> 

Alguma documentação da Microsoft descreve cenários entre instalações de modo um pouco diferente, especialmente para configurações de HA do DBMS. No caso de saudação de documentos relacionados à SAP do hello, cenário entre locais de saudação apenas resume toohaving um site a site ou privado (rota expressa) conectividade e toohello fato que o cenário SAP Olá é distribuído entre local e o Azure.

### <a name="resources"></a>Recursos
Olá a guias a seguir estão disponíveis para o tópico Olá das implantações do SAP no Azure:

* [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]
* [Implantação de Máquinas Virtuais do Azure para SAP NetWeaver][deployment-guide]
* [Implantação do DBMS de Máquinas Virtuais do Azure para SAP NetWeaver][dbms-guide]

Olá SAP observações a seguir está relacionadas toohello tópico do SAP no Azure:

| Número da observação | Title |
| --- | --- |
| [1928533] |Aplicativos SAP no Azure: tipos de VM do Azure e produtos com suporte |
| [2015553] |SAP no Microsoft Azure: pré-requisitos de suporte |
| [1999351] |Solução de problemas de monitoramento aprimorado do Azure para SAP |
| [2178632] |Métricas-chave de monitoramento para SAP no Microsoft Azure |
| [1409604] |Virtualização no Windows: monitoramento avançado |
| [2191498] |SAP no Linux com o Azure: monitoramento avançado |
| [2039619] |Aplicativos SAP no Microsoft Azure usando Olá banco de dados Oracle: suporte para produtos e versões |
| [2233094] |DB6: Aplicativos SAP no Azure usando o IBM DB2 para Linux, UNIX e Windows - informações adicionais |
| [2243692] |Linux na VM do Microsoft Azure (IaaS): problemas de licença SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: notas de instalação |
| [2002167] |Red Hat Enterprise Linux 7.x: instalação e atualização |
| [2069760] |Atualização e instalação do SAP do Oracle Linux 7.x |
| [1597355] |Recomendação de troca de espaço para Linux |
| [2171857] |Oracle Database 12c – suporte do sistema de arquivos em Linux |
| [1114181] |Oracle Database 11g – suporte do sistema de arquivos em Linux |


Leia também Olá [Wiki de SCN](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) que contém todas as observações sobre o SAP para Linux.

Você deve ter um conhecimento prático sobre hello arquitetura do Microsoft Azure e como as máquinas virtuais do Microsoft Azure são implantadas e operadas. Você pode encontrar mais informações em <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Estamos **não** discutir sobre a plataforma Microsoft Azure como uma oferta de serviço (PaaS) do hello plataforma Microsoft Azure. Este artigo é sobre a execução de um sistema de gerenciamento de banco de dados (DBMS) em máquinas virtuais Microsoft Azure (IaaS) exatamente como você executaria Olá DBMS em seu ambiente local. As funcionalidades e recursos do banco de dados entre essas duas ofertas são muito diferentes e não devem ser misturados uns com os outros. Confira também: <https://azure.microsoft.com/services/sql-database/>
> 
> 

Já que estamos discutindo IaaS, em geral configuração e instalação do Windows, Linux e DBMS Olá são essencialmente Olá igual a qualquer máquina virtual ou máquina bare-metal que você instala no local. No entanto, há algumas decisões de implementação de gerenciamento de sistema e arquitetura que são diferentes ao utilizar IaaS. Olá finalidade deste documento é tooexplain Olá arquitetura e sistema de gerenciamento diferenças específicas que você deve estar preparado ao usar IaaS.

Em geral, hello áreas de diferença discutidas neste documento são:

* Planejando o layout VM/disco adequado Olá de tooensure de sistemas SAP tem layout de arquivo de dados apropriados hello e possa obter IOPS suficientes para sua carga de trabalho.
* Considerações de rede ao usar IaaS.
* Toouse de recursos de banco de dados específico no layout do banco de dados da ordem toooptimize hello.
* Considerações sobre backup e restauração no IaaS.
* Uso de diferentes tipos de imagens para implantação.
* Alta disponibilidade no Azure IaaS.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Estrutura de uma implantação do RDBMS
Em ordem toofollow neste capítulo, é necessário toounderstand que foi apresentado no [isso] [ deployment-guide-3] capítulo Olá [guia de implantação] [ deployment-guide]. Conhecimento sobre Olá série de VM diferente e suas diferenças e as diferenças de padrão do Azure e armazenamento Premium devem ser entendidas e conhecidas antes de ler este capítulo.

Até março de 2015, discos, que contém um sistema operacional foram limitado too127 GB de tamanho. Essa limitação foi removida em março de 2015 (para obter informações, confira <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/>). Daí em discos de sistema de operacional Olá contendo pode ter Olá mesmo tamanho como qualquer outro disco. No entanto, ainda estamos preferir uma estrutura de implantação de onde o sistema de operacional hello, DBMS e eventuais binários SAP são separados dos arquivos de banco de dados de saudação. Portanto, esperamos que sistemas SAP em execução em máquinas virtuais do Azure tem Olá base VM (ou disco) instalado com o sistema operacional de hello, executáveis do sistema de gerenciamento de banco de dados e arquivos executáveis do SAP. Olá dados do DBMS e arquivos de log são armazenados no armazenamento do Azure (Standard ou Premium armazenamento) em discos separados e anexados como discos lógicos toohello original do Azure imagem do sistema operacional VM. 

Dependentes de aproveitar o armazenamento Premium ou padrão do Azure (por exemplo, usando Olá série DS ou série GS VMs) existe são outras cotas no Azure, que são documentadas [aqui (Linux)] [ virtual-machines-sizes-linux] e [aqui (Windows)][virtual-machines-sizes-windows]. Ao planejar seu layout de disco, você precisa toofind Olá melhor equilíbrio das cotas Olá para Olá itens a seguir:

* número de saudação de arquivos de dados.
* número de saudação de discos que contêm arquivos de saudação.
* cotas de IOPS de saudação de um único disco.
* transferência de dados Olá por disco.
* número de saudação de discos de dados adicionais possíveis por tamanho da VM.
* Olá geral taxa de transferência de armazenamento uma VM pode fornecer.

O Azure impõe uma cota de IOPS por disco de dados. Essas cotas são diferentes para discos hospedados no Armazenamento Standard e no Armazenamento Premium do Azure. As latências de e/s também são muito diferentes entre dois tipos de armazenamento hello, com o armazenamento Premium fornecendo fatores melhor latências de e/s. Cada um dos diferentes tipos de VM Olá tem um número limitado de discos de dados que você é capaz de tooattach. Outra restrição é que somente determinados tipos de VM podem aproveitar o Armazenamento Premium do Azure. Isso significa que a decisão de saudação para um determinado tipo VM pode ser direcionada não só saudação da CPU e requisitos de memória, mas também por Olá IOPS, requisitos de taxa de transferência do disco e latência que normalmente são dimensionados com número de saudação de discos ou Olá tipo de discos de armazenamento Premium. Especialmente com o armazenamento Premium tamanho Olá de um disco também pode ser determinado pelo número de saudação de IOPS e taxa de transferência que precisa toobe obtida por cada disco.

fato Olá Olá taxa IOPS geral, número de saudação de discos montados e Olá tamanho de saudação VM estão todos interligados pode causar uma configuração do Azure de um sistema SAP toobe diferente de sua implantação local. limites IOPS Olá por LUN são geralmente configuráveis em implantações locais. Enquanto com armazenamento do Azure esses limites são fixas como armazenamento Premium dependente do tipo de disco de saudação. Portanto com implantações locais, vemos configurações de cliente de servidores de banco de dados que usam muitos volumes diferentes para executáveis especiais como SAP e Olá DBMS ou volumes especiais para bancos de dados temporários ou espaços para tabela. Quando desse sistema local é movido tooAzure, isso pode levar tooa perda de largura de banda IOPS potencial por desperdiçar um disco para executáveis ou bancos de dados que não executam nenhum ou não um lote de IOPS. Portanto, em VMs do Azure é recomendável que executáveis DBMS e SAP Olá ser instalado no disco Olá SO se possível.

Olá posicionamento dos arquivos de banco de dados de saudação e arquivos de log e tipo de saudação do armazenamento do Azure usado, deve ser definido por requisitos de taxa de transferência, latência e IOPS. Em ordem toohave IOPS suficientes para o log de transações hello, você pode ser forçado tooleverage vários discos para log de transações de saudação do arquivo ou usam um disco de armazenamento Premium maior. Nesse caso um criaria um software de RAID (por exemplo, Windows Pool de armazenamento do Windows ou MDADM e LVM (Gerenciador de Volume lógico) para Linux) com discos de saudação, que contém o log de transações de saudação.

- - -
> ![Windows][Logo_Windows] Windows
> 
> Unidade D:\ em uma VM do Azure é uma unidade não persistente, que é apoiada por alguns discos locais no nó de computação do Azure hello. Como não persistente, isso significa que qualquer conteúdo de toohello as alterações feitas na unidade D:\ da saudação é perdido quando Olá VM for reinicializado. Por "alterações", queremos dizer arquivos salvos, diretórios criados, aplicativos instalados etc.
> 
> ![Linux][Logo_Linux] Linux
> 
> Máquinas virtuais do Linux do Azure automaticamente montar uma unidade em /mnt/resource é uma unidade não persistente respalda discos locais no nó de computação do Azure hello. Porque é não persistente, isso significa que qualquer toocontent as alterações feitas em /mnt/resource são perdidos quando Olá VM for reinicializado. Por alterações, queremos dizer arquivos salvos, diretórios criados, aplicativos instalados etc.
> 
> 

- - -
Dependente de saudação série de VM do Azure, os discos locais Olá Olá computação nó mostrar diferentes de desempenho, que podem ser categorizados como:

* A0-A7: desempenho muito limitado. Não pode ser usado para nada além do arquivo de paginação do Windows
* A8-A11: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s
* Série D: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s
* Série DS: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s
* Série G: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s
* Série GS: características de desempenho excelentes, com aproximadamente dez mil IOPS e taxa de transferência superior a 1 GB/s

Instruções acima estiver aplicando os tipos de VM toohello certificados com o SAP. Olá séries de VMs com excelente IOPS e taxa de transferência se qualificam para aproveitar alguns recursos do DBMS, como tempdb ou espaço de tabela temporária.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Cache de VMs e discos de dados
Quando criamos os discos de dados por meio do portal hello ou quando montamos tooVMs discos carregados, podemos escolher se o tráfego de e/s de saudação entre hello VM e os discos localizados no armazenamento do Azure são armazenados em cache. O Armazenamento Standard e Premium do Azure usam duas tecnologias diferentes para esse tipo de cache. Em ambos os casos, o cache de Olá em si seria backup em disco na Olá mesmas unidades usadas por hello em disco temporário (D:\ no Windows) ou /mnt/resource no Linux de saudação VM.

Para o armazenamento padrão do Azure tipos de cache possíveis Olá são:

* Sem cache
* Cache de leitura
* Cache de leitura e gravação

Em ordem tooget desempenho consistente e previsível, você deve definir Olá em cache no armazenamento do Azure padrão para todos os discos que contém **arquivos de dados relacionados a DBMS, arquivos de log e too'NONE de espaço de tabela '**. Olá caching de saudação VM pode permanecer com o padrão de saudação.

Para o armazenamento do Azure Premium Olá opções de cache a seguir existe:

* Sem cache
* Cache de leitura

Recomendação para o armazenamento do Azure Premium é tooleverage **cache para arquivos de dados de leitura** de banco de dados do SAP hello e escolha **nenhum cache para discos de saudação de arquivos de log**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>RAID de software
Como já mencionado acima, você precisa toobalance número de saudação de IOPS necessário para arquivos de banco de dados de saudação em número de saudação de discos é possível configurar e Olá IOPS máximo que uma VM do Azure fornece por disco ou tipo de disco de armazenamento Premium. Toodeal de maneira mais fácil com hello que em discos de carga de IOPS é toobuild um RAID de software em discos diferentes hello. Em seguida, coloque um número de arquivos de dados de saudação SAP DBMS em Olá que LUNs gravados fora do software Olá RAID. Dependente de requisitos de hello, que talvez você queira tooconsider Olá uso de armazenamento Premium também desde dois Olá três discos de armazenamento Premium diferentes fornecem maior cota de IOPS que os discos com base no armazenamento padrão. Além disso Olá significativa melhor a latência de e/s fornecido pelo armazenamento Premium do Azure. 

Mesmo se aplica a toohello o log de transações de diferentes sistemas DBMS hello. Com muitos deles apenas adicionar mais arquivos de Tlog não ajuda como sistemas DBMS Olá gravar em um dos arquivos de saudação em apenas uma vez. Se houver necessidade de taxas mais altas de IOPS de um único padrão de que armazenamento com base em disco pode oferecer, você pode distribuir através de vários discos de armazenamento padrão ou você pode usar um tipo de disco de armazenamento Premium maior que, além de taxas mais altas de IOPS também fornece fatores menor latência de gravação da saudação E/s no log de transações de saudação.

As situações ocorridas em implantações do Azure que seriam beneficiadas pelo uso de um RAID de software são:

* O Log de Transações/Log de Refazer requerem mais IOPS do que o Azure fornece para um único disco. Conforme mencionado acima, isso pode ser resolvido com a criação de um LUN em vários discos usando um RAID de software.
* E/s cargas de trabalho distribuição desigual sobre Olá diferentes arquivos de dados do banco de dados do SAP hello. Nesses casos, um pode apresentar um arquivo de dados atingir a cota de saudação em vez disso, muitas vezes. Enquanto outros arquivos de dados ainda não estão obtendo toohello fechar cota de IOPS de um único disco. Olá tais casos solução mais fácil é toobuild um LUN através de vários discos usando um RAID de software. 
* Você não souber quais Olá exata e/s carga de trabalho por arquivo de dados é e apenas aproximadamente saber o que Olá é de carga de trabalho de IOPS Olá DBMS geral. Toodo mais fácil é toobuild um LUN com hello ajuda de um RAID de software. soma de saudação de cotas de vários discos por trás desse LUN, em seguida, deve atender Olá conhecido IOPS taxa.

- - -
> ![Windows][Logo_Windows] Windows
> 
> É recomendável usar Espaços de Armazenamento do Windows se a execução for feita em Windows Server 2012 ou superior. É mais eficiente do que a Divisão do Windows de versões anteriores do Windows. Talvez seja necessário toocreate Olá Pools de armazenamento do Windows e espaços de armazenamento por comandos do PowerShell ao usar o Windows Server 2012 como sistema operacional. comandos do PowerShell Olá podem ser encontrados aqui <https://technet.microsoft.com/library/jj851254.aspx>
> 
> ![Linux][Logo_Linux] Linux
> 
> Somente MDADM e LVM (Gerenciador de Volume lógico) são suportado toobuild um software RAID no Linux. Para obter mais informações, leia Olá artigos a seguir:
> 
> * [Configurar RAID de software no Linux][virtual-machines-linux-configure-raid] (para MDADM)
> * [Configurar o LVM em uma VM Linux no Azure][virtual-machines-linux-configure-lvm]
> 
> 

- - -
Considerações para aproveitar o VM-series costumam ser capaz de toowork com o armazenamento do Azure Premium são:

* Demandas de latências de e/s são fechar toowhat SAN/NAS dispositivos entregar.
* Demanda de fatores de melhores latências de E/S que o Armazenamento Standard do Azure pode fornecer.
* Maior IOPS por VM do que o que pode ser obtido com vários discos de Armazenamento Standard em um determinado tipo de VM.

Desde Olá armazenamento do Azure subjacente replica cada nós de armazenamento do disco tooat pelo menos três, simples de RAID 0 distribuição pode ser usada. Não há nenhum tooimplement necessidade RAID5 ou RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Armazenamento do Microsoft Azure
Repositórios de armazenamento do Microsoft Azure Olá VM de base (com o sistema operacional) e discos ou nós de armazenamento separados tooat pelo menos três BLOBs. Ao criar uma conta de armazenamento ou disco gerenciado, há uma opção de proteção, conforme mostrado aqui:

![Replicação geográfica habilitada para a conta de armazenamento do Azure][dbms-guide-figure-100]

Armazenamento de replicação Local do Azure (localmente redundante) fornece níveis de proteção contra perda de dados devido a falha de tooinfrastructure que alguns clientes podem ter condições toodeploy. Conforme mostrado, acima, há quatro opções diferentes com um quinto sendo uma variação de uma saudação primeiro três. Analisando-as mais de perto, podemos distinguir:

* **LRS (Armazenamento com Redundância Local) Premium**: o Armazenamento Premium do Azure fornece alto desempenho, dá suporte a disco de baixa latência para máquinas virtuais executando cargas de trabalho intensas de E/S. Há três réplicas de dados de saudação em Olá mesmo datacenter do Azure de uma região do Azure. Olá cópias estão em diferentes domínios de falha e atualização (para conceitos, consulte [isso] [ planning-guide-3.2] capítulo Olá [guia de planejamento][planning-guide]). No caso de uma réplica dos dados de saudação vai fora de serviço devido a falha de nó de armazenamento tooa ou falha de disco, uma nova réplica é gerada automaticamente.
* **Armazenamento localmente redundante (LRS)**: nesse caso, há três réplicas dos dados de saudação em hello mesmo datacenter do Azure de uma região do Azure. Olá cópias estão em diferentes domínios de falha e atualização (para conceitos, consulte [isso] [ planning-guide-3.2] capítulo Olá [guia de planejamento][planning-guide]). No caso de uma réplica dos dados de saudação vai fora de serviço devido a falha de nó de armazenamento tooa ou falha de disco, uma nova réplica é gerada automaticamente. 
* **Armazenamento redundante da replicação geográfica (GRS)**: nesse caso, há uma replicação assíncrona que alimenta um adicional de três réplicas dos dados de saudação em outra região do Azure, que é na maioria dos casos Olá Olá mesma região geográfica (como Norte da Europa e Oeste Europa). Isso resulta em três réplicas adicionais, de modo que há seis réplicas no total. Uma variação disso é uma adição em que os dados de saudação na região do Azure do hello geograficamente replicados podem ser usados para fins de leitura (acesso de leitura com redundância geográfica).
* **Zona de armazenamento com redundância (ZRS)**: nesse caso, réplicas Olá três Olá dados permanecem no hello mesma região do Azure. Conforme explicado em [isso] [ planning-guide-3.1] capítulo Olá [guia de planejamento] [ planning-guide] uma região do Azure pode ser um número de datacenters nas proximidades. No caso de saudação de LRS réplicas de Olá poderiam ser distribuídas em Olá diferentes data centers que fazem uma região do Azure.

Mais informações podem ser encontradas [aqui][storage-redundancy].

> [!NOTE]
> Para implantações de DBMS, uso de saudação do armazenamento com redundância geográfica não é recomendado
> 
> A replicação geográfica do Armazenamento do Azure é assíncrona. A replicação dos discos individuais montado tooa única VM não estão sincronizados na etapa de bloqueio. Portanto, não é adequado tooreplicate arquivos DBMS que são distribuídos em discos diferentes ou implantados em um software RAID com base em vários discos. O software DBMS requer que o armazenamento em disco persistente Olá seja sincronizado com precisão em LUNs diferentes e discos/eixos subjacentes. O software DBMS usa vários toosequence mecanismos atividades de gravação de e/s e um DBMS relata que o armazenamento em disco Olá direcionado por replicação hello está corrompido se elas variarem até mesmo em alguns milissegundos. Portanto, se você realmente quiser uma configuração de banco de dados com um banco de dados estendido por vários discos de replicação geográfica, tal replicação precisa toobe executada com meios de banco de dados e a funcionalidade. Um não deve confiar na replicação geográfica do armazenamento do Azure tooperform esse trabalho. 
> 
> problema de saudação é tooexplain mais simples com um sistema de exemplo. Vamos supor que você tenha um sistema SAP carregado no Azure, que tem oito discos que contém arquivos de dados de saudação DBMS mais de um disco que contém o arquivo de log de transações de saudação. Cada um desses nove discos ter dados gravados toothem em um método consistente toohello DBMS, de acordo com se dados hello está sendo gravados toohello arquivos de log de transação ou de dados.
> 
> Replicar geograficamente tooproperly Olá dados e manter uma imagem consistente do banco de dados, o conteúdo de saudação de todos os discos de nove seria ter toobe replicado geograficamente em operações de e/s de saudação ordem exata Olá foram executadas em discos diferentes Olá nove. No entanto, a replicação geográfica do armazenamento do Azure não permite toodeclare dependências entre discos. Isso significa que a replicação geográfica do armazenamento do Microsoft Azure não conhece Olá fato conteúdo Olá desses nove discos diferentes relacionado tooeach outros e que as alterações de dados de saudação são consistentes apenas ao replicar em operações de e/s de Olá Olá ordem aconteceu em todos os discos de nove hello.
> 
> Além de chances de ser alta que imagens replicado geograficamente de Olá no cenário de saudação não fornecem uma imagem de banco de dados consistente, há também uma penalidade de desempenho que é exibido com o armazenamento geograficamente redundante severos pode afeta o desempenho. Em resumo, não use esse tipo de redundância de armazenamento para cargas de trabalho do tipo DBMS.
> 
> 

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Mapeando VHDs em contas de armazenamento do serviço de máquina virtual do Azure
Este capítulo só se aplica a contas de armazenamento tooAzure. Se você planejar toouse gerenciados discos, limitações, Olá mencionado neste capítulo não se aplicam. Para obter mais informações sobre Managed Disks, leia o capítulo [Managed Disks][dbms-guide-managed-disks] deste guia.

Uma Conta de Armazenamento do Azure não é apenas um constructo administrativo, mas também uma entidade de limitações. Enquanto as limitações de saudação podem variar se falamos sobre uma conta de armazenamento do Azure padrão ou uma conta de armazenamento do Azure Premium. limitações e recursos exata Olá são listadas [aqui][storage-scalability-targets]

Portanto para o armazenamento padrão do Azure, é importante toonote há um limite em Olá IOPS por conta de armazenamento (linha contendo 'Taxa Total de solicitação' [artigo Olá][storage-scalability-targets]). Além disso, há um limite inicial de 100 contas de armazenamento por assinatura do Azure (a partir de julho de 2015). Portanto, é recomendável toobalance IOPS de VMs entre várias contas de armazenamento ao usar o armazenamento padrão do Azure. Enquanto uma única VM idealmente usa uma conta de armazenamento se possível. Então, se falamos sobre implantações de DBMS em que cada VHD que é hospedado no Armazenamento Standard do Azure pode atingir seu limite de cota, você deve implantar apenas 30 a 40 VHDs por Conta de Armazenamento do Azure que usa o Armazenamento Standard do Azure. Em Olá outro lado, se você utilizar o armazenamento Premium do Azure e deseja toostore volumes de banco de dados grande, você pode ser refinado em termos de IOPS. Mas uma Conta de Armazenamento Premium do Azure é muito mais restritiva no volume de dados do que uma Conta de Armazenamento Standard do Azure. Como resultado, você pode implantar apenas um número limitado de VHDs em uma conta de armazenamento do Azure Premium antes de atingir o limite de volume de dados hello. No final de saudação pense em uma conta de armazenamento do Azure como uma "SAN Virtual" que limitou os recursos em IOPS e/ou capacidade. Como resultado, Olá tarefa permanece, como em implantações locais, layout de saudação toodefine de saudação VHDs dos diferentes sistemas SAP Olá sobre Olá diferentes 'dispositivos SAN imaginários' ou contas de armazenamento do Azure.

Para o armazenamento do Azure padrão, não é recomendável toopresent armazenamento de armazenamento diferentes contas tooa única VM se possível.

Ao usar o hello DS ou GS-série de máquinas virtuais do Azure, é possível toomount VHDs fora do padrão contas de armazenamento do Azure e contas de armazenamento Premium. Casos de uso como gravar backups no armazenamento padrão feito VHDs e dados do DBMS e arquivos de log no armazenamento Premium vêm toomind onde esse armazenamento heterogêneo pode ser aproveitado. 

Com base em implantações de clientes e teste too40 em torno de 30 VHDs contendo arquivos de dados do banco de dados e arquivos de log podem ser provisionados em uma única conta do Azure padrão armazenamento com desempenho aceitável. Como mencionado anteriormente, limitação de saudação de uma conta de armazenamento do Azure Premium é provavelmente toobe capacidade de dados de saudação pode armazenar e não IOPS.

Como com SAN dispositivos locais, compartilhamento requer algum monitoramento em ordem tooeventually detecte afunilamentos em uma conta de armazenamento do Azure. Olá extensão de monitoramento do Azure para SAP e Olá portal do Azure são ferramentas que podem ser usado toodetect ocupado contas de armazenamento do Azure que possam estar tendo um desempenho abaixo do ideal de e/s.  Se essa situação for detectada, é recomendável tooanother de VMs ocupado toomove conta de armazenamento do Azure. Consulte toohello [guia de implantação] [ deployment-guide] para obter detalhes sobre como tooactivate Olá SAP hospedar recursos de monitoramento.

Outro artigo que resume as práticas recomendadas em relação ao Armazenamento Standard e às Contas de Armazenamento Standard do Azure pode ser encontrado aqui <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="f42c6cb5-d563-484d-9667-b07ae51bce29"></a>Managed Disks
Managed Disks são um novo tipo de recurso no Azure Resource Manager que pode ser usado em vez de VHDs armazenados em Contas de Armazenamento do Azure. Discos gerenciados alinham automaticamente com hello conjunto de disponibilidade da máquina virtual de saudação estiverem anexados tooand, portanto, aumentar a disponibilidade de sua máquina virtual e serviços Olá em execução na máquina virtual de Olá Olá. toolearn mais, leia Olá [artigo de visão geral](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

O SAP atualmente dá suporte apenas a Managed Disks Premium. Leia a Nota SAP [1928533] para obter mais detalhes.

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Movendo implantado VMs de DBMS do armazenamento do Azure Standard tooAzure armazenamento Premium
Podemos encontrar algum cenários onde como cliente deseja toomove uma VM implantada do armazenamento do Azure padrão para armazenamento Premium do Azure. Se os discos são armazenados em contas de armazenamento do Azure, isso não é possível sem mover fisicamente os dados de saudação. Há vários meta de saudação do tooachieve maneiras:

* Você pode simplesmente copiar todos os VHDs, VHD base, bem como VHDs de dados em uma nova Conta de Armazenamento Premium do Azure. Geralmente você escolheu número Olá de VHDs no armazenamento padrão do Azure não devido ao fato Olá que é necessário o volume de dados hello. Mas necessários que muitos VHDs devido a saudação IOPS. Agora que você mover tooAzure poderá ir maneira menos tooachieve de VHDs de armazenamento de Premium Olá mesma taxa de transferência IOPS. Considerando Olá fato de que no armazenamento padrão do Azure, você paga Olá usados dados e tamanho de disco nominal do hello, número de saudação de VHDs não importa em termos de custos. No entanto, com o armazenamento do Azure Premium, você pagaria para tamanho de disco nominal hello. Portanto, a maioria dos clientes Olá tente tookeep Olá inúmeros VHDs do Azure no armazenamento Premium no Olá número tooachieve necessário Olá produtividade de IOPS necessário. Portanto, a maioria dos clientes decidir em forma de saudação de um simples 1:1 cópia.
* Se ainda não estiver montado, você montará um único VHD que pode conter um backup de banco de dados do seu banco de dados SAP. Depois do backup hello, desmontar todos os VHDs incluindo Olá VHD contendo Olá backup e Olá cópia VHD de base e Olá VHD com o backup de saudação em uma conta de armazenamento Premium do Azure. Em seguida, implanta Olá que VM com base em Olá base VHD e montagem Olá VHD com o backup de saudação. Agora você pode criar adicionais Premium armazenamento discos vazios para Olá VM toorestore usado o banco de dados de saudação em. Isso pressupõe que Olá DBMS permite toochange caminhos toohello dados e arquivos de log como parte do processo de restauração de saudação.
* Outra possibilidade é uma variação do processo anterior hello, onde você simplesmente copie o backup Olá VHD no armazenamento Premium do Azure e anexá-lo contra uma VM que é implantado e instalado recentemente.
* possibilidade de quarto Olá escolha quando estiver em necessidade toochange número de saudação dos arquivos de dados do banco de dados. Nesse caso, você executaria uma cópia homogênea do sistema SAP usando a exportação/importação. Coloque os exportar arquivos em um VHD que é copiado para uma conta de armazenamento do Azure Premium e anexação-lo tooa VM que você use processos de importação toorun hello. Os clientes usam essa possibilidade principalmente quando quiserem que o número de saudação toodecrease dos arquivos de dados.

Se você usar discos gerenciados, você pode migrar tooPremium armazenamento por:

1. Desalocar máquina virtual de saudação
2. Se necessário, redimensione tamanho tooa da máquina virtual Olá que dá suporte ao armazenamento Premium (por exemplo, DS ou GS)
3. Alterar tooPremium de tipo de conta do hello disco gerenciado (SSD)
4. Inicie a máquina virtual

### <a name="deployment-of-vms-for-sap-in-azure"></a>Implantação de VMs para SAP no Azure
Microsoft Azure oferece várias maneiras toodeploy VMs e discos associados. Portanto, é toounderstand importantes diferenças de saudação desde preparativos das VMs Olá podem diferir dependentes na forma de saudação de implantação. Em geral, analisamos cenários Olá descritos Olá capítulos a seguir.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Implantar uma VM do hello Azure Marketplace
Como tootake Microsoft ou de terceiros fornecido a imagem de saudação do Azure Marketplace toodeploy sua VM. Depois de implantar a VM no Azure, você seguir Olá mesmas diretrizes e ferramentas tooinstall Olá software SAP em sua VM como você faria em um ambiente local. Para instalar o software SAP hello dentro Olá VM do Azure, SAP e Microsoft recomendam carregar e armazenar mídia de instalação do SAP Olá em discos ou toocreate uma VM do Azure trabalhando como 'servidor de arquivos', que contém todas as mídias instalação SAP necessárias Olá.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Como implantar uma VM com uma imagem generalizada específica do cliente
Devido a requisitos de patch toospecific sobre a sua versão do SO ou DBMS, imagens de saudação fornecida em hello Azure Marketplace podem não atender às suas necessidades. Portanto, talvez seja necessário toocreate uma VM usando sua própria imagem de VM do SO/DBMS 'private', que pode ser implantada várias vezes depois. tooprepare uma imagem 'private' para eliminação de duplicação, Olá que SO deve ser generalizado no hello local VM. Consulte toohello [guia de implantação] [ deployment-guide] para obter detalhes sobre como toogeneralize uma VM.

Se você já tiver instalado conteúdo SAP em sua VM local (especialmente para sistemas de camada 2), você pode adaptar configurações do sistema SAP Olá depois de implantação de saudação do hello VM do Azure por meio da instância de saudação renomear procedimento Olá provisionamento de Software SAP com suporte Manager (nota da SAP [1619720]). Caso contrário, você pode instalar o software SAP de saudação posteriormente após a implantação de saudação do hello VM do Azure.

A partir do conteúdo do banco de dados de Olá usado pelo Olá aplicativo SAP, você pode gerar conteúdo Olá recentemente por uma instalação do SAP ou pode importar seu conteúdo para o Azure usando um VHD com um backup de banco de dados DBMS ou aproveitando os recursos de saudação DBMS toodirectly backup no armazenamento do Microsoft Azure. Nesse caso, você pode também preparar VHDs com hello dados do DBMS e local do arquivos de log e, em seguida, importá-los como discos no Azure. Mas, transferência de saudação de dados DBMS que estão sendo carregados do local tooAzure funcionaria em discos VHD que precisam toobe preparados no local.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Mover uma VM do tooAzure local com um disco não generalizado
Planejar toomove um sistema SAP específico do local tooAzure (comparar e deslocar). Isso pode ser feito Carregando disco hello, que contém Olá OS binários SAP Olá e eventuais binários de DBMS mais discos de saudação com dados hello e arquivos de log de saudação DBMS tooAzure. Em tooscenario oposta #2 acima, você lembre-Olá hostname, SID do SAP e contas de usuário SAP Olá VM do Azure como eles foram configurados no ambiente local de saudação. Portanto, não é necessário generalizar a imagem de saudação. Neste caso, aplica-se principalmente para cenários entre locais onde uma parte da saudação estrutura SAP é executada no local e partes no Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Alta disponibilidade e recuperação de desastre com VMs do Azure
O Azure oferece Olá seguintes funcionalidades de alta disponibilidade (HA) e recuperação de desastres (DR), que se aplicam a toodifferent componentes que usaríamos para implantações de DBMS e SAP

### <a name="vms-deployed-on-azure-nodes"></a>VMs implantadas em nós do Azure
Olá plataforma Azure não oferece recursos como migração dinâmica para VMs implantadas. Isso significa que se for necessária manutenção em um cluster de servidor no qual uma VM é implantada, Olá VM precisa tooget interrompido e reiniciado. A manutenção no Azure é realizada usando os chamados domínios de atualização em clusters de servidores. A manutenção é realizada em apenas um domínio de atualização de cada vez. Durante a reinicialização, houver uma interrupção de serviço durante a saudação que VM for desligada, manutenção é executada e reinicialização de VM. No entanto, a maioria dos fornecedores DBMS fornecer funcionalidade de alta disponibilidade e recuperação de desastres que reinicia os serviços DBMS de saudação em outro nó rapidamente se o nó primário Olá não está disponível. Olá plataforma Azure oferece funcionalidade toodistribute máquinas virtuais, armazenamento e outros serviços do Azure entre domínios de atualização tooensure planejado manutenção ou falhas de infraestrutura só afetem um pequeno subconjunto de VMs ou serviços.  Com um planejamento cuidadoso, é tooachieve possíveis infraestruturas de tooon local comparável de níveis de disponibilidade.

Conjuntos de disponibilidade do Microsoft Azure são um agrupamento lógico de VMs ou serviços que garante que as VMs e outros serviços são distribuída toodifferent falha e domínios de atualização em um cluster, de modo que apenas haveria um desligamento de nó em qualquer ponto no tempo (leitura [esse (Linux)] [ virtual-machines-manage-availability-linux] ou [esta (Windows)] [ virtual-machines-manage-availability-windows] artigo para obter mais detalhes).

Ele precisa toobe configurado por finalidade ao distribuir VMs, como visto aqui:

![Definição de conjunto de disponibilidade para configurações de HA do DBMS][dbms-guide-figure-200]

Se quisermos toocreate configurações de alta disponibilidade de implantações do DBMS (independentes da saudação individual HA do DBMS funcionalidade usado), as VMs de DBMS Olá precisa:

* Adicionar Olá VMs toohello mesma rede Virtual do Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Olá VMs da configuração de HA Olá também deve estar no hello mesma sub-rede. Resolução de nomes entre sub-redes Olá não é possível em implantações somente em nuvem, funciona apenas de resolução IP. Usando a conectividade de ExpressRoute ou site a site para implantações Entre Instalações, uma rede com pelo menos uma sub-rede já está estabelecida. Resolução de nomes é feita de acordo com o toohello local infraestrutura de rede e diretivas de AD. 

[comment]: <> (Teste TODO MSSedusch se ainda for verdadeiro no ARM)

#### <a name="ip-addresses"></a>Endereços IP
É altamente recomendável toosetup Olá VMs para configurações de HA de forma resiliente. Contar endereços IP tooaddress parceiros HA Olá na configuração de HA Olá não é confiável no Azure, a menos que os endereços IP estáticos são usados. Há dois conceitos de "Desligamento" no Azure:

* Desligamento por meio do portal do Azure ou o cmdlet do PowerShell do Azure Stop-AzureRmVM: nesse caso, a saudação Máquina Virtual é desligada e desalocada. Sua conta do Azure não é cobrada por essa VM para que sejam únicas cobranças do hello que incorrem em armazenamento Olá usado. No entanto, se o endereço IP privado de Olá Olá da interface de rede não for estático, Olá endereço IP é liberado e não há garantia dessa que interface de rede Olá obtém endereço IP antigo Olá atribuído novamente após uma reinicialização do hello VM. Executar Olá desligado por meio de saudação do Azure portal ou chamando AzureRmVM parar automaticamente faz com que desalocação. Se você não quiser toodeallocate Olá máquina e use Stop-AzureRmVM - StayProvisioned 
* Se você desligar Olá VM por meio de um nível de sistema operacional, Olá VM obtém desligado e não é desalocada. No entanto, nesse caso, sua conta do Azure é ainda será cobrada para Olá VM, apesar de saudação desligada. Nesse caso, a atribuição de saudação do tooa de endereço IP hello interrompida VM permanece intacto. Desligando Olá VM de dentro de não força automaticamente desalocação.

Mesmo para cenários entre locais, por padrão um desligamento e a desalocação significa desatribuição dos endereços IP de saudação do hello VM, mesmo se políticas locais nas configurações de DHCP são diferentes. 

* Olá exceção se atribui uma estático IP endereço tooa interface de rede como descrita [aqui][virtual-networks-reserved-private-ip].
* Nesse caso o endereço IP de saudação permanece fixo como interface de rede de saudação não é excluído.

> [!IMPORTANT]
> Em ordem tookeep Olá todo implantação simple e gerenciável, Olá claro recomendação é toosetup Olá VMs estão em parceria em uma configuração de HA do DBMS ou recuperação de desastres no Azure de forma que não há uma resolução de nomes está funcionando entre hello diferentes VMs envolvidas.
> 
> 

## <a name="deployment-of-host-monitoring"></a>Implantação do monitoramento de host
Para o uso produtivo de aplicativos SAP em máquinas virtuais do Azure, o SAP requer host de tooget de capacidade Olá dados de monitoramento de hosts físicos do hello executando Olá máquinas virtuais do Azure. É necessário um nível de patch do Agente de Host SAP específico que habilite essa funcionalidade no SAPOSCOL e no Agente de Host SAP. nível de patch exata Hello está documentado na nota da SAP [1409604].

Para obter detalhes de saudação sobre implantação de componentes que fornecem tooSAPOSCOL de dados do host e SAP Host Agent e o gerenciamento de ciclo de vida de saudação desses componentes, consulte toohello [guia de implantação][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>TooMicrosoft informações específicas do SQL Server
### <a name="sql-server-iaas"></a>IaaS do SQL Server
Começando com o Microsoft Azure, você pode facilmente migrar seus aplicativos existentes do SQL Server criados na plataforma de servidor Windows tooAzure máquinas virtuais. SQL Server em uma máquina Virtual permite que você tooreduce Olá custo total de propriedade de implantação, gerenciamento e manutenção de aplicativos de amplitude empresarial migrando facilmente esses tooMicrosoft de aplicativos do Azure. Com o SQL Server em uma máquina Virtual do Azure, administradores e desenvolvedores ainda podem usar Olá mesmas ferramentas de desenvolvimento e administração que estão disponíveis no local. 

> [!IMPORTANT]
> Não estamos discutindo Microsoft Azure SQL Database, que é uma plataforma como uma oferta de serviço de saudação plataforma Microsoft Azure. discussão Olá neste artigo é sobre a execução de produto do SQL Server hello como é conhecido para implantações de local em máquinas virtuais do Azure, aproveitando Olá infraestrutura como um recurso de serviço do Azure. As funcionalidades e recursos do banco de dados entre essas duas ofertas são muito diferentes e não devem ser misturados entre si. Confira também: <https://azure.microsoft.com/services/sql-database/>
> 
> 

É altamente recomendável tooreview [isso] [ virtual-machines-sql-server-infrastructure-services] documentação antes de continuar.

Em Olá seguintes partes de seções de partes da documentação Olá no link de saudação acima são agregados e mencionados. Informações especificas do SAP também são mencionadas e alguns conceitos são descritos mais detalhadamente. No entanto, é altamente recomendável toowork pela documentação Olá acima primeiro antes de ler a documentação específica do SQL Server hello.

Há algumas informações específicas do SQL Server no IaaS que você deve conhecer antes de continuar:

* **SLA da Máquina Virtual**: há um SLA para Máquinas Virtuais em execução no Azure, que pode ser encontrado aqui: <https://azure.microsoft.com/support/legal/sla/>  
* **Suporte de versão do SQL**: para clientes SAP, damos suporte para SQL Server 2008 R2 e superior na máquina virtual do Microsoft Azure. Não há suporte para edições anteriores. Examine esta [Instrução de suporte](https://support.microsoft.com/kb/956893) geral para obter mais detalhes. Observe que, em geral, o SQL Server 2008 também tem suporte da Microsoft. No entanto, devido a funcionalidade toosignificant para SAP, que foi introduzida com o SQL Server 2008 R2, SQL Server 2008 R2 é a versão mínima Olá para SAP. Tenha em mente que o SQL Server 2012 e 2014 foi ampliado com a integração mais aprofundada no cenário de IaaS hello (como o backup diretamente no armazenamento do Azure). Portanto, nós restringimos este tooSQL papel Server 2012 e 2014 com seu nível de patch mais recente do Azure.
* **Suporte ao recurso de SQL**: a maioria dos recursos do SQL Server tem suporte em Máquinas Virtuais do Microsoft Azure com algumas exceções. **Não há suporte para o clustering de failover do SQL Server usando discos compartilhados**.  Tecnologias distribuídas, como o espelhamento de banco de dados, grupos de disponibilidade AlwaysOn, replicação, envio de logs e Service Broker, têm suporte dentro de uma única região do Azure. O AlwaysOn do SQL Server também tem suporte entre diferentes regiões do Azure, conforme documentado aqui: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Saudação de revisão [declaração de suporte](https://support.microsoft.com/kb/956893) para obter mais detalhes. Um exemplo de como toodeploy uma configuração de AlwaysOn é mostrada na [isso] [ virtual-machines-workload-template-sql-alwayson] artigo. Além disso, confira Olá práticas recomendadas documentadas [aqui][virtual-machines-sql-server-infrastructure-services] 
* **Desempenho do SQL**: estamos confiantes de que o Microsoft Azure máquinas virtuais hospedadas funcionam muito bem em ofertas de virtualização de nuvem pública de tooother de comparação, mas os resultados individuais podem variar. Confira [este][virtual-machines-sql-server-performance-best-practices] artigo.
* **Usando imagens do Azure Marketplace**: toodeploy de maneira mais rápida de saudação uma nova VM do Microsoft Azure é toouse uma imagem de saudação do Azure Marketplace. Há imagens na hello Azure Marketplace, que contêm o SQL Server. imagens de saudação onde do SQL Server já está instalado não podem ser usadas imediatamente para aplicativos do SAP NetWeaver. motivo Olá é o agrupamento do saudação padrão do SQL Server é instalado dentro dessas imagens e não agrupamento Olá exigido pelos sistemas SAP NetWeaver. Em ordem toouse essas imagens, verifique etapas Olá documentadas no capítulo [usando uma imagem do SQL Server fora do Microsoft Azure Marketplace de saudação][dbms-guide-5.6]. 
* Consulte os [Detalhes de preço](https://azure.microsoft.com/pricing/) para obter mais informações. Olá [guia de licenciamento do SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) e [guia de licenciamento do SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) também são um recurso importante.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Diretrizes de configuração do SQL Server para instalações do SQL Server relacionadas ao SAP em VMs do Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Recomendações sobre a estrutura de VM/VHD para implantações do SQL Server relacionadas ao SAP
Conforme a descrição geral do hello, executáveis do SQL Server devem ser localizado ou instalados na unidade de sistema de saudação do disco do sistema operacional da VM hello (unidade c:\).  Normalmente, a maioria dos bancos de dados do sistema saudação do SQL Server não é utilizadas em um alto nível pela carga de trabalho do SAP NetWeaver. Portanto, bancos de dados de sistema de saudação do SQL Server (master, msdb e modelo) podem permanecer no Olá unidade C:\ também. Uma exceção poderia ser tempdb, que, no caso de saudação de alguns SAP ERP e todas as cargas de trabalho do BW, pode exigir o maior volume de dados ou o volume de operações de e/s, que não cabe na Olá VM original. Para tais sistemas, Olá etapas a seguir deve ser executada:

* Mover Olá tempdb principal dados arquivos toohello mesma unidade lógica que hello (s) de dados primário do banco de dados do SAP hello.
* Adicione qualquer tooeach de arquivos de dados tempdb adicional de saudação outras unidades lógicas que contém um arquivo de dados do banco de dados do usuário Olá SAP.
* Adicione Olá tempdb logfile toohello unidade lógica, que contém o arquivo de log Olá usuário do banco de dados.
* **Exclusivamente para tipos VM que usam SSDs local** Olá computação nó de dados tempdb e o log de arquivos podem ser colocados em Olá unidade D:\. No entanto, pode ser recomendável toouse vários arquivos de dados tempdb. Esteja ciente de volumes de unidade D:\ são diferentes com base em Olá tipo de VM.

Essas configurações permitem tempdb tooconsume mais espaço do que a unidade do sistema Olá é capaz de tooprovide. No tamanho do pedido toodetermine Olá adequado de tempdb, é possível verificar tamanhos de tempdb Olá em sistemas existentes, que são executados localmente. Além disso, essa configuração permitiria números de IOPS em relação a tempdb, que não pode ser fornecida com a unidade do sistema hello. Novamente, os sistemas que estejam em execução no local podem ser toomonitor usado e/s de carga de trabalho em relação a tempdb para que você possa derivar os números de IOPS Olá toosee que o esperado em tempdb.

Uma configuração de VM, que executa o SQL Server com um banco de dados do SAP e onde os dados tempdb e o arquivo de log tempdb são colocados na unidade D:\ de saudação pareceria com:

![Configuração de referência da VM IaaS do Azure para SAP][dbms-guide-figure-300]

Lembre-se de que essa unidade D:\ Olá tem Olá tipo VM dependentes de tamanhos diferentes. Dependente de requisito de tamanho de saudação de tempdb pode ser forçado toopair de dados tempdb e arquivos de log com hello SAP do banco de dados e arquivos de log em casos em que a unidade D:\ é muito pequena.

#### <a name="formatting-hello-disks"></a>Formatar discos Olá
Para tamanho do bloco NTFS para discos que contém o log e dados do SQL Server de saudação do servidor de SQL arquivos devem ser 64K. Não há nenhum tooformat de necessidade Olá unidade D:\. Essa unidade vem pré-formatada.

Em ordem toomake se hello restauração ou a criação de bancos de dados não está inicializando os arquivos de dados de saudação zerando o conteúdo de saudação de arquivos de saudação, é necessário ter certeza que Olá usuário contexto saudação do SQL Server está sendo executado tem determinada permissão. Normalmente, os usuários no grupo do administrador do Windows hello têm essas permissões. Se Olá serviço do SQL Server é executado no contexto de usuário de saudação do usuário administrador não - Windows, será necessário tooassign que saudação do usuário 'Executar tarefas de manutenção de volume' direito de usuário.  Consulte os detalhes de saudação neste artigo da Base de Conhecimento Microsoft: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Impacto da compactação do banco de dados
Em configurações onde largura de banda de e/s pode se tornar um fator limitante, todas as medidas, que reduzem o IOPS podem ajudar a carga de trabalho do hello toostretch pode ser executada em um cenário de IaaS como o Azure. Portanto, se ainda não tiver feito, aplicar a compactação de página do SQL Server é altamente recomendável SAP e da Microsoft antes de carregar um tooAzure de banco de dados do SAP existente.

Olá recomendação tooperform compactação de banco de dados antes de carregar tooAzure é indicada por duas razões:

* saudação de toobe dados carregado é menor.
* duração de saudação da execução de compactação de saudação é menor, supondo que você pode usar hardware mais poderoso com mais CPUs ou maior largura de banda de e/s ou menor latência de e/s no local.
* Os tamanhos menores de banco de dados podem causar custos tooless para alocação de disco

A compactação de banco de dados funciona bem nas máquinas virtuais do Azure como o faz localmente. Para obter mais detalhes sobre como toocompress um banco de dados do SQL Server do SAP existente, marque aqui: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blob-storage"></a>SQL Server 2014 – armazenando arquivos do banco de dados arquivos diretamente no Armazenamento de Blobs do Azure
SQL Server 2014 abre arquivos de banco de dados de toostore Olá possibilidade diretamente no repositório de Blob do Azure sem Olá wrapper de um VHD ao redor deles. Principalmente com o uso do armazenamento do Azure Standard ou tipos VM menores, isso permite cenários onde você pode superar os limites de saudação de IOPS deve ser imposta por um número limitado de discos que podem ser montados toosome tipos de VM menores. Isso funciona para bancos de dados de usuário, no entanto, não para bancos de dados de sistema do SQL Server. Ele também funciona para arquivos de log e dados do SQL Server. Se você gostaria que toodeploy um SQL Server do SAP banco de dados dessa maneira, em vez de 'encapsulá-lo' em VHDs, lembre-Olá seguinte:

* Olá toobe de necessidades de conta de armazenamento usada no hello mesma região do Azure como Olá que é usado toodeploy hello VM SQL Server está em execução no.
* Considerações listadas anteriormente sobre distribuição de saudação de VHDs em diferentes contas de armazenamento do Azure se aplicam para esse método de implantações. Significa Olá contagem de operações de e/s em limites de saudação do hello conta de armazenamento do Azure.

[comment]: <> (MSSedusch TODO Porém, isso usará largura de banda de rede e não largura de banda de armazenamento, não é?)

Os detalhes sobre esse tipo de implantação estão listados aqui: <https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure>

Em arquivos de dados ordem toostore do SQL Server diretamente no armazenamento do Azure Premium, você precisa toohave um SQL Server 2014 mínimo a versão de patch, o que é documentado aqui: <https://support.microsoft.com/kb/3063054>. Armazenar arquivos de dados do SQL Server no armazenamento padrão do Azure funciona com a versão lançada de saudação do SQL Server 2014. No entanto, patches mesmo Olá contém outra série de correções, o que fazer uso direto de saudação do armazenamento de Blob do Azure para backups de arquivos de dados do SQL Server e mais confiável. Portanto, é recomendável usar esses patches em geral.

### <a name="sql-server-2014-buffer-pool-extension"></a>Extensão do pool de buffers do SQL Server 2014
O SQL Server 2014 introduziu um novo recurso, chamado Extensão do Pool de Buffers. Essa funcionalidade estende o pool de buffers de saudação do SQL Server, que é mantido na memória com um cache segundo nível que é apoiada por SSDs local de um servidor ou VM. Isso permite que tookeep um maior conjunto de trabalho de dados 'na memória'. Tooaccessing em comparação com o acesso de saudação de armazenamento padrão do Azure para a extensão de saudação do pool de buffers hello, que é armazenado no local SSDs de uma VM do Azure é muitos fatores mais rápido.  Portanto, aproveitando a unidade D:\ local de saudação dos tipos de VM Olá com excelente IOPS e taxa de transferência pode ser uma saudação tooreduce de maneira muito razoável IOPS carregar no armazenamento do Azure e melhorar os tempos de resposta de consultas consideravelmente. Isso se aplica especialmente quando não usar o Armazenamento Premium. No caso de armazenamento Premium e o uso de saudação do hello Cache de leitura do Premium do Azure no nó de computação hello, conforme recomendado para arquivos de dados, não há diferenças significativas são esperadas. Motivo é que ambos os caches (extensão do Pool de buffers do SQL Server e o Cache de leitura de armazenamento Premium) estiver usando discos locais de Olá Olá de nós de computação.
Para obter mais detalhes sobre essa funcionalidade, consulte esta documentação: <https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension> 

### <a name="backuprecovery-considerations-for-sql-server"></a>Considerações sobre backup e recuperação para o SQL Server
Ao implantar o SQL Server no Azure, sua metodologia de backup deve ser examinada. Mesmo se o sistema de saudação não é um sistema de produção, banco de dados do SAP Olá hospedado pelo SQL Server deve ser feito periodicamente. Como o armazenamento do Azure mantém três imagens, um backup agora é menos importante na relação toocompensating uma falha de armazenamento. razão de prioridade de saudação para manter um plano de backup e recuperação adequado é maior que você pode compensar erros lógicos/manuais fornecendo recursos de recuperação pontual. Meta de saudação é tooeither use backups toorestore Olá banco de dados tooa determinado ponto no tempo ou toouse backups Olá no Azure tooseed outro sistema copiando o banco de dados existente do hello. Por exemplo, você pode transferir de uma configuração do sistema de 3 camadas da camada 2 SAP configuração tooa de saudação mesmo sistema restaurando um backup.

Há três maneiras diferentes toobackup do SQL Server tooAzure armazenamento:

1. SQL Server 2012 CU4 e superior pode nativamente backup de bancos de dados tooa URL. Isso é detalhado no blog de saudação [nova funcionalidade no SQL Server 2014 – parte 5 – melhorias de Backup/restauração](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Veja o capítulo [SQL Server 2012 SP1 CU4 e posterior][dbms-guide-5.5.1].
2. TooSQL anterior do SQL Server versões 2012 CU4 pode usar um tooa de toobackup de funcionalidade de redirecionamento VHD e fluxo de gravação da saudação basicamente, mover para um local de armazenamento do Azure que foi configurado. Veja o capítulo [SQL Server 2012 SP1 CU3 e versões anteriores][dbms-guide-5.5.2].
3. método final Hello é tooperform um comando de toodisk backup convencional do SQL Server em um dispositivo de disco. Este é o padrão de implantação de local toohello idênticos e não é discutido em detalhes neste documento.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 e posterior
Essa funcionalidade permite o armazenamento de BLOB de backup tooAzure toodirectly. Sem esse método, você deve fazer o backup de discos tooother, o que consumiam disco e capacidade IOPS. Olá basicamente, trata isso:

 ![Usando o Backup do SQL Server 2012 tooMicrosoft BLOB de armazenamento do Azure][dbms-guide-figure-400]

Nesse caso, a vantagem de saudação é que não é preciso backups do SQL Server toospend discos toostore em. Então você tem menos discos alocados e Olá toda largura de banda do disco de que IOPS pode ser usado para arquivos de log e de dados. Observe que o tamanho máximo de saudação de um backup é limitado tooa máximo de 1 TB conforme documentado na seção de saudação 'Limitações' neste artigo: <https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url#limitations>. Se o tamanho do backup hello, apesar de usar a compactação de Backup do SQL Server exceder 1 TB de tamanho, Olá funcionalidades descritas nos capítulos [SQL Server 2012 SP1 CU3 e versões anteriores] [ dbms-guide-5.5.2] neste documento precisa toobe usado.

[Relacionados documentação](https://docs.microsoft.com/sql/relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure) que descreve a restauração de bancos de dados de backups no armazenamento de Blob do Azure Olá recomendável não toorestore diretamente do armazenamento de BLOBs do Azure se não houver backup hello > 25 GB. recomendação Olá neste artigo simplesmente com base em considerações de desempenho e não devido a restrições de toofunctional. Portanto, diferentes condições podem se aplicar caso a caso.

A documentação sobre como esse tipo de backup é configurado e utilizado pode ser encontrada [neste](https://docs.microsoft.com/sql/relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016) tutorial

Um exemplo de sequência de saudação de etapas pode ser lidos [aqui](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url).

A automatização de backups, é mais alto toomake importância-se de que os BLOBs Olá para cada backup forem nomeadas diferentemente. Caso contrário, eles são substituídos e cadeia de restauração Olá foi interrompida.

Não toomix as coisas entre Olá três tipos diferentes de backups, é aconselhável toocreate contêineres diferentes Olá conta de armazenamento usada para backups. contêineres de saudação podem ser apenas por VM ou por VM e tipo de Backup. esquema de saudação seria semelhante ao seguinte:

 ![Usando o Backup do SQL Server 2012 tooMicrosoft BLOB de armazenamento do Azure – diferentes contêineres na conta de armazenamento separada][dbms-guide-figure-500]

No exemplo hello acima, Olá backups não seriam realizados em Olá mesmo armazenamento de conta onde hello VMs são implantadas. Deve haver uma nova conta de armazenamento especificamente para backups de saudação. Em contas de armazenamento hello, haveria diferentes contêineres criados com uma matriz do tipo de saudação do backup e hello nome VM. Essa segmentação, torna mais fácil backups de saudação tooadministrate de saudação diferentes VMs.

Olá BLOBs um grava diretamente os backups hello, não está adicionando contagem toohello Olá de discos de dados de uma VM. Portanto, um pode maximizar o máximo de saudação de discos de dados montados de saudação específicos SKU de VM para dados de saudação e arquivo de log de transações e ainda executar um backup de um contêiner de armazenamento. 

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 e versões anteriores
Olá primeira etapa, você deve executar na ordem tooachieve um backup diretamente no armazenamento do Azure seria toodownload Olá msi, que é vinculado muito[isso](https://www.microsoft.com/download/details.aspx?id=40740) artigo da KBA.

Baixe o arquivo de instalação Olá x64 e documentação hello. arquivo Hello instala um programa chamado: 'Backup do Microsoft SQL Server tooMicrosoft ferramenta do Azure'. Leia a documentação de saudação do produto Olá completamente.  ferramenta de saudação basicamente funciona Olá maneira a seguir:

* De saudação do servidor SQL, um local de disco para backup do SQL Server de saudação é definido (não use a unidade D:\ de saudação para isso).
* ferramenta de saudação permite toodefine regras, que podem ser usado toodirect diferentes tipos de contêineres de armazenamento do Azure toodifferent backups.
* Depois que as regras de saudação entram em vigor, ferramenta Olá redireciona o fluxo de gravação de saudação do hello tooone de backup de saudação VHDs/discos toohello local de armazenamento do Azure, que foi definido anteriormente.
* ferramenta de saudação deixa um pequeno arquivo stub de tamanho de alguns KB no hello VHD/disco, que foi definido para a saudação do SQL Server backup. **Esse arquivo deve ser deixado no local de armazenamento Olá porque é necessário toorestore novamente do armazenamento do Azure.**
  * Se você tiver perdido o arquivo de stub de saudação (por exemplo por meio de perda de saudação da mídia de armazenamento que continha o arquivo stub de saudação) e você tiver escolhido a opção de saudação do backup tooa conta de armazenamento do Microsoft Azure, você poderá recuperar o arquivo de stub Olá por meio de armazenamento do Microsoft Azure por baixá-lo no contêiner de armazenamento Olá no qual ele foi colocado. Em seguida, você deve colocar o arquivo stub de saudação em uma pasta no computador local Olá onde Olá ferramenta é configurado toohello toodetect e carregamento mesmo contêiner com hello mesma senha de criptografia se a criptografia foi usada com a regra original hello. 

Isso significa que o esquema de saudação conforme descrito acima para versões mais recentes do SQL Server pode ser colocada em prática para versões do SQL Server, que não permitem um local de armazenamento do Azure o endereçamento direto.

Esse método não deve ser usado com versões mais recentes do SQL Server que dão suporte à realização do backup nativamente no armazenamento do Azure. As exceções são onde limitações do backup nativo Olá no Azure estão bloqueando a execução do backup nativo no Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Outros bancos de dados do SQL Server de toobackup possibilidades
Outros bancos de dados de toobackup possibilidades é tooa de discos de dados adicionais tooattach VM que usam backups toostore em. Nesse caso, você precisaria toomake-se de que discos de saudação não estão em execução completos. Se esse for o caso de Olá, você precisaria de discos de saudação toounmount e então toospeak 'arquivar'-lo e substituí-lo por um novo disco vazio. Se você for para esse caminho, você deseja tookeep esses VHDs em contas de armazenamento do Azure separado de saudação que Olá VHDs com arquivos de banco de dados de saudação.

Uma segunda possibilidade é toouse uma VM grande que pode ter muitos discos anexados, por exemplo, um D14 com 32VHDs. Use espaços de armazenamento toobuild um ambiente flexível onde você pode criar compartilhamentos são usados, em seguida, como destinos de backup para servidores diferentes de DBMS hello.

Algumas práticas recomendadas também foram documentadas [aqui](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) . 

#### <a name="performance-considerations-for-backupsrestores"></a>Considerações de desempenho para backups/restaurações
Como em implantações bare-metal, o desempenho de backup/restauração é dependente de quantos volumes podem ser lidas em paralelo e taxa de transferência que Olá desses volumes pode ser. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com apenas os segmentos de CPU de tooeight. Portanto, é possível supor que:

* Olá menos Olá número de discos usada toostore arquivos de dados Olá, Olá Olá menor taxa de transferência geral na leitura.
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup.
* Olá menos destinos (BLOBs, VHDs ou discos) toowrite Olá backup, Olá menos throughput de saudação.
* Olá Olá menor tamanho da VM, Olá menor Olá taxa de transferência cota de armazenamento de gravação e leitura do armazenamento do Azure. Independente de se os backups de saudação são armazenados diretamente no Blob do Azure ou se eles são armazenados em VHDs novamente são armazenados em Blobs do Azure.

Ao usar um armazenamento de BLOBs do Microsoft Azure como destino de backup Olá nas versões mais recentes, você está restrito toodesignating apenas uma URL de destino para cada backup específico.

Mas, ao usar o hello 'Backup do Microsoft SQL Server tooMicrosoft ferramenta do Azure' nas versões mais antigas, você pode definir mais de um destino de arquivo. Com mais de um destino, Olá backup pode ser dimensionado e hello taxa de transferência de backup Olá for maior. Isso resultaria em vários arquivos, bem como em Olá conta de armazenamento do Azure. Em nossos testes, usando vários destinos de arquivo definitivamente possível alcançar taxa de transferência hello, que pode ser obtida com extensões de backup Olá implementadas do SQL Server 2012 SP1 CU4 em. Você também não é bloqueadas pelo limite de 1TB hello como backup nativo Olá no Azure.

No entanto, tenha em mente, a taxa de transferência Olá também é dependente de local de saudação do hello conta de armazenamento do Azure é usada para o backup de saudação. Uma ideia pode ser uma conta de armazenamento Olá toolocate em uma região diferente Olá que VMs estão sendo executadas no. Por exemplo poderia executar a configuração da VM Olá na Europa Ocidental, mas colocar Olá conta de armazenamento que você use tooback em backup no Norte da Europa. Que certamente tem um impacto na taxa de transferência de backup do hello e provavelmente não toogenerate uma produtividade de 150MB/s pareça toobe possível, em casos onde o armazenamento de destino hello e Olá VMs estão em execução no hello mesmo datacenter regional.

#### <a name="managing-backup-blobs"></a>Gerenciando blobs de Backup
Há uma necessidade toomanage Olá de backups por conta própria. Como expectativa Olá que muitos blobs são criados com a execução de backups de log de transações frequentes, administração desses blobs pode facilmente sobrecarregar Olá portal do Azure. Portanto, é recomendável tooleverage um Gerenciador de armazenamento do Azure. Há vários bons gerenciadores disponíveis, que podem ajudar a toomanage uma conta de armazenamento do Azure

* Microsoft Visual Studio com o SDK do Azure instalado (<https://azure.microsoft.com/downloads/>)
* Gerenciador de Armazenamento do Microsoft Azure (<https://azure.microsoft.com/downloads/>)
* Ferramentas de terceiros

Para obter uma discussão mais completa de Backup e SAP no Azure, consulte muito[Olá SAP Backup guia](sap-hana-backup-guide.md) para obter mais informações.

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Usando uma imagem do SQL Server fora do hello Microsoft Azure Marketplace
A Microsoft oferece VMs em hello Azure Marketplace, que já contêm versões do SQL Server. Para os clientes da SAP que necessitam de licenças para o SQL Server e Windows, isso pode ser uma necessidade de Olá oportunidade toobasically cobertura de licenças por ativar ou desativar VMs com o SQL Server já instalado. Em ordem toouse essas imagens para SAP, Olá considerações a seguir necessário toobe feita:

* versões de avaliação não SQL Server Olá acarretam custos mais elevados de apenas um 'Somente do Windows' VM implantadas do Azure Marketplace. Consulte os preços de toocompare esses artigos: <https://azure.microsoft.com/pricing/details/virtual-machines/windows/> e <https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-enterprise/>. 
* Você pode usar apenas versões do SQL Server que têm suporte da SAP, como o SQL Server 2012.
* agrupamento de Olá Olá instância do SQL Server, que é instalado em máquinas virtuais de saudação oferecidos em hello Azure Marketplace não é agrupamento Olá SAP NetWeaver requer Olá toorun de instância de SQL Server. Você pode alterar o agrupamento de saudação embora com instruções Olá Olá seção a seguir.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Olá alterando o agrupamento do SQL Server de uma VM do Microsoft Windows/SQL Server
Como imagens do SQL Server de saudação em hello Azure Marketplace não estão configuradas agrupamento de saudação toouse, que é exigido pelos aplicativos do SAP NetWeaver, ele precisa toobe alterado imediatamente após a implantação de saudação. Para o SQL Server 2012, isso pode ser feito com hello seguintes etapas assim hello VM foi implantada e um administrador é capaz de toolog em Olá implantado VM:

* Abra uma janela de comando do Windows ‘como administrador’.
* Altere Olá diretório tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Executar o comando Olá: Setup.exe /QUIET /ACTION = REBUILDDATABASE /INSTANCENAME = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`> /SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> é a conta de saudação, que foi definida como conta de administrador Olá ao implantar hello VM para Olá primeira vez por meio da Galeria de saudação.

processo de saudação só deve levar alguns minutos. Em ordem toomake-se de que se Olá etapa terminou com o resultado correto hello, execute Olá etapas a seguir:

* Abra o SQL Server Management Studio.
* Abra uma Janela de Consulta.
* Execute Olá comando sp_helpsort no banco de dados mestre do SQL Server hello.

resultado de saudação desejado deve parecer com:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Se esse não é o resultado de Olá, INTERROMPER a implantação do SAP e investigue por que o comando de instalação Olá não funcionou conforme o esperado. Implantação de aplicativos do SAP NetWeaver na instância do SQL Server com diferentes páginas de código do SQL Server de Olá um mencionado acima é **não** com suporte.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Alta disponibilidade do SQL Server para SAP no Azure
Como mencionado anteriormente neste documento, não há nenhum armazenamento de toocreate compartilhado possibilidade, que é necessário para uso de saudação da funcionalidade de alta disponibilidade do hello mais antiga do SQL Server. Essa funcionalidade instalaria duas ou mais instâncias do SQL Server em um servidor de Failover de Cluster WSFC (Windows) usando um disco compartilhado para bancos de dados de usuário de saudação (e, eventualmente, tempdb). Esse é o método de alta disponibilidade padrão do hello muito tempo, que também é suportado pelo SAP. Como o Azure não dá suporte ao armazenamento compartilhado, as configurações de alta disponibilidade do SQL Server com uma configuração de cluster de disco compartilhado não podem ser realizadas. No entanto, muitos outros métodos de alta disponibilidade ainda são possíveis e são descritos nas seções a seguir de saudação.

#### <a name="sql-server-log-shipping"></a>Envio de logs do SQL Server
Um dos métodos de saudação de alta disponibilidade (HA) é o envio de logs do SQL Server. Se VMs Olá participando da configuração de HA Olá tem resolução de nomes funcional, não há nenhum problema e instalação Olá no Azure não é diferente de qualquer configuração que é feita no local. Não é recomendável toorely apenas a resolução de IP. Com relação toosetting o envio de logs e princípios de saudação em torno de envio de logs, consulte esta documentação:

<https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server>

Em ordem tooreally alcançar a alta disponibilidade, é necessário toodeploy Olá VMs, que estão dentro de tal um toobe de configuração de envio de logs em Olá mesmo conjunto de disponibilidade do Azure.

#### <a name="database-mirroring"></a>Espelhamento de banco de dados
Espelhamento de banco de dados com suporte do SAP (consulte a nota SAP [965908]) se baseia na definição de um parceiro de failover em Olá cadeia de caracteres de conexão SAP. Para casos de saudação entre locais, vamos supor que Olá duas VMs estão em Olá mesmo domínio e o contexto do usuário que Olá Olá SQL Server duas instâncias estiverem sendo executadas em um usuário de domínio e tem privilégios suficientes em instâncias do SQL Server Olá dois envolvidas. Portanto, a instalação de saudação do espelhamento de banco de dados no Azure não diferem entre uma configuração da instalação típica de local.

Como de implantações de nuvem, o método mais fácil de saudação é toohave outro domínio de instalação no Azure toohave essas VMs de DBMS (e VMs do SAP idealmente dedicadas) dentro de um domínio.

Se um domínio não for possível, um também pode usar certificados para o banco de dados de saudação pontos de extremidade de espelhamento, conforme descrito aqui: <https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql>

Um tutorial tooset o espelhamento de banco de dados no Azure pode ser encontrada aqui: <https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server> 

#### <a name="sql-server-always-on"></a>SQL Server Always On
Como sempre no suporte para o local do SAP (consulte a nota SAP [1772688]), é usado em combinação com o SAP no Azure de toobe com suporte. fato Olá que não é capaz de toocreate compartilhado discos no Azure não significa que não seja possível criar uma configuração sempre em Windows Server Failover Cluster (WSFC) entre VMs diferentes. Isso significa apenas que você não tem Olá possibilidade toouse um disco compartilhado como um quorum na configuração de cluster de saudação. Portanto, você pode criar uma configuração sempre WSFC no Azure e simplesmente não selecionar tipo de quorum Olá que utiliza o disco compartilhado. Olá ambiente Azure essas VMs são implantadas deve resolver Olá VMs pelo nome e Olá VMs deve estar na Olá mesmo domínio. Isso é verdadeiro para implantações somente do Azure e entre instalações. Há algumas considerações especiais para implantar Olá ouvinte de grupo de disponibilidade do SQL Server (não toobe confundido com hello conjunto de disponibilidade do Azure) desde que o Azure não permite neste momento toosimply criar um objeto AD/DNS como é possível no local. Portanto, algumas etapas de instalação diferentes estão tooovercome necessário Olá comportamento específico do Azure.

Algumas considerações sobre o uso de um ouvinte de grupo de disponibilidade são:

* Usar um ouvinte de grupo de disponibilidade só é possível com o Windows Server 2012 ou superior como o sistema operacional convidado da VM de saudação. Para o Windows Server 2012, você precisa toomake-se de que este patch é aplicado: <https://support.microsoft.com/kb/2854082> 
* Para Windows Server 2008 R2 esse patch não existe e AlwaysOn precisaria toobe usado em Olá mesma maneira que o espelhamento de banco de dados, especificando um parceiro de failover na cadeia de caracteres de conexões de saudação (por meio Olá SAP default.pfl parâmetro dbs/mss/server – consulte a nota SAP [965908]).
* Quando usar um ouvinte do grupo de disponibilidade, Olá VMs de banco de dados precisar toobe conectado tooa dedicado balanceador de carga. A resolução de nome em implantações somente em nuvem seja exigiria todas as VMs de um SAP sistema (servidores de aplicativos, servidor DBMS e servidor (A) SCS) estão em Olá mesma rede virtual ou exigiria de uma manutenção de Olá de camada de aplicativo SAP do arquivo etc\host Olá nomes de VM ordem tooget Olá de saudação VMs do SQL Server resolvidos. Em ordem tooavoid de que o Azure atribua novos endereços IP nos casos em que ambas as VMs são desligadas acidentalmente, é necessário atribuir endereços IP estáticos interfaces de rede toohello dessas VMs Olá sempre na configuração (definindo um endereço IP estático é descrito em [isso] [ virtual-networks-reserved-private-ip] artigo)

[comment]: <> (Blogs antigos)
[comment]: <> (<https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, <https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>) 
* Há etapas especiais necessárias ao compilar a configuração do cluster WSFC Olá onde cluster Olá precisa de um endereço IP especial atribuído, porque o Azure com sua funcionalidade atual atribuiria nome do cluster Olá Olá mesmo endereço IP como cluster de saudação do nó de saudação é criado no. Isso significa que uma etapa manual deve ser executada tooassign um cluster de toohello de endereço IP diferente.
* Olá ouvinte do grupo de disponibilidade será toobe criado no Azure com pontos de extremidade de TCP/IP, que são atribuídos toohello VMs em execução réplicas primárias e secundárias de Olá Olá do grupo de disponibilidade.
* Pode haver uma necessidade toosecure esses pontos de extremidade com ACLs.

[comment]: <> (Blog antigo TODO)
[comment]: <> (Olá etapas detalhadas e das necessidades da instalação de uma configuração AlwaysOn no Azure são uma noção melhor acompanhará Olá tutorial disponíveis [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Pré-configurado AlwaysOn instalação via Olá Galeria do Azure < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (A criação de um Ouvinte do Grupo de Disponibilidade é mais bem descrita [neste][virtual-machines-windows-classic-ps-sql-int-listener] tutorial)
[comment]: <> (A proteção dos pontos de extremidade da rede com ACLs é explicada aqui:)
[comment]: <> (*    <https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx> )
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>) 

É possível toodeploy um SQL Server sempre no grupo de disponibilidade em diferentes regiões do Azure também. Essa funcionalidade aproveita a conectividade de saudação do Azure VNet para Vnet ([mais detalhes][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Blog antigo TODO)
[comment]: <> (instalação de saudação de grupos de disponibilidade do AlwaysOn do SQL Server nesse cenário é descrita aqui: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.) 

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Resumo da alta disponibilidade do SQL Server no Azure
Considerando que o armazenamento do Azure é proteger o conteúdo de saudação do fato de saudação, há uma menor tooinsist motivo em uma imagem de espera ativa. Isso significa que seu cenário de alta disponibilidade precisa tooonly proteger a saudação casos a seguir:

* Indisponibilidade de saudação VM como um todo devido toomaintenance no cluster de servidor de saudação no Azure ou outros motivos
* Problemas de software na instância do SQL Server Olá
* Proteção contra erros manuais em que os dados são excluídos e a recuperação pontual é necessária

Examinando as tecnologias correspondentes, é possível argumentar que os dois primeiros casos de saudação podem ser cobertos por espelhamento de banco de dados ou sempre em enquanto o terceiro caso de Olá só pode ser abrangido pelo envio de logs.

Você precisa toobalance hello mais complexidade da configuração do AlwaysOn, tooDatabase em comparação com o espelhamento, com as vantagens de saudação do AlwaysOn. É possível listar essas vantagens como:

* Replicas secundárias legíveis.
* Backups de réplicas secundárias.
* Melhor escalabilidade.
* Mais de uma réplica secundária.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Resumo do SQL Server para SAP no Azure geral
Há muitas recomendações neste guia e recomendamos que você o leia mais de uma vez antes de planejar sua implantação do Azure. Em geral, porém, não Olá de toofollow se superior DBMS gerais dez em pontos específicos do Azure:

[comment]: <> (Taxa de transferência superior a 2.3 do que o que? De um VHD?)
1. Use a última versão DBMS hello, como SQL Server 2014, que tem hello mais vantagens no Azure. Para SQL Server, esse é o SQL Server 2012 SP1 CU4, que incluiria o recurso de saudação de backup no armazenamento do Azure. No entanto, em conjunto com o SAP, recomendamos pelo menos atualização Cumulativa mais recente do SQL Server 2014 SP1 CU1 ou SQL Server 2012 SP2 e hello.
2. Planeje cuidadosamente seu cenário de sistema SAP no layout de arquivo de dados do Azure toobalance hello e restrições do Azure:
   * Não tem muitos discos, mas tem suficiente tooensure pode alcançar seus IOPS necessários.
   * Se você não usar Managed Disks, lembre-se de que IOPS também estão limitados pela Conta de Armazenamento do Azure e que as Contas de Armazenamento são limitadas em cada assinatura do Azure ([mais detalhes][azure-subscription-service-limits]). 
   * Só distribua entre discos, se você precisar tooachieve uma maior taxa de transferência.
3. Nunca instale software nem coloque arquivos que exigem persistência Olá unidade D:\, conforme é não é permanente e tudo nessa unidade é perdido na reinicialização do Windows.
4. Não use cache de disco para o Armazenamento Standard do Azure.
5. Não use contas de armazenamento com replicação geográfica do Azure.  Use Localmente Redundante para cargas de trabalho do DBMS.
6. Use o HA/DR solução tooreplicate banco de dados seu fornecedor do DBMS.
7. Sempre use a resolução de nome, não confie em endereços IP.
8. Use hello mais alta compactação banco de dados possível. Para o SQL Server, essa é a compactação de página.
9. Tenha cuidado ao usar imagens do SQL Server do hello Azure Marketplace. Se você usar saudação de um SQL Server, você deve alterar o agrupamento de instância de saudação antes de instalar qualquer sistema SAP NetWeaver.
10. Instalar e configurar Olá monitoramento de Host do SAP para o Azure conforme descrito em [guia de implantação][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Especificações tooSAP ASE no Windows
Começando com o Microsoft Azure, você pode migrar facilmente sua tooAzure de aplicativos SAP ASE existente máquinas virtuais. SAP ASE em uma máquina Virtual permite que você tooreduce Olá custo total de propriedade de implantação, gerenciamento e manutenção de aplicativos de amplitude empresarial migrando facilmente esses tooMicrosoft de aplicativos do Azure. Com o SAP ASE em uma máquina Virtual do Azure, administradores e desenvolvedores ainda podem usar Olá mesmas ferramentas de desenvolvimento e administração que estão disponíveis no local.

Há um SLA para Olá máquinas virtuais do Azure, que podem ser encontradas aqui: <https://azure.microsoft.com/support/legal/sla/virtual-machines>

Estamos confiantes de que o Microsoft Azure máquinas virtuais hospedadas executa muito bem em ofertas de virtualização de nuvem pública de tooother de comparação, mas os resultados individuais podem variar. Números de SAPS de saudação certificado pela SAP diferente SKUs de VM é fornecido em uma nota da SAP separado de dimensionamento do SAP [1928533].

Instruções e recomendações do uso de toohello de relação do armazenamento do Azure, implantação de VMs SAP ou monitoramento do SAP aplicam toodeployments do SAP ASE em conjunto com aplicativos SAP, conforme mencionado em toda a saudação quatro primeiros capítulos deste documento.

### <a name="sap-ase-version-support"></a>Suporte de versão do SAP ASE
No momento, a SAP dá suporte ao SAP ASE versão 16.0 para uso com produtos SAP Business Suite. Todas as atualizações para o servidor SAP ASE ou toobe de drivers JDBC e ODBC usado com produtos são fornecidos apenas por meio do SAP Business Suite Olá SAP Service Marketplace em: <https://support.sap.com/swdc>.

Para instalações locais, não baixe atualizações para o servidor de SAP ASE hello, ou hello JDBC e drivers ODBC diretamente do Sybase sites. Para obter informações detalhadas sobre os patches, que são suportados para uso com o SAP Business Suite produtos locais e em máquinas virtuais Azure consulte Olá SAP observações a seguir:

* [1590719]
* [1973241]

Informações gerais sobre como executar o SAP Business Suite em SAP ASE podem ser encontradas no hello [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Diretrizes de configuração do SAP ASE para instalações do SAP ASE relacionadas ao SAP em VMs do Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Estrutura de saudação SAP ASE implantação
Conforme a descrição geral do hello, SAP ASE executáveis devem ser localizados ou instalados na unidade de sistema de saudação do disco do sistema operacional da VM hello (unidade c:\). Normalmente, a maioria das Olá SAP ASE ferramentas de sistema e bancos de dados não é realmente aproveitada rígido por carga de trabalho do SAP NetWeaver. Olá, portanto, o sistema e bancos de dados de ferramentas (mestre, modelo, saptools, sybmgmtdb, sybsystemdb) podem permanecer na unidade C:\ Olá também. 

Uma exceção poderia ser o banco de dados temporário Olá contendo todas as tabelas de trabalho e tabelas temporárias criadas pelo SAP ASE, que, no caso de algumas SAP ERP e todas as cargas de trabalho do BW, pode exigir maior volume de dados ou volume de operações de e/s, que não cabe na Olá original Disco do sistema operacional da VM (unidade c:\).

Dependendo da saudação versão SAPInst/SWPM usado tooinstall sistema de hello, Olá pode conter:

* Um único tempdb do SAP ASE, que é criado durante a instalação do SAP ASE
* Um tempdb SAP ASE criado pela instalação SAP ASE e um saptempdb adicional criados pelo Olá rotina de instalação do SAP
* Um tempdb SAP ASE criado pela instalação SAP ASE e um tempdb adicionais que tenha sido criado manualmente (por exemplo, após a nota SAP [1752266]) toomeet requisitos de tempdb específico de ERP/BW

No caso de ERP específica ou todas as cargas de trabalho do BW, faz sentido, em relação tooperformance, tempdb dispositivos Olá tookeep Olá adicionalmente criado tempdb (pelo SWPM ou manualmente) em uma unidade diferente C:\. Não se existir nenhum tempdb adicionais, é recomendável toocreate um (nota da SAP [1752266]).

Para tal Olá sistemas etapas a seguir devem ser executadas para Olá adicionalmente criado tempdb:

* Mover Olá primeiro tempdb dispositivos toohello primeiro dispositivo de banco de dados do SAP Olá
* Adicionar tempdb dispositivos tooeach de saudação VHDs contendo um dispositivo de banco de dados do SAP Olá

Este tooeither do configuração habilita tempdb consumir mais espaço do que a unidade do sistema Olá é capaz de tooprovide. Como uma referência é possível verificar tamanhos de dispositivo Olá tempdb em sistemas existentes, que são executados localmente. Ou, tal configuração habilitaria números de IOPS em relação a tempdb, que não pode ser fornecida com a unidade do sistema hello. Novamente sistemas que estejam em execução no local podem ser usados toomonitor e/s de carga de trabalho em relação a tempdb.

Nunca coloque todos os dispositivos SAP ASE em Olá unidade D:\ da VM de saudação. Isso também se aplica toohello tempdb, mesmo se objetos Olá mantidos em tempdb Olá só são temporários.

#### <a name="impact-of-database-compression"></a>Impacto da compactação do banco de dados
Em configurações onde largura de banda de e/s pode se tornar um fator limitante, todas as medidas, que reduzem o IOPS podem ajudar a carga de trabalho do hello toostretch pode ser executada em um cenário de IaaS como o Azure. Portanto, é altamente recomendável toomake-se de que a compactação de SAP ASE é usada antes de carregar um tooAzure de banco de dados do SAP existente.

compactação de tooperform de recomendação de saudação antes de carregar tooAzure se já não está implementado é indicada por vários motivos:

* quantidade de saudação de dados carregado de toobe tooAzure é inferior
* duração de Olá da execução de compactação de saudação é menor, supondo que você pode usar hardware mais poderoso com mais CPUs ou maior largura de banda de e/s ou menor latência de e/s no local
* Os tamanhos menores de banco de dados podem causar custos tooless para alocação de disco

A compactação de LOB e dados funciona em uma VM hospedada em máquinas virtuais do Azure como o faz localmente. Para obter mais detalhes sobre como toocheck se compactação já está em uso em um banco de dados do SAP ASE existente, verifique a nota SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Usando as instâncias de banco de dados de toomonitor DBACockpit
Para sistemas SAP, que estão usando o SAP ASE como plataforma de banco de dados, Olá DBACockpit é acessível como janelas de navegador incorporado na transação DBACockpit ou Webdynpro. Porém Olá funcionalidade completa para o monitoramento e administração banco de dados de saudação está disponível em implementação Webdynpro Olá Olá DBACockpit somente.

Como com o local sistemas que várias etapas são necessárias tooenable usada pela implementação de Webdynpro de saudação do hello DBACockpit toda a funcionalidade do SAP NetWeaver. Siga a nota SAP [1245200] tooenable Olá uso de webdynpros e gerar Olá necessárias às. Ao seguir as instruções Olá Olá acima anotações, também configurar Olá Gerenciador de comunicação da Internet (icm) junto com hello toobe de portas usada para conexões http e https. configuração padrão de saudação para http tem esta aparência:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

e links Olá gerado na transação DBACockpit terá aparência semelhante toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

Dependendo de se e como hospedagem Máquina Virtual do Azure Olá Olá sistema SAP é conectado por meio do site a site, vários locais ou rota expressa (implantação entre locais), você precisa toomake-se de que ICM está usando um nome de host totalmente qualificado que pode ser resolvido Olá computador onde você está tentando tooopen Olá DBACockpit do. Consulte a nota SAP [773830] toounderstand como ICM determina Olá nome de host totalmente qualificado dependendo de parâmetros de perfil e o parâmetro de conjunto icm/host_name_full explicitamente se necessário.

Se você implantou Olá VM em um cenário somente na nuvem sem conectividade entre locais entre local e o Azure, você precisa toodefine um endereço IP público e um domainlabel. formato de saudação do nome DNS público de saudação do hello VM parecido com:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

Mais detalhes relacionados ao nome DNS de toohello pode ser encontrado [aqui][virtual-machines-azurerm-versus-azuresm].

Definindo Olá SAP perfil parâmetro icm/host_name_full toohello nome DNS do link de saudação do hello VM do Azure pode parecer semelhante a:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

Nesse caso você precisa toomake-se de:

* Adicionar regras de entrada toohello grupo de segurança de rede no portal do Azure para toocommunicate de portas usadas Olá TCP/IP com ICM de saudação
* Adicionar configuração de Firewall do Windows toohello as regras de entrada para toocommunicate de portas usadas Olá TCP/IP com hello ICM

Para importar um automatizada de todas as correções disponíveis, é recomendável tooperiodically aplicar Olá correção coleção SAP Observação tooyour aplicável SAP versão:

* [1558958]
* [1619967]
* [1882376]

Mais informações sobre Cockpit DBA para SAP ASE podem ser encontradas no hello SAP observações a seguir:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considerações sobre backup/recuperação para o SAP ASE
Ao implantar o SAP ASE no Azure, sua metodologia de backup deve ser examinada. Mesmo se o sistema de saudação não é um sistema de produção, banco de dados do SAP Olá hospedado pelo SAP ASE deve ser feito periodicamente. Como o armazenamento do Azure mantém três imagens, um backup agora é menos importante na relação toocompensating uma falha de armazenamento. Olá principal motivo para manter um plano de backup e restauração correto é mais que você pode compensar erros lógicos/manuais fornecendo recursos de recuperação pontual. Meta de saudação é tooeither use backups toorestore Olá banco de dados tooa determinado ponto no tempo ou toouse backups Olá no Azure tooseed outro sistema copiando o banco de dados existente do hello. Por exemplo, você pode transferir de uma configuração do sistema de 3 camadas da camada 2 SAP configuração tooa de saudação mesmo sistema restaurando um backup.

Fazendo backup e restaurando um banco de dados no Azure funciona Olá mesma maneira como faz no local. Consulte as observações do SAP:

* [1588316]
* [1585981]

para obter detalhes sobre como criar configurações de despejo e agendar backups. Dependendo de sua estratégia e necessidades, você pode configurar o banco de dados e log toodisk em um dos discos existentes Olá de despejos de memória ou adicionar um disco adicional para o backup de saudação. tooreduce o risco de saudação de perda de dados no caso de erro, é recomendável toouse um disco onde não há nenhum dispositivo de banco de dados está localizado.

Além da compactação do LOB e dados, o SAP ASE também oferece a compactação de backup. descarrega toooccupy menos espaço de log e banco de dados de saudação é recomendável toouse compactação de backup. Para obter mais informações, consulte a Nota SAP [1588316]. A compactação de backup de saudação é também tooreduce crucial Olá toobe dados transferido se planejar backups toodownload ou VHDs contendo backup despejos de saudação local tooon de máquina Virtual do Azure.

Não use a unidade D:\ como destino de despejo de log ou banco de dados.

#### <a name="performance-considerations-for-backupsrestores"></a>Considerações de desempenho para backups/restaurações
Como em implantações bare-metal, o desempenho de backup/restauração é dependente de quantos volumes podem ser lidas em paralelo e taxa de transferência que Olá desses volumes pode ser. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com apenas os segmentos de CPU de tooeight. Portanto, é possível supor que:

* Hello menos Olá número de discos usados toostore Olá dispositivos de banco de dados, Olá Olá menor geral taxa de transferência de leitura
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup
* Olá menos destinos (diretórios de distribuição, discos) toowrite Olá backup, Olá menos throughput de saudação

número de saudação do tooincrease de destinos toowrite toothere são duas opções, que podem ser usado/combinados dependendo de suas necessidades:

* A distribuição de volume de destino de backup Olá através de vários discos montados na taxa de transferência de ordem tooimprove Olá IOPS nesse volume distribuído
* Criar uma configuração de despejo no nível do SAP ASE, que usa mais de um destino diretório toowrite Olá despejo de memória para

A divisão de um volume em vários discos montados foi discutida anteriormente nesse guia. Para obter mais informações sobre o uso de vários diretórios na configuração de despejo do SAP ASE hello, consulte a documentação do toohello em sp_config_dump do procedimento armazenado, que é usado toocreate Olá despejo configuração em Olá [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Recuperação de desastre com VMs do Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replicação de dados com o Servidor de Replicação do SAP Sybase
Com hello o SAP Sybase servidor SRS (replicação) SAP ASE fornece um local distante solução em espera passiva tootransfer banco de dados transações tooa assincronamente. 

instalação de saudação e operação do SRS funciona bem funcionalmente em uma VM hospedada nos serviços de máquina Virtual do Azure como faz no local.

O ASE HADR por meio do servidor de replicação do SAP é planejado com uma versão futura. Ele será testado com e liberado para plataformas Microsoft Azure assim que estiver disponível.

## <a name="specifics-toosap-ase-on-linux"></a>Especificações tooSAP ASE no Linux
Começando com o Microsoft Azure, você pode migrar facilmente sua tooAzure de aplicativos SAP ASE existente máquinas virtuais. SAP ASE em uma máquina Virtual permite que você tooreduce Olá custo total de propriedade de implantação, gerenciamento e manutenção de aplicativos de amplitude empresarial migrando facilmente esses tooMicrosoft de aplicativos do Azure. Com o SAP ASE em uma máquina Virtual do Azure, administradores e desenvolvedores ainda podem usar Olá mesmas ferramentas de desenvolvimento e administração que estão disponíveis no local.

Para implantar máquinas virtuais do Azure é importante tooknow Olá SLAs oficiais, que podem ser encontrados aqui: <https://azure.microsoft.com/support/legal/sla>

As informações de dimensionamento do SAP e uma lista dos SKUs de VM certificados do SAP são fornecidas na Nota SAP [1928533]. Documentos adicionais sobre dimensionamento de SAP para máquinas virtuais do Azure podem ser encontrados aqui <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> e aqui <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Instruções e recomendações do uso de toohello de relação do armazenamento do Azure, implantação de VMs SAP ou monitoramento do SAP aplicam toodeployments do SAP ASE em conjunto com aplicativos SAP, conforme mencionado em toda a saudação quatro primeiros capítulos deste documento.

Olá seguintes duas Observações sobre o SAP incluem informações gerais sobre ASE em Linux e ASE em Olá nuvem:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Suporte de versão do SAP ASE
No momento, a SAP dá suporte ao SAP ASE versão 16.0 para uso com produtos SAP Business Suite. Todas as atualizações para o servidor SAP ASE ou toobe de drivers JDBC e ODBC usado com produtos são fornecidos apenas por meio do SAP Business Suite Olá SAP Service Marketplace em: <https://support.sap.com/swdc>.

Para instalações locais, não baixe atualizações para o servidor de SAP ASE hello, ou hello JDBC e drivers ODBC diretamente do Sybase sites. Para obter informações detalhadas sobre os patches, que são suportados para uso com o SAP Business Suite produtos locais e em máquinas virtuais Azure consulte Olá SAP observações a seguir:

* [1590719]
* [1973241]

Informações gerais sobre como executar o SAP Business Suite em SAP ASE podem ser encontradas no hello [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Diretrizes de configuração do SAP ASE para instalações do SAP ASE relacionadas ao SAP em VMs do Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Estrutura de saudação SAP ASE implantação
Conforme a descrição geral do hello, SAP ASE executáveis devem ser localizados ou instalado no sistema de arquivos de raiz de saudação do hello VM (/sybase). Normalmente, a maioria das Olá SAP ASE ferramentas de sistema e bancos de dados não é realmente aproveitada rígido por carga de trabalho do SAP NetWeaver. Olá, portanto, o sistema e bancos de dados de ferramentas (mestre, modelo, saptools, sybmgmtdb, sybsystemdb) podem permanecer no sistema de arquivos de raiz Olá também. 

Uma exceção poderia ser o banco de dados temporário Olá contendo todas as tabelas de trabalho e tabelas temporárias criadas pelo SAP ASE, que pode exigir maior volume de dados ou operações de e/s, volume que não cabe na Olá original no caso de algumas SAP ERP e todas as cargas de trabalho do BW Disco do sistema operacional da VM.

Dependendo da saudação versão SAPInst/SWPM usado tooinstall sistema de hello, Olá pode conter:

* Um único tempdb do SAP ASE, que é criado durante a instalação do SAP ASE
* Um tempdb SAP ASE criado pela instalação SAP ASE e um saptempdb adicional criados pelo Olá rotina de instalação do SAP
* Um tempdb SAP ASE criado pela instalação SAP ASE e um tempdb adicionais que tenha sido criado manualmente (por exemplo, após a nota SAP [1752266]) toomeet requisitos de tempdb específico de ERP/BW

No caso de ERP específica ou todas as cargas de trabalho do BW, faz sentido, em relação tooperformance, tempdb dispositivos Olá tookeep tempdb Olá adicionalmente criado (por SWPM ou manualmente) em um sistema de arquivo separado, que pode ser representado por um disco de dados do Azure único ou um RAID de Linux inclusão de vários discos de dados do Azure. Não se existir nenhum tempdb adicionais, é recomendável toocreate um (nota da SAP [1752266]).

Para tal Olá sistemas etapas a seguir devem ser executadas para Olá adicionalmente criado tempdb:

* Mover Olá primeiro tempdb diretório toohello primeiro sistema de arquivos do banco de dados do SAP Olá
* Adicionar tempdb diretórios tooeach de discos de saudação que contém um sistema de arquivos do banco de dados do SAP Olá

Este tooeither do configuração habilita tempdb consumir mais espaço do que a unidade do sistema Olá é capaz de tooprovide. Como uma referência é possível verificar tamanhos de diretório de tempdb Olá em sistemas existentes, que são executados no local. Ou, tal configuração habilitaria números de IOPS em relação a tempdb, que não pode ser fornecida com a unidade do sistema hello. Novamente sistemas que estejam em execução no local podem ser usados toomonitor e/s de carga de trabalho em relação a tempdb.

Nunca coloque quaisquer diretórios SAP ASE em /mnt ou /mnt/resource de saudação VM. Isso também se aplica toohello tempdb, mesmo se os objetos de Olá mantidos em tempdb Olá somente são temporários porque /mnt ou /mnt/resource é um VM do Azure temp espaço padrão, que não é persistente. Mais detalhes sobre Olá espaço temporário em VM do Azure podem ser encontrados em [neste artigo][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Impacto da compactação do banco de dados
Em configurações onde largura de banda de e/s pode se tornar um fator limitante, todas as medidas, que reduzem o IOPS podem ajudar a carga de trabalho do hello toostretch pode ser executada em um cenário de IaaS como o Azure. Portanto, é altamente recomendável toomake-se de que a compactação de SAP ASE é usada antes de carregar um tooAzure de banco de dados do SAP existente.

compactação de tooperform de recomendação de saudação antes de carregar tooAzure se já não está implementado é indicada por vários motivos:

* quantidade de saudação de dados carregado de toobe tooAzure é inferior
* duração de Olá da execução de compactação de saudação é menor, supondo que você pode usar hardware mais poderoso com mais CPUs ou maior largura de banda de e/s ou menor latência de e/s no local
* Os tamanhos menores de banco de dados podem causar custos tooless para alocação de disco

A compactação de LOB e dados funciona em uma VM hospedada em máquinas virtuais do Azure como o faz localmente. Para obter mais detalhes sobre como toocheck se compactação já está em uso em um banco de dados do SAP ASE existente, verifique a nota SAP [1750510]. Para obter informações adicionais sobre a compactação de banco de dados, consulte a Nota SAP [2121797].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Usando as instâncias de banco de dados de toomonitor DBACockpit
Para sistemas SAP, que estão usando o SAP ASE como plataforma de banco de dados, Olá DBACockpit é acessível como janelas de navegador incorporado na transação DBACockpit ou Webdynpro. Porém Olá funcionalidade completa para o monitoramento e administração banco de dados de saudação está disponível em implementação Webdynpro Olá Olá DBACockpit somente.

Como com o local sistemas que várias etapas são necessárias tooenable usada pela implementação de Webdynpro de saudação do hello DBACockpit toda a funcionalidade do SAP NetWeaver. Siga a nota SAP [1245200] tooenable Olá uso de webdynpros e gerar Olá necessárias às. Ao seguir as instruções Olá Olá acima anotações, também configurar Olá Gerenciador de comunicação da Internet (icm) junto com hello toobe de portas usada para conexões http e https. configuração padrão de saudação para http tem esta aparência:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

e links Olá gerado na transação DBACockpit terá aparência semelhante toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

Dependendo de se e como hospedagem Máquina Virtual do Azure Olá Olá sistema SAP é conectado por meio do site a site, vários locais ou rota expressa (implantação entre locais), você precisa toomake-se de que ICM está usando um nome de host totalmente qualificado que pode ser resolvido Olá computador onde você está tentando tooopen Olá DBACockpit do. Consulte a nota SAP [773830] toounderstand como ICM determina Olá nome de host totalmente qualificado dependendo de parâmetros de perfil e o parâmetro de conjunto icm/host_name_full explicitamente se necessário.

Se você implantou Olá VM em um cenário somente na nuvem sem conectividade entre locais entre local e o Azure, você precisa toodefine um endereço IP público e um domainlabel. formato de saudação do nome DNS público de saudação do hello VM parecido com:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

Mais detalhes relacionados ao nome DNS de toohello pode ser encontrado [aqui][virtual-machines-azurerm-versus-azuresm].

Definindo Olá SAP perfil parâmetro icm/host_name_full toohello nome DNS do link de saudação do hello VM do Azure pode parecer semelhante a:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

Nesse caso você precisa toomake-se de:

* Adicionar regras de entrada toohello grupo de segurança de rede no portal do Azure para toocommunicate de portas usadas Olá TCP/IP com ICM de saudação
* Adicionar configuração de Firewall do Windows toohello as regras de entrada para toocommunicate de portas usadas Olá TCP/IP com hello ICM

Para importar um automatizada de todas as correções disponíveis, é recomendável tooperiodically aplicar Olá correção coleção SAP Observação tooyour aplicável SAP versão:

* [1558958]
* [1619967]
* [1882376]

Mais informações sobre Cockpit DBA para SAP ASE podem ser encontradas no hello SAP observações a seguir:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Considerações sobre backup/recuperação para o SAP ASE
Ao implantar o SAP ASE no Azure, sua metodologia de backup deve ser examinada. Mesmo se o sistema de saudação não é um sistema de produção, banco de dados do SAP Olá hospedado pelo SAP ASE deve ser feito periodicamente. Como o armazenamento do Azure mantém três imagens, um backup agora é menos importante na relação toocompensating uma falha de armazenamento. Olá principal motivo para manter um plano de backup e restauração correto é mais que você pode compensar erros lógicos/manuais fornecendo recursos de recuperação pontual. Meta de saudação é tooeither use backups toorestore Olá banco de dados tooa determinado ponto no tempo ou toouse backups Olá no Azure tooseed outro sistema copiando o banco de dados existente do hello. Por exemplo, você pode transferir de uma configuração do sistema de 3 camadas da camada 2 SAP configuração tooa de saudação mesmo sistema restaurando um backup.

Fazendo backup e restaurando um banco de dados no Azure funciona Olá mesma maneira como faz no local. Consulte as observações do SAP:

* [1588316]
* [1585981]

para obter detalhes sobre como criar configurações de despejo e agendar backups. Dependendo de sua estratégia e necessidades, você pode configurar o banco de dados e log toodisk em um dos discos existentes Olá de despejos de memória ou adicionar um disco adicional para o backup de saudação. risco de saudação tooreduce de perda de dados no caso de erro é recomendado toouse um disco onde nenhum diretório/arquivo de banco de dados está localizado.

Além da compactação do LOB e dados, o SAP ASE também oferece a compactação de backup. descarrega toooccupy menos espaço de log e banco de dados de saudação é recomendável toouse compactação de backup. Para obter mais informações, consulte a Nota SAP [1588316]. A compactação de backup de saudação é também tooreduce crucial Olá toobe dados transferido se planejar backups toodownload ou VHDs contendo backup despejos de saudação local tooon de máquina Virtual do Azure.

Não use hello Azure VM espaço temporário /mnt ou /mnt/resource como destino de despejo de banco de dados ou log.

#### <a name="performance-considerations-for-backupsrestores"></a>Considerações de desempenho para backups/restaurações
Como em implantações bare-metal, o desempenho de backup/restauração é dependente de quantos volumes podem ser lidas em paralelo e taxa de transferência que Olá desses volumes pode ser. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com apenas os segmentos de CPU de tooeight. Portanto, é possível supor que:

* Hello menos Olá número de discos usados toostore Olá dispositivos de banco de dados, Olá Olá menor geral taxa de transferência de leitura
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup
* Olá menos toowrite de destinos (Linux RAID de software, discos) Olá backup, Olá menos throughput de saudação

número de saudação do tooincrease de destinos toowrite toothere são duas opções, que podem ser usado/combinados dependendo de suas necessidades:

* A distribuição de volume de destino de backup Olá através de vários discos montados na taxa de transferência de ordem tooimprove Olá IOPS nesse volume distribuído
* Criar uma configuração de despejo no nível do SAP ASE, que usa mais de um destino diretório toowrite Olá despejo de memória para

A divisão de um volume em vários discos montados foi discutida anteriormente nesse guia. Para obter mais informações sobre o uso de vários diretórios na configuração de despejo do SAP ASE hello, consulte a documentação do toohello em sp_config_dump do procedimento armazenado, que é usado toocreate Olá despejo configuração em Olá [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Recuperação de desastre com VMs do Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replicação de dados com o Servidor de Replicação do SAP Sybase
Com hello o SAP Sybase servidor SRS (replicação) SAP ASE fornece um local distante solução em espera passiva tootransfer banco de dados transações tooa assincronamente. 

instalação de saudação e operação do SRS funciona bem funcionalmente em uma VM hospedada nos serviços de máquina Virtual do Azure como faz no local.

O ASE HADR por meio do servidor de replicação do SAP NÃO tem suporte neste momento. Pode ser testado com e liberada para plataformas do Microsoft Azure em Olá futuras.

## <a name="specifics-toooracle-database-on-windows"></a>Especificações tooOracle banco de dados no Windows
Software Oracle é compatível com Oracle toorun no Microsoft Windows Hyper-V e o Azure. Para obter detalhes sobre o suporte de saudação geral do Hyper-V do Windows e do Azure, consulte: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

A seguir suporte geral do hello, cenário específico de saudação dos aplicativos SAP aproveitando os bancos de dados Oracle há suporte para também. Detalhes são nomeados nesta parte do documento hello.

### <a name="oracle-version-support"></a>Suporte de versão do Oracle
As versões do Oracle e as versões de SO correspondentes que têm suporte para execução do SAP no Oracle nas Máquinas Virtuais do Azure podem ser encontrados na Nota SAP [2039619].

Informações gerais sobre como executar o SAP Business Suite em Oracle podem ser encontradas em 1DX: <https://www.sap.com/community/topic/oracle.html>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do Oracle para instalações do SAP em VMs do Azure
#### <a name="storage-configuration"></a>Configuração de armazenamento
Há suporte a apenas uma única instância do Oracle usando discos formatados em NTFS. Todos os arquivos de banco de dados devem ser armazenados em Olá com base em VHDs ou discos gerenciados de sistema de arquivos NTFS. Esses discos são montado toohello VM do Azure e são baseados no armazenamento de BLOB de página do Azure (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) ou em discos gerenciado (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Qualquer variante de unidades de rede ou compartilhamentos remotos como serviços de arquivo do Azure:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**NÃO** têm suporte para arquivos de banco de dados Oracle!

Usando discos com base no armazenamento de BLOB de página do Azure ou discos gerenciados, Olá instruções feitas neste documento capítulo [cache para máquinas virtuais e discos de dados] [ dbms-guide-2.1] e [dearmazenamentodoMicrosoftAzure] [ dbms-guide-2.3] aplicar toodeployments com hello banco de dados Oracle.

Conforme explicado anteriormente na parte de geral de saudação do documento hello, existem cotas em produtividade de IOPS para discos do Azure. Olá exata cotas são dependendo do tipo de VM Olá usadas. Uma lista de tipos VM com suas cotas pode ser encontrada [aqui (Linux)][virtual-machines-sizes-linux] e [aqui (Windows)][virtual-machines-sizes-windows].

Olá tooidentify suporte para tipos de VM do Azure, consulte a Observação tooSAP [1928533].

Contanto que a cota de IOPS atual Olá por disco atende aos requisitos de Olá, é possível toostore Olá a todos os arquivos de banco de dados em um único disco montado. 

Se mais IOPS forem necessários, é altamente recomendável toouse Pools de armazenamento de janela (somente disponível no Windows Server 2012 e superior) ou Windows distribuição para o Windows 2008 R2 toocreate um dispositivo lógico grande através de vários discos montados (Consulte também o capítulo [RAID de software] [ dbms-guide-2.2] deste documento). Essa abordagem simplifica a espaço em disco Olá Olá administração toomanage sobrecarga e evita o esforço de saudação toomanually distribuir arquivos em vários discos montados.

#### <a name="backup--restore"></a>Backup/restauração
Para backup / restaurar a funcionalidade, Olá SAP BR * ferramentas para Oracle têm suporte em Olá mesma maneira como no padrão de sistemas operacionais Windows Server e Hyper-V. Também há suporte para o Oracle Recovery Manager (RMAN) para toodisk de backups e restauração do disco.

#### <a name="high-availability"></a>Alta disponibilidade
O Oracle Data Guard tem suporte para fins de recuperação de desastre e alta disponibilidade. É possível encontrar detalhes [nesta][virtual-machines-windows-classic-configure-oracle-data-guard] documentação.

#### <a name="other"></a>outro
Todos os outros tópicos gerais como o monitoramento de conjuntos de disponibilidade do Azure ou SAP aplicam conforme descrito em Olá três primeiros capítulos deste documento para implantações de VMs com hello banco de dados Oracle.

## <a name="specifics-toooracle-database-on-oracle-linux"></a>Especificações tooOracle banco de dados Oracle Linux
Software Oracle é compatível com Oracle toorun no Microsoft Windows Hyper-V e o Azure. Para obter detalhes sobre o suporte de saudação geral do Hyper-V do Windows e do Azure, consulte: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

A seguir suporte geral do hello, cenário específico de saudação dos aplicativos SAP aproveitando os bancos de dados Oracle há suporte para também. Detalhes são nomeados nesta parte do documento hello.

### <a name="oracle-version-support"></a>Suporte de versão do Oracle
As versões do Oracle e as versões de SO correspondentes que têm suporte para execução do SAP no Oracle nas Máquinas Virtuais do Azure podem ser encontrados na Nota SAP [2039619].

Informações gerais sobre como executar o SAP Business Suite em Oracle podem ser encontradas em 1DX: <https://www.sap.com/community/topic/oracle.html>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do Oracle para instalações do SAP em VMs do Azure
#### <a name="storage-configuration"></a>Configuração de armazenamento
Há suporte para uma única instância do Oracle usando discos formatados em ext3, ext4 e xfs. Todos os arquivos de banco de dados devem ser armazenados no sistemas de arquivos baseados em VHDs ou Managed Disks. Esses discos são montado toohello VM do Azure e são baseados no armazenamento de BLOB de página do Azure (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) ou em discos gerenciado (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Qualquer variante de unidades de rede ou compartilhamentos remotos como serviços de arquivo do Azure:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**NÃO** têm suporte para arquivos de banco de dados Oracle!

Usando discos com base no armazenamento de BLOB de página do Azure ou discos gerenciados, Olá instruções feitas neste documento capítulo [cache para máquinas virtuais e discos de dados] [ dbms-guide-2.1] e [dearmazenamentodoMicrosoftAzure] [ dbms-guide-2.3] aplicar toodeployments com hello banco de dados Oracle.

Conforme explicado anteriormente na parte de geral de saudação do documento hello, existem cotas em produtividade de IOPS para discos do Azure. Olá exata cotas são dependendo do tipo de VM Olá usadas. Uma lista de tipos VM com suas cotas pode ser encontrada [aqui (Linux)][virtual-machines-sizes-linux] e [aqui (Windows)][virtual-machines-sizes-windows].

Olá tooidentify suporte para tipos de VM do Azure, consulte a Observação tooSAP [1928533]

Contanto que a cota de IOPS atual Olá por disco atende aos requisitos de Olá, é possível toostore Olá a todos os arquivos de banco de dados em um único disco montado. 

Se mais IOPS forem necessários, é altamente recomendável toouse LVM (Gerenciador de Volume lógico) ou MDADM toocreate um grande volume lógico através de vários discos montados. Veja também o capítulo [RAID de Software][dbms-guide-2.2] deste documento. Essa abordagem simplifica a espaço em disco Olá Olá administração toomanage sobrecarga e evita o esforço de saudação toomanually distribuir arquivos em vários discos montados.

#### <a name="backup--restore"></a>Backup/restauração
Para backup / restaurar a funcionalidade, Olá SAP BR * ferramentas para Oracle têm suporte em Olá mesma maneira como no Hyper-V e bare-metal. Também há suporte para o Oracle Recovery Manager (RMAN) para toodisk de backups e restauração do disco.

#### <a name="high-availability"></a>Alta disponibilidade
O Oracle Data Guard tem suporte para fins de recuperação de desastre e alta disponibilidade. É possível encontrar detalhes [nesta][virtual-machines-windows-classic-configure-oracle-data-guard] documentação.

#### <a name="other"></a>outro
Todos os outros tópicos gerais como o monitoramento de conjuntos de disponibilidade do Azure ou SAP aplicam conforme descrito em Olá três primeiros capítulos deste documento para implantações de VMs com hello banco de dados Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Especificações de saudação banco de dados do SAP MaxDB no Windows
### <a name="sap-maxdb-version-support"></a>Suporte de versão do SAP MaxDB
No momento, o SAP dá suporte ao SAP MaxDB versão 7.9 para o uso com produtos baseados no SAP NetWeaver no Azure. Todas as atualizações para o servidor SAP MaxDB ou toobe de drivers JDBC e ODBC usado com produtos baseados no SAP NetWeaver são fornecidas apenas por meio da saudação SAP Service Marketplace em <https://support.sap.com/swdc>.
Informações gerais sobre como executar o SAP NetWeaver no SAP MaxDB podem ser encontradas em <https://www.sap.com/community/topic/maxdb.html>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Versões do Microsoft Windows e tipos de VM do Azure com suporte para DBMS do SAP MaxDB
versão do Microsoft Windows hello suporte toofind para SAP MaxDB DBMS no Azure, consulte:

* [PAM (Matriz de Disponibilidade de Produto) da SAP][sap-pam]
* Nota SAP [1928533]

É altamente recomendável toouse hello mais recente versão de hello sistema operacional Microsoft Windows, que é o Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Documentação do SAP MaxDB disponível
Você pode encontrar a lista de saudação atualizada da documentação do SAP MaxDB em Olá seguindo a nota SAP [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do SAP MaxDB para instalações do SAP em VMs do Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Configuração de armazenamento
Práticas recomendadas de armazenamento do Azure para SAP MaxDB siga as recomendações gerais Olá mencionadas no capítulo [estrutura de uma implantação do RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Como outros bancos de dados, o SAP MaxDB também tem arquivos de log e de dados. No entanto, na terminologia de SAP MaxDB termo correto Olá é "volume" (não "file"). Por exemplo, há volumes de dados e volumes de log do SAP MaxDB. Não os confunda com volumes de disco do SO. 
> 
> 

Em resumo, você precisa:

* Se você usar contas de armazenamento do Azure, defina a conta de armazenamento do Azure de saudação que mantém Olá SAP MaxDB dados e volumes de log (ou seja, arquivos) muito**armazenamento redundante Local (LRS)** conforme especificado no capítulo [dearmazenamentodoMicrosoftAzure] [dbms-guide-2.3].
* Caminho de e/s de saudação separado para volumes de dados SAP MaxDB (ou seja, arquivos) do caminho de e/s de saudação para volumes do log (ou seja, arquivos). Isso significa que os volumes de dados SAP MaxDB (ou seja, arquivos) têm toobe instalado em uma unidade lógica e volumes de log do SAP MaxDB (ou seja, arquivos) têm toobe instalado em outra unidade lógica.
* Conjunto Olá cache tipo adequado para cada disco, dependendo se você usá-lo para SAP MaxDB dados ou log volumes (ou seja, arquivos), e se você usar padrão do Azure ou armazenamento do Azure Premium, conforme descrito no capítulo [cache para máquinas virtuais e discos de dados][dbms-guide-2.1].
* Desde que a cota de IOPS atual Olá por disco atende aos requisitos de Olá, é possível toostore todos os volumes de dados de saudação em um único disco montado e também armazenar todos os volumes de log do banco de dados em outro disco montado único.
* Se mais IOPS e/ou espaço forem necessário, é altamente recomendável toouse os Pools de armazenamento Microsoft janela (somente disponível no Microsoft Windows Server 2012 e superior) ou o Microsoft Windows distribuição para Microsoft Windows 2008 R2 toocreate um dispositivo lógico grande através de vários discos montados. Veja também o capítulo [RAID de Software][dbms-guide-2.2] deste documento. Essa abordagem simplifica a espaço em disco Olá Olá administração toomanage sobrecarga e evita o esforço de saudação de distribuir manualmente os arquivos em vários discos montados.
* Para mais altos requisitos de IOPS hello, você pode usar o armazenamento do Azure Premium, que está disponível na série DS e as VMs da série GS.

![Configuração de referência da VM IaaS do Azure para DBMS do SAP MaxDB][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Backup e restauração
Ao implantar o SAP MaxDB no Azure, você deve examinar sua metodologia de backup. Mesmo se o sistema de saudação não é um sistema de produção, banco de dados do SAP Olá hospedado pelo SAP MaxDB deve ser feito periodicamente. Como o armazenamento do Azure mantém três imagens, um backup agora é menos importante em termos de proteger seu sistema contra falhas de armazenamento e falhas administrativas ou operacionais mais importantes. Olá principal motivo para manter um backup apropriado e um plano de restauração é para que você pode compensar erros lógicos ou manuais, fornecendo recursos de recuperação point-in-time. Portanto Olá objetivo é tooeither use backups toorestore Olá banco de dados tooa determinados ponto no tempo ou toouse backups Olá no Azure tooseed outro sistema copiando o banco de dados existente do hello. Por exemplo, você pode transferir de uma configuração do sistema de 3 camadas da camada 2 SAP configuração tooa de saudação mesmo sistema restaurando um backup.

Fazendo backup e restaurando um banco de dados do Azure funciona Olá mesma maneira que faz para sistemas locais, então você pode usar o padrão MaxDB de SAP ferramentas, que são descritas em um dos documentos de documentação do SAP MaxDB Olá backup/restauração listado na nota da SAP [767598 ]. 

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Considerações de desempenho para backup e restauração
Como em implantações bare-metal, o desempenho de backup e restauração é dependente de quantos volumes podem ser lidas em paralelo e hello produtividade desses volumes. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com os segmentos de CPU tooeight. Portanto, é possível supor que:

* Olá menor número de saudação de dispositivos de banco de dados os discos usados toostore hello, Olá Olá geral mais baixa taxa de transferência de leitura
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup
* Olá menos destinos (diretórios de distribuição, discos) toowrite Olá backup, throughput menor de Olá Olá

tooincrease Olá inúmeros destinos toowrite para, há duas opções que você pode usar, possivelmente em combinação, dependendo de suas necessidades:

* Dedicando volumes separados para backup
* A distribuição de volume de destino de backup Olá através de vários discos montados na taxa de transferência de ordem tooimprove Olá IOPS nesse volume de discos distribuídos
* Com dispositivos de disco lógico dedicados separados para:
  * Volumes de backup (ou seja, arquivos) do SAP MaxDB
  * Volumes de dados do SAP MaxDB (ou seja, arquivos)
  * Volumes de log do SAP MaxDB (ou seja, arquivos)

A divisão de um volume em vários discos montados foi discutida anteriormente no capítulo [RAID de software][dbms-guide-2.2] deste documento. 

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Outros
Todos os outros tópicos gerais, como monitoramento de conjuntos de disponibilidade do Azure ou SAP também se aplicam a conforme descrito em Olá três primeiros capítulos deste documento para implantações de VMs com o banco de dados do SAP MaxDB hello.
Outras configurações específicas do SAP MaxDB tooAzure transparente VMs e são descritas em diferentes documentos listados na nota da SAP [767598 ] e nestas notas SAP:

* [826037] 
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Informações específicas para o SAP liveCache no Windows
### <a name="sap-livecache-version-support"></a>Suporte de versão do SAP liveCache
A versão mínima do SAP liveCache com suporte nas Máquinas Virtuais do Azure é **SAP LC/LCAPPS 10.0 SP 25**, incluindo **liveCache 7.9.08.31** e **LCA-Build 25**, lançado para **EhP 2 for SAP SCM 7.0** e superior.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Versões do Microsoft Windows e tipos de VM do Azure com suporte para DBMS do SAP liveCache
versão do Microsoft Windows hello suporte toofind para liveCache SAP no Azure, consulte:

* [PAM (Matriz de Disponibilidade de Produto) da SAP][sap-pam]
* Nota SAP [1928533]

É altamente recomendável toouse hello mais nova versão do sistema operacional de saudação do Microsoft Windows Server. 

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do SAP liveCache para instalações do SAP em VMs do Azure
#### <a name="recommended-azure-vm-types"></a>Tipos de VM do Azure recomendados
Como SAP liveCache é um aplicativo que executa cálculos imensos, quantidade hello e velocidade de RAM e CPU tem uma influência principais no desempenho de liveCache do SAP. 

Para tipos de VM do Azure Olá suportados pelo SAP (nota da SAP [1928533]), todos os recursos de CPU virtuais alocada toohello VM contam com recursos de CPU físicos dedicados de hipervisor hello. Não ocorre o excesso de provisionamento (e, portanto, nenhuma competição por recursos de CPU).

Da mesma forma, para todos os tipos de instância de VM do Azure suportados pelo SAP, a memória da VM Olá é 100% mapeado toohello memória física – excesso de provisionamento (sobreposição), por exemplo, não é usada.

Sob essa perspectiva, é altamente recomendável toouse Olá nova série D ou série DS (em combinação com o armazenamento do Azure Premium) do Azure VM tipo, pois eles não têm processadores mais rápidos de 60% de Olá série. Para hello mais RAM e CPU de carga, você pode usar série G e as VMs da série GS (em combinação com o armazenamento do Azure Premium) com o processador de Intel® Xeon® mais recente Olá E5 v3 família, que têm duas vezes a memória hello e quatro vezes Olá unidade armazenamento de estado sólido (SSDs) de saudação D / Série DS.

#### <a name="storage-configuration"></a>Configuração de armazenamento
Como o SAP liveCache se baseia na tecnologia de SAP MaxDB, todos os Olá armazenamento do Azure práticas recomendadas mencionadas para SAP MaxDB capítulo [configuração de armazenamento] [ dbms-guide-8.4.1] também são válidos para liveCache do SAP. 

#### <a name="dedicated-azure-vm-for-livecache"></a>VM do Azure dedicada para o liveCache
Como o SAP liveCache usa intensivamente a potência computacional, para o uso produtivo é altamente recomendável toodeploy em uma máquina de Virtual dedicado do Azure. 

![VM do Azure dedicada para liveCache para caso de uso produtivo][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Backup e restauração
Backup e restauração, incluindo considerações de desempenho, já estão descritas nos capítulos de SAP MaxDB relevantes Olá [de Backup e restauração] [ dbms-guide-8.4.2] e [considerações sobre desempenho de Backup e restaurar][dbms-guide-8.4.3]. 

#### <a name="other"></a>outro
Todos os outros tópicos gerais são descritos Olá MaxDB relevantes do SAP [isso] [ dbms-guide-8.4.4] capítulo. 

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Especificações de saudação servidor de conteúdo do SAP no Windows
saudação de servidor de conteúdo do SAP é um conteúdo de toostore componente separado, com base em servidor, como documentos eletrônicos em formatos diferentes. saudação de servidor de conteúdo do SAP é fornecida pelo desenvolvimento de tecnologia e está entre aplicativos toobe usado para todos os aplicativos SAP. Ele é instalado em um sistema separado. Conteúdo típico é treinamento material e a documentação do depósito de dados de conhecimento ou técnicos desenhos provenientes de saudação mySAP PLM sistema de gerenciamento de documentos. 

### <a name="sap-content-server-version-support"></a>Suporte de versão do SAP Content Server
No momento o SAP dá suporte ao:

* **SAP Content Server** com a versão **6.50 (e superiores)**
* **SAP MaxDB versão 7.9**
* **IIS (Servidor de informações da Internet) da Microsoft versão 8.0 (e posterior)**

É altamente recomendável toouse hello mais nova versão do servidor de conteúdo SAP, que em tempo de saudação de escrever este documento é **6.50 SP4**e a versão mais recente de saudação do **Microsoft IIS 8.5**. 

Verificar versões hello mais recente com suporte do servidor de conteúdo do SAP e o Microsoft IIS no hello [matriz de disponibilidade de produto do SAP (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Tipos de VM do Azure e Microsoft Windows com suporte para o SAP Content Server
toofind-out da versão com suporte do Windows para o servidor de conteúdo do SAP no Azure, consulte:

* [PAM (Matriz de Disponibilidade de Produto) da SAP][sap-pam]
* Nota SAP [1928533]

É altamente recomendável toouse hello mais nova versão do Microsoft Windows Server.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do SAP Content Server para instalações do SAP em VMs do Azure
#### <a name="storage-configuration"></a>Configuração de armazenamento
Se você configurar os arquivos do servidor de conteúdo do SAP toostore no banco de dados de SAP MaxDB hello, todo o armazenamento do Azure melhor práticas recomendação mencionada para SAP MaxDB capítulo [configuração de armazenamento] [ dbms-guide-8.4.1] também são válido para o cenário de servidor de conteúdo do SAP hello. 

Se você configurar arquivos do servidor de conteúdo do SAP toostore no sistema de arquivos Olá, é recomendável toouse uma unidade lógica dedicada. Usando espaços de armazenamento do Windows permite que você tooalso aumente o tamanho de disco lógico e produtividade de IOPS, conforme descrito no capítulo [RAID de Software][dbms-guide-2.2]. 

#### <a name="sap-content-server-location"></a>Local do SAP Content Server
Servidor de conteúdo do SAP tem toobe implantado em Olá mesma região do Azure e rede virtual do Azure onde Olá sistema SAP é implantado. Você é livre toodecide se deseja toodeploy componentes de servidor de conteúdo do SAP em uma VM do Azure dedicada ou em Olá mesma VM onde Olá sistema SAP está sendo executado. 

![VM do Azure dedicada para SAP Content Server][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Local do SAP Cache Server
Olá SAP servidor de Cache é um componente adicional com base em servidor tooprovide too(cached) documentos acesso localmente. Olá SAP servidor de Cache armazena em cache os documentos de saudação de um servidor de conteúdo do SAP. Isso é o tráfego de rede toooptimize se documentos tem toobe mais de uma vez recuperado de diferentes locais. regra geral Olá é que o servidor de Cache SAP Olá tem toobe toohello fisicamente fechar cliente que acessa Olá servidor de Cache do SAP. 

Aqui você tem duas opções:

1. **Cliente é um sistema SAP de back-end** se um sistema SAP de back-end estiver configurado tooaccess servidor de conteúdo do SAP, esse sistema SAP é um cliente. Como o sistema SAP e o servidor de conteúdo do SAP são implantados em Olá mesma região do Azure – em Olá mesmo datacenter do Azure – eles são fisicamente fechar tooeach outros. Portanto, não há nenhuma necessidade toohave um servidor de Cache dedicado do SAP. Olá acesso de clientes (SAP GUI ou navegador da web) da interface do usuário do SAP sistema SAP diretamente e hello SAP sistema recupera documentos de saudação servidor de conteúdo do SAP.
2. **Cliente é um navegador da web local** Olá servidor de conteúdo do SAP pode ser configurado toobe acessado diretamente pelo navegador da web de saudação. Nesse caso, um navegador da web em execução no local é um cliente de saudação servidor de conteúdo do SAP. Datacenter local e datacenter do Azure são colocados em locais físicos diferentes (o ideal é fechar tooeach outros). Seu datacenter local é tooAzure conectado por meio de VPN Site a Site do Azure, ou rota expressa. Embora as duas opções oferecem tooAzure de conexão de rede VPN segura, conexão de rede site a site não tem um SLA de largura de banda e latência de rede entre o datacenter local de saudação e Olá datacenter do Azure. toospeed backup toodocuments de acesso, você pode fazer um dos seguintes hello:
   1. Instalar o local do servidor de Cache do SAP, feche o navegador de local toohello (opção [isso] [ dbms-guide-900-sap-cache-server-on-premises] figura)
   2. Configure a Azure ExpressRoute, que oferece uma conexão de rede dedicada de alta velocidade e baixa latência entre o datacenter local e o datacenter do Azure.

![Opção tooinstall SAP servidor de Cache local][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Backup/restauração
Se você configurar arquivos de toostore do servidor de conteúdo do SAP Olá no banco de dados de SAP MaxDB hello, considerações de desempenho e o procedimento de backup/restauração Olá já são descritas nos capítulos de SAP MaxDB [de Backup e restauração] [ dbms-guide-8.4.2] e capítulo [considerações sobre desempenho de Backup e restauração][dbms-guide-8.4.3]. 

Se você configurar arquivos de toostore do servidor de conteúdo do SAP Olá no sistema de arquivos hello, uma opção é backup/restauração tooexecute manual da estrutura de todo o arquivo hello onde se encontram os documentos de saudação. Semelhante tooSAP MaxDB backup/restauração, é recomendável toohave um volume de disco dedicado para fins de backup. 

#### <a name="other"></a>outro
Outras configurações específicas do servidor de conteúdo do SAP são VMs tooAzure transparente e são descritas em vários documentos e observações sobre o SAP:

* <https://service.sap.com/contentserver> 
* Nota SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Especificações tooIBM DB2 para LUW no Windows
Com o Microsoft Azure, você pode facilmente migrar seu aplicativo existente do SAP em execução no IBM DB2 para máquinas virtuais de tooAzure Linux, UNIX e Windows (LUW). Com o SAP no IBM DB2 para LUW, administradores e desenvolvedores ainda podem usar Olá mesmas ferramentas de desenvolvimento e administração que estão disponíveis no local.
Informações gerais sobre como executar o SAP Business Suite no IBM DB2 para LUW pode ser encontrada no hello SAP comunidade rede (SCN) em <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>.

Para obter informações adicionais e atualizações sobre o SAP no DB2 para LUW no Azure, consulte a Nota SAP [2233094]. 

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Suporte de versão do IBM DB2 para Linux, UNIX e Windows
Há suporte para o SAP no IBM DB2 para LUW nos serviços de máquina virtual do Microsoft Azure a partir da versão 10.5 do DB2.

Para obter informações sobre produtos SAP com suporte e tipos de VM do Azure, consulte tooSAP Observação [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do IBM DB2 para Linux, UNIX e Windows para instalações do SAP em VMs do Azure
#### <a name="storage-configuration"></a>Configuração de armazenamento
Todos os arquivos de banco de dados devem ser armazenados no sistema de arquivos NTFS de saudação com base nos discos conectados diretamente. Esses discos são montado toohello VM do Azure e são baseados no armazenamento de BLOB de página do Azure (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) ou em discos gerenciado (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Qualquer tipo de unidades de rede ou de compartilhamentos remotos como Olá seguintes serviços de arquivo do Azure é **não** tem suporte para arquivos de banco de dados: 

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Se você estiver usando discos com base no armazenamento de BLOB de página do Azure ou discos gerenciados, Olá instruções feitas neste documento capítulo [estrutura de uma implantação do RDBMS] [ dbms-guide-2] também se aplicam toodeployments com hello IBM DB2 para LUW o banco de dados. 

Conforme explicado anteriormente na parte de geral de saudação do documento hello, existem cotas em produtividade de IOPS para discos. cotas exata Olá dependem Olá VM tipo usado. Uma lista de tipos VM com suas cotas pode ser encontrada [aqui (Linux)][virtual-machines-sizes-linux] e [aqui (Windows)][virtual-machines-sizes-windows].

Como Olá atual cota IOPS por disco é suficiente, é possível toostore todos Olá arquivos de banco de dados em um único disco montado. 

Para desempenho considerações também consulte toochapter "de segurança e desempenho considerações para banco de dados de diretórios de dados" no guia de instalação do SAP.

Como alternativa, você pode usar Pools de armazenamento do Windows (somente disponível no Windows Server 2012 e superior) ou a distribuição do Windows para o Windows 2008 R2, como descrito no capítulo [RAID de Software] [ dbms-guide-2.2] deste documento toocreate um grande dispositivo lógico através de vários discos.
Para discos de saudação que contém os caminhos de armazenamento Olá DB2 para os diretórios dadosSAP e saptmp, você deve especificar um tamanho de setor do disco físico de 512 KB. Ao usar Pools de armazenamento do Windows, você deve criar hello pools de armazenamento manualmente por meio da interface de linha de comando usando o parâmetro hello "-LogicalSectorSizeDefault". Para obter mais informações, consulte <https://technet.microsoft.com/itpro/powershell/windows/storage/new-storagepool>.

#### <a name="backuprestore"></a>Backup/restauração
funcionalidade de backup/restauração Olá para IBM DB2 para LUW tem suporte em Olá mesmo a maneira como no padrão de sistemas operacionais Windows Server e Hyper-V.

Você deve se certificar de que tenha uma estratégia de backup do banco de dados válida em vigor. 

Como em implantações bare-metal, o desempenho de backup/restauração depende de quantos volumes podem ser lidas em paralelo e taxa de transferência que Olá desses volumes pode ser. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com apenas os segmentos de CPU de tooeight. Portanto, é possível supor que:

* Hello menos Olá número de discos usados toostore Olá dispositivos de banco de dados, Olá Olá menor geral taxa de transferência de leitura
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup
* Olá menos destinos (diretórios de distribuição, discos) toowrite Olá backup, throughput menor de Olá Olá

número de saudação de tooincrease de toowrite de destinos para, duas opções podem ser usado/combinados dependendo de suas necessidades:

* A distribuição de volume de destino de backup Olá através de vários discos na taxa de transferência de ordem tooimprove Olá IOPS nesse volume distribuído
* Usar mais de um destino diretório toowrite Olá backup em

#### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastre
Não há suporte para o MSCS (Microsoft Cluster Server).

Há suporte para HADR (alta disponibilidade e recuperação de desastre) do DB2. Se máquinas virtuais de saudação da configuração de HA Olá tiver resolução de nomes funcional, instalação Olá no Azure não diferente de qualquer configuração que é feita no local. Não é recomendável toorely apenas a resolução de IP.

Não use a replicação geográfica para contas de armazenamento Olá que armazenam discos de banco de dados de saudação. Para obter mais informações, consulte toochapter [armazenamento do Microsoft Azure] [ dbms-guide-2.3] e capítulo [alta disponibilidade e recuperação de desastres com VMs do Azure] [ dbms-guide-3].

#### <a name="other"></a>outro
Todos os outros tópicos gerais como o monitoramento de conjuntos de disponibilidade do Azure ou SAP aplicam conforme descrito em Olá três primeiros capítulos deste documento para implantações de VMs com IBM DB2 para LUW também. 

Consulte também toochapter [gerais do SQL Server para SAP no Azure resumo][dbms-guide-5.8].

## <a name="specifics-tooibm-db2-for-luw-on-linux"></a>Especificações tooIBM DB2 para LUW no Linux
Com o Microsoft Azure, você pode facilmente migrar seu aplicativo existente do SAP em execução no IBM DB2 para máquinas virtuais de tooAzure Linux, UNIX e Windows (LUW). Com o SAP no IBM DB2 para LUW, administradores e desenvolvedores ainda podem usar Olá mesmas ferramentas de desenvolvimento e administração que estão disponíveis no local. Informações gerais sobre como executar o SAP Business Suite no IBM DB2 para LUW pode ser encontrada no hello SAP comunidade rede (SCN) em <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>.

Para obter informações adicionais e atualizações sobre o SAP no DB2 para LUW no Azure, consulte a Nota SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Suporte de versão do IBM DB2 para Linux, UNIX e Windows
Há suporte para o SAP no IBM DB2 para LUW nos serviços de máquina virtual do Microsoft Azure a partir da versão 10.5 do DB2.

Para obter informações sobre produtos SAP com suporte e tipos de VM do Azure, consulte tooSAP Observação [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Diretrizes de configuração do IBM DB2 para Linux, UNIX e Windows para instalações do SAP em VMs do Azure
#### <a name="storage-configuration"></a>Configuração de armazenamento
Todos os arquivos de banco de dados devem ser armazenados no sistema de arquivos com base em discos de conexão direta. Esses discos são montado toohello VM do Azure e são baseados no armazenamento de BLOB de página do Azure (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) ou em discos gerenciado (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Qualquer tipo de unidades de rede ou de compartilhamentos remotos como Olá seguintes serviços de arquivo do Azure é **não** tem suporte para arquivos de banco de dados:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Se você estiver usando discos com base no armazenamento de BLOB de página do Azure, Olá instruções feitas neste documento capítulo [estrutura de uma implantação do RDBMS] [ dbms-guide-2] também se aplicam toodeployments com hello IBM DB2 para LUW banco de dados.

Conforme explicado anteriormente na parte de geral de saudação do documento hello, existem cotas em produtividade de IOPS para discos. cotas exata Olá dependem Olá VM tipo usado. Uma lista de tipos VM com suas cotas pode ser encontrada [aqui (Linux)][virtual-machines-sizes-linux] e [aqui (Windows)][virtual-machines-sizes-windows].

Como Olá atual cota IOPS por disco é suficiente, é possível toostore todos Olá arquivos de banco de dados em um único disco.

Para desempenho considerações também consulte toochapter "de segurança e desempenho considerações para banco de dados de diretórios de dados" no guia de instalação do SAP.

Como alternativa, você pode usar LVM (Gerenciador de Volume lógico) ou MDADM conforme descrito no capítulo [RAID de Software] [ dbms-guide-2.2] deste documento toocreate uma grande lógico dispositivo através de vários discos.
Para discos de saudação que contém os caminhos de armazenamento Olá DB2 para os diretórios dadosSAP e saptmp, você deve especificar um tamanho de setor do disco físico de 512 KB.

#### <a name="backuprestore"></a>Backup/restauração
funcionalidade de backup/restauração Olá para IBM DB2 para LUW tem suporte em Olá mesma maneira padrão Linux instalação local.

Você deve se certificar de que tenha uma estratégia de backup do banco de dados válida em vigor.

Como em implantações bare-metal, o desempenho de backup/restauração depende de quantos volumes podem ser lidas em paralelo e taxa de transferência que Olá desses volumes pode ser. Além disso, Olá consumo de CPU usado pela compactação de backup pode têm um papel significativo em VMs com apenas os segmentos de CPU de tooeight. Portanto, é possível supor que:

* Hello menos Olá número de discos usados toostore Olá dispositivos de banco de dados, Olá Olá menor geral taxa de transferência de leitura
* Olá menor número de saudação de threads de CPU no Olá VM, Olá mais graves do impacto de saudação da compactação de backup
* Olá menos destinos (diretórios de distribuição, discos) toowrite Olá backup, throughput menor de Olá Olá

número de saudação de tooincrease de toowrite de destinos para, duas opções podem ser usado/combinados dependendo de suas necessidades:

* A distribuição de volume de destino de backup Olá através de vários discos na taxa de transferência de ordem tooimprove Olá IOPS nesse volume distribuído
* Usar mais de um destino diretório toowrite Olá backup em

#### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastre
Há suporte para HADR (alta disponibilidade e recuperação de desastre) do DB2. Se máquinas virtuais de saudação da configuração de HA Olá tiver resolução de nomes funcional, instalação Olá no Azure não diferente de qualquer configuração que é feita no local. Não é recomendável toorely apenas a resolução de IP.

Não use a replicação geográfica para contas de armazenamento Olá que armazenam discos de banco de dados de saudação. Para obter mais informações, consulte toochapter [armazenamento do Microsoft Azure] [ dbms-guide-2.3] e capítulo [alta disponibilidade e recuperação de desastres com VMs do Azure] [ dbms-guide-3].

#### <a name="other"></a>outro
Todos os outros tópicos gerais como o monitoramento de conjuntos de disponibilidade do Azure ou SAP aplicam conforme descrito em Olá três primeiros capítulos deste documento para implantações de VMs com IBM DB2 para LUW também.

Consulte também toochapter [gerais do SQL Server para SAP no Azure resumo][dbms-guide-5.8].

