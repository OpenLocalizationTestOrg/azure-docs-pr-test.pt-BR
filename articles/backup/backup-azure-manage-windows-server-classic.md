---
title: "os cofres de Backup do Azure aaaManage e servidores do Azure usando o modelo de implantação clássico Olá | Microsoft Docs"
description: Use este tutorial toolearn como toomanage Backup do Azure cofres e servidores.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="0aa4c-103">Gerenciar servidores usando o modelo de implantação clássico hello e cofres de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="0aa4c-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0aa4c-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="0aa4c-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="0aa4c-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="0aa4c-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="0aa4c-106">Neste artigo, você encontrará uma visão geral de tarefas de gerenciamento de backup de Olá disponíveis por meio de saudação portal clássico do Azure e o agente de Backup do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0aa4c-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0aa4c-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0aa4c-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0aa4c-110">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="0aa4c-111">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0aa4c-112">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="0aa4c-113">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="0aa4c-114">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="0aa4c-115">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="0aa4c-116">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="0aa4c-117">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="0aa4c-118">Tarefas do portal de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0aa4c-118">Management portal tasks</span></span>
1. <span data-ttu-id="0aa4c-119">Entrar toohello [Portal de gerenciamento](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0aa4c-120">Clique em **dos serviços de recuperação**, clique em nome de saudação da página de início rápido do Cofre de backup tooview hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Serviços de Recuperação](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="0aa4c-122">Selecionando opções de saudação na parte superior de saudação da página de início rápido do hello, você pode ver tarefas de gerenciamento disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Gerenciar guias](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="0aa4c-124">Painel</span><span class="sxs-lookup"><span data-stu-id="0aa4c-124">Dashboard</span></span>
<span data-ttu-id="0aa4c-125">Selecione **painel** toosee visão geral de uso de saudação para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="0aa4c-126">Olá **visão geral de uso** inclui:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="0aa4c-127">número de saudação de servidores Windows registrados toocloud</span><span class="sxs-lookup"><span data-stu-id="0aa4c-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="0aa4c-128">número de saudação de máquinas virtuais do Azure protegidas na nuvem</span><span class="sxs-lookup"><span data-stu-id="0aa4c-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="0aa4c-129">armazenamento total de saudação consumido no Azure</span><span class="sxs-lookup"><span data-stu-id="0aa4c-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="0aa4c-130">status de saudação de trabalhos recentes</span><span class="sxs-lookup"><span data-stu-id="0aa4c-130">hello status of recent jobs</span></span>

<span data-ttu-id="0aa4c-131">Na parte inferior de saudação do hello painel, você pode executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="0aa4c-132">**Gerenciar certificado** - se um certificado foi usado tooregister Olá servidor, use este certificado de saudação tooupdate.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="0aa4c-133">Se estiver usando as credenciais do cofre, não use **Gerenciar certificados**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="0aa4c-134">**Excluir** -Cofre de backup atual de saudação exclusões.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="0aa4c-135">Se já não estiver sendo usado um cofre de backup, você pode excluir toofree o espaço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="0aa4c-136">**Excluir** só estará habilitada após a exclusão de todos os servidores registrados do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="0aa4c-138">Itens registrados</span><span class="sxs-lookup"><span data-stu-id="0aa4c-138">Registered items</span></span>
<span data-ttu-id="0aa4c-139">Selecione **itens registrados** nomes de saudação do tooview de servidores de saudação que são registrados toothis cofre.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="0aa4c-141">Olá **tipo** filtrar padrões tooAzure Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="0aa4c-142">nomes de Olá tooview de servidores Olá cofre toothis registrado, selecione **do Windows server** de saudação menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="0aa4c-143">Aqui você pode executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="0aa4c-144">**Permitir novo registro** - quando essa opção é selecionada para um servidor que você pode usar Olá **Assistente de registro** em Olá Microsoft Azure Backup agent tooregister Olá servidor local com o Cofre de backup Olá uma segunda vez .</span><span class="sxs-lookup"><span data-stu-id="0aa4c-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="0aa4c-145">Talvez seja necessário toore registro devido a erro tooan no certificado de saudação ou se um servidor tiver toobe recriado.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="0aa4c-146">**Excluir** -exclui um servidor do Cofre de backup hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="0aa4c-147">Todos os dados de saudação armazenado associados ao servidor de saudação são excluídos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Tarefas de itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="0aa4c-149">Itens protegidos</span><span class="sxs-lookup"><span data-stu-id="0aa4c-149">Protected items</span></span>
<span data-ttu-id="0aa4c-150">Selecione **itens protegidos** tooview itens de saudação que foi feitos um backup de servidores de saudação.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Itens protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="0aa4c-152">Configurar</span><span class="sxs-lookup"><span data-stu-id="0aa4c-152">Configure</span></span>
<span data-ttu-id="0aa4c-153">De saudação **configurar** guia, você pode selecionar a opção de redundância de armazenamento apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="0aa4c-154">Olá melhor tempo tooselect Olá redundância opção de armazenamento é logo após a criação de um cofre e antes de todas as máquinas tooit registrado.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="0aa4c-155">Depois que um item tiver sido registrado toohello cofre, opção de redundância de armazenamento hello está bloqueada e não pode ser modificada.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configurar](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="0aa4c-157">Confira este artigo para saber mais sobre a [redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="0aa4c-158">Tarefas do agente de Backup do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0aa4c-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="0aa4c-159">Console</span><span class="sxs-lookup"><span data-stu-id="0aa4c-159">Console</span></span>
<span data-ttu-id="0aa4c-160">Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="0aa4c-162">De saudação **ações** disponíveis em Olá direita do console do agente de backup Olá executar Olá tarefas de gerenciamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="0aa4c-163">Registrar Servidor</span><span class="sxs-lookup"><span data-stu-id="0aa4c-163">Register Server</span></span>
* <span data-ttu-id="0aa4c-164">Agendar backup</span><span class="sxs-lookup"><span data-stu-id="0aa4c-164">Schedule Backup</span></span>
* <span data-ttu-id="0aa4c-165">Fazer backup agora</span><span class="sxs-lookup"><span data-stu-id="0aa4c-165">Back Up now</span></span>
* <span data-ttu-id="0aa4c-166">Alterar propriedades</span><span class="sxs-lookup"><span data-stu-id="0aa4c-166">Change Properties</span></span>

![Ações do console do agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="0aa4c-168">muito**recuperar dados**, consulte [restaurar arquivos tooa Windows server ou o computador de cliente do Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="0aa4c-169">Modificar um backup existente</span><span class="sxs-lookup"><span data-stu-id="0aa4c-169">Modify an existing backup</span></span>
1. <span data-ttu-id="0aa4c-170">No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="0aa4c-172">Em Olá **Assistente de agendamento de Backup** deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificar um backup agendado](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="0aa4c-174">Se você quiser tooadd ou alterar itens na Olá **selecionar itens tooBackup** tela clique **adicionar itens**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="0aa4c-175">Você também pode definir **configurações de exclusão** desta página no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="0aa4c-176">Se você quiser tooexclude arquivos ou tipos de arquivo de leitura procedimento Olá para adicionar [configurações de exclusão](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="0aa4c-177">Selecione arquivos hello e pastas que deseja tooback backup e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Adicionar Itens](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="0aa4c-179">Especifique a saudação **agendamento de backup** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="0aa4c-180">Você pode agendar backups diários (no máximo três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Especificar o agendamento do Backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="0aa4c-182">Especificar o agendamento de backup Olá é explicado em detalhes nesta [artigo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="0aa4c-183">Selecione Olá **política de retenção** para cópia de backup hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Selecionar a política de retenção](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="0aa4c-185">Em Olá **confirmação** tela hello Revise as informações e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="0aa4c-186">Depois que a conclusão do Assistente de saudação criando Olá **agendamento de backup**, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="0aa4c-187">Depois de modificar a proteção, você pode confirmar que os backups provocarem corretamente pelo vai toohello **trabalhos** guia e confirmando que as alterações sejam refletidas no hello trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="0aa4c-188">Habilitar a limitação de rede</span><span class="sxs-lookup"><span data-stu-id="0aa4c-188">Enable Network Throttling</span></span>
<span data-ttu-id="0aa4c-189">Agente de Backup do Azure Olá fornece uma guia de limitação que permite que você toocontrol como largura de banda de rede é usada durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="0aa4c-190">Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de internet.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="0aa4c-191">Transferência de limitação de dados aplica tooback backup e atividades de restauração.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="0aa4c-192">tooenable limitação:</span><span class="sxs-lookup"><span data-stu-id="0aa4c-192">tooenable throttling:</span></span>

1. <span data-ttu-id="0aa4c-193">Em Olá **agente de Backup**, clique em **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="0aa4c-194">Selecione Olá **habilitar limitação para operações de backup do uso de largura de banda de internet** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitação de rede](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="0aa4c-196">Depois que você habilitou a limitação, especificar Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="0aa4c-197">os valores de largura de banda Olá começam em 512 quilobytes por segundo (Kbps) e podem subir too1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="0aa4c-198">Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são considerados trabalho dias.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="0aa4c-199">tempo de saudação fora Olá designado de horas de trabalho é considerado toobe horas de folga.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="0aa4c-200">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="0aa4c-201">Configurações de Exclusão</span><span class="sxs-lookup"><span data-stu-id="0aa4c-201">Exclusion settings</span></span>
1. <span data-ttu-id="0aa4c-202">Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Abrir agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="0aa4c-204">No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="0aa4c-206">No Assistente de agendamento de Backup de saudação deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificar um agendamento](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="0aa4c-208">Clique em **Configurações de Exclusões**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-208">Click **Exclusions Settings**.</span></span>

    ![Selecione os itens tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="0aa4c-210">Clique em **Adicionar Exclusão**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-210">Click **Add Exclusion**.</span></span>

    ![Adicionar exclusões](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="0aa4c-212">Selecione Olá e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-212">Select hello location and then, click **OK**.</span></span>

    ![Selecionar um local para exclusão](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="0aa4c-214">Adicionar extensão de arquivo hello em Olá **tipo de arquivo** campo.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Excluir por tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="0aa4c-216">Adição de uma extensão .mp3</span><span class="sxs-lookup"><span data-stu-id="0aa4c-216">Adding an .mp3 extension</span></span>

    ![Exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="0aa4c-218">tooadd outra extensão, clique em **Adicionar exclusão** e insira outra extensão de tipo de arquivo (Adicionar uma extensão. JPEG).</span><span class="sxs-lookup"><span data-stu-id="0aa4c-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Outro exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="0aa4c-220">Quando você tiver adicionado todas as extensões de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="0aa4c-221">Continuar por Olá Assistente de agendamento de Backup clicando em **próximo** até Olá **página de confirmação**, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="0aa4c-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmação de exclusão](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="0aa4c-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0aa4c-223">Next steps</span></span>
* [<span data-ttu-id="0aa4c-224">Restaurar o Windows Server ou o Windows Client do Azure</span><span class="sxs-lookup"><span data-stu-id="0aa4c-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="0aa4c-225">toolearn mais sobre o Backup do Azure, consulte [visão geral do Backup do Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="0aa4c-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="0aa4c-226">Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="0aa4c-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
