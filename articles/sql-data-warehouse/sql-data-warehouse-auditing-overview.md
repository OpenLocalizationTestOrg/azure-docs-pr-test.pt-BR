---
title: Auditoria no SQL Data Warehouse do Azure | Microsoft Docs
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
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="490aa-103">Auditoria no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="490aa-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="490aa-104">Auditoria</span><span class="sxs-lookup"><span data-stu-id="490aa-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="490aa-105">Detecção de ameaças</span><span class="sxs-lookup"><span data-stu-id="490aa-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="490aa-106">A auditoria do SQL Data Warehouse permite registrar eventos no banco de dados em um log de auditoria na sua Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="490aa-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="490aa-107">A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="490aa-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="490aa-108">A auditoria do SQL Data Warehouse também se integra ao Microsoft Power BI para relatórios e análises de buscas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="490aa-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="490aa-109">As ferramentas de auditoria permitem e facilitam a adoção de padrões de conformidade, mas não garantem a conformidade.</span><span class="sxs-lookup"><span data-stu-id="490aa-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="490aa-110">Para obter mais informações sobre os programas Azure que oferecem suporte à conformidade com os padrões, consulte a <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Central de Confiabilidade do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="490aa-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="490aa-111">[Fundamentos da Auditoria do Banco de Dados]</span><span class="sxs-lookup"><span data-stu-id="490aa-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="490aa-112">[Configurar a auditoria do banco de dados]</span><span class="sxs-lookup"><span data-stu-id="490aa-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="490aa-113">[Analisar os logs e relatórios de auditoria]</span><span class="sxs-lookup"><span data-stu-id="490aa-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="490aa-114"><a id="subheading-1"></a>Fundamentos da Auditoria do Banco de Dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="490aa-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="490aa-115">A auditoria do banco de dados do SQL Data Warehouse permite que você:</span><span class="sxs-lookup"><span data-stu-id="490aa-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="490aa-116">**Retenha** uma trilha de auditoria dos eventos selecionados.</span><span class="sxs-lookup"><span data-stu-id="490aa-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="490aa-117">Definir categorias de ações de banco de dados a ser auditadas.</span><span class="sxs-lookup"><span data-stu-id="490aa-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="490aa-118">**Relate** sobre a atividade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="490aa-118">**Report** on database activity.</span></span> <span data-ttu-id="490aa-119">Utilizar relatórios pré-configurados e um painel para iniciar rapidamente um relatório de atividades e eventos.</span><span class="sxs-lookup"><span data-stu-id="490aa-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="490aa-120">**Analise** relatórios.</span><span class="sxs-lookup"><span data-stu-id="490aa-120">**Analyze** reports.</span></span> <span data-ttu-id="490aa-121">Encontrar eventos suspeitos, atividades incomuns e tendências.</span><span class="sxs-lookup"><span data-stu-id="490aa-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="490aa-122">Você pode configurar a auditoria para as categorias de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="490aa-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="490aa-123">**SQL simples** e **SQL parametrizado** para os quais os logs de auditoria coletados são classificados como</span><span class="sxs-lookup"><span data-stu-id="490aa-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="490aa-124">**Acesso a dados**</span><span class="sxs-lookup"><span data-stu-id="490aa-124">**Access to data**</span></span>
* <span data-ttu-id="490aa-125">**Alterações de esquema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="490aa-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="490aa-126">**Alterações de dados (DML)**</span><span class="sxs-lookup"><span data-stu-id="490aa-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="490aa-127">**Contas, funções e permissões (DCL)**</span><span class="sxs-lookup"><span data-stu-id="490aa-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="490aa-128">**Procedimento armazenado**, **Logon** e **Gerenciamento de transações**.</span><span class="sxs-lookup"><span data-stu-id="490aa-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="490aa-129">Para cada categoria de evento, as operações de auditoria de **sucesso** e **falha** são configuradas separadamente.</span><span class="sxs-lookup"><span data-stu-id="490aa-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="490aa-130">Para obter mais informações sobre as atividades e os eventos auditados, consulte a <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Referência de Formato de Log de Auditoria (download do arquivo .doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="490aa-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="490aa-131">Logs de auditoria são armazenados na sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="490aa-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="490aa-132">Você pode definir um período de retenção para logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="490aa-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="490aa-133">Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão do servidor.</span><span class="sxs-lookup"><span data-stu-id="490aa-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="490aa-134">Uma política de auditoria padrão do servidor é aplicada a todos os bancos de dados em um servidor que não contém uma política de auditoria de banco de dados substituta específica definida.</span><span class="sxs-lookup"><span data-stu-id="490aa-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="490aa-135">Antes de configurar a auditoria, verifique se você está usando um ["Cliente de nível inferior"](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="490aa-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="490aa-136"><a id="subheading-2"></a>Configurar a auditoria do banco de dados</span><span class="sxs-lookup"><span data-stu-id="490aa-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="490aa-137">Inicie o <a href="https://portal.azure.com" target="_blank">Portal do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="490aa-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="490aa-138">Acesse a folha **Configurações** do SQL Data Warehouse que deseja auditar.</span><span class="sxs-lookup"><span data-stu-id="490aa-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="490aa-139">Na folha **Configurações**, selecione **Auditoria e Detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="490aa-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="490aa-140">Em seguida, habilite a auditoria clicando no botão **ON** .</span><span class="sxs-lookup"><span data-stu-id="490aa-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="490aa-141">Na folha de configuração de auditoria, selecione **DETALHES DE ARMAZENAMENTO** para abrir a folha Armazenamento de Logs de Auditoria.</span><span class="sxs-lookup"><span data-stu-id="490aa-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="490aa-142">Selecione a conta de armazenamento do Azure na qual os logs serão salvos e o período de retenção.</span><span class="sxs-lookup"><span data-stu-id="490aa-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="490aa-143">Use a mesma conta de armazenamento para todos os bancos de dados auditados para aproveitar ao máximo os modelos de relatórios pré-configurados.</span><span class="sxs-lookup"><span data-stu-id="490aa-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="490aa-144">Clique no botão **OK** para salvar a configuração de detalhes do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="490aa-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="490aa-145">Em **REGISTRO EM LOG POR EVENTO**, clique em **SUCESSO** e **FALHA** para registrar todos os eventos ou escolha categorias de evento individuais.</span><span class="sxs-lookup"><span data-stu-id="490aa-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="490aa-146">Se você estiver configurando a Auditoria para um banco de dados, talvez seja necessário alterar a cadeia de conexão do cliente para garantir que os dados de auditoria sejam capturados corretamente.</span><span class="sxs-lookup"><span data-stu-id="490aa-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="490aa-147">Verifique o tópico [Modificar o FQDN do servidor na cadeia de conexão](sql-data-warehouse-auditing-downlevel-clients.md) para conexões de cliente de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="490aa-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="490aa-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="490aa-148">Click **OK**.</span></span>

## <span data-ttu-id="490aa-149"><a id="subheading-3"></a>Analisar os logs e relatórios de auditoria</span><span class="sxs-lookup"><span data-stu-id="490aa-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="490aa-150">Logs de auditoria são agregados em uma coleção de tabelas de armazenamento com um prefixo **SQLDBAuditLogs** na conta de armazenamento do Azure que você escolheu durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="490aa-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="490aa-151">Você pode ver os arquivos de log usando uma ferramenta como o <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Gerenciador de Armazenamento do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="490aa-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="490aa-152">Um modelo de relatório do painel pré-configurado está disponível como uma planilha do <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">Excel para download</a> para ajudar você a analisar rapidamente os dados de log.</span><span class="sxs-lookup"><span data-stu-id="490aa-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="490aa-153">Para utilizar o modelo em seus logs de auditoria, você precisará do Excel 2013 ou mais recente e do Power Query, que pode ser baixado <a href="http://www.microsoft.com/download/details.aspx?id=39379">aqui</a>.</span><span class="sxs-lookup"><span data-stu-id="490aa-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="490aa-154">O modelo possui dados de amostra fictícios, e você pode configurar o Power Query para importar seu log de auditoria diretamente da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="490aa-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="490aa-155"><a id="subheading-4"></a>Regeneração de chave de armazenamento</span><span class="sxs-lookup"><span data-stu-id="490aa-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="490aa-156">Em produção, você provavelmente atualizará suas chaves de armazenamento periodicamente.</span><span class="sxs-lookup"><span data-stu-id="490aa-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="490aa-157">Ao atualizar suas chaves, é necessário salvar a política.</span><span class="sxs-lookup"><span data-stu-id="490aa-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="490aa-158">O processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="490aa-158">The process is as follows:</span></span>

1. <span data-ttu-id="490aa-159">Na folha de configuração de auditoria (descrita acima na seção de configuração de auditoria), altere a **Chave de Acesso de Armazenamento** de *Primária* para *Secundária* e clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="490aa-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="490aa-160">Acesse a folha de configuração de armazenamento e **regenere** a *Chave de Acesso Primária*.</span><span class="sxs-lookup"><span data-stu-id="490aa-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="490aa-161">Volte para a folha de configuração de auditoria, altere a **Chave de Acesso de Armazenamento** de *Secundária* para *Primária* e pressione **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="490aa-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="490aa-162">Volte para a interface do usuário de armazenamento e **regenere** a *Chave de Acesso Secundária* (como preparação para o próximo ciclo de atualização de chaves.</span><span class="sxs-lookup"><span data-stu-id="490aa-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="490aa-163"><a id="subheading-5"></a>Automação (PowerShell/API REST)</span><span class="sxs-lookup"><span data-stu-id="490aa-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="490aa-164">Você também pode configurar a auditoria no SQL Data Warehouse do Azure usando as seguintes ferramentas de automação:</span><span class="sxs-lookup"><span data-stu-id="490aa-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="490aa-165">**Cmdlets do PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="490aa-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="490aa-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="490aa-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="490aa-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="490aa-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="490aa-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="490aa-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="490aa-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="490aa-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="490aa-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="490aa-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="490aa-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="490aa-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="490aa-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="490aa-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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