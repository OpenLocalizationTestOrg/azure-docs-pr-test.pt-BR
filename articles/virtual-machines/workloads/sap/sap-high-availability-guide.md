---
title: "Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver | Microsoft Docs"
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
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="5f0da-103">Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="5f0da-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="5f0da-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="5f0da-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="5f0da-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="5f0da-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="5f0da-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="5f0da-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="5f0da-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="5f0da-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="5f0da-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="5f0da-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="5f0da-109">As Máquinas Virtuais do Azure são a solução para as organizações que precisam de recursos de computação, armazenamento e rede, no mínimo de tempo e sem ciclos de compra longos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="5f0da-110">Você pode usar Máquinas Virtuais do Azure para implantar aplicativos clássicos como o ABAP baseado no SAP NetWeaver, Java e uma pilha ABAP+Java.</span><span class="sxs-lookup"><span data-stu-id="5f0da-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="5f0da-111">Estenda a confiabilidade e a disponibilidade sem recursos locais adicionais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="5f0da-112">As Máquinas Virtuais do Azure dão suporte à conectividade entre locais, o que permite que você integre as Máquinas Virtuais do Azure aos seus domínios locais, a nuvens privadas e à estrutura do sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="5f0da-113">Neste artigo, abordaremos as etapas que você pode tomar para implantar sistemas SAP de alta disponibilidade no Azure usando o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f0da-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5f0da-114">Vamos percorrer estas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="5f0da-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="5f0da-115">Encontrar os guias de instalação e Notas de SAP corretos, listados na seção [Recursos][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="5f0da-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="5f0da-116">Este artigo complementa a documentação de instalação do SAP e as Notas do SAP, que são os principais recursos para ajudar a instalar e a implantar o software SAP em plataformas específicas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="5f0da-117">Descubra as diferenças entre o modelo de implantação do Azure Resource Manager e o modelo de implantação clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="5f0da-118">Aprenda sobre os modos de quorum do Clustering de Failover do Windows Server para que você possa escolher o modelo certo para sua implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="5f0da-119">Aprenda sobre o armazenamento compartilhado do Windows Server Failover Clustering nos serviços Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="5f0da-120">Saiba como proteger componentes com ponto único de falha como ABAP (Advanced Business Application Programming) do ASCS (SAP Central Services)/SCS (SAP Central Services) e DBMS (sistemas de gerenciamento de banco de dados), e componentes redundantes como Servidor de Aplicativos SAP, no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="5f0da-121">Execute um exemplo passo a passo da instalação e configuração de um sistema SAP de alta disponibilidade em um cluster do Clustering de Failover do Windows Server no o Azure usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f0da-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="5f0da-122">Saiba mais sobre etapas adicionais necessárias para usar o Windows Server Failover Clustering no Azure, mas que não são necessárias em uma implantação local.</span><span class="sxs-lookup"><span data-stu-id="5f0da-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="5f0da-123">Para simplificar a implantação e a configuração, estamos usando os modelos de três camadas SAP do Resource Manager de alta disponibilidade neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="5f0da-124">Os modelos automatizam a implantação de toda a infraestrutura de que você precisa para um sistema SAP de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="5f0da-125">A infraestrutura também dá suporte ao dimensionamento SAPS (SAP Application Performance Standard) do seu sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="5f0da-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5f0da-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="5f0da-127">Antes de começar, verifique se os pré-requisitos descritos nos capítulos a seguir são atendidos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="5f0da-128">Além disso, não deixe de verificar todos os recursos listados na seção [Recursos][sap-ha-guide-2].</span><span class="sxs-lookup"><span data-stu-id="5f0da-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="5f0da-129">Neste artigo, podemos usar modelos do Azure Resource Manager para [SAP NetWeaver de três camadas usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="5f0da-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="5f0da-130">Para uma visão geral dos modelos, confira [Modelos do Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="5f0da-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="5f0da-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos</span><span class="sxs-lookup"><span data-stu-id="5f0da-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="5f0da-132">Esses artigos abordam implantações SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="5f0da-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="5f0da-133">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5f0da-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="5f0da-134">[Implantação de Máquinas Virtuais do Azure para SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5f0da-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="5f0da-135">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5f0da-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="5f0da-136">[Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver (este guia)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="5f0da-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-137">Sempre que possível, daremos a você um link para o guia de instalação do SAP de referência (confira os [guias de instalação de SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="5f0da-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="5f0da-138">Para pré-requisitos e informações sobre o processo de instalação, é recomendável que você leia os guias de instalação do SAP NetWeaver cuidadosamente.</span><span class="sxs-lookup"><span data-stu-id="5f0da-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="5f0da-139">Este artigo aborda apenas as tarefas específicas para sistemas baseados no SAP NetWeaver que você pode usar com as Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="5f0da-140">As seguintes Notas do SAP são relacionadas ao tópico do SAP no Azure:</span><span class="sxs-lookup"><span data-stu-id="5f0da-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="5f0da-141">Número da observação</span><span class="sxs-lookup"><span data-stu-id="5f0da-141">Note number</span></span> | <span data-ttu-id="5f0da-142">Title</span><span class="sxs-lookup"><span data-stu-id="5f0da-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="5f0da-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="5f0da-143">[1928533]</span></span> |<span data-ttu-id="5f0da-144">Aplicativos SAP no Azure: dimensionamento e produtos com suporte</span><span class="sxs-lookup"><span data-stu-id="5f0da-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="5f0da-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="5f0da-145">[2015553]</span></span> |<span data-ttu-id="5f0da-146">SAP no Microsoft Azure: pré-requisitos de suporte</span><span class="sxs-lookup"><span data-stu-id="5f0da-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="5f0da-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5f0da-147">[1999351]</span></span> |<span data-ttu-id="5f0da-148">Monitoramento aprimorado do Azure para SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="5f0da-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="5f0da-149">[2178632]</span></span> |<span data-ttu-id="5f0da-150">Métricas-chave de monitoramento para SAP no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="5f0da-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="5f0da-151">[1999351]</span></span> |<span data-ttu-id="5f0da-152">Virtualização no Windows: monitoramento avançado</span><span class="sxs-lookup"><span data-stu-id="5f0da-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="5f0da-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="5f0da-153">[2243692]</span></span> |<span data-ttu-id="5f0da-154">Usar o Armazenamento SSD Premium do Azure para instância do SAP DBMS</span><span class="sxs-lookup"><span data-stu-id="5f0da-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="5f0da-155">Saiba mais sobre as [limitações das assinaturas do Azure][azure-subscription-service-limits-subscription], incluindo limitações máximas e gerais padrão.</span><span class="sxs-lookup"><span data-stu-id="5f0da-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="5f0da-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidade com o Azure Resource Manager versus o modelo de implantação clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="5f0da-157">Os modelos de implantação clássico do Azure e do Azure Resource Manager são diferentes nos seguintes aspectos:</span><span class="sxs-lookup"><span data-stu-id="5f0da-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="5f0da-158">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5f0da-158">Resource groups</span></span>
- <span data-ttu-id="5f0da-159">Dependência do balanceador interno de carga do Azure no grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="5f0da-160">Suporte para cenário SAP com vários SID</span><span class="sxs-lookup"><span data-stu-id="5f0da-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="5f0da-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="5f0da-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="5f0da-162">No Azure Resource Manager, você pode usar grupos de recursos para gerenciar todos os recursos do aplicativo em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="5f0da-163">Uma abordagem integrada, em um grupo de recursos, todos os recursos têm o mesmo ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="5f0da-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="5f0da-164">Por exemplo, todos os recursos são criados ao mesmo tempo e excluídos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="5f0da-165">Saiba mais sobre [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="5f0da-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="5f0da-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Dependência do balanceador interno de carga do Azure no grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="5f0da-167">No modelo de implantação clássico do Azure, há uma dependência entre o balanceador de carga interno do Azure (o serviço do Azure Load Balancer) e os serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5f0da-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="5f0da-168">Cada balanceador de carga interno precisa de um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5f0da-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="5f0da-169">No Azure Resource Manager, todos os recursos do Azure precisam ser colocados em um grupo de recursos do Azure, e isso também é válido para o balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="5f0da-170">No entanto, não é necessário ter um grupo de recursos do Azure por balanceador de carga do Azure, por exemplo, um grupo de recursos do Azure pode conter vários balanceadores de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="5f0da-171">O ambiente é mais simples e mais flexível.</span><span class="sxs-lookup"><span data-stu-id="5f0da-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="5f0da-172">Suporte para cenário SAP com vários SID</span><span class="sxs-lookup"><span data-stu-id="5f0da-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="5f0da-173">No Azure Resource Manager, você pode instalar várias instâncias ASCS/SCS do SID (identificador do sistema SAP) em um cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="5f0da-174">Instâncias de vários SID são possíveis devido ao suporte de vários endereços IP para cada balanceador de carga interno de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="5f0da-175">Para usar o modelo de implantação clássico do Azure, siga procedimento descrito no documento [SAP NetWeaver no Azure: instâncias de SAP ASCS/SCS de clustering usando o Clustering de Failover do Windows Server no Azure com o SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="5f0da-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f0da-176">Recomendamos fortemente que você use o modelo de implantação do Azure Resource Manager para as instalações do SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="5f0da-177">Ele oferece muitos benefícios que não estão disponíveis no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="5f0da-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="5f0da-178">Saiba mais sobre os [modelos de implantação do Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="5f0da-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="5f0da-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span><span class="sxs-lookup"><span data-stu-id="5f0da-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="5f0da-180">O Windows Server Failover Clustering é a base de uma instalação do SAP ASCS/SCS de alta disponibilidade e DBMS no Windows.</span><span class="sxs-lookup"><span data-stu-id="5f0da-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="5f0da-181">Um cluster de failover é um grupo servidores 1+n independentes (nós) que trabalham juntos para aumentar a disponibilidade de aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="5f0da-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="5f0da-182">Se ocorrer uma falha de nó, o Clustering de Failover do Windows Server calculará o número de falhas que podem ocorrer e manterá um cluster íntegro para fornecer serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="5f0da-183">Você pode escolher dentre diferentes modos de quorum para obter o clustering de failover.</span><span class="sxs-lookup"><span data-stu-id="5f0da-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="5f0da-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de quorum</span><span class="sxs-lookup"><span data-stu-id="5f0da-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="5f0da-185">Você pode escolher dentre quatro modos de quorum quando usa o Windows Server Failover Clustering:</span><span class="sxs-lookup"><span data-stu-id="5f0da-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="5f0da-186">**Maioria de nós**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-186">**Node Majority**.</span></span> <span data-ttu-id="5f0da-187">Cada nó do cluster pode votar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="5f0da-188">O cluster funciona somente com a maioria dos votos, ou seja, com mais da metade dos votos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5f0da-189">Recomendamos essa opção para clusters com número ímpar de nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="5f0da-190">Por exemplo, três nós em um cluster de sete nós podem falhar e o cluster ainda pode ter maioria e continuar a executar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="5f0da-191">**Maioria de nós e disco**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="5f0da-192">Todos os nós e um disco designado no armazenamento de cluster (a testemunha de disco) podem votar sempre que estão disponíveis e em comunicação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="5f0da-193">O cluster funciona somente com a maioria dos votos, ou seja, com mais da metade dos votos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5f0da-194">Esse modo faz sentido em um ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5f0da-195">Se a metade dos nós e o disco estiverem online, o cluster permanecerá em estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="5f0da-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="5f0da-196">**Maioria de nós e compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="5f0da-197">Todos os nós e um compartilhamento de arquivos designado criado pelo administrador (a testemunha de compartilhamento de arquivos) poderão votar, independente de serem os nós e compartilhamentos de arquivos disponíveis e em comunicação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="5f0da-198">O cluster funciona somente com a maioria dos votos, ou seja, com mais da metade dos votos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="5f0da-199">Esse modo faz sentido em um ambiente de cluster com um número par de nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="5f0da-200">É semelhante ao modo Maioria de nós e disco, mas usa uma testemunha de compartilhamento de arquivos em vez de uma testemunha de disco.</span><span class="sxs-lookup"><span data-stu-id="5f0da-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="5f0da-201">Esse modo é fácil de implementar, mas se o próprio compartilhamento de arquivos não estiver altamente disponível, ele poderá se tornar um ponto único de falha.</span><span class="sxs-lookup"><span data-stu-id="5f0da-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="5f0da-202">**Sem maioria: somente disco**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="5f0da-203">O cluster terá um quorum se um nó estiver disponível e em comunicação com um disco específico no armazenamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="5f0da-204">Somente os nós que também estão em comunicação com esse disco podem ingressar no cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="5f0da-205">Recomendamos que você não use esse modo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="5f0da-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering no local</span><span class="sxs-lookup"><span data-stu-id="5f0da-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="5f0da-207">A Figura 1 mostra um cluster de dois nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="5f0da-208">Se a conexão de rede entre os nós falha e eles permanecem ativos e em execução, um compartilhamento de arquivo ou disco de quorum determina qual nó continuará a fornecer os serviços e aplicativos do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="5f0da-209">O nó que tem acesso ao compartilhamento de arquivo ou disco de quorum é o nó que garante que os serviços continuarão.</span><span class="sxs-lookup"><span data-stu-id="5f0da-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="5f0da-210">Como esse exemplo usa um cluster de dois nós, usamos o modo de quorum Maioria dos nós e compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="5f0da-211">A maioria dos nós e disco também é uma opção válida.</span><span class="sxs-lookup"><span data-stu-id="5f0da-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="5f0da-212">Em um ambiente de produção, recomendamos que você use um disco de quorum.</span><span class="sxs-lookup"><span data-stu-id="5f0da-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="5f0da-213">Você pode usar tecnologia de sistema de rede e de armazenamento para torná-lo altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="5f0da-213">You can use network and storage system technology to make it highly available.</span></span>

![Figura 1: exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="5f0da-215">_**Figura 1:** exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure_</span><span class="sxs-lookup"><span data-stu-id="5f0da-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="5f0da-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Armazenamento compartilhado</span><span class="sxs-lookup"><span data-stu-id="5f0da-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="5f0da-217">A Figura 1 também mostra um cluster de armazenamento compartilhado de dois nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="5f0da-218">Em um cluster de armazenamento compartilhado local, todos os nós no cluster detectam armazenamento compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="5f0da-219">Um mecanismo de bloqueio protege os dados contra corrupção.</span><span class="sxs-lookup"><span data-stu-id="5f0da-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="5f0da-220">Todos os nós podem detectar se outro nó falhar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="5f0da-221">Se um nó falhar, o outro assume a propriedade dos recursos de armazenamento e garante a disponibilidade dos serviços.</span><span class="sxs-lookup"><span data-stu-id="5f0da-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-222">Você não precisa de discos compartilhados de alta disponibilidade com alguns aplicativos de DBMS, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f0da-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="5f0da-223">O AlwaysOn do SQL Server replica os arquivos de log e dados do DBMS do disco local de um nó do cluster para o disco local de outro nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5f0da-224">Nesse caso, a configuração de cluster do Windows não precisa de um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5f0da-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Resolução de nome e rede</span><span class="sxs-lookup"><span data-stu-id="5f0da-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="5f0da-226">Os computadores clientes acessam o cluster em um endereço IP virtual com um nome de host virtual que o servidor DNS fornece.</span><span class="sxs-lookup"><span data-stu-id="5f0da-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="5f0da-227">Os nós locais e o servidor DNS podem lidar com vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="5f0da-228">Em uma instalação comum, você usa duas ou mais conexões de rede:</span><span class="sxs-lookup"><span data-stu-id="5f0da-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="5f0da-229">Uma conexão dedicada com o armazenamento</span><span class="sxs-lookup"><span data-stu-id="5f0da-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="5f0da-230">Uma conexão de rede interna de cluster para a pulsação</span><span class="sxs-lookup"><span data-stu-id="5f0da-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="5f0da-231">Uma rede pública que os clientes usam para se conectar ao cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="5f0da-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering no Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5f0da-233">Comparados a implantações de nuvem privada ou bare metal, as Máquinas Virtuais do Azure exigem etapas adicionais para configurar o Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="5f0da-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5f0da-234">Quando você cria um disco de cluster compartilhado, precisa definir vários endereços IP e nomes de host virtual para a instância do SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="5f0da-235">Neste artigo, discutiremos os principais conceitos e as etapas adicionais necessárias para criar um cluster SAP de serviços centrais de alta disponibilidade no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="5f0da-236">Mostramos a você como configurar a ferramenta de terceiros SIOS DataKeeper e como configurar o balanceador de carga interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="5f0da-237">Você pode usar essas ferramentas para criar um cluster de failover do Windows com uma testemunha de compartilhamento de arquivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Figura 2: configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado][sap-ha-guide-figure-1001]

<span data-ttu-id="5f0da-239">_**Figura 2:** configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado_</span><span class="sxs-lookup"><span data-stu-id="5f0da-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="5f0da-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartilhado no Azure com SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5f0da-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="5f0da-241">Você precisa de armazenamento compartilhado em cluster para uma instância do SAP ASCS/SCS de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5f0da-242">A partir de setembro de 2016, o Azure não oferece armazenamento compartilhado que você possa usar para criar um cluster de armazenamento compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="5f0da-243">Você pode usar o software de terceiros SIOS DataKeeper Cluster Edition para criar um armazenamento espelhado que simula o armazenamento compartilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="5f0da-244">A solução SIOS fornece replicação síncrona de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5f0da-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="5f0da-245">É assim que você pode criar um recurso de disco compartilhado para um cluster:</span><span class="sxs-lookup"><span data-stu-id="5f0da-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="5f0da-246">Anexe um disco adicional a cada uma das máquinas virtuais (VMs) em uma configuração de cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="5f0da-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="5f0da-247">Execute o SIOS DataKeeper Cluster Edition em ambos os nós da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="5f0da-248">Configure o SIOS DataKeeper Cluster Edition para que ele reflita o conteúdo do volume anexado do disco adicional da máquina virtual de origem para o volume anexado do disco adicional da máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="5f0da-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="5f0da-249">O SIOS DataKeeper abstrai os volumes locais de origem e de destino e os apresenta ao Windows Server Failover Clustering como um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="5f0da-250">Saiba mais sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="5f0da-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Figura 3: configuração do Clustering de Failover do Windows Server no Azure com o SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="5f0da-252">_**Figura 3:** configuração do Windows Server Failover Cluster no Azure com o SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-253">Você não precisa de discos compartilhados de alta disponibilidade com alguns produtos de DBMS, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f0da-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="5f0da-254">O AlwaysOn do SQL Server replica os arquivos de log e dados do DBMS do disco local de um nó do cluster para o disco local de outro nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="5f0da-255">Nesse caso, a configuração de cluster do Windows não precisa de um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="5f0da-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolução de nomes no Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="5f0da-257">A plataforma de nuvem do Azure não oferece a opção de configurar endereços IP virtual, como endereços IPs flutuantes.</span><span class="sxs-lookup"><span data-stu-id="5f0da-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="5f0da-258">Você precisa de uma solução alternativa para configurar um endereço IP virtual a fim de alcançar o recurso de cluster na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5f0da-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="5f0da-259">O Azure tem um balanceador de carga interno no serviço Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5f0da-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="5f0da-260">Com o balanceador de carga interno, os clientes alcançam o cluster pelo endereço IP virtual do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="5f0da-261">Você precisa implantar o balanceador de carga interno no grupo de recursos que contém os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="5f0da-262">Em seguida, configure todas as regras necessárias de encaminhamento de porta com as portas de investigação do balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="5f0da-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="5f0da-263">Os clientes podem se conectar por meio do nome de host virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="5f0da-264">O servidor DNS resolve o endereço IP do cluster e o balanceador de carga interno trata da porta que encaminha para o nó ativo do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="5f0da-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver de alta disponibilidade na Azure IaaS (Infraestrutura como um serviço)</span><span class="sxs-lookup"><span data-stu-id="5f0da-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="5f0da-266">Para obter a alta disponibilidade do SAP, como no caso de componentes de software SAP, você precisará proteger os componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f0da-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="5f0da-267">Instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-267">SAP Application Server instance</span></span>
* <span data-ttu-id="5f0da-268">Instância ASCS/SCS SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="5f0da-269">Servidor DBMS</span><span class="sxs-lookup"><span data-stu-id="5f0da-269">DBMS server</span></span>

<span data-ttu-id="5f0da-270">Para obter mais informações sobre como proteger os componentes SAP em cenários de alta disponibilidade, consulte [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="5f0da-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="5f0da-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Servidor de Aplicativos SAP de Alta Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5f0da-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="5f0da-272">Normalmente, não é necessária uma solução específica de alta disponibilidade para Servidor de Aplicativos SAP e instâncias de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="5f0da-273">Você atinge alta disponibilidade por redundância e configura várias instâncias de caixa de diálogo em diferentes Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="5f0da-274">Você deve ter pelo menos duas instâncias do aplicativo SAP instaladas em duas Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Figura 4: Servidor de Aplicativos SAP de alta disponibilidade][sap-ha-guide-figure-2000]

<span data-ttu-id="5f0da-276">_**Figura 4:** Servidor de Aplicativos SAP de alta disponibilidade_</span><span class="sxs-lookup"><span data-stu-id="5f0da-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="5f0da-277">Você deve colocar todas as máquinas virtuais que hospedam instâncias do Servidor de Aplicativos SAP no mesmo conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="5f0da-278">Um conjunto de disponibilidade do Azure garante que:</span><span class="sxs-lookup"><span data-stu-id="5f0da-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="5f0da-279">Todas as máquinas virtuais são parte do mesmo domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="5f0da-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="5f0da-280">Por exemplo, um domínio de atualização faz com que as máquinas virtuais não sejam atualizadas ao mesmo tempo durante o tempo de inatividade de manutenção planejada.</span><span class="sxs-lookup"><span data-stu-id="5f0da-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="5f0da-281">Todas as máquinas virtuais são parte do mesmo domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="5f0da-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="5f0da-282">Por exemplo, um domínio de falha faz com que as máquinas virtuais sejam implantadas de forma que nenhum ponto único de falha afete a disponibilidade de todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="5f0da-283">Saiba mais sobre como [gerenciar a disponibilidade de máquinas virtuais][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="5f0da-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="5f0da-284">Somente disco não gerenciado: Como a conta de armazenamento do Azure é um possível ponto único de falha, é importante ter pelo menos duas contas de armazenamento do Azure, nas quais pelo menos duas máquinas virtuais estejam distribuídas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="5f0da-285">Em uma configuração ideal, os discos de cada máquina virtual que está executando uma instância de diálogo SAP deveria ser implantada em uma conta de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="5f0da-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="5f0da-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instância do SAP ASCS/SCS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5f0da-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="5f0da-287">A Figura 5 é um exemplo de instância do SAP ASCS/SCS de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Figura 5: instância do SAP ASCS/SCS de alta disponibilidade][sap-ha-guide-figure-2001]

<span data-ttu-id="5f0da-289">_**Figura 5:** instância do SAP ASCS/SCS de alta disponibilidade_</span><span class="sxs-lookup"><span data-stu-id="5f0da-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="5f0da-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidade da Instância do SAP ASCS/SCS com o Clustering de Failover do Windows Server no Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="5f0da-291">Comparados a implantações de nuvem privada ou bare metal, as Máquinas Virtuais do Azure exigem etapas adicionais para configurar o Windows Server Failover Clustering.</span><span class="sxs-lookup"><span data-stu-id="5f0da-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="5f0da-292">Para criar um cluster de failover do Windows, você precisará de um Disco de Cluster Compartilhado, vários endereços IP e nomes de host virtuais e um balanceador de carga interno do Azure para clustering da instância do SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5f0da-293">Abordaremos isso em mais detalhes mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-293">We discuss this in more detail later in the article.</span></span>

![Figura 6: configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure usando SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="5f0da-295">_**Figura 6:** configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure com SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="5f0da-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Instância do DBMS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5f0da-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="5f0da-297">O DBMS também é um ponto único de contato em um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="5f0da-298">Você precisa protegê-lo usando uma solução de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="5f0da-299">A Figura 7 mostra uma solução de alta disponibilidade Always On do SQL Server no Clustering de Failover do Windows Server e no balanceador interno de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="5f0da-300">O AlwaysOn do SQL Server replica os arquivos de log e dados do DBMS usando sua própria replicação DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="5f0da-301">Nesse caso, você não precisa de discos compartilhados de cluster, o que simplifica toda a configuração.</span><span class="sxs-lookup"><span data-stu-id="5f0da-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Figura 7: exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server][sap-ha-guide-figure-2003]

<span data-ttu-id="5f0da-303">_**Figura 7:** exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server_</span><span class="sxs-lookup"><span data-stu-id="5f0da-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="5f0da-304">Para saber mais sobre o clustering do SQL Server no Azure usando o modelo de implantação do Azure Resource Manager, confira estes artigos:</span><span class="sxs-lookup"><span data-stu-id="5f0da-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="5f0da-305">[Configure o grupo de disponibilidade Always On em Máquinas Virtuais do Azure manualmente usando o Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="5f0da-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="5f0da-306">[Configurar um balanceador interno de carga do Azure para um grupo de disponibilidade Always On no Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="5f0da-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="5f0da-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Cenários de implantação de alta disponibilidade de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="5f0da-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="5f0da-308">Cenário de implantação usando o Modelo Arquitetônico 1</span><span class="sxs-lookup"><span data-stu-id="5f0da-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="5f0da-309">A Figura 8 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5f0da-310">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5f0da-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5f0da-311">Um cluster dedicado é usado para a instância SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="5f0da-312">Um cluster dedicado é usado para a instância DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="5f0da-313">Instâncias do Servidor de Aplicativos SAP são implantadas em suas próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Figura 8: Modelo Arquitetônico 1 de alta disponibilidade de SAP, com cluster dedicado para ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

<span data-ttu-id="5f0da-315">_**Figura 8:** Modelo Arquitetônico 1 de alta disponibilidade de SAP, com clusters dedicados para ASCS/SCS e DBMS_</span><span class="sxs-lookup"><span data-stu-id="5f0da-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="5f0da-316">Cenário de implantação usando o Modelo Arquitetônico 2</span><span class="sxs-lookup"><span data-stu-id="5f0da-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="5f0da-317">A Figura 9 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="5f0da-318">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5f0da-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5f0da-319">Um cluster dedicado é usado para **ambas** a instância SAP ASCS/SCS e o DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="5f0da-320">Instâncias do Servidor de Aplicativos SAP são implantados em VMs próprias dedicadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Figura 9: Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="5f0da-322">_**Figura 9:** Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS_</span><span class="sxs-lookup"><span data-stu-id="5f0da-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="5f0da-323">Cenário de implantação usando o Modelo Arquitetônico 3</span><span class="sxs-lookup"><span data-stu-id="5f0da-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="5f0da-324">A Figura 10 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **dois** sistemas SAP, com &lt;SID1&gt; e &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="5f0da-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="5f0da-325">Esse cenário é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5f0da-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="5f0da-326">Um cluster dedicado é usado para **ambas** as instâncias SID1 de SAP ASCS/SCS *e* SID2 de SAP ASCS/SCS (um cluster).</span><span class="sxs-lookup"><span data-stu-id="5f0da-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="5f0da-327">Um cluster dedicado é usado para SID1 e outro para SID2 de DBMS (dois clusters).</span><span class="sxs-lookup"><span data-stu-id="5f0da-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="5f0da-328">Instâncias do Servidor de Aplicativos SAP para o SID1 do Sistema SAP são implantadas em suas próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="5f0da-329">Instâncias do Servidor de Aplicativos SAP para o SID2 do Sistema SAP são implantadas em suas próprias VMs dedicadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Figura 10: Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS][sap-ha-guide-figure-6003]

<span data-ttu-id="5f0da-331">_**Figura 10:** Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="5f0da-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="5f0da-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Preparar a infraestrutura</span><span class="sxs-lookup"><span data-stu-id="5f0da-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="5f0da-333">Preparar a infraestrutura para o Modelo Arquitetônico 1</span><span class="sxs-lookup"><span data-stu-id="5f0da-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="5f0da-334">Os modelos do Azure Resource Manager para SAP ajudam a simplificar a implantação dos recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="5f0da-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="5f0da-335">Os modelos de três camadas no Azure Resource Manager também dão suporte a cenários de alta disponibilidade, tal como o Modelo Arquitetônico 1, que tem dois clusters.</span><span class="sxs-lookup"><span data-stu-id="5f0da-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="5f0da-336">Cada cluster é um ponto único de falha de SAP para SAP ASCS/SCS e DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="5f0da-337">É aqui que você pode obter os modelos do Azure Resource Manager para o cenário de exemplo descrito neste artigo:</span><span class="sxs-lookup"><span data-stu-id="5f0da-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="5f0da-338">Imagem do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5f0da-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="5f0da-339">Imagem do Marketplace do Azure usando Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5f0da-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="5f0da-340">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="5f0da-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="5f0da-341">Imagem personalizada usando Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5f0da-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="5f0da-342">Para preparar a infraestrutura para o Modelo Arquitetônico 1:</span><span class="sxs-lookup"><span data-stu-id="5f0da-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="5f0da-343">No Portal do Azure, na folha **Parâmetros**, na caixa **SYSTEMAVAILABILITY**, selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Figura 11: definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager][sap-ha-guide-figure-3000]

<span data-ttu-id="5f0da-345">_**Figura 11:** definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager_</span><span class="sxs-lookup"><span data-stu-id="5f0da-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="5f0da-346">Os modelos criam:</span><span class="sxs-lookup"><span data-stu-id="5f0da-346">The templates create:</span></span>

  * <span data-ttu-id="5f0da-347">**Máquinas virtuais**:</span><span class="sxs-lookup"><span data-stu-id="5f0da-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="5f0da-348">Máquinas virtuais do Servidor de Aplicativos SAP: <*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="5f0da-349">Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="5f0da-350">Cluster DBMS: <*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="5f0da-351">**Placas de rede para todas as máquinas virtuais, com endereços IP associados**:</span><span class="sxs-lookup"><span data-stu-id="5f0da-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="5f0da-352"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="5f0da-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="5f0da-354"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="5f0da-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="5f0da-355">**Contas de armazenamento do Azure (apenas discos não gerenciados)**</span><span class="sxs-lookup"><span data-stu-id="5f0da-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="5f0da-356">**Grupos de Disponibilidade** para:</span><span class="sxs-lookup"><span data-stu-id="5f0da-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="5f0da-357">Máquinas virtuais do Servidor de Aplicativos do SAP: <*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="5f0da-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="5f0da-358">Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="5f0da-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="5f0da-359">Máquinas virtuais de cluster DBMS: <*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="5f0da-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="5f0da-360">**Balanceador de carga interno do Azure**:</span><span class="sxs-lookup"><span data-stu-id="5f0da-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="5f0da-361">Com todas as portas para a instância ASCS/SCS e endereço IP <*SAPSystemSID*>-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5f0da-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="5f0da-362">Com todas as portas para o DBMS do SQL Server e endereço IP <*SAPSystemSID*>-lb-db</span><span class="sxs-lookup"><span data-stu-id="5f0da-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="5f0da-363">**Grupo de segurança de rede**: <*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="5f0da-364">Com uma porta de protocolo RDP externa aberta para o <*SAPSystemSID*>-ascs-0 virtual machine</span><span class="sxs-lookup"><span data-stu-id="5f0da-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-365">Todos os endereços IP das placas de rede e dos balanceadores de carga interno do Azure são **dinâmicos** por padrão.</span><span class="sxs-lookup"><span data-stu-id="5f0da-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="5f0da-366">Altere-os para endereços IP **Estáticos**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="5f0da-367">Descrevemos como fazer isso posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="5f0da-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Implantar máquinas virtuais com conectividade de rede corporativa (entre locais) para uso na produção</span><span class="sxs-lookup"><span data-stu-id="5f0da-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="5f0da-369">Para sistemas SAP de produção, implante máquinas virtuais do Azure com [conectividade de rede corporativa (entre instalações)][planning-guide-2.2] usando o VPN Site a Site ou o ExpressRoute do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-370">Você pode usar a instância da Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="5f0da-371">A rede virtual e a sub-rede já foram criadas e preparadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="5f0da-372">No Portal do Azure, na folha **Parâmetros**, na caixa **NEWOREXISTINGSUBNET**, selecione **existente**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="5f0da-373">Na caixa **SUBNETID**, adicione a cadeia de caracteres completa da sua SubnetID da rede do Azure preparada na qual você planeja implantar suas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="5f0da-374">Para obter uma lista de todas as sub-redes da rede do Azure, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5f0da-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="5f0da-375">O campo **ID** mostra o **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="5f0da-376">Para obter uma lista de todos os valores **SUBNETID**, execute este comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5f0da-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="5f0da-377">O **SUBNETID** tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5f0da-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="5f0da-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implantar instâncias de SAP somente na nuvem para teste e demonstração</span><span class="sxs-lookup"><span data-stu-id="5f0da-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="5f0da-379">Você pode implantar o sistema SAP de alta disponibilidade em um modelo de implantação somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5f0da-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="5f0da-380">Esse tipo de implantação é principalmente útil para casos de uso de demonstração e teste.</span><span class="sxs-lookup"><span data-stu-id="5f0da-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="5f0da-381">Ele não é adequado para casos de uso de produção.</span><span class="sxs-lookup"><span data-stu-id="5f0da-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="5f0da-382">No Portal do Azure, na folha **Parâmetros**, na caixa **NEWOREXISTINGSUBNET**, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="5f0da-383">Deixe o campo **SUBNETID** vazio.</span><span class="sxs-lookup"><span data-stu-id="5f0da-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="5f0da-384">O modelo do Resource Manager de SAP cria automaticamente a rede virtual e a sub-rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-385">Você também precisa implantar pelo menos uma máquina virtual dedicada para o Active Directory e DNS na mesma instância de rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="5f0da-386">O modelo não cria essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="5f0da-387">Preparar a infraestrutura para o Modelo Arquitetônico 2</span><span class="sxs-lookup"><span data-stu-id="5f0da-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="5f0da-388">Você pode usar esse modelos do Azure Resource Manager para SAP para ajudar a simplificar a implantação dos recursos de infraestrutura necessários para o Modelo Arquitetônico 2 de SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="5f0da-389">Aqui é onde você pode obter os modelos do Azure Resource Manager para esse cenário de implantação:</span><span class="sxs-lookup"><span data-stu-id="5f0da-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="5f0da-390">Imagem do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5f0da-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="5f0da-391">Imagem do Marketplace do Azure usando Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5f0da-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="5f0da-392">Imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="5f0da-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="5f0da-393">Imagem personalizada usando Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5f0da-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="5f0da-394">Preparar a infraestrutura para o Modelo Arquitetônico 3</span><span class="sxs-lookup"><span data-stu-id="5f0da-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="5f0da-395">Você pode preparar a infraestrutura e configurar SAP para **vários SID**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="5f0da-396">Por exemplo, você pode adicionar uma instância SAP ASCS/SCS adicional em uma configuração de cluster *existente*.</span><span class="sxs-lookup"><span data-stu-id="5f0da-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="5f0da-397">Para obter mais informações, consulte [Configurar uma instância adicional do SAP ASCS/SCS em uma configuração de cluster existente para criar uma configuração de vários SID de SAP no Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="5f0da-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="5f0da-398">Se você quiser criar um novo cluster com múltiplos SID, use os [modelos de início rápido de vários SID no GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5f0da-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="5f0da-399">Para criar um novo cluster de vários SID, você precisa implantar os três modelos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f0da-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="5f0da-400">Modelo de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="5f0da-401">Modelo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="5f0da-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="5f0da-402">Modelo dos servidores de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5f0da-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="5f0da-403">As seções a seguir têm mais detalhes sobre os modelos e os parâmetros que você precisa fornecer nos modelos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="5f0da-404"><a name="ASCS-SCS-template"></a> Modelo de ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="5f0da-405">O modelo de ASCS/SCS implanta duas máquinas virtuais que podem ser usadas para criar um cluster de failover do Windows Server que hospeda várias instâncias de ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="5f0da-406">Para configurar o modelo de vários SID de ASCS/SCS, no [modelo de vários SID de ASCS/SCS][sap-templates-3-tier-multisid-xscs-marketplace-image] ou [modelo de vários SID de ASCS/SCS usando Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], insira valores para os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5f0da-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="5f0da-407">**Prefixo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-407">**Resource Prefix**.</span></span>  <span data-ttu-id="5f0da-408">Defina o prefixo do recurso, que é usado para prefixar todos os recursos que são criados durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="5f0da-409">Como os recursos não pertencem apenas a um sistema SAP, o prefixo do recurso não é o SID de um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="5f0da-410">O prefixo deve ter entre **três e seis caracteres**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="5f0da-411">**Tipo de Pilha**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-411">**Stack Type**.</span></span> <span data-ttu-id="5f0da-412">Selecione o tipo de pilha do sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="5f0da-413">Dependendo do tipo de pilha, o Azure Load Balancer tem um (ABAP ou Java apenas) ou dois (ABAP+Java) endereços IP privados por sistema de SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="5f0da-414">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-414">**OS Type**.</span></span> <span data-ttu-id="5f0da-415">Selecione o sistema operacional das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5f0da-416">**Contagem do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-416">**SAP System Count**.</span></span> <span data-ttu-id="5f0da-417">Selecione o número de sistemas de SAP que você deseja instalar neste cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="5f0da-418">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-418">**System Availability**.</span></span> <span data-ttu-id="5f0da-419">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-419">Select **HA**.</span></span>
  -  <span data-ttu-id="5f0da-420">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5f0da-421">Cria um novo usuário que pode ser usado para se conectar no computador.</span><span class="sxs-lookup"><span data-stu-id="5f0da-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5f0da-422">**Sub-rede Nova ou Existente**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="5f0da-423">Define se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="5f0da-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="5f0da-424">Se você já tiver uma rede virtual conectada à sua rede local, selecione a rede **existente**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="5f0da-425">**ID da Sub-rede**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-425">**Subnet Id**.</span></span> <span data-ttu-id="5f0da-426">Defina a ID da sub-rede à qual as máquinas virtuais devem se conectar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="5f0da-427">Selecione a sub-rede da sua VPN (rede privada virtual) ou rede virtual ExpressRoute para conectar a máquina virtual à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="5f0da-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="5f0da-428">A ID geralmente tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5f0da-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="5f0da-429">/subscriptions/<*ID da assinatura*>/resourceGroups/<*nome do grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nome de rede virtual*>/subnets/<*nome de sub-rede*></span><span class="sxs-lookup"><span data-stu-id="5f0da-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="5f0da-430">O modelo implanta uma instância do Azure Load Balancer que dá suporte a vários sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="5f0da-431">As instâncias ASCS são configuradas para o número de instância 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="5f0da-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="5f0da-432">As instâncias SCS são configuradas para o número de instância 01, 11, 21...</span><span class="sxs-lookup"><span data-stu-id="5f0da-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="5f0da-433">As instâncias ASCS ERS (Enqueue Replication Server) (somente Linux) são configuradas para o número de instância 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="5f0da-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="5f0da-434">As instâncias SCS ERS (somente Linux) são configuradas para o número de instância 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="5f0da-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="5f0da-435">O balanceador de carga contém 1 (2 para Linux) VIPs, 1x VIP para ASCS/SCS e 1x VIP para ERS (somente no Linux).</span><span class="sxs-lookup"><span data-stu-id="5f0da-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="5f0da-436">A lista a seguir contém todas as regras de balanceamento de carga (em que x é o número do sistema SAP, por exemplo, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="5f0da-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5f0da-437">Portas específicas do Windows para cada o sistema SAP: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="5f0da-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="5f0da-438">Portas ASCS (número de instância x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="5f0da-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="5f0da-439">Portas SCS (número de instância x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="5f0da-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="5f0da-440">Portas ASCS ERS no Linux (número de instância x2): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="5f0da-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="5f0da-441">Portas SCS ERS no Linux (número de instância x3): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="5f0da-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="5f0da-442">O balanceador de carga será configurado para usar as seguintes portas de investigação (em que x é o número do sistema SAP, por exemplo, 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="5f0da-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="5f0da-443">Porta de investigação do balanceador interno de carga ASCS/SCS: 620x0</span><span class="sxs-lookup"><span data-stu-id="5f0da-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="5f0da-444">Porta de investigação do balanceador interno de carga ERS (somente Linux): 621x2</span><span class="sxs-lookup"><span data-stu-id="5f0da-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="5f0da-445"><a name="database-template"></a> Modelo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="5f0da-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="5f0da-446">O modelo de banco de dados implanta uma ou duas máquinas virtuais que você pode usar para instalar o RDBMS (sistema de gerenciamento de banco de dados relacional) para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="5f0da-447">Se, por exemplo, você implantou um modelo ASCS/SCS para cinco sistemas SAP, precisará implantar esse modelo cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="5f0da-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5f0da-448">Para configurar o modelo de vários SID de banco de dados, no [modelo de vários SID de banco de dados][sap-templates-3-tier-multisid-db-marketplace-image] ou [modelo de vários SID de banco de dados usando Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], insira valores para os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5f0da-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5f0da-449">**ID do sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-449">**Sap System Id**.</span></span> <span data-ttu-id="5f0da-450">Insira a ID do sistema SAP do sistema SAP que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5f0da-451">A ID será usada como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="5f0da-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5f0da-452">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-452">**Os Type**.</span></span> <span data-ttu-id="5f0da-453">Selecione o sistema operacional das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5f0da-454">**Dbtype**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-454">**Dbtype**.</span></span> <span data-ttu-id="5f0da-455">Selecione o tipo do banco de dados que você deseja instalar no cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="5f0da-456">Selecione **SQL** se você deseja instalar o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f0da-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="5f0da-457">Selecione **HANA** se você planeja instalar SAP HANA nas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="5f0da-458">Selecione o tipo de sistema operacional correto: **Windows** para SQL e uma distribuição Linux para HANA.</span><span class="sxs-lookup"><span data-stu-id="5f0da-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="5f0da-459">O Azure Load Balancer que está conectado às máquinas virtuais será configurado para suporte ao tipo de banco de dados selecionado:</span><span class="sxs-lookup"><span data-stu-id="5f0da-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="5f0da-460">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-460">**SQL**.</span></span> <span data-ttu-id="5f0da-461">O balanceador de carga balanceará a carga da porta 1433.</span><span class="sxs-lookup"><span data-stu-id="5f0da-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="5f0da-462">Use essa porta para a instalação do SQL Server Always On.</span><span class="sxs-lookup"><span data-stu-id="5f0da-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="5f0da-463">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-463">**HANA**.</span></span> <span data-ttu-id="5f0da-464">O balanceador de carga balanceará a carga das portas 35015 e 35017.</span><span class="sxs-lookup"><span data-stu-id="5f0da-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="5f0da-465">Instale o SAP HANA com o número de instância **50**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="5f0da-466">O balanceador de carga usará a porta de investigação 62550.</span><span class="sxs-lookup"><span data-stu-id="5f0da-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="5f0da-467">**Tamanho do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-467">**Sap System Size**.</span></span> <span data-ttu-id="5f0da-468">Defina o número de SAPS que o novo sistema fornecerá.</span><span class="sxs-lookup"><span data-stu-id="5f0da-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="5f0da-469">Se você não tiver certeza de quantos SAPs o sistema precisará, pergunte ao seu Parceiro de Tecnologia SAP ou Integrador de Sistemas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5f0da-470">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-470">**System Availability**.</span></span> <span data-ttu-id="5f0da-471">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-471">Select **HA**.</span></span>
  -  <span data-ttu-id="5f0da-472">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5f0da-473">Cria um novo usuário que pode ser usado para se conectar no computador.</span><span class="sxs-lookup"><span data-stu-id="5f0da-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5f0da-474">**ID da Sub-rede**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-474">**Subnet Id**.</span></span> <span data-ttu-id="5f0da-475">Insira a ID da sub-rede que você usou durante a implantação do modelo ASCS/SCS ou a ID da sub-rede que foi criada como parte da implantação do modelo ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="5f0da-476"><a name="application-servers-template"></a> Modelo dos servidores de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5f0da-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="5f0da-477">O modelo de servidores de aplicativo implanta duas ou mais máquinas virtuais que podem ser usadas como instâncias do Servidor de Aplicativos SAP para um sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="5f0da-478">Se, por exemplo, você implantou um modelo ASCS/SCS para cinco sistemas SAP, precisará implantar esse modelo cinco vezes.</span><span class="sxs-lookup"><span data-stu-id="5f0da-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="5f0da-479">Para configurar o modelo de vários SID de servidores de aplicativos, no [modelo de vários SID de servidores de aplicativos][sap-templates-3-tier-multisid-apps-marketplace-image] ou [modelo de vários SID de servidores de aplicativos usando Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], insira valores para os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5f0da-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="5f0da-480">**ID do sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-480">**Sap System Id**.</span></span> <span data-ttu-id="5f0da-481">Insira a ID do sistema SAP do sistema SAP que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="5f0da-482">A ID será usada como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="5f0da-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="5f0da-483">**Tipo de sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-483">**Os Type**.</span></span> <span data-ttu-id="5f0da-484">Selecione o sistema operacional das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="5f0da-485">**Tamanho do Sistema SAP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-485">**Sap System Size**.</span></span> <span data-ttu-id="5f0da-486">O número de SAPS que o novo sistema fornecerá.</span><span class="sxs-lookup"><span data-stu-id="5f0da-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="5f0da-487">Se você não tiver certeza de quantos SAPs o sistema precisará, pergunte ao seu Parceiro de Tecnologia SAP ou Integrador de Sistemas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="5f0da-488">**Disponibilidade do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-488">**System Availability**.</span></span> <span data-ttu-id="5f0da-489">Selecione **HA**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-489">Select **HA**.</span></span>
  -  <span data-ttu-id="5f0da-490">**Nome de Usuário e Senha de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="5f0da-491">Cria um novo usuário que pode ser usado para se conectar no computador.</span><span class="sxs-lookup"><span data-stu-id="5f0da-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="5f0da-492">**ID da Sub-rede**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-492">**Subnet Id**.</span></span> <span data-ttu-id="5f0da-493">Insira a ID da sub-rede que você usou durante a implantação do modelo ASCS/SCS ou a ID da sub-rede que foi criada como parte da implantação do modelo ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="5f0da-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="5f0da-495">Em nosso exemplo, o espaço de endereço da rede virtual do Azure é 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="5f0da-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="5f0da-496">Há uma sub-rede chamada **Subnet**, com um intervalo de endereços de 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="5f0da-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="5f0da-497">Todas as máquinas virtuais e balanceadores de carga internos são implantados nessa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f0da-498">Não faça nenhuma alteração nas configurações de rede dentro do sistema operacional convidado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="5f0da-499">Isso inclui endereços IP, servidores DNS e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5f0da-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="5f0da-500">Configure todas as configurações de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="5f0da-501">O serviço do protocolo DHCP propaga as configurações.</span><span class="sxs-lookup"><span data-stu-id="5f0da-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="5f0da-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Endereços IP de DNS</span><span class="sxs-lookup"><span data-stu-id="5f0da-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="5f0da-503">Para definir os endereços IP de DNS necessários, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="5f0da-504">No Portal do Azure, na folha de **Servidores DNS**, verifique se sua opção de rede virtual **Servidores DNS** está definida para **DNS Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="5f0da-505">Selecione suas configurações com base no seu tipo de rede.</span><span class="sxs-lookup"><span data-stu-id="5f0da-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="5f0da-506">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f0da-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="5f0da-507">[Conectividade de Rede Corporativa (Entre Instalações)][planning-guide-2.2]: adicione os endereços IP dos servidores DNS locais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="5f0da-508">Você pode estender os servidores DNS locais às máquinas virtuais que estão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="5f0da-509">Nesse cenário, você pode adicionar os endereços IP das máquinas virtuais do Azure nos quais executa o serviço DNS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="5f0da-510">[Implantação somente em nuvem][planning-guide-2.1]: implantar uma máquina virtual adicional na mesma instância de Rede Virtual que serve como servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="5f0da-511">Adicione os endereços IP das máquinas virtuais do Azure que você configurou para executar o serviço DNS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Figura 12: Configurar servidores DNS da Rede Virtual do Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="5f0da-513">_**Figura 12:** Configurar servidores DNS da Rede Virtual do Azure_</span><span class="sxs-lookup"><span data-stu-id="5f0da-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="5f0da-514">Se você mudar os endereços IP dos servidores DNS, será preciso reinicializar as máquinas virtuais do Azure de modo a aplicar a alteração e propagar os novos servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="5f0da-515">Em nosso exemplo, o serviço DNS está instalado e configurado nas seguintes máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="5f0da-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="5f0da-516">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-516">Virtual machine role</span></span> | <span data-ttu-id="5f0da-517">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-517">Virtual machine host name</span></span> | <span data-ttu-id="5f0da-518">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="5f0da-518">Network card name</span></span> | <span data-ttu-id="5f0da-519">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="5f0da-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f0da-520">Primeiro servidor DNS</span><span class="sxs-lookup"><span data-stu-id="5f0da-520">First DNS server</span></span> |<span data-ttu-id="5f0da-521">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-521">domcontr-0</span></span> |<span data-ttu-id="5f0da-522">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="5f0da-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="5f0da-523">10.0.0.10</span></span> |
| <span data-ttu-id="5f0da-524">Segundo servidor DNS</span><span class="sxs-lookup"><span data-stu-id="5f0da-524">Second DNS server</span></span> |<span data-ttu-id="5f0da-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-525">domcontr-1</span></span> |<span data-ttu-id="5f0da-526">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="5f0da-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="5f0da-527">10.0.0.11</span></span> |

### <span data-ttu-id="5f0da-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Nomes de host e endereços IP estáticos para a instância clusterizada do SAP ASCS/SCS e a instância clusterizada do DBMS</span><span class="sxs-lookup"><span data-stu-id="5f0da-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="5f0da-529">Para implantação local, você precisa destes endereços IP e nomes de host reservados:</span><span class="sxs-lookup"><span data-stu-id="5f0da-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="5f0da-530">Função de nome de host virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-530">Virtual host name role</span></span> | <span data-ttu-id="5f0da-531">Nome de host virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-531">Virtual host name</span></span> | <span data-ttu-id="5f0da-532">Endereço IP estático virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f0da-533">Nome de host virtual do primeiro cluster SAP ASCS/SCS (para gerenciamento de cluster)</span><span class="sxs-lookup"><span data-stu-id="5f0da-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="5f0da-534">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="5f0da-534">pr1-ascs-vir</span></span> |<span data-ttu-id="5f0da-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="5f0da-535">10.0.0.42</span></span> |
| <span data-ttu-id="5f0da-536">Nome de host virtual da instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="5f0da-537">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="5f0da-537">pr1-ascs-sap</span></span> |<span data-ttu-id="5f0da-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5f0da-538">10.0.0.43</span></span> |
| <span data-ttu-id="5f0da-539">Nome de host virtual do segundo cluster SAP DBMS (gerenciamento de cluster)</span><span class="sxs-lookup"><span data-stu-id="5f0da-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="5f0da-540">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="5f0da-540">pr1-dbms-vir</span></span> |<span data-ttu-id="5f0da-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="5f0da-541">10.0.0.32</span></span> |

<span data-ttu-id="5f0da-542">Quando você criar o cluster, crie os nomes de host virtual **pr1-ascs-vir** e **pr1-dbms- vir** e os endereços IP associados que gerenciam o cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="5f0da-543">Para obter informações sobre como fazer isso, consulte [Coletar nós de cluster em uma configuração de cluster][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="5f0da-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="5f0da-544">Você pode criar manualmente os outros dois nomes de host virtuais, **pr1-ascs-sap** e **pr1-dbms-sap**, e os endereços IP associados no servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="5f0da-545">A instância clusterizada da instância SAP ASCS/SCS e a instância clusterizada do DBMS usam esses recursos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="5f0da-546">Para obter informações sobre como fazer isso, consulte [Criar um nome de host virtual para uma instância SAP ASCS/SCS clusterizada][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="5f0da-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="5f0da-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Definir endereços IP estáticos para as máquinas virtuais de SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="5f0da-548">Depois de implantar as máquinas virtuais para usar no seu cluster, você precisará definir endereços IP estáticos para todas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="5f0da-549">Faça isso na configuração da Rede Virtual do Azure e não no sistema operacional convidado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="5f0da-550">No Portal do Azure, selecione **Grupo de Recursos** > **Placa de Rede** > **Configurações** > **Endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="5f0da-551">Na folha **Endereços IP**, em **Atribuição**, selecione **Estático**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="5f0da-552">Na caixa **Endereço IP**, digite o endereço IP que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5f0da-553">Se você mudar o endereço IP da placa de rede, será preciso reinicializar as máquinas virtuais do Azure para aplicar a alteração.</span><span class="sxs-lookup"><span data-stu-id="5f0da-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Figura 13: Definir endereços IP estáticos para a placa de rede de cada máquina virtual][sap-ha-guide-figure-3002]

  <span data-ttu-id="5f0da-555">_**Figura 13:** Definir endereços IP estáticos para a placa de rede de cada máquina virtual_</span><span class="sxs-lookup"><span data-stu-id="5f0da-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="5f0da-556">Repita essa etapa para todas as interfaces de rede, isto é, para todas as máquinas virtuais, incluindo as máquinas virtuais que você deseja usar para seu serviço DNS/Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f0da-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="5f0da-557">Em nosso exemplo, temos estas máquinas virtuais e endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="5f0da-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="5f0da-558">Função da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-558">Virtual machine role</span></span> | <span data-ttu-id="5f0da-559">Nome do host de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5f0da-559">Virtual machine host name</span></span> | <span data-ttu-id="5f0da-560">Nome da placa de rede</span><span class="sxs-lookup"><span data-stu-id="5f0da-560">Network card name</span></span> | <span data-ttu-id="5f0da-561">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="5f0da-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f0da-562">Primeira instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-562">First SAP Application Server instance</span></span> |<span data-ttu-id="5f0da-563">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-563">pr1-di-0</span></span> |<span data-ttu-id="5f0da-564">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-564">pr1-nic-di-0</span></span> |<span data-ttu-id="5f0da-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="5f0da-565">10.0.0.50</span></span> |
| <span data-ttu-id="5f0da-566">Segunda instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="5f0da-567">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-567">pr1-di-1</span></span> |<span data-ttu-id="5f0da-568">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-568">pr1-nic-di-1</span></span> |<span data-ttu-id="5f0da-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="5f0da-569">10.0.0.51</span></span> |
| <span data-ttu-id="5f0da-570">...</span><span class="sxs-lookup"><span data-stu-id="5f0da-570">...</span></span> |<span data-ttu-id="5f0da-571">...</span><span class="sxs-lookup"><span data-stu-id="5f0da-571">...</span></span> |<span data-ttu-id="5f0da-572">...</span><span class="sxs-lookup"><span data-stu-id="5f0da-572">...</span></span> |<span data-ttu-id="5f0da-573">...</span><span class="sxs-lookup"><span data-stu-id="5f0da-573">...</span></span> |
| <span data-ttu-id="5f0da-574">Última instância do Servidor de Aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="5f0da-575">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="5f0da-575">pr1-di-5</span></span> |<span data-ttu-id="5f0da-576">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="5f0da-576">pr1-nic-di-5</span></span> |<span data-ttu-id="5f0da-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="5f0da-577">10.0.0.55</span></span> |
| <span data-ttu-id="5f0da-578">Primeiro nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5f0da-579">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-579">pr1-ascs-0</span></span> |<span data-ttu-id="5f0da-580">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="5f0da-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="5f0da-581">10.0.0.40</span></span> |
| <span data-ttu-id="5f0da-582">Segundo nó de cluster para a instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5f0da-583">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-583">pr1-ascs-1</span></span> |<span data-ttu-id="5f0da-584">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="5f0da-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="5f0da-585">10.0.0.41</span></span> |
| <span data-ttu-id="5f0da-586">Primeiro nó de cluster para a instância do DBMS</span><span class="sxs-lookup"><span data-stu-id="5f0da-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="5f0da-587">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-587">pr1-db-0</span></span> |<span data-ttu-id="5f0da-588">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="5f0da-588">pr1-nic-db-0</span></span> |<span data-ttu-id="5f0da-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="5f0da-589">10.0.0.30</span></span> |
| <span data-ttu-id="5f0da-590">Segundo nó de cluster para a instância do DBMS</span><span class="sxs-lookup"><span data-stu-id="5f0da-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="5f0da-591">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-591">pr1-db-1</span></span> |<span data-ttu-id="5f0da-592">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="5f0da-592">pr1-nic-db-1</span></span> |<span data-ttu-id="5f0da-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="5f0da-593">10.0.0.31</span></span> |

### <span data-ttu-id="5f0da-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Defina um endereço IP estático para o balanceador interno de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="5f0da-595">O modelo do Azure Resource Manager para SAP cria um balanceador de carga interno do Azure usado para o cluster da instância do ASCS/SCS e para o cluster do DBMS do SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f0da-596">O endereço IP do nome de host virtual do SAP ASCS/SCS é o mesmo que o endereço IP do balanceador de carga interno SAP ASCS/SCS: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="5f0da-597">O endereço IP do nome virtual do DBMS é o mesmo que o endereço IP do balanceador interno de carga do DBMS: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="5f0da-598">Para definir um endereço IP estático para o balanceador interno de carga do Azure:</span><span class="sxs-lookup"><span data-stu-id="5f0da-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="5f0da-599">A implantação inicial define o endereço IP do balanceador de carga interno como **Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="5f0da-600">No Portal do Azure, na folha **Endereços IP**, em **Atribuição**, selecione **Estático**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="5f0da-601">Defina o endereço IP do balanceador interno de carga, **pr1-lb-ascs**, para o endereço IP do nome de host virtual da instância do SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="5f0da-602">Defina o endereço IP do balanceador interno de carga, **pr1-lb-dbms**, para o endereço IP do nome de host virtual da instância do DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Figura 14: Definir endereços IP estáticos para o balanceador de carga interno da instância SAP ASCS/SCS][sap-ha-guide-figure-3003]

  <span data-ttu-id="5f0da-604">_**Figura 14:** Definir endereços IP estáticos para o balanceador de carga interno da instância SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="5f0da-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="5f0da-605">Em nosso exemplo, temos dois balanceadores de carga internos do Azure que têm esses endereços IP estáticos:</span><span class="sxs-lookup"><span data-stu-id="5f0da-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="5f0da-606">Função do balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-606">Azure internal load balancer role</span></span> | <span data-ttu-id="5f0da-607">Nome balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-607">Azure internal load balancer name</span></span> | <span data-ttu-id="5f0da-608">Endereço IP estático</span><span class="sxs-lookup"><span data-stu-id="5f0da-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f0da-609">Balanceador de carga interno da instância SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="5f0da-610">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5f0da-610">pr1-lb-ascs</span></span> |<span data-ttu-id="5f0da-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="5f0da-611">10.0.0.43</span></span> |
| <span data-ttu-id="5f0da-612">Balanceador de carga interno de DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="5f0da-613">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="5f0da-613">pr1-lb-dbms</span></span> |<span data-ttu-id="5f0da-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="5f0da-614">10.0.0.33</span></span> |


### <span data-ttu-id="5f0da-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Regras do balanceamento de carga do ASCS/SCS padrão para o balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5f0da-616">O modelo do Azure Resource Manager de SAP cria as portas de que você precisa:</span><span class="sxs-lookup"><span data-stu-id="5f0da-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="5f0da-617">Uma instância do ASCS ABAP com número de instância padrão **00**</span><span class="sxs-lookup"><span data-stu-id="5f0da-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="5f0da-618">Uma instância do SCS Java com número de instância padrão **01**</span><span class="sxs-lookup"><span data-stu-id="5f0da-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="5f0da-619">Quando você instala sua instância SAP ASCS/SCS, deve usar o número de instância padrão **00** para sua instância ASCS ABAP e o número de instância padrão **01** para sua instância SCS Java.</span><span class="sxs-lookup"><span data-stu-id="5f0da-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="5f0da-620">Em seguida, crie os pontos de extremidade de balanceamento interno de carga necessários para as portas do SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="5f0da-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="5f0da-621">Para criar os pontos de extremidade de balanceamento interno de carga, crie esses pontos de extremidade do balanceamento de carga para as portas do ASCS ABAP do SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="5f0da-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="5f0da-622">Nome da regra do balanceamento de carga/serviço</span><span class="sxs-lookup"><span data-stu-id="5f0da-622">Service/load balancing rule name</span></span> | <span data-ttu-id="5f0da-623">Números de porta padrão</span><span class="sxs-lookup"><span data-stu-id="5f0da-623">Default port numbers</span></span> | <span data-ttu-id="5f0da-624">Portas concretas para (instância do ASCS com número de instância 00) (ERS com 10)</span><span class="sxs-lookup"><span data-stu-id="5f0da-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f0da-625">Enfileirar Servidor / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="5f0da-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="5f0da-626">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-627">3200</span><span class="sxs-lookup"><span data-stu-id="5f0da-627">3200</span></span> |
| <span data-ttu-id="5f0da-628">Servidor de Mensagens ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="5f0da-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="5f0da-629">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-630">3600</span><span class="sxs-lookup"><span data-stu-id="5f0da-630">3600</span></span> |
| <span data-ttu-id="5f0da-631">Mensagem interna ABAP / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5f0da-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="5f0da-632">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-633">3900</span><span class="sxs-lookup"><span data-stu-id="5f0da-633">3900</span></span> |
| <span data-ttu-id="5f0da-634">HTTP do Servidor de Mensagens / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="5f0da-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="5f0da-635">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-636">8100</span><span class="sxs-lookup"><span data-stu-id="5f0da-636">8100</span></span> |
| <span data-ttu-id="5f0da-637">HTTP do SAP para Iniciar Serviço ASCS / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="5f0da-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="5f0da-638">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="5f0da-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5f0da-639">50013</span><span class="sxs-lookup"><span data-stu-id="5f0da-639">50013</span></span> |
| <span data-ttu-id="5f0da-640">HTTPS do SAP para Iniciar Serviço ASCS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="5f0da-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="5f0da-641">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="5f0da-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5f0da-642">50014</span><span class="sxs-lookup"><span data-stu-id="5f0da-642">50014</span></span> |
| <span data-ttu-id="5f0da-643">Enfileirar Replicação / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="5f0da-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="5f0da-644">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="5f0da-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5f0da-645">50016</span><span class="sxs-lookup"><span data-stu-id="5f0da-645">50016</span></span> |
| <span data-ttu-id="5f0da-646">HTTP do SAP para Iniciar Serviço ERS *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="5f0da-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="5f0da-647">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="5f0da-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5f0da-648">51013</span><span class="sxs-lookup"><span data-stu-id="5f0da-648">51013</span></span> |
| <span data-ttu-id="5f0da-649">HTTP do SAP para Iniciar Serviço ERS *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="5f0da-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="5f0da-650">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="5f0da-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5f0da-651">51014</span><span class="sxs-lookup"><span data-stu-id="5f0da-651">51014</span></span> |
| <span data-ttu-id="5f0da-652">RM Win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5f0da-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5f0da-653">5985</span><span class="sxs-lookup"><span data-stu-id="5f0da-653">5985</span></span> |
| <span data-ttu-id="5f0da-654">Compartilhamento de Arquivos *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5f0da-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5f0da-655">445</span><span class="sxs-lookup"><span data-stu-id="5f0da-655">445</span></span> |

<span data-ttu-id="5f0da-656">_**Tabela 1:** números de porta das instâncias do ASCS ABAP do SAP NetWeaver_</span><span class="sxs-lookup"><span data-stu-id="5f0da-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="5f0da-657">Em seguida, crie os pontos de extremidade do balanceamento de carga para as portas do SCS Java do SAP NetWeaver:</span><span class="sxs-lookup"><span data-stu-id="5f0da-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="5f0da-658">Nome da regra do balanceamento de carga/serviço</span><span class="sxs-lookup"><span data-stu-id="5f0da-658">Service/load balancing rule name</span></span> | <span data-ttu-id="5f0da-659">Números de porta padrão</span><span class="sxs-lookup"><span data-stu-id="5f0da-659">Default port numbers</span></span> | <span data-ttu-id="5f0da-660">Portas concretas para (instância do SCS com número de instância 01) (ERS com 11)</span><span class="sxs-lookup"><span data-stu-id="5f0da-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f0da-661">Enfileirar Servidor / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="5f0da-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="5f0da-662">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-663">3201</span><span class="sxs-lookup"><span data-stu-id="5f0da-663">3201</span></span> |
| <span data-ttu-id="5f0da-664">Servidor do Gateway / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="5f0da-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="5f0da-665">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-666">3301</span><span class="sxs-lookup"><span data-stu-id="5f0da-666">3301</span></span> |
| <span data-ttu-id="5f0da-667">Servidor de Mensagens Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="5f0da-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="5f0da-668">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-669">3901</span><span class="sxs-lookup"><span data-stu-id="5f0da-669">3901</span></span> |
| <span data-ttu-id="5f0da-670">HTTP do Servidor de Mensagens / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="5f0da-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="5f0da-671">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="5f0da-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="5f0da-672">8101</span><span class="sxs-lookup"><span data-stu-id="5f0da-672">8101</span></span> |
| <span data-ttu-id="5f0da-673">HTTP do SAP para Iniciar Serviço SCS / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="5f0da-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="5f0da-674">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="5f0da-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5f0da-675">50113</span><span class="sxs-lookup"><span data-stu-id="5f0da-675">50113</span></span> |
| <span data-ttu-id="5f0da-676">HTTPS do SAP para Iniciar Serviço SCS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="5f0da-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="5f0da-677">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="5f0da-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5f0da-678">50114</span><span class="sxs-lookup"><span data-stu-id="5f0da-678">50114</span></span> |
| <span data-ttu-id="5f0da-679">Enfileirar Replicação / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="5f0da-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="5f0da-680">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="5f0da-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="5f0da-681">50116</span><span class="sxs-lookup"><span data-stu-id="5f0da-681">50116</span></span> |
| <span data-ttu-id="5f0da-682">HTTP do SAP para Iniciar Serviço ERS *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="5f0da-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="5f0da-683">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="5f0da-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="5f0da-684">51113</span><span class="sxs-lookup"><span data-stu-id="5f0da-684">51113</span></span> |
| <span data-ttu-id="5f0da-685">HTTP do SAP para Iniciar Serviço ERS *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="5f0da-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="5f0da-686">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="5f0da-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="5f0da-687">51114</span><span class="sxs-lookup"><span data-stu-id="5f0da-687">51114</span></span> |
| <span data-ttu-id="5f0da-688">RM Win *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="5f0da-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="5f0da-689">5985</span><span class="sxs-lookup"><span data-stu-id="5f0da-689">5985</span></span> |
| <span data-ttu-id="5f0da-690">Compartilhamento de Arquivos *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="5f0da-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="5f0da-691">445</span><span class="sxs-lookup"><span data-stu-id="5f0da-691">445</span></span> |

<span data-ttu-id="5f0da-692">_**Tabela 2:** números de porta das instâncias do SCS Java do SAP NetWeaver_</span><span class="sxs-lookup"><span data-stu-id="5f0da-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Figura 15: regras do balanceamento de carga do ASCS/SCS padrão para o Azure Internal Load Balancer][sap-ha-guide-figure-3004]

<span data-ttu-id="5f0da-694">_**Figura 15:** regras do balanceamento de carga do ASCS/SCS padrão para o Azure Internal Load Balancer_</span><span class="sxs-lookup"><span data-stu-id="5f0da-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="5f0da-695">Defina o endereço IP do balanceador de carga **pr1-lb-dbms** como o endereço IP do nome de host virtual da instância do DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="5f0da-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Alterar as regras do balanceamento de carga padrão do ASCS/SCS para o balanceador de carga interno do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0da-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="5f0da-697">Se você quiser usar números diferentes para as instâncias SAP ASCS ou SCS, precisará alterar os nomes e os valores das portas do padrão.</span><span class="sxs-lookup"><span data-stu-id="5f0da-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="5f0da-698">No portal do Azure, selecione **<*SID*>-lb-ascs load balancer** > **Regras de Balanceamento de Carga**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="5f0da-699">Para todas as regras de balanceamento de carga que pertencem à instância do SAP ASCS ou SCS, altere estes valores:</span><span class="sxs-lookup"><span data-stu-id="5f0da-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="5f0da-700">Nome</span><span class="sxs-lookup"><span data-stu-id="5f0da-700">Name</span></span>
  * <span data-ttu-id="5f0da-701">Porta</span><span class="sxs-lookup"><span data-stu-id="5f0da-701">Port</span></span>
  * <span data-ttu-id="5f0da-702">Porta de back-end</span><span class="sxs-lookup"><span data-stu-id="5f0da-702">Back-end port</span></span>

  <span data-ttu-id="5f0da-703">Por exemplo, se você quer alterar o número de instância do ASCS padrão de 00 para 31, precisa fazer as alterações em todas as portas listadas na Tabela 1.</span><span class="sxs-lookup"><span data-stu-id="5f0da-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="5f0da-704">Veja um exemplo de uma atualização para a porta *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="5f0da-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Figura 16: Alterar as regras do balanceamento de carga padrão do ASCS/SCS para o Azure Internal Load Balancer][sap-ha-guide-figure-3005]

  <span data-ttu-id="5f0da-706">_**Figura 16:** alterar as regras do balanceamento de carga padrão do ASCS/SCS para o balanceador interno de carga do Azure_</span><span class="sxs-lookup"><span data-stu-id="5f0da-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="5f0da-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Adicionar máquinas virtuais do Windows ao domínio</span><span class="sxs-lookup"><span data-stu-id="5f0da-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="5f0da-708">Depois de atribuir um endereço IP estático às máquinas virtuais, adicione as máquinas virtuais ao domínio.</span><span class="sxs-lookup"><span data-stu-id="5f0da-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Figura 17: Adicionar uma máquina virtual a um domínio][sap-ha-guide-figure-3006]

<span data-ttu-id="5f0da-710">_**Figura 17:** Adicionar uma máquina virtual a um domínio_</span><span class="sxs-lookup"><span data-stu-id="5f0da-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="5f0da-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Adicionar entradas de registro em ambos os nós de cluster da instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5f0da-712">O Azure Load Balancer tem um balanceador de carga interno que fecha conexões quando elas estão ociosas por determinado período de tempo (um tempo limite de ociosidade).</span><span class="sxs-lookup"><span data-stu-id="5f0da-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="5f0da-713">Os processos de trabalho do SAP em instâncias de caixa de diálogo abrem conexões com o processo de enfileiramento do SAP assim que a primeira solicitação para enfileirar/desenfileirar precisa ser enviada.</span><span class="sxs-lookup"><span data-stu-id="5f0da-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="5f0da-714">Essas conexões geralmente permanecem estabelecidas até que o processo de trabalho ou o processo de enfileiramento seja reiniciado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="5f0da-715">No entanto, se a conexão ficar ociosa por um certo período, o balanceador interno de carga do Azure fechará as conexões.</span><span class="sxs-lookup"><span data-stu-id="5f0da-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="5f0da-716">Isso não é um problema porque o processo de trabalho do SAP restabelece a conexão com o processo de enfileiramento se ele não existe mais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="5f0da-717">Essas atividades são documentadas nos rastreamentos de desenvolvedor dos processos da SAP, mas criam uma grande quantidade de conteúdo extra nesses rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="5f0da-718">É uma boa ideia para alterar o TCP/IP `KeepAliveTime` e `KeepAliveInterval` em ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="5f0da-719">Combine essas alterações nos parâmetros de TCP/IP com parâmetros de perfil do SAP, descritos posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="5f0da-720">Para adicionar entradas de Registro em ambos os nós de cluster da instância SAP ASCS/SCS, primeiro adicione essas entradas de Registro do Windows a ambos os nós de cluster do Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="5f0da-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5f0da-721">Caminho</span><span class="sxs-lookup"><span data-stu-id="5f0da-721">Path</span></span> | <span data-ttu-id="5f0da-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5f0da-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5f0da-723">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="5f0da-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="5f0da-724">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="5f0da-724">Variable type</span></span> |<span data-ttu-id="5f0da-725">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="5f0da-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5f0da-726">Valor</span><span class="sxs-lookup"><span data-stu-id="5f0da-726">Value</span></span> |<span data-ttu-id="5f0da-727">120000</span><span class="sxs-lookup"><span data-stu-id="5f0da-727">120000</span></span> |
| <span data-ttu-id="5f0da-728">Vincular à documentação</span><span class="sxs-lookup"><span data-stu-id="5f0da-728">Link to documentation</span></span> |[<span data-ttu-id="5f0da-729">https://technet.microsoft.com/pt-BR/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="5f0da-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="5f0da-730">_**Tabela 3:** alterar o primeiro parâmetro de TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5f0da-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="5f0da-731">Em seguida, adicione as seguintes entradas de Registro em nós de cluster do Windows para SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="5f0da-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="5f0da-732">Caminho</span><span class="sxs-lookup"><span data-stu-id="5f0da-732">Path</span></span> | <span data-ttu-id="5f0da-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="5f0da-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="5f0da-734">Nome da variável</span><span class="sxs-lookup"><span data-stu-id="5f0da-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="5f0da-735">Tipo de variável</span><span class="sxs-lookup"><span data-stu-id="5f0da-735">Variable type</span></span> |<span data-ttu-id="5f0da-736">REG_DWORD (Decimal)</span><span class="sxs-lookup"><span data-stu-id="5f0da-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="5f0da-737">Valor</span><span class="sxs-lookup"><span data-stu-id="5f0da-737">Value</span></span> |<span data-ttu-id="5f0da-738">120000</span><span class="sxs-lookup"><span data-stu-id="5f0da-738">120000</span></span> |
| <span data-ttu-id="5f0da-739">Vincular à documentação</span><span class="sxs-lookup"><span data-stu-id="5f0da-739">Link to documentation</span></span> |[<span data-ttu-id="5f0da-740">https://technet.microsoft.com/pt-BR/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="5f0da-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="5f0da-741">_**Tabela 4:** alterar o segundo parâmetro de TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5f0da-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="5f0da-742">**Para aplicar as alterações, reinicie ambos os nós de cluster**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="5f0da-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurar um cluster Windows Server Failover Clustering para uma instância do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="5f0da-744">Configurar um cluster do Clustering de Failover do Windows Server para uma instância do SAP ASCS/SCS envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="5f0da-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5f0da-745">Coletar nós de cluster em uma configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="5f0da-746">Configurando a testemunha de compartilhamento de arquivos do cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="5f0da-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Coletar nós de cluster em uma configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="5f0da-748">O Assistente para Adicionar Funções e Recursos adiciona clustering de failover a ambos os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="5f0da-749">Configure o cluster de failover usando o Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="5f0da-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="5f0da-750">No Gerenciador de Cluster de Failover, selecione **Criar Cluster** e adicione apenas o nome do primeiro cluster, do nó A. Não adicione o segundo nó ainda; ele será adicionado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="5f0da-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Figura 18: Adicionar o nome de servidor ou máquina virtual do primeiro nó de cluster][sap-ha-guide-figure-3007]

  <span data-ttu-id="5f0da-752">_**Figura 18:** Adicionar o nome de servidor ou máquina virtual do primeiro nó de cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="5f0da-753">Insira o nome de rede (nome de host virtual) do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Figura 19: digite o nome do cluster][sap-ha-guide-figure-3008]

  <span data-ttu-id="5f0da-755">_**Figura 19:** digite o nome do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="5f0da-756">Depois de criar o cluster, execute um teste de validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![Figura 20: Executar a verificação de validação de cluster][sap-ha-guide-figure-3009]

  <span data-ttu-id="5f0da-758">_**Figura 20:** Executar a verificação de validação de cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="5f0da-759">Você pode ignorar os avisos sobre discos nessa altura do processo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="5f0da-760">Você adicionará uma testemunha de compartilhamento de arquivo e discos compartilhados do SIOS mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5f0da-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="5f0da-761">Neste estágio, você não precisa se preocupar em ter um quorum.</span><span class="sxs-lookup"><span data-stu-id="5f0da-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Figura 21: Nenhum disco de quorum é encontrado][sap-ha-guide-figure-3010]

  <span data-ttu-id="5f0da-763">_**Figura 21:** Nenhum disco de quorum é encontrado_</span><span class="sxs-lookup"><span data-stu-id="5f0da-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![Figura 22: Recurso de cluster principal precisa de um novo endereço IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="5f0da-765">_**Figura 22:** Recurso de cluster principal precisa de um novo endereço IP_</span><span class="sxs-lookup"><span data-stu-id="5f0da-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="5f0da-766">Altere o endereço IP do serviço de cluster principal.</span><span class="sxs-lookup"><span data-stu-id="5f0da-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="5f0da-767">O cluster não pode iniciar até você alterar o endereço IP do serviço de cluster principal, pois o endereço IP do servidor aponta para um dos nós da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="5f0da-768">Faça isso na página **Propriedades** do recurso IP do serviço de cluster principal.</span><span class="sxs-lookup"><span data-stu-id="5f0da-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="5f0da-769">Por exemplo, precisamos atribuir um endereço IP (em nosso exemplo **10.0.0.42**) ao nome de host virtual do cluster **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Figura 23: na caixa de diálogo Propriedades, altere o endereço IP][sap-ha-guide-figure-3012]

  <span data-ttu-id="5f0da-771">_**Figura 23:** na caixa de diálogo **Propriedades**, altere o endereço IP_</span><span class="sxs-lookup"><span data-stu-id="5f0da-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Figura 24: Atribuir o endereço IP reservado para o cluster][sap-ha-guide-figure-3013]

  <span data-ttu-id="5f0da-773">_**Figura 24:** Atribuir o endereço IP reservado para o cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="5f0da-774">Coloque o nome do host virtual de cluster online.</span><span class="sxs-lookup"><span data-stu-id="5f0da-774">Bring the cluster virtual host name online.</span></span>

  ![Figura 25: Serviço principal do cluster funcionando com o endereço IP correto][sap-ha-guide-figure-3014]

  <span data-ttu-id="5f0da-776">_**Figura 25:** Serviço principal do cluster funcionando com o endereço IP correto_</span><span class="sxs-lookup"><span data-stu-id="5f0da-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="5f0da-777">Adicione o segundo nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-777">Add the second cluster node.</span></span>

  <span data-ttu-id="5f0da-778">Agora que o serviço principal do cluster está em execução, você pode adicionar o segundo nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Figura 26: Adicionar o segundo nó do cluster][sap-ha-guide-figure-3015]

  <span data-ttu-id="5f0da-780">_**Figura 26:** Adicionar o segundo nó do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="5f0da-781">Insira um nome para o segundo host do nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-781">Enter a name for the second cluster node host.</span></span>

  ![Figura 27: insira o segundo nome de host do nó de cluster][sap-ha-guide-figure-3016]

  <span data-ttu-id="5f0da-783">_**Figura 27:** insira o segundo nome de host do nó de cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5f0da-784">Verifique se a caixa de seleção **Adicionar todo o armazenamento qualificado ao cluster** **NÃO** está marcada.</span><span class="sxs-lookup"><span data-stu-id="5f0da-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Figura 28: Não marcar a caixa de seleção][sap-ha-guide-figure-3017]

  <span data-ttu-id="5f0da-786">_**Figura 28:** **Não** marque a caixa de seleção_</span><span class="sxs-lookup"><span data-stu-id="5f0da-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="5f0da-787">Você pode ignorar os avisos sobre quorum e discos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="5f0da-788">Você configurará o quorum e compartilhará o disco mais tarde, conforme descrito em [Instalando o SIOS DataKeeper Cluster Edition para o disco compartilhado de cluster do SAP ASCS/SCS][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="5f0da-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Figura 29: Ignorar os avisos sobre o quorum de disco][sap-ha-guide-figure-3018]

  <span data-ttu-id="5f0da-790">_**Figura 29:** Ignorar os avisos sobre o quorum de disco_</span><span class="sxs-lookup"><span data-stu-id="5f0da-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="5f0da-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurar a testemunha de compartilhamento de arquivos do cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="5f0da-792">Configurar a testemunha de compartilhamento de arquivos do cluster envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="5f0da-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="5f0da-793">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="5f0da-793">Creating a file share</span></span>
- <span data-ttu-id="5f0da-794">Configurar o quorum de testemunha de compartilhamento de arquivos no Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="5f0da-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="5f0da-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="5f0da-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="5f0da-796">Selecione uma testemunha de compartilhamento de arquivos em vez de um disco de quorum.</span><span class="sxs-lookup"><span data-stu-id="5f0da-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="5f0da-797">O SIOS DataKeeper dá suporte a essa opção.</span><span class="sxs-lookup"><span data-stu-id="5f0da-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="5f0da-798">Nos exemplos citados neste artigo, a testemunha de compartilhamento de arquivo está no servidor DNS/Active Directory em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="5f0da-799">A testemunha de compartilhamento de arquivo é chamada **domcontr-0**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="5f0da-800">Como uma conexão VPN seria configurada para o Azure (via VPN Site a Site ou Azure ExpressRoute), o serviço Active Directory/DNS é local e não é adequado para executar uma testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="5f0da-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5f0da-801">Se seu serviço DNS/Active Directory é executado somente no local, não configure a testemunha de compartilhamento de arquivo no sistema operacional Windows do Active Directory/DNS que está sendo executado no local.</span><span class="sxs-lookup"><span data-stu-id="5f0da-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="5f0da-802">A latência de rede entre os nós de cluster em execução no Azure e o Active Directory/DNS local pode ser muito grande e causar problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="5f0da-803">Não deixe de configurar a testemunha de compartilhamento de arquivo em uma máquina virtual do Azure que está em execução perto do nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="5f0da-804">A unidade de quorum precisa de pelo menos 1.024 MB de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="5f0da-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="5f0da-805">É recomendável ter 2.048 MB de espaço livre na unidade de quorum.</span><span class="sxs-lookup"><span data-stu-id="5f0da-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="5f0da-806">Adicione o objeto do nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-806">Add the cluster name object.</span></span>

  ![Figura 30: Atribuir as permissões no compartilhamento para o objeto de nome do cluster][sap-ha-guide-figure-3019]

  <span data-ttu-id="5f0da-808">_**Figura 30:** Atribuir as permissões no compartilhamento para o objeto de nome do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="5f0da-809">Verifique se as permissões incluem o poder de alterar dados no compartilhamento para o objeto de nome de cluster (em nosso exemplo **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="5f0da-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="5f0da-810">Para adicionar o objeto de nome do cluster à lista, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="5f0da-811">Altere o filtro para procurar objetos de computador além daqueles mostrados na Figura 31.</span><span class="sxs-lookup"><span data-stu-id="5f0da-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Figura 31: alterar os tipos de objetos para incluir computadores][sap-ha-guide-figure-3020]

  <span data-ttu-id="5f0da-813">_**Figura 31:** alterar os tipos de objetos para incluir computadores_</span><span class="sxs-lookup"><span data-stu-id="5f0da-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Figura 32: marque a caixa de seleção Computadores][sap-ha-guide-figure-3021]

  <span data-ttu-id="5f0da-815">_**Figura 32:** marque a caixa de seleção **Computadores**_</span><span class="sxs-lookup"><span data-stu-id="5f0da-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="5f0da-816">Insira o objeto de nome do cluster conforme mostrado na Figura 31.</span><span class="sxs-lookup"><span data-stu-id="5f0da-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="5f0da-817">Como o registro já foi criado, você pode alterar as permissões conforme mostrado na Figura 30.</span><span class="sxs-lookup"><span data-stu-id="5f0da-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="5f0da-818">Selecione a guia **Segurança** do compartilhamento e defina permissões mais detalhadas para o objeto de nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Figura 33: Definir os atributos de segurança para o objeto de nome do cluster no quórum de compartilhamento de arquivos][sap-ha-guide-figure-3022]

  <span data-ttu-id="5f0da-820">_**Figura 33:** Definir os atributos de segurança para o objeto de nome do cluster no quórum de compartilhamento de arquivos_</span><span class="sxs-lookup"><span data-stu-id="5f0da-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="5f0da-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Definir o quorum de testemunha de compartilhamento de arquivos no Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="5f0da-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="5f0da-822">Abra o Assistente para Definir a Configuração de Quorum.</span><span class="sxs-lookup"><span data-stu-id="5f0da-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![Figura 34: Iniciar o Assistente de configuração de quorum do cluster][sap-ha-guide-figure-3023]

  <span data-ttu-id="5f0da-824">_**Figura 34:** Iniciar o Assistente de configuração de quorum do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="5f0da-825">Na página **Selecionar Configuração de Quorum**, escolha **Selecionar a testemunha de quorum**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Figura 35: Configurações de quorum à sua escolha][sap-ha-guide-figure-3024]

  <span data-ttu-id="5f0da-827">_**Figura 35:** Configurações de quorum à sua escolha_</span><span class="sxs-lookup"><span data-stu-id="5f0da-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="5f0da-828">Na página **Selecionar Testemunha de Quorum**, escolha **Configurar uma testemunha de compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Figura 36: Selecionar a testemunha de compartilhamento de arquivo][sap-ha-guide-figure-3025]

  <span data-ttu-id="5f0da-830">_**Figura 36:** Selecionar a testemunha de compartilhamento de arquivo_</span><span class="sxs-lookup"><span data-stu-id="5f0da-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="5f0da-831">Digite o caminho UNC para o compartilhamento de arquivos (em nosso exemplo, \\domcontr-0\FSW).</span><span class="sxs-lookup"><span data-stu-id="5f0da-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="5f0da-832">Para ver uma lista das alterações que você pode fazer, selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![Figura 37: Definir o local do compartilhamento de arquivos para a testemunha de compartilhamento][sap-ha-guide-figure-3026]

  <span data-ttu-id="5f0da-834">_**Figura 37:** Definir o local do compartilhamento de arquivos para a testemunha de compartilhamento_</span><span class="sxs-lookup"><span data-stu-id="5f0da-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="5f0da-835">Selecione as alterações que você deseja e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="5f0da-836">Você precisa redefinir com êxito a configuração do cluster, conforme mostrado na Figura 38.</span><span class="sxs-lookup"><span data-stu-id="5f0da-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![Figura 38: confirmação de que você reconfigurou o cluster][sap-ha-guide-figure-3027]

  <span data-ttu-id="5f0da-838">_**Figura 38:** confirmação de que você reconfigurou o cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="5f0da-839">Depois de instalar com êxito o Cluster de Failover do Windows, é necessário alterar alguns limites para adaptar a detecção de failover às condições no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="5f0da-840">Os parâmetros a alterar estão documentados neste blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="5f0da-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="5f0da-841">Supondo que as duas VMs que criam a configuração de Cluster do Windows para ASCS/SCS estejam na mesma sub-rede, os parâmetros a seguir precisam ser alterados para estes valores:</span><span class="sxs-lookup"><span data-stu-id="5f0da-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="5f0da-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="5f0da-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="5f0da-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="5f0da-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="5f0da-844">Essas configurações foram testadas com clientes e, por um lado, forneceram um compromisso satisfatório de serem suficientemente resilientes.</span><span class="sxs-lookup"><span data-stu-id="5f0da-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="5f0da-845">Por outro lado, essas configurações ofereciam failover suficientemente rápido em condições de erro real de software SAP ou falha de nó/VM.</span><span class="sxs-lookup"><span data-stu-id="5f0da-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="5f0da-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Instalar SIOS DataKeeper Cluster Edition para disco de compartilhamento de cluster do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="5f0da-847">Agora você tem uma configuração do Clustering de Failover do Windows Server em funcionamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="5f0da-848">Mas para instalar uma instância do SAP ASCS/SCS, você precisa de um recurso de disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="5f0da-849">Não é possível criar os recursos de disco compartilhado que você precisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="5f0da-850">O SIOS DataKeeper Cluster Edition é uma solução de terceiros que você pode usar para criar recursos de disco compartilhados.</span><span class="sxs-lookup"><span data-stu-id="5f0da-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="5f0da-851">Instalar o SIOS DataKeeper Cluster Edition para o disco de compartilhamento de cluster do SAP ASCS/SCS envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="5f0da-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="5f0da-852">Adicionar o .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5f0da-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="5f0da-853">Instalando o SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5f0da-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="5f0da-854">Configurar o SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5f0da-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="5f0da-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Adicionar o .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="5f0da-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="5f0da-856">O Microsoft .NET Framework 3.5 não é automaticamente ativado ou instalado no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5f0da-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="5f0da-857">Como SIOS DataKeeper requer que o .NET Framework esteja em todos os nós nos quais o DataKeeper for instalado, será necessário instalar o .NET Framework 3.5 no sistema operacional convidado de todas as máquinas virtuais no cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="5f0da-858">Há duas maneiras de adicionar o .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="5f0da-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="5f0da-859">Uma delas é usar o Assistente para Adicionar Funções e Recursos no Windows, como mostrado na Figura 39.</span><span class="sxs-lookup"><span data-stu-id="5f0da-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Figura 39: Instalar o .NET Framework 3.5 usando o assistente Adicionar funções e recursos][sap-ha-guide-figure-3028]

  <span data-ttu-id="5f0da-861">_**Figura 39:** Instalar o .NET Framework 3.5 usando o assistente Adicionar funções e recursos_</span><span class="sxs-lookup"><span data-stu-id="5f0da-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![Figura 40: Barra de progresso da instalação quando você instala o .NET Framework 3.5 usando o assistente Adicionar funções e recursos][sap-ha-guide-figure-3029]

  <span data-ttu-id="5f0da-863">_**Figura 40:** barra de progresso da instalação no momento que você instala o .NET Framework 3.5 usando o Assistente para Adicionar Funções e Recursos_</span><span class="sxs-lookup"><span data-stu-id="5f0da-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="5f0da-864">Use a ferramenta de linha de comando dism.exe.</span><span class="sxs-lookup"><span data-stu-id="5f0da-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="5f0da-865">Para esse tipo de instalação, você precisa acessar o diretório SxS na mídia de instalação do Windows.</span><span class="sxs-lookup"><span data-stu-id="5f0da-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="5f0da-866">Em um prompt de comandos com privilégios elevados, digite:</span><span class="sxs-lookup"><span data-stu-id="5f0da-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="5f0da-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5f0da-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="5f0da-868">Instale o SIOS DataKeeper Cluster Edition em cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="5f0da-869">Para criar um armazenamento compartilhado virtual com o SIOS DataKeeper, crie um espelho sincronizado e simule o armazenamento compartilhado do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="5f0da-870">Antes de instalar o software SIOS, crie o usuário de domínio **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-871">Adicione esse usuário **DataKeeperSvc** ao grupo **Administradores locais** em ambos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="5f0da-872">Para instalar SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="5f0da-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="5f0da-873">Instale o software SIOS em ambos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-873">Install the SIOS software on both cluster nodes.</span></span>

  ![Instalador do SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: primeira página da instalação do SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="5f0da-876">_**Figura 41:** primeira página da instalação do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="5f0da-877">Na caixa de diálogo mostrada na figura 42, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Figura 42: O DataKeeper informa a você que um serviço será desabilitado][sap-ha-guide-figure-3032]

  <span data-ttu-id="5f0da-879">_**Figura 42:** O DataKeeper informa a você que um serviço será desabilitado_</span><span class="sxs-lookup"><span data-stu-id="5f0da-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="5f0da-880">Na caixa de diálogo mostrada na Figura 43, recomendamos que você selecione **Conta de domínio ou servidor**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Figura 43: Seleção do usuário para o SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="5f0da-882">_**Figura 43:** Seleção do usuário para o SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="5f0da-883">Insira o nome de usuário da conta de domínio e senhas que você criou para o SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5f0da-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Figura 44: Inserir o nome de usuário de domínio e a senha para a instalação do SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="5f0da-885">_**Figura 44:** Inserir o nome de usuário de domínio e a senha para a instalação do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="5f0da-886">Instale a chave de licença para o SIOS DataKeeper conforme mostrado na Figura 45.</span><span class="sxs-lookup"><span data-stu-id="5f0da-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Figura 45: insira a chave da licença do SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="5f0da-888">_**Figura 45:** insira a chave da licença do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="5f0da-889">Quando solicitado, reinicie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="5f0da-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurar SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="5f0da-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="5f0da-891">Depois de instalar o SIOS DataKeeper em ambos os nós, você precisará iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="5f0da-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="5f0da-892">O objetivo da configuração é ter a replicação de dados síncrona entre os discos adicionais anexados a cada uma das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5f0da-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="5f0da-893">Inicie a ferramenta de Configuração e Gerenciamento de DataKeeper e selecione **Conectar Servidor**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="5f0da-894">(Na Figura 46, essa opção é marcada em vermelho.)</span><span class="sxs-lookup"><span data-stu-id="5f0da-894">(In Figure 46, this option is circled in red.)</span></span>

  ![Figura 46: Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper][sap-ha-guide-figure-3036]

  <span data-ttu-id="5f0da-896">_**Figura 46:** Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="5f0da-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="5f0da-897">Insira o nome ou endereço TCP/IP do primeiro nó ao qual a ferramenta de Gerenciamento e Configuração deve se conectar e, em uma segunda etapa, as informações do segundo nó.</span><span class="sxs-lookup"><span data-stu-id="5f0da-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Figura 47: inserir o nome ou endereço TCP/IP do primeiro nó ao qual a ferramenta de gerenciamento deve se conectar e, em uma segunda etapa, o segundo nó][sap-ha-guide-figure-3037]

  <span data-ttu-id="5f0da-899">_**Figura 47:** inserir o nome ou endereço TCP/IP do primeiro nó ao qual a ferramenta de gerenciamento deve se conectar e, em uma segunda etapa, o segundo nó_</span><span class="sxs-lookup"><span data-stu-id="5f0da-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="5f0da-900">Crie o trabalho de replicação entre os dois nós.</span><span class="sxs-lookup"><span data-stu-id="5f0da-900">Create the replication job between the two nodes.</span></span>

  ![Figura 48: Criar trabalho de replicação][sap-ha-guide-figure-3038]

  <span data-ttu-id="5f0da-902">_**Figura 48:** Criar trabalho de replicação_</span><span class="sxs-lookup"><span data-stu-id="5f0da-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="5f0da-903">Um assistente orienta você pelo processo de criação de um trabalho de replicação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="5f0da-904">Defina o nome, o endereço TCP/IP e o volume de disco do nó de origem.</span><span class="sxs-lookup"><span data-stu-id="5f0da-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Figura 49: Definir o nome do trabalho de replicação][sap-ha-guide-figure-3039]

  <span data-ttu-id="5f0da-906">_**Figura 49:** Definir o nome do trabalho de replicação_</span><span class="sxs-lookup"><span data-stu-id="5f0da-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Figura 50: Definir os dados de base do nó que deve ser o nó de origem atual][sap-ha-guide-figure-3040]

  <span data-ttu-id="5f0da-908">_**Figura 50:** Definir os dados de base do nó que deve ser o nó de origem atual_</span><span class="sxs-lookup"><span data-stu-id="5f0da-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="5f0da-909">Defina o nome, o endereço TCP/IP e o volume de disco do nó de destino.</span><span class="sxs-lookup"><span data-stu-id="5f0da-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Figura 51: Definir os dados base do nó que deve ser o nó de destino atual][sap-ha-guide-figure-3041]

  <span data-ttu-id="5f0da-911">_**Figura 51:** Definir os dados base do nó que deve ser o nó de destino atual_</span><span class="sxs-lookup"><span data-stu-id="5f0da-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="5f0da-912">Defina os algoritmos de compactação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-912">Define the compression algorithms.</span></span> <span data-ttu-id="5f0da-913">Em nosso exemplo, recomendamos que você compacte o fluxo de replicação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="5f0da-914">Particularmente em situações de ressincronização, a compactação do fluxo de replicação reduz consideravelmente o tempo de ressincronização.</span><span class="sxs-lookup"><span data-stu-id="5f0da-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="5f0da-915">Observe que a compactação utiliza os recursos de CPU e RAM de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f0da-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="5f0da-916">Conforme aumenta a taxa de compactação, aumenta o volume de recursos de CPU usados.</span><span class="sxs-lookup"><span data-stu-id="5f0da-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="5f0da-917">Você também pode ajustar essa configuração mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5f0da-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="5f0da-918">Outra configuração que precisa ser verificada é se a replicação é executada de modo síncrono ou assíncrono.</span><span class="sxs-lookup"><span data-stu-id="5f0da-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="5f0da-919">*Quando você protege configurações SAP ASCS/SCS, deve usar a replicação síncrona*.</span><span class="sxs-lookup"><span data-stu-id="5f0da-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Figura 52: Definir detalhes de replicação][sap-ha-guide-figure-3042]

  <span data-ttu-id="5f0da-921">_**Figura 52:** Definir detalhes de replicação_</span><span class="sxs-lookup"><span data-stu-id="5f0da-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="5f0da-922">Defina se o volume que é replicado pelo trabalho de replicação deve ser representado em uma configuração de cluster Clustering de Failover do Windows Server como um disco compartilhado.</span><span class="sxs-lookup"><span data-stu-id="5f0da-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="5f0da-923">Para a configuração do SAP ASCS/SCS, escolha **Sim** para que o cluster do Windows veja o volume replicado como disco compartilhado que pode ser usado como volume de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Figura 53: selecione Sim para definir o volume replicado como um volume de cluster][sap-ha-guide-figure-3043]

  <span data-ttu-id="5f0da-925">_**Figura 53:** selecionar **Sim** para definir o volume replicado como um volume de cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="5f0da-926">Depois que o volume é criado, a ferramenta de Configuração e Gerenciamento do DataKeeper mostra que o trabalho de replicação está ativo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Figura 54: O espelhamento síncrono do DataKeeper para o disco de compartilhamento do SAP ASCS/SCS está ativo][sap-ha-guide-figure-3044]

  <span data-ttu-id="5f0da-928">_**Figura 54:** O espelhamento síncrono do DataKeeper para o disco de compartilhamento do SAP ASCS/SCS está ativo_</span><span class="sxs-lookup"><span data-stu-id="5f0da-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="5f0da-929">O Gerenciador de Cluster de Failover agora mostra o disco como um disco do DataKeeper, conforme ilustrado na Figura 55.</span><span class="sxs-lookup"><span data-stu-id="5f0da-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Figura 55: O Gerenciador de Cluster de Failover mostra o disco do DataKeeper replicado][sap-ha-guide-figure-3045]

  <span data-ttu-id="5f0da-931">_**Figura 55:** O Gerenciador de Cluster de Failover mostra o disco do DataKeeper replicado_</span><span class="sxs-lookup"><span data-stu-id="5f0da-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="5f0da-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Instalar o sistema SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="5f0da-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="5f0da-933">Não descreveremos a instalação DBMS porque as configurações variam dependendo do sistema DBMS que você usar.</span><span class="sxs-lookup"><span data-stu-id="5f0da-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="5f0da-934">No entanto, supomos que as preocupações de alta disponibilidade com o DBMS são dissipadas com o suporte às funcionalidades que os diferentes fornecedores de DBMS dão para o Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="5f0da-935">Por exemplo, o Always On ou o Espelhamento de Banco de Dados para SQL Server e Oracle Data Guard para bancos de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="5f0da-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="5f0da-936">No cenário que usamos neste artigo, não adicionamos outra proteção ao DBMS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="5f0da-937">Não existem considerações especiais quando diferentes serviços DBMS interagem com esse tipo de configuração de SAP ASCS/SCS clusterizada no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-938">O procedimento de instalação dos sistemas ABAP, sistemas Java e sistemas ABAP+Java do SAP NetWeaver é quase idêntico.</span><span class="sxs-lookup"><span data-stu-id="5f0da-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="5f0da-939">A diferença mais significativa é que um sistema SAP ABAP tem uma instância ASCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="5f0da-940">O sistema SAP Java tem uma instância SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="5f0da-941">O sistema ABAP+Java do SAP tem uma instância ASCS e uma instância ABAP+Java em execução no mesmo grupo de cluster de failover da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5f0da-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="5f0da-942">As diferenças de instalação para cada pilha de instalação do SAP NetWeaver serão explicitamente mencionadas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="5f0da-943">Você pode assumir que todas as outras partes são as mesmas.</span><span class="sxs-lookup"><span data-stu-id="5f0da-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="5f0da-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5f0da-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f0da-945">Não coloque o arquivo da página em volumes espelhados do DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5f0da-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="5f0da-946">O DataKeeper não dá suporte a volumes espelhados.</span><span class="sxs-lookup"><span data-stu-id="5f0da-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="5f0da-947">Você pode deixar o arquivo de página na unidade D temporária de uma máquina virtual do Azure, o que é o padrão.</span><span class="sxs-lookup"><span data-stu-id="5f0da-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="5f0da-948">Se já não estiver lá, mova o arquivo da página do Windows para a unidade D: da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="5f0da-949">Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade envolve as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="5f0da-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="5f0da-950">Criar um nome de host virtual para a instância clusterizada do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="5f0da-951">Instalar o primeiro nó de cluster do SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="5f0da-952">Modificar o perfil SAP da instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="5f0da-953">Adicionando uma porta de investigação</span><span class="sxs-lookup"><span data-stu-id="5f0da-953">Adding a probe port</span></span>
- <span data-ttu-id="5f0da-954">Abrindo a porta de investigação do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="5f0da-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="5f0da-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Criar um nome de host virtual para a instância clusterizada do SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="5f0da-956">No Gerenciador de DNS do Windows, crie uma entrada DNS para o nome de host virtual da instância ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5f0da-957">O endereço IP que você atribui ao nome de host virtual da instância ASCS/SCS deve ser o mesmo que o endereço IP que você atribuiu ao Azure Load Balancer (**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="5f0da-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="5f0da-958">O endereço IP do nome de host virtual do SAP ASCS/SCS (**pr1-ascs-sap**) é o mesmo que o endereço IP do Azure Load Balancer (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="5f0da-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Figura 56: Definir a entrada DNS para o nome virtual do cluster do SAP ASCS/SCS e endereço TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="5f0da-960">_**Figura 56:** Definir a entrada DNS para o nome virtual do cluster do SAP ASCS/SCS e endereço TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="5f0da-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="5f0da-961">Para definir o endereço IP atribuído ao nome de host virtual, selecione **Gerenciador de DNS** > **Domínio**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![Figura 57: Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="5f0da-963">_**Figura 57:** Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="5f0da-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="5f0da-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Instalar o primeiro nó do cluster do SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="5f0da-965">Execute a primeira opção do nó de cluster no nó A de cluster, por exemplo, no host **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="5f0da-966">Para manter as portas padrão para o balanceador interno de carga do Azure, escolha:</span><span class="sxs-lookup"><span data-stu-id="5f0da-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="5f0da-967">**Sistema ABAP**: número da instância **ASCS** **00**</span><span class="sxs-lookup"><span data-stu-id="5f0da-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="5f0da-968">**Sistema Java**: número da instância **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="5f0da-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="5f0da-969">**Sistema ABAP + Java**: número da instância **ASCS** **00** e número da instância **SCS** **01**</span><span class="sxs-lookup"><span data-stu-id="5f0da-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="5f0da-970">Para usar números de instância além de 00 para a instância do ASCS ABAP e 01 para a instância do SCS Java, primeiramente será preciso alterar as regras padrão de balanceamento de carga do Azure Internal Load Balancer, conforme descrito em [Alterar as regras do balanceamento de carga padrão do ASCS/SCS para o Azure Internal Load Balancer][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="5f0da-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="5f0da-971">As próximas tarefas não são descritas na documentação de instalação padrão do SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-972">A documentação de instalação do SAP descreve como instalar o primeiro nó ASCS/SCS do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="5f0da-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modificar o perfil SAP da instância do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="5f0da-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="5f0da-974">Você precisa adicionar um novo parâmetro de perfil.</span><span class="sxs-lookup"><span data-stu-id="5f0da-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="5f0da-975">O parâmetro de perfil impede conexões entre os processos de trabalho do SAP e o servidor de enfileiramento de fechar quando estão ociosas por muito tempo.</span><span class="sxs-lookup"><span data-stu-id="5f0da-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="5f0da-976">Mencionamos o cenário de problema em [Adicionar entradas do Registro a ambos os nós de cluster da instância SAP ASCS/SCS][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="5f0da-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="5f0da-977">Nessa seção, também apresentamos duas alterações para alguns parâmetros básicos de conexão TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="5f0da-978">Na segunda etapa, você precisará configurar o servidor de enfileiramento para enviar um sinal `keep_alive` para que as conexões não atinjam o limite de ociosidade do balanceador interno de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0da-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="5f0da-979">Para modificar o perfil SAP da instância do ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="5f0da-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="5f0da-980">Adicione este parâmetro de perfil ao perfil da instância do SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="5f0da-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="5f0da-981">Em nosso exemplo, o caminho é:</span><span class="sxs-lookup"><span data-stu-id="5f0da-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="5f0da-982">Por exemplo, para o perfil da instância do SAP SCS e o caminho correspondente:</span><span class="sxs-lookup"><span data-stu-id="5f0da-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="5f0da-983">Para aplicar as alterações, reinicie a instância SAP ASCS /SCS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="5f0da-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Adicionar uma porta de investigação</span><span class="sxs-lookup"><span data-stu-id="5f0da-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="5f0da-985">Use a funcionalidade de investigação do balanceador interno de carga para fazer com que toda a configuração do cluster funcione com o Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5f0da-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="5f0da-986">Normalmente, um balanceador de carga interno do Azure distribui a carga de trabalho de entrada igualmente entre as máquinas virtuais participantes.</span><span class="sxs-lookup"><span data-stu-id="5f0da-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="5f0da-987">No entanto, isso não funcionará em algumas configurações de cluster porque apenas uma instância está ativa.</span><span class="sxs-lookup"><span data-stu-id="5f0da-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="5f0da-988">A outra instância é passiva e não pode aceitar parte da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f0da-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="5f0da-989">A funcionalidade de investigação ajuda quando o balanceador de carga interno do Azure atribui o trabalho apenas a uma instância ativa.</span><span class="sxs-lookup"><span data-stu-id="5f0da-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="5f0da-990">Com a funcionalidade de investigação, o balanceador de carga interno pode detectar quais instâncias estão ativas e mirar apenas na instância com a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f0da-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="5f0da-991">Para adicionar uma porta de investigação:</span><span class="sxs-lookup"><span data-stu-id="5f0da-991">To add a probe port:</span></span>

1.  <span data-ttu-id="5f0da-992">Verifique a configuração **ProbePort** atual executando o seguinte comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f0da-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="5f0da-993">Execute-o dentro de uma das máquinas virtuais na configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="5f0da-994">Defina uma porta de investigação.</span><span class="sxs-lookup"><span data-stu-id="5f0da-994">Define a probe port.</span></span> <span data-ttu-id="5f0da-995">O número da porta de investigação padrão é **0**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-995">The default probe port number is **0**.</span></span> <span data-ttu-id="5f0da-996">Em nosso exemplo, usamos a porta de investigação **62000**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-996">In our example, we use probe port **62000**.</span></span>

  ![Figura 58: A porta de investigação da configuração de cluster é 0 por padrão][sap-ha-guide-figure-3048]

  <span data-ttu-id="5f0da-998">_**Figura 58:** a porta de investigação da configuração de cluster padrão é 0_</span><span class="sxs-lookup"><span data-stu-id="5f0da-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="5f0da-999">O número da porta é definido nos modelos do Azure Resource Manager para SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="5f0da-1000">Você pode atribuir o número da porta no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="5f0da-1001">Para definir um novo valor de ProbePort para o recurso de cluster **SAP <*SID*> IP**, execute o seguinte script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="5f0da-1002">Atualize as variáveis do PowerShell para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="5f0da-1003">Depois que o script é executado, será solicitado que você reinicie o grupo de clusters do SAP para ativar as alterações.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="5f0da-1004">Depois de colocar a função de cluster **SAP <*SID*>** online, verifique se **ProbePort** está definido como o novo valor.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Investigar a porta de cluster depois de definir o novo valor][sap-ha-guide-figure-3049]

  <span data-ttu-id="5f0da-1006">_**Figura 59:** Investigar a porta de cluster depois de definir o novo valor_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="5f0da-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Abrir a porta de investigação do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="5f0da-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="5f0da-1008">Você precisa abrir a porta de investigação do firewall do Windows nos dois nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="5f0da-1009">Use o script a seguir para abrir uma porta de investigação no firewall do Windows.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="5f0da-1010">Atualize as variáveis do PowerShell para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="5f0da-1011">A **ProbePort** é definida como **62000**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="5f0da-1012">Agora é possível acessar o compartilhamento de arquivos **\\ascsha-clsap\sapmnt** de outros hosts como **ascsha-dbas**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="5f0da-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Instalar a instância de banco de dados</span><span class="sxs-lookup"><span data-stu-id="5f0da-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="5f0da-1014">Para instalar a instância de banco de dados, siga o processo descrito na documentação de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="5f0da-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar o segundo nó do cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="5f0da-1016">Para instalar o segundo cluster, siga as etapas no guia de instalação do SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="5f0da-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Alterar o tipo de início da instância do serviço Windows ERS do SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="5f0da-1018">Altere o tipo de inicialização do serviço Windows do SAP ERS para **Automático (Atraso na Inicialização)** em ambos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Figura 60: Alterar o tipo de serviço da instância ERS do SAP para atraso automático][sap-ha-guide-figure-3050]

<span data-ttu-id="5f0da-1020">_**Figura 60:** Alterar o tipo de serviço da instância ERS do SAP para atraso automático_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="5f0da-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Instalar o servidor de aplicativos primário SAP</span><span class="sxs-lookup"><span data-stu-id="5f0da-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="5f0da-1022">Instalar a instância <*SID*>-di-0 do PAS (Servidor de Aplicativos primário) na máquina virtual que você designou para hospedar o PAS.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="5f0da-1023">Não há dependências nas configurações específicas do Azure ou do DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="5f0da-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Instalar o servidor de aplicativos SAP adicional</span><span class="sxs-lookup"><span data-stu-id="5f0da-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="5f0da-1025">Instale um AAS (Servidor de Aplicativos Adicional) SAP em todas as máquinas virtuais que você designou para hospedar um Servidor de Aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="5f0da-1026">Por exemplo, de <*SID*>-di-1 para <*SID*>-di-&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="5f0da-1027">Isso conclui a instalação de um sistema SAP NetWeaver de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="5f0da-1028">Em seguida, continue com o teste de failover.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="5f0da-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Testar o failover da instância do SAP ASCS/SCS e a replicação do SIOS</span><span class="sxs-lookup"><span data-stu-id="5f0da-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="5f0da-1030">É muito fácil testar e monitorar um failover de instância de SAP ASCS/SCS e a replicação do disco SIOS usando o Gerenciador de Cluster de Failover e a ferramenta de Gerenciamento e Configuração do SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="5f0da-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> A instância do SAP ASCS/SCS está em execução no Nó A do Cluster</span><span class="sxs-lookup"><span data-stu-id="5f0da-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="5f0da-1032">O grupo de clusters **SAP PR1** está em execução no nó A do cluster. Por exemplo, em **pr1-ascs-0**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="5f0da-1033">Atribua a unidade de disco compartilhado S, que é parte do grupo de cluster **SAP PR1** e é usada pela instância ASCS/SCS, ao cluster A do nó.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![Figura 61: Gerenciador de Cluster de Failover: o grupo de clusters <SID> de SAP está em execução no nó A de cluster][sap-ha-guide-figure-5000]

<span data-ttu-id="5f0da-1035">_**Figura 61:** Gerenciador de Cluster de Failover: o grupo de clusters SAP <*SID*> está em execução no Nó A do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="5f0da-1036">Na ferramenta de Gerenciamento e Configuração do DataKeeper SIOS, você pode ver que os dados do disco compartilhado são replicados de modo síncrono da unidade do volume de origem S em um nó A de cluster para a unidade do volume de destino S no nó B de cluster. Por exemplo, é replicado de **pr1-ascs-0 [10.0.0.40]** a **pr1-ascs-1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Figura 62: No SIOS DataKeeper, replique o volume local do nó A do cluster para o nó B do cluster][sap-ha-guide-figure-5001]

<span data-ttu-id="5f0da-1038">_**Figura 62:** No SIOS DataKeeper, replique o volume local do nó A do cluster para o nó B do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="5f0da-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover do nó A para o nó B</span><span class="sxs-lookup"><span data-stu-id="5f0da-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="5f0da-1040">Você pode usar estas opções para iniciar um failover do grupo de clusters <*SID*> do SAP do nó A para o nó B de cluster:</span><span class="sxs-lookup"><span data-stu-id="5f0da-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="5f0da-1041">Usar o Gerenciador de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="5f0da-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="5f0da-1042">Usar o PowerShell de Cluster de Failover</span><span class="sxs-lookup"><span data-stu-id="5f0da-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="5f0da-1043">Reiniciar o nó A de cluster no sistema operacional convidado do Windows (isso iniciará um failover automático do grupo de clusters SAP <*SID*> do nó A para o nó B).</span><span class="sxs-lookup"><span data-stu-id="5f0da-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="5f0da-1044">Reiniciar o nó de cluster A do portal do Azure (isso iniciará um failover automático do grupo de clusters SAP <*SID*> do nó A para o nó B).</span><span class="sxs-lookup"><span data-stu-id="5f0da-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="5f0da-1045">Reiniciar o nó de cluster A usando o Azure PowerShell (isso iniciará um failover automático do grupo de clusters SAP <*SID*> do nó A para o nó B).</span><span class="sxs-lookup"><span data-stu-id="5f0da-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="5f0da-1046">Após o failover, o grupo de clusters SAP <*SID*> está em execução no nó de cluster B. Por exemplo, em **pr1-ascs-1**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Figura 63: no Gerenciador de Cluster de Failover, o grupo de clusters <SID> de SAP está em execução no nó de cluster B][sap-ha-guide-figure-5002]

  <span data-ttu-id="5f0da-1048">_**Figura 63**: No gerenciador de Cluster de Failover, o grupo de clusters SAP <*SID*> está em execução no nó B do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="5f0da-1049">O disco compartilhado agora é montado no nó de cluster B. O SIOS DataKeeper está replicando dados da unidade do volume de origem S no nó de cluster B para a unidade do volume de destino S no nó de cluster A. Por exemplo, ele está replicando **pr1-ascs-1 [10.0.0.41]** a **pr1-ascs-0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="5f0da-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Figura 64: o SIOS DataKeeper replica o volume local do nó B do cluster para o nó A do cluster][sap-ha-guide-figure-5003]

  <span data-ttu-id="5f0da-1051">_**Figura 64:** o SIOS DataKeeper replica o volume local do nó B do cluster para o nó A do cluster_</span><span class="sxs-lookup"><span data-stu-id="5f0da-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
