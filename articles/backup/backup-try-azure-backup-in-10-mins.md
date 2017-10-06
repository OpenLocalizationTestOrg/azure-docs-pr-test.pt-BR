---
title: aaaBack backup Windows tooAzure arquivos e pastas (Gerenciador de recursos) | Microsoft Docs
description: "Saiba tooback backup tooAzure de arquivos e pastas do Windows em uma implantação do Gerenciador de recursos."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: como toobackup; como tooback; pastas e arquivos de backup
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="190b5-104">Introdução: fazer backup de arquivos e pastas na implantação do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="190b5-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="190b5-105">Este artigo explica como tooback backup do Windows Server (ou o computador com Windows) tooAzure arquivos e pastas usando uma implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="190b5-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="190b5-106">É um tutorial toowalk pretendido você sobre conceitos básicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="190b5-107">Se você quiser tooget iniciado usando o Backup do Azure, você está no lugar certo hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="190b5-108">Se você quiser tooknow mais sobre o Backup do Azure, leia este [visão geral](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="190b5-109">Se não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/) , que permitirá o acesso a qualquer serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="190b5-110">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="190b5-110">Create a recovery services vault</span></span>
<span data-ttu-id="190b5-111">tooback backup de seus arquivos e pastas, é necessário toocreate um cofre de serviços de recuperação na região Olá onde você deseja toostore Olá dados.</span><span class="sxs-lookup"><span data-stu-id="190b5-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="190b5-112">Você também precisa toodetermine como você deseja que o armazenamento replicado.</span><span class="sxs-lookup"><span data-stu-id="190b5-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="190b5-113">toocreate um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="190b5-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="190b5-114">Se você ainda não fez isso, entre no toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="190b5-115">No menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação** e clique em **os cofres de serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="190b5-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="190b5-117">Se houver cofres de serviços de recuperação na assinatura hello, cofres hello serão listados.</span><span class="sxs-lookup"><span data-stu-id="190b5-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="190b5-118">Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="190b5-120">Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.</span><span class="sxs-lookup"><span data-stu-id="190b5-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="190b5-122">Para **nome**, insira um cofre de saudação tooidentify nome amigável.</span><span class="sxs-lookup"><span data-stu-id="190b5-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="190b5-123">nome da saudação precisa toobe exclusivo Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="190b5-124">Digite um nome que contenha entre 2 e 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="190b5-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="190b5-125">Ele deve começar com uma letra e pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="190b5-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="190b5-126">Em Olá **assinatura** seção, use Olá toochoose de menu suspenso Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="190b5-127">Se você usar apenas uma assinatura, essa assinatura será exibida e você pode ignorar toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="190b5-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="190b5-128">Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura.</span><span class="sxs-lookup"><span data-stu-id="190b5-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="190b5-129">Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="190b5-130">Em Olá **grupo de recursos** seção:</span><span class="sxs-lookup"><span data-stu-id="190b5-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="190b5-131">Selecione **criar novo** se você quiser toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="190b5-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="190b5-132">Ou</span><span class="sxs-lookup"><span data-stu-id="190b5-132">Or</span></span>
    * <span data-ttu-id="190b5-133">Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="190b5-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="190b5-134">Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="190b5-135">Clique em **local** tooselect Olá região para o cofre hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="190b5-136">Essa opção determina a região geográfica hello, onde os dados de backup são enviados.</span><span class="sxs-lookup"><span data-stu-id="190b5-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="190b5-137">Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="190b5-138">Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="190b5-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="190b5-139">Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="190b5-140">Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="190b5-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="190b5-141">Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="190b5-143">Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="190b5-144">Definir a redundância de armazenamento para o cofre Olá</span><span class="sxs-lookup"><span data-stu-id="190b5-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="190b5-145">Quando você criar um cofre de serviços de recuperação, certifique-se de redundância de armazenamento é a maneira de saudação configurado desejado.</span><span class="sxs-lookup"><span data-stu-id="190b5-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="190b5-146">De saudação **os cofres de serviços de recuperação** folha, clique em novo cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecione Novo cofre de saudação da lista de saudação do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="190b5-148">Hello quando você seleciona o cofre hello, **Cofre de serviços de recuperação** restringe de folha e folha de configurações de saudação (*que tem o nome de saudação do cofre Olá na parte superior da saudação*) e Olá cofre detalhes blade aberto.</span><span class="sxs-lookup"><span data-stu-id="190b5-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Exibir configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="190b5-150">Na folha de configurações do cofre novo hello, Olá slide vertical tooscroll para baixo toohello seção gerenciar e clique em **Backup infraestrutura**.</span><span class="sxs-lookup"><span data-stu-id="190b5-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="190b5-151">Abre a folha de infraestrutura de Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="190b5-152">Na folha de infraestrutura de Backup hello, clique em **configuração de Backup** tooopen Olá **configuração de Backup** folha.</span><span class="sxs-lookup"><span data-stu-id="190b5-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Definir a configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="190b5-154">Escolha a opção de replicação de armazenamento apropriado Olá para seu Cofre de.</span><span class="sxs-lookup"><span data-stu-id="190b5-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="190b5-156">Por padrão, seu cofre tem armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="190b5-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="190b5-157">Se você usar o Azure como um ponto de extremidade de armazenamento de backup primário, continuar toouse **georredundante**.</span><span class="sxs-lookup"><span data-stu-id="190b5-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="190b5-158">Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="190b5-159">Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="190b5-160">Agora que você criou um cofre, configure-o para fazer backup de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="190b5-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="190b5-161">Configurar o cofre Olá</span><span class="sxs-lookup"><span data-stu-id="190b5-161">Configure hello vault</span></span>
1. <span data-ttu-id="190b5-162">Olá folha de Cofre de serviços de recuperação (para Olá cofre você acabou de criar), na seção de introdução de saudação em, clique em **Backup**, em seguida, na Olá **Introdução ao Backup** folha, selecione  **Meta de backup**.</span><span class="sxs-lookup"><span data-stu-id="190b5-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="190b5-164">Olá **Backup meta** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="190b5-164">hello **Backup Goal** blade opens.</span></span>

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="190b5-166">De saudação **onde sua carga de trabalho está executando?** menu suspenso, selecione **local**.</span><span class="sxs-lookup"><span data-stu-id="190b5-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="190b5-167">Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.</span><span class="sxs-lookup"><span data-stu-id="190b5-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="190b5-168">De saudação **o que fazer você deseja toobackup?** menu, selecione **arquivos e pastas**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="190b5-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configuração de arquivos e pastas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="190b5-170">Depois de clicar em Okey, uma marca de seleção aparece próxima muito**meta Backup**e hello **preparar infraestrutura** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="190b5-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Meta de backup configurada, prepare a infraestrutura em seguida](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="190b5-172">Em Olá **preparar infraestrutura** folha, clique em **baixar agente para Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="190b5-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="190b5-174">Se você estiver usando o Windows Server essenciais, em seguida, escolha o agente de Olá de toodownload para essenciais do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="190b5-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="190b5-175">Um menu pop-up solicita toorun ou salvar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="190b5-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Diálogo MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="190b5-177">No menu pop-up de download de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="190b5-178">Por padrão, Olá **MARSagentinstaller.exe** arquivo é salvo tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="190b5-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="190b5-179">Quando o instalador de saudação for concluída, você verá um pop-up perguntando se deseja toorun Olá installer, ou abra a pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="190b5-181">Você não precisa de agente de saudação tooinstall ainda.</span><span class="sxs-lookup"><span data-stu-id="190b5-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="190b5-182">Você pode instalar o agente de saudação depois de baixar credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="190b5-183">Em Olá **preparar infraestrutura** folha, clique em **baixar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![baixar as credenciais do cofre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="190b5-185">as credenciais do cofre Olá baixam tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="190b5-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="190b5-186">Depois que as credenciais do cofre Olá conclusão do download, você verá um pop-up perguntando se você deseja tooopen ou salva credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="190b5-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-187">Click **Save**.</span></span> <span data-ttu-id="190b5-188">Se você clicar acidentalmente **abrir**, deixe a caixa de diálogo Olá tentativas de credenciais do cofre Olá tooopen, falha.</span><span class="sxs-lookup"><span data-stu-id="190b5-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="190b5-189">Não é possível abrir as credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="190b5-190">Continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="190b5-190">Proceed toohello next step.</span></span> <span data-ttu-id="190b5-191">as credenciais do cofre Olá estão na pasta de Downloads de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![o download das credenciais do cofre foi concluído](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="190b5-193">Instalar e registrar o agente Olá</span><span class="sxs-lookup"><span data-stu-id="190b5-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="190b5-194">Habilitar o backup por meio de saudação portal do Azure ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="190b5-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="190b5-195">Use Olá Microsoft Azure Recovery Services Agent tooback backup de seus arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="190b5-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="190b5-196">Localize e clique duas vezes em Olá **MARSagentinstaller.exe** de pasta de Downloads de hello (ou outro local salvo).</span><span class="sxs-lookup"><span data-stu-id="190b5-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="190b5-197">instalador de saudação fornece uma série de mensagens enquanto ele extrai, instala e registra o agente de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![execute as credenciais do instalador do agente dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="190b5-199">Olá concluir o Assistente de instalação do Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="190b5-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="190b5-200">Assistente de saudação toocomplete, você precisa:</span><span class="sxs-lookup"><span data-stu-id="190b5-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="190b5-201">Escolha um local para a pasta de instalação e o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="190b5-202">Forneça seu proxy informações do servidor se você usar um toohello de tooconnect do servidor de proxy à internet.</span><span class="sxs-lookup"><span data-stu-id="190b5-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="190b5-203">Forneça os detalhes do seu nome de usuário e de sua senha se usar um proxy autenticado.</span><span class="sxs-lookup"><span data-stu-id="190b5-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="190b5-204">Forneça as credenciais do cofre Olá baixado</span><span class="sxs-lookup"><span data-stu-id="190b5-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="190b5-205">Salve senha de criptografia de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="190b5-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="190b5-206">Se você perde ou esquecer a senha hello, Microsoft não pode ajudar a recuperar dados de backup hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="190b5-207">Salve o arquivo de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="190b5-207">Save hello file in a secure location.</span></span> <span data-ttu-id="190b5-208">É necessário toorestore um backup.</span><span class="sxs-lookup"><span data-stu-id="190b5-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="190b5-209">Olá agent já está instalado e o computador é registrado toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="190b5-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="190b5-210">Você está pronto tooconfigure e agenda o backup.</span><span class="sxs-lookup"><span data-stu-id="190b5-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="190b5-211">Requisitos de conectividade e rede</span><span class="sxs-lookup"><span data-stu-id="190b5-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="190b5-212">Se sua máquina/proxy limitou o acesso à internet, verifique se as configurações de firewall Olá mcahine/proxy Olá tooallow configurado URLs a seguir:</span><span class="sxs-lookup"><span data-stu-id="190b5-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="190b5-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="190b5-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="190b5-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="190b5-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="190b5-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="190b5-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="190b5-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="190b5-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="190b5-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="190b5-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="190b5-218">Fazer o backup de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="190b5-218">Back up your files and folders</span></span>
<span data-ttu-id="190b5-219">backup de saudação inicial inclui duas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="190b5-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="190b5-220">Agendamento de backup Olá</span><span class="sxs-lookup"><span data-stu-id="190b5-220">Schedule hello backup</span></span>
* <span data-ttu-id="190b5-221">Fazer backup de arquivos e pastas para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="190b5-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="190b5-222">toocomplete saudação inicial fazer backup, agente de serviços de recuperação do Microsoft Azure use hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="190b5-223">trabalho de backup tooschedule Olá</span><span class="sxs-lookup"><span data-stu-id="190b5-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="190b5-224">Abra o agente de serviços de recuperação do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="190b5-225">Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="190b5-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Inicie o agente de serviços de recuperação do Azure Olá](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="190b5-227">No agente de serviços de recuperação de saudação, clique em **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="190b5-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Agendar um backup do Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="190b5-229">Em Olá Introdução página do Assistente de agendamento de Backup de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="190b5-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="190b5-230">Na página de tooBackup do hello selecionar itens, clique em **adicionar itens**.</span><span class="sxs-lookup"><span data-stu-id="190b5-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="190b5-231">Selecione Olá arquivos e pastas que você deseja tooback backup e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="190b5-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="190b5-232">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-232">Click **Next**.</span></span>
7. <span data-ttu-id="190b5-233">Em Olá **especificar agendamento de Backup** especifique Olá **agendamento de backup** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="190b5-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="190b5-234">Você pode agendar backups diários (com uma taxa máxima de três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="190b5-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Itens para o backup do Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="190b5-236">Para obter mais informações sobre como toospecify Olá agendamento de backup, consulte o artigo Olá [tooreplace uso do Azure Backup sua infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="190b5-237">Em Olá **Selecionar política de retenção** página, selecione Olá **política de retenção** para cópia de backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="190b5-238">política de retenção de saudação especifica quanto tempo os dados de backup Olá são armazenados.</span><span class="sxs-lookup"><span data-stu-id="190b5-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="190b5-239">Em vez de especificar uma "política simples" para todos os pontos de backup, você pode especificar diferentes políticas de retenção com base em quando Olá backup ocorrer.</span><span class="sxs-lookup"><span data-stu-id="190b5-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="190b5-240">Você pode modificar toomeet de políticas de retenção diária, semanal, mensal e anual Olá suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="190b5-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="190b5-241">Na página de escolher tipo de Backup inicial de saudação, escolha o tipo de backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="190b5-242">Deixe a opção Olá **automaticamente pela rede Olá** selecionado e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="190b5-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="190b5-243">Você pode fazer backup automaticamente pela rede hello, ou você pode fazer backup offline.</span><span class="sxs-lookup"><span data-stu-id="190b5-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="190b5-244">restante Olá deste artigo descreve o processo de saudação para fazer backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="190b5-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="190b5-245">Se você preferir toodo um backup offline, leia o artigo de saudação [Offline fluxo de trabalho de backup no Backup do Azure](backup-azure-backup-import-export.md) para obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="190b5-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="190b5-246">Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="190b5-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="190b5-247">Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="190b5-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="190b5-248">tooback backup de arquivos e pastas para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="190b5-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="190b5-249">No agente de serviços de recuperação de saudação, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Fazer backup do Windows Server agora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="190b5-251">Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="190b5-252">Em seguida, clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="190b5-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="190b5-253">Clique em **fechar** tooclose Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="190b5-254">Se você fechar o Assistente de saudação antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="190b5-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="190b5-255">Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.</span><span class="sxs-lookup"><span data-stu-id="190b5-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR completo](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="190b5-257">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="190b5-257">Questions?</span></span>
<span data-ttu-id="190b5-258">Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="190b5-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="190b5-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="190b5-259">Next steps</span></span>
* <span data-ttu-id="190b5-260">Obtenha mais detalhes sobre o [backup de computadores que usam o Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="190b5-261">Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="190b5-262">Se você precisar toorestore um backup, use este artigo muito[restaurar arquivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="190b5-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
