---
title: Use o agente de Backup do Azure para fazer backup de arquivos e pastas | Microsoft Docs
description: "Use o agente de Backup do Microsoft Azure para fazer backup de seus arquivos e pastas do Windows no Azure. Crie um cofre de Serviços de Recuperação, instale o agente de Backup, definir a política de backup e execute o backup inicial nos arquivos e pastas."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="58fe5-105">Fazer backup de um cliente ou servidor do Windows Azure usando o modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="58fe5-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58fe5-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="58fe5-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="58fe5-107">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="58fe5-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="58fe5-108">Este artigo explica como fazer backup dos seus arquivos e pastas do Windows Server (ou cliente Windows) no Azure com o Backup do Azure usando o modelo de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="58fe5-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Etapas do processo de backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="58fe5-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="58fe5-110">Before you start</span></span>
<span data-ttu-id="58fe5-111">Para fazer backup de um servidor ou cliente no Azure, você precisará de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="58fe5-112">Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="58fe5-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="58fe5-113">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="58fe5-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="58fe5-114">Um cofre dos Serviços de Recuperação é uma entidade que armazena todos os backups e pontos de recuperação criados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="58fe5-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="58fe5-115">O cofre dos Serviços de Recuperação também contém a política de backup aplicada às pastas e arquivos protegidos.</span><span class="sxs-lookup"><span data-stu-id="58fe5-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="58fe5-116">Quando você cria um cofre dos Serviços de Recuperação, também deve selecionar a opção de redundância de armazenamento apropriada.</span><span class="sxs-lookup"><span data-stu-id="58fe5-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="58fe5-117">Para criar um cofre de Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="58fe5-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="58fe5-118">Se ainda não tiver feito isso, entre no [Portal do Azure](https://portal.azure.com/) usando a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="58fe5-119">No menu Hub, clique em **Mais serviços** e, na lista de recursos, digite **Serviços de Recuperação** e clique em **Cofres dos Serviços de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="58fe5-121">Se houver cofres dos serviços de recuperação na assinatura, os cofres serão listados.</span><span class="sxs-lookup"><span data-stu-id="58fe5-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="58fe5-122">No menu **Cofres de Serviços de Recuperação**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="58fe5-124">A folha do cofre dos Serviços de Recuperação será aberta, solicitando que você forneça o **Nome**, a **Assinatura**, o **Grupo de recursos** e o **Local**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Criar Cofre de Serviços de Recuperação - etapa 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="58fe5-126">Em **Nome**, insira um nome amigável para identificar o cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="58fe5-127">O nome deve ser exclusivo para a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="58fe5-128">Digite um nome que contenha de 2 a 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="58fe5-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="58fe5-129">Ele deve começar com uma letra e pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="58fe5-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="58fe5-130">Na seção **Assinatura**, use o menu suspenso para escolher a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="58fe5-131">Se você usar apenas uma assinatura, essa assinatura será exibida e você poderá pular para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="58fe5-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="58fe5-132">Se você não tiver certeza sobre qual assinatura usar, utilize a assinatura padrão (ou sugerida).</span><span class="sxs-lookup"><span data-stu-id="58fe5-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="58fe5-133">Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="58fe5-134">Na seção **Grupo de recursos**:</span><span class="sxs-lookup"><span data-stu-id="58fe5-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="58fe5-135">selecione **Criar novo** se quiser criar um novo Grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="58fe5-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="58fe5-136">Ou</span><span class="sxs-lookup"><span data-stu-id="58fe5-136">Or</span></span>
    * <span data-ttu-id="58fe5-137">Selecione **Usar existente** e clique no menu suspenso para ver a lista de grupos de recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="58fe5-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="58fe5-138">Para obter informações completas sobre Grupos de recursos, confira a [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="58fe5-139">Clique em **Local** para selecionar a região geográfica do cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="58fe5-140">Essa escolha determina a região geográfica para a qual os dados de backup são enviados.</span><span class="sxs-lookup"><span data-stu-id="58fe5-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="58fe5-141">Na parte inferior da folha Cofre dos Serviços de Recuperação, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="58fe5-142">Talvez demore alguns minutos para o cofre de Serviços de Recuperação ser criado.</span><span class="sxs-lookup"><span data-stu-id="58fe5-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="58fe5-143">Monitore as notificações de status na área superior direita do portal.</span><span class="sxs-lookup"><span data-stu-id="58fe5-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="58fe5-144">Depois que o cofre é criado, ele aparece na lista de cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="58fe5-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="58fe5-145">Se após alguns minutos, você não vir seu cofre, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Clique no botão Atualizar](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="58fe5-147">Depois de ver seu cofre na lista de cofres dos Serviços de Recuperação, você estará pronto para configurar a redundância de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="58fe5-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="58fe5-148">Definir redundância de armazenamento</span><span class="sxs-lookup"><span data-stu-id="58fe5-148">Set storage redundancy</span></span>
<span data-ttu-id="58fe5-149">Quando você cria um cofre dos Serviços de Recuperação, determina como o armazenamento é replicado.</span><span class="sxs-lookup"><span data-stu-id="58fe5-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="58fe5-150">Na folha **Cofres dos Serviços de Recuperação**, clique no novo cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Selecionar o novo cofre da lista de cofres do Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="58fe5-152">Quando você selecionar o cofre, a folha **Cofre de Serviços de Recuperação** será reduzida e a folha Configurações (*que tem o nome do cofre na parte superior*) e a folha de detalhes do cofre serão abertas.</span><span class="sxs-lookup"><span data-stu-id="58fe5-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Exibir a configuração de armazenamento para um novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="58fe5-154">Na folha de configurações do novo cofre, use o slide vertical para rolar para baixo até a seção Gerenciar e clique em **Infraestrutura de Backup**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="58fe5-155">A folha Infraestrutura de Backup é aberta.</span><span class="sxs-lookup"><span data-stu-id="58fe5-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="58fe5-156">Na folha Infraestrutura de Backup, clique em **Configuração de Backup** para abrir a folha **Configuração de Backup**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Definir a configuração de armazenamento para o novo cofre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="58fe5-158">Escolha a opção de replicação de armazenamento adequada para o cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![opções de configuração de armazenamento](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="58fe5-160">Por padrão, seu cofre tem armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="58fe5-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="58fe5-161">Se você usar o Azure como um ponto de extremidade de armazenamento de backup principal, continue a usar **Georredundante**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="58fe5-162">Se você não usar o Azure como um ponto de extremidade de armazenamento de backup principal, escolha **Localmente redundante**, que reduz os custos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="58fe5-163">Leia mais sobre as opções de armazenamento [com redundância geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [com redundância local](../storage/common/storage-redundancy.md#locally-redundant-storage) nesta [Visão geral de redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="58fe5-164">Agora que você criou um cofre, prepare a sua infraestrutura para fazer backup de arquivos e pastas, baixando e instalando o agente dos Serviços de Recuperação do Microsoft Azure, baixar credenciais de cofre e usar essas credenciais para registrar o agente no cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="58fe5-165">Configurar o cofre</span><span class="sxs-lookup"><span data-stu-id="58fe5-165">Configure the vault</span></span>

1. <span data-ttu-id="58fe5-166">Na folha do cofre dos Serviços de Recuperação (para o cofre recém-criado), na seção Introdução, clique em **Backup**, na folha **Introdução ao Backup**, selecione **Meta de Backup**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="58fe5-168">A folha **Meta de Backup** será aberta.</span><span class="sxs-lookup"><span data-stu-id="58fe5-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="58fe5-169">Se o cofre de Serviços de Recuperação tiver sido configurado anteriormente, a folha **Meta de Backup** é exibida quando você clica em **Backup** na folha do cofre de Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="58fe5-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Abrir folha de meta backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="58fe5-171">No menu suspenso **Onde sua carga de trabalho é executada?**, selecione **Local**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="58fe5-172">Você escolhe **Local** porque o Windows Server ou o computador do Windows é uma máquina física que não está no Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="58fe5-173">No menu **Do que você deseja fazer backup?**, selecione **Arquivos e pastas** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuração de arquivos e pastas](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="58fe5-175">Depois de clicar em OK, uma marca de seleção aparece ao lado de **Meta de backup** e a folha **Preparar infraestrutura** será aberta.</span><span class="sxs-lookup"><span data-stu-id="58fe5-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Meta de backup configurada, prepare a infraestrutura em seguida](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="58fe5-177">Na folha **Preparar infraestrutura**, clique em **Baixar agente do Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="58fe5-179">Se você estiver usando o Windows Server Essential, opte por baixar o agente para o Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="58fe5-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="58fe5-180">Um menu pop-up solicitará que você execute ou salve MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="58fe5-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Diálogo MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="58fe5-182">Clique em **Salvar** no menu pop-up de download.</span><span class="sxs-lookup"><span data-stu-id="58fe5-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="58fe5-183">Por padrão, o arquivo **MARSagentinstaller.exe** será salvo em sua pasta Downloads.</span><span class="sxs-lookup"><span data-stu-id="58fe5-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="58fe5-184">Quando o instalador for concluído, será exibido um pop-up perguntando se você deseja executar o instalador ou abrir a pasta.</span><span class="sxs-lookup"><span data-stu-id="58fe5-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![Preparar infraestrutura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="58fe5-186">Você não precisa instalar o agente ainda.</span><span class="sxs-lookup"><span data-stu-id="58fe5-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="58fe5-187">Você poderá instalar o agente depois de baixar as credenciais do cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="58fe5-188">Na folha **Preparar infraestrutura**, clique em **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![baixar as credenciais do cofre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="58fe5-190">As credenciais do cofre são baixadas para a pasta Downloads.</span><span class="sxs-lookup"><span data-stu-id="58fe5-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="58fe5-191">Após o término do download das credenciais do cofre, você verá um pop-up perguntando se deseja abrir ou salvar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="58fe5-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="58fe5-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-192">Click **Save**.</span></span> <span data-ttu-id="58fe5-193">Se você clicar acidentalmente em **Abrir**, deixe a caixa de diálogo que tenta abrir as credenciais do cofre falhar.</span><span class="sxs-lookup"><span data-stu-id="58fe5-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="58fe5-194">Não é possível abrir as credenciais do cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="58fe5-195">Vá para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="58fe5-195">Proceed to the next step.</span></span> <span data-ttu-id="58fe5-196">As credenciais do cofre estão na pasta Downloads.</span><span class="sxs-lookup"><span data-stu-id="58fe5-196">The vault credentials are in the Downloads folder.</span></span>   

  ![o download das credenciais do cofre foi concluído](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="58fe5-198">Instalar e registrar o agente</span><span class="sxs-lookup"><span data-stu-id="58fe5-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="58fe5-199">A habilitação do backup pelo portal do Azure ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="58fe5-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="58fe5-200">Use o Agente dos Serviços de Recuperação do Microsoft Azure para fazer backup de seus arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="58fe5-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="58fe5-201">Localize e clique duas vezes no **MARSagentinstaller.exe** na pasta Downloads (ou em outro local salvo).</span><span class="sxs-lookup"><span data-stu-id="58fe5-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="58fe5-202">O instalador fornece uma série de mensagens, pois extrai, instala e registra o agente dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="58fe5-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![execute as credenciais do instalador do agente dos Serviços de Recuperação](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="58fe5-204">Conclua o Assistente de Instalação do Agente do Serviços de Recuperação do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="58fe5-205">Para concluir o assistente, você precisa fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="58fe5-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="58fe5-206">Escolher um local para a instalação e a pasta de cache.</span><span class="sxs-lookup"><span data-stu-id="58fe5-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="58fe5-207">Fornecer as informações de seu servidor proxy se você usar um servidor proxy para conectar-se à Internet.</span><span class="sxs-lookup"><span data-stu-id="58fe5-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="58fe5-208">Forneça os detalhes do seu nome de usuário e de sua senha se usar um proxy autenticado.</span><span class="sxs-lookup"><span data-stu-id="58fe5-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="58fe5-209">Forneça as credenciais do cofre baixado</span><span class="sxs-lookup"><span data-stu-id="58fe5-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="58fe5-210">Salve a senha de criptografia em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="58fe5-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="58fe5-211">Se você perder ou esquecer a senha, a Microsoft não poderá ajudar a recuperar os dados de backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="58fe5-212">Salve o arquivo em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="58fe5-212">Save the file in a secure location.</span></span> <span data-ttu-id="58fe5-213">Isso é necessário para restaurar um backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="58fe5-214">Agora, o agente está instalado e seu computador está registrado no cofre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="58fe5-215">Você está pronto para configurar e agendar o backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="58fe5-216">Requisitos de conectividade e rede</span><span class="sxs-lookup"><span data-stu-id="58fe5-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="58fe5-217">Se seu computador/proxy tiver acesso limitado à Internet, verifique se as configurações do firewall no computador/proxy estão definidas para permitir as seguintes URLs:</span><span class="sxs-lookup"><span data-stu-id="58fe5-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="58fe5-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="58fe5-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="58fe5-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="58fe5-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="58fe5-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="58fe5-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="58fe5-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="58fe5-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="58fe5-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="58fe5-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="58fe5-223">Criar a política de backup</span><span class="sxs-lookup"><span data-stu-id="58fe5-223">Create the backup policy</span></span>
<span data-ttu-id="58fe5-224">A política de backup é a agenda de quando os pontos de recuperação são criados e por quanto tempo esses pontos de recuperação serão mantidos.</span><span class="sxs-lookup"><span data-stu-id="58fe5-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="58fe5-225">Use o agente de Backup do Microsoft Azure para criar a política de backup para arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="58fe5-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="58fe5-226">Para criar uma agenda de backup</span><span class="sxs-lookup"><span data-stu-id="58fe5-226">To create a backup schedule</span></span>
1. <span data-ttu-id="58fe5-227">Abra o Agente de Backup do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="58fe5-228">Você pode localizá-lo pesquisando no seu computador por **Backup do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Iniciar o agente de Backup do Azure](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="58fe5-230">No painel **Ações** do agente de Backup, clique em **Agendar Backup** para iniciar o Assistente Agendar Backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Agendar um backup do Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="58fe5-232">Na página de **Introdução** do Assistente de Agendamento de Backup, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="58fe5-233">Na tela **Selecionar Itens para Backup**, clique em **Adicionar Itens**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="58fe5-234">A caixa de diálogo Selecionar Itens é exibida.</span><span class="sxs-lookup"><span data-stu-id="58fe5-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="58fe5-235">Selecione os arquivos e pastas que você deseja proteger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="58fe5-236">Na página **Selecionar Itens para Backup**, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="58fe5-237">Na página **Especificar Agenda de Backup**, especifique a agenda de backup e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="58fe5-238">Você pode agendar backups diários (com uma taxa máxima de três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="58fe5-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Itens para o backup do Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="58fe5-240">Para saber mais sobre como especificar o agendamento de backup, confira o artigo [Usar o Backup do Azure para substituir a sua infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="58fe5-241">Na página **Selecionar Política de Retenção**, escolha as políticas de retenção específicas para a cópia de backup e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="58fe5-242">A política de retenção especifica a duração do armazenamento do backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="58fe5-243">Em vez de especificar apenas uma “política simples” para todos os pontos de backup, você pode especificar políticas de retenção diferentes com base em quando o backup ocorre.</span><span class="sxs-lookup"><span data-stu-id="58fe5-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="58fe5-244">Você pode modificar as políticas de retenção diária, semanal, mensal e anual para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="58fe5-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="58fe5-245">Na tela Escolher Tipo de Backup Inicial, escolha o tipo de backup inicial.</span><span class="sxs-lookup"><span data-stu-id="58fe5-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="58fe5-246">Deixe a opção **Automaticamente pela rede** selecionada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="58fe5-247">Você pode fazer backup automaticamente pela rede ou pode fazer backup offline.</span><span class="sxs-lookup"><span data-stu-id="58fe5-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="58fe5-248">O restante deste artigo descreve o processo para realização de backup automático.</span><span class="sxs-lookup"><span data-stu-id="58fe5-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="58fe5-249">Se preferir fazer um backup offline, examine o artigo [Fluxo de trabalho de backup offline no Backup do Azure](backup-azure-backup-import-export.md) para obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="58fe5-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="58fe5-250">Na página Confirmação, examine as informações e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="58fe5-251">Depois que o assistente terminar de criar o agendamento de backup, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="58fe5-252">Habilitar a limitação de rede</span><span class="sxs-lookup"><span data-stu-id="58fe5-252">Enable network throttling</span></span>
<span data-ttu-id="58fe5-253">O agente do Backup do Microsoft Azure fornece a limitação de rede.</span><span class="sxs-lookup"><span data-stu-id="58fe5-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="58fe5-254">A limitação controles como a largura de banda de rede é usada durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="58fe5-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="58fe5-255">Esse controle poderá ser útil se você precisar fazer backup de dados durante o horário de expediente, mas não quiser que o processo de backup interfira em outro tráfego de Internet.</span><span class="sxs-lookup"><span data-stu-id="58fe5-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="58fe5-256">A limitação aplica-se a atividades de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="58fe5-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="58fe5-257">A limitação de rede não está disponível no Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ou Windows 7 (com service packs).</span><span class="sxs-lookup"><span data-stu-id="58fe5-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="58fe5-258">A limitação de recurso de rede do Backup do Azure envolve a QoS (Qualidade de Serviço) no sistema operacional local.</span><span class="sxs-lookup"><span data-stu-id="58fe5-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="58fe5-259">Embora o Backup do Azure possa proteger esses sistemas operacionais, a versão de QoS disponível nessas plataformas não funciona com a limitação de rede do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="58fe5-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="58fe5-260">A limitação de rede pode ser usada em todos os outros [sistemas operacionais com suporte](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="58fe5-261">**Para habilitar a limitação de rede**</span><span class="sxs-lookup"><span data-stu-id="58fe5-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="58fe5-262">No agente de Backup do Microsoft Azure, clique em **Alterar Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Alterar Propriedades](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="58fe5-264">Na guia **Limitação**, marque a caixa de seleção **Habilitar limitação de uso de largura de banda da Internet para operações de backup**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitação de rede](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="58fe5-266">Depois de habilitar a limitação, especifique a largura de banda permitida para transferência de dados de backup durante as **Horas úteis** e as **Horas não úteis**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="58fe5-267">Os valores de largura de banda começam em 512 quilobits por segundo (Kbps) e podem ir até 1.023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="58fe5-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="58fe5-268">Você também pode indicar o início e o término para **Horas úteis**e quais dias da semana são considerados dias úteis.</span><span class="sxs-lookup"><span data-stu-id="58fe5-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="58fe5-269">Horas fora das horas úteis designadas são consideradas horas não úteis.</span><span class="sxs-lookup"><span data-stu-id="58fe5-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="58fe5-270">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="58fe5-271">Para fazer backup de arquivos e pastas pela primeira vez</span><span class="sxs-lookup"><span data-stu-id="58fe5-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="58fe5-272">No agente de backup, clique em **Fazer Backup Agora** para concluir a propagação inicial pela rede.</span><span class="sxs-lookup"><span data-stu-id="58fe5-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Fazer backup do Windows Server agora](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="58fe5-274">Na página Confirmação, examine as configurações que o Assistente Fazer Backup Agora usará para fazer backup do computador.</span><span class="sxs-lookup"><span data-stu-id="58fe5-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="58fe5-275">Em seguida, clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="58fe5-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="58fe5-276">Clique em **Fechar** para fechar o assistente.</span><span class="sxs-lookup"><span data-stu-id="58fe5-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="58fe5-277">Se você fizer isso antes da conclusão do processo de backup, o assistente continuará a ser executado em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="58fe5-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="58fe5-278">Depois que o backup inicial for concluído, o status **Trabalho concluído** aparecerá no Console de backup.</span><span class="sxs-lookup"><span data-stu-id="58fe5-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR completo](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="58fe5-280">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="58fe5-280">Questions?</span></span>
<span data-ttu-id="58fe5-281">Se você tiver dúvidas ou gostaria de ver algum recurso incluído, [envie-nos seus comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="58fe5-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58fe5-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58fe5-282">Next steps</span></span>
<span data-ttu-id="58fe5-283">Para saber mais sobre como fazer backup de VMs ou de outras cargas de trabalho, confira:</span><span class="sxs-lookup"><span data-stu-id="58fe5-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="58fe5-284">Agora que você faz backup de seus arquivos e pastas, poderá [gerenciar seus servidores e cofres](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="58fe5-285">Se você precisar restaurar um backup, use este artigo para [restaurar os arquivos para um computador que usa o Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="58fe5-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
