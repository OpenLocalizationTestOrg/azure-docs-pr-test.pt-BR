---
title: "aaaManage bancos de dados do SQL Azure usando a automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automação do Azure pode ser usado toomanage bancos de dados SQL do Azure em escala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="039c7-103">Gerenciando bancos de dados SQL do Azure usando a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="039c7-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="039c7-104">Este guia apresentará toohello serviço de automação do Azure e como ela pode ser usado toosimplify gerenciamento de seus bancos de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="039c7-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="039c7-105">O que é Automação do Azure?</span><span class="sxs-lookup"><span data-stu-id="039c7-105">What is Azure Automation?</span></span>
<span data-ttu-id="039c7-106">[Automação do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo.</span><span class="sxs-lookup"><span data-stu-id="039c7-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="039c7-107">Tarefas de longa execução, manuais, propensas a erros e repetidas com frequência usando a automação do Azure, podem ser automatizado tooincrease confiabilidade, a eficiência e toovalue de tempo para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="039c7-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="039c7-108">Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que dimensiona toomeet suas necessidades que sua organização cresce.</span><span class="sxs-lookup"><span data-stu-id="039c7-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="039c7-109">Na Automação do Azure, os processos podem ser inicializados manualmente por sistemas de terceiros ou a intervalos agendados para que as tarefas aconteçam exatamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="039c7-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="039c7-110">Reduzir a sobrecarga operacional e liberar IT / DevOps equipe toofocus no trabalho que adiciona valor comercial, movendo o toobe de tarefas de gerenciamento de nuvem executados automaticamente pela automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="039c7-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="039c7-111">Como a Automação do Azure pode ajudar a gerenciar bancos de dados SQL do Azure?</span><span class="sxs-lookup"><span data-stu-id="039c7-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="039c7-112">Banco de dados SQL do Azure podem ser gerenciado na automação do Azure usando Olá [cmdlets do PowerShell de banco de dados do SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) que estão disponíveis no hello [ferramentas do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="039c7-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="039c7-113">Automação do Azure tem esses cmdlets de banco de dados do SQL Azure PowerShell disponíveis fora da caixa hello, para que você pode executar todas as tarefas de gerenciamento de banco de dados SQL no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="039c7-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="039c7-114">Esses cmdlets na automação do Azure com os cmdlets de saudação para outros serviços do Azure, as tarefas complexas tooautomate também podem ser emparelhados por serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="039c7-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="039c7-115">Automação do Azure também tem Olá capacidade toocommunicate com servidores SQL diretamente, emitindo os comandos SQL usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="039c7-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="039c7-116">Olá [Galeria de runbook de automação do Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contém uma variedade de produtos equipe e comunidade runbooks tooget iniciado automatizar o gerenciamento de bancos de dados do SQL Azure, outros serviços do Azure e 3º sistemas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="039c7-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="039c7-117">A galeria de runbooks inclui:</span><span class="sxs-lookup"><span data-stu-id="039c7-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="039c7-118">Executar consultas SQL em um banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="039c7-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="039c7-119">Escalar verticalmente (para cima ou para baixo) um Banco de Dados SQL do Azure em uma agenda</span><span class="sxs-lookup"><span data-stu-id="039c7-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="039c7-120">Truncar uma tabela SQL se seu banco de dados se aproximar do tamanho máximo</span><span class="sxs-lookup"><span data-stu-id="039c7-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="039c7-121">Indexar tabelas em um Banco de Dados SQL do Azure se elas estiverem muito fragmentadas</span><span class="sxs-lookup"><span data-stu-id="039c7-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="039c7-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="039c7-122">Next steps</span></span>
<span data-ttu-id="039c7-123">Agora que você aprendeu as Noções básicas de saudação de automação do Azure e como ela pode ser usado toomanage bancos de dados do SQL Azure, siga essas toolearn links mais informações sobre a automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="039c7-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="039c7-124">Visão geral da Automação</span><span class="sxs-lookup"><span data-stu-id="039c7-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="039c7-125">Meu primeiro runbook</span><span class="sxs-lookup"><span data-stu-id="039c7-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="039c7-126">Mapa de aprendizagem de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="039c7-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="039c7-127">Automação do Azure: O SQL Agent no hello nuvem</span><span class="sxs-lookup"><span data-stu-id="039c7-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

