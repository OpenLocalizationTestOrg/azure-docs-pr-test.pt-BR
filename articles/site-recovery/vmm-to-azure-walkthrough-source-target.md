---
title: "Configure a origem e o destino da replicação do Hyper-V para o Azure (com o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas para definir as configurações de origem e destino para replicação de VMs do Hyper-V em nuvens do VMM para armazenamento do Azure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: c72f839d0a1288dccb7deb3e44fc2b20d64818f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-with-vmm-replication-to-azure"></a><span data-ttu-id="0021e-103">Etapa 8: Configurar a origem e o destino para replicação do Hyper-V (com o VMM) para o Azure</span><span class="sxs-lookup"><span data-stu-id="0021e-103">Step 8: Set up the source and target for Hyper-V (with VMM) replication to Azure</span></span>

<span data-ttu-id="0021e-104">Depois de [criar um cofre](vmm-to-azure-walkthrough-create-vault.md) e especificar o que você deseja replicar, use este artigo para definir as configurações de origem e de destino ao replicar local máquinas virtuais de Hyper-V nas nuvens do System Center Virtual Machine Manager (VMM) do Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0021e-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want to replicate, use this article to configure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="0021e-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0021e-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="0021e-106">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="0021e-106">Set up the source environment</span></span>

<span data-ttu-id="0021e-107">S1.</span><span class="sxs-lookup"><span data-stu-id="0021e-107">S1.</span></span> <span data-ttu-id="0021e-108">Clique em **Preparar a Infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="0021e-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="0021e-109">Em **Preparar origem**, clique em **+ VMM** para adicionar um servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-109">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="0021e-111">Em **Adicionar Servidor**, verifique se **Servidor System Center VMM** é exibido em **Tipo de servidor** e se o servidor VMM atende aos [pré-requisitos e aos requisitos de URL](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0021e-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="0021e-112">Baixe o arquivo de instalação do Provedor do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0021e-112">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="0021e-113">Baixe a chave do registro.</span><span class="sxs-lookup"><span data-stu-id="0021e-113">Download the registration key.</span></span> <span data-ttu-id="0021e-114">Você precisará dela quando executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="0021e-114">You need this when you run setup.</span></span> <span data-ttu-id="0021e-115">A chave é válida por cinco dias após ser gerada.</span><span class="sxs-lookup"><span data-stu-id="0021e-115">The key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-the-provider-on-the-vmm-server"></a><span data-ttu-id="0021e-117">Instalar o Provedor no servidor VMM</span><span class="sxs-lookup"><span data-stu-id="0021e-117">Install the Provider on the VMM server</span></span>

1. <span data-ttu-id="0021e-118">Execute o arquivo de configuração do provedor no servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-118">Run the Provider setup file on the VMM server.</span></span>
2. <span data-ttu-id="0021e-119">No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="0021e-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="0021e-120">Em **Instalação**, aceite ou modifique o local de instalação padrão do Provedor e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0021e-120">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>

    ![Local de instalação](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="0021e-122">Quando a instalação terminar, clique em **Registrar** para registrar o servidor do VMM no cofre.</span><span class="sxs-lookup"><span data-stu-id="0021e-122">When installation finishes, click **Register** to register the VMM server in the vault.</span></span>
5. <span data-ttu-id="0021e-123">Na página **Configurações do Cofre**, clique em **Procurar** para selecionar o arquivo da chave do cofre.</span><span class="sxs-lookup"><span data-stu-id="0021e-123">In the **Vault Settings** page, click **Browse** to select the vault key file.</span></span> <span data-ttu-id="0021e-124">Especifique a assinatura do Azure Site Recovery e o nome do cofre.</span><span class="sxs-lookup"><span data-stu-id="0021e-124">Specify the Azure Site Recovery subscription and the vault name.</span></span>

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="0021e-126">Em **Conexão da Internet**, especifique como o Provedor em execução no servidor VMM conectará a Recuperação de Site pela Internet.</span><span class="sxs-lookup"><span data-stu-id="0021e-126">In **Internet Connection**, specify how the Provider running on the VMM server will connect to Site Recovery over the internet.</span></span>

   * <span data-ttu-id="0021e-127">Se você quiser que o Provedor se conecte diretamente, selecione **Conectar diretamente o Azure Site Recovery sem um proxy**.</span><span class="sxs-lookup"><span data-stu-id="0021e-127">If you want the Provider to connect directly, select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="0021e-128">Se o proxy existente exigir autenticação ou se você quiser usar um proxy personalizado, selecione **Conectar o Azure Site Recovery com um servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="0021e-128">If your existing proxy requires authentication, or you want to use a custom proxy, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="0021e-129">Se você usar um proxy personalizado, especifique o endereço, a porta e as credenciais.</span><span class="sxs-lookup"><span data-stu-id="0021e-129">If you use a custom proxy, specify the address, port, and credentials.</span></span>
   * <span data-ttu-id="0021e-130">Se estiver usando um proxy, você já deverá ter concedido as URLs descritas em [pré-requisitos](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0021e-130">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="0021e-131">Se você usar um proxy personalizado, uma conta RunAs VMM (DRAProxyAccount) será criada automaticamente usando as credenciais de proxy especificadas.</span><span class="sxs-lookup"><span data-stu-id="0021e-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="0021e-132">Configure o servidor proxy para que essa conta possa ser autenticada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0021e-132">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="0021e-133">As configurações da conta RunAs VMM podem ser modificadas no console do VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-133">The VMM RunAs account settings can be modified in the VMM console.</span></span> <span data-ttu-id="0021e-134">Em **Configurações**, expanda **Segurança** > **Contas Executar como** e modifique a senha de DRAProxyAccount.</span><span class="sxs-lookup"><span data-stu-id="0021e-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify the password for DRAProxyAccount.</span></span> <span data-ttu-id="0021e-135">Você precisará reiniciar o serviço VMM para que essa configuração entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="0021e-135">You’ll need to restart the VMM service so that this setting takes effect.</span></span>

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="0021e-137">Aceite ou modifique o local de um certificado SSL automaticamente gerado para criptografia de dados.</span><span class="sxs-lookup"><span data-stu-id="0021e-137">Accept or modify the location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="0021e-138">Esse certificado é usado se você habilitar a criptografia de dados para uma nuvem protegida pelo Azure no portal de Recuperação de Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="0021e-138">This certificate is used if you enable data encryption for a cloud protected by Azure in the Azure Site Recovery portal.</span></span> <span data-ttu-id="0021e-139">Mantenha esse certificado protegido.</span><span class="sxs-lookup"><span data-stu-id="0021e-139">Keep this certificate safe.</span></span> <span data-ttu-id="0021e-140">Quando você executar um failover para o Azure, precisará dele para descriptografar se a criptografia de dados estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="0021e-140">When you run a failover to Azure you’ll need it to decrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="0021e-141">Em **Nome do servidor**, especifique um nome amigável para identificar o servidor VMM no cofre.</span><span class="sxs-lookup"><span data-stu-id="0021e-141">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="0021e-142">Em uma configuração de cluster, especifique o nome de função de cluster do VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-142">In a cluster configuration, specify the VMM cluster role name.</span></span>
9. <span data-ttu-id="0021e-143">Habilite **Sincronizar metadados de nuvem**, se quiser sincronizar os metadados para todas as nuvens no servidor VMM com o cofre.</span><span class="sxs-lookup"><span data-stu-id="0021e-143">Enable **Sync cloud metadata**, if you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="0021e-144">Esta ação só precisa acontecer uma vez em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="0021e-144">This action only needs to happen once on each server.</span></span> <span data-ttu-id="0021e-145">Se você não quiser sincronizar todas as nuvens, você pode deixar essa configuração desmarcada e sincronizar cada nuvem individualmente nas propriedades da nuvem no console VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-145">If you don't want to synchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in the cloud properties in the VMM console.</span></span> <span data-ttu-id="0021e-146">Clique em **Registrar** para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="0021e-146">Click **Register** to complete the process.</span></span>

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="0021e-148">O registro é iniciado.</span><span class="sxs-lookup"><span data-stu-id="0021e-148">Registration starts.</span></span> <span data-ttu-id="0021e-149">Após a conclusão do registro, o servidor é exibido em **Infraestrutura do Site Recovery** > **Servidores VMM**.</span><span class="sxs-lookup"><span data-stu-id="0021e-149">After registration finishes, the server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="0021e-150">Instalar o Agente de Serviços de Recuperação do Azure em hosts do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0021e-150">Install the Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="0021e-151">Depois de configurar o Provedor, será necessário baixar o arquivo de instalação do agente de Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0021e-151">After you've set up the Provider, you need to download the installation file for the Azure Recovery Services agent.</span></span> <span data-ttu-id="0021e-152">Execute a instalação em cada servidor do Hyper-V na nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="0021e-152">Run setup on each Hyper-V server in the VMM cloud.</span></span>

    ![Sites do Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="0021e-154">Em **Verificação de Pré-requisitos**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0021e-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="0021e-155">Quaisquer pré-requisitos faltantes serão instalados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0021e-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Agente de Serviços de Recuperação de Pré-requisitos](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="0021e-157">Em **Configurações da Instalação**, aceite ou modifique o local de instalação e o local do cache.</span><span class="sxs-lookup"><span data-stu-id="0021e-157">In **Installation Settings**, accept or modify the installation location, and the cache location.</span></span> <span data-ttu-id="0021e-158">Você pode configurar o cache em uma unidade que tenha pelo menos 5 GB de armazenamento disponível, mas é recomendável uma unidade de cache com 600 GB ou mais de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="0021e-158">You can configure the cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="0021e-159">Em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0021e-159">Then click **Install**.</span></span>
4. <span data-ttu-id="0021e-160">Quando a instalação terminar, clique no botão **Fechar** para concluir.</span><span class="sxs-lookup"><span data-stu-id="0021e-160">After installation is complete, click **Close** to finish.</span></span>

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="0021e-162">Instalação de linha de comando</span><span class="sxs-lookup"><span data-stu-id="0021e-162">Command line installation</span></span>
<span data-ttu-id="0021e-163">Você pode instalar o Agente de Serviços de Recuperação do Microsoft Azure por meio da linha de comando usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0021e-163">You can install the Microsoft Azure Recovery Services Agent from command line using the following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a><span data-ttu-id="0021e-164">Configurar o acesso de proxy de Internet para a Recuperação de Site de hosts do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0021e-164">Set up internet proxy access to Site Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="0021e-165">O agente dos Serviços de Recuperação em execução em hosts do Hyper-V precisam de acesso à Internet para o Azure para a replicação de VMs.</span><span class="sxs-lookup"><span data-stu-id="0021e-165">The Recovery Services agent running on Hyper-V hosts needs internet access to Azure for VM replication.</span></span> <span data-ttu-id="0021e-166">Se você estiver acessando a Internet por meio de um proxy, configure-o da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0021e-166">If you're accessing the internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="0021e-167">Abra o snap-in MMC do Backup do Microsoft Azure no host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0021e-167">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host.</span></span> <span data-ttu-id="0021e-168">Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho ou C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="0021e-168">By default, a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="0021e-169">No snap-in, clique em **Alterar Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="0021e-169">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="0021e-170">Na guia **Configuração do Proxy** , especifique as informações do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="0021e-170">On the **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="0021e-172">Verifique se o agente pode acessar as URLs descritas nos [pré-requisitos](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0021e-172">Check that the agent can reach the URLs described in the [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-the-target-environment"></a><span data-ttu-id="0021e-173">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="0021e-173">Set up the target environment</span></span>
<span data-ttu-id="0021e-174">Especifique a conta de armazenamento do Azure a ser usada para a replicação e a rede do Azure à qual as VMs do Azure se conectarão após o failover.</span><span class="sxs-lookup"><span data-stu-id="0021e-174">Specify the Azure storage account to be used for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="0021e-175">Clique em **Preparar infraestrutura** > **Destino**, selecione a assinatura e o grupo de recursos no qual deseja criar as máquinas virtuais do failover.</span><span class="sxs-lookup"><span data-stu-id="0021e-175">Click **Prepare infrastructure** > **Target**, select the subscription and the resource group where you want to create the failed over virtual machines.</span></span> <span data-ttu-id="0021e-176">Escolha o modelo de implantação que você deseja usar no Azure (clássico ou gerenciamento de recursos) para as máquinas virtuais do failover.</span><span class="sxs-lookup"><span data-stu-id="0021e-176">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span></span>

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="0021e-178">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="0021e-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="0021e-180">Se você não tiver criado uma conta de armazenamento e se desejar criar uma usando o Resource Manager, clique em **+Conta de armazenamento** para fazer isso de forma embutida.</span><span class="sxs-lookup"><span data-stu-id="0021e-180">If you haven't created a storage account, and you want to create one using Resource Manager, click **+Storage account** to do that inline.</span></span>  <span data-ttu-id="0021e-181">Na folha **Criar conta de armazenamento** , especifique um nome de conta, um tipo, uma assinatura e uma localização.</span><span class="sxs-lookup"><span data-stu-id="0021e-181">On the **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="0021e-182">A conta deve estar no mesmo local do que o cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="0021e-182">The account should be in the same location as the Recovery Services vault.</span></span>

   ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="0021e-184">Se você quiser criar uma conta de armazenamento usando o modelo clássico, faça isso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0021e-184">If you want to create a storage account using the classic model, do that in the Azure portal.</span></span> [<span data-ttu-id="0021e-185">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="0021e-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="0021e-186">Se você estiver usando uma conta de armazenamento premium para os dados replicados, configure uma conta de armazenamento standard adicional para armazenar os logs de replicação que capturam as alterações contínuas nos dados locais.</span><span class="sxs-lookup"><span data-stu-id="0021e-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, to store replication logs that capture ongoing changes to on-premises data.</span></span>
5. <span data-ttu-id="0021e-187">Se você não tiver criado uma rede do Azure e se quiser criar uma usando o Resource Manager, clique em **+Rede** para fazer isso de forma embutida.</span><span class="sxs-lookup"><span data-stu-id="0021e-187">If you haven't created an Azure network, and you want to create one using Resource Manager, click **+Network** to do that inline.</span></span> <span data-ttu-id="0021e-188">Na folha **Criar rede virtual** , especifique um nome de rede, um intervalo de endereços, detalhes de sub-rede, uma assinatura e uma localização.</span><span class="sxs-lookup"><span data-stu-id="0021e-188">On the **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="0021e-189">A rede deve estar no mesmo local do que o cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="0021e-189">The network should be in the same location as the Recovery Services vault.</span></span>

   ![Rede](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="0021e-191">Se você quiser criar uma rede usando o modelo clássico, faça isso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0021e-191">If you want to create a network using the classic model, do that in the Azure portal.</span></span> <span data-ttu-id="0021e-192">[Saiba mais](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="0021e-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="0021e-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0021e-193">Next steps</span></span>

<span data-ttu-id="0021e-194">Vá para a [Etapa 9: Configurar o mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="0021e-194">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
