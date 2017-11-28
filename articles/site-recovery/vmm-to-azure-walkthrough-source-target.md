---
title: "aaaSet a origem de saudação e de destino para tooAzure de replicação do Hyper-V (com o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de máquinas virtuais do Hyper-V no armazenamento de tooAzure de nuvens do VMM com o Azure Site Recovery"
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
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="ce872-103">Etapa 8: Configurar a origem de saudação e de destino para tooAzure de replicação do Hyper-V (com o VMM)</span><span class="sxs-lookup"><span data-stu-id="ce872-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="ce872-104">Depois de [criar um cofre](vmm-to-azure-walkthrough-create-vault.md) e especificar o que você deseja tooreplicate, usar esta fonte de tooconfigure de artigo e configurações de destino durante a replicação de máquinas virtuais de Hyper-V no local no System Center Virtual Machine Manager (VMM) tooAzure de nuvens, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce872-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="ce872-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ce872-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="ce872-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="ce872-106">Set up hello source environment</span></span>

<span data-ttu-id="ce872-107">S1.</span><span class="sxs-lookup"><span data-stu-id="ce872-107">S1.</span></span> <span data-ttu-id="ce872-108">Clique em **Preparar a Infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="ce872-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="ce872-109">Em **preparar fonte**, clique em **+ VMM** tooadd um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="ce872-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="ce872-111">Em **Adicionar servidor**, verifique se **servidor do System Center VMM** aparece na **tipo de servidor** e servidor do VMM Olá atende Olá [pré-requisitos e URL requisitos de](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="ce872-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="ce872-112">Baixe o arquivo de instalação do provedor Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="ce872-113">Baixe a chave de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce872-113">Download hello registration key.</span></span> <span data-ttu-id="ce872-114">Você precisará dela quando executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="ce872-114">You need this when you run setup.</span></span> <span data-ttu-id="ce872-115">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="ce872-115">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="ce872-117">Instalar Olá provedor no servidor do VMM Olá</span><span class="sxs-lookup"><span data-stu-id="ce872-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="ce872-118">Execute o arquivo de instalação do provedor Olá no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="ce872-119">No **Microsoft Update**, você pode aceitar as atualizações para que as atualizações do Provedor sejam instaladas de acordo com a política do Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ce872-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="ce872-120">Em **instalação**, aceite ou modifique o local de instalação do provedor de padrão de saudação e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="ce872-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![Local de instalação](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="ce872-122">Quando a instalação for concluída, clique em **registrar** servidor do VMM Olá tooregister no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="ce872-123">Em Olá **as configurações do cofre** , clique em **procurar** tooselect arquivo de chave do Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce872-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="ce872-124">Especifique a assinatura do Azure Site Recovery hello e nome do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="ce872-126">Em **Conexão de Internet**, especifique como Olá provedor em execução no servidor do VMM Olá conectará tooSite recuperação sobre Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="ce872-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="ce872-127">Se você desejar Olá provedor tooconnect diretamente, selecione **se conectar diretamente tooAzure recuperação de Site sem um proxy**.</span><span class="sxs-lookup"><span data-stu-id="ce872-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="ce872-128">Se o proxy existente exige autenticação ou deseja toouse um proxy personalizado, selecione **conectar tooAzure recuperação de Site usando um servidor proxy**.</span><span class="sxs-lookup"><span data-stu-id="ce872-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="ce872-129">Se você usar um proxy personalizado, especifique as credenciais, porta e endereço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce872-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="ce872-130">Se você estiver usando um proxy, você deve ter já Olá URLs permitidas descritos em [pré-requisitos](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="ce872-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="ce872-131">Se você usar um proxy personalizado, uma conta de RunAs VMM (DRAProxyAccount) será criada automaticamente Olá especificado, usando as credenciais do proxy.</span><span class="sxs-lookup"><span data-stu-id="ce872-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="ce872-132">Configure o servidor de proxy de saudação para que essa conta possa autenticar com êxito.</span><span class="sxs-lookup"><span data-stu-id="ce872-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="ce872-133">configurações de conta de RunAs VMM Olá podem ser modificadas no console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="ce872-134">Em **configurações**, expanda **segurança** > **contas executar como**e, em seguida, modificar a senha Olá para DRAProxyAccount.</span><span class="sxs-lookup"><span data-stu-id="ce872-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="ce872-135">O serviço VMM toorestart hello, será necessário para que essa configuração tenha efeito.</span><span class="sxs-lookup"><span data-stu-id="ce872-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="ce872-137">Aceite ou modifique o local de saudação de um certificado SSL que é gerado automaticamente para a criptografia de dados.</span><span class="sxs-lookup"><span data-stu-id="ce872-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="ce872-138">Este certificado será usado se você habilitar a criptografia de dados para uma nuvem protegida pelo Azure no portal do Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="ce872-139">Mantenha esse certificado protegido.</span><span class="sxs-lookup"><span data-stu-id="ce872-139">Keep this certificate safe.</span></span> <span data-ttu-id="ce872-140">Quando você executa um failover tooAzure você precisará dele toodecrypt, se a criptografia de dados está habilitada.</span><span class="sxs-lookup"><span data-stu-id="ce872-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="ce872-141">Em **nome do servidor**, especifique um servidor do VMM do nome amigável tooidentify Olá no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="ce872-142">Em uma configuração de cluster, especifique o nome de função de cluster saudação do VMM.</span><span class="sxs-lookup"><span data-stu-id="ce872-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="ce872-143">Habilitar **sincronizar metadados de nuvem**, se você quiser toosynchronize metadados para todas as nuvens no servidor do VMM Olá cofre hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="ce872-144">Essa ação precisa apenas toohappen uma vez em cada servidor.</span><span class="sxs-lookup"><span data-stu-id="ce872-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="ce872-145">Se você não quiser toosynchronize todas as nuvens, você pode deixar essa configuração está desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem Olá no console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="ce872-146">Clique em **registrar** toocomplete processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce872-146">Click **Register** toocomplete hello process.</span></span>

    ![Registros do servidor](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="ce872-148">O registro é iniciado.</span><span class="sxs-lookup"><span data-stu-id="ce872-148">Registration starts.</span></span> <span data-ttu-id="ce872-149">Após a conclusão do registro, o servidor de saudação é exibido na **infra-estrutura de recuperação de Site** > **servidores VMM**.</span><span class="sxs-lookup"><span data-stu-id="ce872-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="ce872-150">Instalar o agente de serviços de recuperação do Azure Olá nos hosts Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ce872-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="ce872-151">Depois de configurar Olá provedor, você precisa arquivo de instalação toodownload Olá para agente de serviços de recuperação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="ce872-152">Execute a instalação em cada servidor Hyper-V Olá nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="ce872-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Sites do Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="ce872-154">Em **Verificação de Pré-requisitos**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ce872-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="ce872-155">Quaisquer pré-requisitos faltantes serão instalados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ce872-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Agente de Serviços de Recuperação de Pré-requisitos](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="ce872-157">Em **configurações de instalação**, aceite ou modifique o local de instalação hello e Olá cache local.</span><span class="sxs-lookup"><span data-stu-id="ce872-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="ce872-158">Você pode configurar o cache de saudação em uma unidade que tenha pelo menos 5 GB de armazenamento disponível, mas é recomendável uma unidade de cache com 600 GB ou mais de espaço livre.</span><span class="sxs-lookup"><span data-stu-id="ce872-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="ce872-159">Em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ce872-159">Then click **Install**.</span></span>
4. <span data-ttu-id="ce872-160">Após a conclusão da instalação, clique em **fechar** toofinish.</span><span class="sxs-lookup"><span data-stu-id="ce872-160">After installation is complete, click **Close** toofinish.</span></span>

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="ce872-162">Instalação de linha de comando</span><span class="sxs-lookup"><span data-stu-id="ce872-162">Command line installation</span></span>
<span data-ttu-id="ce872-163">Você pode instalar Olá Microsoft Azure Recovery Services Agent na linha de comando usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce872-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="ce872-164">Configurar tooSite de acesso de proxy de internet recuperação a partir de hosts Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ce872-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="ce872-165">Agente de serviços de recuperação de saudação em execução em hosts do Hyper-V precisa tooAzure de acesso à internet para replicação de VM.</span><span class="sxs-lookup"><span data-stu-id="ce872-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="ce872-166">Se você estiver acessando Olá internet através de um proxy, configurá-lo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ce872-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="ce872-167">Abra o snap-in MMC do Backup do Microsoft Azure de saudação no host do Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="ce872-168">Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="ce872-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="ce872-169">Olá snap-in, clique em **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ce872-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="ce872-170">Em Olá **configuração de Proxy** especifique as informações do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="ce872-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![Registrar o Agente MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="ce872-172">Verifique que o agente Olá pode alcançar Olá URLs descritos em Olá [pré-requisitos](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="ce872-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="ce872-173">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="ce872-173">Set up hello target environment</span></span>
<span data-ttu-id="ce872-174">Especifique Olá toobe de conta de armazenamento do Azure usado para replicação e Olá toowhich de rede do Azure VMs do Azure irão se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="ce872-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="ce872-175">Clique em **preparar infraestrutura** > **destino**, selecione a assinatura hello e Olá onde você deseja toocreate Olá failover de máquinas virtuais do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce872-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="ce872-176">Escolha o modelo de implantação de saudação que você deseja toouse no Azure (gerenciamento clássico ou recurso) para Olá máquinas virtuais com failover.</span><span class="sxs-lookup"><span data-stu-id="ce872-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="ce872-178">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="ce872-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="ce872-180">Se você não tiver criado uma conta de armazenamento, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ conta de armazenamento** toodo que embutido.</span><span class="sxs-lookup"><span data-stu-id="ce872-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="ce872-181">Em Olá **criar conta de armazenamento** folha especificar um nome de conta, tipo, assinatura e local.</span><span class="sxs-lookup"><span data-stu-id="ce872-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="ce872-182">Olá conta deve ser no hello Cofre de serviços de recuperação do mesmo local que hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![Armazenamento](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="ce872-184">Se você quiser toocreate uma conta de armazenamento usando o modelo clássico hello, use Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce872-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="ce872-185">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="ce872-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="ce872-186">Se você estiver usando uma conta de armazenamento premium para os dados replicados, configure uma conta de armazenamento padrão, os logs de replicação toostore capturam alterações contínuas tooon de dados locais.</span><span class="sxs-lookup"><span data-stu-id="ce872-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="ce872-187">Se você não tiver criado uma rede do Azure, e você desejar toocreate um usando o Gerenciador de recursos, clique em **+ rede** toodo que embutido.</span><span class="sxs-lookup"><span data-stu-id="ce872-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="ce872-188">Em Olá **criar rede virtual** folha especificar um nome de rede, intervalo de endereços, detalhes de sub-rede, assinatura e local.</span><span class="sxs-lookup"><span data-stu-id="ce872-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="ce872-189">rede Olá deve estar no hello Cofre de serviços de recuperação do mesmo local que hello.</span><span class="sxs-lookup"><span data-stu-id="ce872-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![Rede](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="ce872-191">Se você quiser toocreate uma rede usando o modelo clássico hello, use Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce872-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="ce872-192">[Saiba mais](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ce872-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="ce872-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce872-193">Next steps</span></span>

<span data-ttu-id="ce872-194">Vá muito[etapa 9: Configurar mapeamento de rede](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="ce872-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
