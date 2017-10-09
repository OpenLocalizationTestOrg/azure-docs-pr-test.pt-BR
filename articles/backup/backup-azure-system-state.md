---
title: aaaBack backup tooAzure de estado do sistema Windows | Microsoft Docs
description: "Saiba tooback backup de estado do sistema de saudação do Windows Server e/ou tooAzure de computadores Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: como toobackup; como tooback; pastas e arquivos de backup
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="d1677-104">Fazer backup de estado do sistema do Windows na implementação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="d1677-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="d1677-105">Este artigo explica como tooback o sistema Windows Server estado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d1677-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="d1677-106">É um tutorial toowalk pretendido você sobre conceitos básicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="d1677-107">Se você quiser tooknow mais sobre o Backup do Azure, leia este [visão geral](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="d1677-108">Se não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/) , que permitirá o acesso a qualquer serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d1677-109">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="d1677-109">Create a recovery services vault</span></span>
<span data-ttu-id="d1677-110">tooback backup de seus arquivos e pastas, é necessário toocreate um cofre de serviços de recuperação na região Olá onde você deseja toostore Olá dados.</span><span class="sxs-lookup"><span data-stu-id="d1677-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="d1677-111">Você também precisa toodetermine como você deseja que o armazenamento replicado.</span><span class="sxs-lookup"><span data-stu-id="d1677-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="d1677-112">toocreate um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="d1677-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="d1677-113">Se você ainda não fez isso, entre no toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="d1677-114">No menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação** e clique em **os cofres de serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="d1677-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="d1677-116">Se houver cofres de serviços de recuperação na assinatura hello, cofres hello serão listados.</span><span class="sxs-lookup"><span data-stu-id="d1677-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="d1677-117">Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="d1677-119">Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.</span><span class="sxs-lookup"><span data-stu-id="d1677-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="d1677-121">Para **nome**, insira um cofre de saudação tooidentify nome amigável.</span><span class="sxs-lookup"><span data-stu-id="d1677-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="d1677-122">nome da saudação precisa toobe exclusivo Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="d1677-123">Digite um nome que contenha de 2 a 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1677-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="d1677-124">Ele deve começar com uma letra e pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="d1677-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="d1677-125">Em Olá **assinatura** seção, use Olá toochoose de menu suspenso Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="d1677-126">Se você usar apenas uma assinatura, essa assinatura será exibida e você pode ignorar toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="d1677-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="d1677-127">Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura.</span><span class="sxs-lookup"><span data-stu-id="d1677-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="d1677-128">Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="d1677-129">Em Olá **grupo de recursos** seção:</span><span class="sxs-lookup"><span data-stu-id="d1677-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="d1677-130">Selecione **criar novo** se você quiser toocreate um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1677-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="d1677-131">Ou</span><span class="sxs-lookup"><span data-stu-id="d1677-131">Or</span></span>
    * <span data-ttu-id="d1677-132">Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1677-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="d1677-133">Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="d1677-134">Clique em **local** tooselect Olá região para o cofre hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="d1677-135">Essa opção determina a região geográfica hello, onde os dados de backup são enviados.</span><span class="sxs-lookup"><span data-stu-id="d1677-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="d1677-136">Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="d1677-137">Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d1677-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="d1677-138">Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="d1677-139">Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d1677-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="d1677-140">Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="d1677-142">Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="d1677-143">Definir a redundância de armazenamento para o cofre Olá</span><span class="sxs-lookup"><span data-stu-id="d1677-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="d1677-144">Quando você criar um cofre de serviços de recuperação, certifique-se de redundância de armazenamento é a maneira de saudação configurado desejado.</span><span class="sxs-lookup"><span data-stu-id="d1677-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="d1677-145">De saudação **os cofres de serviços de recuperação** folha, clique em novo cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecione Novo cofre de saudação da lista de saudação do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="d1677-147">Hello quando você seleciona o cofre hello, **Cofre de serviços de recuperação** restringe de folha e folha de configurações de saudação (*que tem o nome de saudação do cofre Olá na parte superior da saudação*) e Olá cofre detalhes blade aberto.</span><span class="sxs-lookup"><span data-stu-id="d1677-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Exibir configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="d1677-149">Na folha de configurações do cofre novo hello, Olá slide vertical tooscroll para baixo toohello seção gerenciar e clique em **Backup infraestrutura**.</span><span class="sxs-lookup"><span data-stu-id="d1677-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="d1677-150">Abre a folha de infraestrutura de Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="d1677-151">Na folha de infraestrutura de Backup hello, clique em **configuração de Backup** tooopen Olá **configuração de Backup** folha.</span><span class="sxs-lookup"><span data-stu-id="d1677-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Definir a configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="d1677-153">Escolha a opção de replicação de armazenamento apropriado Olá para seu Cofre de.</span><span class="sxs-lookup"><span data-stu-id="d1677-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="d1677-155">Por padrão, seu cofre tem armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="d1677-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="d1677-156">Se você usar o Azure como um ponto de extremidade de armazenamento de backup primário, continuar toouse **georredundante**.</span><span class="sxs-lookup"><span data-stu-id="d1677-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="d1677-157">Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="d1677-158">Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="d1677-159">Agora que você criou um cofre, configure-o para fazer backup do Estado do Sistema do Windows.</span><span class="sxs-lookup"><span data-stu-id="d1677-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="d1677-160">Configurar o cofre Olá</span><span class="sxs-lookup"><span data-stu-id="d1677-160">Configure hello vault</span></span>
1. <span data-ttu-id="d1677-161">Olá folha de Cofre de serviços de recuperação (para Olá cofre você acabou de criar), na seção de introdução de saudação em, clique em **Backup**, em seguida, na Olá **Introdução ao Backup** folha, selecione  **Meta de backup**.</span><span class="sxs-lookup"><span data-stu-id="d1677-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="d1677-163">Olá **Backup meta** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="d1677-163">hello **Backup Goal** blade opens.</span></span>

    ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="d1677-165">De saudação **onde sua carga de trabalho está executando?** menu suspenso, selecione **local**.</span><span class="sxs-lookup"><span data-stu-id="d1677-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="d1677-166">Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.</span><span class="sxs-lookup"><span data-stu-id="d1677-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="d1677-167">De saudação **o que fazer você deseja toobackup?** menu, selecione **o estado do sistema**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d1677-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configuração de arquivos e pastas](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="d1677-169">Depois de clicar em Okey, uma marca de seleção aparece próxima muito**meta Backup**e hello **preparar infraestrutura** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="d1677-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Meta de backup configurada, prepare a infraestrutura em seguida](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="d1677-171">Em Olá **preparar infraestrutura** folha, clique em **baixar agente para Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="d1677-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="d1677-173">Se você estiver usando o Windows Server essenciais, em seguida, escolha o agente de Olá de toodownload para essenciais do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d1677-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="d1677-174">Um menu pop-up solicita toorun ou salvar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="d1677-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Diálogo MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="d1677-176">No menu pop-up de download de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="d1677-177">Por padrão, Olá **MARSagentinstaller.exe** arquivo é salvo tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="d1677-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="d1677-178">Quando o instalador de saudação for concluída, você verá um pop-up perguntando se deseja toorun Olá installer, ou abra a pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="d1677-180">Você não precisa de agente de saudação tooinstall ainda.</span><span class="sxs-lookup"><span data-stu-id="d1677-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="d1677-181">Você pode instalar o agente de saudação depois de baixar credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="d1677-182">Em Olá **preparar infraestrutura** folha, clique em **baixar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![baixar as credenciais do cofre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="d1677-184">as credenciais do cofre Olá baixam tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="d1677-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="d1677-185">Depois que as credenciais do cofre Olá conclusão do download, você verá um pop-up perguntando se você deseja tooopen ou salva credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="d1677-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-186">Click **Save**.</span></span> <span data-ttu-id="d1677-187">Se você clicar acidentalmente **abrir**, deixe a caixa de diálogo Olá tentativas de credenciais do cofre Olá tooopen, falha.</span><span class="sxs-lookup"><span data-stu-id="d1677-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="d1677-188">Não é possível abrir as credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="d1677-189">Continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="d1677-189">Proceed toohello next step.</span></span> <span data-ttu-id="d1677-190">as credenciais do cofre Olá estão na pasta de Downloads de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![o download das credenciais do cofre foi concluído](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="d1677-192">Instalar e registrar o agente Olá</span><span class="sxs-lookup"><span data-stu-id="d1677-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="d1677-193">Habilitar o backup por meio de saudação portal do Azure ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="d1677-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="d1677-194">Use Olá Microsoft Azure Recovery Services Agent tooback backup de estado do sistema do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d1677-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="d1677-195">Localize e clique duas vezes em Olá **MARSagentinstaller.exe** de pasta de Downloads de hello (ou outro local salvo).</span><span class="sxs-lookup"><span data-stu-id="d1677-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="d1677-196">instalador de saudação fornece uma série de mensagens enquanto ele extrai, instala e registra o agente de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![execute as credenciais do instalador do agente dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="d1677-198">Olá concluir o Assistente de instalação do Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="d1677-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="d1677-199">Assistente de saudação toocomplete, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d1677-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="d1677-200">Escolha um local para a pasta de instalação e o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="d1677-201">Forneça seu proxy informações do servidor se você usar um toohello de tooconnect do servidor de proxy à internet.</span><span class="sxs-lookup"><span data-stu-id="d1677-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="d1677-202">Forneça os detalhes do seu nome de usuário e de sua senha se usar um proxy autenticado.</span><span class="sxs-lookup"><span data-stu-id="d1677-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="d1677-203">Forneça as credenciais do cofre Olá baixado</span><span class="sxs-lookup"><span data-stu-id="d1677-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="d1677-204">Salve senha de criptografia de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="d1677-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d1677-205">Se você perde ou esquecer a senha hello, Microsoft não pode ajudar a recuperar dados de backup hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="d1677-206">Salve o arquivo de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="d1677-206">Save hello file in a secure location.</span></span> <span data-ttu-id="d1677-207">É necessário toorestore um backup.</span><span class="sxs-lookup"><span data-stu-id="d1677-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="d1677-208">Olá agent já está instalado e o computador é registrado toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="d1677-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="d1677-209">Você está pronto tooconfigure e agenda o backup.</span><span class="sxs-lookup"><span data-stu-id="d1677-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="d1677-210">Fazer backup do Estado do Sistema do Windows Server (visualização prévia)</span><span class="sxs-lookup"><span data-stu-id="d1677-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="d1677-211">backup de saudação inicial inclui três tarefas:</span><span class="sxs-lookup"><span data-stu-id="d1677-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="d1677-212">Habilitar o Backup de estado do sistema usando hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="d1677-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="d1677-213">Agendamento de backup Olá</span><span class="sxs-lookup"><span data-stu-id="d1677-213">Schedule hello backup</span></span>
* <span data-ttu-id="d1677-214">Fazer backup de arquivos e pastas para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="d1677-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="d1677-215">toocomplete saudação inicial fazer backup, agente de serviços de recuperação do Microsoft Azure use hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="d1677-216">backup de estado do sistema tooenable usando hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="d1677-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="d1677-217">Em uma sessão do PowerShell, execute Olá mecanismo de Backup do Azure do comando toostop Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1677-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="d1677-218">Abra a saudação do registro do Windows.</span><span class="sxs-lookup"><span data-stu-id="d1677-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="d1677-219">Adicione Olá seguinte chave de registro com hello especificado valor DWord.</span><span class="sxs-lookup"><span data-stu-id="d1677-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="d1677-220">Caminho do registro</span><span class="sxs-lookup"><span data-stu-id="d1677-220">Registry path</span></span> | <span data-ttu-id="d1677-221">Chave do registro</span><span class="sxs-lookup"><span data-stu-id="d1677-221">Registry key</span></span> | <span data-ttu-id="d1677-222">Valor DWord</span><span class="sxs-lookup"><span data-stu-id="d1677-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="d1677-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="d1677-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="d1677-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="d1677-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="d1677-225">2</span><span class="sxs-lookup"><span data-stu-id="d1677-225">2</span></span> |

4. <span data-ttu-id="d1677-226">Reinicie o mecanismo de Backup de saudação executando Olá comando em um prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1677-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="d1677-227">trabalho de backup tooschedule Olá</span><span class="sxs-lookup"><span data-stu-id="d1677-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="d1677-228">Abra o agente de serviços de recuperação do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="d1677-229">Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d1677-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Inicie o agente de serviços de recuperação do Azure Olá](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="d1677-231">No agente de serviços de recuperação de saudação, clique em **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="d1677-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Agendar um backup do Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="d1677-233">Em Olá Introdução página do Assistente de agendamento de Backup de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d1677-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="d1677-234">Na página de tooBackup do hello selecionar itens, clique em **adicionar itens**.</span><span class="sxs-lookup"><span data-stu-id="d1677-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="d1677-235">Selecione **Estado do sistema** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1677-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="d1677-236">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-236">Click **Next**.</span></span>

7. <span data-ttu-id="d1677-237">Olá agenda de Backup de estado do sistema e de retenção é definida automaticamente tooback backup de todos os domingos às 9:00 PM, horário local e período de retenção de saudação é definido too60 dias.</span><span class="sxs-lookup"><span data-stu-id="d1677-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d1677-238">A política de backup e retenção do estado do sistema é configurada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d1677-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="d1677-239">Se você fizer backup de arquivos e pastas além toohello estado de sistema do Windows Server, especifique a única política de Backup e retenção de saudação para backups de arquivo do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="d1677-240">Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="d1677-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="d1677-241">Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="d1677-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="d1677-242">tooback backup de estado do sistema do Windows Server para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="d1677-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="d1677-243">Certifique-se de que não existem atualizações pendentes para o Windows Server que exigem uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="d1677-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="d1677-244">No agente de serviços de recuperação de saudação, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Fazer backup do Windows Server agora](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="d1677-246">Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="d1677-247">Em seguida, clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="d1677-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="d1677-248">Clique em **fechar** tooclose Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="d1677-249">Se você fechar o Assistente de saudação antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="d1677-250">Se você fizer backup de arquivos e pastas no servidor, além de toohello estado de sistema do Windows Server, o assistente Fazer Backup agora Olá fará backup somente arquivos.</span><span class="sxs-lookup"><span data-stu-id="d1677-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="d1677-251">tooperform um estado de sistema ad hoc backup, use Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1677-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="d1677-252">Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR completo](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="d1677-254">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="d1677-254">Frequently asked questions</span></span>

<span data-ttu-id="d1677-255">Olá perguntas e respostas a seguir fornecem informações complementares.</span><span class="sxs-lookup"><span data-stu-id="d1677-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="d1677-256">O que é Olá preparo Volume?</span><span class="sxs-lookup"><span data-stu-id="d1677-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="d1677-257">Olá preparo Volume representa local intermediário de saudação onde Olá disponível de modo nativo, Backup do Windows Server prepara Olá Backup de estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="d1677-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="d1677-258">Agente de Backup do Azure, em seguida, compacta e criptografa esse backup intermediário e envia a que ele por meio de toohello de protocolo HTTPS seguro configurado Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d1677-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="d1677-259">**É altamente recomendável que estabelecer Olá preparo Volume em um volume não-Windows-OS. Se você observar problemas com Backups de estado do sistema, verificar o local de saudação do seu Volume de preparo é a primeira etapa de solução de problemas de saudação.**</span><span class="sxs-lookup"><span data-stu-id="d1677-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="d1677-260">Como alterar Olá preparo caminho do Volume especificado no agente de Backup do Azure Olá?</span><span class="sxs-lookup"><span data-stu-id="d1677-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="d1677-261">Olá Volume de preparo está localizado na pasta de cache Olá por padrão.</span><span class="sxs-lookup"><span data-stu-id="d1677-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="d1677-262">toochange nesse local, use Olá comando (em um prompt de comando com privilégios elevados) a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1677-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="d1677-263">Em seguida, atualize Olá entradas do registro com hello caminho toohello nova preparação Volume pasta a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1677-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="d1677-264">Caminho do registro</span><span class="sxs-lookup"><span data-stu-id="d1677-264">Registry path</span></span>|<span data-ttu-id="d1677-265">Chave do registro</span><span class="sxs-lookup"><span data-stu-id="d1677-265">Registry key</span></span>|<span data-ttu-id="d1677-266">Valor</span><span class="sxs-lookup"><span data-stu-id="d1677-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="d1677-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="d1677-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="d1677-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="d1677-268">SSBStagingPath</span></span> | <span data-ttu-id="d1677-269">novo local do volume de preparo</span><span class="sxs-lookup"><span data-stu-id="d1677-269">new staging volume location</span></span> |

<span data-ttu-id="d1677-270">Olá preparo caminho diferencia maiusculas de minúsculas e deve ser Olá exata mesmo maiusculas e minúsculas como o que existe no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="d1677-271">Depois que você alterar o caminho do volume de preparo hello, reinicie o mecanismo de Backup de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1677-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="d1677-272">toopick caminho Olá alterado, agente de serviços de recuperação do Microsoft Azure Olá abrir e gatilho um backup ad hoc do estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="d1677-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="d1677-273">Por que é o estado do sistema Olá retenção padrão definido too60 dias?</span><span class="sxs-lookup"><span data-stu-id="d1677-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="d1677-274">vida útil de saudação de um backup de estado do sistema é Olá igual a configuração hello "tempo de desativação" para a função do Windows Server Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="d1677-275">valor padrão de saudação para entrada de tempo de vida de desativação Olá é 60 dias.</span><span class="sxs-lookup"><span data-stu-id="d1677-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="d1677-276">Esse valor pode ser definido no objeto de configuração do serviço de diretório (NTDS) hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="d1677-277">Como alterar o padrão de saudação Backup e política de retenção para o estado do sistema?</span><span class="sxs-lookup"><span data-stu-id="d1677-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="d1677-278">padrão de saudação toochange Backup e política de retenção para o estado do sistema:</span><span class="sxs-lookup"><span data-stu-id="d1677-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="d1677-279">Pare o mecanismo de Backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-279">Stop hello Backup engine.</span></span> <span data-ttu-id="d1677-280">Execute Olá comando a seguir em um prompt de comando com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="d1677-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="d1677-281">Adicionar ou atualizar Olá entradas de chave de registro em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1677-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="d1677-282">Nome do Registro</span><span class="sxs-lookup"><span data-stu-id="d1677-282">Registry Name</span></span>|<span data-ttu-id="d1677-283">Descrição</span><span class="sxs-lookup"><span data-stu-id="d1677-283">Description</span></span>|<span data-ttu-id="d1677-284">Valor</span><span class="sxs-lookup"><span data-stu-id="d1677-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="d1677-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="d1677-285">SSBScheduleTime</span></span>|<span data-ttu-id="d1677-286">Tempo de saudação tooconfigure usado do backup hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="d1677-287">O horário padrão está configurado para as 21 horas da hora local.</span><span class="sxs-lookup"><span data-stu-id="d1677-287">Default is 9PM local time.</span></span>|<span data-ttu-id="d1677-288">DWord: Formato HHMM (decimal). 2130, por exemplo, significa 21h30 da hora local.</span><span class="sxs-lookup"><span data-stu-id="d1677-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="d1677-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="d1677-289">SSBScheduleDays</span></span>|<span data-ttu-id="d1677-290">Dias de saudação tooconfigure usado quando o Backup de estado do sistema deve ser executada no hello especificado de tempo.</span><span class="sxs-lookup"><span data-stu-id="d1677-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="d1677-291">Dígitos individuais especificam dias da semana hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="d1677-292">0 representa domingo, 1 é a segunda-feira, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d1677-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="d1677-293">O dia padrão para o backup é domingo.</span><span class="sxs-lookup"><span data-stu-id="d1677-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="d1677-294">DWord: dias do backup toorun da semana hello (decimal), por exemplo 1230 agenda de backups na segunda-feira, terça-feira, quarta-feira e domingo.</span><span class="sxs-lookup"><span data-stu-id="d1677-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="d1677-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="d1677-295">SSBRetentionDays</span></span>|<span data-ttu-id="d1677-296">Backup de tooretain do tooconfigure usado Olá dias.</span><span class="sxs-lookup"><span data-stu-id="d1677-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="d1677-297">O valor padrão é de 60.</span><span class="sxs-lookup"><span data-stu-id="d1677-297">Default value is 60.</span></span> <span data-ttu-id="d1677-298">O valor máximo permitido é de 180.</span><span class="sxs-lookup"><span data-stu-id="d1677-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="d1677-299">DWord: Backup de tooretain dias (decimal).</span><span class="sxs-lookup"><span data-stu-id="d1677-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="d1677-300">Use Olá mecanismo de backup do comando toorestart Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1677-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="d1677-301">Abra o agente de serviços de recuperação do Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="d1677-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="d1677-302">Clique em **agendamento de Backup** e, em seguida, clique em **próximo** até ver as alterações de saudação refletidas.</span><span class="sxs-lookup"><span data-stu-id="d1677-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="d1677-303">Clique em **concluir** tooapply alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1677-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="d1677-304">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="d1677-304">Questions?</span></span>
<span data-ttu-id="d1677-305">Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="d1677-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1677-306">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1677-306">Next steps</span></span>
* <span data-ttu-id="d1677-307">Obtenha mais detalhes sobre o [backup de computadores que usam o Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="d1677-308">Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="d1677-309">Se você precisar toorestore um backup, use este artigo muito[restaurar arquivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="d1677-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
