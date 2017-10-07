---
title: aaaGetting iniciado com a SAP em VMs do Azure | Microsoft Docs
description: "Saiba como executar as soluções SAP em VMs (máquinas virtuais) no Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a>Usar o Azure para hospedar e executar cenários de carga de trabalho do SAP
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

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
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
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
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
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
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
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

Escolhendo o Microsoft Azure como seu parceiro de nuvem pronto SAP, você está tooreliably capaz de executar dos cenários e críticas SAP cargas de trabalho em uma plataforma escalonável, compatível e corporativa comprovada.  Obter escalabilidade hello, flexibilidade, economia e de custos do Azure. Com hello expandido parceria entre a Microsoft e SAP, você pode executar aplicativos SAP em cenários de desenvolvimento/teste e produção no Azure - e totalmente suportados. Do SAP NetWeaver tooSAP S4/HANA, SAP BI, tooWindows Linux, tooSQL do SAP HANA, temos suas necessidades. 

Além de hospedagem cenários SAP NetWeaver com Olá diferentes DBMS no Azure, você pode hospedar diferentes outros cenários de carga de trabalho do SAP, como SAP BI no Azure. Documentação sobre as implantações do SAP NetWeaver em máquinas virtuais nativo do Azure pode ser encontrada na seção de hello "SAP NetWeaver nas máquinas virtuais do Azure". 

O Azure tem nativo ofertas de máquina Virtual do Azure que já estão crescendo em tamanho de memória e CPU recursos toocover SAP carga de trabalho que utiliza o SAP HANA. Para obter mais informações sobre este tópico, procurar documentos Olá na seção Olá SAP HANA em máquinas virtuais do Azure."

exclusividade de saudação do Azure para SAP HANA é uma oferta exclusiva que destaca Azure concorrência. Em ordem tooenable hospedagem mais recursos de CPU e memória SAP exigente cenários que envolvem o SAP HANA, o Azure oferece uso de saudação do cliente dedicado hardware bare-metal para finalidade de saudação da execução de implantações do SAP HANA que exigem até too20 TB (expansão do 60 TB) de memória para 4HANA/S ou outra carga de trabalho do SAP HANA. Essa solução exclusiva do Azure do SAP HANA no Azure (instâncias grandes) permite que você toorun SAP HANA em hardware de bare-metal Olá dedicado com camada do aplicativo SAP hello ou camada de intermediários de carga de trabalho hospedados em nativo máquinas virtuais do Azure. Esta solução está documentada em vários documentos na seção hello "SAP HANA no Azure (instâncias grandes)".   

Cenários de carga de trabalho do SAP no Azure de hospedagem também podem criar requisitos de integração de identidade e Single-Sign-On usando componentes do diretório de atividade do Azure toodifferent SAP e SAP SaaS ou PaaS oferece. Uma lista de tais integração e cenários de logon único com entidades do Azure Active Directory (AAD) e SAP é descrita e documentada na seção hello "integração do AAD SAP identidade e logon único."


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a>SAP HANA no SAP HANA no Azure (Instâncias Grandes)

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a>Visão geral e arquitetura do SAP HANA no Azure (Instâncias Grandes)
título: aaaOverview e arquitetura do HANA SAP no Azure (instâncias grandes)

Resumo: Essa arquitetura e o guia de implantação técnica fornece informações toohelp você implanta um sistema SAP em Olá novo HANA SAP no Azure (instâncias grandes) no Azure. Não é pretendido toobe uma configuração específica de cobertura abrangente do guia de soluções SAP, mas as informações úteis na sua implantação inicial e as operações em andamento. Documentação do SAP não deve substituir relacionadas toohello instalação do SAP HANA (ou Olá muitas anotações de suporte do SAP que abrangem o tópico de saudação). Ele fornece uma visão geral e fornece detalhes adicionais de saudação de instalação do SAP HANA no Azure (instâncias grandes).

Atualização: julho de 2017

[Esse guia pode ser encontrado aqui](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a>Infraestrutura e conectividade tooSAP HANA no Azure (instâncias grandes)
título: aaaInfrastructure e conectividade tooSAP HANA no Azure (instâncias grandes)

Resumo: Após a compra de saudação do HANA SAP no Azure (instâncias grandes) é finalizada entre você e Olá, equipe de contas da Microsoft enterprise, várias configurações de rede são necessárias na conectividade adequada de tooensure de ordem.  Essas informações de Olá de estruturas de tópicos de documento que tenha toobe compartilhado com hello informações a seguir são necessárias. Este documento descreve quais informações tem toobe coletados e quais scripts de configuração têm toobe executar. 

Atualização: julho de 2017

[Esse guia pode ser encontrado aqui](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a>Instalar o SAP HANA no SAP HANA no Azure (Instâncias Grandes)
título: aaaInstall SAP HANA no SAP HANA no Azure (instâncias grandes)

Resumo: Este documento descreve procedimentos Olá de instalação do SAP HANA na instância grande do Azure. 

Atualização: julho de 2017

[Esse guia pode ser encontrado aqui](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a>Alta disponibilidade e recuperação de desastre do SAP HANA no Azure (Instâncias Grandes)
título: aaaHigh disponibilidade e desastres recuperação do SAP HANA no Azure (instâncias grandes)

Resumo: HA (Alta Disponibilidade) e DR (Recuperação de Desastre) são aspectos muito importantes da execução do SAP HANA crítico em servidores do Azure (Instâncias Grandes). Seu toowork importação com o SAP, o integrador de sistema e/ou Microsoft tooproperly projetar e implementa direita Olá estratégia de HA/DR para você. Considerações importantes como o objetivo de ponto de recuperação (RPO) e recuperação tempo RTO (objetivo de), ambiente tooyour específico, devem ser consideradas.  Este documento explica as opções para habilitar o nível preferencial de HA e DR.

Atualização: dezembro de 2016

[Este documento pode ser encontrado aqui](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a>Solução de problemas e monitoramento do SAP HANA no Azure (Instâncias Grandes)
título: aaaTroubleshooting e monitoramento do SAP HANA no Azure (instâncias grandes)

Resumo: Este guia inclui informações úteis para estabelecer o monitoramento do SAP HANA no ambiente do Azure, bem como informações de solução de problemas adicionais. 

Atualização: dezembro de 2016

[Este documento pode ser encontrado aqui](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a>SAP HANA em Máquinas Virtuais do Azure

### <a name="getting-started-with-sap-hana-on-azure"></a>Introdução ao SAP HANA no Azure
título: guia aaaQuickstart para instalação manual do HANA SAP em VMs do Azure

Resumo: Este guia de início rápido ajuda tooset um sistema de SAP HANA do instância única em VMs do Azure por uma instalação manual de 7.5 do SAP NetWeaver e SAP HANA SP12. Guia de saudação presume que o leitor de saudação esteja familiarizado com conceitos básicos de IaaS do Azure como como máquinas virtuais de toodeploy ou redes virtuais através de saudação portal do Azure ou do Powershell/CLI incluindo Olá modelos de json toouse opção. Além disso é esperado que o leitor Olá esteja familiarizado com como tooinstall-lo no local, SAP NetWeaver e SAP HANA.

Atualização: junho de 2017

[Esse guia pode ser encontrado aqui](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a>Implantação do CAL SAP S/4HANA no Azure
título: aaaDeploy 4HANA/S de SAP ou BW/4HANA no Azure

Resumo: Este guia ajuda a implantação de saudação toodemonstrate de S/4HANA do SAP no Azure usando a biblioteca de dispositivo de nuvem do SAP. Biblioteca de dispositivo de nuvem do SAP é um serviço SAP que permite que os aplicativos toodeploy SAP no Azure. Guia de saudação descreve Olá passo a passo de implantação.

Atualização: junho de 2017

[Esse guia pode ser encontrado aqui](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a>Alta disponibilidade do SAP HANA em máquinas virtuais do Azure
título: aaaHigh disponibilidade do SAP HANA em máquinas virtuais do Azure

Resumo: Este guia orienta você durante a configuração de alta disponibilidade de saudação do hello SUSE 12 SO e replicação de sistema do HANA SAP HANA tooaccommodate com failover automático. Guia de saudação é específico para máquinas virtuais do Azure e o SUSE. Guia de saudação não se aplica a ainda Red Hat ou bare-metal ou privada nuvem ou outras implantações de nuvem pública do Azure não.

Atualização: junho de 2017

[Esse guia pode ser encontrado aqui](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a>Visão geral de backup do SAP HANA em VMs do Azure
título: guia aaaBackup do SAP HANA em máquinas virtuais do Azure

Resumo: este guia fornece informações básicas sobre possibilidades de backup ao executar SAP HANA em máquinas virtuais do Azure.

Atualização: março de 2017

[Esse guia pode ser encontrado aqui](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a>Backup de nível de arquivo do SAP HANA em VMs do Azure
título: backup do HANA aaaSAP com base em instantâneos de armazenamento

Resumo: este guia fornece informações sobre como usar backups baseados em instantâneo com base em VMs do Azure ao executar o SAP HANA em máquinas virtuais do Azure.

Atualização: março de 2017

[Esse guia pode ser encontrado aqui](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a>Backups baseados em instantâneo SAP HANA em VMs do Azure
título: aaaSAP HANA Azure Backup em nível de arquivo

Resumo: este guia fornece informações sobre como usar backup em nível de arquivo do SAP HANA ao executar o SAP HANA em máquinas virtuais do Azure

Atualização: março de 2017

[Esse guia pode ser encontrado aqui](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>SAP NetWeaver implantado em Máquinas Virtuais do Azure

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a>Implantar o sistema SAP IDES no Windows e o SQL Server por meio de CAL do SAP no Azure
título: aaaTesting SAP NetWeaver nas máquinas virtuais do Microsoft Azure SUSE Linux 

Resumo: Este documento descreve a implantação de saudação de um sistema SAP IDES com base no Windows e no SQL Server no Azure usando a biblioteca de dispositivo de nuvem do SAP. Dispositivo de nuvem do SAP biblioteca é um serviço SAP que permite a implantação de saudação de produtos SAP no Azure. Este documento vai passo a passo através da implantação de saudação de um sistema SAP IDES. Olá sistema IDES é apenas um exemplo de vários outros aplicativos de doze que podem ser implantadas por meio do dispositivo de nuvem do SAP no Microsoft Azure.

Atualização: junho de 2017

[Esse guia pode ser encontrado aqui](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a>Guia de início rápido do NetWeaver no SUSE Linux no Azure
título: aaaTesting SAP NetWeaver nas máquinas virtuais do Microsoft Azure SUSE Linux 

Resumo: Este artigo descreve vários tooconsider de coisas quando você estiver executando o SAP NetWeaver nas máquinas virtuais de SUSE Linux do Microsoft Azure (VMs). O SAP NetWeaver tem suporte oficial em VMs do SUSE Linux no Azure. Todos os detalhes relativos a versões do Linux, versões de kernel do SAP e outros detalhes podem ser encontrados na Nota SAP 1928533 "Aplicativos SAP no Azure: produtos com suporte e tipos de VM do Azure".

Atualizado: setembro de 2016

[Esse guia pode ser encontrado aqui](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planejamento e implementação
título: aaaAzure máquinas virtuais de planejamento e implementação do SAP NetWeaver

Resumo: Este documento é Olá guia toostart com se você está pensando em SAP NetWeaver no Azure máquinas virtuais em execução. Este guia de planejamento e implementação ajuda você a avaliar se um sistema baseado em SAP NetWeaver existente ou planejado pode ser implantado tooan ambiente de máquinas virtuais do Azure. Ele abrange vários cenários de implantação do SAP NetWeaver e inclui configurações SAP que são tooAzure específico. papel Olá lista e descreve todas as Olá informações de configuração necessárias, será necessário no hello SAP/Azure lado toorun uma paisagem SAP híbrida. Medidas que você pode tomar tooensure alta disponibilidade de sistemas baseados no SAP NetWeaver em IaaS também são abordadas.

Atualização: junho de 2017

[Este guia pode ser encontrado aqui][planning-guide]

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a>Configurações de alta disponibilidade do SAP NetWeaver em VMs do Azure
título: aaaAzure alta disponibilidade de máquinas virtuais para o SAP NetWeaver

Resumo: Este documento, abordaremos Olá etapas que toodeploy sistemas SAP de alta disponibilidade no Azure usando o modelo de implantação do Azure Resource Manager hello. Percorreremos essas tarefas principais. Documento hello, descreveremos como único-ponto de falha componentes como avançado Business aplicativo programação (ABAP) SAP Central Services (ASCS) / SAP Central Services (SCS) e sistemas de gerenciamento de banco de dados (DBMS) e componentes redundantes, como SAP Servidor de aplicativos for toobe protegido durante a execução em VMs do Azure. Um exemplo passo a passo da instalação e configuração de um sistema SAP de alta disponibilidade em um cluster do Clustering de Failover do Windows Server no o Azure é demonstrado neste documento.

Atualização: junho de 2017

[Esse guia pode ser encontrado aqui](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a>Reconhecimento de implantações multi-SID do SAP NetWeaver em VMs do Azure
título: aaaCreate uma configuração de multi-SID do SAP NetWeaver 

Resumo: Este é um documento de toohello adição alta disponibilidade para o SAP NetWeaver em VMs do Azure. Devido a funcionalidade de toonew no Azure que foi introduzido em setembro de 2016, é possível toodeploy vários SAP NetWeaver ASCS/SCS instâncias em um par de máquinas virtuais do Azure. Com essa configuração, você pode reduzir o número de saudação de VMs toodeploy necessário toorealize altamente disponível SAP NetWeaver configurações. Guia de saudação descreve instalação Olá essas configurações de multi-SID.

Atualização: dezembro de 2016

[Esse guia pode ser encontrado aqui](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Implantação do SAP NetWeaver em VMs do Azure
título: aaaAzure implantação de máquinas virtuais para o SAP NetWeaver

Resumo: Este documento fornece orientação de procedimentos para implantação de máquinas de toovirtual de software SAP NetWeaver no Azure. Este documento se concentra em três cenários de implantação específicos, com ênfase em capacitar as extensões de monitoramento do Azure Olá para SAP, incluindo recomendações de solução para Olá extensões de monitoramento do Azure para SAP. Este artigo pressupõe que você leu Olá planejamento e guia de implementação.

Atualização: junho de 2017

[Este guia pode ser encontrado aqui][deployment-guide]

### <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Guia de implantação de DBMS
título: aaaAzure implantação de máquinas virtuais de DBMS para SAP NetWeaver

Resumo: Este documento aborda considerações de planejamento e implementação de sistemas DBMS Olá que devem ser executado em conjunto com o SAP. Na primeira parte de hello, considerações gerais são listadas e apresentadas. Olá seguintes partes do documento hello relacionam toodeployments dos diferentes DBMS suportados pelo SAP no Azure. Os DBMS diferentes apresentados são o SQL Server, o SAP ASE e o Oracle. Essas partes específicas, considerações têm tooaccount para quando você estiver executando os sistemas SAP no Azure em conjunto com esses DBMS são discutidas. Assuntos como métodos de backup e alta disponibilidade que são suportados pelo Olá que diferentes DBMS no Azure são apresentados para uso de saudação com aplicativos SAP.

Atualização: junho de 2017

[Este guia pode ser encontrado aqui][dbms-guide]

### <a name="using-azure-site-recovery-for-sap-workload"></a>Usando o Azure Site Recovery para carga de trabalho SAP
título: aaaSAP NetWeaver: Criando uma solução de recuperação de desastres com o Azure Site Recovery 

Resumo: Este documento descreve a forma de saudação como serviços do Azure Site Recovery podem ser usados para fins de saudação de lidar com cenários de recuperação de desastres. Casos em que o Azure é usado como local de recuperação de desastre para uma paisagem SAP local usando os Serviços do Azure Site Recovery. Outro cenário descrito no documento de saudação é o caso de recuperação de desastres Olá Aure para Azure (A2A) e como ele é gerenciado com o Azure Site Recovery.  

Atualização: agosto de 2017

[Esse guia pode ser encontrado aqui](http://aka.ms/asr-sap)

