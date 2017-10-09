---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação do Hyper-V (sem o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de armazenamento de tooAzure de VMs Hyper-V com o Azure Site Recovery"
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
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="fe0de-103">Etapa 8: Configurar a origem de saudação e de destino para tooAzure de replicação do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fe0de-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="fe0de-104">Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais (sem o System Center VMM) do Hyper-V, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0de-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="fe0de-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fe0de-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="fe0de-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="fe0de-106">Set up hello source environment</span></span>

<span data-ttu-id="fe0de-107">Configurar site Olá Hyper-V, instale hello provedor Azure Site Recovery e o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V e registrar site Olá no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe0de-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="fe0de-108">Em **Preparar a infraestrutura**, clique em **Origem**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="fe0de-109">Clique em um novo site de Hyper-V como um contêiner para seus hosts Hyper-V ou clusters de tooadd **+ Site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="fe0de-111">Em **site Hyper-V criar**, especifique um nome para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe0de-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="fe0de-112">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-112">Then click **OK**.</span></span> <span data-ttu-id="fe0de-113">Agora, selecione o site Olá você criou e clique em **+ servidor Hyper-V** tooadd um site de toohello do servidor.</span><span class="sxs-lookup"><span data-stu-id="fe0de-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="fe0de-115">Em **Adicionar Servidor** > **Tipo de servidor**, verifique se **Servidor Hyper-V** é exibido.</span><span class="sxs-lookup"><span data-stu-id="fe0de-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="fe0de-116">Verifique se o servidor Olá Hyper-V você deseja tooadd está em conformidade com hello [pré-requisitos](#on-premises-prerequisites), e é capaz de tooaccess Olá URLs especificadas.</span><span class="sxs-lookup"><span data-stu-id="fe0de-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="fe0de-117">Baixe o arquivo de instalação do provedor Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="fe0de-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="fe0de-118">Executar este Olá tooinstall do arquivo provedor e Olá agente de serviços de recuperação em cada host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe0de-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Configurar origem](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="fe0de-120">Instalar hello provedor e agente</span><span class="sxs-lookup"><span data-stu-id="fe0de-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="fe0de-121">Execute o arquivo de instalação do provedor de saudação em cada host que você adicionou site toohello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fe0de-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="fe0de-122">Se você estiver instalando em um cluster do Hyper-V, execute a instalação em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="fe0de-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="fe0de-123">Instalar e registrar cada nó de cluster do Hyper-V garante que as VMs estarão protegidas, mesmo se migrarem entre nós.</span><span class="sxs-lookup"><span data-stu-id="fe0de-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="fe0de-124">No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="fe0de-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="fe0de-125">Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="fe0de-126">Em **as configurações do cofre**, clique em **procurar** tooselect Olá cofre arquivo de chave que você baixou.</span><span class="sxs-lookup"><span data-stu-id="fe0de-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="fe0de-127">Especifique a assinatura do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.</span><span class="sxs-lookup"><span data-stu-id="fe0de-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Registros do servidor](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="fe0de-129">Em **as configurações de Proxy**, especifique como Olá tooAzure recuperação de Site se conecta de provedor em execução em hosts Hyper-V em Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="fe0de-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="fe0de-130">Se você quiser Olá provedor tooconnect diretamente selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="fe0de-131">Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado para conexão de provedor hello, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="fe0de-132">Se você usar um proxy:</span><span class="sxs-lookup"><span data-stu-id="fe0de-132">If you use a proxy:</span></span>
        - <span data-ttu-id="fe0de-133">Especificar credenciais, porta e endereço Olá</span><span class="sxs-lookup"><span data-stu-id="fe0de-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="fe0de-134">Criar URLs de saudação se descrito em Olá [pré-requisitos](#prerequisites) são permitidas por meio do proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe0de-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="fe0de-136">Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="fe0de-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Local de instalação](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="fe0de-138">Após a conclusão do registro, os metadados do servidor de saudação Hyper-V são recuperados pelo Azure Site Recovery e saudação do servidor é exibida no **infra-estrutura de recuperação de Site** > **Hosts Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="fe0de-139">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="fe0de-139">Set up hello target environment</span></span>

<span data-ttu-id="fe0de-140">Especifique a conta de armazenamento do Azure Olá para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="fe0de-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="fe0de-141">Clique em **Preparar a Infraestrutura** > **Destino**.</span><span class="sxs-lookup"><span data-stu-id="fe0de-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="fe0de-142">Selecione a assinatura de saudação e grupo de recursos de saudação no qual você deseja toocreate Olá VMs do Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="fe0de-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="fe0de-143">Escolha deployment Olá modelo que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="fe0de-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="fe0de-144">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="fe0de-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="fe0de-145">Se você não tiver uma conta de armazenamento, clique em **+ armazenamento** toocreate embutido uma conta baseada no Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fe0de-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="fe0de-146">Se você não tiver uma rede do Azure, clique em **+ rede** toocreate embutido um Gerenciador de recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="fe0de-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="fe0de-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe0de-147">Next steps</span></span>

<span data-ttu-id="fe0de-148">Vá muito[etapa 9: configurar uma política de replicação](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="fe0de-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
