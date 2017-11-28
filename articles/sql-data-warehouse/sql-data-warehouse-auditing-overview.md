---
title: aaaAuditing no Azure SQL Data Warehouse | Microsoft Docs
description: "Introdução à auditoria no SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="7b8f6-103">Auditoria no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7b8f6-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b8f6-104">Auditoria</span><span class="sxs-lookup"><span data-stu-id="7b8f6-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="7b8f6-105">Detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="7b8f6-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="7b8f6-106">Auditoria do SQL Data Warehouse permite toorecord eventos no log de auditoria de banco de dados tooan em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="7b8f6-107">A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="7b8f6-108">A auditoria do SQL Data Warehouse também se integra ao Microsoft Power BI para relatórios e análises de buscas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="7b8f6-109">Ferramentas de auditoria habilitar e facilitar os padrões toocompliance aderência mas não garantem a conformidade.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="7b8f6-110">Para obter mais informações sobre o Azure programas que conformidade com padrões de suporte, consulte Olá <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="7b8f6-111">[Fundamentos da Auditoria do Banco de Dados]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="7b8f6-112">[Configurar a auditoria do banco de dados]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="7b8f6-113">[Analisar os logs e relatórios de auditoria]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="7b8f6-114"><a id="subheading-1"></a>Fundamentos da Auditoria do Banco de Dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f6-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="7b8f6-115">A auditoria do banco de dados do SQL Data Warehouse permite que você:</span><span class="sxs-lookup"><span data-stu-id="7b8f6-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="7b8f6-116">**Retenha** uma trilha de auditoria dos eventos selecionados.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="7b8f6-117">Você pode definir categorias de banco de dados ações toobe auditado.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="7b8f6-118">**Relate** sobre a atividade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-118">**Report** on database activity.</span></span> <span data-ttu-id="7b8f6-119">Você pode usar relatórios pré-configurados e um tooget painel iniciada rapidamente com a atividade e o relatório de eventos.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="7b8f6-120">**Analise** relatórios.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-120">**Analyze** reports.</span></span> <span data-ttu-id="7b8f6-121">Encontrar eventos suspeitos, atividades incomuns e tendências.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="7b8f6-122">Você pode configurar a auditoria de saudação categorias de evento a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b8f6-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="7b8f6-123">**SQL simples** e **SQL parametrizadas** para qual Olá logs de auditoria coletados são classificados como</span><span class="sxs-lookup"><span data-stu-id="7b8f6-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="7b8f6-124">**Toodata de acesso**</span><span class="sxs-lookup"><span data-stu-id="7b8f6-124">**Access toodata**</span></span>
* <span data-ttu-id="7b8f6-125">**Alterações de esquema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="7b8f6-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="7b8f6-126">**Alterações de dados (DML)**</span><span class="sxs-lookup"><span data-stu-id="7b8f6-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="7b8f6-127">**Contas, funções e permissões (DCL)**</span><span class="sxs-lookup"><span data-stu-id="7b8f6-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="7b8f6-128">**Procedimento armazenado**, **Logon** e **Gerenciamento de transações**.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="7b8f6-129">Para cada categoria de evento, as operações de auditoria de **sucesso** e **falha** são configuradas separadamente.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="7b8f6-130">Para obter mais informações sobre atividades hello e eventos de auditoria, consulte Olá <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referência de formato de Log de auditoria (download do arquivo doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="7b8f6-131">Logs de auditoria são armazenados na sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="7b8f6-132">Você pode definir um período de retenção para logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="7b8f6-133">Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão do servidor.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="7b8f6-134">Uma política de auditoria de servidor padrão se aplica a bancos de dados tooall em um servidor, que não têm uma substituição de banco de dados auditoria política específica definida.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="7b8f6-135">Antes de configurar a auditoria, verifique se você está usando um ["Cliente de nível inferior"](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f6-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="7b8f6-136"><a id="subheading-2"></a>Configurar a auditoria do banco de dados</span><span class="sxs-lookup"><span data-stu-id="7b8f6-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="7b8f6-137">Iniciar Olá <a href="https://portal.azure.com" target="_blank">portal do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="7b8f6-138">Vá toohello **configurações** folha de saudação SQL Data Warehouse, você deseja tooaudit.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="7b8f6-139">Em Olá **configurações** folha, selecione **detecção de auditoria e ameaças**.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="7b8f6-140">Em seguida, habilitar a auditoria clicando Olá **ON** botão.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="7b8f6-141">No hello folha de configuração de auditoria, selecione **detalhes armazenamento** tooopen folha de armazenamento de Logs de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="7b8f6-142">Selecione Olá conta de armazenamento do Azure onde os logs serão salvas e hello período de retenção.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="7b8f6-143">Olá Use pré-configurado de mesma conta de armazenamento para todos os Olá de tooget auditados bancos de dados máximo Olá relatórios de modelos.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="7b8f6-144">Clique em Olá **Okey** configuração detalhes de armazenamento de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="7b8f6-145">Em **registro em log pelo evento**, clique em **êxito** e **falha** toolog todos os eventos, ou escolha categorias de evento individuais.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="7b8f6-146">Se você estiver configurando a auditoria para um banco de dados, talvez seja necessário cadeia de caracteres de conexão Olá de tooalter de sua tooensure cliente dados de auditoria é capturado corretamente.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="7b8f6-147">Verificar Olá [modificar o FQDN do servidor na cadeia de caracteres de conexão Olá](sql-data-warehouse-auditing-downlevel-clients.md) tópico para conexões de cliente de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="7b8f6-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-148">Click **OK**.</span></span>

## <span data-ttu-id="7b8f6-149"><a id="subheading-3"></a>Analisar os logs e relatórios de auditoria</span><span class="sxs-lookup"><span data-stu-id="7b8f6-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="7b8f6-150">Logs de auditoria são agregados em uma coleção de tabelas de armazenamento com uma **SQLDBAuditLogs** prefixo no hello escolhido durante a instalação de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="7b8f6-151">Você pode ver os arquivos de log usando uma ferramenta como o <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Gerenciador de Armazenamento do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="7b8f6-152">Um modelo de relatório do painel pré-configurado está disponível como um <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">planilha do Excel para download</a> toohelp você analisar rapidamente os dados de log.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="7b8f6-153">modelo de saudação toouse em seus logs de auditoria, você precisa Excel 2013 ou posterior e o Power Query, que você pode baixar <a href="http://www.microsoft.com/download/details.aspx?id=39379">aqui</a>.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="7b8f6-154">Olá possui dados de exemplo fictício nele, e você pode configurar tooimport Power Query seu log de auditoria diretamente de sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="7b8f6-155"><a id="subheading-4"></a>Regeneração de chave de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7b8f6-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="7b8f6-156">Em produção, você está provavelmente toorefresh o armazenamento de chaves periodicamente.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="7b8f6-157">Ao atualizar as chaves, é necessário toosave política de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="7b8f6-158">processo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7b8f6-158">hello process is as follows:</span></span>

1. <span data-ttu-id="7b8f6-159">No hello auditoria folha de configuração (instalação Olá auditoria seção descrita acima), alterne Olá **chave de acesso de armazenamento** de *primário* muito*secundário* e  **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="7b8f6-160">Folha de configuração de armazenamento vá toohello e **regenerar** Olá *chave de acesso primário*.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="7b8f6-161">Voltar toohello auditoria folha de configuração de comutador hello **chave de acesso de armazenamento** de *secundário* muito*primário* e pressione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="7b8f6-162">Voltar toohello armazenamento da interface do usuário e **regenerar** Olá *chave de acesso secundária* (como preparação para Olá chaves próximas ciclo de atualização.</span><span class="sxs-lookup"><span data-stu-id="7b8f6-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="7b8f6-163"><a id="subheading-5"></a>Automação (PowerShell/API REST)</span><span class="sxs-lookup"><span data-stu-id="7b8f6-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="7b8f6-164">Você também pode configurar a auditoria no Azure SQL Data Warehouse usando Olá ferramentas de automação a seguir:</span><span class="sxs-lookup"><span data-stu-id="7b8f6-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="7b8f6-165">**Cmdlets do PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="7b8f6-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="7b8f6-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="7b8f6-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="7b8f6-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="7b8f6-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="7b8f6-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="7b8f6-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="7b8f6-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="7b8f6-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Fundamentos da Auditoria do Banco de Dados]: #subheading-1
[Configurar a auditoria do banco de dados]: #subheading-2
[Analisar os logs e relatórios de auditoria]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy