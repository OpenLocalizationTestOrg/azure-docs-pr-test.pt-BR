---
title: "aaaCreate e gerenciar trabalhos Elásticos usando o PowerShell | Microsoft Docs"
description: PowerShell usado toomanage pools de banco de dados SQL
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="d3f98-103">Criar e gerenciar trabalhos elástico do Banco de Dados SQL usando o PowerShell (visualização)</span><span class="sxs-lookup"><span data-stu-id="d3f98-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="d3f98-104">Olá APIs do PowerShell para **trabalhos do banco de dados Elástico** (na visualização), permitem que você defina um grupo de bancos de dados no qual os scripts serão executados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="d3f98-105">Este artigo mostra como toocreate e gerenciar **trabalhos do banco de dados Elástico** usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3f98-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="d3f98-106">Consulte [Visão geral dos trabalhos elásticos](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3f98-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d3f98-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d3f98-107">Prerequisites</span></span>
* <span data-ttu-id="d3f98-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f98-108">An Azure subscription.</span></span> <span data-ttu-id="d3f98-109">Para obter uma avaliação gratuita, confira [Um mês de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3f98-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d3f98-110">Um conjunto de bancos de dados criados com as ferramentas de banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="d3f98-111">Consulte [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d3f98-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="d3f98-112">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f98-112">Azure PowerShell.</span></span> <span data-ttu-id="d3f98-113">Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3f98-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="d3f98-114">**trabalhos de Banco de Dados Elástico** : consulte [Installing trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="d3f98-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="d3f98-115">Selecionar sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="d3f98-115">Select your Azure subscription</span></span>
<span data-ttu-id="d3f98-116">assinatura de saudação tooselect necessário a Id da assinatura (**- SubscriptionId**) ou o nome da assinatura (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="d3f98-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="d3f98-117">Se você tiver várias assinaturas, você pode executar Olá **AzureRmSubscription Get** Olá cmdlet e cópia desejado informações de assinatura do conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="d3f98-118">Uma vez que as informações de assinatura, executar Olá commandlet tooset a seguir esta assinatura como padrão hello, Olá como destino para criar e gerenciar trabalhos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="d3f98-119">Olá [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) é recomendado para uso toodevelop e executar scripts do PowerShell em relação aos trabalhos do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="d3f98-120">Objetos de trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d3f98-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="d3f98-121">Olá a seguinte tabela lista todos os tipos de objeto de saudação do **trabalhos do banco de dados Elástico** junto com sua descrição e relevantes APIs do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3f98-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="d3f98-122">Tipo de objeto</span><span class="sxs-lookup"><span data-stu-id="d3f98-122">Object Type</span></span></th>
    <th><span data-ttu-id="d3f98-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="d3f98-123">Description</span></span></th>
    <th><span data-ttu-id="d3f98-124">APIs do PowerShell relacionadas</span><span class="sxs-lookup"><span data-stu-id="d3f98-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="d3f98-125">Credencial</span><span class="sxs-lookup"><span data-stu-id="d3f98-125">Credential</span></span></td>
    <td><span data-ttu-id="d3f98-126">Nome de usuário e senha toouse ao conectar-se toodatabases para execução de scripts ou aplicativos de DACPACs.</span><span class="sxs-lookup"><span data-stu-id="d3f98-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="d3f98-127">Olá senha é criptografada antes de enviar tooand armazenar no banco de dados de trabalhos do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="d3f98-128">senha de saudação é descriptografada pelo Olá serviço trabalhos Elástico de banco de dados por meio da credencial de saudação criado e carregado a partir de script de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="d3f98-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d3f98-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="d3f98-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d3f98-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="d3f98-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d3f98-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="d3f98-132">Script</span><span class="sxs-lookup"><span data-stu-id="d3f98-132">Script</span></span></td>
    <td><span data-ttu-id="d3f98-133">Toobe de script do Transact-SQL usado para execução em bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="d3f98-134">script Hello deve ser idempotente toobe criados desde que o serviço Olá tentará novamente a execução do script hello após falhas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d3f98-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d3f98-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d3f98-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="d3f98-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d3f98-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d3f98-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d3f98-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="d3f98-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="d3f98-139">DACPAC</span></span></td>
    <td><span data-ttu-id="d3f98-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicativo da camada de dados </a> toobe aplicado em bancos de dados do pacote.</span><span class="sxs-lookup"><span data-stu-id="d3f98-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="d3f98-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d3f98-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d3f98-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d3f98-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d3f98-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d3f98-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="d3f98-144">Destino do Banco de Dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-144">Database Target</span></span></td>
    <td><span data-ttu-id="d3f98-145">Banco de dados e servidor de nome apontando tooan banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d3f98-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="d3f98-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d3f98-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="d3f98-148">Destino do mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="d3f98-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="d3f98-149">Combinação de um destino de banco de dados e toobe uma credencial usada toodetermine informações armazenadas em um mapa de fragmento de banco de dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d3f98-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d3f98-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d3f98-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="d3f98-153">Destino de coleção personalizada</span><span class="sxs-lookup"><span data-stu-id="d3f98-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="d3f98-154">Usar o grupo definido de toocollectively de bancos de dados para execução.</span><span class="sxs-lookup"><span data-stu-id="d3f98-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d3f98-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="d3f98-157">Destino filho de coleção personalizada</span><span class="sxs-lookup"><span data-stu-id="d3f98-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="d3f98-158">Destino do banco de dados que é referenciado em uma coleção personalizada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="d3f98-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="d3f98-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-161">Trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-162">Definição de parâmetros para um trabalho que pode ser usado tootrigger execução ou toofulfill uma agenda.</span><span class="sxs-lookup"><span data-stu-id="d3f98-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d3f98-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="d3f98-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d3f98-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="d3f98-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d3f98-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-166">Execução do Trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-167">Contêiner de toofulfill necessário de tarefas seja executar um script ou aplicando um destino de tooa DACPAC usando as credenciais para conexões de banco de dados com falhas tratadas na política de execução de tooan de acordo.</span><span class="sxs-lookup"><span data-stu-id="d3f98-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-172">Execução de tarefa de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-173">Uma unidade de trabalho toofulfill um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="d3f98-174">Se uma tarefa de trabalho não é capaz de toosuccessfully executar, mensagem de exceção Olá resultante será registrada e uma nova tarefa de trabalho correspondente será criada e executada no acordo toohello especificado política de execução.</span><span class="sxs-lookup"><span data-stu-id="d3f98-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d3f98-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d3f98-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-179">Política de execução de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-180">Controla os tempos limite de execução do trabalho, os limites de repetição e os intervalos entre as tentativas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="d3f98-181">O recurso trabalhos de banco de dados elástico inclui uma política de execução de trabalho padrão que gera, essencialmente, infinitas repetições de tarefas de trabalho com falha, com retirada exponencial de intervalos entre cada repetição.</span><span class="sxs-lookup"><span data-stu-id="d3f98-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d3f98-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="d3f98-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d3f98-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="d3f98-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d3f98-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-185">Agenda</span><span class="sxs-lookup"><span data-stu-id="d3f98-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-186">Especificação de execução tootake local em um intervalo recorrente ou de uma vez com base no tempo.</span><span class="sxs-lookup"><span data-stu-id="d3f98-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d3f98-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="d3f98-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d3f98-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="d3f98-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d3f98-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d3f98-190">Gatilhos de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="d3f98-191">Um mapeamento entre um trabalho e a execução do trabalho tootrigger uma agenda de acordo com o agendamento de toohello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d3f98-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="d3f98-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="d3f98-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="d3f98-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="d3f98-194">Tipos de grupo de trabalhos de Banco de Dados Elástico com suporte</span><span class="sxs-lookup"><span data-stu-id="d3f98-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="d3f98-195">trabalho Olá executa scripts Transact-SQL (T-SQL) ou o aplicativo de DACPACs por meio de um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="d3f98-196">Quando um trabalho é enviado toobe executado em um grupo de bancos de dados, trabalho hello "expande" hello em trabalhos filhos onde cada executa Olá solicitou a execução em um único banco de dados no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="d3f98-197">Há dois tipos de grupos que você pode criar:</span><span class="sxs-lookup"><span data-stu-id="d3f98-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="d3f98-198">[Mapa do fragmento](sql-database-elastic-scale-shard-map-management.md) grupo: quando um trabalho é enviado tootarget um mapa do fragmento, trabalho Olá consultas toodetermine de mapa do fragmento Olá seu conjunto atual de fragmentos e cria filho trabalhos para cada fragmento no mapa do fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="d3f98-199">Grupo Coleção Personalizada: um conjunto personalizado definido de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="d3f98-200">Quando um trabalho tem como alvo uma coleção personalizada, ele cria filho trabalhos para cada banco de dados atualmente na coleção de saudação personalizada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="d3f98-201">Olá tooset conexão de trabalhos do banco de dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d3f98-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="d3f98-202">Precisa de uma conexão toobe conjunto toohello trabalhos *banco de dados de controle* Olá toousing anteriores trabalhos APIs.</span><span class="sxs-lookup"><span data-stu-id="d3f98-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="d3f98-203">Executar este cmdlet dispara um toopop da janela de credencial backup solicitando nome de saudação do usuário e senha criados durante a instalação de trabalhos do banco de dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d3f98-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="d3f98-204">Todos os exemplos fornecidos neste tópico pressupõem que a primeira etapa já foi executada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="d3f98-205">Abra um trabalhos de banco de dados Elástico toohello conexão:</span><span class="sxs-lookup"><span data-stu-id="d3f98-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="d3f98-206">Credenciais criptografadas em trabalhos do banco de dados Elástico Olá</span><span class="sxs-lookup"><span data-stu-id="d3f98-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="d3f98-207">Credenciais de banco de dados podem ser inseridas em trabalhos Olá *banco de dados de controle* com a senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="d3f98-208">É necessário toostore credenciais tooenable trabalhos toobe executado em um momento posterior, (usando agendas de trabalho).</span><span class="sxs-lookup"><span data-stu-id="d3f98-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="d3f98-209">Criptografia funciona por meio de um certificado criado como parte do script de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="d3f98-210">cria o script de instalação Hello e carregamentos certificado Olá Olá serviço de nuvem do Azure para a descriptografia da saudação armazenado senhas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="d3f98-211">Olá posteriormente no serviço de nuvem do Azure armazena a chave pública Olá em trabalhos Olá *banco de dados de controle* que permite Olá API PowerShell ou o Portal clássico do Azure interface tooencrypt uma senha fornecida sem a necessidade de certificado Olá toobe instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="d3f98-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="d3f98-212">senhas de credencial de saudação são criptografados e protegidos contra usuários com objetos de trabalhos de banco de dados de tooElastic acesso somente leitura.</span><span class="sxs-lookup"><span data-stu-id="d3f98-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="d3f98-213">Mas é possível que um usuário mal-intencionado com acesso de leitura-gravação tooElastic trabalhos do banco de dados objetos tooextract uma senha.</span><span class="sxs-lookup"><span data-stu-id="d3f98-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="d3f98-214">As credenciais são projetada toobe reutilizado em execuções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="d3f98-215">As credenciais são passadas tootarget bancos de dados durante o estabelecimento de conexões.</span><span class="sxs-lookup"><span data-stu-id="d3f98-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="d3f98-216">Atualmente, não existem restrições em bancos de dados de destino Olá usados para cada credencial, o usuário mal-intencionado pode adicionar um destino de banco de dados para um banco de dados sob controle do usuário mal-intencionado hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="d3f98-217">usuário Olá subsequentemente foi possível iniciar um trabalho de direcionamento a senha da credencial esse banco de dados toogain hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="d3f98-218">As práticas recomendadas de segurança para o recurso trabalhos de Banco de Dados Elástico incluem:</span><span class="sxs-lookup"><span data-stu-id="d3f98-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="d3f98-219">Limitar o uso de outras pessoas tootrusted APIs de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="d3f98-220">As credenciais devem ter Olá menos privilégios tooperform necessário Olá tarefas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="d3f98-221">Mais informações podem ser vistas dentro desse artigo [Autorização e Permissões](https://msdn.microsoft.com/library/bb669084.aspx) do MSDN do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d3f98-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="d3f98-222">toocreate uma credencial criptografada para a execução de trabalhos em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="d3f98-223">toocreate criptografada de uma nova credencial, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) solicitará um nome de usuário e senha que pode ser passada toohello [ **AzureSqlJobCredential novo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="d3f98-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="d3f98-224">credenciais tooupdate</span><span class="sxs-lookup"><span data-stu-id="d3f98-224">tooupdate credentials</span></span>
<span data-ttu-id="d3f98-225">Ao alterar as senhas, use Olá [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e conjunto hello **CredentialName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d3f98-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="d3f98-226">toodefine um destino de mapa de fragmento de banco de dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d3f98-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="d3f98-227">tooexecute um trabalho em todos os bancos de dados em um conjunto de fragmentos (criada usando [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md)), use um mapa do fragmento como destino de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="d3f98-228">Este exemplo exige um aplicativo de fragmentados criado usando a biblioteca de cliente do banco de dados Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="d3f98-229">Consulte [Introdução ao exemplo de ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d3f98-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="d3f98-230">o banco de dados do Hello fragmento mapa manager deve ser definido como um destino de banco de dados e, em seguida, o mapa de fragmentos específicos Olá deve ser especificado como um destino.</span><span class="sxs-lookup"><span data-stu-id="d3f98-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="d3f98-231">Criar um script T-SQL para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="d3f98-232">Ao criar scripts T-SQL para execução, é altamente recomendável toobuild-los toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) e resilientes a falhas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="d3f98-233">Trabalhos do banco de dados Elásticos tentará novamente a execução de um script sempre que a execução encontrar uma falha, independentemente de classificação de saudação de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="d3f98-234">Saudação de uso [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e salvar um script para execução e definir Olá **- ContentName** e **- CommandText**parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d3f98-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="d3f98-235">Criar um novo script com base em um arquivo</span><span class="sxs-lookup"><span data-stu-id="d3f98-235">Create a new script from a file</span></span>
<span data-ttu-id="d3f98-236">Se Olá script T-SQL é definido dentro de um arquivo, use esse script de saudação tooimport:</span><span class="sxs-lookup"><span data-stu-id="d3f98-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="d3f98-237">script de tooupdate um T-SQL para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="d3f98-238">Essas atualizações de script do PowerShell Olá texto do comando T-SQL para um script existente.</span><span class="sxs-lookup"><span data-stu-id="d3f98-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="d3f98-239">Saudação de conjunto de variáveis tooreflect Olá desejado script definição toobe conjunto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="d3f98-240">script existente de tooan tooupdate Olá definição</span><span class="sxs-lookup"><span data-stu-id="d3f98-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="d3f98-241">toocreate tooexecute um trabalho um script em um mapa do fragmento</span><span class="sxs-lookup"><span data-stu-id="d3f98-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="d3f98-242">Esse script de PowerShell inicia um trabalho para execução de um script em cada fragmento de um mapa de fragmentos de Escala Elástica.</span><span class="sxs-lookup"><span data-stu-id="d3f98-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="d3f98-243">Conjunto Olá Olá de tooreflect variáveis a seguir desejado script e destino:</span><span class="sxs-lookup"><span data-stu-id="d3f98-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="d3f98-244">tooexecute um trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-244">tooexecute a job</span></span>
<span data-ttu-id="d3f98-245">Esse script de PowerShell executa um trabalho existente:</span><span class="sxs-lookup"><span data-stu-id="d3f98-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="d3f98-246">Atualize Olá tooreflect variável Olá desejado trabalho nome toohave executada a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="d3f98-247">estado de saudação tooretrieve uma única de execução do trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="d3f98-248">Saudação de uso [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e conjunto hello **JobExecutionId** estado de saudação do parâmetro tooview de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="d3f98-249">Use Olá mesmo **Get-AzureSqlJobExecution** cmdlet com hello **IncludeChildren** estado de saudação do parâmetro tooview de execuções do trabalho filho, ou seja, Olá estado específico para cada execução do trabalho em relação a cada banco de dados de destino pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="d3f98-250">estado de saudação tooview entre várias execuções de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="d3f98-251">Olá [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tem vários parâmetros opcionais que podem ser usado toodisplay várias execuções de trabalho, filtradas por meio de parâmetros de saudação fornecido.</span><span class="sxs-lookup"><span data-stu-id="d3f98-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="d3f98-252">Olá segue uma demonstração de algumas das maneiras possíveis de saudação toouse AzureSqlJobExecution Get:</span><span class="sxs-lookup"><span data-stu-id="d3f98-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="d3f98-253">Recupere todas as execuções de trabalhos ativos de nível superior:</span><span class="sxs-lookup"><span data-stu-id="d3f98-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="d3f98-254">Recupere todas as execuções do trabalho de nível superior, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="d3f98-255">Recupere todas as execuções de trabalhos filho de uma ID de execução de trabalho fornecida, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="d3f98-256">Recupere todas as execuções de trabalho criadas usando uma combinação de agenda/trabalho, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="d3f98-257">Recupere todos os trabalhos direcionados a um mapa de fragmentos especificado, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="d3f98-258">Recupere todos os trabalhos direcionados a uma coleção personalizada especificada, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d3f98-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="d3f98-259">Recupere a lista de saudação de execuções de tarefa de trabalho em uma execução de trabalho específico:</span><span class="sxs-lookup"><span data-stu-id="d3f98-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="d3f98-260">Recupere detalhes de execução de tarefa de trabalho:</span><span class="sxs-lookup"><span data-stu-id="d3f98-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="d3f98-261">saudação de script do PowerShell a seguir pode ser usado tooview Olá detalhes de uma execução de tarefa do trabalho, é particularmente útil ao depurar falhas de execução.</span><span class="sxs-lookup"><span data-stu-id="d3f98-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="d3f98-262">execuções de tooretrieve falhas no trabalho de tarefas</span><span class="sxs-lookup"><span data-stu-id="d3f98-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="d3f98-263">Olá **JobTaskExecution objeto** inclui uma propriedade para o ciclo de vida de saudação de tarefa Olá junto com uma propriedade de mensagem.</span><span class="sxs-lookup"><span data-stu-id="d3f98-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="d3f98-264">Se uma execução de tarefa de trabalho falhou, propriedade de ciclo de vida de saudação será definida muito*falha* e propriedade de mensagem de saudação definirá toohello mensagem de exceção resultante e sua pilha.</span><span class="sxs-lookup"><span data-stu-id="d3f98-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="d3f98-265">Se um trabalho não foi bem-sucedida, é importante tooview detalhes de Olá das tarefas de trabalho que não teve êxito para um determinado trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="d3f98-266">toowait para um toocomplete de execução do trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="d3f98-267">Olá script do PowerShell a seguir pode ser usado toowait para um toocomplete de tarefa do trabalho:</span><span class="sxs-lookup"><span data-stu-id="d3f98-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="d3f98-268">Criar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="d3f98-268">Create a custom execution policy</span></span>
<span data-ttu-id="d3f98-269">O recurso trabalhos de Banco de Dados Elástico dá suporte à criação de políticas de execução personalizadas, que podem ser aplicadas ao iniciar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d3f98-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="d3f98-270">Atualmente, as políticas de execução permitem definir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="d3f98-271">Nome: O identificador de política de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="d3f98-272">Tempo Limite do Trabalho: tempo total antes que um trabalho seja cancelado pelo recurso Trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d3f98-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="d3f98-273">Intervalo de repetição inicial: Toowait de intervalo antes da primeira nova tentativa.</span><span class="sxs-lookup"><span data-stu-id="d3f98-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="d3f98-274">Intervalo de repetição máximo: Limite de toouse de intervalos de repetição.</span><span class="sxs-lookup"><span data-stu-id="d3f98-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="d3f98-275">Coeficiente de retirada de intervalo de repetição: Coeficiente usado toocalculate Olá próximo intervalo entre repetições.</span><span class="sxs-lookup"><span data-stu-id="d3f98-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="d3f98-276">Olá fórmula a seguir é usada: (intervalo de repetição iniciais) * Math.pow ((coeficiente de retirada de intervalo), (número de tentativas de) - 2).</span><span class="sxs-lookup"><span data-stu-id="d3f98-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="d3f98-277">Máximo de tentativas: número máximo de saudação de tooperform de tentativas de repetição dentro de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="d3f98-278">política de execução padrão Olá usa Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="d3f98-279">Nome: política de execução padrão</span><span class="sxs-lookup"><span data-stu-id="d3f98-279">Name: Default execution policy</span></span>
* <span data-ttu-id="d3f98-280">Tempo Limite do Trabalho: 1 semana</span><span class="sxs-lookup"><span data-stu-id="d3f98-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="d3f98-281">Intervalo de Repetição Inicial: 100 milissegundos</span><span class="sxs-lookup"><span data-stu-id="d3f98-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="d3f98-282">Intervalo Máximo de Repetição: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="d3f98-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="d3f98-283">Coeficiente de Intervalo de Repetição: 2</span><span class="sxs-lookup"><span data-stu-id="d3f98-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="d3f98-284">Máximo de Tentativas: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="d3f98-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="d3f98-285">Crie política de execução de saudação desejada:</span><span class="sxs-lookup"><span data-stu-id="d3f98-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="d3f98-286">Atualizar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="d3f98-286">Update a custom execution policy</span></span>
<span data-ttu-id="d3f98-287">Atualize tooupdate de política de execução de saudação desejada:</span><span class="sxs-lookup"><span data-stu-id="d3f98-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="d3f98-288">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-288">Cancel a job</span></span>
<span data-ttu-id="d3f98-289">O recurso trabalhos de Banco de Dados Elástico dá suporte a solicitações de cancelamento de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d3f98-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="d3f98-290">Se trabalhos de banco de dados Elástico detectar uma solicitação de cancelamento para um trabalho que está sendo executada no momento, ele tentará toostop trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="d3f98-291">Há duas maneiras diferentes pelas quais o recurso Trabalhos de Banco de Dados Elástico pode executar um cancelamento:</span><span class="sxs-lookup"><span data-stu-id="d3f98-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="d3f98-292">Cancelar tarefas em execução atualmente: se um cancelamento for detectado enquanto uma tarefa estiver em execução, um cancelamento será tentado no hello aspecto da tarefa de saudação em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="d3f98-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="d3f98-293">Por exemplo: se houver atualmente sendo executada quando uma tentativa de um cancelamento de consultas de longa execução, haverá uma consulta de saudação toocancel tentativa.</span><span class="sxs-lookup"><span data-stu-id="d3f98-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="d3f98-294">Cancelando tentativas de tarefa: se um cancelamento for detectado pelo thread de controle de saudação antes de uma tarefa é iniciada para execução, a thread de controle de saudação evitar iniciar tarefa hello e declarar solicitação hello como cancelada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="d3f98-295">Se for solicitado um cancelamento de trabalho para um trabalho pai, solicitação de cancelamento hello será respeitada para trabalho de pai hello e para todos os seus trabalhos filho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="d3f98-296">toosubmit uma solicitação de cancelamento, use Olá [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e conjunto hello **JobExecutionId** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d3f98-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="d3f98-297">toodelete um trabalho e o histórico de trabalho assíncrona</span><span class="sxs-lookup"><span data-stu-id="d3f98-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="d3f98-298">O recurso trabalhos de Banco de Dados Elástico dá suporte à exclusão assíncrona de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d3f98-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="d3f98-299">Um trabalho pode ser marcado para exclusão e sistema Olá excluirá trabalho hello e todo o seu histórico de trabalho depois de concluir todas as execuções de trabalho para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3f98-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="d3f98-300">sistema de saudação não cancelará automaticamente execuções de trabalho ativo.</span><span class="sxs-lookup"><span data-stu-id="d3f98-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="d3f98-301">Invocar [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel execuções de trabalho ativo.</span><span class="sxs-lookup"><span data-stu-id="d3f98-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="d3f98-302">exclusão de trabalho tootrigger, use Olá [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e conjunto hello **JobName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d3f98-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="d3f98-303">toocreate um destino de banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="d3f98-303">toocreate a custom database target</span></span>
<span data-ttu-id="d3f98-304">Você pode definir os destinos de banco de dados personalizado para execução direta ou para inclusão em um grupo de bancos de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="d3f98-305">Por exemplo, porque **pools Elásticos** são ainda não suporte direto usando APIs do PowerShell, você pode criar um destino da coleção de banco de dados personalizado que abrange todos os bancos de dados de saudação no pool de saudação e um destino de banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="d3f98-306">Saudação de conjunto de informações de banco de dados variáveis tooreflect Olá desejado a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="d3f98-307">toocreate um destino de coleção do banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="d3f98-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="d3f98-308">Saudação de uso [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet uma execução de tooenable do banco de dados personalizado coleção destino em vários destinos de banco de dados definido.</span><span class="sxs-lookup"><span data-stu-id="d3f98-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="d3f98-309">Depois de criar um grupo de banco de dados, bancos de dados podem ser associados ao destino da coleção personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="d3f98-310">Definir Olá seguinte configuração de destino variáveis tooreflect Olá coleta personalizado desejado:</span><span class="sxs-lookup"><span data-stu-id="d3f98-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="d3f98-311">destino da coleção de banco de dados personalizado tooa tooadd bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="d3f98-312">tooadd um banco de dados tooa específico de coleta personalizado use Olá [ **adicionar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d3f98-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="d3f98-313">Revisão Olá bancos de dados dentro de um destino de coleção do banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="d3f98-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="d3f98-314">Saudação de uso [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) bancos de dados do cmdlet tooretrieve Olá filho dentro de um destino de coleção do banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="d3f98-315">Criar um script de um trabalho tooexecute em um destino de coleção do banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="d3f98-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="d3f98-316">Saudação de uso [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet um trabalho para um grupo de bancos de dados definidos por um destino de coleção do banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="d3f98-317">Trabalhos do banco de dados Elásticos expandirá trabalho Olá para vários trabalhos filho, cada banco de dados tooa correspondente associada ao destino de coleção de banco de dados personalizado hello e certifique-se de que o script hello é executada em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="d3f98-318">Novamente, é importante que os scripts são idempotentes toobe resiliente tooretries.</span><span class="sxs-lookup"><span data-stu-id="d3f98-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="d3f98-319">Coleta de dados em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-319">Data collection across databases</span></span>
<span data-ttu-id="d3f98-320">Você pode usar um trabalho tooexecute uma consulta em um grupo de bancos de dados e enviar Olá resultados tooa tabela.</span><span class="sxs-lookup"><span data-stu-id="d3f98-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="d3f98-321">tabela Olá pode ser consultada depois dos resultados da consulta do hello fatos toosee Olá de cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="d3f98-322">Isso fornece um método assíncrono tooexecute uma consulta em muitos bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="d3f98-323">Tentativas fracassadas são processadas automaticamente por meio de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="d3f98-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="d3f98-324">tabela de destino especificado Olá será criada automaticamente se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="d3f98-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="d3f98-325">nova tabela de saudação coincide com o esquema de saudação do hello retornada um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="d3f98-326">Se um script retornar vários conjuntos de resultados, os trabalhos de banco de dados Elástico enviará apenas primeira tabela de destino toohello hello.</span><span class="sxs-lookup"><span data-stu-id="d3f98-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="d3f98-327">Olá seguinte script do PowerShell executa um script e coleta seus resultados em uma tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="d3f98-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="d3f98-328">Esse script presume que foi criado um script T-SQL, que produz um único conjunto de resultados, e que um destino de coleção de bancos de dados personalizada foi criado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="d3f98-329">Esse script usa Olá [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d3f98-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="d3f98-330">Defina os parâmetros de saudação de script, credenciais e o destino de execução:</span><span class="sxs-lookup"><span data-stu-id="d3f98-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="d3f98-331">toocreate e iniciar um trabalho para cenários de coleta de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="d3f98-332">Esse script usa Olá [ **início AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d3f98-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="d3f98-333">tooschedule um gatilho de execução do trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="d3f98-334">saudação de script do PowerShell a seguir pode ser usado toocreate um agendamento recorrente.</span><span class="sxs-lookup"><span data-stu-id="d3f98-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="d3f98-335">Esse script usa um intervalo de minutos, mas o [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) também dá suporte aos parâmetros -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="d3f98-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="d3f98-336">Agendas que são executadas apenas uma vez podem ser criadas pela passagem de -OneTime.</span><span class="sxs-lookup"><span data-stu-id="d3f98-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="d3f98-337">Crie uma nova agenda:</span><span class="sxs-lookup"><span data-stu-id="d3f98-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="d3f98-338">tootrigger um trabalho executado em um agendamento de tempo</span><span class="sxs-lookup"><span data-stu-id="d3f98-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="d3f98-339">Um gatilho de trabalho pode ser definido toohave um agendamento de tempo de tooa acordo do trabalho executado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="d3f98-340">saudação de script do PowerShell a seguir pode ser usado toocreate um gatilho de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d3f98-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="d3f98-341">Use [AzureSqlJobTrigger novo](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e saudação do conjunto de variáveis toocorrespond toohello desejado trabalho e uma agenda a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3f98-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="d3f98-342">tooremove um trabalho de toostop associação agendados sejam executados na agenda</span><span class="sxs-lookup"><span data-stu-id="d3f98-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="d3f98-343">toodiscontinue ocorrer a execução de trabalho por meio de um gatilho de trabalho, o gatilho de trabalho Olá pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="d3f98-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="d3f98-344">Remover um gatilho de trabalho toostop um trabalho seja executado acordo agenda tooa usando Olá [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="d3f98-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="d3f98-345">Recuperar o agendamento de tempo de tooa associada de gatilhos de trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="d3f98-346">Olá script do PowerShell a seguir pode ser usado tooobtain e exibir agendamento de tempo específico Olá trabalho gatilhos tooa registrado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="d3f98-347">gatilhos de trabalho tooretrieve associado tooa trabalho</span><span class="sxs-lookup"><span data-stu-id="d3f98-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="d3f98-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e Exibir agendas que contém um trabalho registrado.</span><span class="sxs-lookup"><span data-stu-id="d3f98-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="d3f98-349">toocreate um aplicativo da camada de dados (DACPAC) para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="d3f98-350">toocreate um DACPAC, consulte [aplicativos da camada de dados](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3f98-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="d3f98-351">toodeploy um DACPAC, use Olá [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="d3f98-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="d3f98-352">Olá DACPAC deve ser acessível toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="d3f98-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="d3f98-353">É recomendável tooupload um tooAzure DACPAC criado armazenamento e criar um [assinatura de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para Olá DACPAC.</span><span class="sxs-lookup"><span data-stu-id="d3f98-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="d3f98-354">tooupdate um aplicativo da camada de dados (DACPAC) para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="d3f98-355">DACPACs existentes registrados em trabalhos Elástico de banco de dados podem ser atualizado toopoint toonew URIs.</span><span class="sxs-lookup"><span data-stu-id="d3f98-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="d3f98-356">Saudação de uso [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate Olá URI DACPAC em um existente registrado DACPAC:</span><span class="sxs-lookup"><span data-stu-id="d3f98-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="d3f98-357">toocreate tooapply um trabalho um aplicativo da camada de dados (DACPAC) em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d3f98-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="d3f98-358">Depois de um DACPAC foi criado no trabalhos Elástico de banco de dados, um trabalho pode ser criado Olá tooapply DACPAC em um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d3f98-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="d3f98-359">saudação de script do PowerShell a seguir pode ser usado toocreate um trabalho DACPAC em um conjunto personalizado de bancos de dados:</span><span class="sxs-lookup"><span data-stu-id="d3f98-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
