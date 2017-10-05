---
title: "Grupos de Disponibilidade do SQL Server - máquinas virtuais do Azure - tutorial | Microsoft Docs"
description: "Este tutorial mostra como criar um grupo de disponibilidade Always On do SQL Server em Máquinas Virtuais do Azure."
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
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="d4c53-103">Configurar grupos de disponibilidade Sempre ativo na VM do Azure manualmente</span><span class="sxs-lookup"><span data-stu-id="d4c53-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="d4c53-104">Este tutorial mostra como criar um grupo de disponibilidade Always On do SQL Server em Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="d4c53-105">O tutorial completo cria um Grupo de Disponibilidade com uma réplica do banco de dados em dois SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="d4c53-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="d4c53-106">**Tempo estimado**: cerca de 30 minutos para ser concluído depois que os pré-requisitos forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="d4c53-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="d4c53-107">O diagrama ilustra o que você cria no tutorial.</span><span class="sxs-lookup"><span data-stu-id="d4c53-107">The diagram illustrates what you build in the tutorial.</span></span>

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="d4c53-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4c53-109">Prerequisites</span></span>

<span data-ttu-id="d4c53-110">O tutorial supõe que você tem uma compreensão básica dos Grupos de Disponibilidade Always On do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="d4c53-111">Se você precisa saber mais, confira [Visão geral dos Grupos de Disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c53-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="d4c53-112">A tabela a seguir lista os pré-requisitos que precisam ser concluídos antes de iniciar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="d4c53-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="d4c53-113">Requisito</span><span class="sxs-lookup"><span data-stu-id="d4c53-113">Requirement</span></span> |<span data-ttu-id="d4c53-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c53-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="d4c53-116">Dois servidores SQL</span><span class="sxs-lookup"><span data-stu-id="d4c53-116">Two SQL Servers</span></span> | <span data-ttu-id="d4c53-117">-Em um conjunto de disponibilidade do Azure</span><span class="sxs-lookup"><span data-stu-id="d4c53-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="d4c53-118">-Em um único domínio</span><span class="sxs-lookup"><span data-stu-id="d4c53-118">- In a single domain</span></span> <br/> <span data-ttu-id="d4c53-119">-Com o recurso Cluster de Failover instalado</span><span class="sxs-lookup"><span data-stu-id="d4c53-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="d4c53-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-121">Windows Server</span></span> | <span data-ttu-id="d4c53-122">Compartilhamento de arquivos para a testemunha do cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="d4c53-124">Conta de serviço do SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-124">SQL Server service account</span></span> | <span data-ttu-id="d4c53-125">Conta do domínio</span><span class="sxs-lookup"><span data-stu-id="d4c53-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="d4c53-127">Conta do serviço SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="d4c53-127">SQL Server Agent service account</span></span> | <span data-ttu-id="d4c53-128">Conta do domínio</span><span class="sxs-lookup"><span data-stu-id="d4c53-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="d4c53-130">Portas de firewall abertas</span><span class="sxs-lookup"><span data-stu-id="d4c53-130">Firewall ports open</span></span> | <span data-ttu-id="d4c53-131">- SQL Server: **1433** para instância padrão</span><span class="sxs-lookup"><span data-stu-id="d4c53-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="d4c53-132">- Ponto de extremidade de espelhamento de banco de dados: **5022** ou outra porta disponível</span><span class="sxs-lookup"><span data-stu-id="d4c53-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="d4c53-133">- Investigação do Azure Load Balancer: **59999** ou outra porta disponível</span><span class="sxs-lookup"><span data-stu-id="d4c53-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="d4c53-135">Adicionar o recurso Cluster de Failover à VM</span><span class="sxs-lookup"><span data-stu-id="d4c53-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="d4c53-136">Os dois SQL Servers precisam desse recurso</span><span class="sxs-lookup"><span data-stu-id="d4c53-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="d4c53-138">Conta do domínio de instalação</span><span class="sxs-lookup"><span data-stu-id="d4c53-138">Installation domain account</span></span> | <span data-ttu-id="d4c53-139">- Administrador local em cada SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="d4c53-140">- Membro da função de servidor fixa sysadmin do SQL Server para cada instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="d4c53-141">Antes de iniciar o tutorial, você precisará [Concluir os pré-requisitos para a criação de Grupos de Disponibilidade AlwaysOn em Máquinas Virtuais do Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="d4c53-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="d4c53-142">Se esses pré-requisitos já foram concluídos,vá para [Criar Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="d4c53-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="d4c53-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Criar o cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="d4c53-144">Depois de concluir os pré-requisitos, a primeira etapa é criar um cluster de failover do Windows Server que inclui dois SQL Servers e um servidor testemunha.</span><span class="sxs-lookup"><span data-stu-id="d4c53-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="d4c53-145">Faça RDP para o primeiro SQL Server usando uma conta de domínio que seja de administrador no SQL Server e no servidor testemunha.</span><span class="sxs-lookup"><span data-stu-id="d4c53-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="d4c53-146">Se você seguiu o [documento de pré-requisitos](virtual-machines-windows-portal-sql-availability-group-prereq.md), criou uma conta chamada **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="d4c53-147">Use essa conta.</span><span class="sxs-lookup"><span data-stu-id="d4c53-147">Use this account.</span></span>

2. <span data-ttu-id="d4c53-148">No painel **Gerenciador do Servidor** selecione **Ferramentas**, e clique em **Gerenciador de Cluster de Failover**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="d4c53-149">No painel esquerdo, clique com botão direito do mouse em **Gerenciador de Cluster de Failover** e clique em **Criar um Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="d4c53-150">![Criar cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="d4c53-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="d4c53-151">No Assistente para Criação de Cluster, crie um cluster de um nó percorrendo as páginas com as configurações na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="d4c53-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="d4c53-152">Página</span><span class="sxs-lookup"><span data-stu-id="d4c53-152">Page</span></span> | <span data-ttu-id="d4c53-153">Configurações</span><span class="sxs-lookup"><span data-stu-id="d4c53-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="d4c53-154">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d4c53-154">Before You Begin</span></span> |<span data-ttu-id="d4c53-155">Usar padrões</span><span class="sxs-lookup"><span data-stu-id="d4c53-155">Use defaults</span></span> |
   | <span data-ttu-id="d4c53-156">Selecionar Servidores</span><span class="sxs-lookup"><span data-stu-id="d4c53-156">Select Servers</span></span> |<span data-ttu-id="d4c53-157">Digite o primeiro nome do SQL Server em **Digite o nome do servidor** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="d4c53-158">Aviso de Validação</span><span class="sxs-lookup"><span data-stu-id="d4c53-158">Validation Warning</span></span> |<span data-ttu-id="d4c53-159">Selecione **Não. Eu não preciso de suporte da Microsoft para este cluster e, portanto, não desejo executar testes de validação. Continuar a criar o cluster quando eu clicar em Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="d4c53-160">Ponto de Acesso para Administrar o Cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="d4c53-161">Digite um nome de cluster, por exemplo, **SQLAGCluster1** em **Nome do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="d4c53-162">Confirmação</span><span class="sxs-lookup"><span data-stu-id="d4c53-162">Confirmation</span></span> |<span data-ttu-id="d4c53-163">Use os padrões, a menos que você esteja usando Espaços de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d4c53-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="d4c53-164">Consulte a observação após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="d4c53-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="d4c53-165">Definir o endereço IP do cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="d4c53-166">Em **Gerenciador de Cluster de Failover**, role para baixo até **Recursos Principais de Cluster** e expanda os detalhes do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="d4c53-167">Você verá os recursos de **Nome** e de **Endereço IP** no estado **Com Falha**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="d4c53-168">O recurso de endereço IP não pode ficar online porque o cluster recebeu o mesmo endereço IP que a própria máquina, ou seja, um endereço duplicado.</span><span class="sxs-lookup"><span data-stu-id="d4c53-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="d4c53-169">Clique com o botão direito do mouse no recurso **Endereço IP** com falha e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Propriedades do Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="d4c53-171">Selecione **Endereço IP estático** e especifique um endereço disponível da sub-rede onde o SQL Server está na caixa de texto Endereço.</span><span class="sxs-lookup"><span data-stu-id="d4c53-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="d4c53-172">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="d4c53-173">Na seção **Recursos Principais do Cluster**, clique com o botão direito do mouse no nome do cluster e clique em **Colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="d4c53-174">Em seguida, aguarde até que ambos os recursos estejam online.</span><span class="sxs-lookup"><span data-stu-id="d4c53-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="d4c53-175">Quando o recurso de nome de cluster fica online, ele atualiza o servidor DC com uma nova conta de computador do AD.</span><span class="sxs-lookup"><span data-stu-id="d4c53-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="d4c53-176">Use essa conta do AD para executar o serviço clusterizado do Grupo de Disponibilidade posteriormente.</span><span class="sxs-lookup"><span data-stu-id="d4c53-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="d4c53-177"><a name="addNode"></a>Adicionar o outro SQL Server ao cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="d4c53-178">Adicione o outro SQL Server ao cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="d4c53-179">Na árvore do navegador, clique com o botão direito do mouse no cluster e clique em **Adicionar Nó**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Adicionar Nó ao Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="d4c53-181">No **Assistente para Adicionar Nó**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="d4c53-182">Na página **Selecionar Servidores**, adicione o segundo SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="d4c53-183">Digite o nome do servidor em **Digite o nome do servidor** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="d4c53-184">Quando terminar, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="d4c53-185">Na página **Aviso de Validação**, clique em **Não** (em um cenário de produção, você deve executar os testes de validação).</span><span class="sxs-lookup"><span data-stu-id="d4c53-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="d4c53-186">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="d4c53-187">Na página **Confirmação**, se você estiver usando Espaços de Armazenamento, desmarque a caixa de seleção **Adicione todo o armazenamento qualificado ao cluster.**</span><span class="sxs-lookup"><span data-stu-id="d4c53-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Adicionar Confirmação do Nó](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="d4c53-189">Se você estiver usando Espaços de Armazenamento e não desmarcar **Adicionar todo o armazenamento qualificado ao cluster**, o Windows desconectará os discos virtuais durante o processo de clustering.</span><span class="sxs-lookup"><span data-stu-id="d4c53-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="d4c53-190">Como resultado, eles não aparecem no Gerenciador ou Explorador de Discos até que os espaços de armazenamento sejam removidos do cluster e reanexados usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4c53-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="d4c53-191">Espaços de Armazenamento agrupam vários discos em pools de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d4c53-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="d4c53-192">Para obter mais informações, consulte [Espaços de Armazenamento](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="d4c53-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="d4c53-193">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-193">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-194">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-194">Click **Finish**.</span></span>

   <span data-ttu-id="d4c53-195">O Gerenciador de Cluster de Failover mostra que o cluster tem um novo nó e o lista no contêiner **Nós**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="d4c53-196">Faça logoff da sessão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="d4c53-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="d4c53-197">Adicionar um compartilhamento de arquivos de quorum de cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="d4c53-198">Neste exemplo, o cluster do Windows usa um compartilhamento de arquivos para criar um quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="d4c53-199">Este tutorial usa um quorum Maioria de Compartilhamento de Arquivos e Nós.</span><span class="sxs-lookup"><span data-stu-id="d4c53-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="d4c53-200">Para saber mais, confira [Noções básicas sobre configurações de quorum em um cluster de failover](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c53-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="d4c53-201">Conecte-se ao servidor membro de testemunha de compartilhamento de arquivos com uma sessão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="d4c53-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="d4c53-202">No **Gerenciador do Servidor**, clique em **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="d4c53-203">Abra **Gerenciamento do Computador**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="d4c53-204">Clique em **Pastas Compartilhadas**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="d4c53-205">Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .</span><span class="sxs-lookup"><span data-stu-id="d4c53-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="d4c53-207">Use **Criar um Assistente de Pasta Compartilhada** para criar um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="d4c53-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="d4c53-208">Em **Caminho da Pasta**, clique em **Procurar** e localize ou crie um caminho para a pasta compartilhada.</span><span class="sxs-lookup"><span data-stu-id="d4c53-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="d4c53-209">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-209">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-210">Em **Nome, Descrição e Configurações**, verifique o nome de compartilhamento e o caminho.</span><span class="sxs-lookup"><span data-stu-id="d4c53-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="d4c53-211">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-211">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-212">Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="d4c53-213">Clique em **Personalizar...**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="d4c53-214">Em **Personalizar Permissões**, clique em **Adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="d4c53-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="d4c53-215">Verifique se a conta usada para criar o cluster tem controle total.</span><span class="sxs-lookup"><span data-stu-id="d4c53-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="d4c53-217">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-217">Click **OK**.</span></span>

1. <span data-ttu-id="d4c53-218">Em **Permissões de Pasta Compartilhada**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="d4c53-219">Clique em **Concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="d4c53-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="d4c53-220">Logoff do servidor</span><span class="sxs-lookup"><span data-stu-id="d4c53-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="d4c53-221">Configurar quorum do cluster</span><span class="sxs-lookup"><span data-stu-id="d4c53-221">Configure cluster quorum</span></span>

<span data-ttu-id="d4c53-222">Em seguida, configure o quorum do cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="d4c53-223">Conecte-se ao primeiro nó de cluster com a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="d4c53-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="d4c53-224">Em **Gerenciador de Cluster de Failover**, clique com o botão direito do mouse no cluster, aponte para **Mais Ações**e clique em **Configurar Quorum do Cluster...** .</span><span class="sxs-lookup"><span data-stu-id="d4c53-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="d4c53-226">No **Assistente para Configurar Quorum do Cluster**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="d4c53-227">Em **Selecionar Opção de Configuração de Quorum**, escolha **Selecionar a testemunha de quorum**e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="d4c53-228">Em **Selecionar Testemunha de Quorum**, clique em **Configurar testemunha de compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="d4c53-229">O Windows Server 2016 dá suporte a testemunha de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d4c53-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="d4c53-230">Se você escolher esse tipo de testemunha, não precisará de testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4c53-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="d4c53-231">Para saber mais, confira [Implantar uma testemunha de nuvem para um Cluster de Failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="d4c53-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="d4c53-232">Este tutorial usa uma testemunha de compartilhamento de arquivos, o que tem suporte de sistemas operacionais anteriores.</span><span class="sxs-lookup"><span data-stu-id="d4c53-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="d4c53-233">Em **Configurar Testemunha de Compartilhamento de Arquivos**, insira o caminho para o compartilhamento criado.</span><span class="sxs-lookup"><span data-stu-id="d4c53-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="d4c53-234">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-234">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-235">Verifique as configurações em **Confirmação**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="d4c53-236">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-236">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-237">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-237">Click **Finish**.</span></span>

<span data-ttu-id="d4c53-238">Os recursos principais de cluster são configurados com uma testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4c53-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="d4c53-239">Habilitar Grupos de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d4c53-239">Enable Availability Groups</span></span>

<span data-ttu-id="d4c53-240">Em seguida, habilite o recurso **Grupos de Disponibilidade AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="d4c53-241">Siga estas etapas em ambos os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="d4c53-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="d4c53-242">Na tela **Iniciar**, inicie o **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="d4c53-243">Na árvore do navegador, clique em **Serviços do SQL Server**, clique com o botão direito do mouse no serviço **SQL Server (MSSQLSERVER)** e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="d4c53-244">Clique na guia **Alta Disponibilidade AlwaysOn** e selecione **Habilitar Grupos de Disponibilidade AlwaysOn**, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d4c53-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Habilitar Grupos de Disponibilidade AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="d4c53-246">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-246">Click **Apply**.</span></span> <span data-ttu-id="d4c53-247">Clique em **OK** no diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="d4c53-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="d4c53-248">Reinicie o serviço SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="d4c53-249">Repita essas etapas no outro SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="d4c53-250">Criar um banco de dados no primeiro SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="d4c53-251">Inicie o arquivo RDP para o primeiro SQL Server com uma conta de domínio que seja membro da função de servidor fixa sysadmin.</span><span class="sxs-lookup"><span data-stu-id="d4c53-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="d4c53-252">Abra o SQL Server Management Studio e conecte-se ao primeiro SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="d4c53-253">No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Bancos de Dados** e em **Novo Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="d4c53-254">Em **Nome do banco de dados**, digite **MyDB1** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="d4c53-255"><a name="backupshare"></a>Criar um compartilhamento de backup</span><span class="sxs-lookup"><span data-stu-id="d4c53-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="d4c53-256">No primeiro SQL Server em **Gerenciador do Servidor**, clique em **Ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="d4c53-257">Abra **Gerenciamento do Computador**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="d4c53-258">Clique em **Pastas Compartilhadas**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="d4c53-259">Clique com botão direito do mouse em **Compartilhamentos** e clique em **Novo Compartilhamento...** .</span><span class="sxs-lookup"><span data-stu-id="d4c53-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="d4c53-261">Use **Criar um Assistente de Pasta Compartilhada** para criar um compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="d4c53-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="d4c53-262">Em **Caminho da Pasta**, clique em **Procurar** e localize ou crie um caminho para a pasta compartilhada de backup do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d4c53-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="d4c53-263">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-263">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-264">Em **Nome, Descrição e Configurações**, verifique o nome de compartilhamento e o caminho.</span><span class="sxs-lookup"><span data-stu-id="d4c53-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="d4c53-265">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-265">Click **Next**.</span></span>

1. <span data-ttu-id="d4c53-266">Em **Permissões de Pasta Compartilhada**, defina **Personalizar permissões**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="d4c53-267">Clique em **Personalizar...**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="d4c53-268">Em **Personalizar Permissões**, clique em **Adicionar...** .</span><span class="sxs-lookup"><span data-stu-id="d4c53-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="d4c53-269">Verifique se as contas de serviço do SQL Server e do SQL Server Agent para ambos os servidores têm controle total.</span><span class="sxs-lookup"><span data-stu-id="d4c53-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Novo compartilhamento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="d4c53-271">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-271">Click **OK**.</span></span>

1. <span data-ttu-id="d4c53-272">Em **Permissões de Pasta Compartilhada**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="d4c53-273">Clique em **Concluir** novamente.</span><span class="sxs-lookup"><span data-stu-id="d4c53-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="d4c53-274">Fazer um backup completo do banco de dados</span><span class="sxs-lookup"><span data-stu-id="d4c53-274">Take a full backup of the database</span></span>

<span data-ttu-id="d4c53-275">Você precisa fazer backup do novo banco de dados para inicializar a cadeia de logs.</span><span class="sxs-lookup"><span data-stu-id="d4c53-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="d4c53-276">Se você não fizer um backup do novo banco de dados, ele não poderá ser incluído em um Grupo de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="d4c53-277">Em **Pesquisador de Objetos**, clique com o botão direito do mouse no banco de dados, aponte para **Tarefas...**  e clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="d4c53-278">Clique em **OK** para realizar um backup completo no local de backup padrão.</span><span class="sxs-lookup"><span data-stu-id="d4c53-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="d4c53-279">Criar o Grupo de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d4c53-279">Create the Availability Group</span></span>
<span data-ttu-id="d4c53-280">Agora você está pronto para configurar um Grupo de Disponibilidade usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d4c53-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="d4c53-281">Crie um banco de dados no SQL Server primeiro.</span><span class="sxs-lookup"><span data-stu-id="d4c53-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="d4c53-282">Faça um backup completo e um backup de log de transações do banco de dados</span><span class="sxs-lookup"><span data-stu-id="d4c53-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="d4c53-283">Restaure os backups completo e de log no segundo SQL Server com a opção **NORECOVERY**</span><span class="sxs-lookup"><span data-stu-id="d4c53-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="d4c53-284">Crie o Grupo de Disponibilidade (**AG1**) com confirmação síncrona, failover automático e réplicas secundárias legíveis</span><span class="sxs-lookup"><span data-stu-id="d4c53-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="d4c53-285">Crie o Grupo de Disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="d4c53-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="d4c53-286">Na sessão da área de trabalho remota para o primeiro SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="d4c53-287">Em **Pesquisador de Objetos** no SSMS, clique com o botão direito do mouse em **Alta Disponibilidade AlwaysOn** e clique em **Assistente de Novo Grupo de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Inicie o Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="d4c53-289">Na página **Introdução**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="d4c53-290">Na página **Especificar Nome do Grupo de Disponibilidade**, digite um nome para o Grupo de Disponibilidade, por exemplo, **AG1**, em **Nome do Grupo de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="d4c53-291">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-291">Click **Next**.</span></span>

    ![Novo assistente de AG, especifique o nome do AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="d4c53-293">Na página **Selecionar Bancos de Dados**, selecione seu banco de dados e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d4c53-294">Esse banco de dados atende aos pré-requisitos para um Grupo de Disponibilidade, pois você fez pelo menos um backup completo na réplica primária pretendida.</span><span class="sxs-lookup"><span data-stu-id="d4c53-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![Novo assistente AG, selecione os bancos de dados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="d4c53-296">Na página **Especificar Réplicas**, clique em **Adicionar Réplica**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Novo assistente AG, especifique as réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="d4c53-298">A caixa de diálogo **Conectar ao Servidor** é aberta.</span><span class="sxs-lookup"><span data-stu-id="d4c53-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="d4c53-299">Digite o nome do segundo servidor em **Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="d4c53-300">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-300">Click **Connect**.</span></span>

   <span data-ttu-id="d4c53-301">De volta à página **Especificar Réplicas**, você verá o segundo servidor listado em **Réplicas de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="d4c53-302">Configure as réplicas como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4c53-302">Configure the replicas as follows.</span></span>

   ![Novo assistente de AG, Especificar Réplicas (Completo)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="d4c53-304">Clique em **Pontos de extremidade** para ver o ponto de extremidade de espelhamento de banco de dados para esse Grupo de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="d4c53-305">Use a mesma porta que você usou ao definir a [regra de firewall para pontos de extremidade de espelhamento de banco de dados](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="d4c53-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="d4c53-307">Na página **Selecionar Sincronização de Dados Inicial** , selecione **Completo** e especifique um local de rede compartilhada.</span><span class="sxs-lookup"><span data-stu-id="d4c53-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="d4c53-308">Para o local, use o [compartilhamento de backup criado](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="d4c53-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="d4c53-309">No exemplo, era **\\\\\<First SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="d4c53-310">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d4c53-311">A sincronização completa usa um backup completo do banco de dados na primeira instância do SQL Server e o restaura na segunda instância.</span><span class="sxs-lookup"><span data-stu-id="d4c53-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="d4c53-312">Em caso de grandes bancos de dados, a sincronização completa não é recomendada porque pode levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="d4c53-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="d4c53-313">Você pode reduzir esse tempo manualmente usando um backup do banco de dados e restaurando-o com `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="d4c53-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="d4c53-314">Se o banco de dados já foi restaurado com `NO RECOVERY` no segundo SQL Server antes da configuração do Grupo de Disponibilidade, escolha **Somente junção**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="d4c53-315">Se você quiser usar o backup depois de configurar o Grupo de Disponibilidade, escolha **Ignorar sincronização inicial de dados**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Novo assistente de AG, selecionar sincronização de dados inicial](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="d4c53-317">Na página **Validação**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="d4c53-318">O arquivo deve ser semelhante à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="d4c53-318">This page should look similar to the following image:</span></span>

    ![Novo assistente AG, Validação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="d4c53-320">Há um aviso para a configuração de ouvinte porque você não configurou um ouvinte de Grupo de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="d4c53-321">Você pode ignorar esse aviso porque, nas máquinas virtuais do Azure, o ouvinte é criado depois do balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="d4c53-322">Na página **Resumo**, clique em **Concluir** e aguarde enquanto o assistente configura o novo Grupo de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="d4c53-323">Na página **Progresso**, você pode clicar em **Mais detalhes** para exibir o progresso detalhado.</span><span class="sxs-lookup"><span data-stu-id="d4c53-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="d4c53-324">Quando o assistente for concluído, inspecione a página **Resultados** para verificar se o Grupo de Disponibilidade foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d4c53-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![Novo assistente de AG, Resultados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="d4c53-326">Clique em **Fechar** para sair do assistente.</span><span class="sxs-lookup"><span data-stu-id="d4c53-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="d4c53-327">Conferir o Grupo de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d4c53-327">Check the Availability Group</span></span>

1. <span data-ttu-id="d4c53-328">Em **Pesquisador de Objetos**, expanda **Alta Disponibilidade AlwaysOn** e expanda **Grupos de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="d4c53-329">Agora você poderá ver o novo Grupo de Disponibilidade neste contêiner.</span><span class="sxs-lookup"><span data-stu-id="d4c53-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="d4c53-330">Clique com botão direito do mouse no Grupo de Disponibilidade e clique em **Mostrar Painel**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![Mostrar Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="d4c53-332">O **Painel AlwaysOn** deve ser semelhante ao mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d4c53-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![Painel de AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="d4c53-334">Você pode ver as réplicas, o modo de failover de cada réplica e o estado de sincronização.</span><span class="sxs-lookup"><span data-stu-id="d4c53-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="d4c53-335">No **Gerenciador de Cluster de Failover**, clique em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="d4c53-336">Selecione **funções**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-336">Select **Roles**.</span></span> <span data-ttu-id="d4c53-337">O nome do Grupo de Disponibilidade usado é uma função no cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="d4c53-338">Esse Grupo de Disponibilidade não tem um endereço IP para conexões de cliente porque você não configurou um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d4c53-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="d4c53-339">Você configurará o ouvinte depois de criar um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="d4c53-341">Não tente fazer failover do Grupo de Disponibilidade no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="d4c53-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="d4c53-342">Todas as operações de failover devem ser executadas no **Painel AlwaysOn** no SSMS.</span><span class="sxs-lookup"><span data-stu-id="d4c53-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="d4c53-343">Para obter mais informações, consulte [Restrições do uso do Gerenciador de Cluster de Failover com Grupos de Disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c53-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="d4c53-344">Agora você tem um Grupo de Disponibilidade com réplicas em duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4c53-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="d4c53-345">Você pode mover o Grupo de Disponibilidade entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="d4c53-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="d4c53-346">Você ainda não pode se conectar ao Grupo de Disponibilidade porque não tem um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d4c53-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="d4c53-347">Nas máquinas virtuais do Azure, o ouvinte precisa de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="d4c53-348">A próxima etapa é criar o balanceador de carga no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="d4c53-349">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="d4c53-349">Create an Azure load balancer</span></span>

<span data-ttu-id="d4c53-350">Nas máquinas virtuais do Azure, um Grupo de Disponibilidade do SQL Server precisa de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="d4c53-351">O balanceador de carga contém o endereço IP do ouvinte do Grupo de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="d4c53-352">Esta seção resume como criar o balanceador de carga no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="d4c53-353">No portal do Azure, vá para o grupo de recursos em que estão seus SQL Servers e clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="d4c53-354">Pesquise pelo **Balanceador de Carga**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="d4c53-355">Escolha o balanceador de carga publicado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d4c53-355">Choose the load balancer published by Microsoft.</span></span>

   ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="d4c53-357">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-357">Click **Create**.</span></span>
3. <span data-ttu-id="d4c53-358">Configure os seguintes parâmetros para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="d4c53-359">Configuração</span><span class="sxs-lookup"><span data-stu-id="d4c53-359">Setting</span></span> | <span data-ttu-id="d4c53-360">Campo</span><span class="sxs-lookup"><span data-stu-id="d4c53-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="d4c53-361">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d4c53-361">**Name**</span></span> |<span data-ttu-id="d4c53-362">Use um nome para o balanceador de carga, por exemplo, **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="d4c53-363">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="d4c53-363">**Type**</span></span> |<span data-ttu-id="d4c53-364">Interna</span><span class="sxs-lookup"><span data-stu-id="d4c53-364">Internal</span></span> |
   | <span data-ttu-id="d4c53-365">**Rede virtual**</span><span class="sxs-lookup"><span data-stu-id="d4c53-365">**Virtual network**</span></span> |<span data-ttu-id="d4c53-366">Use o nome da rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="d4c53-367">**Sub-rede**</span><span class="sxs-lookup"><span data-stu-id="d4c53-367">**Subnet**</span></span> |<span data-ttu-id="d4c53-368">Use o nome da sub-rede em que a máquina virtual está.</span><span class="sxs-lookup"><span data-stu-id="d4c53-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="d4c53-369">**Atribuição de endereço IP**</span><span class="sxs-lookup"><span data-stu-id="d4c53-369">**IP address assignment**</span></span> |<span data-ttu-id="d4c53-370">Estático</span><span class="sxs-lookup"><span data-stu-id="d4c53-370">Static</span></span> |
   | <span data-ttu-id="d4c53-371">**Endereço IP**</span><span class="sxs-lookup"><span data-stu-id="d4c53-371">**IP address**</span></span> |<span data-ttu-id="d4c53-372">Use um endereço disponível da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d4c53-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="d4c53-373">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="d4c53-373">**Subscription**</span></span> |<span data-ttu-id="d4c53-374">Use a mesma assinatura da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d4c53-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="d4c53-375">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="d4c53-375">**Location**</span></span> |<span data-ttu-id="d4c53-376">Use o mesmo local da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d4c53-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="d4c53-377">A folha do portal do Azure deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="d4c53-377">The Azure portal blade should look like this:</span></span>

   ![Criar balanceador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="d4c53-379">Clique em **Criar** para criar o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="d4c53-380">Para configurar o balanceador de carga, você precisará criar um pool de back-end, um teste e definir regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="d4c53-381">Faça isso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c53-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="d4c53-382">Adicionar pool de back-end</span><span class="sxs-lookup"><span data-stu-id="d4c53-382">Add backend pool</span></span>

1. <span data-ttu-id="d4c53-383">No portal do Azure, vá para o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="d4c53-384">Talvez seja necessário atualizar a exibição para ver o balanceador de carga recém-criado.</span><span class="sxs-lookup"><span data-stu-id="d4c53-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Encontrar o Balanceador de Carga no Grupo de Recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="d4c53-386">Clique no balanceador de carga, clique em **Pools de back-end**e clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="d4c53-387">Configure o pool de back-end da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4c53-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="d4c53-388">Configuração</span><span class="sxs-lookup"><span data-stu-id="d4c53-388">Setting</span></span> | <span data-ttu-id="d4c53-389">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c53-389">Description</span></span> | <span data-ttu-id="d4c53-390">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4c53-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="d4c53-391">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d4c53-391">**Name**</span></span> | <span data-ttu-id="d4c53-392">Digite um nome de texto</span><span class="sxs-lookup"><span data-stu-id="d4c53-392">Type a text name</span></span> | <span data-ttu-id="d4c53-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="d4c53-393">SQLLBBE</span></span>
   | <span data-ttu-id="d4c53-394">**Associado a**</span><span class="sxs-lookup"><span data-stu-id="d4c53-394">**Associated to**</span></span> | <span data-ttu-id="d4c53-395">Selecione uma opção na lista</span><span class="sxs-lookup"><span data-stu-id="d4c53-395">Pick from list</span></span> | <span data-ttu-id="d4c53-396">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d4c53-396">Availability set</span></span>
   | <span data-ttu-id="d4c53-397">**Conjunto de disponibilidade**</span><span class="sxs-lookup"><span data-stu-id="d4c53-397">**Availability set**</span></span> | <span data-ttu-id="d4c53-398">Use um nome do conjunto de disponibilidade em que suas VMs do SQL Server estão</span><span class="sxs-lookup"><span data-stu-id="d4c53-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="d4c53-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="d4c53-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="d4c53-400">**Máquinas virtuais**</span><span class="sxs-lookup"><span data-stu-id="d4c53-400">**Virtual machines**</span></span> |<span data-ttu-id="d4c53-401">Os dois nomes de VM do Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="d4c53-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="d4c53-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="d4c53-403">Digite o nome do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="d4c53-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="d4c53-404">Clique em **+ Adicionar uma máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="d4c53-405">Para o conjunto de disponibilidade, escolha o conjunto de disponibilidade em que os SQL Servers estão.</span><span class="sxs-lookup"><span data-stu-id="d4c53-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="d4c53-406">No caso das máquinas virtuais, inclua ambos os SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="d4c53-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="d4c53-407">Não inclua o servidor de testemunha de compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d4c53-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="d4c53-408">Clique em **OK** para criar o pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="d4c53-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="d4c53-409">Definir a investigação</span><span class="sxs-lookup"><span data-stu-id="d4c53-409">Set the probe</span></span>

1. <span data-ttu-id="d4c53-410">Clique no balanceador de carga, clique em **Investigação de integridade**e clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="d4c53-411">Defina a investigação de integridade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d4c53-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="d4c53-412">Configuração</span><span class="sxs-lookup"><span data-stu-id="d4c53-412">Setting</span></span> | <span data-ttu-id="d4c53-413">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c53-413">Description</span></span> | <span data-ttu-id="d4c53-414">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4c53-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="d4c53-415">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d4c53-415">**Name**</span></span> | <span data-ttu-id="d4c53-416">Texto</span><span class="sxs-lookup"><span data-stu-id="d4c53-416">Text</span></span> | <span data-ttu-id="d4c53-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="d4c53-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="d4c53-418">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="d4c53-418">**Protocol**</span></span> | <span data-ttu-id="d4c53-419">Escolher TCP</span><span class="sxs-lookup"><span data-stu-id="d4c53-419">Choose TCP</span></span> | <span data-ttu-id="d4c53-420">TCP</span><span class="sxs-lookup"><span data-stu-id="d4c53-420">TCP</span></span> |
   | <span data-ttu-id="d4c53-421">**Porta**</span><span class="sxs-lookup"><span data-stu-id="d4c53-421">**Port**</span></span> | <span data-ttu-id="d4c53-422">Qualquer porta não utilizada</span><span class="sxs-lookup"><span data-stu-id="d4c53-422">Any unused port</span></span> | <span data-ttu-id="d4c53-423">59999</span><span class="sxs-lookup"><span data-stu-id="d4c53-423">59999</span></span> |
   | <span data-ttu-id="d4c53-424">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="d4c53-424">**Interval**</span></span>  | <span data-ttu-id="d4c53-425">O tempo entre as tentativas de investigação, em segundos</span><span class="sxs-lookup"><span data-stu-id="d4c53-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="d4c53-426">5</span><span class="sxs-lookup"><span data-stu-id="d4c53-426">5</span></span> |
   | <span data-ttu-id="d4c53-427">**Limite não íntegro**</span><span class="sxs-lookup"><span data-stu-id="d4c53-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="d4c53-428">O número de falhas de investigação consecutivas que deve ocorrer para uma máquina virtual ser considerada não íntegra</span><span class="sxs-lookup"><span data-stu-id="d4c53-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="d4c53-429">2</span><span class="sxs-lookup"><span data-stu-id="d4c53-429">2</span></span> |

1. <span data-ttu-id="d4c53-430">Clique em **OK** para definir a investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="d4c53-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="d4c53-431">Definir as regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="d4c53-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="d4c53-432">Clique no balanceador de carga, clique em **Regras de balanceamento de carga**e clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="d4c53-433">Defina as regras de balanceamento de carga da forma indicada a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4c53-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="d4c53-434">Configuração</span><span class="sxs-lookup"><span data-stu-id="d4c53-434">Setting</span></span> | <span data-ttu-id="d4c53-435">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c53-435">Description</span></span> | <span data-ttu-id="d4c53-436">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4c53-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="d4c53-437">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d4c53-437">**Name**</span></span> | <span data-ttu-id="d4c53-438">Texto</span><span class="sxs-lookup"><span data-stu-id="d4c53-438">Text</span></span> | <span data-ttu-id="d4c53-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="d4c53-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="d4c53-440">**Endereço IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="d4c53-440">**Frontend IP address**</span></span> | <span data-ttu-id="d4c53-441">Escolher um endereço</span><span class="sxs-lookup"><span data-stu-id="d4c53-441">Choose an address</span></span> |<span data-ttu-id="d4c53-442">Use o endereço que você criou ao criar o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="d4c53-443">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="d4c53-443">**Protocol**</span></span> | <span data-ttu-id="d4c53-444">Escolher TCP</span><span class="sxs-lookup"><span data-stu-id="d4c53-444">Choose TCP</span></span> |<span data-ttu-id="d4c53-445">TCP</span><span class="sxs-lookup"><span data-stu-id="d4c53-445">TCP</span></span> |
   | <span data-ttu-id="d4c53-446">**Porta**</span><span class="sxs-lookup"><span data-stu-id="d4c53-446">**Port**</span></span> | <span data-ttu-id="d4c53-447">Usar a porta para a instância do SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4c53-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="d4c53-448">1433</span><span class="sxs-lookup"><span data-stu-id="d4c53-448">1433</span></span> |
   | <span data-ttu-id="d4c53-449">**Porta de back-end**</span><span class="sxs-lookup"><span data-stu-id="d4c53-449">**Backend Port**</span></span> | <span data-ttu-id="d4c53-450">Este campo não é usado quando o IP flutuante é definido para o retorno de servidor direto</span><span class="sxs-lookup"><span data-stu-id="d4c53-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="d4c53-451">1433</span><span class="sxs-lookup"><span data-stu-id="d4c53-451">1433</span></span> |
   | <span data-ttu-id="d4c53-452">**Investigação**</span><span class="sxs-lookup"><span data-stu-id="d4c53-452">**Probe**</span></span> |<span data-ttu-id="d4c53-453">O nome especificado para o teste</span><span class="sxs-lookup"><span data-stu-id="d4c53-453">The name you specified for the probe</span></span> | <span data-ttu-id="d4c53-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="d4c53-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="d4c53-455">**Persistência de sessão**</span><span class="sxs-lookup"><span data-stu-id="d4c53-455">**Session Persistence**</span></span> | <span data-ttu-id="d4c53-456">Lista suspensa</span><span class="sxs-lookup"><span data-stu-id="d4c53-456">Drop down list</span></span> | <span data-ttu-id="d4c53-457">**Nenhum**</span><span class="sxs-lookup"><span data-stu-id="d4c53-457">**None**</span></span> |
   | <span data-ttu-id="d4c53-458">**Tempo limite de ociosidade**</span><span class="sxs-lookup"><span data-stu-id="d4c53-458">**Idle Timeout**</span></span> | <span data-ttu-id="d4c53-459">Minutos para manter uma conexão TCP aberta</span><span class="sxs-lookup"><span data-stu-id="d4c53-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="d4c53-460">4</span><span class="sxs-lookup"><span data-stu-id="d4c53-460">4</span></span> |
   | <span data-ttu-id="d4c53-461">**IP flutuante (retorno de servidor direto)**</span><span class="sxs-lookup"><span data-stu-id="d4c53-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="d4c53-462">Habilitado</span><span class="sxs-lookup"><span data-stu-id="d4c53-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="d4c53-463">O retorno de servidor direto é definido durante a criação.</span><span class="sxs-lookup"><span data-stu-id="d4c53-463">Direct server return is set during creation.</span></span> <span data-ttu-id="d4c53-464">Ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="d4c53-464">It cannot be changed.</span></span>

1. <span data-ttu-id="d4c53-465">Clique em **OK** para definir as regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="d4c53-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="d4c53-466"><a name="configure-listener"></a> Configurar o ouvinte</span><span class="sxs-lookup"><span data-stu-id="d4c53-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="d4c53-467">A próxima etapa é configurar um ouvinte do Grupo de Disponibilidade no cluster de failover.</span><span class="sxs-lookup"><span data-stu-id="d4c53-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d4c53-468">Este tutorial mostra como criar um ouvinte usando um endereço IP de ILB.</span><span class="sxs-lookup"><span data-stu-id="d4c53-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="d4c53-469">Para criar um ou mais ouvintes usando um ou mais endereços IP, veja [Criar ouvinte e balanceador de carga do Grupo de Disponibilidade | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4c53-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="d4c53-470">Definir porta do ouvinte</span><span class="sxs-lookup"><span data-stu-id="d4c53-470">Set listener port</span></span>

<span data-ttu-id="d4c53-471">No SQL Server Management Studio, defina a porta do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d4c53-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="d4c53-472">Inicie o SQL Server Management Studio e conecte-se à réplica principal.</span><span class="sxs-lookup"><span data-stu-id="d4c53-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="d4c53-473">Navegue até **Alta Disponibilidade do AlwaysOn** | **Grupos de Disponibilidade** | **Ouvintes do Grupo de Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="d4c53-474">Agora você deve ver o nome do ouvinte que você criou no Gerenciador de Cluster de Failover.</span><span class="sxs-lookup"><span data-stu-id="d4c53-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="d4c53-475">Clique com o botão direito do mouse no nome do ouvinte e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="d4c53-476">Na caixa **Porta**, especifique o número da porta para o ouvinte do Grupo de Disponibilidade usando o $EndpointPort usado anteriormente (1433 era o padrão) e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4c53-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="d4c53-477">Agora você tem um Grupo de Disponibilidade do SQL Server em máquinas virtuais do Azure, em execução no modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4c53-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="d4c53-478">Testar conexão com o ouvinte</span><span class="sxs-lookup"><span data-stu-id="d4c53-478">Test connection to listener</span></span>

<span data-ttu-id="d4c53-479">Para testar a conexão:</span><span class="sxs-lookup"><span data-stu-id="d4c53-479">To test the connection:</span></span>

1. <span data-ttu-id="d4c53-480">RDP para um SQL Server que está na mesma rede virtual, mas não tem a réplica.</span><span class="sxs-lookup"><span data-stu-id="d4c53-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="d4c53-481">Você pode usar o outro SQL Server no cluster.</span><span class="sxs-lookup"><span data-stu-id="d4c53-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="d4c53-482">Use o utilitário **sqlcmd** para testar a conexão.</span><span class="sxs-lookup"><span data-stu-id="d4c53-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="d4c53-483">Por exemplo, o script a seguir estabelece uma conexão de **sqlcmd** com a réplica primária por meio do ouvinte com autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="d4c53-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="d4c53-484">Se o ouvinte estiver usando uma porta diferente da porta padrão (1433), especifique a porta na cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="d4c53-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="d4c53-485">Por exemplo, o comando sqlcmd a seguir conecta-se a um ouvinte na porta 1435:</span><span class="sxs-lookup"><span data-stu-id="d4c53-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="d4c53-486">A conexão SQLCMD se conecta automaticamente a qualquer instância do SQL Server que hospede a réplica primária.</span><span class="sxs-lookup"><span data-stu-id="d4c53-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="d4c53-487">Verifique se a porta especificada está aberta no firewall dos servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="d4c53-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="d4c53-488">Ambos os servidores exigem uma regra de entrada para a porta TCP que você usa.</span><span class="sxs-lookup"><span data-stu-id="d4c53-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="d4c53-489">Para saber mais, confira [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c53-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="d4c53-490">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4c53-490">Next steps</span></span>

- <span data-ttu-id="d4c53-491">[Adicionar um endereço IP a um balanceador de carga para um segundo grupo de disponibilidade](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="d4c53-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
