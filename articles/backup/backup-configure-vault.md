---
title: aaaUse tooback de agente de Backup do Azure backup de arquivos e pastas | Microsoft Docs
description: "Use Olá tooback de agente de Backup do Microsoft Azure backup tooAzure de arquivos e pastas do Windows. Crie um cofre de serviços de recuperação, instalar o agente de Backup hello, definir a política de backup hello e executar o backup inicial Olá em pastas e arquivos de saudação."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: cofre de backup; fazer backup de um Windows server; backup do windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="9b582-105">Fazer backup de um tooAzure de cliente ou servidor do Windows usando o modelo de implantação do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="9b582-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b582-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b582-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="9b582-107">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="9b582-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="9b582-108">Este artigo explica como tooAzure tooback backup do Windows Server (ou o cliente do Windows) de arquivos e pastas com o Backup do Azure usando Olá modelo de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b582-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Etapas do processo de backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="9b582-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9b582-110">Before you start</span></span>
<span data-ttu-id="9b582-111">tooback backup de um servidor ou cliente tooAzure, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="9b582-112">Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9b582-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="9b582-113">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="9b582-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="9b582-114">Um cofre de serviços de recuperação é uma entidade que armazena todos os backups de saudação e pontos de recuperação criados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="9b582-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="9b582-115">Cofre de serviços de recuperação de saudação também contém Olá backup política aplicada toohello protegido arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="9b582-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="9b582-116">Quando você criar um cofre de serviços de recuperação, você também deve selecionar opção de redundância de armazenamento apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="9b582-117">toocreate um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="9b582-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="9b582-118">Se você ainda não fez isso, entre no toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="9b582-119">No menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação** e clique em **os cofres de serviços de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="9b582-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="9b582-121">Se houver cofres de serviços de recuperação na assinatura hello, cofres hello serão listados.</span><span class="sxs-lookup"><span data-stu-id="9b582-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="9b582-122">Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="9b582-124">Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.</span><span class="sxs-lookup"><span data-stu-id="9b582-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="9b582-126">Para **nome**, insira um cofre de saudação tooidentify nome amigável.</span><span class="sxs-lookup"><span data-stu-id="9b582-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="9b582-127">nome da saudação precisa toobe exclusivo Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="9b582-128">Digite um nome que contenha de 2 a 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b582-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="9b582-129">Ele deve começar com uma letra e pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="9b582-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="9b582-130">Em Olá **assinatura** seção, use Olá toochoose de menu suspenso Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="9b582-131">Se você usar apenas uma assinatura, essa assinatura será exibida e você pode ignorar toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="9b582-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="9b582-132">Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura.</span><span class="sxs-lookup"><span data-stu-id="9b582-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="9b582-133">Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="9b582-134">Em Olá **grupo de recursos** seção:</span><span class="sxs-lookup"><span data-stu-id="9b582-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="9b582-135">Selecione **criar novo** se você quiser toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b582-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="9b582-136">Ou</span><span class="sxs-lookup"><span data-stu-id="9b582-136">Or</span></span>
    * <span data-ttu-id="9b582-137">Selecione **usar existente** e clique em Olá Olá menu suspenso toosee disponíveis lista de grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b582-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="9b582-138">Para obter informações completas sobre grupos de recursos, consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="9b582-139">Clique em **local** tooselect Olá região para o cofre hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="9b582-140">Essa opção determina a região geográfica hello, onde os dados de backup são enviados.</span><span class="sxs-lookup"><span data-stu-id="9b582-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="9b582-141">Na parte inferior de saudação da folha de Cofre de serviços de recuperação de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="9b582-142">Pode levar vários minutos para Olá que toobe criado de Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9b582-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="9b582-143">Monitorar as notificações de status Olá na área de direito superior de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="9b582-144">Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9b582-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="9b582-145">Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="9b582-147">Quando você vir seu cofre na lista de saudação de cofres de serviços de recuperação, você está pronto tooset redundância de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="9b582-148">Definir redundância de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9b582-148">Set storage redundancy</span></span>
<span data-ttu-id="9b582-149">Quando você cria um cofre dos Serviços de Recuperação, determina como o armazenamento é replicado.</span><span class="sxs-lookup"><span data-stu-id="9b582-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="9b582-150">De saudação **os cofres de serviços de recuperação** folha, clique em novo cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecione Novo cofre de saudação da lista de saudação do Cofre de serviços de recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="9b582-152">Hello quando você seleciona o cofre hello, **Cofre de serviços de recuperação** restringe de folha e folha de configurações de saudação (*que tem o nome de saudação do cofre Olá na parte superior da saudação*) e Olá cofre detalhes blade aberto.</span><span class="sxs-lookup"><span data-stu-id="9b582-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Exibir configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="9b582-154">Na folha de configurações do cofre novo hello, Olá slide vertical tooscroll para baixo toohello seção gerenciar e clique em **Backup infraestrutura**.</span><span class="sxs-lookup"><span data-stu-id="9b582-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="9b582-155">Abre a folha de infraestrutura de Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="9b582-156">Na folha de infraestrutura de Backup hello, clique em **configuração de Backup** tooopen Olá **configuração de Backup** folha.</span><span class="sxs-lookup"><span data-stu-id="9b582-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Definir a configuração de armazenamento Olá para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="9b582-158">Escolha a opção de replicação de armazenamento apropriado Olá para seu Cofre de.</span><span class="sxs-lookup"><span data-stu-id="9b582-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="9b582-160">Por padrão, seu cofre tem armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="9b582-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="9b582-161">Se você usar o Azure como um ponto de extremidade de armazenamento de backup primário, continuar toouse **georredundante**.</span><span class="sxs-lookup"><span data-stu-id="9b582-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="9b582-162">Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, em seguida, escolha **localmente redundante**, que reduz os custos de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="9b582-163">Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="9b582-164">Agora que você criou um cofre, preparar tooback sua infraestrutura backup de arquivos e pastas, baixando e instalando o agente de serviços de recuperação do Microsoft Azure hello, baixando as credenciais do cofre e, em seguida, usar essas credenciais tooregister Olá agente Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="9b582-165">Configurar o cofre Olá</span><span class="sxs-lookup"><span data-stu-id="9b582-165">Configure hello vault</span></span>

1. <span data-ttu-id="9b582-166">Olá folha de Cofre de serviços de recuperação (para Olá cofre você acabou de criar), na seção de introdução de saudação em, clique em **Backup**, em seguida, na Olá **Introdução ao Backup** folha, selecione  **Meta de backup**.</span><span class="sxs-lookup"><span data-stu-id="9b582-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="9b582-168">Olá **Backup meta** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="9b582-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="9b582-169">Se tiver sido configurado anteriormente Olá Cofre de serviços de recuperação, Olá **meta de Backup** folhas abre quando você clica em **Backup** em serviços de recuperação de saudação cofre folha.</span><span class="sxs-lookup"><span data-stu-id="9b582-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="9b582-171">De saudação **onde sua carga de trabalho está executando?** menu suspenso, selecione **local**.</span><span class="sxs-lookup"><span data-stu-id="9b582-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="9b582-172">Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="9b582-173">De saudação **o que fazer você deseja toobackup?** menu, selecione **arquivos e pastas**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9b582-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuração de arquivos e pastas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="9b582-175">Depois de clicar em Okey, uma marca de seleção aparece próxima muito**meta Backup**e hello **preparar infraestrutura** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="9b582-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Meta de backup configurada, prepare a infraestrutura em seguida](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="9b582-177">Em Olá **preparar infraestrutura** folha, clique em **baixar agente para Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="9b582-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="9b582-179">Se você estiver usando o Windows Server essenciais, em seguida, escolha o agente de Olá de toodownload para essenciais do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="9b582-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="9b582-180">Um menu pop-up solicita toorun ou salvar MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="9b582-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Diálogo MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="9b582-182">No menu pop-up de download de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="9b582-183">Por padrão, Olá **MARSagentinstaller.exe** arquivo é salvo tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="9b582-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="9b582-184">Quando o instalador de saudação for concluída, você verá um pop-up perguntando se deseja toorun Olá installer, ou abra a pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="9b582-186">Você não precisa de agente de saudação tooinstall ainda.</span><span class="sxs-lookup"><span data-stu-id="9b582-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="9b582-187">Você pode instalar o agente de saudação depois de baixar credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="9b582-188">Em Olá **preparar infraestrutura** folha, clique em **baixar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![baixar as credenciais do cofre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="9b582-190">as credenciais do cofre Olá baixam tooyour pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="9b582-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="9b582-191">Depois que as credenciais do cofre Olá conclusão do download, você verá um pop-up perguntando se você deseja tooopen ou salva credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="9b582-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-192">Click **Save**.</span></span> <span data-ttu-id="9b582-193">Se você clicar acidentalmente **abrir**, deixe a caixa de diálogo Olá tentativas de credenciais do cofre Olá tooopen, falha.</span><span class="sxs-lookup"><span data-stu-id="9b582-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="9b582-194">Não é possível abrir as credenciais do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="9b582-195">Continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="9b582-195">Proceed toohello next step.</span></span> <span data-ttu-id="9b582-196">as credenciais do cofre Olá estão na pasta de Downloads de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![o download das credenciais do cofre foi concluído](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="9b582-198">Instalar e registrar o agente Olá</span><span class="sxs-lookup"><span data-stu-id="9b582-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="9b582-199">Habilitar o backup por meio de saudação portal do Azure ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="9b582-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="9b582-200">Use Olá Microsoft Azure Recovery Services Agent tooback backup de seus arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="9b582-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="9b582-201">Localize e clique duas vezes em Olá **MARSagentinstaller.exe** de pasta de Downloads de hello (ou outro local salvo).</span><span class="sxs-lookup"><span data-stu-id="9b582-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="9b582-202">instalador de saudação fornece uma série de mensagens enquanto ele extrai, instala e registra o agente de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![execute as credenciais do instalador do agente dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="9b582-204">Olá concluir o Assistente de instalação do Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="9b582-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="9b582-205">Assistente de saudação toocomplete, você precisa:</span><span class="sxs-lookup"><span data-stu-id="9b582-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="9b582-206">Escolha um local para a pasta de instalação e o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="9b582-207">Forneça seu proxy informações do servidor se você usar um toohello de tooconnect do servidor de proxy à internet.</span><span class="sxs-lookup"><span data-stu-id="9b582-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="9b582-208">Forneça os detalhes do seu nome de usuário e de sua senha se usar um proxy autenticado.</span><span class="sxs-lookup"><span data-stu-id="9b582-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="9b582-209">Forneça as credenciais do cofre Olá baixado</span><span class="sxs-lookup"><span data-stu-id="9b582-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="9b582-210">Salve senha de criptografia de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="9b582-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9b582-211">Se você perde ou esquecer a senha hello, Microsoft não pode ajudar a recuperar dados de backup hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="9b582-212">Salve o arquivo de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="9b582-212">Save hello file in a secure location.</span></span> <span data-ttu-id="9b582-213">É necessário toorestore um backup.</span><span class="sxs-lookup"><span data-stu-id="9b582-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="9b582-214">Olá agent já está instalado e o computador é registrado toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="9b582-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="9b582-215">Você está pronto tooconfigure e agenda o backup.</span><span class="sxs-lookup"><span data-stu-id="9b582-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="9b582-216">Requisitos de conectividade e rede</span><span class="sxs-lookup"><span data-stu-id="9b582-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="9b582-217">Se sua máquina/proxy limitou o acesso à internet, verifique se as configurações do firewall no computador/proxy Olá Olá tooallow configurado seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="9b582-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="9b582-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="9b582-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="9b582-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="9b582-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="9b582-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="9b582-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="9b582-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9b582-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="9b582-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="9b582-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="9b582-223">Criar política de backup Olá</span><span class="sxs-lookup"><span data-stu-id="9b582-223">Create hello backup policy</span></span>
<span data-ttu-id="9b582-224">política de backup Olá é agenda hello quando pontos de recuperação são realizados e Olá período de tempo que os pontos de recuperação de saudação são mantidos.</span><span class="sxs-lookup"><span data-stu-id="9b582-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="9b582-225">Use Olá Microsoft Azure Backup agent toocreate Olá política de backup de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="9b582-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="9b582-226">toocreate um agendamento de backup</span><span class="sxs-lookup"><span data-stu-id="9b582-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="9b582-227">Abra o agente de Backup do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="9b582-228">Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="9b582-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Inicie o agente de Backup do Azure Olá](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="9b582-230">No agente de Backup a saudação **ações** painel, clique em **agendamento de Backup** toolaunch Olá Assistente de agendamento de Backup.</span><span class="sxs-lookup"><span data-stu-id="9b582-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Agendar um backup do Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="9b582-232">Em Olá **Introdução** página de saudação Assistente de agendamento de Backup, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9b582-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="9b582-233">Em Olá **selecionar itens tooBackup** , clique em **adicionar itens**.</span><span class="sxs-lookup"><span data-stu-id="9b582-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="9b582-234">Abre a caixa de diálogo Olá selecionar itens.</span><span class="sxs-lookup"><span data-stu-id="9b582-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="9b582-235">Selecione arquivos hello e as pastas que você deseja tooprotect e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9b582-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="9b582-236">Em Olá **selecionar itens tooBackup** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9b582-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="9b582-237">Em Olá **especificar agendamento de Backup** , especifique o agendamento de backup hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9b582-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="9b582-238">Você pode agendar backups diários (com uma taxa máxima de três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="9b582-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Itens para o backup do Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="9b582-240">Para obter mais informações sobre como toospecify Olá agendamento de backup, consulte o artigo Olá [tooreplace uso do Azure Backup sua infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="9b582-241">Em Olá **Selecionar política de retenção** página, escolha Olá Olá de políticas de retenção específico para cópia de backup hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9b582-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="9b582-242">política de retenção de saudação especifica a duração de saudação qual backup Olá é armazenado.</span><span class="sxs-lookup"><span data-stu-id="9b582-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="9b582-243">Em vez de especificar apenas uma "política simples" para todos os pontos de backup, você pode especificar diferentes políticas de retenção com base em quando Olá backup ocorrer.</span><span class="sxs-lookup"><span data-stu-id="9b582-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="9b582-244">Você pode modificar toomeet de políticas de retenção diária, semanal, mensal e anual Olá suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9b582-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="9b582-245">Na página de escolher tipo de Backup inicial de saudação, escolha o tipo de backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="9b582-246">Deixe a opção Olá **automaticamente pela rede Olá** selecionado e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9b582-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="9b582-247">Você pode fazer backup automaticamente pela rede hello, ou você pode fazer backup offline.</span><span class="sxs-lookup"><span data-stu-id="9b582-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="9b582-248">restante Olá deste artigo descreve o processo de saudação para fazer backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9b582-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="9b582-249">Se você preferir toodo um backup offline, leia o artigo de saudação [Offline fluxo de trabalho de backup no Backup do Azure](backup-azure-backup-import-export.md) para obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="9b582-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="9b582-250">Na página de confirmação hello, revise as informações de saudação e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="9b582-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="9b582-251">Após criar o agendamento de backup Olá de conclusão do Assistente de saudação, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="9b582-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="9b582-252">Habilitar a limitação de rede</span><span class="sxs-lookup"><span data-stu-id="9b582-252">Enable network throttling</span></span>
<span data-ttu-id="9b582-253">Agente de Backup do Microsoft Azure Olá fornece a limitação de rede.</span><span class="sxs-lookup"><span data-stu-id="9b582-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="9b582-254">A limitação controles como a largura de banda de rede é usada durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="9b582-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="9b582-255">Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de Internet.</span><span class="sxs-lookup"><span data-stu-id="9b582-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="9b582-256">Limitação se aplica a tooback backup e atividades de restauração.</span><span class="sxs-lookup"><span data-stu-id="9b582-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="9b582-257">A limitação de rede não está disponível no Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ou Windows 7 (com service packs).</span><span class="sxs-lookup"><span data-stu-id="9b582-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="9b582-258">limitação de recurso de rede de Backup do Azure de Olá emprega qualidade de serviço (QoS) no sistema operacional local de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="9b582-259">Embora o Backup do Azure pode proteger esses sistemas operacionais, versão de saudação do QoS disponíveis nessas plataformas não funciona com a limitação de rede de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b582-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="9b582-260">A limitação de rede pode ser usada em todos os outros [sistemas operacionais com suporte](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="9b582-261">**a limitação de rede tooenable**</span><span class="sxs-lookup"><span data-stu-id="9b582-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="9b582-262">No agente de Backup do Microsoft Azure hello, clique em **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="9b582-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Alterar Propriedades](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="9b582-264">Em Olá **limitação** guia, selecione Olá **habilitar limitação para operações de backup do uso de largura de banda de internet** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="9b582-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitação de rede](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="9b582-266">Depois de habilitar a limitação, especifique Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.</span><span class="sxs-lookup"><span data-stu-id="9b582-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="9b582-267">os valores de largura de banda Olá começam em 512 Kbps por segundo (Kbps) e podem subir too1, 023 megabytes por segundo (MBps).</span><span class="sxs-lookup"><span data-stu-id="9b582-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="9b582-268">Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são consideradas trabalho dias.</span><span class="sxs-lookup"><span data-stu-id="9b582-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="9b582-269">Horas fora das horas úteis designadas são consideradas horas não úteis.</span><span class="sxs-lookup"><span data-stu-id="9b582-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="9b582-270">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b582-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="9b582-271">tooback backup de arquivos e pastas para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="9b582-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="9b582-272">No agente de backup hello, clique em **backup agora** toocomplete saudação inicial de propagação pela rede hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Fazer backup do Windows Server agora](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="9b582-274">Na página de confirmação hello, configurações de saudação de revisão que Olá Assistente fazer backup agora usará tooback máquina hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="9b582-275">Em seguida, clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="9b582-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="9b582-276">Clique em **fechar** tooclose Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="9b582-277">Se você fizer isso, antes de concluir o processo de backup Olá, o assistente Olá continua toorun no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b582-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="9b582-278">Após o backup inicial hello, Olá **trabalho concluído** status aparece no console de Backup hello.</span><span class="sxs-lookup"><span data-stu-id="9b582-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR completo](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="9b582-280">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="9b582-280">Questions?</span></span>
<span data-ttu-id="9b582-281">Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="9b582-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b582-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b582-282">Next steps</span></span>
<span data-ttu-id="9b582-283">Para saber mais sobre como fazer backup de VMs ou de outras cargas de trabalho, confira:</span><span class="sxs-lookup"><span data-stu-id="9b582-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="9b582-284">Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="9b582-285">Se você precisar toorestore um backup, use este artigo muito[restaurar arquivos tooa Windows máquina](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9b582-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
