---
title: "aaaCreate e restaurar um backup nos Serviços BizTalk | Microsoft Docs"
description: "Os serviços BizTalk incluem backup e restauração. Saiba como toocreate e restaurar um backup e determinar o que foi feito backup. MABS, WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="6855c-105">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="6855c-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="6855c-106">Os Serviços BizTalk do Azure incluem recursos de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="6855c-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="6855c-107">Este tópico descreve como toobackup e restauração de serviços do BizTalk usando Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6855c-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="6855c-108">Você também pode fazer backup de serviços do BizTalk usando Olá [API REST dos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="6855c-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="6855c-109">Conexões híbridas não estão incluídas no backup independentemente Olá Edition.</span><span class="sxs-lookup"><span data-stu-id="6855c-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="6855c-110">Você deve recriar suas conexões híbridas.</span><span class="sxs-lookup"><span data-stu-id="6855c-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="6855c-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6855c-111">Before you Begin</span></span>
* <span data-ttu-id="6855c-112">É possível que o backup e a restauração não estejam disponíveis para todas as edições.</span><span class="sxs-lookup"><span data-stu-id="6855c-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="6855c-113">Consulte [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="6855c-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="6855c-114">Usando Olá portal clássico do Azure, você pode criar um backup sob demanda ou criar um backup agendado.</span><span class="sxs-lookup"><span data-stu-id="6855c-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="6855c-115">Conteúdo de backup pode ser restaurado toohello mesmo BizTalk Service ou tooa novo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="6855c-116">toorestore Olá BizTalk Service usando Olá Olá existente BizTalk Service de mesmo nome deve ser excluído e Olá nome deve estar disponível.</span><span class="sxs-lookup"><span data-stu-id="6855c-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="6855c-117">Depois de excluir um BizTalk Service, pode levar mais tempo do que desejar para Olá mesmo nome toobe disponível.</span><span class="sxs-lookup"><span data-stu-id="6855c-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="6855c-118">Se você não puder esperar pela Olá mesmo nome toobe disponível, em seguida, restaure tooa novo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="6855c-119">Os serviços do BizTalk pode ser restaurado toohello mesma edição ou uma edição superior.</span><span class="sxs-lookup"><span data-stu-id="6855c-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="6855c-120">Restauração de Serviços BizTalk tooa edição inferior, quando foi feito o backup de hello, não há suporte.</span><span class="sxs-lookup"><span data-stu-id="6855c-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="6855c-121">Por exemplo, um backup usando Olá que edição Basic pode ser restaurado toohello edição Premium.</span><span class="sxs-lookup"><span data-stu-id="6855c-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="6855c-122">Um backup usando Olá que Premium Edition não pode ser restaurado toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="6855c-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="6855c-123">números de controle de EDI Olá backup toomaintain continuidade de números de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="6855c-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="6855c-124">Se as mensagens são processadas após o último backup de hello, restaurar o conteúdo de backup pode causar números de controle duplicados.</span><span class="sxs-lookup"><span data-stu-id="6855c-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="6855c-125">Se um lote de mensagens ativas processar em lotes de saudação **antes de** executar um backup.</span><span class="sxs-lookup"><span data-stu-id="6855c-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="6855c-126">Ao criar um backup (conforme necessário ou agendado), as mensagens em lotes nunca são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="6855c-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="6855c-127">**Se um backup for feito com mensagens ativas em um lote, o backup dessas mensagens não será feito e, portanto, elas serão perdidas.**</span><span class="sxs-lookup"><span data-stu-id="6855c-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="6855c-128">Opcional: Olá Portal de Serviços BizTalk, pare de quaisquer operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6855c-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="6855c-129">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-129">Create a backup</span></span>
<span data-ttu-id="6855c-130">Um backup pode ser obtido a qualquer momento e é totalmente controlado por você.</span><span class="sxs-lookup"><span data-stu-id="6855c-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="6855c-131">Esta seção lista os backups de toocreate etapas Olá Olá clássico do Azure usando o portal, incluindo:</span><span class="sxs-lookup"><span data-stu-id="6855c-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="6855c-132">Backup sob demanda</span><span class="sxs-lookup"><span data-stu-id="6855c-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="6855c-133">Agendar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="6855c-134"><a name="backupnow"></a>Backup sob demanda</span><span class="sxs-lookup"><span data-stu-id="6855c-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="6855c-135">No portal clássico do Azure do hello, selecione **Serviços BizTalk**, e, em seguida, selecione Olá BizTalk Service toobackup desejado.</span><span class="sxs-lookup"><span data-stu-id="6855c-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="6855c-136">Em Olá **painel** guia, selecione **backup** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="6855c-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="6855c-137">Insira um nome de backup.</span><span class="sxs-lookup"><span data-stu-id="6855c-137">Enter a backup name.</span></span> <span data-ttu-id="6855c-138">Por exemplo, digite *meuServiçoBizTalk*BU*Data*.</span><span class="sxs-lookup"><span data-stu-id="6855c-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="6855c-139">Escolha uma conta de armazenamento de blob e backup de Olá Olá selecione marca de seleção toostart.</span><span class="sxs-lookup"><span data-stu-id="6855c-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="6855c-140">Após a conclusão do backup hello, um contêiner com o nome do backup Olá que você inserir é criado na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="6855c-141">Esse contêiner contém a configuração de backup do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6855c-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="6855c-142"><a name="backupschedule"></a>Agendar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="6855c-143">No portal clássico do Azure do hello, selecione **Serviços BizTalk**, selecione Olá nome BizTalk Service deseja tooschedule Olá backup e, em seguida, selecione Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="6855c-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="6855c-144">Saudação de conjunto **Status de Backup** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="6855c-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="6855c-145">Selecione Olá **conta de armazenamento** toostore Olá backup, digite Olá **frequência** toocreate Olá backups e quanto tempo tookeep hello (**dias de retenção**):</span><span class="sxs-lookup"><span data-stu-id="6855c-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="6855c-146">**Observações**</span><span class="sxs-lookup"><span data-stu-id="6855c-146">**Notes**</span></span>     
   
   * <span data-ttu-id="6855c-147">Em **dias de retenção**, período de retenção Olá deve ser maior que a frequência de backup hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="6855c-148">Selecione **sempre manter pelo menos um backup**, mesmo se ele for após o período de retenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="6855c-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="6855c-149">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6855c-149">Select **Save**.</span></span>

<span data-ttu-id="6855c-150">Quando um trabalho de backup agendado é executado, ele cria um contêiner (dados de backup toostore) na conta de armazenamento Olá inserido.</span><span class="sxs-lookup"><span data-stu-id="6855c-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="6855c-151">nome de saudação do contêiner de saudação é nomeada *BizTalk Service nome-data-hora*.</span><span class="sxs-lookup"><span data-stu-id="6855c-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="6855c-152">Se Olá painel do BizTalk Service mostra um **falha** status:</span><span class="sxs-lookup"><span data-stu-id="6855c-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Último status do backup agendado][BackupStatus] 

<span data-ttu-id="6855c-154">Olá link abre o hello Logs de operação de serviços de gerenciamento toohelp solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="6855c-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="6855c-155">Consulte [Serviços BizTalk: solução de problemas usando logs de operação](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="6855c-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="6855c-156">Restaurar</span><span class="sxs-lookup"><span data-stu-id="6855c-156">Restore</span></span>
<span data-ttu-id="6855c-157">Você pode restaurar backups de saudação portal clássico do Azure ou de saudação [restaurar API de REST de Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="6855c-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="6855c-158">Esta seção lista Olá etapas toorestore usando o portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="6855c-159">Antes de restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-159">Before restoring a backup</span></span>
* <span data-ttu-id="6855c-160">Os novos armazenamentos de acompanhamento, arquivamento e monitoramento podem ser especificados durante a restauração de um Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6855c-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="6855c-161">Olá mesmos dados de tempo de execução de EDI são restaurados.</span><span class="sxs-lookup"><span data-stu-id="6855c-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="6855c-162">backup de tempo de execução de EDI Olá armazena números de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="6855c-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="6855c-163">Olá restaurado números de controle estão em sequência de tempo de saudação do backup hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="6855c-164">Se as mensagens são processadas após o último backup de hello, restaurar o conteúdo de backup pode causar números de controle duplicados.</span><span class="sxs-lookup"><span data-stu-id="6855c-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="6855c-165">Restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-165">Restore a backup</span></span>
1. <span data-ttu-id="6855c-166">No portal clássico do Azure do hello, selecione **novo** > **serviços de aplicativos** > **BizTalk Service** > **restaurar** :</span><span class="sxs-lookup"><span data-stu-id="6855c-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restaurar um backup][Restore]
2. <span data-ttu-id="6855c-168">Em **Backup URL**, selecione o ícone de pasta hello e expanda a conta de armazenamento do Azure Olá repositórios Olá backup de configuração do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="6855c-169">Expanda o contêiner de saudação e no painel direito da saudação, selecione Olá correspondente backup de arquivo. txt.</span><span class="sxs-lookup"><span data-stu-id="6855c-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="6855c-170">Selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="6855c-170">Select **Open**.</span></span>
3. <span data-ttu-id="6855c-171">Em Olá **serviço de restauração do BizTalk** , insira um **nome do serviço BizTalk** e verifique se Olá **URL do domínio**, **edição**e **Região** para Olá restaurado BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="6855c-172">**Criar uma nova instância de banco de dados SQL** para Olá banco de dados de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="6855c-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="6855c-173">Selecione a seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="6855c-174">Verificar Olá nome do banco de dados do SQL hello, insira o servidor físico hello, onde o banco de dados SQL Olá será criado e uma nome de usuário/senha para o servidor.</span><span class="sxs-lookup"><span data-stu-id="6855c-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="6855c-175">Se você desejar a edição de banco de dados SQL tooconfigure hello, tamanho e outras propriedades, selecione **definir configurações avançadas do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="6855c-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="6855c-176">Selecione a seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="6855c-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="6855c-177">Criar uma nova conta de armazenamento ou insira uma conta de armazenamento existente para Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="6855c-178">Selecione a restauração de Olá Olá marca de seleção toostart.</span><span class="sxs-lookup"><span data-stu-id="6855c-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="6855c-179">Depois que a restauração de saudação for concluído com êxito, um BizTalk Service novo é listado em um estado suspenso na página de Serviços BizTalk Olá no hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6855c-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="6855c-180"><a name="postrestore"></a>Depois de restaurar um backup</span><span class="sxs-lookup"><span data-stu-id="6855c-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="6855c-181">Olá BizTalk Service sempre é restaurado em um **suspenso** estado.</span><span class="sxs-lookup"><span data-stu-id="6855c-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="6855c-182">Nesse estado, você pode fazer alterações de configuração antes que o novo ambiente do hello está funcionando, incluindo:</span><span class="sxs-lookup"><span data-stu-id="6855c-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="6855c-183">Se você criar aplicativos do BizTalk Service usando Olá SDK dos Serviços BizTalk do Azure, talvez seja necessário credenciais de controle de acesso (ACS) Olá tootooupdate em toowork esses aplicativos com o ambiente de saudação restaurada.</span><span class="sxs-lookup"><span data-stu-id="6855c-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="6855c-184">Restaurar um tooreplicate BizTalk Service um ambiente existente do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="6855c-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="6855c-185">Nessa situação, se houver contratos configurados no portal de Serviços BizTalk original Olá que usam uma pasta de origem FTP, talvez seja necessário tooupdate contratos Olá Olá recém restaurado ambiente toouse uma pasta FTP de origem diferente.</span><span class="sxs-lookup"><span data-stu-id="6855c-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="6855c-186">Caso contrário, pode haver dois contratos diferentes tentar toopull Olá a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="6855c-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="6855c-187">Se você restaurou toohave vários ambientes de BizTalk Service, certifique-se de que ambiente correto de saudação em aplicativos do Visual Studio hello, cmdlets do PowerShell, APIs REST ou APIs de OM de gerenciamento de parceiros comerciais de destino.</span><span class="sxs-lookup"><span data-stu-id="6855c-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="6855c-188">É um backup de tooconfigure automatizada prática recomendada no ambiente do serviço BizTalk Olá recentemente restaurado.</span><span class="sxs-lookup"><span data-stu-id="6855c-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="6855c-189">Olá toostart BizTalk Service em Olá portal clássico do Azure, selecione Olá restaurado BizTalk Service e selecione **retomar** na barra de tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="6855c-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="6855c-190">Do que é feito backup</span><span class="sxs-lookup"><span data-stu-id="6855c-190">What gets backed up</span></span>
<span data-ttu-id="6855c-191">Quando um backup é criado, hello itens a seguir são feitos:</span><span class="sxs-lookup"><span data-stu-id="6855c-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="6855c-192">Itens do backup</span><span class="sxs-lookup"><span data-stu-id="6855c-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="6855c-193">
 <strong>Portal de Serviços BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="6855c-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="6855c-194">Configuração e tempo de execução</span><span class="sxs-lookup"><span data-stu-id="6855c-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="6855c-195">Detalhes e perfil do parceiro</span><span class="sxs-lookup"><span data-stu-id="6855c-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="6855c-196">Contratos de parceiro</span><span class="sxs-lookup"><span data-stu-id="6855c-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="6855c-197">Assemblies personalizados implantados</span><span class="sxs-lookup"><span data-stu-id="6855c-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="6855c-198">Pontes implantadas</span><span class="sxs-lookup"><span data-stu-id="6855c-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="6855c-199">Certificados</span><span class="sxs-lookup"><span data-stu-id="6855c-199">Certificates</span></span></li>
<li><span data-ttu-id="6855c-200">Transformações implantadas</span><span class="sxs-lookup"><span data-stu-id="6855c-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="6855c-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="6855c-201">Pipelines</span></span></li>
<li><span data-ttu-id="6855c-202">Modelos criados e salvos em Olá Portal de Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="6855c-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="6855c-203">Mapeamentos de X12 ST01 e GS01</span><span class="sxs-lookup"><span data-stu-id="6855c-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="6855c-204">Números de controle (EDI)</span><span class="sxs-lookup"><span data-stu-id="6855c-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="6855c-205">Valores de MIC de mensagens AS2</span><span class="sxs-lookup"><span data-stu-id="6855c-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="6855c-206">
 <strong>Serviço BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="6855c-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="6855c-207">Certificado SSL</span><span class="sxs-lookup"><span data-stu-id="6855c-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="6855c-208">Dados do certificado SSL</span><span class="sxs-lookup"><span data-stu-id="6855c-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="6855c-209">Senha do certificado SSL</span><span class="sxs-lookup"><span data-stu-id="6855c-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="6855c-210">Configurações do Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="6855c-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="6855c-211">Contagem de unidades da escala</span><span class="sxs-lookup"><span data-stu-id="6855c-211">Scale unit count</span></span></li>
<li><span data-ttu-id="6855c-212">Edição</span><span class="sxs-lookup"><span data-stu-id="6855c-212">Edition</span></span></li>
<li><span data-ttu-id="6855c-213">Versão do produto</span><span class="sxs-lookup"><span data-stu-id="6855c-213">Product Version</span></span></li>
<li><span data-ttu-id="6855c-214">Região/Datacenter</span><span class="sxs-lookup"><span data-stu-id="6855c-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="6855c-215">O namespace e a chave do ACS (Serviço de Controle de Acesso)</span><span class="sxs-lookup"><span data-stu-id="6855c-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="6855c-216">Cadeia de conexão do banco de dados de acompanhamento</span><span class="sxs-lookup"><span data-stu-id="6855c-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="6855c-217">Cadeia de conexão da conta de armazenamento de arquivamento</span><span class="sxs-lookup"><span data-stu-id="6855c-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="6855c-218">Cadeia de conexão da conta de armazenamento de monitoramento</span><span class="sxs-lookup"><span data-stu-id="6855c-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="6855c-219">
 <strong>Itens Adicionais</strong></span><span class="sxs-lookup"><span data-stu-id="6855c-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="6855c-220">Banco de Dados de Acompanhamento</span><span class="sxs-lookup"><span data-stu-id="6855c-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="6855c-221">Quando Olá BizTalk Service é criado, detalhes do banco de dados de rastreamento de saudação são inseridos, incluindo hello servidor de banco de dados do SQL Azure e o nome de banco de dados de rastreamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="6855c-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="6855c-222">Olá banco de dados de rastreamento não é automaticamente backup.</span><span class="sxs-lookup"><span data-stu-id="6855c-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="6855c-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="6855c-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="6855c-224">Se Olá banco de dados de rastreamento é excluído e Olá necessidades de banco de dados recuperadas, deve existir um backup anterior.</span><span class="sxs-lookup"><span data-stu-id="6855c-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="6855c-225">Se não existir um backup, a saudação banco de dados de controle e seus dados não são recuperáveis.</span><span class="sxs-lookup"><span data-stu-id="6855c-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="6855c-226">Nessa situação, crie um novo banco de dados de rastreamento com hello mesmo nome de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6855c-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="6855c-227">A Replicação Geográfica é recomendada.</span><span class="sxs-lookup"><span data-stu-id="6855c-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="6855c-228">Avançar</span><span class="sxs-lookup"><span data-stu-id="6855c-228">Next</span></span>
<span data-ttu-id="6855c-229">Serviços de BizTalk do Azure toocreate em hello Azure clássico, acesse muito[Serviços BizTalk: provisionamento usando o portal do Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="6855c-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="6855c-230">toostart criação de aplicativos, vá muito[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="6855c-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="6855c-231">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6855c-231">See Also</span></span>
* [<span data-ttu-id="6855c-232">Fazer o backup do Serviço BizTalk</span><span class="sxs-lookup"><span data-stu-id="6855c-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="6855c-233">Restaurar o Serviço BizTalk do backup</span><span class="sxs-lookup"><span data-stu-id="6855c-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="6855c-234">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="6855c-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="6855c-235">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6855c-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="6855c-236">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="6855c-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="6855c-237">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="6855c-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="6855c-238">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="6855c-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="6855c-239">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="6855c-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="6855c-240">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="6855c-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

