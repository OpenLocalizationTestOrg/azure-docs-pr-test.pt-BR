---
title: "aaaSQL servidor FCI - máquinas virtuais do Azure | Microsoft Docs"
description: "Este artigo explica como toocreate instância de Cluster de Failover do SQL Server em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="27247-103">Configurar a instância de Cluster de Failover do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="27247-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="27247-104">Este artigo explica como toocreate um SQL Server de Cluster de Failover (FCI) da instância em máquinas virtuais do Azure no modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="27247-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="27247-105">Esta solução usa [direta de espaços de armazenamento do Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como uma SAN virtual com base em software que sincroniza o armazenamento de saudação (discos de dados) entre nós de saudação (máquinas virtuais do Azure) em um Cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="27247-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="27247-106">S2D é novo no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="27247-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="27247-107">Olá diagrama a seguir mostra solução completa de saudação em máquinas virtuais do Azure:</span><span class="sxs-lookup"><span data-stu-id="27247-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="27247-109">Olá precede o diagrama mostra:</span><span class="sxs-lookup"><span data-stu-id="27247-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="27247-110">Duas máquinas virtuais do Azure em um Cluster de Failover do Windows.</span><span class="sxs-lookup"><span data-stu-id="27247-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="27247-111">Quando uma máquina virtual está em um cluster de failover, ela também é chamada de *nó de cluster* ou *nós*.</span><span class="sxs-lookup"><span data-stu-id="27247-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="27247-112">Cada máquina virtual tem dois ou mais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="27247-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="27247-113">S2D sincroniza dados Olá no disco de dados hello e apresenta Olá sincronizado de armazenamento como um pool de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="27247-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="27247-114">pool de armazenamento Olá apresenta um cluster de failover do cluster (CSV) de volume compartilhado toohello.</span><span class="sxs-lookup"><span data-stu-id="27247-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="27247-115">função de cluster do SQL Server FCI Olá usa Olá CSV Olá para unidades de dados.</span><span class="sxs-lookup"><span data-stu-id="27247-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="27247-116">Um carga do Azure balanceador toohold Olá endereço IP hello FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="27247-117">Um conjunto de disponibilidade do Azure mantém todos os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="27247-118">Todos os recursos do Azure estão no diagrama Olá estão em Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27247-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="27247-119">Para obter detalhes sobre S2D, confira [Espaços de Armazenamento Direto do Windows Server 2016 Datacenter Edition \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="27247-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="27247-120">O S2D dá suporte a dois tipos de arquiteturas: convergida e hiperconvergida.</span><span class="sxs-lookup"><span data-stu-id="27247-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="27247-121">arquitetura de saudação neste documento é hiperconvergida.</span><span class="sxs-lookup"><span data-stu-id="27247-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="27247-122">Um armazenamento de saudação infraestrutura hiperconvergida locais no hello mesmos servidores de aplicativo hello cluster host.</span><span class="sxs-lookup"><span data-stu-id="27247-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="27247-123">Nesta arquitetura, o armazenamento de saudação é em cada nó de FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="27247-124">Exemplo de modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="27247-124">Example Azure template</span></span>

<span data-ttu-id="27247-125">Você pode criar a solução inteira Olá no Azure de um modelo.</span><span class="sxs-lookup"><span data-stu-id="27247-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="27247-126">Um exemplo de um modelo está disponível no GitHub de saudação [modelos de início rápido do Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="27247-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="27247-127">Este exemplo não é criado ou testado para qualquer carga de trabalho específica.</span><span class="sxs-lookup"><span data-stu-id="27247-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="27247-128">Você pode executar Olá modelo toocreate um FCI do SQL Server com o domínio do S2D armazenamento tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="27247-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="27247-129">Você pode avaliar modelo hello e modificá-lo para suas finalidades.</span><span class="sxs-lookup"><span data-stu-id="27247-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="27247-130">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="27247-130">Before you begin</span></span>

<span data-ttu-id="27247-131">Há algumas coisas que você precisa tooknow e algumas coisas que você precisa em vigor antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="27247-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="27247-132">Quais tooknow</span><span class="sxs-lookup"><span data-stu-id="27247-132">What tooknow</span></span>
<span data-ttu-id="27247-133">Você deve ter uma compreensão operacional de saudação tecnologias a seguir:</span><span class="sxs-lookup"><span data-stu-id="27247-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="27247-134">Tecnologias de cluster do Windows</span><span class="sxs-lookup"><span data-stu-id="27247-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="27247-135">[Instâncias de Cluster de Failover do SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="27247-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="27247-136">Além disso, você deve ter uma compreensão geral dos Olá tecnologias a seguir:</span><span class="sxs-lookup"><span data-stu-id="27247-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="27247-137">Solução hiperconvergida usando Espaços de Armazenamento Direto no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="27247-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="27247-138">Grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="27247-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="27247-139">Quais toohave</span><span class="sxs-lookup"><span data-stu-id="27247-139">What toohave</span></span>

<span data-ttu-id="27247-140">Antes de seguir as instruções neste artigo hello, você já deve ter:</span><span class="sxs-lookup"><span data-stu-id="27247-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="27247-141">Uma assinatura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="27247-142">Um domínio do Windows em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="27247-143">Uma conta com objetos toocreate permissão Olá máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="27247-144">Uma rede virtual do Azure e sub-rede com espaço de endereços IP suficiente para Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="27247-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="27247-145">As duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-145">Both virtual machines.</span></span>
   - <span data-ttu-id="27247-146">endereço IP de cluster de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="27247-147">Um endereço IP para cada FCI.</span><span class="sxs-lookup"><span data-stu-id="27247-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="27247-148">DNS configurado no hello rede do Azure, apontando toohello controladores de domínio.</span><span class="sxs-lookup"><span data-stu-id="27247-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="27247-149">Com esses pré-requisitos em vigor, é possível continuar com a criação do cluster de failover.</span><span class="sxs-lookup"><span data-stu-id="27247-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="27247-150">Olá primeira etapa é toocreate Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="27247-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="27247-151">Etapa 1: criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="27247-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="27247-152">Faça logon no toohello [portal do Azure](http://portal.azure.com) com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="27247-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="27247-153">[Criar um conjunto de disponibilidade do Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="27247-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="27247-154">disponibilidade de saudação defina agrupa máquinas virtuais em domínios de falha e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="27247-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="27247-155">conjunto de disponibilidade Olá torna-se de que seu aplicativo não seja afetado por pontos únicos de falha, como o comutador de rede hello ou unidade de energia de saudação de um rack de servidores.</span><span class="sxs-lookup"><span data-stu-id="27247-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="27247-156">Se você não tiver criado o grupo de recursos de saudação para as máquinas virtuais, fazê-lo quando você cria um conjunto de disponibilidade do Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="27247-157">Se você estiver usando o conjunto de disponibilidade de Olá Olá toocreate portal do Azure, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="27247-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="27247-158">No portal do Azure de Olá, clique em  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="27247-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="27247-159">Procure **Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="27247-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="27247-160">Clique em **Conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="27247-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="27247-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27247-161">Click **Create**.</span></span>
   - <span data-ttu-id="27247-162">Em Olá **criar conjunto de disponibilidade** folha, Olá do conjunto de valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="27247-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="27247-163">**Nome**: um nome para o conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="27247-164">**Assinatura**: sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="27247-165">**Grupo de recursos**: toouse um grupo existente, clique em **usar existente** e grupo Olá selecione da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="27247-166">Caso contrário, escolha **criar novo** e digite um nome para o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="27247-167">**Local**: definir o local de saudação onde você planeja toocreate suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="27247-168">**Domínios de falha**: usar saudação padrão (3).</span><span class="sxs-lookup"><span data-stu-id="27247-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="27247-169">**Atualizar domínios**: usar saudação padrão (5).</span><span class="sxs-lookup"><span data-stu-id="27247-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="27247-170">Clique em **criar** toocreate conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="27247-171">Crie máquinas virtuais de saudação no conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="27247-172">Provisione duas máquinas virtuais de SQL Server no conjunto de disponibilidade do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="27247-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="27247-173">Para obter instruções, consulte [provisionar uma máquina de virtual do SQL Server no portal do Azure de saudação](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="27247-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="27247-174">Coloque as duas máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="27247-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="27247-175">Olá mesmo grupo de recursos do Azure que sua disponibilidade definida está na.</span><span class="sxs-lookup"><span data-stu-id="27247-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="27247-176">Em Olá mesma rede como o controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="27247-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="27247-177">Em uma sub-rede com espaço suficiente de endereços IP para ambas as máquinas virtuais e todos ps FCIs que você pode vir a usar nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="27247-178">No conjunto de disponibilidade do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="27247-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="27247-179">Você não pode definir nem alterar a disponibilidade definida depois que uma máquina virtual é criada.</span><span class="sxs-lookup"><span data-stu-id="27247-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="27247-180">Escolha uma imagem de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="27247-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="27247-181">Você pode usar um mercado imagem com o que inclui o Windows Server e SQL Server ou apenas saudação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="27247-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="27247-182">Para obter detalhes, confira [Visão geral do SQL Server em máquinas virtuais do Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="27247-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="27247-183">Olá oficial do SQL Server imagens Olá Galeria do Azure incluem uma instância instalada do SQL Server, além de software de instalação do SQL Server hello e chave necessária hello.</span><span class="sxs-lookup"><span data-stu-id="27247-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="27247-184">Escolha a imagem à direita de saudação de acordo com toohow que deseja toopay de licença do SQL Server hello:</span><span class="sxs-lookup"><span data-stu-id="27247-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="27247-185">**Pagar por uso de licenciamento**: Olá por minuto dessas imagens inclui licenciamento do hello do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="27247-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="27247-186">**SQL Server 2016 Enterprise no Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="27247-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="27247-187">**SQL Server 2016 Standard no Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="27247-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="27247-188">**SQL Server 2016 Developer no Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="27247-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="27247-189">**BYOL (Traga sua própria licença)**</span><span class="sxs-lookup"><span data-stu-id="27247-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="27247-190">**{BYOL} SQL Server 2016 Enterprise no Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="27247-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="27247-191">**{BYOL} SQL Server 2016 Standard no Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="27247-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="27247-192">Depois de criar a máquina virtual de Olá, remova a instância do SQL Server autônomo pré-instalados Olá.</span><span class="sxs-lookup"><span data-stu-id="27247-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="27247-193">Depois de configurar o cluster de failover hello e S2D, você usará Olá pré-instaladas do SQL Server mídia toocreate Olá FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="27247-194">Como alternativa, você pode usar imagens do Azure Marketplace com apenas o sistema de operacional hello.</span><span class="sxs-lookup"><span data-stu-id="27247-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="27247-195">Escolha um **Datacenter do Windows Server 2016** da imagem e instalar Olá FCI do SQL Server depois de configurar o cluster de failover hello e S2D.</span><span class="sxs-lookup"><span data-stu-id="27247-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="27247-196">Esta imagem não contém a mídia de instalação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="27247-197">Coloque a mídia de instalação de saudação em um local onde você pode executar a instalação do SQL Server Olá para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="27247-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="27247-198">Depois que o Azure cria suas máquinas virtuais, conecte-se tooeach VM com o RDP.</span><span class="sxs-lookup"><span data-stu-id="27247-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="27247-199">Quando você primeiro se conectar máquina virtual de tooa com o RDP, computador Olá perguntará se você deseja tooallow toobe este PC podem ser descobertos na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="27247-200">Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="27247-200">Click **Yes**.</span></span>

1. <span data-ttu-id="27247-201">Se você estiver usando uma das imagens de máquina virtual com o SQL Server hello, remova instância do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="27247-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="27247-202">Em **Programas e Recursos**, clique com o botão direito do mouse em **Microsoft SQL Server 2016 (64 bits)** e clique em **Desinstalar/Alterar**.</span><span class="sxs-lookup"><span data-stu-id="27247-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="27247-203">Clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="27247-203">Click **Remove**.</span></span>
   - <span data-ttu-id="27247-204">Selecione a instância padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-204">Select hello default instance.</span></span>
   - <span data-ttu-id="27247-205">Remova todos os recursos em **Serviços de Mecanismo de Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="27247-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="27247-206">Não remova **Recursos Compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="27247-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="27247-207">Consulte Olá figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="27247-207">See hello following picture:</span></span>

      ![Remover Recursos](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="27247-209">Clique em **Avançar** e em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="27247-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="27247-210"><a name="ports"></a>Abra as portas de firewall hello.</span><span class="sxs-lookup"><span data-stu-id="27247-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="27247-211">Em cada máquina virtual, abra Olá portas a seguir no hello Firewall do Windows.</span><span class="sxs-lookup"><span data-stu-id="27247-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="27247-212">Finalidade</span><span class="sxs-lookup"><span data-stu-id="27247-212">Purpose</span></span> | <span data-ttu-id="27247-213">Porta TCP</span><span class="sxs-lookup"><span data-stu-id="27247-213">TCP Port</span></span> | <span data-ttu-id="27247-214">Observações</span><span class="sxs-lookup"><span data-stu-id="27247-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="27247-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="27247-215">SQL Server</span></span> | <span data-ttu-id="27247-216">1433</span><span class="sxs-lookup"><span data-stu-id="27247-216">1433</span></span> | <span data-ttu-id="27247-217">Porta normal para instâncias padrão do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="27247-218">Se você usou uma imagem da Galeria hello, essa porta é aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="27247-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="27247-219">Investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="27247-219">Health probe</span></span> | <span data-ttu-id="27247-220">59999</span><span class="sxs-lookup"><span data-stu-id="27247-220">59999</span></span> | <span data-ttu-id="27247-221">Qualquer porta TCP aberta.</span><span class="sxs-lookup"><span data-stu-id="27247-221">Any open TCP port.</span></span> <span data-ttu-id="27247-222">Em uma etapa posterior, configure o balanceador de carga de saudação [investigação de integridade](#probe) e Olá cluster toouse essa porta.</span><span class="sxs-lookup"><span data-stu-id="27247-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="27247-223">Adicione armazenamento toohello VM.</span><span class="sxs-lookup"><span data-stu-id="27247-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="27247-224">Para obter informações detalhadas, confira [adicionar armazenamento](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="27247-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="27247-225">As duas máquinas virtuais precisam de pelo menos dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="27247-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="27247-226">Anexe discos brutos - não discos formatado com NTFS.</span><span class="sxs-lookup"><span data-stu-id="27247-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="27247-227">Se anexar discos formatados com NTFS, você só poderá habilitar S2D sem verificação de qualificação do disco.</span><span class="sxs-lookup"><span data-stu-id="27247-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="27247-228">Anexe um mínimo de dois tooeach de armazenamento Premium (discos SSD) VM.</span><span class="sxs-lookup"><span data-stu-id="27247-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="27247-229">É recomendável ter pelo menos discos P30 (1 TB).</span><span class="sxs-lookup"><span data-stu-id="27247-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="27247-230">Host de conjunto de cache muito**somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="27247-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="27247-231">capacidade de armazenamento Olá que usar em ambientes de produção depende de sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="27247-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="27247-232">valores de saudação descritos neste artigo são para teste e demonstração.</span><span class="sxs-lookup"><span data-stu-id="27247-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="27247-233">[Adicionar máquinas virtuais de saudação tooyour domínio pré-existente](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="27247-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="27247-234">Depois de máquinas virtuais de saudação sejam criadas e configuradas, você pode configurar o cluster de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="27247-235">Etapa 2: Configurar Olá Cluster de Failover do Windows com S2D</span><span class="sxs-lookup"><span data-stu-id="27247-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="27247-236">Olá próxima etapa é o cluster de failover de saudação tooconfigure com S2D.</span><span class="sxs-lookup"><span data-stu-id="27247-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="27247-237">Nesta etapa, você fará Olá subetapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27247-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="27247-238">Adicionar o recurso Clustering de Failover do Windows</span><span class="sxs-lookup"><span data-stu-id="27247-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="27247-239">Validar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="27247-239">Validate hello cluster</span></span>
1. <span data-ttu-id="27247-240">Criar o cluster de failover Olá</span><span class="sxs-lookup"><span data-stu-id="27247-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="27247-241">Criar a testemunha de nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="27247-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="27247-242">Adicionar armazenamento</span><span class="sxs-lookup"><span data-stu-id="27247-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="27247-243">Adicionar o recurso Clustering de Failover do Windows</span><span class="sxs-lookup"><span data-stu-id="27247-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="27247-244">toobegin, conecte-se a máquina virtual da primeira toohello com RDP usando uma conta de domínio que é um membro do grupo local Administradores e objetos de toocreate permissões no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27247-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="27247-245">Use essa conta para o restante da saudação da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="27247-246">[Adicionar o Clustering de Failover máquina de virtual do recurso tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="27247-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="27247-247">recurso de cluster de Failover de tooinstall de saudação da interface do usuário, Olá seguindo as etapas em ambas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="27247-248">Em **Gerenciador de Servidor**, clique em **Gerenciar** e clique em **Adicionar Funções e Recursos**.</span><span class="sxs-lookup"><span data-stu-id="27247-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="27247-249">Em **assistente Adicionar funções e recursos**, clique em **próximo** até chegar muito**selecionar recursos**.</span><span class="sxs-lookup"><span data-stu-id="27247-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="27247-250">Em **Selecionar Recursos**, clique em **Clustering de Failover**.</span><span class="sxs-lookup"><span data-stu-id="27247-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="27247-251">Inclua todos os recursos necessários e ferramentas de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="27247-252">Clique em **Adicionar Recursos**.</span><span class="sxs-lookup"><span data-stu-id="27247-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="27247-253">Clique em **próximo** e, em seguida, clique em **concluir** tooinstall recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="27247-254">tooinstall Olá recurso cluster de Failover com o PowerShell, execute Olá script a partir de uma sessão do PowerShell de administrador a seguir em uma das máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="27247-255">Para referência, as próximas etapas Olá siga instruções de saudação na etapa 3 do [solução convergida Hyper usando espaços de armazenamento diretos no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="27247-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="27247-256">Validar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="27247-256">Validate hello cluster</span></span>

<span data-ttu-id="27247-257">Este guia se refere a tooinstructions em [validar cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="27247-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="27247-258">Valide cluster Olá em Olá da interface do usuário ou com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27247-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="27247-259">cluster de saudação toovalidate com hello da interface do usuário, Olá seguindo as etapas de uma das máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="27247-260">Em **Gerenciador do Servidor**, clique em **Ferramentas** e clique em **Gerenciador de Cluster de Failover**.</span><span class="sxs-lookup"><span data-stu-id="27247-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="27247-261">Em **Gerenciador de Cluster de Failover**, clique em **Ação** e clique em **Validar Configuração...**.</span><span class="sxs-lookup"><span data-stu-id="27247-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="27247-262">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27247-262">Click **Next**.</span></span>
1. <span data-ttu-id="27247-263">Em **selecionar servidores ou um Cluster**, nome de tipo de saudação de ambas as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="27247-264">Em **Opções de teste**, escolha **Executar apenas os testes selecionados**.</span><span class="sxs-lookup"><span data-stu-id="27247-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="27247-265">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27247-265">Click **Next**.</span></span>
1. <span data-ttu-id="27247-266">Em **Testar seleção**, inclua todos os testes, exceto **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="27247-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="27247-267">Consulte Olá figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="27247-267">See hello following picture:</span></span>

   ![Validar Testes](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="27247-269">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27247-269">Click **Next**.</span></span>
1. <span data-ttu-id="27247-270">Em **Confirmação**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27247-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="27247-271">Olá **validar um Assistente de configuração** Olá de execuções de testes de validação.</span><span class="sxs-lookup"><span data-stu-id="27247-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="27247-272">cluster de saudação toovalidate com o PowerShell, execute Olá script a partir de uma sessão do PowerShell de administrador a seguir em uma das máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="27247-273">Depois de validar cluster hello, crie o cluster de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="27247-274">Criar o cluster de failover Olá</span><span class="sxs-lookup"><span data-stu-id="27247-274">Create hello failover cluster</span></span>

<span data-ttu-id="27247-275">Este guia refere-se muito[criar cluster de failover Olá](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="27247-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="27247-276">cluster de failover do toocreate hello, você precisa:</span><span class="sxs-lookup"><span data-stu-id="27247-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="27247-277">nomes de saudação de máquinas virtuais de saudação que se tornam Olá nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="27247-278">Um nome de cluster de failover Olá</span><span class="sxs-lookup"><span data-stu-id="27247-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="27247-279">Um endereço IP de cluster de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="27247-280">Você pode usar um endereço IP que não é usado em Olá mesma rede virtual do Azure e sub-redes Olá nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="27247-281">Olá PowerShell a seguir cria um cluster de failover.</span><span class="sxs-lookup"><span data-stu-id="27247-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="27247-282">Atualizar o script hello com nomes de saudação de nós de saudação (nomes de máquina virtual de saudação) e um endereço IP disponível do hello VNET do Azure:</span><span class="sxs-lookup"><span data-stu-id="27247-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="27247-283">Criar uma testemunha de nuvem</span><span class="sxs-lookup"><span data-stu-id="27247-283">Create a cloud witness</span></span>

<span data-ttu-id="27247-284">A Testemunha de Nuvem é um novo tipo de testemunha de quorum de cluster armazenado em um Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="27247-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="27247-285">Isso elimina a necessidade de saudação de uma VM separada que hospeda uma testemunha de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="27247-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="27247-286">[Criar uma testemunha de nuvem para o cluster de failover Olá](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="27247-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="27247-287">Criar um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="27247-287">Create a blob container.</span></span>

1. <span data-ttu-id="27247-288">Salve as chaves de acesso de saudação e URL do contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="27247-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="27247-289">Configure testemunha de quorum de cluster do hello failover cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="27247-290">Consulte a [configurar testemunha de quorum de saudação na interface do usuário Olá]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) no hello da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="27247-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="27247-291">Adicionar armazenamento</span><span class="sxs-lookup"><span data-stu-id="27247-291">Add storage</span></span>

<span data-ttu-id="27247-292">discos Olá S2D necessário toobe vazias e sem partições ou outros dados.</span><span class="sxs-lookup"><span data-stu-id="27247-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="27247-293">Siga os discos tooclean [Olá as etapas neste guia](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="27247-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="27247-294">[Habilitar Espaços de Armazenamento Diretos \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="27247-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="27247-295">Olá PowerShell a seguir permite que os espaços de armazenamento direct.</span><span class="sxs-lookup"><span data-stu-id="27247-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="27247-296">Em **Gerenciador de Cluster de Failover**, agora você pode ver o pool de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="27247-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="27247-297">[Criar um volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="27247-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="27247-298">Um dos recursos de saudação do S2D é que ele cria automaticamente um pool de armazenamento quando você habilitá-la.</span><span class="sxs-lookup"><span data-stu-id="27247-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="27247-299">Agora você está pronto toocreate um volume.</span><span class="sxs-lookup"><span data-stu-id="27247-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="27247-300">Olá commandlet PowerShell `New-Volume` automatiza o processo de criação de volume hello, incluindo formatação, adicionar cluster toohello e criação de um volume compartilhado de cluster (CSV).</span><span class="sxs-lookup"><span data-stu-id="27247-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="27247-301">saudação de exemplo a seguir cria um 800 GB (gigabyte) CSV.</span><span class="sxs-lookup"><span data-stu-id="27247-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="27247-302">Após a conclusão do comando, um volume de 800 GB é montado como um recurso de cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="27247-303">volume Hello está em `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="27247-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="27247-304">Olá diagrama a seguir mostra um volume compartilhado de cluster com S2D:</span><span class="sxs-lookup"><span data-stu-id="27247-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="27247-306">Etapa 3: Testar o failover do cluster de failover</span><span class="sxs-lookup"><span data-stu-id="27247-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="27247-307">No Gerenciador de Cluster de Failover, verifique se que você pode mover Olá toohello de recursos de armazenamento a outro nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="27247-308">Se você puder se conectar de cluster de failover toohello com **Gerenciador de Cluster de Failover** e mover o armazenamento de saudação de toohello um nó para outro, você estará pronto tooconfigure Olá FCI.</span><span class="sxs-lookup"><span data-stu-id="27247-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="27247-309">Etapa 4: criar FCI do SQL Server</span><span class="sxs-lookup"><span data-stu-id="27247-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="27247-310">Depois que você configurou o cluster de failover hello e todos os componentes do cluster, incluindo o armazenamento, você pode criar hello FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="27247-311">Conecte a máquina virtual da primeira toohello com RDP.</span><span class="sxs-lookup"><span data-stu-id="27247-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="27247-312">Em **Gerenciador de Cluster de Failover**, verifique se todos os recursos principais de cluster estão na primeira máquina virtual do hello.</span><span class="sxs-lookup"><span data-stu-id="27247-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="27247-313">Se necessário, mova todos os recursos toothis VM.</span><span class="sxs-lookup"><span data-stu-id="27247-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="27247-314">Localize a mídia de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-314">Locate hello installation media.</span></span> <span data-ttu-id="27247-315">Se a máquina virtual de saudação usa uma das imagens do Azure Marketplace hello, mídia hello está localizada em `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="27247-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="27247-316">Clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="27247-316">Click **Setup**.</span></span>

1. <span data-ttu-id="27247-317">Em Olá **Central de instalação do SQL Server**, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="27247-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="27247-318">Clique em **Nova instalação de cluster de failover do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="27247-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="27247-319">Siga as instruções de Olá Olá tooinstall de assistente Olá FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="27247-320">diretórios de dados do Hello FCI necessário toobe no armazenamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="27247-321">Com S2D, não é um disco compartilhado, mas um volume de tooa de ponto de montagem em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="27247-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="27247-322">S2D sincroniza volume Olá entre os dois nós.</span><span class="sxs-lookup"><span data-stu-id="27247-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="27247-323">volume de saudação é apresentado toohello cluster como um volume compartilhado de cluster.</span><span class="sxs-lookup"><span data-stu-id="27247-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="27247-324">Use o ponto de montagem CSV de saudação para diretórios de dados hello.</span><span class="sxs-lookup"><span data-stu-id="27247-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="27247-326">Depois de concluir o Assistente de saudação, a instalação instalará um FCI do SQL Server no primeiro nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="27247-327">Após a instalação com êxito Olá FCI no primeiro nó de hello, conecte-se toohello segundo nó ao RDP.</span><span class="sxs-lookup"><span data-stu-id="27247-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="27247-328">Olá abrir **Central de instalação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="27247-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="27247-329">Clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="27247-329">Click **Installation**.</span></span>

1. <span data-ttu-id="27247-330">Clique em **cluster de failover do SQL Server do adicionar nó tooa**.</span><span class="sxs-lookup"><span data-stu-id="27247-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="27247-331">Siga as instruções de Olá Olá Assistente tooinstall SQL servidor e adicione toohello esse servidor FCI.</span><span class="sxs-lookup"><span data-stu-id="27247-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="27247-332">Se você usou uma imagem da Galeria do Azure Marketplace com o SQL Server, ferramentas do SQL Server foram incluídas com a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="27247-333">Se você não usou essa imagem, instale ferramentas do SQL Server Olá separadamente.</span><span class="sxs-lookup"><span data-stu-id="27247-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="27247-334">Confira [Baixar o SSMS (SQL Server Management Studio)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="27247-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="27247-335">Etapa 5: criar o balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="27247-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="27247-336">Em máquinas virtuais do Azure, os clusters usam um balanceador de carga toohold um endereço IP que precisa toobe em um nó de cluster por vez.</span><span class="sxs-lookup"><span data-stu-id="27247-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="27247-337">Nesta solução, o balanceador de carga Olá contém endereço IP Olá Olá FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="27247-338">[Criar e configurar um balanceador de carga do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="27247-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="27247-339">Criar balanceador de carga Olá Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="27247-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="27247-340">Balanceador de carga de saudação toocreate:</span><span class="sxs-lookup"><span data-stu-id="27247-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="27247-341">No hello portal do Azure, vá toohello grupo de recursos com máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="27247-342">Clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27247-342">Click **+ Add**.</span></span> <span data-ttu-id="27247-343">Saudação de pesquisa Marketplace para **balanceador de carga**.</span><span class="sxs-lookup"><span data-stu-id="27247-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="27247-344">Clique em **Balanceador de Carga**.</span><span class="sxs-lookup"><span data-stu-id="27247-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="27247-345">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27247-345">Click **Create**.</span></span>

1. <span data-ttu-id="27247-346">Configure o balanceador de carga de saudação com:</span><span class="sxs-lookup"><span data-stu-id="27247-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="27247-347">**Nome**: um nome que identifica o balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="27247-348">**Tipo**: balanceador de carga Olá pode ser público ou privado.</span><span class="sxs-lookup"><span data-stu-id="27247-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="27247-349">Um balanceador de carga privadas pode ser acessado de dentro Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="27247-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="27247-350">A maioria dos aplicativos do Azure pode usar um balanceador de carga privado.</span><span class="sxs-lookup"><span data-stu-id="27247-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="27247-351">Se seu aplicativo precisa de acesso tooSQL Server diretamente pela Internet de hello, use um balanceador de carga público.</span><span class="sxs-lookup"><span data-stu-id="27247-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="27247-352">**Rede virtual**: Olá mesma rede como máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="27247-353">**Subrede**: Olá mesma sub-rede que máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="27247-354">**Endereço IP privado**: Olá mesmo endereço IP que você atribuiu o recurso de rede de cluster toohello FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="27247-355">**assinatura**: sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="27247-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="27247-356">**Grupo de recursos**: Use Olá mesmo grupo de recursos que as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="27247-357">**Local**: Use Olá mesmo local do Azure que suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="27247-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="27247-358">Consulte Olá figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="27247-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="27247-360">Configurar o pool de back-end do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="27247-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="27247-361">Retornar toohello grupo de recursos do Azure com máquinas virtuais de saudação e localize o balanceador de carga novo hello.</span><span class="sxs-lookup"><span data-stu-id="27247-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="27247-362">Você pode ter o modo de exibição de saudação toorefresh em Olá grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27247-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="27247-363">Clique o balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="27247-364">Na folha de Balanceador de carga hello, clique em **pools de back-end**.</span><span class="sxs-lookup"><span data-stu-id="27247-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="27247-365">Clique em **+ adicionar** tooadd um pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="27247-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="27247-366">Digite um nome para o pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="27247-367">Clique em **Adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="27247-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="27247-368">Em Olá **escolha máquinas virtuais** folha, clique em **escolher um conjunto de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="27247-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="27247-369">Escolha o conjunto de disponibilidade de saudação que você colocou Olá máquinas de virtuais do SQL Server em.</span><span class="sxs-lookup"><span data-stu-id="27247-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="27247-370">Em Olá **escolha máquinas virtuais** folha, clique em **escolha máquinas virtuais de saudação**.</span><span class="sxs-lookup"><span data-stu-id="27247-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="27247-371">Seu portal do Azure deve ter aparência Olá figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="27247-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="27247-373">Clique em **selecione** em Olá **escolha máquinas virtuais** folha.</span><span class="sxs-lookup"><span data-stu-id="27247-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="27247-374">Clique em **OK** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="27247-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="27247-375">Configurar um teste de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="27247-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="27247-376">Na folha de Balanceador de carga hello, clique em **sondas de integridade**.</span><span class="sxs-lookup"><span data-stu-id="27247-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="27247-377">Clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27247-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="27247-378">Em Olá **investigação de integridade de adicionar** folha, <a name="probe"> </a>definir parâmetros de teste de integridade hello:</span><span class="sxs-lookup"><span data-stu-id="27247-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="27247-379">**Nome**: um nome para a investigação de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="27247-380">**Protocolo**: TCP.</span><span class="sxs-lookup"><span data-stu-id="27247-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="27247-381">**Porta**: definir tooan porta TCP disponível.</span><span class="sxs-lookup"><span data-stu-id="27247-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="27247-382">Essa porta exige uma porta de firewall aberta.</span><span class="sxs-lookup"><span data-stu-id="27247-382">This port requires an open firewall port.</span></span> <span data-ttu-id="27247-383">Saudação de uso [mesma porta](#ports) definido para a investigação de integridade Olá no firewall hello.</span><span class="sxs-lookup"><span data-stu-id="27247-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="27247-384">**Intervalo**: 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="27247-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="27247-385">**Limite não íntegro**: duas falhas consecutivas.</span><span class="sxs-lookup"><span data-stu-id="27247-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="27247-386">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="27247-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="27247-387">Definir regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="27247-387">Set load balancing rules</span></span>

1. <span data-ttu-id="27247-388">Na folha de Balanceador de carga hello, clique em **regras de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="27247-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="27247-389">Clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27247-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="27247-390">Definir parâmetros de regras de balanceamento da carga de saudação:</span><span class="sxs-lookup"><span data-stu-id="27247-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="27247-391">**Nome**: um nome para as regras de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="27247-392">**Endereço IP de Frontend**: Use o endereço IP Olá Olá recursos de rede de cluster FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="27247-393">**Porta**: definido para Olá porta TCP do SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="27247-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="27247-394">porta de instância saudação padrão é 1433.</span><span class="sxs-lookup"><span data-stu-id="27247-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="27247-395">**Porta de back-end**: este valor usa Olá mesma porta como Olá **porta** valor quando você habilitar **IP flutuante (retorno de servidor direto)**.</span><span class="sxs-lookup"><span data-stu-id="27247-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="27247-396">**Pool de back-end**: Use Olá back-end nome do pool que você configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27247-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="27247-397">**Investigação de integridade**: investigação de integridade de saudação de uso que você configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27247-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="27247-398">**Persistência de sessão**: nenhuma.</span><span class="sxs-lookup"><span data-stu-id="27247-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="27247-399">**Tempo limite de ociosidade (minutos)**: 4.</span><span class="sxs-lookup"><span data-stu-id="27247-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="27247-400">**IP flutuante (retorno de servidor direto)**: habilitado</span><span class="sxs-lookup"><span data-stu-id="27247-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="27247-401">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27247-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="27247-402">Etapa 6: configurar o cluster para investigação</span><span class="sxs-lookup"><span data-stu-id="27247-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="27247-403">Defina o parâmetro de porta de investigação de cluster hello no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27247-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="27247-404">tooset Olá parâmetro de porta de investigação de cluster, atualize as variáveis no hello script a seguir do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="27247-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="27247-405">Etapa 7: testar o failover de FCI</span><span class="sxs-lookup"><span data-stu-id="27247-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="27247-406">Failover de teste de saudação funcionalidade do cluster toovalidate FCI.</span><span class="sxs-lookup"><span data-stu-id="27247-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="27247-407">Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="27247-407">Do hello following steps:</span></span>

1. <span data-ttu-id="27247-408">Conecte-se tooone Olá FCI do SQL Server de nós de cluster com o RDP.</span><span class="sxs-lookup"><span data-stu-id="27247-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="27247-409">Abra o **Gerenciador de Cluster de Failover**.</span><span class="sxs-lookup"><span data-stu-id="27247-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="27247-410">Clique em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="27247-410">Click **Roles**.</span></span> <span data-ttu-id="27247-411">Aviso de nó que possui a função de FCI do SQL Server de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="27247-412">Clique a função do hello FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="27247-413">Clique em **Mover** e em **Melhor Nó Possível**.</span><span class="sxs-lookup"><span data-stu-id="27247-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="27247-414">**Gerenciador de Cluster de failover** mostra Olá função e seus recursos offline.</span><span class="sxs-lookup"><span data-stu-id="27247-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="27247-415">Olá recursos, em seguida, mover e ficar online Olá no outro nó.</span><span class="sxs-lookup"><span data-stu-id="27247-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="27247-416">Testar a conectividade</span><span class="sxs-lookup"><span data-stu-id="27247-416">Test connectivity</span></span>

<span data-ttu-id="27247-417">conectividade de tootest log na máquina virtual tooanother Olá mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="27247-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="27247-418">Abra **SQL Server Management Studio** e conecte-se o nome do toohello FCI do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="27247-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="27247-419">Se necessário, você pode [baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="27247-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="27247-420">Limitações</span><span class="sxs-lookup"><span data-stu-id="27247-420">Limitations</span></span>
<span data-ttu-id="27247-421">Em máquinas virtuais do Azure, o coordenador de transações distribuídas (DTC) da Microsoft não é suportado em FCIs porque Olá porta RPC não é suportado pelo Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="27247-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="27247-422">Consulte também</span><span class="sxs-lookup"><span data-stu-id="27247-422">See Also</span></span>

[<span data-ttu-id="27247-423">Instalação S2D com área de trabalho remota (Azure)</span><span class="sxs-lookup"><span data-stu-id="27247-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="27247-424">[Solução hiperconvergida com espaços de armazenamento diretos](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="27247-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="27247-425">Visão geral direta de espaço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="27247-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="27247-426">Suporte do SQL Server para S2D</span><span class="sxs-lookup"><span data-stu-id="27247-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
