---
title: "Configurar a origem e destino de replicação do Hyper-V para um site secundário com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como configurar a origem e o destino ao replicar VMs do Hyper-V para um site de VMM secundário com o Azure Site Recovery."
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
ms.openlocfilehash: 07135e9b5e619971a59cc22ec68a0a4e8bcaabe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-set-up-the-replication-source-and-target"></a><span data-ttu-id="7cb6d-103">Etapa 6: Configurar a origem e o destino de replicação</span><span class="sxs-lookup"><span data-stu-id="7cb6d-103">Step 6: Set up the replication source and target</span></span>


<span data-ttu-id="7cb6d-104">Depois de criar um cofre para os Serviços de Recuperação para replicação do Hyper-V em um site secundário do VMM com o [Azure Site Recovery](site-recovery-overview.md), use este artigo para configurar os locais de replicação de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-104">After creating a Recovery Services vault for Hyper-V replication to a secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article to set up the source and target replication locations.</span></span> 

<span data-ttu-id="7cb6d-105">Depois de ler este artigo, poste comentários na parte inferior ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7cb6d-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-the-source-environment"></a><span data-ttu-id="7cb6d-106">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="7cb6d-106">Set up the source environment</span></span>

<span data-ttu-id="7cb6d-107">Instale o Provedor do Azure Site Recovery nos servidores VMM e descubra e registre os servidores no cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-107">Install the Azure Site Recovery Provider on VMM servers, and discover and register servers in the vault.</span></span>

1. <span data-ttu-id="7cb6d-108">Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="7cb6d-110">Em **Preparar origem**, clique em **+ VMM** para adicionar um servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-110">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="7cb6d-112">Em **Adicionar Servidor**, verifique se **Servidor System Center VMM** é exibido em **Tipo de servidor** e se o servidor VMM atende aos [pré-requisitos](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7cb6d-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="7cb6d-113">Baixe o arquivo de instalação do Provedor do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-113">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="7cb6d-114">Baixe a chave do registro.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-114">Download the registration key.</span></span> <span data-ttu-id="7cb6d-115">Você precisará dela quando executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-115">You need this when you run setup.</span></span> <span data-ttu-id="7cb6d-116">A chave é válida por cinco dias após ser gerada.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-116">The key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="7cb6d-118">Instale o Provedor do Azure Site Recovery no servidor do VMM de origem.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-118">Install the Azure Site Recovery Provider on the VMM server.</span></span> <span data-ttu-id="7cb6d-119">Você não precisa instalar nada explicitamente nos servidores de host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-119">You don't need to explicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-the-azure-site-recovery-provider"></a><span data-ttu-id="7cb6d-120">Instalar o Provedor de Recuperação do Site do Azure</span><span class="sxs-lookup"><span data-stu-id="7cb6d-120">Install the Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="7cb6d-121">Execute o arquivo de configuração do Provedor em cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-121">Run the Provider setup file on each VMM server.</span></span> <span data-ttu-id="7cb6d-122">Se o VMM é implantado em um cluster, faça o seguinte na primeira vez que você instala:</span><span class="sxs-lookup"><span data-stu-id="7cb6d-122">If VMM is deployed in a cluster, do the following the first time you install:</span></span>
    -  <span data-ttu-id="7cb6d-123">Instale o provedor em um nó ativo e conclua a instalação para registrar o servidor VMM no cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-123">Install the provider on an active node, and finish the installation to register the VMM server in the vault.</span></span>
    - <span data-ttu-id="7cb6d-124">Em seguida, instale o Provedor nos outros nós.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-124">Then, install the Provider on the other nodes.</span></span> <span data-ttu-id="7cb6d-125">Nós de cluster devem todos executar a mesma versão do provedor.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-125">Cluster nodes should all run the same version of the Provider.</span></span>
2. <span data-ttu-id="7cb6d-126">A instalação executa algumas verificações de pré-requisito e solicita permissão para interromper o serviço do VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-126">Setup runs a few prerequisite checks, and requests permission to stop the VMM service.</span></span> <span data-ttu-id="7cb6d-127">O serviço VMM será reiniciado automaticamente quando a instalação for finalizada.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-127">The VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="7cb6d-128">Se estiver instalando em um cluster do VMM, será solicitado que você pare a função de Cluster.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-128">If you install on a VMM cluster, you're prompted to stop the Cluster role.</span></span>
3. <span data-ttu-id="7cb6d-129">No **Microsoft Update**, você pode aceitar que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-129">In **Microsoft Update**, you can opt in to specify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="7cb6d-130">Em **Instalação**, aceite ou modifique o local de instalação padrão e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-130">In **Installation**, accept or modify the default installation location, and click **Install**.</span></span>

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="7cb6d-132">Quando a instalação for concluída, clique em **Registrar** para registrar o servidor no cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-132">After installation is complete, click **Register** to register the server in the vault.</span></span>

    ![Local de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="7cb6d-134">Em **Nome do cofre**, verifique o nome do cofre para o qual o servidor será registrado.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-134">In **Vault name**, verify the name of the vault in which the server will be registered.</span></span> <span data-ttu-id="7cb6d-135">Clique em *Próximo*.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-135">Click *Next*.</span></span>

    ![Registros do servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="7cb6d-137">Em **Conexão com a Internet**, especifique como o provedor em execução no servidor VMM se conecta ao Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-137">In **Internet Connection**, specify how the provider running on the VMM server connects to Azure.</span></span>

    ![Configurações da Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="7cb6d-139">Você pode especificar que o provedor deve se conectar diretamente à internet ou por meio de um proxy.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-139">You can specify that the provider should connect directly to the internet, or via a proxy.</span></span>
   - <span data-ttu-id="7cb6d-140">Especifique as configurações de proxy, se necessário.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="7cb6d-141">Se você usar um proxy, uma conta RunAs do VMM (DRAProxyAccount) será criada automaticamente usando as credenciais de proxy especificadas.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="7cb6d-142">Configure o servidor proxy para que essa conta possa ser autenticada com êxito.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-142">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="7cb6d-143">As configurações de conta executar como podem ser modificadas no console do VMM > **configurações** > **segurança** > **contas executar como**.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-143">The RunAs account settings can be modified in the VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="7cb6d-144">Reinicie o serviço VMM para atualizar as alterações.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-144">Restart the VMM service to update changes.</span></span>
8. <span data-ttu-id="7cb6d-145">Em **Chave de Registro**, selecione a chave que você baixou no Azure Site Recovery e copiou para o servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-145">In **Registration Key**, select the key that you downloaded from Azure Site Recovery and copied to the VMM server.</span></span>
9. <span data-ttu-id="7cb6d-146">A configuração de criptografia é usada somente quando você estiver replicando VMs do Hyper-V em nuvens do VMM no Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-146">The encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds to Azure.</span></span> <span data-ttu-id="7cb6d-147">Se estiver replicando para um site secundário, ela não é usada.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-147">If you're replicating to a secondary site it's not used.</span></span>
10. <span data-ttu-id="7cb6d-148">Em **Nome do servidor**, especifique um nome amigável para identificar o servidor VMM no cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-148">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="7cb6d-149">Em uma configuração de cluster, especifique o nome de função de cluster do VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-149">In a cluster configuration specify the VMM cluster role name.</span></span>
11. <span data-ttu-id="7cb6d-150">Em **Sincronizar metadados de nuvem**, selecione se você deseja sincronizar os metadados para todas as nuvens no servidor VMM com o cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-150">In **Synchronize cloud metadata**, select whether you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="7cb6d-151">Esta ação só precisa acontecer uma vez em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-151">This action only needs to happen once on each server.</span></span> <span data-ttu-id="7cb6d-152">Se você não desejar sincronizar todas as nuvens, deixe essa configuração desmarcada e sincronize cada nuvem individualmente nas propriedades da nuvem no console do VMM.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-152">If you don't want to synchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in the cloud properties in the VMM console.</span></span>
12. <span data-ttu-id="7cb6d-153">Clique em **Avançar** para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-153">Click **Next** to complete the process.</span></span> <span data-ttu-id="7cb6d-154">Após o registro, os metadados do servidor VMM é recuperado pela Recuperação de Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-154">After registration, metadata from the VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="7cb6d-155">O servidor é exibido na guia **Servidores VMM** da página **Servidores** no cofre.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-155">The server is displayed on the **VMM Servers** tab on the **Servers** page in the vault.</span></span>

    ![Servidor](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="7cb6d-157">Depois que o servidor estiver disponível no console de Recuperação de Site, em **Origem** > **Preparar origem** selecione o servidor VMM e selecione a nuvem na qual o host Hyper-V está localizado.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-157">After the server is available in the Site Recovery console, in **Source** > **Prepare source** select the VMM server, and select the cloud in which the Hyper-V host is located.</span></span> <span data-ttu-id="7cb6d-158">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-158">Then click **OK**.</span></span>

<span data-ttu-id="7cb6d-159">Você também pode instalar o provedor usando a linha de comando:</span><span class="sxs-lookup"><span data-stu-id="7cb6d-159">You can also install the provider from the command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-the-target-environment"></a><span data-ttu-id="7cb6d-160">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="7cb6d-160">Set up the target environment</span></span>

<span data-ttu-id="7cb6d-161">Selecione o servidor VMM e a nuvem de destino:</span><span class="sxs-lookup"><span data-stu-id="7cb6d-161">Select the target VMM server and cloud:</span></span>

1. <span data-ttu-id="7cb6d-162">Clique em **Preparar infraestrutura** > **Destino** e selecione o servidor VMM de destino que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-162">Click **Prepare infrastructure** > **Target**, and select the target VMM server you want to use.</span></span>
2. <span data-ttu-id="7cb6d-163">Nuvens no servidor sincronizadas com a Recuperação de Site serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-163">Clouds on the server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="7cb6d-164">Selecione a nuvem de destino.</span><span class="sxs-lookup"><span data-stu-id="7cb6d-164">Select the target cloud.</span></span>

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="7cb6d-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7cb6d-166">Next steps</span></span>

<span data-ttu-id="7cb6d-167">Acesse a [Etapa 7: Configurar o mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="7cb6d-167">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
