---
title: bancos de dados aaaManage no Azure SQL Data Warehouse | Microsoft Docs
description: "Visão geral do gerenciamento de bancos de dados do SQL Data Warehouse. Inclui ferramentas de gerenciamento, DWUs e escalar o desempenho horizontalmente, solucionar problemas de desempenho de consulta, estabelecer políticas de segurança e restaurar um banco de dados contra dados corrompidos ou de uma interrupção regional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="5133e-104">Gerenciar bancos de dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="5133e-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="5133e-105">O SQL Data Warehouse automatiza muitos aspectos do gerenciamento de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5133e-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="5133e-106">Por exemplo, o desempenho tooscale você só precisa tooadjust pague Olá o nível certo de recursos de computação e permitir que o SQL Data Warehouse fazer todo o trabalho de saudação de expansão e dimensionamento back.</span><span class="sxs-lookup"><span data-stu-id="5133e-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="5133e-107">Você certamente desejará toomonitor tooidentify sua carga de trabalho, seu desempenho precisa, bem como solucionar problemas de consultas de longa execução.</span><span class="sxs-lookup"><span data-stu-id="5133e-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="5133e-108">Você também precisará tooperform alguns segurança tarefas toomanage permissões para usuários e logons.</span><span class="sxs-lookup"><span data-stu-id="5133e-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="5133e-109">Esta visão geral aborda esses aspectos do gerenciamento do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5133e-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="5133e-110">Ferramentas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5133e-110">Management tools</span></span>
* <span data-ttu-id="5133e-111">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="5133e-111">Scale Compute</span></span>
* <span data-ttu-id="5133e-112">Pausar e retomar</span><span class="sxs-lookup"><span data-stu-id="5133e-112">Pause and Resume</span></span>
* <span data-ttu-id="5133e-113">Práticas recomendadas de desempenho</span><span class="sxs-lookup"><span data-stu-id="5133e-113">Performance Best Practices</span></span>
* <span data-ttu-id="5133e-114">Monitoramento de consulta</span><span class="sxs-lookup"><span data-stu-id="5133e-114">Query Monitoring</span></span>
* <span data-ttu-id="5133e-115">Segurança</span><span class="sxs-lookup"><span data-stu-id="5133e-115">Security</span></span>
* <span data-ttu-id="5133e-116">Backup e restauração</span><span class="sxs-lookup"><span data-stu-id="5133e-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="5133e-117">Ferramentas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5133e-117">Management tools</span></span>
<span data-ttu-id="5133e-118">Você pode usar uma variedade de bancos de dados de toomanage ferramentas no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5133e-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="5133e-119">Como você gerencia bancos de dados, você desenvolverá preferências de ferramenta para cada tipo de tarefa, você precisa tooperform.</span><span class="sxs-lookup"><span data-stu-id="5133e-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="5133e-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5133e-120">Azure portal</span></span>
<span data-ttu-id="5133e-121">Olá [portal do Azure] [ Azure portal] é um portal baseado na web, onde você pode criar, atualizar, excluir bancos de dados e monitorar os recursos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5133e-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="5133e-122">Essa ferramenta é ótima é se você estiver apenas começando com o Azure, Gerenciando um pequeno número de bancos de dados do data warehouse, ou precisa tooquickly fazer algo.</span><span class="sxs-lookup"><span data-stu-id="5133e-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="5133e-123">tooget iniciado com hello portal do Azure, consulte [criar um Data Warehouse de SQL (portal do Azure)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="5133e-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="5133e-124">SQL Server Data Tools no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5133e-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="5133e-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) no Visual Studio permite que você tooconnect gerenciar e desenvolver seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5133e-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="5133e-126">Se você for um desenvolvedor de aplicativos familiarizado com o Visual Studio ou com outros ambientes de desenvolvimento integrados (IDEs), tente usar o SSDT no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5133e-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="5133e-127">Olá Pesquisador de objetos do SQL Server que permite que você toovisualize o SSDT inclui, conectar e executar scripts em bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5133e-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="5133e-128">tooquickly conectar tooSQL Data Warehouse, você pode simplesmente clicar Olá **aberto no Visual Studio** botão na barra de comandos Olá ao exibir detalhes do banco de dados de saudação da saudação Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5133e-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="5133e-129">tooget iniciado com o SSDT no Visual Studio, consulte [consulta Azure SQL Data Warehouse com o Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="5133e-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="5133e-130">Ferramentas da linha de comando</span><span class="sxs-lookup"><span data-stu-id="5133e-130">Command-line tools</span></span>
<span data-ttu-id="5133e-131">Ferramentas de linha de comando são ideais para automatizar suas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5133e-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="5133e-132">PowerShell e o sqlcmd são tooautomate de duas maneiras ótimas seus processos.</span><span class="sxs-lookup"><span data-stu-id="5133e-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="5133e-133">Recomendamos essas ferramentas para gerenciar um grande número de servidores lógicos e implantar as alterações de recursos em um ambiente de produção, como tarefas de saudação necessárias podem ser incluídos no script e automatizadas, em seguida.</span><span class="sxs-lookup"><span data-stu-id="5133e-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="5133e-134">Exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="5133e-134">Dynamic management views</span></span>
<span data-ttu-id="5133e-135">DMVs são Olá base do SQL Data Warehouse de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5133e-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="5133e-136">Quase todas as informações que aparece no portal de saudação depende DMVs.</span><span class="sxs-lookup"><span data-stu-id="5133e-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="5133e-137">toosee uma lista de DMVs de depósito de dados do SQL, consulte [exibições do sistema SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="5133e-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="5133e-138">tooget iniciado, consulte [conectar e consultar com sqlcmd][Connect and query with sqlcmd], e [criar um banco de dados (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="5133e-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="5133e-139">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="5133e-139">Scale compute</span></span>
<span data-ttu-id="5133e-140">No SQL Data Warehouse você pode, com rapidez, escalar horizontalmente o desempenho ou reverter esse processo, aumentando ou diminuindo os recursos de computação de CPU, memória e largura de banda de E/S.</span><span class="sxs-lookup"><span data-stu-id="5133e-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="5133e-141">desempenho tooscale, tudo o que você precisa toodo é ajustar Olá número de unidades de depósito de dados (DWUs) que o SQL Data Warehouse aloca tooyour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5133e-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="5133e-142">SQL Data Warehouse faz hello e trata todos os Olá subjacente alterações toohardware ou software rapidamente.</span><span class="sxs-lookup"><span data-stu-id="5133e-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="5133e-143">toolearn mais sobre como dimensionar DWUs, consulte [dimensionar o desempenho].</span><span class="sxs-lookup"><span data-stu-id="5133e-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="5133e-144">Pausar e retomar</span><span class="sxs-lookup"><span data-stu-id="5133e-144">Pause and resume</span></span>
<span data-ttu-id="5133e-145">toosave custos, você pode pausar e retomar computação recursos sob demanda.</span><span class="sxs-lookup"><span data-stu-id="5133e-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="5133e-146">Por exemplo, se você não usar o banco de dados de saudação durante a noite hello e nos finais de semana, você pode pausá-la durante os horários e retomá-lo durante o dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="5133e-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="5133e-147">Você não será cobrado para DWUs enquanto o banco de dados de saudação está em pausa.</span><span class="sxs-lookup"><span data-stu-id="5133e-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="5133e-148">Para saber mais, confira [Pausar computação][Pause compute] e [Retomar a computação][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="5133e-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="5133e-149">Práticas recomendadas de desempenho</span><span class="sxs-lookup"><span data-stu-id="5133e-149">Performance Best Practices</span></span>
<span data-ttu-id="5133e-150">Quando a guia de Introdução com uma nova tecnologia, descoberta dicas hello e truques que funcionam melhor direita do início da saudação pode economizar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="5133e-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="5133e-151">Você encontrará as práticas recomendadas ao longo de muitos tópicos.</span><span class="sxs-lookup"><span data-stu-id="5133e-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="5133e-152">toosee muitos um resumo das considerações de hello mais importantes ao desenvolver sua carga de trabalho, consulte [práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="5133e-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="5133e-153">Monitoramento de consulta</span><span class="sxs-lookup"><span data-stu-id="5133e-153">Query Monitoring</span></span>
<span data-ttu-id="5133e-154">Às vezes, uma consulta está em execução muito longa, mas você não tiver certeza de qual é responsável hello.</span><span class="sxs-lookup"><span data-stu-id="5133e-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="5133e-155">SQL Data Warehouse tem modos de exibição de gerenciamento dinâmico (DMVs) que você pode usar toofigure out qual consulta está demorando muito.</span><span class="sxs-lookup"><span data-stu-id="5133e-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="5133e-156">consultas de longa execução toofind, consulte [monitorar sua carga de trabalho usando DMVs][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="5133e-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="5133e-157">Segurança</span><span class="sxs-lookup"><span data-stu-id="5133e-157">Security</span></span>
<span data-ttu-id="5133e-158">toomaintain um sistema seguro, você deve estar em alerta hello e proteger contra qualquer tipo de acesso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="5133e-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="5133e-159">Um sistema de segurança deve toomake-se de que as regras de firewall estão em vigor autorizado para que somente endereços IP podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="5133e-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="5133e-160">Ele precisa de autenticação adequada das credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="5133e-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="5133e-161">Depois que um usuário se conectou toohello banco de dados, Olá usuário deve ter somente permissões tooperform um número mínimo de ações.</span><span class="sxs-lookup"><span data-stu-id="5133e-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="5133e-162">toosecure dados, você pode usar criptografia.</span><span class="sxs-lookup"><span data-stu-id="5133e-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="5133e-163">Também é importante toohave de auditoria e controle para que você pode refazer eventos se há alguma atividade suspeita.</span><span class="sxs-lookup"><span data-stu-id="5133e-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="5133e-164">toolearn sobre gerenciamento de segurança, dirija-toohello [visão geral de segurança][Security overview].</span><span class="sxs-lookup"><span data-stu-id="5133e-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="5133e-165">Backup e restauração</span><span class="sxs-lookup"><span data-stu-id="5133e-165">Backup and restore</span></span>
<span data-ttu-id="5133e-166">Ter backups confiáveis de seus dados é uma parte essencial de qualquer banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="5133e-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="5133e-167">O SQL Data Warehouse mantém seus dados seguros fazendo backup automaticamente de seus bancos de dados ativos em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="5133e-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="5133e-168">Esses backups permitem toorecover de cenários onde você seus dados corrompidos ou descartado acidentalmente seus dados ou o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5133e-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="5133e-169">Para agendamento de backup de dados do hello, política de retenção e como toorestore um banco de dados, consulte [restauração do instantâneo][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="5133e-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5133e-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5133e-170">Next steps</span></span>
<span data-ttu-id="5133e-171">Usar os princípios de design de banco de dados bom tornará mais fácil toomanage seus bancos de dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5133e-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="5133e-172">toolearn mais, dirija-toohello [visão geral do desenvolvimento][Development overview].</span><span class="sxs-lookup"><span data-stu-id="5133e-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[dimensionar o desempenho]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
