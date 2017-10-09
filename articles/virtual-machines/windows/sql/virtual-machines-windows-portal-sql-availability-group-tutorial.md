---
title: "Grupos de disponibilidade de servidor - máquinas virtuais do Azure - Tutorial de aaaSQL | Microsoft Docs"
description: "Este tutorial mostra como toocreate um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="afe55-103">Configurar grupos de disponibilidade Sempre ativo na VM do Azure manualmente</span><span class="sxs-lookup"><span data-stu-id="afe55-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="afe55-104">Este tutorial mostra como toocreate um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="afe55-105">tutorial completo Olá cria um grupo de disponibilidade com uma réplica de banco de dados em dois servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="afe55-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="afe55-106">**Tempo estimado**: leva aproximadamente 30 minutos toocomplete depois Olá pré-requisitos forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="afe55-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="afe55-107">diagrama de saudação ilustra o que você cria no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="afe55-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="afe55-109">Prerequisites</span></span>

<span data-ttu-id="afe55-110">tutorial de saudação pressupõe que você tem uma compreensão básica do SQL Server AlwaysOn em grupos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="afe55-111">Se você precisa saber mais, confira [Visão geral dos Grupos de Disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="afe55-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="afe55-112">Olá tabela a seguir lista os pré-requisitos de saudação que você precisa toocomplete antes de iniciar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="afe55-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="afe55-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="afe55-113">Requirement</span></span> |<span data-ttu-id="afe55-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="afe55-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="afe55-116">Dois servidores SQL</span><span class="sxs-lookup"><span data-stu-id="afe55-116">Two SQL Servers</span></span> | <span data-ttu-id="afe55-117">-Em um conjunto de disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="afe55-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="afe55-118">-Em um único domínio</span><span class="sxs-lookup"><span data-stu-id="afe55-118">- In a single domain</span></span> <br/> <span data-ttu-id="afe55-119">-Com o recurso Cluster de Failover instalado</span><span class="sxs-lookup"><span data-stu-id="afe55-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="afe55-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="afe55-121">Windows Server</span></span> | <span data-ttu-id="afe55-122">Compartilhamento de arquivos para a testemunha do cluster</span><span class="sxs-lookup"><span data-stu-id="afe55-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="afe55-124">Conta de serviço do SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-124">SQL Server service account</span></span> | <span data-ttu-id="afe55-125">Conta do domínio</span><span class="sxs-lookup"><span data-stu-id="afe55-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="afe55-127">Conta do serviço SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="afe55-127">SQL Server Agent service account</span></span> | <span data-ttu-id="afe55-128">Conta do domínio</span><span class="sxs-lookup"><span data-stu-id="afe55-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="afe55-130">Portas de firewall abertas</span><span class="sxs-lookup"><span data-stu-id="afe55-130">Firewall ports open</span></span> | <span data-ttu-id="afe55-131">- SQL Server: **1433** para instância padrão</span><span class="sxs-lookup"><span data-stu-id="afe55-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="afe55-132">- Ponto de extremidade de espelhamento de banco de dados: **5022** ou outra porta disponível</span><span class="sxs-lookup"><span data-stu-id="afe55-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="afe55-133">- Investigação do Azure Load Balancer: **59999** ou outra porta disponível</span><span class="sxs-lookup"><span data-stu-id="afe55-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="afe55-135">Adicionar o recurso Cluster de Failover à VM</span><span class="sxs-lookup"><span data-stu-id="afe55-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="afe55-136">Os dois SQL Servers precisam desse recurso</span><span class="sxs-lookup"><span data-stu-id="afe55-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="afe55-138">Conta do domínio de instalação</span><span class="sxs-lookup"><span data-stu-id="afe55-138">Installation domain account</span></span> | <span data-ttu-id="afe55-139">- Administrador local em cada SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="afe55-140">- Membro da função de servidor fixa sysadmin do SQL Server para cada instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="afe55-141">Antes de começar o tutorial Olá, é necessário muito[concluir os pré-requisitos para a criação de grupos de disponibilidade AlwaysOn em máquinas virtuais Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="afe55-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="afe55-142">Se esses pré-requisitos forem concluídos já, você pode ir muito[criar Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="afe55-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="afe55-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="afe55-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="afe55-144">Após Olá pré-requisitos forem concluídos, Olá primeira etapa é toocreate um Cluster de Failover do Windows Server que inclui dois SQL Servers e um servidor testemunha.</span><span class="sxs-lookup"><span data-stu-id="afe55-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="afe55-145">RDP toohello primeiro do SQL Server usando uma conta de domínio que seja um administrador nos servidores SQL e o servidor de testemunha hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="afe55-146">Se você seguiu Olá [documento de pré-requisitos](virtual-machines-windows-portal-sql-availability-group-prereq.md), você criou uma conta chamada **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="afe55-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="afe55-147">Use essa conta.</span><span class="sxs-lookup"><span data-stu-id="afe55-147">Use this account.</span></span>

2. <span data-ttu-id="afe55-148">Em Olá **Gerenciador do servidor** painel, selecione **ferramentas**e, em seguida, clique em **Gerenciador de Cluster de Failover**.</span><span class="sxs-lookup"><span data-stu-id="afe55-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="afe55-149">No painel esquerdo do hello, clique com botão direito **Gerenciador de Cluster de Failover**e, em seguida, clique em **criar um Cluster**.</span><span class="sxs-lookup"><span data-stu-id="afe55-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="afe55-150">![Criar cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="afe55-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="afe55-151">No hello Assistente para criação de Cluster, crie um cluster de um nó percorrendo as páginas de saudação com configurações Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="afe55-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="afe55-152">Página</span><span class="sxs-lookup"><span data-stu-id="afe55-152">Page</span></span> | <span data-ttu-id="afe55-153">Configurações</span><span class="sxs-lookup"><span data-stu-id="afe55-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="afe55-154">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="afe55-154">Before You Begin</span></span> |<span data-ttu-id="afe55-155">Usar padrões</span><span class="sxs-lookup"><span data-stu-id="afe55-155">Use defaults</span></span> |
   | <span data-ttu-id="afe55-156">Selecionar Servidores</span><span class="sxs-lookup"><span data-stu-id="afe55-156">Select Servers</span></span> |<span data-ttu-id="afe55-157">Saudação de tipo SQL Server primeiro nome no **digite o nome do servidor** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="afe55-158">Aviso de Validação</span><span class="sxs-lookup"><span data-stu-id="afe55-158">Validation Warning</span></span> |<span data-ttu-id="afe55-159">Selecione **n º eu não precisar do suporte da Microsoft para este cluster e, portanto, não quiser que a validação de saudação toorun testes. Quando clico em Avançar, continuo a criar o cluster Olá**.</span><span class="sxs-lookup"><span data-stu-id="afe55-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="afe55-160">Ponto de acesso para administrar Olá Cluster</span><span class="sxs-lookup"><span data-stu-id="afe55-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="afe55-161">Digite um nome de cluster, por exemplo, **SQLAGCluster1** em **Nome do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="afe55-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="afe55-162">Confirmação</span><span class="sxs-lookup"><span data-stu-id="afe55-162">Confirmation</span></span> |<span data-ttu-id="afe55-163">Use os padrões, a menos que você esteja usando Espaços de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="afe55-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="afe55-164">Consulte Olá Observação Após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="afe55-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="afe55-165">Definir o endereço IP do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="afe55-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="afe55-166">Em **Gerenciador de Cluster de Failover**, role para baixo demais**recursos principais de Cluster** e expanda detalhes do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="afe55-167">Você deverá ver dois Olá **nome** e hello **endereço IP** recursos Olá **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="afe55-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="afe55-168">Hello recurso de endereço IP não pode ser colocado online porque o cluster Olá recebeu Olá mesmo endereço IP como máquina Olá em si, portanto, ele é um endereço duplicado.</span><span class="sxs-lookup"><span data-stu-id="afe55-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="afe55-169">Com o botão direito Olá falhado **endereço IP** recursos e depois clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="afe55-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Propriedades do Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="afe55-171">Selecione **endereço IP estático** e especifique um endereço disponível na sub-rede onde saudação do SQL Server está na caixa de texto endereço hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="afe55-172">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="afe55-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="afe55-173">Em Olá **recursos principais de Cluster** seção, clique o nome do cluster e clique em **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="afe55-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="afe55-174">Em seguida, aguarde até que ambos os recursos estejam online.</span><span class="sxs-lookup"><span data-stu-id="afe55-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="afe55-175">Quando o recurso de nome de cluster Olá fica online, ele atualiza o servidor de DC Olá com uma nova conta de computador do AD.</span><span class="sxs-lookup"><span data-stu-id="afe55-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="afe55-176">Use esta saudação de toorun AD conta Serviço de cluster do grupo de disponibilidade mais tarde.</span><span class="sxs-lookup"><span data-stu-id="afe55-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="afe55-177"><a name="addNode"></a>Adicionar Olá outros toocluster do SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="afe55-178">Adicionar Olá outro cluster de toohello do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="afe55-179">Na árvore do navegador hello, mouse cluster hello e clique em **adicionar nó**.</span><span class="sxs-lookup"><span data-stu-id="afe55-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Adicionar nó toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="afe55-181">Em Olá **Assistente para adicionar nó**, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="afe55-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="afe55-182">Em Olá **selecionar servidores** página, adicione Olá segundo servidor do SQL.</span><span class="sxs-lookup"><span data-stu-id="afe55-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="afe55-183">Nome do servidor de saudação tipo na **digite o nome do servidor** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="afe55-184">Quando terminar, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="afe55-185">Em Olá **aviso de validação** , clique em **não** (em um cenário de produção, você deve executar testes de validação de saudação).</span><span class="sxs-lookup"><span data-stu-id="afe55-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="afe55-186">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="afe55-187">Em Olá **confirmação** página se você estiver usando espaços de armazenamento, Olá desmarque a caixa de seleção **adicionar todos os cluster toohello de armazenamento qualificado.**</span><span class="sxs-lookup"><span data-stu-id="afe55-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Adicionar Confirmação do Nó](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="afe55-189">Se você estiver usando espaços de armazenamento e não desmarque **adicionar todos os armazenamento qualificado ao cluster toohello**, Windows desanexa discos virtuais Olá durante a saudação processo de clustering.</span><span class="sxs-lookup"><span data-stu-id="afe55-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="afe55-190">Como resultado, eles não aparecem no Gerenciador de discos até que os espaços de armazenamento Olá são removidos do cluster hello e reanexados usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afe55-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="afe55-191">Espaços de armazenamento agrupam vários discos em pools de toostorage.</span><span class="sxs-lookup"><span data-stu-id="afe55-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="afe55-192">Para obter mais informações, consulte [Espaços de Armazenamento](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="afe55-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="afe55-193">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-193">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-194">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="afe55-194">Click **Finish**.</span></span>

   <span data-ttu-id="afe55-195">Gerenciador de Cluster de failover mostra que o cluster tem um novo nó e a lista em Olá **nós** contêiner.</span><span class="sxs-lookup"><span data-stu-id="afe55-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="afe55-196">Faça logoff da sessão de área de trabalho remota hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="afe55-197">Adicionar um compartilhamento de arquivos de quorum de cluster</span><span class="sxs-lookup"><span data-stu-id="afe55-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="afe55-198">Neste exemplo o cluster do Windows hello usa um compartilhamento de arquivo toocreate um quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="afe55-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="afe55-199">Este tutorial usa um quorum Maioria de Compartilhamento de Arquivos e Nós.</span><span class="sxs-lookup"><span data-stu-id="afe55-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="afe55-200">Para saber mais, confira [Noções básicas sobre configurações de quorum em um cluster de failover](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="afe55-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="afe55-201">Conecte o servidor de membro de testemunha de compartilhamento de arquivo toohello com uma sessão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="afe55-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="afe55-202">No **Gerenciador do Servidor**, clique em **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="afe55-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="afe55-203">Abra **Gerenciamento do Computador**.</span><span class="sxs-lookup"><span data-stu-id="afe55-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="afe55-204">Clique em **Pastas Compartilhadas**.</span><span class="sxs-lookup"><span data-stu-id="afe55-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="afe55-205">Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .</span><span class="sxs-lookup"><span data-stu-id="afe55-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="afe55-207">Use **criar um Assistente de pasta compartilhada** toocreate um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="afe55-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="afe55-208">Em **caminho da pasta**, clique em **procurar** e localizar ou criar um caminho de pasta compartilhada hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="afe55-209">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-209">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-210">Em **nome, descrição e configurações** Verifique se o nome de compartilhamento de saudação e o caminho.</span><span class="sxs-lookup"><span data-stu-id="afe55-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="afe55-211">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-211">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-212">Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="afe55-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="afe55-213">Clique em **Personalizar...**.</span><span class="sxs-lookup"><span data-stu-id="afe55-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="afe55-214">Em **Personalizar Permissões**, clique em **Adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="afe55-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="afe55-215">Verifique se o cluster Olá Olá conta usada toocreate tem controle total.</span><span class="sxs-lookup"><span data-stu-id="afe55-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="afe55-217">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="afe55-217">Click **OK**.</span></span>

1. <span data-ttu-id="afe55-218">Em **Permissões de Pasta Compartilhada**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="afe55-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="afe55-219">Clique em **Concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="afe55-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="afe55-220">Faça logoff do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="afe55-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="afe55-221">Configurar quorum do cluster</span><span class="sxs-lookup"><span data-stu-id="afe55-221">Configure cluster quorum</span></span>

<span data-ttu-id="afe55-222">Em seguida, configure o quorum do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="afe55-223">Conecte-se toohello primeiro nó de cluster com área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="afe55-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="afe55-224">Em **Gerenciador de Cluster de Failover**, clique com botão direito cluster hello, aponte muito**mais ações**e clique em **Configurar Quorum do Cluster...** .</span><span class="sxs-lookup"><span data-stu-id="afe55-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="afe55-226">No **Assistente para Configurar Quorum do Cluster**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="afe55-227">Em **Selecionar opção de configuração de Quorum**, escolha **selecionar testemunha de quorum Olá**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="afe55-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="afe55-228">Em **Selecionar Testemunha de Quorum**, clique em **Configurar testemunha de compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="afe55-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="afe55-229">O Windows Server 2016 dá suporte a testemunha de nuvem.</span><span class="sxs-lookup"><span data-stu-id="afe55-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="afe55-230">Se você escolher esse tipo de testemunha, não precisará de testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="afe55-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="afe55-231">Para saber mais, confira [Implantar uma testemunha de nuvem para um Cluster de Failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="afe55-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="afe55-232">Este tutorial usa uma testemunha de compartilhamento de arquivos, o que tem suporte de sistemas operacionais anteriores.</span><span class="sxs-lookup"><span data-stu-id="afe55-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="afe55-233">Em **configurar testemunha de compartilhamento de arquivo**, digitar o caminho de saudação para compartilhamento Olá criado.</span><span class="sxs-lookup"><span data-stu-id="afe55-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="afe55-234">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-234">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-235">Verifique se as configurações de saudação em **confirmação**.</span><span class="sxs-lookup"><span data-stu-id="afe55-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="afe55-236">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-236">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-237">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="afe55-237">Click **Finish**.</span></span>

<span data-ttu-id="afe55-238">recursos de núcleo de cluster Olá são configurados com uma testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="afe55-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="afe55-239">Habilitar Grupos de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="afe55-239">Enable Availability Groups</span></span>

<span data-ttu-id="afe55-240">Em seguida, habilite Olá **grupos de disponibilidade do AlwaysOn** recurso.</span><span class="sxs-lookup"><span data-stu-id="afe55-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="afe55-241">Siga estas etapas em ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="afe55-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="afe55-242">De saudação **iniciar** tela, inicie **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="afe55-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="afe55-243">Na árvore do navegador de saudação, clique em **serviços SQL Server**, em seguida, clique com botão direito Olá **SQL Server (MSSQLSERVER)** de serviço e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="afe55-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="afe55-244">Clique em Olá **alta disponibilidade AlwaysOn** guia e, em seguida, selecione **habilitar grupos de disponibilidade do AlwaysOn**, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="afe55-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Habilitar Grupos de Disponibilidade AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="afe55-246">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-246">Click **Apply**.</span></span> <span data-ttu-id="afe55-247">Clique em **Okey** na caixa de diálogo pop-up hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="afe55-248">Reinicie o serviço do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="afe55-249">Repita essas etapas em Olá outros SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="afe55-250">Criar um banco de dados em Olá primeiro o SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="afe55-251">Iniciar Olá RDP arquivo toohello primeiro o SQL Server com um domínio de conta que é um membro da função sysadmin função de servidor fixa.</span><span class="sxs-lookup"><span data-stu-id="afe55-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="afe55-252">Abra o SQL Server Management Studio e conecte-se toohello primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="afe55-253">No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Bancos de Dados** e em **Novo Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="afe55-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="afe55-254">Em **Nome do banco de dados**, digite **MyDB1** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="afe55-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="afe55-255"><a name="backupshare"></a>Criar um compartilhamento de backup</span><span class="sxs-lookup"><span data-stu-id="afe55-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="afe55-256">Em Olá primeiro o SQL Server em **Gerenciador do servidor**, clique em **ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="afe55-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="afe55-257">Abra **Gerenciamento do Computador**.</span><span class="sxs-lookup"><span data-stu-id="afe55-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="afe55-258">Clique em **Pastas Compartilhadas**.</span><span class="sxs-lookup"><span data-stu-id="afe55-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="afe55-259">Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .</span><span class="sxs-lookup"><span data-stu-id="afe55-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="afe55-261">Use **criar um Assistente de pasta compartilhada** toocreate um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="afe55-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="afe55-262">Em **caminho da pasta**, clique em **procurar** e localizar ou criar um caminho de pasta compartilhada backup do banco de dados do hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="afe55-263">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-263">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-264">Em **nome, descrição e configurações** Verifique se o nome de compartilhamento de saudação e o caminho.</span><span class="sxs-lookup"><span data-stu-id="afe55-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="afe55-265">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-265">Click **Next**.</span></span>

1. <span data-ttu-id="afe55-266">Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="afe55-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="afe55-267">Clique em **Personalizar...**.</span><span class="sxs-lookup"><span data-stu-id="afe55-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="afe55-268">Em **Personalizar Permissões**, clique em **Adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="afe55-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="afe55-269">Certifique-se de que as contas de serviço do SQL Server e o SQL Server Agent de saudação para ambos os servidores têm controle total.</span><span class="sxs-lookup"><span data-stu-id="afe55-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="afe55-271">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="afe55-271">Click **OK**.</span></span>

1. <span data-ttu-id="afe55-272">Em **Permissões de Pasta Compartilhada**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="afe55-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="afe55-273">Clique em **Concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="afe55-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="afe55-274">Faça um backup de banco de dados de saudação completo</span><span class="sxs-lookup"><span data-stu-id="afe55-274">Take a full backup of hello database</span></span>

<span data-ttu-id="afe55-275">É necessário tooback backup Olá novo banco de dados tooinitialize Olá cadeia de logs.</span><span class="sxs-lookup"><span data-stu-id="afe55-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="afe55-276">Se você não faça um backup de banco de dados novo hello, ele não pode ser incluído em um grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="afe55-277">Em **Pesquisador de objetos**, clique o banco de dados hello, aponte muito**tarefas...** , clique em **backup**.</span><span class="sxs-lookup"><span data-stu-id="afe55-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="afe55-278">Clique em **Okey** tootake um local de backup padrão toohello backup completo.</span><span class="sxs-lookup"><span data-stu-id="afe55-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="afe55-279">Criar hello grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="afe55-279">Create hello Availability Group</span></span>
<span data-ttu-id="afe55-280">Agora você está pronto tooconfigure um grupo de disponibilidade usando Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="afe55-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="afe55-281">Criar um banco de dados em Olá primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="afe55-282">Faça um backup completo e um backup de log de transações do banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="afe55-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="afe55-283">Saudação de restauração completa e toohello de backups de log segundo do SQL Server com hello **NORECOVERY** opção</span><span class="sxs-lookup"><span data-stu-id="afe55-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="afe55-284">Criar hello grupo de disponibilidade (**AG1**) com confirmação síncrona, failover automático e réplicas secundárias legíveis</span><span class="sxs-lookup"><span data-stu-id="afe55-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="afe55-285">Crie hello grupo de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="afe55-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="afe55-286">Na sessão de área de trabalho remota toohello primeiro o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="afe55-287">Em **Pesquisador de Objetos** no SSMS, clique com o botão direito do mouse em **Alta Disponibilidade AlwaysOn** e clique em **Assistente de Novo Grupo de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="afe55-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Inicie o Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="afe55-289">Em Olá **Introdução** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="afe55-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="afe55-290">Em Olá **especificar nome do grupo de disponibilidade** página, digite um nome para Olá grupo de disponibilidade, por exemplo **AG1**, na **nome do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="afe55-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="afe55-291">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-291">Click **Next**.</span></span>

    ![Novo assistente de AG, especifique o nome do AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="afe55-293">Em Olá **Selecionar bancos de dados** , selecione o banco de dados e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="afe55-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="afe55-294">banco de dados de saudação atende aos pré-requisitos de saudação para um grupo de disponibilidade porque você ter obtido pelo menos um backup completo na réplica primária pretendida de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Novo assistente AG, selecione os bancos de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="afe55-296">Em Olá **especificar réplicas** , clique em **adicionar réplica**.</span><span class="sxs-lookup"><span data-stu-id="afe55-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Novo assistente AG, especifique as réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="afe55-298">Olá **conectar tooServer** caixa de diálogo será exibida.</span><span class="sxs-lookup"><span data-stu-id="afe55-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="afe55-299">Nome de saudação do tipo do segundo servidor de saudação em **nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="afe55-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="afe55-300">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-300">Click **Connect**.</span></span>

   <span data-ttu-id="afe55-301">Em Olá **especificar réplicas** página, você verá agora listado no segundo servidor de saudação **réplicas de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="afe55-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="afe55-302">Configure réplicas de saudação da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="afe55-302">Configure hello replicas as follows.</span></span>

   ![Novo assistente de AG, Especificar Réplicas (Completo)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="afe55-304">Clique em **pontos de extremidade** banco de dados do hello toosee ponto de extremidade de espelhamento para este grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="afe55-305">Olá Use mesma porta que você usou ao configurar Olá [regra de firewall para pontos de extremidade de espelhamento de banco de dados](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="afe55-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="afe55-307">Em Olá **selecionar sincronização de dados inicial** , selecione **completo** e especifique um local de rede compartilhada.</span><span class="sxs-lookup"><span data-stu-id="afe55-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="afe55-308">Para o local do hello, use Olá [compartilhamento de backup que você criou](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="afe55-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="afe55-309">No exemplo hello era, **\\\\\<primeiro servidor do SQL\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="afe55-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="afe55-310">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="afe55-311">Sincronização completa usa um backup completo do banco de dados de saudação na primeira instância de saudação do SQL Server e restaurá-lo toohello segunda instância.</span><span class="sxs-lookup"><span data-stu-id="afe55-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="afe55-312">Em caso de grandes bancos de dados, a sincronização completa não é recomendada porque pode levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="afe55-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="afe55-313">Você pode reduzir esse tempo manualmente fazer um backup de banco de dados de saudação e restaurando-o com `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="afe55-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="afe55-314">Se o banco de dados de saudação já é restaurado com `NO RECOVERY` em Olá segundo do SQL Server antes de configurar Olá grupo de disponibilidade, escolha **somente junção**.</span><span class="sxs-lookup"><span data-stu-id="afe55-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="afe55-315">Backup de saudação tootake depois de configurar Olá grupo de disponibilidade, escolha **ignorar sincronização de dados inicial**.</span><span class="sxs-lookup"><span data-stu-id="afe55-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="afe55-317">Em Olá **validação** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="afe55-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="afe55-318">Esta página deve ser semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="afe55-318">This page should look similar toohello following image:</span></span>

    ![Novo assistente AG, Validação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="afe55-320">Há um aviso para configuração de ouvinte Olá porque você não configurou um ouvinte de grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="afe55-321">Você pode ignorar este aviso porque em máquinas virtuais do Azure criar ouvinte Olá depois de criar o balanceador de carga do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="afe55-322">Em Olá **resumo** , clique em **concluir**, em seguida, aguarde enquanto o Assistente de saudação configura Olá novo grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="afe55-323">Em Olá **andamento** página, você pode clicar em **mais detalhes** tooview Olá detalhadas progresso.</span><span class="sxs-lookup"><span data-stu-id="afe55-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="afe55-324">Quando a saudação assistente for concluído, inspecione Olá **resultados** tooverify de página que Olá grupo de disponibilidade é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="afe55-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Novo assistente de AG, Resultados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="afe55-326">Clique em **fechar** tooexit Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="afe55-327">Saudação de verificação de grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="afe55-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="afe55-328">Em **Pesquisador de Objetos**, expanda **Alta Disponibilidade AlwaysOn** e expanda **Grupos de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="afe55-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="afe55-329">Agora você deve ver Olá novo grupo de disponibilidade neste contêiner.</span><span class="sxs-lookup"><span data-stu-id="afe55-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="afe55-330">Olá grupo de disponibilidade de mouse e clique em **Mostrar painel**.</span><span class="sxs-lookup"><span data-stu-id="afe55-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrar Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="afe55-332">O **painel AlwaysOn** deve ter aparência semelhante toothis.</span><span class="sxs-lookup"><span data-stu-id="afe55-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="afe55-334">Você pode ver réplicas hello, modo de failover Olá cada réplica e saudação do estado de sincronização.</span><span class="sxs-lookup"><span data-stu-id="afe55-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="afe55-335">No **Gerenciador de Cluster de Failover**, clique em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="afe55-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="afe55-336">Selecione **funções**.</span><span class="sxs-lookup"><span data-stu-id="afe55-336">Select **Roles**.</span></span> <span data-ttu-id="afe55-337">nome do grupo de disponibilidade Olá usado é uma função em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="afe55-338">Esse Grupo de Disponibilidade não tem um endereço IP para conexões de cliente porque você não configurou um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="afe55-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="afe55-339">Você irá configurar o ouvinte Olá depois de criar um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="afe55-341">Não tente toofail sobre Olá grupo de disponibilidade do hello Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="afe55-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="afe55-342">Todas as operações de failover devem ser executadas no **Painel AlwaysOn** no SSMS.</span><span class="sxs-lookup"><span data-stu-id="afe55-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="afe55-343">Para obter mais informações, consulte [restrições usando Olá Gerenciador de Cluster de Failover com grupos de disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="afe55-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="afe55-344">Agora você tem um Grupo de Disponibilidade com réplicas em duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afe55-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="afe55-345">Você pode mover Olá grupo de disponibilidade entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="afe55-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="afe55-346">Você não pode se conectar toohello grupo de disponibilidade ainda não tiver um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="afe55-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="afe55-347">Em máquinas virtuais do Azure, o ouvinte de saudação exige um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="afe55-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="afe55-348">Olá próxima etapa é toocreate balanceador de carga Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="afe55-349">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="afe55-349">Create an Azure load balancer</span></span>

<span data-ttu-id="afe55-350">Nas máquinas virtuais do Azure, um Grupo de Disponibilidade do SQL Server precisa de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="afe55-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="afe55-351">Balanceador de carga Olá contém o endereço IP de Olá para o ouvinte de grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="afe55-352">Esta seção resume como toocreate Olá balanceador de carga no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="afe55-353">No hello portal do Azure, vá toohello grupo de recursos onde os SQL Servers estão e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="afe55-354">Pesquise pelo **Balanceador de Carga**.</span><span class="sxs-lookup"><span data-stu-id="afe55-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="afe55-355">Escolha o balanceador de carga Olá publicado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afe55-355">Choose hello load balancer published by Microsoft.</span></span>

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="afe55-357">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-357">Click **Create**.</span></span>
3. <span data-ttu-id="afe55-358">Configure Olá parâmetros Olá balanceador de carga a seguir.</span><span class="sxs-lookup"><span data-stu-id="afe55-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="afe55-359">Configuração</span><span class="sxs-lookup"><span data-stu-id="afe55-359">Setting</span></span> | <span data-ttu-id="afe55-360">Campo</span><span class="sxs-lookup"><span data-stu-id="afe55-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="afe55-361">**Nome**</span><span class="sxs-lookup"><span data-stu-id="afe55-361">**Name**</span></span> |<span data-ttu-id="afe55-362">Use um nome para o balanceador de carga hello, por exemplo **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="afe55-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="afe55-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="afe55-363">**Type**</span></span> |<span data-ttu-id="afe55-364">Interna</span><span class="sxs-lookup"><span data-stu-id="afe55-364">Internal</span></span> |
   | <span data-ttu-id="afe55-365">**Rede virtual**</span><span class="sxs-lookup"><span data-stu-id="afe55-365">**Virtual network**</span></span> |<span data-ttu-id="afe55-366">Use nome de saudação do hello rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="afe55-367">**Sub-rede**</span><span class="sxs-lookup"><span data-stu-id="afe55-367">**Subnet**</span></span> |<span data-ttu-id="afe55-368">Use o nome de saudação da sub-rede Olá Olá a máquina virtual está em.</span><span class="sxs-lookup"><span data-stu-id="afe55-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="afe55-369">**Atribuição de endereço IP**</span><span class="sxs-lookup"><span data-stu-id="afe55-369">**IP address assignment**</span></span> |<span data-ttu-id="afe55-370">Estático</span><span class="sxs-lookup"><span data-stu-id="afe55-370">Static</span></span> |
   | <span data-ttu-id="afe55-371">**Endereço IP**</span><span class="sxs-lookup"><span data-stu-id="afe55-371">**IP address**</span></span> |<span data-ttu-id="afe55-372">Use um endereço disponível da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="afe55-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="afe55-373">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="afe55-373">**Subscription**</span></span> |<span data-ttu-id="afe55-374">Use Olá a mesma assinatura que a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="afe55-375">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="afe55-375">**Location**</span></span> |<span data-ttu-id="afe55-376">Use Olá mesmo local que a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="afe55-377">Olá folha portal do Azure deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="afe55-377">hello Azure portal blade should look like this:</span></span>

   ![Criar balanceador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="afe55-379">Clique em **criar**, balanceador de carga toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="afe55-380">Balanceador de carga de saudação tooconfigure, é necessário toocreate um pool de back-end, uma investigação e regras de balanceamento de carga de Olá conjunto.</span><span class="sxs-lookup"><span data-stu-id="afe55-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="afe55-381">Siga estes procedimentos na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="afe55-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="afe55-382">Adicionar pool de back-end</span><span class="sxs-lookup"><span data-stu-id="afe55-382">Add backend pool</span></span>

1. <span data-ttu-id="afe55-383">No hello portal do Azure, vá tooyour o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="afe55-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="afe55-384">Talvez seja necessário balanceador de carga toorefresh Olá exibição toosee Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="afe55-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Encontrar o Balanceador de Carga no Grupo de Recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="afe55-386">Clique em balanceador de carga Olá, **pools de back-end**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="afe55-387">Configure o pool de back-end de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="afe55-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="afe55-388">Configuração</span><span class="sxs-lookup"><span data-stu-id="afe55-388">Setting</span></span> | <span data-ttu-id="afe55-389">Descrição</span><span class="sxs-lookup"><span data-stu-id="afe55-389">Description</span></span> | <span data-ttu-id="afe55-390">Exemplo</span><span class="sxs-lookup"><span data-stu-id="afe55-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="afe55-391">**Nome**</span><span class="sxs-lookup"><span data-stu-id="afe55-391">**Name**</span></span> | <span data-ttu-id="afe55-392">Digite um nome de texto</span><span class="sxs-lookup"><span data-stu-id="afe55-392">Type a text name</span></span> | <span data-ttu-id="afe55-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="afe55-393">SQLLBBE</span></span>
   | <span data-ttu-id="afe55-394">**Associado a**</span><span class="sxs-lookup"><span data-stu-id="afe55-394">**Associated to**</span></span> | <span data-ttu-id="afe55-395">Selecione uma opção na lista</span><span class="sxs-lookup"><span data-stu-id="afe55-395">Pick from list</span></span> | <span data-ttu-id="afe55-396">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="afe55-396">Availability set</span></span>
   | <span data-ttu-id="afe55-397">**Conjunto de disponibilidade**</span><span class="sxs-lookup"><span data-stu-id="afe55-397">**Availability set**</span></span> | <span data-ttu-id="afe55-398">Use um nome de conjunto de disponibilidade de saudação que suas VMs do SQL Server estão em</span><span class="sxs-lookup"><span data-stu-id="afe55-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="afe55-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="afe55-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="afe55-400">**Máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="afe55-400">**Virtual machines**</span></span> |<span data-ttu-id="afe55-401">Olá dois nomes de VM do Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="afe55-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="afe55-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="afe55-403">Digite o nome de saudação para pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="afe55-404">Clique em **+ Adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="afe55-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="afe55-405">Para conjunto de disponibilidade hello, escolha conjunto de disponibilidade de saudação que Olá SQL Servers estão no.</span><span class="sxs-lookup"><span data-stu-id="afe55-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="afe55-406">Para máquinas virtuais, incluem ambos Olá SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="afe55-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="afe55-407">Não inclua o servidor de testemunha de compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="afe55-408">Clique em **Okey** toocreate pool de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="afe55-409">Investigação de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="afe55-409">Set hello probe</span></span>

1. <span data-ttu-id="afe55-410">Clique em balanceador de carga Olá, **sondas de integridade**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="afe55-411">Defina investigação de integridade de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="afe55-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="afe55-412">Configuração</span><span class="sxs-lookup"><span data-stu-id="afe55-412">Setting</span></span> | <span data-ttu-id="afe55-413">Descrição</span><span class="sxs-lookup"><span data-stu-id="afe55-413">Description</span></span> | <span data-ttu-id="afe55-414">Exemplo</span><span class="sxs-lookup"><span data-stu-id="afe55-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="afe55-415">**Nome**</span><span class="sxs-lookup"><span data-stu-id="afe55-415">**Name**</span></span> | <span data-ttu-id="afe55-416">Texto</span><span class="sxs-lookup"><span data-stu-id="afe55-416">Text</span></span> | <span data-ttu-id="afe55-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="afe55-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="afe55-418">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="afe55-418">**Protocol**</span></span> | <span data-ttu-id="afe55-419">Escolher TCP</span><span class="sxs-lookup"><span data-stu-id="afe55-419">Choose TCP</span></span> | <span data-ttu-id="afe55-420">TCP</span><span class="sxs-lookup"><span data-stu-id="afe55-420">TCP</span></span> |
   | <span data-ttu-id="afe55-421">**Porta**</span><span class="sxs-lookup"><span data-stu-id="afe55-421">**Port**</span></span> | <span data-ttu-id="afe55-422">Qualquer porta não utilizada</span><span class="sxs-lookup"><span data-stu-id="afe55-422">Any unused port</span></span> | <span data-ttu-id="afe55-423">59999</span><span class="sxs-lookup"><span data-stu-id="afe55-423">59999</span></span> |
   | <span data-ttu-id="afe55-424">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="afe55-424">**Interval**</span></span>  | <span data-ttu-id="afe55-425">quantidade de saudação de tempo entre a investigação tentativas em segundos</span><span class="sxs-lookup"><span data-stu-id="afe55-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="afe55-426">5</span><span class="sxs-lookup"><span data-stu-id="afe55-426">5</span></span> |
   | <span data-ttu-id="afe55-427">**Limite não íntegro**</span><span class="sxs-lookup"><span data-stu-id="afe55-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="afe55-428">Olá número de falhas de investigação consecutivas que deve ocorrer para um toobe de máquina virtual considerado não íntegro</span><span class="sxs-lookup"><span data-stu-id="afe55-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="afe55-429">2</span><span class="sxs-lookup"><span data-stu-id="afe55-429">2</span></span> |

1. <span data-ttu-id="afe55-430">Clique em **Okey** tooset investigação de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="afe55-431">Definir regras de balanceamento de carga de Olá</span><span class="sxs-lookup"><span data-stu-id="afe55-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="afe55-432">Clique em balanceador de carga Olá, **regras de balanceamento de carga**e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="afe55-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="afe55-433">Defina a saudação de balanceamento de carga regras da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="afe55-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="afe55-434">Configuração</span><span class="sxs-lookup"><span data-stu-id="afe55-434">Setting</span></span> | <span data-ttu-id="afe55-435">Descrição</span><span class="sxs-lookup"><span data-stu-id="afe55-435">Description</span></span> | <span data-ttu-id="afe55-436">Exemplo</span><span class="sxs-lookup"><span data-stu-id="afe55-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="afe55-437">**Nome**</span><span class="sxs-lookup"><span data-stu-id="afe55-437">**Name**</span></span> | <span data-ttu-id="afe55-438">Texto</span><span class="sxs-lookup"><span data-stu-id="afe55-438">Text</span></span> | <span data-ttu-id="afe55-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="afe55-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="afe55-440">**Endereço IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="afe55-440">**Frontend IP address**</span></span> | <span data-ttu-id="afe55-441">Escolher um endereço</span><span class="sxs-lookup"><span data-stu-id="afe55-441">Choose an address</span></span> |<span data-ttu-id="afe55-442">Use endereço Olá criada quando criou o balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="afe55-443">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="afe55-443">**Protocol**</span></span> | <span data-ttu-id="afe55-444">Escolher TCP</span><span class="sxs-lookup"><span data-stu-id="afe55-444">Choose TCP</span></span> |<span data-ttu-id="afe55-445">TCP</span><span class="sxs-lookup"><span data-stu-id="afe55-445">TCP</span></span> |
   | <span data-ttu-id="afe55-446">**Porta**</span><span class="sxs-lookup"><span data-stu-id="afe55-446">**Port**</span></span> | <span data-ttu-id="afe55-447">Usar porta Olá Olá instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="afe55-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="afe55-448">1433</span><span class="sxs-lookup"><span data-stu-id="afe55-448">1433</span></span> |
   | <span data-ttu-id="afe55-449">**Porta de back-end**</span><span class="sxs-lookup"><span data-stu-id="afe55-449">**Backend Port**</span></span> | <span data-ttu-id="afe55-450">Este campo não é usado quando o IP flutuante é definido para o retorno de servidor direto</span><span class="sxs-lookup"><span data-stu-id="afe55-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="afe55-451">1433</span><span class="sxs-lookup"><span data-stu-id="afe55-451">1433</span></span> |
   | <span data-ttu-id="afe55-452">**Investigação**</span><span class="sxs-lookup"><span data-stu-id="afe55-452">**Probe**</span></span> |<span data-ttu-id="afe55-453">nome de saudação especificado para investigação Olá</span><span class="sxs-lookup"><span data-stu-id="afe55-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="afe55-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="afe55-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="afe55-455">**Persistência de sessão**</span><span class="sxs-lookup"><span data-stu-id="afe55-455">**Session Persistence**</span></span> | <span data-ttu-id="afe55-456">Lista suspensa</span><span class="sxs-lookup"><span data-stu-id="afe55-456">Drop down list</span></span> | <span data-ttu-id="afe55-457">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="afe55-457">**None**</span></span> |
   | <span data-ttu-id="afe55-458">**Tempo limite de ociosidade**</span><span class="sxs-lookup"><span data-stu-id="afe55-458">**Idle Timeout**</span></span> | <span data-ttu-id="afe55-459">Minutos tookeep abrir uma conexão TCP</span><span class="sxs-lookup"><span data-stu-id="afe55-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="afe55-460">4</span><span class="sxs-lookup"><span data-stu-id="afe55-460">4</span></span> |
   | <span data-ttu-id="afe55-461">**IP flutuante (retorno de servidor direto)**</span><span class="sxs-lookup"><span data-stu-id="afe55-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="afe55-462">Habilitado</span><span class="sxs-lookup"><span data-stu-id="afe55-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="afe55-463">O retorno de servidor direto é definido durante a criação.</span><span class="sxs-lookup"><span data-stu-id="afe55-463">Direct server return is set during creation.</span></span> <span data-ttu-id="afe55-464">Ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="afe55-464">It cannot be changed.</span></span>

1. <span data-ttu-id="afe55-465">Clique em **Okey** regras de balanceamento de carga de saudação de tooset.</span><span class="sxs-lookup"><span data-stu-id="afe55-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="afe55-466"><a name="configure-listener"></a>Configurar ouvinte Olá</span><span class="sxs-lookup"><span data-stu-id="afe55-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="afe55-467">Olá próxima coisa toodo é tooconfigure um ouvinte de grupo de disponibilidade no cluster de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="afe55-468">Este tutorial mostra como tratar toocreate um ouvinte único - com um IP do ILB.</span><span class="sxs-lookup"><span data-stu-id="afe55-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="afe55-469">toocreate um ou mais ouvintes usando um ou mais endereços IP, consulte [balanceador de carga e de ouvinte criar grupo de disponibilidade | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe55-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="afe55-470">Definir porta do ouvinte</span><span class="sxs-lookup"><span data-stu-id="afe55-470">Set listener port</span></span>

<span data-ttu-id="afe55-471">No SQL Server Management Studio, defina a porta do ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="afe55-472">Inicie o SQL Server Management Studio e conecte-se a réplica primária toohello.</span><span class="sxs-lookup"><span data-stu-id="afe55-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="afe55-473">Navegue muito**alta disponibilidade AlwaysOn** | **grupos de disponibilidade** | **ouvintes do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="afe55-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="afe55-474">Agora você deve ver o nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="afe55-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="afe55-475">Nome do ouvinte de saudação de mouse e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="afe55-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="afe55-476">Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade de saudação usando Olá $EndpointPort utilizado antes (1433 foi padrão Olá), em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="afe55-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="afe55-477">Agora você tem um Grupo de Disponibilidade do SQL Server em máquinas virtuais do Azure, em execução no modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afe55-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="afe55-478">Toolistener de conexão de teste</span><span class="sxs-lookup"><span data-stu-id="afe55-478">Test connection toolistener</span></span>

<span data-ttu-id="afe55-479">conexão de saudação tootest:</span><span class="sxs-lookup"><span data-stu-id="afe55-479">tootest hello connection:</span></span>

1. <span data-ttu-id="afe55-480">RDP tooa SQL Server que está em Olá mesmo virtual de rede, mas não não réplica Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="afe55-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="afe55-481">Você pode usar Olá outros SQL Server em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="afe55-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="afe55-482">Use **sqlcmd** conexão de saudação do utilitário tootest.</span><span class="sxs-lookup"><span data-stu-id="afe55-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="afe55-483">Por exemplo, a saudação script a seguir estabelece uma **sqlcmd** réplica primária de toohello de conexão por meio do ouvinte Olá com autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="afe55-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="afe55-484">Se o ouvinte Olá estiver usando uma porta diferente de Olá padrão (1433) de porta, especifique a porta Olá na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="afe55-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="afe55-485">Por exemplo, hello seguinte comando sqlcmd conecta tooa escuta na porta 1435:</span><span class="sxs-lookup"><span data-stu-id="afe55-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="afe55-486">Olá conexão SQLCMD conecta-se automaticamente toowhichever instância do SQL Server hospeda Olá a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="afe55-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="afe55-487">Certifique-se de que a porta de Olá especificado é aberta no firewall Olá de ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="afe55-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="afe55-488">Ambos os servidores exigem uma regra de entrada para Olá a porta TCP que você usa.</span><span class="sxs-lookup"><span data-stu-id="afe55-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="afe55-489">Para saber mais, confira [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="afe55-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="afe55-490">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="afe55-490">Next steps</span></span>

- <span data-ttu-id="afe55-491">[Adicionar um balanceador de carga tooa de endereço IP para um segundo grupo de disponibilidade](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="afe55-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
