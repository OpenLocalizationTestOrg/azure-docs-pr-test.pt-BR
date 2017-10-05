---
title: "Introdução à auditoria do banco de dados SQL do Azure | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="4b9dc-103">Introdução à auditoria do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="4b9dc-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="4b9dc-104">A auditoria do banco de dados SQL do Azure acompanha eventos do banco de dados e grava-os em um log de auditoria em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="4b9dc-105">A auditoria também:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-105">Auditing also:</span></span>

* <span data-ttu-id="4b9dc-106">Ajuda você a manter a conformidade regulatória, entender a atividade do banco de dados e obter informações sobre discrepâncias e anomalias que podem indicar preocupações para os negócios ou suspeitas de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="4b9dc-107">Permite e facilita a adesão aos padrões de conformidade, embora não garanta a conformidade.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="4b9dc-108">Para obter mais informações sobre os programas Azure que oferecem suporte à conformidade com os padrões, consulte o [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="4b9dc-109"><a id="subheading-1"></a>Visão geral da auditoria do banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4b9dc-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="4b9dc-110">É possível usar a auditoria do banco de dados SQL para:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="4b9dc-111">**Retenha** uma trilha de auditoria dos eventos selecionados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="4b9dc-112">Definir categorias de ações de banco de dados a ser auditadas.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="4b9dc-113">**Relate** sobre a atividade do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-113">**Report** on database activity.</span></span> <span data-ttu-id="4b9dc-114">Utilizar relatórios pré-configurados e um painel para iniciar rapidamente um relatório de atividades e eventos.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="4b9dc-115">**Analise** relatórios.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-115">**Analyze** reports.</span></span> <span data-ttu-id="4b9dc-116">Encontrar eventos suspeitos, atividades incomuns e tendências.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="4b9dc-117">Você pode configurar a auditoria para diferentes tipos de categorias de evento, conforme explicado na seção [Configurar a auditoria do banco de dados](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="4b9dc-118">Os logs de auditoria são gravados no Armazenamento de blobs do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="4b9dc-119"><a id="subheading-8"></a>Definir a política de auditoria no nível do servidor versus no nível do banco de dados</span><span class="sxs-lookup"><span data-stu-id="4b9dc-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="4b9dc-120">Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão de servidor:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="4b9dc-121">Uma política de servidor se aplica a todos os bancos de dados existentes e recém-criados no servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="4b9dc-122">Se a *auditoria de blob do servidor estiver habilitada*, ela *sempre se aplicará ao banco de dados* (ou seja, o banco de dados será auditado), independentemente das configurações de auditoria do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="4b9dc-123">A habilitação da auditoria de blob no banco de dados, além de sua habilitação no servidor, *não* substituirá nem alterará as configurações de auditoria de blob do servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="4b9dc-124">Ambas as auditorias existirão lado a lado.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-124">Both audits will exist side by side.</span></span> <span data-ttu-id="4b9dc-125">Em outras palavras, o banco de dados será auditado duas vezes em paralelo (uma vez pela política de servidor e uma vez pela política de banco de dados).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b9dc-126">Evite habilitar a auditoria de blobs de servidor e a auditoria de blobs do banco de dados juntas, a menos que:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="4b9dc-127">Você deseja usar outra *conta de armazenamento* ou outro *período de retenção* para um banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="4b9dc-128">Você deseja auditar categorias ou tipos de evento de um banco de dados específico que são diferentes das categorias ou dos tipos de evento que estão sendo auditados no restante dos bancos de dados no servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="4b9dc-129">Por exemplo, talvez você tenha inserções de tabela que precisam ser auditadas somente em um banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="4b9dc-130">Caso contrário, recomendamos habilitar somente a auditoria de blob no nível do servidor e deixar a auditoria no nível do banco de dados desabilitada para todos os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="4b9dc-131"><a id="subheading-2"></a>Configurar a auditoria do banco de dados</span><span class="sxs-lookup"><span data-stu-id="4b9dc-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="4b9dc-132">A seção a seguir descreve a configuração de auditoria usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="4b9dc-133">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b9dc-134">Acesse a folha **Configurações** do banco de dados SQL/SQL Server que você deseja auditar.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="4b9dc-135">Na folha **Configurações**, selecione **Auditoria e Detecção de ameaças**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="4b9dc-136"><a id="auditing-screenshot"></a> ![Painel de navegação][1]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="4b9dc-137">Se você preferir configurar uma política de auditoria do servidor (que se aplicará a todos os bancos de dados existentes e recém-criados neste servidor), poderá selecionar o link **Exibir configurações do servidor** na folha de auditoria do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="4b9dc-138">Depois, é possível exibir ou modificar as configurações de auditoria do servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-138">You can then view or modify the server auditing settings.</span></span>

    ![Painel de navegação][2]
4. <span data-ttu-id="4b9dc-140">Se você preferir habilitar a auditoria de blob no nível do banco de dados (além ou em vez da auditoria no nível do servidor), em **Auditoria**, selecione **ATIVADO** e, em **Tipo de auditoria**, selecione **Blob**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="4b9dc-141">Se a auditoria de blob do servidor estiver habilitada, a auditoria configurada para o banco de dados existirá lado a lado com a auditoria de blob do servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Painel de navegação][3]
5. <span data-ttu-id="4b9dc-143">Para abrir a folha **Armazenamento de Logs de Auditoria**, selecione **Detalhes de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="4b9dc-144">Selecione a conta de armazenamento do Azure em que os logs serão salvos e, depois, selecione o período de retenção, após o qual os logs antigos serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="4b9dc-145">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="4b9dc-146">Para aproveitar ao máximo os modelos de relatórios de auditoria, use a mesma conta de armazenamento para todos os bancos de dados auditados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="4b9dc-147"><a id="storage-screenshot"></a> ![Painel de navegação][4]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="4b9dc-148">Se quiser personalizar os eventos auditados, você poderá fazer isso por meio do PowerShell ou da API REST.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="4b9dc-149">Para obter mais detalhes, consulte a seção [Automação (PowerShell/API REST)](#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="4b9dc-150">Depois de definir as configurações de auditoria, você poderá ativar o novo recurso de detecção de ameaças e configurar emails para receber alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="4b9dc-151">Ao usar a detecção de ameaças, você recebe alertas proativos sobre atividades anômalas do banco de dados que podem indicar possíveis ameaças à segurança.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="4b9dc-152">Para obter mais detalhes, consulte [Introdução à detecção de ameaças](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="4b9dc-153">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-153">Click **Save**.</span></span>





## <span data-ttu-id="4b9dc-154"><a id="subheading-3"></a>Analisar os logs e relatórios de auditoria</span><span class="sxs-lookup"><span data-stu-id="4b9dc-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="4b9dc-155">Os logs de auditoria são agregados na conta do Azure Storage escolhida durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="4b9dc-156">Explore os logs de auditoria usando uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="4b9dc-157">Os logs de auditoria de blob são salvos como uma coleção de arquivos de blob em um contêiner chamado **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="4b9dc-158">Para obter mais detalhes sobre a hierarquia da pasta de armazenamento dos logs de auditoria de blob, as convenções de nomenclatura do blob e o formato do log, consulte a [Referência de formato do log de auditoria de blob (download de arquivo .doc)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="4b9dc-159">Há vários métodos que podem ser usados para exibir os logs de auditoria de blob:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="4b9dc-160">Use o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="4b9dc-161">Abra o banco de dados relevante.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-161">Open the relevant database.</span></span> <span data-ttu-id="4b9dc-162">Na parte superior da folha **Auditoria e Detecção de ameaças** do banco de dados, clique em **Exibir logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Painel de navegação][7]

    <span data-ttu-id="4b9dc-164">Uma folha **Registros de auditoria** será aberta, na qual você poderá exibir os logs.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="4b9dc-165">Exiba datas específicas clicando em **Filtro** na parte superior da folha **Registros de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="4b9dc-166">Alterne entre os registros de auditoria que foram criados por uma auditoria da política de servidor ou da política de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Painel de navegação][8]

* <span data-ttu-id="4b9dc-168">Use a função do sistema **sys.fn_get_audit_file** (T-SQL) para retornar os dados do log de auditoria em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="4b9dc-169">Para obter mais informações sobre como usar essa função, consulte a [documentação de sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="4b9dc-170">Use a opção **Mesclar Arquivos de Auditoria** no SQL Server Management Studio (a partir do SSMS 17):</span><span class="sxs-lookup"><span data-stu-id="4b9dc-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="4b9dc-171">No menu do SSMS, selecione **Arquivo** > **Abrir** > **Mesclar Arquivos de Auditoria**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Painel de navegação][9]
    2. <span data-ttu-id="4b9dc-173">A caixa de diálogo **Adicionar Arquivos de Auditoria** será aberta.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="4b9dc-174">Selecione uma das opções **Adicionar** para escolher se deseja mesclar arquivos de auditoria de um disco local ou importá-los do Armazenamento do Azure (você deverá fornecer os detalhes e a chave de conta do Armazenamento do Azure).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="4b9dc-175">Depois que todos os arquivos a serem mesclados forem adicionados, clique em **OK** para concluir a operação de mesclagem.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="4b9dc-176">O arquivo mesclado é aberto no SSMS, no qual você pode exibi-lo e analisá-lo, bem como exportá-lo para um arquivo XEL ou CSV ou para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="4b9dc-177">Use o [aplicativo de sincronização](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que criamos.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="4b9dc-178">Ele é executado no Azure e utiliza APIs públicas do Log Analytics do OMS (Operations Management Suite) para enviar os logs de auditoria do SQL por push para o OMS.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="4b9dc-179">O aplicativo de sincronização envia os logs de auditoria do SQL por push para o Log Analytics do OMS para consumo por meio do painel do Log Analytics do OMS.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="4b9dc-180">Use o Power BI.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-180">Use Power BI.</span></span> <span data-ttu-id="4b9dc-181">Você pode exibir e analisar dados do log de auditoria no Power BI.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="4b9dc-182">Saiba mais sobre o [Power BI e acesse um modelo para download](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="4b9dc-183">Baixe os arquivos de log do contêiner de Azure Storage Blob por meio do portal ou usando uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="4b9dc-184">Depois de baixar um arquivo de log localmente, clique duas vezes no arquivo para abrir, exibir e analisar os logs no SSMS.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="4b9dc-185">Baixe também vários arquivos simultaneamente por meio do Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="4b9dc-186">Clique com o botão direito do mouse em uma subpasta específica (por exemplo, uma subpasta que inclui todos os arquivos de log de uma data específica) e selecione **Salvar como** para salvar em uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="4b9dc-187">Métodos adicionais:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-187">Additional methods:</span></span>
   * <span data-ttu-id="4b9dc-188">Depois de baixar vários arquivos (ou uma subpasta que inclui arquivos de log de um dia inteiro, conforme descrito no item anterior nesta lista), você pode mesclá-los localmente, conforme descrito nas instruções da opção Mesclar Arquivos de Auditoria do SSMS indicadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="4b9dc-189">Exiba os logs de auditoria de blob de forma programática:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="4b9dc-190">Use a biblioteca C# do [Leitor de Eventos Estendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="4b9dc-191">[Consulte Arquivos de Eventos Estendidos usando o PowerShell](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="4b9dc-192"><a id="subheading-5"></a>Práticas de produção</span><span class="sxs-lookup"><span data-stu-id="4b9dc-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="4b9dc-193"><a id="subheading-6">Auditoria de bancos de dados replicados geograficamente</a></span><span class="sxs-lookup"><span data-stu-id="4b9dc-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="4b9dc-194">Ao usar bancos de dados com replicação geográfica, é possível configurar a auditoria no banco de dados primário, no banco de dados secundário ou em ambos, dependendo do tipo de auditoria.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="4b9dc-195">Siga estas instruções (lembre-se de que a auditoria de blob pode ser ativada ou desativada somente nas configurações de auditoria do banco de dados primário):</span><span class="sxs-lookup"><span data-stu-id="4b9dc-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="4b9dc-196">**Banco de dados primário**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-196">**Primary database**.</span></span> <span data-ttu-id="4b9dc-197">Ative a auditoria de blob, no servidor ou no próprio banco de dados, conforme descrito na seção [Configurar a auditoria do banco de dados](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="4b9dc-198">**Banco de dados secundário**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-198">**Secondary database**.</span></span> <span data-ttu-id="4b9dc-199">Ative a auditoria de blob no banco de dados primário, conforme descrito na seção [Configurar a auditoria do banco de dados](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="4b9dc-200">A auditoria de blob precisa estar habilitada no *banco de dados primário*, não no servidor.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="4b9dc-201">Depois que a auditoria de blob estiver habilitada no banco de dados primário, ela também será habilitada no banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="4b9dc-202">Por padrão, as configurações de armazenamento do banco de dados secundário serão idênticas às do banco de dados primário, causando um tráfego entre regiões.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="4b9dc-203">Evite isso habilitando a auditoria de blob no servidor secundário e configurando o armazenamento local nas configurações de armazenamento do servidor secundário.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="4b9dc-204">Isso substituirá o local de armazenamento do banco de dados secundário e o resultado será que cada banco de dados salvará seus logs de auditoria no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="4b9dc-205"><a id="subheading-6">Regeneração de chave de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="4b9dc-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="4b9dc-206">Em produção, você provavelmente atualizará suas chaves de armazenamento periodicamente.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="4b9dc-207">Ao atualizar as chaves, é necessário salvar novamente a política de auditoria.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="4b9dc-208">O processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-208">The process is as follows:</span></span>

1. <span data-ttu-id="4b9dc-209">Abra a folha **Detalhes de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="4b9dc-210">Na caixa **Chave de Acesso de Armazenamento**, selecione **Secundária** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="4b9dc-211">Em seguida, clique em **Salvar** na parte superior da folha de configuração de auditoria.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Painel de navegação][5]
2. <span data-ttu-id="4b9dc-213">Acesse a folha de configuração de armazenamento e regenere a chave de acesso primária.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Painel de navegação][6]
3. <span data-ttu-id="4b9dc-215">Volte para a folha de configuração de auditoria, alterne a chave de acesso de armazenamento de secundária para primária e, depois, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="4b9dc-216">Em seguida, clique em **Salvar** na parte superior da folha de configuração de auditoria.</span><span class="sxs-lookup"><span data-stu-id="4b9dc-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="4b9dc-217">Volte para a folha de configuração de armazenamento e regenere a chave de acesso secundária (em preparação para o próximo ciclo de atualização da chave).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="4b9dc-218"><a id="subheading-7"></a>Automação (PowerShell/API REST)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="4b9dc-219">Configure também a auditoria no Banco de Dados SQL do Azure usando as seguintes ferramentas de automação:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="4b9dc-220">**Cmdlets do PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="4b9dc-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="4b9dc-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="4b9dc-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="4b9dc-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="4b9dc-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="4b9dc-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="4b9dc-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="4b9dc-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="4b9dc-228">Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4b9dc-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="4b9dc-229">**API REST – Auditoria de blob**:</span><span class="sxs-lookup"><span data-stu-id="4b9dc-229">**REST API - Blob auditing**:</span></span>

   * <span data-ttu-id="4b9dc-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Criar ou atualizar a política de auditoria de blob do banco de dados)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-230">[Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)</span></span>
   * <span data-ttu-id="4b9dc-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Criar ou atualizar uma política de auditoria de blob de servidor)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-231">[Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)</span></span>
   * <span data-ttu-id="4b9dc-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obter a política de auditoria de blob do banco de dados)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-232">[Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)</span></span>
   * <span data-ttu-id="4b9dc-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obter a política de auditoria de blob do servidor)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-233">[Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)</span></span>
   * <span data-ttu-id="4b9dc-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obter o resultado da operação de auditoria do blob do servidor)</span><span class="sxs-lookup"><span data-stu-id="4b9dc-234">[Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)</span></span>


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
