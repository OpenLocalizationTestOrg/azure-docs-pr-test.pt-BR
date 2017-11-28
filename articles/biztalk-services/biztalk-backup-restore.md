---
title: "Criar e restaurar um backup nos Serviços BizTalk | Microsoft Docs"
description: "Os serviços BizTalk incluem backup e restauração. Saiba como criar e restaurar um backup e determinar do que é feito backup. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="c33a9-105">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="c33a9-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="c33a9-106">Os Serviços BizTalk do Azure incluem recursos de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="c33a9-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="c33a9-107">Este tópico descreve como fazer backup e restaurar os Serviços BizTalk usando o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c33a9-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="c33a9-108">Você também pode fazer backup dos Serviços do BizTalk usando os [API REST dos Serviços do BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="c33a9-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="c33a9-109">NÃO se faz backup das conexões híbridas, independentemente da Edição.</span><span class="sxs-lookup"><span data-stu-id="c33a9-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="c33a9-110">Você deve recriar suas conexões híbridas.</span><span class="sxs-lookup"><span data-stu-id="c33a9-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c33a9-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c33a9-111">Before you Begin</span></span>
* <span data-ttu-id="c33a9-112">É possível que o backup e a restauração não estejam disponíveis para todas as edições.</span><span class="sxs-lookup"><span data-stu-id="c33a9-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="c33a9-113">Consulte [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="c33a9-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="c33a9-114">Usando o portal clássico do Azure, você pode criar um backup sob demanda ou criar um backup agendado.</span><span class="sxs-lookup"><span data-stu-id="c33a9-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="c33a9-115">O conteúdo de backup pode ser restaurado para o mesmo Serviço do BizTalk ou para um novo Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="c33a9-116">Para restaurar o Serviço do BizTalk usando o mesmo nome, o Serviço do BizTalk existente precisa ser excluído e o nome precisa estar disponível.</span><span class="sxs-lookup"><span data-stu-id="c33a9-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="c33a9-117">Após excluir um Serviço do BizTalk, pode levar mais tempo do que o desejado para que o mesmo nome esteja disponível.</span><span class="sxs-lookup"><span data-stu-id="c33a9-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="c33a9-118">Se você não puder esperar para o mesmo nome esteja disponível, faça a restauração para um novo Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="c33a9-119">Os Serviços do BizTalk podem ser restaurados para a mesma edição ou para uma edição superior.</span><span class="sxs-lookup"><span data-stu-id="c33a9-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="c33a9-120">Não há suporte para a restauração dos Serviços do BizTalk para uma edição inferior, de quando foi feito um backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="c33a9-121">Por exemplo, um backup usando a Basic Edition pode ser restaurado para a Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="c33a9-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="c33a9-122">Um backup usando a Premium Edition não pode ser restaurado para a Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="c33a9-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="c33a9-123">O backup dos números de controle de EDI são feitos para manter a continuidade dos números de controle.</span><span class="sxs-lookup"><span data-stu-id="c33a9-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="c33a9-124">Se as mensagens forem processadas depois do último backup, a restauração desse conteúdo de backup pode provocar a duplicação dos números de controle.</span><span class="sxs-lookup"><span data-stu-id="c33a9-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="c33a9-125">Se um lote tiver mensagens ativas, processe o lote **antes** de executar um backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="c33a9-126">Ao criar um backup (conforme necessário ou agendado), as mensagens em lotes nunca são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="c33a9-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="c33a9-127">**Se um backup for feito com mensagens ativas em um lote, o backup dessas mensagens não será feito e, portanto, elas serão perdidas.**</span><span class="sxs-lookup"><span data-stu-id="c33a9-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="c33a9-128">Opcional: no Portal dos Serviços BizTalk, interrompa todas as operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c33a9-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="c33a9-129">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-129">Create a backup</span></span>
<span data-ttu-id="c33a9-130">Um backup pode ser obtido a qualquer momento e é totalmente controlado por você.</span><span class="sxs-lookup"><span data-stu-id="c33a9-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="c33a9-131">Esta seção lista as etapas para criar backups usando o portal clássico do Azure, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c33a9-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="c33a9-132">Backup sob demanda</span><span class="sxs-lookup"><span data-stu-id="c33a9-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="c33a9-133">Agendar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="c33a9-134"><a name="backupnow"></a>Backup sob demanda</span><span class="sxs-lookup"><span data-stu-id="c33a9-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="c33a9-135">No portal clássico do Azure, selecione **Serviços BizTalk**e, em seguida, selecione o Serviço BizTalk do você quer fazer backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="c33a9-136">Na guia **Painel**, selecione **Backup** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="c33a9-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="c33a9-137">Insira um nome de backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-137">Enter a backup name.</span></span> <span data-ttu-id="c33a9-138">Por exemplo, digite *meuServiçoBizTalk*BU*Data*.</span><span class="sxs-lookup"><span data-stu-id="c33a9-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="c33a9-139">Escolha uma conta de armazenamento de blob e selecione a marca de seleção para iniciar o backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="c33a9-140">Quando o backup for concluído, um contêiner com o nome do backup inserido será criado na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c33a9-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="c33a9-141">Esse contêiner contém a configuração de backup do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="c33a9-142"><a name="backupschedule"></a>Agendar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="c33a9-143">No portal clássico do Azure, selecione **Serviços BizTalk**, selecione o nome do Serviço BizTalk que você deseja agendar para o backup, em seguida, selecione a guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c33a9-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="c33a9-144">Defina o **Status de Backup** para **Automático**.</span><span class="sxs-lookup"><span data-stu-id="c33a9-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="c33a9-145">Selecione a **Conta de Armazenamento** para armazenar o backup, digite a **Frequência** para criar os backups e por quanto tempo manter os backups (**Dias de Retenção**):</span><span class="sxs-lookup"><span data-stu-id="c33a9-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="c33a9-146">**Observações**</span><span class="sxs-lookup"><span data-stu-id="c33a9-146">**Notes**</span></span>     
   
   * <span data-ttu-id="c33a9-147">Em **Dias de retenção**, o período de retenção deve ser maior do que a frequência de backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="c33a9-148">Selecione **Sempre manter pelo menos um backup**, mesmo que o período de retenção tenha passado.</span><span class="sxs-lookup"><span data-stu-id="c33a9-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="c33a9-149">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c33a9-149">Select **Save**.</span></span>

<span data-ttu-id="c33a9-150">Quando um trabalho de backup agendado é executado, ele cria um contêiner (para armazenar os dados do backup) na conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="c33a9-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="c33a9-151">O nome do contêiner é *Nome do Serviço BizTalk-data-hora*.</span><span class="sxs-lookup"><span data-stu-id="c33a9-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="c33a9-152">Se o painel do Serviço do BizTalk mostrar um status **Falha** :</span><span class="sxs-lookup"><span data-stu-id="c33a9-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Último status do backup agendado][BackupStatus] 

<span data-ttu-id="c33a9-154">O link abre os Logs de Operação de Serviços de Gerenciamento para ajudar solucionar os problemas.</span><span class="sxs-lookup"><span data-stu-id="c33a9-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="c33a9-155">Consulte [Serviços BizTalk: solução de problemas usando logs de operação](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="c33a9-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="c33a9-156">Restore</span><span class="sxs-lookup"><span data-stu-id="c33a9-156">Restore</span></span>
<span data-ttu-id="c33a9-157">Você pode fazer backups no portal clássico do Azure ou em [Restaurar API REST do Serviço do BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="c33a9-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="c33a9-158">Esta seção lista as etapas para restaurar usando o portal clássico.</span><span class="sxs-lookup"><span data-stu-id="c33a9-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="c33a9-159">Antes de restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-159">Before restoring a backup</span></span>
* <span data-ttu-id="c33a9-160">Os novos armazenamentos de acompanhamento, arquivamento e monitoramento podem ser especificados durante a restauração de um Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="c33a9-161">Os mesmos dados de tempo de execução do EDI são restaurados.</span><span class="sxs-lookup"><span data-stu-id="c33a9-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="c33a9-162">O backup do tempo de execução do EDI restaura os números de controle.</span><span class="sxs-lookup"><span data-stu-id="c33a9-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="c33a9-163">Os números de controle restaurados estão em sequência da hora do backup.</span><span class="sxs-lookup"><span data-stu-id="c33a9-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="c33a9-164">Se as mensagens forem processadas depois do último backup, a restauração desse conteúdo de backup pode provocar a duplicação dos números de controle.</span><span class="sxs-lookup"><span data-stu-id="c33a9-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="c33a9-165">Restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-165">Restore a backup</span></span>
1. <span data-ttu-id="c33a9-166">No portal clássico do Azure, selecione **Novo** > **Serviços de Aplicativos** > **Serviço BizTalk** > **Restaurar**:</span><span class="sxs-lookup"><span data-stu-id="c33a9-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restaurar um backup][Restore]
2. <span data-ttu-id="c33a9-168">Na **URL de backup**, selecione o ícone da pasta e expanda a conta de armazenamento do Azure que armazena o backup de configuração do Serviço de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="c33a9-169">Expanda o contêiner e no painel esquerdo, selecione o arquivo .txt de backup correspondente.</span><span class="sxs-lookup"><span data-stu-id="c33a9-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="c33a9-170">Selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="c33a9-170">Select **Open**.</span></span>
3. <span data-ttu-id="c33a9-171">Na página **Restaurar Serviço BizTalk**, insira um **Nome do Serviço BizTalk** e verifique a **URL do Domínio**, **Edição** e **Região** do Serviço BizTalk restaurado.</span><span class="sxs-lookup"><span data-stu-id="c33a9-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="c33a9-172">**Criar uma nova instância de banco de dados do SQL** para o banco de dados de acompanhamento:</span><span class="sxs-lookup"><span data-stu-id="c33a9-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="c33a9-173">Selecione a seta de avanço.</span><span class="sxs-lookup"><span data-stu-id="c33a9-173">Select the next arrow.</span></span>
4. <span data-ttu-id="c33a9-174">Verificar o nome do banco de dados SQL, insira o servidor físico onde será criado o banco de dados SQL, e um nome de usuário/senha para aquele servidor.</span><span class="sxs-lookup"><span data-stu-id="c33a9-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="c33a9-175">Se você quiser configurar a edição do banco de dados SQL, tamanho e outras propriedades, selecione  **Definir Configurações Avançadas do Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="c33a9-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="c33a9-176">Selecione a seta de avanço.</span><span class="sxs-lookup"><span data-stu-id="c33a9-176">Select the next arrow.</span></span>

1. <span data-ttu-id="c33a9-177">Crie uma nova conta de armazenamento ou especifique uma conta de armazenamento existente para o Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="c33a9-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="c33a9-178">Selecione a marca de seleção para começar a restauração.</span><span class="sxs-lookup"><span data-stu-id="c33a9-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="c33a9-179">Quando a restauração for concluída com êxito, um novo Serviço do BizTalk será listado em um estado suspenso na página Serviços do BizTalk no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c33a9-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="c33a9-180"><a name="postrestore"></a>Depois de restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="c33a9-181">O Serviço BizTalk sempre é restaurado em um estado **Suspenso** .</span><span class="sxs-lookup"><span data-stu-id="c33a9-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="c33a9-182">Neste estado, você pode fazer qualquer alteração de configuração antes que o novo ambiente esteja funcional, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c33a9-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="c33a9-183">Se você tiver criado aplicativos do Serviço BizTalk usando o SDK dos Serviços BizTalk do Azure, será necessário atualizar as credenciais de ACS (Controle de Acesso) nesses aplicativos para trabalhar com o ambiente restaurado.</span><span class="sxs-lookup"><span data-stu-id="c33a9-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="c33a9-184">Você restaura um Serviço do BizTalk para replicar um ambiente de Serviço do BizTalk existente.</span><span class="sxs-lookup"><span data-stu-id="c33a9-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="c33a9-185">Nesta situação, se houver contratos configurados no portal original de Serviços do BizTalk que usam uma pasta FTP de origem, é possível que precise atualizar os contratos no ambiente recentemente restaurado para usar uma pasta FTP de origem diferente.</span><span class="sxs-lookup"><span data-stu-id="c33a9-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="c33a9-186">De outra forma, pode haver dois contratos diferentes tentando puxar a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="c33a9-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="c33a9-187">Se você fez a restauração para ter vários ambientes do Serviço do BizTalk, certifique-se de ter como destino o ambiente certo nos aplicativos do Visual Studio, cmdlets do PowerShell, APIs REST ou APIs de OM de Gerenciamento de Parceiros Comerciais.</span><span class="sxs-lookup"><span data-stu-id="c33a9-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="c33a9-188">É uma boa prática configurar backups automáticos no ambiente do Serviço do BizTalk Service recém-restaurado.</span><span class="sxs-lookup"><span data-stu-id="c33a9-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="c33a9-189">Para iniciar o Serviço do BizTalk no portal clássico do Azure, selecione o Serviço de BizTalk e selecione **Retomar** na barra de tarefas.</span><span class="sxs-lookup"><span data-stu-id="c33a9-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="c33a9-190">Do que é feito backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-190">What gets backed up</span></span>
<span data-ttu-id="c33a9-191">Quando um backup é criado, os seguintes itens são copiados:</span><span class="sxs-lookup"><span data-stu-id="c33a9-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="c33a9-192">Itens do backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="c33a9-193">
 <strong>Portal de Serviços BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="c33a9-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c33a9-194">Configuração e tempo de execução</span><span class="sxs-lookup"><span data-stu-id="c33a9-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c33a9-195">Detalhes e perfil do parceiro</span><span class="sxs-lookup"><span data-stu-id="c33a9-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="c33a9-196">Contratos de parceiro</span><span class="sxs-lookup"><span data-stu-id="c33a9-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="c33a9-197">Assemblies personalizados implantados</span><span class="sxs-lookup"><span data-stu-id="c33a9-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="c33a9-198">Pontes implantadas</span><span class="sxs-lookup"><span data-stu-id="c33a9-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="c33a9-199">Certificados</span><span class="sxs-lookup"><span data-stu-id="c33a9-199">Certificates</span></span></li>
<li><span data-ttu-id="c33a9-200">Transformações implantadas</span><span class="sxs-lookup"><span data-stu-id="c33a9-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="c33a9-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="c33a9-201">Pipelines</span></span></li>
<li><span data-ttu-id="c33a9-202">Modelos criados e salvos no Portal de Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="c33a9-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="c33a9-203">Mapeamentos de X12 ST01 e GS01</span><span class="sxs-lookup"><span data-stu-id="c33a9-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="c33a9-204">Números de controle (EDI)</span><span class="sxs-lookup"><span data-stu-id="c33a9-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="c33a9-205">Valores de MIC de mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="c33a9-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="c33a9-206">
 <strong>Serviço BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="c33a9-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c33a9-207">Certificado SSL</span><span class="sxs-lookup"><span data-stu-id="c33a9-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c33a9-208">Dados do certificado SSL</span><span class="sxs-lookup"><span data-stu-id="c33a9-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="c33a9-209">Senha do certificado SSL</span><span class="sxs-lookup"><span data-stu-id="c33a9-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="c33a9-210">Configurações do Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="c33a9-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c33a9-211">Contagem de unidades da escala</span><span class="sxs-lookup"><span data-stu-id="c33a9-211">Scale unit count</span></span></li>
<li><span data-ttu-id="c33a9-212">Edição</span><span class="sxs-lookup"><span data-stu-id="c33a9-212">Edition</span></span></li>
<li><span data-ttu-id="c33a9-213">Versão do produto</span><span class="sxs-lookup"><span data-stu-id="c33a9-213">Product Version</span></span></li>
<li><span data-ttu-id="c33a9-214">Região/Datacenter</span><span class="sxs-lookup"><span data-stu-id="c33a9-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="c33a9-215">O namespace e a chave do ACS (Serviço de Controle de Acesso)</span><span class="sxs-lookup"><span data-stu-id="c33a9-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="c33a9-216">Cadeia de conexão do banco de dados de acompanhamento</span><span class="sxs-lookup"><span data-stu-id="c33a9-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="c33a9-217">Cadeia de conexão da conta de armazenamento de arquivamento</span><span class="sxs-lookup"><span data-stu-id="c33a9-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="c33a9-218">Cadeia de conexão da conta de armazenamento de monitoramento</span><span class="sxs-lookup"><span data-stu-id="c33a9-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="c33a9-219">
 <strong>Itens Adicionais</strong></span><span class="sxs-lookup"><span data-stu-id="c33a9-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c33a9-220">Banco de Dados de Acompanhamento</span><span class="sxs-lookup"><span data-stu-id="c33a9-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="c33a9-221">Quando o Serviço do BizTalk é criado, os detalhes do Banco de Dados de Acompanhamento são inseridos, incluindo o Servidor do Banco de Dados SQL do Azure e o nome do Banco de Dados de Acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="c33a9-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="c33a9-222">O backup do Banco de Dados de Acompanhamento não é feito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c33a9-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="c33a9-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="c33a9-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="c33a9-224">Se o Banco de Dados de Acompanhamento for excluído e o banco de dados precisar ser recuperado, deverá existir um backup anterior.</span><span class="sxs-lookup"><span data-stu-id="c33a9-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="c33a9-225">Se não existir um backup, o Banco de Dados de Acompanhamento e seus dados não poderão ser recuperados.</span><span class="sxs-lookup"><span data-stu-id="c33a9-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="c33a9-226">Nessa situação, crie um novo Banco de Dados de Acompanhamento com o mesmo nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c33a9-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="c33a9-227">A Replicação Geográfica é recomendada.</span><span class="sxs-lookup"><span data-stu-id="c33a9-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="c33a9-228">Avançar</span><span class="sxs-lookup"><span data-stu-id="c33a9-228">Next</span></span>
<span data-ttu-id="c33a9-229">Para criar os Serviços BizTalk do Azure no portal clássico do Azure, confira [Serviços BizTalk: provisionando com o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="c33a9-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="c33a9-230">Para começar a criar aplicativos, visite [Serviços BizTalk do Azure (a página pode estar em inglês)](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="c33a9-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="c33a9-231">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c33a9-231">See Also</span></span>
* [<span data-ttu-id="c33a9-232">Fazer o backup do Serviço BizTalk</span><span class="sxs-lookup"><span data-stu-id="c33a9-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="c33a9-233">Restaurar o Serviço BizTalk do backup</span><span class="sxs-lookup"><span data-stu-id="c33a9-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="c33a9-234">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="c33a9-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="c33a9-235">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="c33a9-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="c33a9-236">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="c33a9-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="c33a9-237">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="c33a9-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="c33a9-238">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="c33a9-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="c33a9-239">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="c33a9-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="c33a9-240">Como começar a usar o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="c33a9-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

