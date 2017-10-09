---
title: "aaaSet a origem de saudação e de destino para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset até a fonte de saudação e de destino quando replicar máquinas virtuais do Hyper-V toosecondary VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="2b3c8-103">Etapa 6: Configurar o destino e origem da replicação Olá</span><span class="sxs-lookup"><span data-stu-id="2b3c8-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="2b3c8-104">Depois de criar serviços de recuperação de um cofre para o Hyper-V replicação tooa VMM site secundário com [do Azure Site Recovery](site-recovery-overview.md), use este artigo tooset fonte hello e locais de replicação de destino.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="2b3c8-105">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2b3c8-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="2b3c8-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="2b3c8-106">Set up hello source environment</span></span>

<span data-ttu-id="2b3c8-107">Instale Olá provedor Azure Site Recovery em servidores do VMM e descobrir e registrar servidores no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="2b3c8-108">Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="2b3c8-110">Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="2b3c8-112">Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2b3c8-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="2b3c8-113">Baixe o arquivo de instalação do provedor Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="2b3c8-114">Baixe a chave de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-114">Download hello registration key.</span></span> <span data-ttu-id="2b3c8-115">Você precisará dela quando executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-115">You need this when you run setup.</span></span> <span data-ttu-id="2b3c8-116">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-116">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="2b3c8-118">Instale Olá provedor Azure Site Recovery no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="2b3c8-119">Você não precisa tooexplicitly instalar nada nos servidores de host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="2b3c8-120">Instalar Olá provedor Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2b3c8-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="2b3c8-121">Execute o arquivo de instalação do provedor de saudação em cada servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="2b3c8-122">Se o VMM for implantado em um cluster, a seguir Olá Olá primeira vez que você instala:</span><span class="sxs-lookup"><span data-stu-id="2b3c8-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="2b3c8-123">Instalar o provedor de saudação em um nó ativo e concluir o servidor do VMM Olá instalação tooregister Olá no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="2b3c8-124">Em seguida, instale Olá provedor em Olá outros nós.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="2b3c8-125">Nós de cluster devem todos executados Olá mesma versão do provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="2b3c8-126">A instalação executa algumas verificações de pré-requisitos e solicitações permissão toostop saudação do serviço do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="2b3c8-127">saudação de serviço do VMM será reiniciada automaticamente quando a instalação for concluída.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="2b3c8-128">Se você instalar em um cluster do VMM, você está função de Cluster Olá toostop solicitada.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="2b3c8-129">Em **Microsoft Update**, você pode aceitar toospecify que provedor serão instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="2b3c8-130">Em **instalação**, aceite ou modifique o local de instalação padrão hello e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="2b3c8-132">Após a conclusão da instalação, clique em **registrar** tooregister servidor de saudação no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="2b3c8-134">Em **nome do cofre**, verificar nome de saudação do cofre Olá quais saudação servidor será registrado.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="2b3c8-135">Clique em *Avançar*.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-135">Click *Next*.</span></span>

    ![Registros do servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="2b3c8-137">Em **Conexão de Internet**, especifique como o provedor de saudação em execução no servidor do VMM Olá se conecta tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Configurações da Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="2b3c8-139">Você pode especificar o provedor Olá deve se conectar diretamente toohello internet, ou por meio de um proxy.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="2b3c8-140">Especifique as configurações de proxy, se necessário.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="2b3c8-141">Se você usar um proxy, uma conta de RunAs VMM (DRAProxyAccount) é criada automaticamente Olá especificado, usando as credenciais do proxy.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="2b3c8-142">Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="2b3c8-143">Olá configurações da conta executar como podem ser modificadas no console do VMM hello > **configurações** > **segurança** > **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="2b3c8-144">Reinicie a alterações de tooupdate de serviço do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="2b3c8-145">Em **chave de registro**, selecione chave Olá que você baixou do Azure Site Recovery e copiou toohello o servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="2b3c8-146">configuração de criptografia de saudação é usada apenas quando você estiver replicando máquinas virtuais do Hyper-V no tooAzure de nuvens do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="2b3c8-147">Se você estiver replicando o site secundário tooa não é usado.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="2b3c8-148">Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="2b3c8-149">Em uma configuração de cluster, especifique nome de função de cluster saudação do VMM.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="2b3c8-150">Em **sincronizar metadados de nuvem**, selecione se deseja toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="2b3c8-151">Essa ação precisa apenas toohappen uma vez em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="2b3c8-152">Se você não quiser toosynchronize todas as nuvens, deixe essa configuração desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="2b3c8-153">Clique em **próximo** toocomplete processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="2b3c8-154">Após o registro, os metadados do servidor do VMM Olá são recuperados pelo Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="2b3c8-155">saudação do servidor é exibida em Olá **servidores VMM** guia Olá **servidores** página no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Servidor](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="2b3c8-157">Depois que o servidor hello está disponível no console de recuperação de Site Olá, em **fonte** > **preparar fonte** Selecionar servidor do VMM hello e nuvem Olá selecione em quais Olá Hyper-V host está localizado.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="2b3c8-158">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-158">Then click **OK**.</span></span>

<span data-ttu-id="2b3c8-159">Você também pode instalar o provedor Olá Olá linha de comando:</span><span class="sxs-lookup"><span data-stu-id="2b3c8-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="2b3c8-160">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="2b3c8-160">Set up hello target environment</span></span>

<span data-ttu-id="2b3c8-161">Selecione a nuvem e o servidor do VMM de destino hello:</span><span class="sxs-lookup"><span data-stu-id="2b3c8-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="2b3c8-162">Clique em **preparar infraestrutura** > **destino**e servidor do VMM de destino select Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="2b3c8-163">Nuvens no servidor de saudação que são sincronizadas com a recuperação de Site serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="2b3c8-164">Selecione a nuvem de destino hello.</span><span class="sxs-lookup"><span data-stu-id="2b3c8-164">Select hello target cloud.</span></span>

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="2b3c8-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b3c8-166">Next steps</span></span>

<span data-ttu-id="2b3c8-167">Vá muito[etapa 7: Configurar mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="2b3c8-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
