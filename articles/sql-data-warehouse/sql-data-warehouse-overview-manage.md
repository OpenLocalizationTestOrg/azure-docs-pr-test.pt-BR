---
title: Gerenciar bancos de dados no Azure SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: b14d0aad5a1f50c225391dbab27ec6240423a65a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="12c77-104">Gerenciar bancos de dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="12c77-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="12c77-105">O SQL Data Warehouse automatiza muitos aspectos do gerenciamento de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="12c77-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="12c77-106">Por exemplo, para aumentar o desempenho, basta ajustar para o nível certo de recursos de computação e pagar por eles, para então deixar o SQL Data Warehouse fazer todo o trabalho de escalar horizontalmente e de reverter essa escala.</span><span class="sxs-lookup"><span data-stu-id="12c77-106">For example, to scale performance you only need to adjust and pay for the right level of compute resources, and then let SQL Data Warehouse do all the work of scaling out and scaling back.</span></span>

<span data-ttu-id="12c77-107">Sem dúvida, você desejará monitorar sua carga de trabalho para identificar suas necessidades de desempenho, bem como solucionar problemas em consultas de execução longa.</span><span class="sxs-lookup"><span data-stu-id="12c77-107">You will undoubtedly want to monitor your workload to identify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="12c77-108">Você também precisará executar algumas tarefas de segurança para gerenciar permissões para usuários e logons.</span><span class="sxs-lookup"><span data-stu-id="12c77-108">You will also need to perform a few security tasks to manage permissions for users and logins.</span></span>

<span data-ttu-id="12c77-109">Esta visão geral aborda esses aspectos do gerenciamento do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c77-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="12c77-110">Ferramentas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="12c77-110">Management tools</span></span>
* <span data-ttu-id="12c77-111">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="12c77-111">Scale Compute</span></span>
* <span data-ttu-id="12c77-112">Pausar e retomar</span><span class="sxs-lookup"><span data-stu-id="12c77-112">Pause and Resume</span></span>
* <span data-ttu-id="12c77-113">Práticas recomendadas de desempenho</span><span class="sxs-lookup"><span data-stu-id="12c77-113">Performance Best Practices</span></span>
* <span data-ttu-id="12c77-114">Monitoramento de consulta</span><span class="sxs-lookup"><span data-stu-id="12c77-114">Query Monitoring</span></span>
* <span data-ttu-id="12c77-115">Segurança</span><span class="sxs-lookup"><span data-stu-id="12c77-115">Security</span></span>
* <span data-ttu-id="12c77-116">Backup e restauração</span><span class="sxs-lookup"><span data-stu-id="12c77-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="12c77-117">Ferramentas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="12c77-117">Management tools</span></span>
<span data-ttu-id="12c77-118">Você pode usar uma variedade de ferramentas para gerenciar bancos de dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c77-118">You can use a variety of tools to manage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="12c77-119">Ao gerenciar bancos de dados, você desenvolverá preferências de ferramenta para cada tipo de tarefa, que você precisa executar.</span><span class="sxs-lookup"><span data-stu-id="12c77-119">As you manage databases, you will develop tool preferences for each type of task you need to perform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="12c77-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="12c77-120">Azure portal</span></span>
<span data-ttu-id="12c77-121">O [Portal do Azure][Azure portal] é um portal baseado na Web, no qual você pode criar, atualizar e excluir bancos de dados e monitorar recursos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="12c77-121">The [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="12c77-122">Essa ferramenta será excelente se você estiver começando a usar o Azure, se estiver gerenciando uma pequena quantidade de bancos de dados de data warehouse ou se precisar fazer alguma coisa rapidamente.</span><span class="sxs-lookup"><span data-stu-id="12c77-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need to quickly do something.</span></span>

<span data-ttu-id="12c77-123">Para começar a usar o Portal do Azure, confira [Criar um SQL Data Warehouse (Portal do Azure)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="12c77-123">To get started with the Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="12c77-124">SQL Server Data Tools no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12c77-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="12c77-125">O SSDT ([SQL Server Data Tools][SQL Server Data Tools]) no Visual Studio permite que você se conecte, gerencie e desenvolva seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="12c77-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you to connect to, manage, and develop your databases.</span></span> <span data-ttu-id="12c77-126">Se você for um desenvolvedor de aplicativos familiarizado com o Visual Studio ou com outros ambientes de desenvolvimento integrados (IDEs), tente usar o SSDT no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12c77-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="12c77-127">O SSDT inclui o Pesquisador de Objetos do SQL Server, que permite a visualização, conexão e execução de scripts em bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c77-127">SSDT includes the SQL Server Object Explorer which enables you to visualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="12c77-128">Para conectar-se rapidamente ao SQL Data Warehouse, você pode simplesmente clicar no botão **Abrir no Visual Studio** na barra de comandos ao exibir os detalhes do banco de dados no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="12c77-128">To quickly connect to SQL Data Warehouse, you can simply click the **Open in Visual Studio** button in the command bar when viewing the database details in the Azure Classic Portal.</span></span>  

<span data-ttu-id="12c77-129">Para uma introdução ao SSDT no Visual Studio, confira [Conectar-se ao SQL Data Warehouse do Azure com o Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="12c77-129">To get started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="12c77-130">Ferramentas da linha de comando</span><span class="sxs-lookup"><span data-stu-id="12c77-130">Command-line tools</span></span>
<span data-ttu-id="12c77-131">Ferramentas de linha de comando são ideais para automatizar suas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="12c77-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="12c77-132">PowerShell e sqlcmd são duas formas incríveis de automatizar os processos.</span><span class="sxs-lookup"><span data-stu-id="12c77-132">PowerShell and sqlcmd are two great ways to automate your processes.</span></span>  <span data-ttu-id="12c77-133">Recomendamos essas ferramentas para gerenciar uma grande quantidade de servidores lógicos e implantar alterações de recursos em um ambiente de produção, pois as tarefas necessárias podem ser incluídas em script e automatizadas.</span><span class="sxs-lookup"><span data-stu-id="12c77-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as the tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="12c77-134">Exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="12c77-134">Dynamic management views</span></span>
<span data-ttu-id="12c77-135">DMVs são a base do gerenciamento de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c77-135">DMVs are the bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="12c77-136">Quase todas as informações que aparecem no portal dependem de DMVs.</span><span class="sxs-lookup"><span data-stu-id="12c77-136">Almost all information that surfaces in the portal relies on DMVs.</span></span> <span data-ttu-id="12c77-137">Para ver uma lista de DMVs do SQL Data Warehouse, confira [Exibições do sistema do SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="12c77-137">To see a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="12c77-138">Para começar, confira [Conectar e consultar com sqlcmd][Connect and query with sqlcmd] e [Criar um banco de dados (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="12c77-138">To get started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="12c77-139">Computação de escala</span><span class="sxs-lookup"><span data-stu-id="12c77-139">Scale compute</span></span>
<span data-ttu-id="12c77-140">No SQL Data Warehouse você pode, com rapidez, escalar horizontalmente o desempenho ou reverter esse processo, aumentando ou diminuindo os recursos de computação de CPU, memória e largura de banda de E/S.</span><span class="sxs-lookup"><span data-stu-id="12c77-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="12c77-141">Para dimensionar o desempenho, tudo o que você precisa fazer é ajustar o número de DWUs (unidades de data warehouse) que o SQL Data Warehouse aloca para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="12c77-141">To scale performance, all you need to do is adjust the number of data warehouse units (DWUs) that SQL Data Warehouse allocates to your database.</span></span> <span data-ttu-id="12c77-142">O SQL Data Warehouse faz rapidamente a alteração e trata de todas as alterações subjacentes de hardware e software.</span><span class="sxs-lookup"><span data-stu-id="12c77-142">SQL Data Warehouse quickly makes the change and handles all the underlying changes to hardware or software.</span></span>

<span data-ttu-id="12c77-143">Para saber mais sobre o dimensionamento de DWUs, confira [Dimensionar o desempenho].</span><span class="sxs-lookup"><span data-stu-id="12c77-143">To learn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="12c77-144">Pausar e retomar</span><span class="sxs-lookup"><span data-stu-id="12c77-144">Pause and resume</span></span>
<span data-ttu-id="12c77-145">Para economizar custos, é possível pausar e retomar os recursos de computação sob demanda.</span><span class="sxs-lookup"><span data-stu-id="12c77-145">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="12c77-146">Por exemplo, se você não usar banco de dados durante a noite e nos finais de semana, você poderá pausá-lo durante esses períodos e retomá-lo durante o dia.</span><span class="sxs-lookup"><span data-stu-id="12c77-146">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="12c77-147">Você não será cobrado por DWUs enquanto o banco de dados estiver em pausa.</span><span class="sxs-lookup"><span data-stu-id="12c77-147">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="12c77-148">Para saber mais, confira [Pausar computação][Pause compute] e [Retomar a computação][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="12c77-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="12c77-149">Práticas recomendadas de desempenho</span><span class="sxs-lookup"><span data-stu-id="12c77-149">Performance Best Practices</span></span>
<span data-ttu-id="12c77-150">Ao ser apresentado a uma nova tecnologia, descobrir as dicas e truques que funcionam melhor desde o início pode economizar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="12c77-150">When getting started with a new technology, discovering the tips and tricks that work best right from the start can save you lots of time.</span></span>  <span data-ttu-id="12c77-151">Você encontrará as práticas recomendadas ao longo de muitos tópicos.</span><span class="sxs-lookup"><span data-stu-id="12c77-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="12c77-152">Para ver um resumo das considerações mais importantes no desenvolvimento de sua carga de trabalho, confira [Práticas recomendadas para o SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="12c77-152">To see many a summary of the most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="12c77-153">Monitoramento de consulta</span><span class="sxs-lookup"><span data-stu-id="12c77-153">Query Monitoring</span></span>
<span data-ttu-id="12c77-154">Às vezes, uma consulta está sendo executada por muito tempo, mas você não tem certeza de qual é o culpada.</span><span class="sxs-lookup"><span data-stu-id="12c77-154">Sometimes a query is running too long, but you aren't sure of which one is the culprit.</span></span> <span data-ttu-id="12c77-155">O SQL Data Warehouse tem DMVs (exibições de gerenciamento dinâmico) que você pode usar para descobrir qual consulta está demorando tempo demais.</span><span class="sxs-lookup"><span data-stu-id="12c77-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use to figure out which query is taking too long.</span></span>

<span data-ttu-id="12c77-156">Para encontrar consultas de longa execução, confira [Monitorar sua carga de trabalho usando DMVs][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="12c77-156">To find long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="12c77-157">Segurança</span><span class="sxs-lookup"><span data-stu-id="12c77-157">Security</span></span>
<span data-ttu-id="12c77-158">Para manter um sistema seguro, você deve estar alerta e protegê-lo contra todo tipo de acesso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="12c77-158">To maintain a secure system, you must be on the alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="12c77-159">Um sistema de segurança precisa verificar se as regras de firewall estão em vigor de modo que apenas endereços IP autorizados possam se conectar.</span><span class="sxs-lookup"><span data-stu-id="12c77-159">A security system needs to make sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="12c77-160">Ele precisa de autenticação adequada das credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="12c77-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="12c77-161">Depois que um usuário se conectou ao banco de dados, o usuário só deve ter permissões para executar um número mínimo de ações.</span><span class="sxs-lookup"><span data-stu-id="12c77-161">After a user has connected to the database, the user should only have permissions to perform a minimal number of actions.</span></span> <span data-ttu-id="12c77-162">Para proteger dados, você pode usar criptografia.</span><span class="sxs-lookup"><span data-stu-id="12c77-162">To secure data, you can use encryption.</span></span> <span data-ttu-id="12c77-163">Também é importante ter auditoria e acompanhamento para que você possa retraçar eventos em caso de qualquer atividade suspeita.</span><span class="sxs-lookup"><span data-stu-id="12c77-163">It's also important to have auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="12c77-164">Para saber sobre como gerenciar a segurança, vá até a [Visão geral de segurança][Security overview].</span><span class="sxs-lookup"><span data-stu-id="12c77-164">To learn about managing security, head over to the [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="12c77-165">Backup e restauração</span><span class="sxs-lookup"><span data-stu-id="12c77-165">Backup and restore</span></span>
<span data-ttu-id="12c77-166">Ter backups confiáveis de seus dados é uma parte essencial de qualquer banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="12c77-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="12c77-167">O SQL Data Warehouse mantém seus dados seguros fazendo backup automaticamente de seus bancos de dados ativos em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="12c77-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="12c77-168">Esses backups permitem que você se recupere de cenários em que corromper ou descartar acidentalmente seus dados ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="12c77-168">These backups allow you to recover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="12c77-169">Para agendamento de backup de dados, política de retenção e como restaurar um banco de dados, confira [Restaurar do instantâneo][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="12c77-169">For the data backup schedule, retention policy and how to restore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c77-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12c77-170">Next steps</span></span>
<span data-ttu-id="12c77-171">Usar bons princípios de design de banco de dados tornará mais fácil gerenciar seus bancos de dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c77-171">Using good database design principles will make it easier to manage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="12c77-172">Para saber mais, vá até a [Visão geral de desenvolvimento][Development overview].</span><span class="sxs-lookup"><span data-stu-id="12c77-172">To learn more, head over to the [Development overview][Development overview].</span></span>

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
<span data-ttu-id="12c77-173">[Dimensionar o desempenho]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span><span class="sxs-lookup"><span data-stu-id="12c77-173">[Scale performance]: sql-data-warehouse-manage-compute-overview.md#scale-compute</span></span>
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
