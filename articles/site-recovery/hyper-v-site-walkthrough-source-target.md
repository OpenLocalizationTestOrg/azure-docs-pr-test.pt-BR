---
title: "Configure a origem e o destino da replicação do Hyper-V para o Azure (sem o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas para definir as configurações de origem e destino para replicação de VMs Hyper-V para armazenamento do Azure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="65b83-103">Etapa 8: configurar a origem e o destino para replicação do Hyper-V para o Azure</span><span class="sxs-lookup"><span data-stu-id="65b83-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="65b83-104">Este artigo descreve como definir as configurações de origem e destino ao replicar máquinas virtuais Hyper-V locais (sem o System Center VMM) para o Azure utilizando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="65b83-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="65b83-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="65b83-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="65b83-106">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="65b83-106">Set up the source environment</span></span>

<span data-ttu-id="65b83-107">Configure o site do Hyper-V, instale o Provedor do Azure Site Recovery e o agente dos Serviços de Recuperação do Azure em hosts do Hyper-V e registre o site no cofre.</span><span class="sxs-lookup"><span data-stu-id="65b83-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="65b83-108">Em **Preparar a infraestrutura**, clique em **Origem**.</span><span class="sxs-lookup"><span data-stu-id="65b83-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="65b83-109">Para adicionar um novo site do Hyper-V como um contêiner para seus hosts ou clusters do Hyper-V, clique em **+ Site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="65b83-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="65b83-111">Em **Criar site do Hyper-V**, especifique um nome para o site.</span><span class="sxs-lookup"><span data-stu-id="65b83-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="65b83-112">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="65b83-112">Then click **OK**.</span></span> <span data-ttu-id="65b83-113">Agora, selecione o site que você criou e clique em **+Servidor Hyper-V** para adicionar um servidor ao site.</span><span class="sxs-lookup"><span data-stu-id="65b83-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="65b83-115">Em **Adicionar Servidor** > **Tipo de servidor**, verifique se **Servidor Hyper-V** é exibido.</span><span class="sxs-lookup"><span data-stu-id="65b83-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="65b83-116">Certifique-se de que o servidor Hyper-V que você deseja adicionar seja compatível com os [pré-requisitos](#on-premises-prerequisites) e seja capaz de acessar as URLs especificadas.</span><span class="sxs-lookup"><span data-stu-id="65b83-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="65b83-117">Baixe o arquivo de instalação do Provedor do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="65b83-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="65b83-118">Você executa esse arquivo para instalar o Provedor e o agente dos Serviços de Recuperação em cada host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="65b83-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="65b83-120">Instalar o Provedor e o agente</span><span class="sxs-lookup"><span data-stu-id="65b83-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="65b83-121">Execute o arquivo de configuração do Provedor em cada host que você adicionou ao site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="65b83-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="65b83-122">Se você estiver instalando em um cluster do Hyper-V, execute a instalação em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="65b83-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="65b83-123">Instalar e registrar cada nó de cluster do Hyper-V garante que as VMs estarão protegidas, mesmo se migrarem entre nós.</span><span class="sxs-lookup"><span data-stu-id="65b83-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="65b83-124">No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="65b83-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="65b83-125">Em **Instalação**, aceite ou modifique o local de instalação padrão do Provedor e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="65b83-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="65b83-126">Em **Configurações do Cofre**, clique em **Procurar** para selecionar o arquivo da chave do cofre baixado.</span><span class="sxs-lookup"><span data-stu-id="65b83-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="65b83-127">Especifique a assinatura do Azure Site Recovery, o nome do cofre e o site de Hyper-V ao qual pertence o servidor Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="65b83-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Registros do servidor](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="65b83-129">Em **Configurações de Proxy**, especifique como o Provedor em execução nos hosts Hyper-V se conecta ao Azure Site Recovery pela Internet.</span><span class="sxs-lookup"><span data-stu-id="65b83-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="65b83-130">Se você quiser que o Provedor conecte diretamente, selecione **Conectar diretamente o Azure Site Recovery sem um proxy**.</span><span class="sxs-lookup"><span data-stu-id="65b83-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="65b83-131">Se o proxy existente exigir autenticação ou se você quiser usar um proxy personalizado para a conexão ao Provedor, selecione **Conectar o Azure Site Recovery com um servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="65b83-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="65b83-132">Se você usar um proxy:</span><span class="sxs-lookup"><span data-stu-id="65b83-132">If you use a proxy:</span></span>
        - <span data-ttu-id="65b83-133">Especifique o endereço, a porta e as credenciais</span><span class="sxs-lookup"><span data-stu-id="65b83-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="65b83-134">Certifique-se de que as URLs descritas nos [pré-requisitos](#prerequisites) sejam permitidas através do proxy.</span><span class="sxs-lookup"><span data-stu-id="65b83-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="65b83-136">Quando a instalação terminar, clique em **Registrar** para registrar o servidor no cofre.</span><span class="sxs-lookup"><span data-stu-id="65b83-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Local de instalação](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="65b83-138">Após a conclusão do registro, os metadados do servidor Hyper-V são recuperados pelo Azure Site Recovery e o servidor é exibido em **Infraestrutura do Site Recovery** > **Hosts Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="65b83-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="65b83-139">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="65b83-139">Set up the target environment</span></span>

<span data-ttu-id="65b83-140">Especifique a conta de armazenamento do Azure para a replicação e a rede do Azure à qual as VMs do Azure se conectarão após o failover.</span><span class="sxs-lookup"><span data-stu-id="65b83-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="65b83-141">Clique em **Preparar a Infraestrutura** > **Destino**.</span><span class="sxs-lookup"><span data-stu-id="65b83-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="65b83-142">Selecione a assinatura e o grupo de recursos em que você deseja criar as VMs do Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="65b83-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="65b83-143">Escolha o modelo de implantação que você deseja usar no Azure (clássico ou gerenciamento de recursos) para as VMs.</span><span class="sxs-lookup"><span data-stu-id="65b83-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="65b83-144">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="65b83-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="65b83-145">Se você não tiver uma conta de armazenamento, clique em **+Armazenamento** para criar um conta embutida baseada no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65b83-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="65b83-146">Se você não tiver uma rede do Azure, clique em **+Rede** para criar um rede embutida baseada no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65b83-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="65b83-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65b83-147">Next steps</span></span>

<span data-ttu-id="65b83-148">Vá para a [Etapa 9: Configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="65b83-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
