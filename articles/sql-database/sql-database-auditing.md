---
title: aaaGet iniciado com a auditoria de banco de dados SQL do Azure | Microsoft Docs
description: "Introdução à auditoria do banco de dados SQL do Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="5dbd3-103">Introdução à auditoria do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5dbd3-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="5dbd3-104">Auditoria de banco de dados SQL Azure rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="5dbd3-105">A auditoria também:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-105">Auditing also:</span></span>

* <span data-ttu-id="5dbd3-106">Ajuda você a manter a conformidade regulatória, entender a atividade do banco de dados e obter informações sobre discrepâncias e anomalias que podem indicar preocupações para os negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="5dbd3-107">Habilita e facilita a padrões de toocompliance aderência, embora ela não garante conformidade.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="5dbd3-108">Para obter mais informações sobre o Azure programas que conformidade com padrões de suporte, consulte Olá [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="5dbd3-109"><a id="subheading-1"></a>Visão geral da auditoria do banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="5dbd3-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="5dbd3-110">É possível usar a auditoria do banco de dados SQL para:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="5dbd3-111">**Retenha** uma trilha de auditoria dos eventos selecionados.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="5dbd3-112">Você pode definir categorias de banco de dados ações toobe auditado.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="5dbd3-113">**Relate** sobre a atividade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-113">**Report** on database activity.</span></span> <span data-ttu-id="5dbd3-114">Você pode usar relatórios pré-configurados e um tooget painel iniciada rapidamente com a atividade e o relatório de eventos.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="5dbd3-115">**Analise** relatórios.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-115">**Analyze** reports.</span></span> <span data-ttu-id="5dbd3-116">Encontrar eventos suspeitos, atividades incomuns e tendências.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="5dbd3-117">Você pode configurar a auditoria para diferentes tipos de categorias de evento, conforme explicado em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="5dbd3-118">Logs de auditoria são gravados tooAzure armazenamento de Blob em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="5dbd3-119"><a id="subheading-8"></a>Definir a política de auditoria no nível do servidor versus no nível do banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dbd3-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="5dbd3-120">Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão de servidor:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="5dbd3-121">Uma política de servidor se aplica a tooall existente e bancos de dados recém-criado no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="5dbd3-122">Se *auditoria de blob do servidor é habilitada*, ele *sempre aplica-se o banco de dados toohello* (ou seja, banco de dados hello será auditado), independentemente do banco de dados de saudação configurações de auditoria.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="5dbd3-123">Habilitar a auditoria no banco de dados do hello em adição tooenabling-lo no servidor de saudação do blob será *não* substituir ou alterar qualquer uma das configurações de saudação de auditoria de blob do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="5dbd3-124">Ambas as auditorias existirão lado a lado.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-124">Both audits will exist side by side.</span></span> <span data-ttu-id="5dbd3-125">Em outras palavras, o banco de dados de saudação será auditado duas vezes em paralelo (uma vez pela política do servidor de saudação e uma vez pela política de banco de dados de saudação).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="5dbd3-126">Evite habilitar a auditoria de blobs de servidor e a auditoria de blobs do banco de dados juntas, a menos que:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="5dbd3-127">Você deseja toouse outro *conta de armazenamento* ou *período de retenção* para um banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="5dbd3-128">Você deseja tooaudit tipos de evento ou categorias para um banco de dados que são diferentes dos tipos de eventos ou as categorias que estão sendo auditadas restante de saudação de bancos de dados Olá no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="5dbd3-129">Por exemplo, você pode ter inserções de tabela que precisa toobe auditada somente para um banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="5dbd3-130">Caso contrário, é recomendável que você habilite a auditoria de nível de servidor apenas blob e deixe Olá nível de banco de dados auditoria desabilitada para todos os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="5dbd3-131"><a id="subheading-2"></a>Configurar a auditoria do banco de dados</span><span class="sxs-lookup"><span data-stu-id="5dbd3-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="5dbd3-132">Olá, seção a seguir descreve configuração Olá de auditoria usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="5dbd3-133">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5dbd3-134">Vá toohello **configurações** folha de saudação do banco de dados/SQL server SQL você deseja tooaudit.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="5dbd3-135">Em Olá **configurações** folha, selecione **detecção de auditoria e ameaças**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="5dbd3-136"><a id="auditing-screenshot"></a> ![Painel de navegação][1]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="5dbd3-137">Se você preferir tooset uma política de auditoria de servidor (que será aplicada tooall existente e bancos de dados recém-criado neste servidor), você pode selecionar Olá **exibir configurações de servidor** link na folha de auditoria de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="5dbd3-138">Você pode exibir ou modificar as configurações de auditoria de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-138">You can then view or modify hello server auditing settings.</span></span>

    ![Painel de navegação][2]
4. <span data-ttu-id="5dbd3-140">Se você preferir tooenable blob auditoria no nível de banco de dados de saudação (em adição tooor em vez de auditoria de nível de servidor), para **auditoria**, selecione **ON**e para **auditoria tipo** , selecione **Blob**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="5dbd3-141">Se o servidor blob auditoria estiver habilitada, a auditoria de banco de dados configurado de saudação existirá lado a lado com a auditoria de blob do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Painel de navegação][3]
5. <span data-ttu-id="5dbd3-143">Olá tooopen **armazenamento de Logs de auditoria** folha, selecione **detalhes de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="5dbd3-144">Selecione a conta de armazenamento do Azure Olá onde os logs serão salvas e, em seguida, selecione o período de retenção hello, após o qual Olá logs antigos serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="5dbd3-145">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="5dbd3-146">Olá tooget máximo de modelos de relatórios auditoria hello, use Olá a mesma conta de armazenamento para todos os bancos de dados auditados.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="5dbd3-147"><a id="storage-screenshot"></a> ![Painel de navegação][4]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="5dbd3-148">Se você quiser toocustomize eventos de saudação auditado, você pode fazer isso por meio do PowerShell ou Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="5dbd3-149">Para obter mais detalhes, consulte Olá [automação (API REST/PowerShell)](#subheading-7) seção.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="5dbd3-150">Depois de configurar as configurações de auditoria, você pode ativar o novo recurso de detecção de ameaças hello e configurar alertas de segurança de tooreceive de emails.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="5dbd3-151">Ao usar a detecção de ameaças, você recebe alertas proativos sobre atividades anômalas do banco de dados que podem indicar possíveis ameaças à segurança.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="5dbd3-152">Para obter mais detalhes, consulte [Introdução à detecção de ameaças](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="5dbd3-153">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-153">Click **Save**.</span></span>





## <span data-ttu-id="5dbd3-154"><a id="subheading-3"></a>Analisar os logs e relatórios de auditoria</span><span class="sxs-lookup"><span data-stu-id="5dbd3-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="5dbd3-155">Logs de auditoria são agregados no hello escolhido durante a instalação de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="5dbd3-156">Explore os logs de auditoria usando uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="5dbd3-157">Os logs de auditoria de blob são salvos como uma coleção de arquivos de blob em um contêiner chamado **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="5dbd3-158">Para obter mais detalhes sobre a hierarquia de saudação da pasta de armazenamento de logs de auditoria de blob hello, convenções de nomenclatura de blob e formato de log, consulte Olá [Blob Audit Log formato referência (download do arquivo. docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="5dbd3-159">Há vários métodos que você pode usar o blob tooview logs de auditoria:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="5dbd3-160">Saudação de uso [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="5dbd3-161">Banco de dados relevante Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-161">Open hello relevant database.</span></span> <span data-ttu-id="5dbd3-162">AT Olá superior do banco de dados Olá **detecção de auditoria e ameaças** folha, clique em **exibir logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Painel de navegação][7]

    <span data-ttu-id="5dbd3-164">Um **registros de auditoria** abre folha, do qual você será capaz de tooview Olá logs.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="5dbd3-165">Você pode exibir datas específicas clicando **filtro** na parte superior de saudação do hello **registros de auditoria** folha.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="5dbd3-166">Alterne entre os registros de auditoria que foram criados por uma auditoria da política de servidor ou da política de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Painel de navegação][8]

* <span data-ttu-id="5dbd3-168">Use a função de sistema hello **sys. fn_get_audit_file** dados de log de auditoria (T-SQL) tooreturn Olá em formato tabular.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="5dbd3-169">Para obter mais informações sobre como usar essa função, consulte Olá [documentação de sys. fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="5dbd3-170">Use a opção **Mesclar Arquivos de Auditoria** no SQL Server Management Studio (a partir do SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="5dbd3-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="5dbd3-171">No menu do SSMS hello, selecione **arquivo** > **abrir** > **mesclar arquivos de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Painel de navegação][9]
    2. <span data-ttu-id="5dbd3-173">Olá **adicionar arquivos de auditoria** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="5dbd3-174">Selecione uma saudação **adicionar** opções se auditoria toomerge arquivos de um local de disco ou importá-los do armazenamento do Azure (será necessário tooprovide seus detalhes de armazenamento do Azure e a chave de conta).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="5dbd3-175">Depois de toomerge de todos os arquivos foram adicionados, clique em **Okey** toocomplete operação de mesclagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="5dbd3-176">arquivo mesclado Olá abre no SSMS, onde você pode exibir e analisá-lo, bem como a exportação-tooan XEL ou CSV arquivo ou tooa tabela.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="5dbd3-177">Saudação de uso [sincronizar aplicativo](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que você criou.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="5dbd3-178">Ele é executado no Azure e utiliza a análise de Log do Operations Management Suite (OMS) pública APIs toopush SQL logs de auditoria ao OMS.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="5dbd3-179">aplicativo de sincronização Hello envia logs de auditoria do SQL em análise de logs do OMS para consumo por meio do painel de análise de logs do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="5dbd3-180">Use o Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-180">Use Power BI.</span></span> <span data-ttu-id="5dbd3-181">Você pode exibir e analisar dados do log de auditoria no Power BI.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="5dbd3-182">Saiba mais sobre o [Power BI e acesse um modelo para download](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="5dbd3-183">Baixar arquivos de log do seu contêiner de blob de armazenamento do Azure por meio do portal hello, ou usando uma ferramenta como [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="5dbd3-184">Depois de baixar um arquivo de log localmente, você pode clicar duas vezes tooopen do arquivo hello, exibir e analisar logs Olá no SSMS.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="5dbd3-185">Baixe também vários arquivos simultaneamente por meio do Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="5dbd3-186">Clique em uma subpasta específica (por exemplo, uma subpasta que inclui todos os arquivos de log para uma data específica) e selecione **Salvar como** toosave em uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="5dbd3-187">Métodos adicionais:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-187">Additional methods:</span></span>
   * <span data-ttu-id="5dbd3-188">Depois de baixar vários arquivos (ou em uma subpasta que inclui arquivos de log para um dia inteiro, conforme descrito no item anterior Olá nesta lista), você pode mesclá-los localmente conforme descrito nas instruções de arquivos de auditoria de mesclagem do SSMS Olá descritas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="5dbd3-189">Exiba os logs de auditoria de blob de forma programática:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="5dbd3-190">Saudação de uso [leitor de eventos estendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteca C#.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="5dbd3-191">[Consulte Arquivos de Eventos Estendidos usando o PowerShell](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="5dbd3-192"><a id="subheading-5"></a>Práticas de produção</span><span class="sxs-lookup"><span data-stu-id="5dbd3-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="5dbd3-193"><a id="subheading-6">Auditoria de bancos de dados replicados geograficamente</a></span><span class="sxs-lookup"><span data-stu-id="5dbd3-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="5dbd3-194">Quando você usa os bancos de dados replicada geograficamente, é possível tooset a auditoria no banco de dados primário Olá, banco de dados secundário hello ou ambos, dependendo do tipo de auditoria de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="5dbd3-195">Siga estas instruções (Lembre-se de que a auditoria de blob pode ser ativada ou desativada somente de banco de dados primário Olá configurações de auditoria):</span><span class="sxs-lookup"><span data-stu-id="5dbd3-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="5dbd3-196">**Banco de dados primário**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-196">**Primary database**.</span></span> <span data-ttu-id="5dbd3-197">Ativar a auditoria de blob, no servidor de saudação ou Olá próprio banco de dados, conforme descrito em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="5dbd3-198">**Banco de dados secundário**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-198">**Secondary database**.</span></span> <span data-ttu-id="5dbd3-199">Ativar a auditoria de blob no banco de dados primário hello, conforme descrito em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="5dbd3-200">Auditoria de blob deve ser habilitada nos Olá *banco de dados primário em si*, não o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="5dbd3-201">Depois que a auditoria de blob estiver habilitada no banco de dados primário hello, ele também será habilitado no banco de dados secundário hello.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="5dbd3-202">Por padrão, as configurações de armazenamento Olá para o banco de dados secundário Olá será idêntico toothose do banco de dados primário Olá, fazendo com que o tráfego entre regional.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="5dbd3-203">Você pode evitar isso, permitindo a auditoria de blob no servidor secundário hello e configurar o armazenamento local nas configurações de armazenamento do servidor secundário Olá.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="5dbd3-204">Isso substituirá o local de armazenamento de saudação para o banco de dados secundário hello e resultam em cada banco de dados salvando seu armazenamento de toolocal de logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="5dbd3-205"><a id="subheading-6">Regeneração de chave de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="5dbd3-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="5dbd3-206">Em produção, você está provavelmente toorefresh o armazenamento de chaves periodicamente.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="5dbd3-207">Ao atualizar as chaves, é necessário a diretiva de auditoria tooresave hello.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="5dbd3-208">processo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-208">hello process is as follows:</span></span>

1. <span data-ttu-id="5dbd3-209">Olá abrir **armazenamento detalhes** folha.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="5dbd3-210">Em Olá **chave de acesso de armazenamento** selecione **secundário**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="5dbd3-211">Em seguida, clique em **salvar** na parte superior de saudação do hello folha de configuração de auditoria.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Painel de navegação][5]
2. <span data-ttu-id="5dbd3-213">Vá toohello folha de configuração de armazenamento e regenerar a chave de acesso primária hello.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Painel de navegação][6]
3. <span data-ttu-id="5dbd3-215">Voltar toohello folha de configuração de auditoria, alternar a chave de acesso de armazenamento de saudação do tooprimary secundário e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="5dbd3-216">Em seguida, clique em **salvar** na parte superior de saudação do hello folha de configuração de auditoria.</span><span class="sxs-lookup"><span data-stu-id="5dbd3-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="5dbd3-217">Volte toohello folha de configuração de armazenamento e chave de acesso secundária Olá regenerar (em preparação para o ciclo de atualização da chave Olá próximo).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="5dbd3-218"><a id="subheading-7"></a>Automação (PowerShell/API REST)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="5dbd3-219">Você também pode configurar a auditoria no banco de dados do SQL Azure usando Olá ferramentas de automação a seguir:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="5dbd3-220">**Cmdlets do PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="5dbd3-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="5dbd3-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="5dbd3-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="5dbd3-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="5dbd3-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="5dbd3-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="5dbd3-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="5dbd3-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="5dbd3-228">Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5dbd3-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="5dbd3-229">**API REST – Auditoria de blob**:</span><span class="sxs-lookup"><span data-stu-id="5dbd3-229">**REST API - Blob auditing**:</span></span>

   * <span data-ttu-id="5dbd3-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Criar ou atualizar a política de auditoria de blob do banco de dados)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)</span></span>
   * <span data-ttu-id="5dbd3-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Criar ou atualizar uma política de auditoria de blob de servidor)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)</span></span>
   * <span data-ttu-id="5dbd3-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obter a política de auditoria de blob do banco de dados)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)</span></span>
   * <span data-ttu-id="5dbd3-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obter a política de auditoria de blob do servidor)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)</span></span>
   * <span data-ttu-id="5dbd3-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obter o resultado da operação de auditoria do blob do servidor)</span><span class="sxs-lookup"><span data-stu-id="5dbd3-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)</span></span>


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
