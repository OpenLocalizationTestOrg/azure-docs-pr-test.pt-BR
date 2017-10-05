---
title: "Gerenciar servidores e cofres de Backup do Azure usando o modelo de implantação clássico | Microsoft Docs"
description: Use este tutorial para aprender a gerenciar servidores e cofres de Backup do Azure.
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
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="4bec6-103">Gerenciar servidores e cofres de Backup do Azure usando o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="4bec6-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bec6-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4bec6-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="4bec6-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="4bec6-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="4bec6-106">Neste artigo, você encontra uma visão geral das tarefas de gerenciamento de backup disponíveis no portal clássico do Azure e o agente de Backup do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4bec6-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bec6-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4bec6-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4bec6-108">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="4bec6-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4bec6-109">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="4bec6-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bec6-110">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="4bec6-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="4bec6-111">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="4bec6-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="4bec6-112">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="4bec6-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="4bec6-113">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="4bec6-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="4bec6-114">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="4bec6-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="4bec6-115">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="4bec6-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="4bec6-116">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="4bec6-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="4bec6-117">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="4bec6-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="4bec6-118">Tarefas do portal de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4bec6-118">Management portal tasks</span></span>
1. <span data-ttu-id="4bec6-119">Entre no [Portal de Gerenciamento](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4bec6-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4bec6-120">Clique em **Serviços de Recuperação**, em seguida, clique no nome do cofre de backup para exibir a página de Início Rápido.</span><span class="sxs-lookup"><span data-stu-id="4bec6-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Serviços de Recuperação](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="4bec6-122">Selecionando as opções na parte superior da página Início Rápido, você pode ver as tarefas de gerenciamento disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4bec6-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Gerenciar guias](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="4bec6-124">Painel</span><span class="sxs-lookup"><span data-stu-id="4bec6-124">Dashboard</span></span>
<span data-ttu-id="4bec6-125">Clique em **Painel** para ver a visão geral do uso para o servidor.</span><span class="sxs-lookup"><span data-stu-id="4bec6-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="4bec6-126">A **visão geral de uso** inclui:</span><span class="sxs-lookup"><span data-stu-id="4bec6-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="4bec6-127">O número de Windows Servers registrados na nuvem</span><span class="sxs-lookup"><span data-stu-id="4bec6-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="4bec6-128">O número de máquinas virtuais do Azure protegidas na nuvem</span><span class="sxs-lookup"><span data-stu-id="4bec6-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="4bec6-129">O armazenamento total consumido no Azure</span><span class="sxs-lookup"><span data-stu-id="4bec6-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="4bec6-130">O status de trabalhos recentes</span><span class="sxs-lookup"><span data-stu-id="4bec6-130">The status of recent jobs</span></span>

<span data-ttu-id="4bec6-131">Na parte inferior do Painel, você pode executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4bec6-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="4bec6-132">**Gerenciar certificado** - se um certificado tiver sido usado para registrar o servidor, então use isso para atualizar o certificado.</span><span class="sxs-lookup"><span data-stu-id="4bec6-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="4bec6-133">Se estiver usando as credenciais do cofre, não use **Gerenciar certificados**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="4bec6-134">**Excluir** - exclui o cofre de backup atual.</span><span class="sxs-lookup"><span data-stu-id="4bec6-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="4bec6-135">Se não estiver sendo usado um cofre de backup, você poderá excluir para liberar mais espaço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4bec6-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="4bec6-136">**Excluir** é ativado somente depois que todos os servidores registrados foram excluídos do cofre.</span><span class="sxs-lookup"><span data-stu-id="4bec6-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="4bec6-138">Itens registrados</span><span class="sxs-lookup"><span data-stu-id="4bec6-138">Registered items</span></span>
<span data-ttu-id="4bec6-139">Selecione **Itens registrados** para exibir os nomes dos servidores registrados para o cofre.</span><span class="sxs-lookup"><span data-stu-id="4bec6-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="4bec6-141">O filtro **Tipo** tem como padrão a Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bec6-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="4bec6-142">Para exibir os nomes dos servidores registrados neste cofre, selecione **Windows Server** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="4bec6-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="4bec6-143">A partir daqui, você pode executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4bec6-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="4bec6-144">**Permitir Novo Registro** - quando essa opção estiver selecionada para um servidor, você poderá usar o **Assistente de Registro** no agente de Backup do Microsoft Azure local para registrar o servidor com o cofre de backup uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="4bec6-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="4bec6-145">Talvez você precise registrar novamente devido a um erro no certificado ou se um servidor tiver que ser refeito.</span><span class="sxs-lookup"><span data-stu-id="4bec6-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="4bec6-146">**Excluir** - Exclui um servidor do cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="4bec6-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="4bec6-147">Todos os dados armazenados associados ao servidor serão excluídos imediatamente.</span><span class="sxs-lookup"><span data-stu-id="4bec6-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Tarefas de itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="4bec6-149">Itens protegidos</span><span class="sxs-lookup"><span data-stu-id="4bec6-149">Protected items</span></span>
<span data-ttu-id="4bec6-150">Clique em **Itens Protegidos** para ver os itens que foram colocados no backup dos servidores.</span><span class="sxs-lookup"><span data-stu-id="4bec6-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Itens protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="4bec6-152">Configurar</span><span class="sxs-lookup"><span data-stu-id="4bec6-152">Configure</span></span>
<span data-ttu-id="4bec6-153">Na guia **Configurar** , você pode selecionar a opção de redundância de armazenamento apropriada.</span><span class="sxs-lookup"><span data-stu-id="4bec6-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="4bec6-154">O melhor momento para selecionar a opção de redundância de armazenamento é logo após a criação de um cofre e antes de qualquer computador ser registrado nele.</span><span class="sxs-lookup"><span data-stu-id="4bec6-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="4bec6-155">Depois que um item tiver sido registrado no cofre, a opção de redundância de armazenamento será bloqueada e não poderá ser modificada.</span><span class="sxs-lookup"><span data-stu-id="4bec6-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configurar](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="4bec6-157">Confira este artigo para saber mais sobre a [redundância de armazenamento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="4bec6-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="4bec6-158">Tarefas do agente de Backup do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4bec6-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="4bec6-159">Console</span><span class="sxs-lookup"><span data-stu-id="4bec6-159">Console</span></span>
<span data-ttu-id="4bec6-160">Abra o **agente de Backup do Microsoft Azure** (você poderá localizá-lo procurando *Backup do Microsoft Azure*em seu computador).</span><span class="sxs-lookup"><span data-stu-id="4bec6-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="4bec6-162">Na guia **Ações** , disponibilizada à direita do console do agente de backup, você pode executar as seguintes tarefas de gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="4bec6-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="4bec6-163">Registrar Servidor</span><span class="sxs-lookup"><span data-stu-id="4bec6-163">Register Server</span></span>
* <span data-ttu-id="4bec6-164">Agendar backup</span><span class="sxs-lookup"><span data-stu-id="4bec6-164">Schedule Backup</span></span>
* <span data-ttu-id="4bec6-165">Fazer backup agora</span><span class="sxs-lookup"><span data-stu-id="4bec6-165">Back Up now</span></span>
* <span data-ttu-id="4bec6-166">Alterar propriedades</span><span class="sxs-lookup"><span data-stu-id="4bec6-166">Change Properties</span></span>

![Ações do console do agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="4bec6-168">Para **Recuperar Dados**, consulte [Restaurar arquivos para um computador cliente Windows ou um servidor Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="4bec6-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="4bec6-169">Modificar um backup existente</span><span class="sxs-lookup"><span data-stu-id="4bec6-169">Modify an existing backup</span></span>
1. <span data-ttu-id="4bec6-170">No agente de Backup do Microsoft Azure, clique em **Agendar Backup**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="4bec6-172">No **Assistente de Agendamento de Backup**, deixe a opção **Fazer alterações aos itens ou horários de backup** selecionada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificar um backup agendado](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="4bec6-174">Se quiser adicionar ou alterar itens, na tela **Selecionar Itens para Backup**, clique em **Adicionar Itens**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="4bec6-175">Você também pode definir **Configurações de Exclusão** nesta página do assistente.</span><span class="sxs-lookup"><span data-stu-id="4bec6-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="4bec6-176">Se você quiser excluir arquivos ou tipos de arquivo, leia o procedimento para adicionar [configurações de exclusão](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="4bec6-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="4bec6-177">Selecione os arquivos e as pastas dos quais você deseja fazer backup e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Adicionar Itens](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="4bec6-179">Especifique o **agendamento de backup** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="4bec6-180">Você pode agendar backups diários (no máximo três vezes por dia) ou backups semanais.</span><span class="sxs-lookup"><span data-stu-id="4bec6-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Especificar o agendamento do Backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="4bec6-182">A especificação do agendamento de backup é explicada em detalhes neste [artigo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="4bec6-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="4bec6-183">Selecione a **Política de Retenção** para a cópia de backup e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Selecionar a política de retenção](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="4bec6-185">Na tela **Confirmação**, examine as informações e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="4bec6-186">Depois que o assistente terminar de criar o **agendamento de backup**, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="4bec6-187">Depois de modificar a proteção, é possível confirmar se os backups estão sendo acionados corretamente acessando a guia **Trabalhos** e confirmando se as alterações são refletidas nos trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="4bec6-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="4bec6-188">Habilitar a limitação de rede</span><span class="sxs-lookup"><span data-stu-id="4bec6-188">Enable Network Throttling</span></span>
<span data-ttu-id="4bec6-189">O agente de Backup do Azure fornece uma guia Limitação, que permite controlar como a largura de banda é usada durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="4bec6-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="4bec6-190">Esse controle pode ser útil se você precisa fazer backup de dados durante o horário de expediente, mas não quer que o processo de backup interfira no outro tráfego de Internet.</span><span class="sxs-lookup"><span data-stu-id="4bec6-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="4bec6-191">A limitação da transferência de dados aplica-se a atividades de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="4bec6-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="4bec6-192">Para habilitar a limitação:</span><span class="sxs-lookup"><span data-stu-id="4bec6-192">To enable throttling:</span></span>

1. <span data-ttu-id="4bec6-193">No **agente de backup**, clique em **Alterar Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="4bec6-194">Marque a caixa de seleção **Habilitar limitação de uso de largura de banda da Internet para operações de backup** .</span><span class="sxs-lookup"><span data-stu-id="4bec6-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitação de rede](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="4bec6-196">Depois de habilitar a limitação, especifique a largura de banda permitida para a transferência de dados de backup durante as **Horas úteis** e **Horas não úteis**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="4bec6-197">Os valores de largura de banda começam em 512 quilobytes por segundo (Kbps) e podem ir até 1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="4bec6-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="4bec6-198">Você também pode indicar o início e o término das **Horas úteis**e quais dias da semana são considerados dias úteis.</span><span class="sxs-lookup"><span data-stu-id="4bec6-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="4bec6-199">O tempo fora das Horas úteis indicadas é considerado como hora não útil.</span><span class="sxs-lookup"><span data-stu-id="4bec6-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="4bec6-200">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="4bec6-201">Configurações de Exclusão</span><span class="sxs-lookup"><span data-stu-id="4bec6-201">Exclusion settings</span></span>
1. <span data-ttu-id="4bec6-202">Abra o **agente de Backup do Microsoft Azure** (você poderá localizá-lo procurando *Backup do Microsoft Azure*em seu computador).</span><span class="sxs-lookup"><span data-stu-id="4bec6-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Abrir agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="4bec6-204">No agente de Backup do Microsoft Azure, clique em **Agendar Backup**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="4bec6-206">No Assistente de Agendamento de Backup, deixe a opção **Fazer alterações aos itens ou horários de backup** selecionada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificar um agendamento](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="4bec6-208">Clique em **Configurações de Exclusões**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-208">Click **Exclusions Settings**.</span></span>

    ![Selecione itens a serem excluídos](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="4bec6-210">Clique em **Adicionar Exclusão**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-210">Click **Add Exclusion**.</span></span>

    ![Adicionar exclusões](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="4bec6-212">Selecione o local e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-212">Select the location and then, click **OK**.</span></span>

    ![Selecionar um local para exclusão](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="4bec6-214">Adicione a extensão de arquivo no campo **Tipo de Arquivo** .</span><span class="sxs-lookup"><span data-stu-id="4bec6-214">Add the file extension in the **File Type** field.</span></span>

    ![Excluir por tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="4bec6-216">Adição de uma extensão .mp3</span><span class="sxs-lookup"><span data-stu-id="4bec6-216">Adding an .mp3 extension</span></span>

    ![Exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="4bec6-218">Para adicionar outra extensão, clique em **Adicionar Exclusão** e insira outra extensão do tipo de arquivo (adicionando uma extensão .jpeg).</span><span class="sxs-lookup"><span data-stu-id="4bec6-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Outro exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="4bec6-220">Quando tiver adicionado todas as extensões, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="4bec6-221">Prossiga com o Assistente de Agendamento de Backup clicando em **Avançar** até a **página Confirmação** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4bec6-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmação de exclusão](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="4bec6-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bec6-223">Next steps</span></span>
* [<span data-ttu-id="4bec6-224">Restaurar o Windows Server ou o Windows Client do Azure</span><span class="sxs-lookup"><span data-stu-id="4bec6-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="4bec6-225">Para saber mais sobre o Backup do Azure, confira [Visão geral do backup do Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="4bec6-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="4bec6-226">Visite o [Fórum de backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="4bec6-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
