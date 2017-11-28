---
title: "Criar e gerenciar trabalhos elásticos usando o PowerShell | Microsoft Docs"
description: PowerShell usado para gerenciar pools do Banco de Dados SQL do Azure
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="d62e8-103">Criar e gerenciar trabalhos elástico do Banco de Dados SQL usando o PowerShell (visualização)</span><span class="sxs-lookup"><span data-stu-id="d62e8-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="d62e8-104">As APIs do PowerShell para o recurso **trabalhos de Banco de Dados Elástico** (em visualização) permitem que você defina um grupo de bancos de dados no qual os scripts serão executados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="d62e8-105">Este artigo mostra como criar e gerenciar o recurso **trabalhos de Banco de Dados Elástico** usando cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d62e8-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="d62e8-106">Consulte [Visão geral dos trabalhos elásticos](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d62e8-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d62e8-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d62e8-107">Prerequisites</span></span>
* <span data-ttu-id="d62e8-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d62e8-108">An Azure subscription.</span></span> <span data-ttu-id="d62e8-109">Para obter uma avaliação gratuita, confira [Um mês de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d62e8-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d62e8-110">Um conjunto de bancos de dados criados com as ferramentas do Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="d62e8-111">Consulte [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d62e8-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="d62e8-112">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="d62e8-112">Azure PowerShell.</span></span> <span data-ttu-id="d62e8-113">Para obter informações detalhadas, confira [Como instalar e configurar o PowerShell do Azure](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d62e8-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="d62e8-114">**trabalhos de Banco de Dados Elástico** : consulte [Installing trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="d62e8-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="d62e8-115">Selecionar sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="d62e8-115">Select your Azure subscription</span></span>
<span data-ttu-id="d62e8-116">Para selecionar a assinatura é necessário ter a ID ou o nome da assinatura (**-SubscriptionId** ou **-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="d62e8-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="d62e8-117">Se você tiver várias assinaturas, poderá executar o cmdlet **Get-AzureRmSubscription** e copiar as informações da assinatura desejada do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="d62e8-118">Uma vez que você tenha suas informações de assinatura, execute o cmdlet a seguir para definir esta assinatura como padrão, ou seja, o destino para a criação e gerenciamento de trabalhos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="d62e8-119">O uso do [ISE do PowerShell](https://technet.microsoft.com/library/dd315244.aspx) é recomendado ao desenvolver e executar scripts do PowerShell em trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="d62e8-120">Objetos de trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d62e8-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="d62e8-121">A tabela a seguir lista todos os tipos de objeto de **trabalhos de Banco de Dados Elástico** junto com sua descrição e as APIs do PowerShell relevantes.</span><span class="sxs-lookup"><span data-stu-id="d62e8-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="d62e8-122">Tipo de objeto</span><span class="sxs-lookup"><span data-stu-id="d62e8-122">Object Type</span></span></th>
    <th><span data-ttu-id="d62e8-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="d62e8-123">Description</span></span></th>
    <th><span data-ttu-id="d62e8-124">APIs do PowerShell relacionadas</span><span class="sxs-lookup"><span data-stu-id="d62e8-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="d62e8-125">Credencial</span><span class="sxs-lookup"><span data-stu-id="d62e8-125">Credential</span></span></td>
    <td><span data-ttu-id="d62e8-126">Nome de usuário e senha para usar ao se conectar a bancos de dados para execução de scripts ou aplicação de DACPACs.</span><span class="sxs-lookup"><span data-stu-id="d62e8-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="d62e8-127">A senha é criptografada antes de enviar para e armazenar no banco de dados de trabalhos de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="d62e8-128">A senha é descriptografada pelo serviço trabalhos de Banco de Dados Elástico por meio da credencial criada e carregada por meio do script de instalação.</span><span class="sxs-lookup"><span data-stu-id="d62e8-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="d62e8-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d62e8-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="d62e8-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d62e8-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="d62e8-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="d62e8-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="d62e8-132">Script</span><span class="sxs-lookup"><span data-stu-id="d62e8-132">Script</span></span></td>
    <td><span data-ttu-id="d62e8-133">O script do Transact-SQL a ser usado para execução em bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="d62e8-134">O script deve ser criado para ser idempotente, já que o serviço tentará novamente executar o script após a ocorrência de quaisquer falhas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d62e8-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d62e8-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d62e8-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="d62e8-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d62e8-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d62e8-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d62e8-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="d62e8-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="d62e8-139">DACPAC</span></span></td>
    <td><span data-ttu-id="d62e8-140">O pacote de <a href="https://msdn.microsoft.com/library/ee210546.aspx">aplicativo da camada de dados</a> a ser aplicado a bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="d62e8-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d62e8-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d62e8-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="d62e8-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="d62e8-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="d62e8-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="d62e8-144">Destino do Banco de Dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-144">Database Target</span></span></td>
    <td><span data-ttu-id="d62e8-145">Nome do banco de dados e do servidor apontando para um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="d62e8-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="d62e8-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d62e8-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="d62e8-148">Destino do mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="d62e8-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="d62e8-149">Combinação de um destino de banco de dados e uma credencial a ser usada para determinar as informações armazenadas em um mapa de fragmentos de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d62e8-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d62e8-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="d62e8-153">Destino de coleção personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="d62e8-154">Grupo definido de bancos de dados a serem usados coletivamente para execução.</span><span class="sxs-lookup"><span data-stu-id="d62e8-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="d62e8-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="d62e8-157">Destino filho de coleção personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="d62e8-158">Destino do banco de dados que é referenciado em uma coleção personalizada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="d62e8-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="d62e8-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-161">Trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-162">Definição de parâmetros para um trabalho que pode ser usado para disparar a execução ou para atender a um cronograma.</span><span class="sxs-lookup"><span data-stu-id="d62e8-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d62e8-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="d62e8-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d62e8-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="d62e8-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="d62e8-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-166">Execução do Trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-167">Contêiner de tarefas necessárias para a execução de um script ou então para a aplicação de um DACPAC em um destino usando credenciais para conexões de banco de dados com falhas tratadas de acordo com uma política de execução.</span><span class="sxs-lookup"><span data-stu-id="d62e8-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-172">Execução de tarefa de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-173">Unidade de trabalho individual para concluir um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="d62e8-174">Se uma tarefa de trabalho não for capaz de executar com êxito, a mensagem de exceção resultante será registrada e uma nova tarefa de trabalho correspondente será criada e executada de acordo com a política de execução especificada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="d62e8-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="d62e8-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-179">Política de execução de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-180">Controla os tempos limite de execução do trabalho, os limites de repetição e os intervalos entre as tentativas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="d62e8-181">O recurso trabalhos de banco de dados elástico inclui uma política de execução de trabalho padrão que gera, essencialmente, infinitas repetições de tarefas de trabalho com falha, com retirada exponencial de intervalos entre cada repetição.</span><span class="sxs-lookup"><span data-stu-id="d62e8-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d62e8-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="d62e8-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d62e8-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="d62e8-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="d62e8-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-185">Agenda</span><span class="sxs-lookup"><span data-stu-id="d62e8-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-186">Especificação baseada em tempo para execução, a ocorrer em um intervalo recorrente ou uma única vez.</span><span class="sxs-lookup"><span data-stu-id="d62e8-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d62e8-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="d62e8-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d62e8-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="d62e8-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="d62e8-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="d62e8-190">Gatilhos de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="d62e8-191">Um mapeamento entre um trabalho e um cronograma, para disparar a execução do trabalho de acordo com esse cronograma.</span><span class="sxs-lookup"><span data-stu-id="d62e8-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="d62e8-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="d62e8-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="d62e8-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="d62e8-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="d62e8-194">Tipos de grupo de trabalhos de Banco de Dados Elástico com suporte</span><span class="sxs-lookup"><span data-stu-id="d62e8-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="d62e8-195">O trabalho executa os scripts Transact-SQL (T-SQL) ou o aplicativo de DACPACs em um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="d62e8-196">Quando um trabalho for enviado para ser executado em um grupo de bancos de dados, o trabalho se “expandirá” em trabalhos filhos, onde cada um deles realizará a execução solicitada em um único banco de dados no grupo.</span><span class="sxs-lookup"><span data-stu-id="d62e8-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="d62e8-197">Há dois tipos de grupos que você pode criar:</span><span class="sxs-lookup"><span data-stu-id="d62e8-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="d62e8-198">[Mapa de Fragmentos](sql-database-elastic-scale-shard-map-management.md) : quando um trabalho é enviado para um mapa de fragmentos, o trabalho consulta o mapa de fragmentos para determinar seu conjunto atual de fragmentos e cria trabalhos filho para cada fragmento no mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="d62e8-199">Grupo Coleção Personalizada: um conjunto personalizado definido de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="d62e8-200">Quando um trabalho tem como alvo uma coleção personalizada, ele cria trabalhos filho para cada banco de dados atualmente na coleção personalizada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="d62e8-201">Para definir a conexão com o recurso trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d62e8-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="d62e8-202">Uma conexão deve ser definida para o *banco de dados de controle* dos trabalhos antes de usar as APIs dos trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="d62e8-203">Executar esse cmdlet dispara uma janela de credencial para solicitar o nome de usuário e a senha criados durante a instalação do recurso trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="d62e8-204">Todos os exemplos fornecidos neste tópico pressupõem que a primeira etapa já foi executada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="d62e8-205">Abrir uma conexão ao recurso trabalhos de Banco de Dados Elástico:</span><span class="sxs-lookup"><span data-stu-id="d62e8-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="d62e8-206">Credenciais criptografadas no recurso trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d62e8-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="d62e8-207">As credenciais do banco de dados podem ser inseridas no *banco de dados de controle* dos trabalhos com a sua senha criptografada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="d62e8-208">É necessário armazenar as credenciais para habilitar os trabalhos que serão executados posteriormente (usando planos de trabalho).</span><span class="sxs-lookup"><span data-stu-id="d62e8-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="d62e8-209">Criptografia funciona por meio de um certificado criado como parte do script de instalação.</span><span class="sxs-lookup"><span data-stu-id="d62e8-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="d62e8-210">O script de instalação cria e carrega o certificado no Serviço de Nuvem do Azure para descriptografia das senhas criptografadas armazenadas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="d62e8-211">O Serviço de Nuvem do Azure armazena posteriormente a chave pública no *banco de dados de controle* dos trabalhos, o que permite que a interface do Portal Clássico do Azure ou a API do PowerShell criptografe uma senha fornecida sem exigir que o certificado seja instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="d62e8-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="d62e8-212">As senhas das credenciais são criptografadas e protegidas contra usuários com acesso somente leitura a objetos do recurso trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="d62e8-213">Mas é possível que um usuário mal-intencionado com acesso de leitura/gravação aos objetos do recurso trabalhos de Banco de Dados Elástico extraia uma senha.</span><span class="sxs-lookup"><span data-stu-id="d62e8-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="d62e8-214">As credenciais são projetadas para ser reutilizadas em execuções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="d62e8-215">As credenciais são passadas aos bancos de dados de destino durante o estabelecimento de conexões.</span><span class="sxs-lookup"><span data-stu-id="d62e8-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="d62e8-216">Atualmente, não existem restrições nos bancos de dados de destino usados para cada credencial. Um usuário mal-intencionado poderia adicionar um destino de banco de dados a um banco de dados sob o controle do usuário mal-intencionado.</span><span class="sxs-lookup"><span data-stu-id="d62e8-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="d62e8-217">O usuário poderia em seguida iniciar um trabalho visando esse banco de dados para obter a senha da credencial.</span><span class="sxs-lookup"><span data-stu-id="d62e8-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="d62e8-218">As práticas recomendadas de segurança para o recurso trabalhos de Banco de Dados Elástico incluem:</span><span class="sxs-lookup"><span data-stu-id="d62e8-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="d62e8-219">Limite o uso das APIs somente a pessoas confiáveis.</span><span class="sxs-lookup"><span data-stu-id="d62e8-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="d62e8-220">As credenciais devem ter os privilégios mínimos necessários para executar a tarefa de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="d62e8-221">Mais informações podem ser vistas dentro desse artigo [Autorização e Permissões](https://msdn.microsoft.com/library/bb669084.aspx) do MSDN do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d62e8-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="d62e8-222">Para criar uma credencial criptografada para a execução de trabalhos nos bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="d62e8-223">Para criar uma nova credencial criptografada, o cmdlet [**Get-Credential**](https://technet.microsoft.com/library/hh849815.aspx) solicita um nome de usuário e senha que podem ser passados para o cmdlet [**New-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="d62e8-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="d62e8-224">Para atualizar as credenciais</span><span class="sxs-lookup"><span data-stu-id="d62e8-224">To update credentials</span></span>
<span data-ttu-id="d62e8-225">Quando alterar as senhas, use o cmdlet [**Set-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e defina o parâmetro **CredentialName**.</span><span class="sxs-lookup"><span data-stu-id="d62e8-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="d62e8-226">Para definir um destino para o mapa de fragmentos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="d62e8-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="d62e8-227">Para executar um trabalho em todos os bancos de dados em um conjunto de fragmentos (criado usando a [biblioteca do cliente de Banco de Dados Elástico](sql-database-elastic-database-client-library.md)) use um mapa de fragmentos como destino para o bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="d62e8-228">Este exemplo requer que você crie um aplicativo fragmentado usando a biblioteca do cliente de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="d62e8-229">Consulte [Introdução ao exemplo de ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d62e8-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="d62e8-230">O banco de dados do gerenciador do mapa de fragmentos deve ser definido como um destino de banco de dados e, em seguida, o mapa de fragmentos específico deve ser especificado como um destino.</span><span class="sxs-lookup"><span data-stu-id="d62e8-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="d62e8-231">Criar um script T-SQL para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="d62e8-232">Ao criar scripts T-SQL para execução, é altamente recomendável criá-los para que sejam [idempotentes](https://en.wikipedia.org/wiki/Idempotence) e resistentes contra falhas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="d62e8-233">O recurso trabalhos de Banco de Dados Elástico tentará novamente a execução de um script sempre que ocorrer uma falha nessa execução, independentemente da classificação da falha.</span><span class="sxs-lookup"><span data-stu-id="d62e8-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="d62e8-234">Use o cmdlet [**New-AzureSqlJobContent**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) para criar e salvar um script para execução e defina os parâmetros **-ContentName** e **-CommandText**.</span><span class="sxs-lookup"><span data-stu-id="d62e8-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="d62e8-235">Criar um novo script com base em um arquivo</span><span class="sxs-lookup"><span data-stu-id="d62e8-235">Create a new script from a file</span></span>
<span data-ttu-id="d62e8-236">Se o script T-SQL é definido dentro de um arquivo, use-o para importar o script:</span><span class="sxs-lookup"><span data-stu-id="d62e8-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="d62e8-237">Para atualizar um script T-SQL para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="d62e8-238">Esse script de PowerShell atualiza o texto do comando T-SQL para um script existente.</span><span class="sxs-lookup"><span data-stu-id="d62e8-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="d62e8-239">Defina as variáveis a seguir para refletirem a definição de script que deseja configurar:</span><span class="sxs-lookup"><span data-stu-id="d62e8-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="d62e8-240">Para atualizar a definição para um script existente</span><span class="sxs-lookup"><span data-stu-id="d62e8-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="d62e8-241">Para criar um trabalho para executar um script em um mapa de fragmentos</span><span class="sxs-lookup"><span data-stu-id="d62e8-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="d62e8-242">Esse script de PowerShell inicia um trabalho para execução de um script em cada fragmento de um mapa de fragmentos de Escala Elástica.</span><span class="sxs-lookup"><span data-stu-id="d62e8-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="d62e8-243">Defina as variáveis a seguir para refletirem a definição de script e o destino desejados:</span><span class="sxs-lookup"><span data-stu-id="d62e8-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="d62e8-244">Para executar um trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-244">To execute a job</span></span>
<span data-ttu-id="d62e8-245">Esse script de PowerShell executa um trabalho existente:</span><span class="sxs-lookup"><span data-stu-id="d62e8-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="d62e8-246">Atualize a variável a seguir para refletir o nome do trabalho desejado a ser executado:</span><span class="sxs-lookup"><span data-stu-id="d62e8-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="d62e8-247">Para recuperar o estado de uma única execução de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="d62e8-248">Use o cmdlet [**Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e defina o parâmetro **JobExecutionId** para exibir o estado de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="d62e8-249">Use o mesmo cmdlet **Get-AzureSqlJobExecution** com o parâmetro **IncludeChildren** para exibir o estado de execuções de trabalhos filho, ou seja, o estado específico de cada execução do trabalho em relação a cada banco de dados a que o trabalho se destina.</span><span class="sxs-lookup"><span data-stu-id="d62e8-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="d62e8-250">Para exibir o estado em várias execuções de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="d62e8-251">O cmdlet [**Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/new-azuresqljob) tem vários parâmetros opcionais que podem ser usados para exibir várias execuções de trabalho, filtradas por meio dos parâmetros fornecidos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="d62e8-252">O exemplo a seguir demonstra algumas das possíveis maneiras de usar o Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="d62e8-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="d62e8-253">Recupere todas as execuções de trabalhos ativos de nível superior:</span><span class="sxs-lookup"><span data-stu-id="d62e8-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="d62e8-254">Recupere todas as execuções do trabalho de nível superior, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="d62e8-255">Recupere todas as execuções de trabalhos filho de uma ID de execução de trabalho fornecida, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="d62e8-256">Recupere todas as execuções de trabalho criadas usando uma combinação de agenda/trabalho, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="d62e8-257">Recupere todos os trabalhos direcionados a um mapa de fragmentos especificado, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="d62e8-258">Recupere todos os trabalhos direcionados a uma coleção personalizada especificada, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="d62e8-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="d62e8-259">Recupere a lista de execuções de tarefas de trabalho contidas na execução de um trabalho específico:</span><span class="sxs-lookup"><span data-stu-id="d62e8-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="d62e8-260">Recupere detalhes de execução de tarefa de trabalho:</span><span class="sxs-lookup"><span data-stu-id="d62e8-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="d62e8-261">O script do PowerShell a seguir pode ser usado para exibir os detalhes de uma execução de tarefa de trabalho, o que é especialmente útil ao depurar falhas de execução.</span><span class="sxs-lookup"><span data-stu-id="d62e8-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="d62e8-262">Para recuperar falhas em execuções de tarefa de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="d62e8-263">O objeto **JobTaskExecution** inclui uma propriedade para o ciclo de vida da tarefa, junto com uma propriedade de mensagem.</span><span class="sxs-lookup"><span data-stu-id="d62e8-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="d62e8-264">Se uma execução de tarefa de trabalho falhar, a propriedade de ciclo de vida será definida como *Falha* , e a propriedade de mensagem será definida como a mensagem de exceção resultante e sua pilha.</span><span class="sxs-lookup"><span data-stu-id="d62e8-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="d62e8-265">Se um trabalho não foi bem-sucedido, é importante exibir os detalhes das tarefas de trabalho que não foram bem-sucedidas para um determinado trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="d62e8-266">Para aguardar a conclusão da execução de um trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="d62e8-267">O script do PowerShell a seguir pode ser usado para aguardar a conclusão de uma tarefa de trabalho:</span><span class="sxs-lookup"><span data-stu-id="d62e8-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="d62e8-268">Criar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-268">Create a custom execution policy</span></span>
<span data-ttu-id="d62e8-269">O recurso trabalhos de Banco de Dados Elástico dá suporte à criação de políticas de execução personalizadas, que podem ser aplicadas ao iniciar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="d62e8-270">Atualmente, as políticas de execução permitem definir:</span><span class="sxs-lookup"><span data-stu-id="d62e8-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="d62e8-271">Nome: o identificador para a política de execução.</span><span class="sxs-lookup"><span data-stu-id="d62e8-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="d62e8-272">Tempo Limite do Trabalho: tempo total antes que um trabalho seja cancelado pelo recurso Trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="d62e8-273">Intervalo de Repetição Inicial: o intervalo de espera antes de primeira repetição de tentativa.</span><span class="sxs-lookup"><span data-stu-id="d62e8-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="d62e8-274">Intervalo Máximo de Repetição: limite de intervalos de repetição a usar.</span><span class="sxs-lookup"><span data-stu-id="d62e8-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="d62e8-275">Coeficiente de Retirada de Intervalo de Repetição: coeficiente usado para calcular o próximo intervalo entre as repetições de tentativas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="d62e8-276">A fórmula a seguir é usada: (Intervalo de Repetição Inicial) * Math.pow((Coeficiente de Retirada do Intervalo), (Número de Novas Tentativas) - 2).</span><span class="sxs-lookup"><span data-stu-id="d62e8-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="d62e8-277">Máximo de Tentativas: o número máximo de novas tentativas a repetir em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="d62e8-278">A política de execução padrão usa os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="d62e8-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="d62e8-279">Nome: política de execução padrão</span><span class="sxs-lookup"><span data-stu-id="d62e8-279">Name: Default execution policy</span></span>
* <span data-ttu-id="d62e8-280">Tempo Limite do Trabalho: 1 semana</span><span class="sxs-lookup"><span data-stu-id="d62e8-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="d62e8-281">Intervalo de Repetição Inicial: 100 milissegundos</span><span class="sxs-lookup"><span data-stu-id="d62e8-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="d62e8-282">Intervalo Máximo de Repetição: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="d62e8-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="d62e8-283">Coeficiente de Intervalo de Repetição: 2</span><span class="sxs-lookup"><span data-stu-id="d62e8-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="d62e8-284">Máximo de Tentativas: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="d62e8-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="d62e8-285">Crie a política de execução desejada:</span><span class="sxs-lookup"><span data-stu-id="d62e8-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="d62e8-286">Atualizar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-286">Update a custom execution policy</span></span>
<span data-ttu-id="d62e8-287">Atualize a política de execução que deseja atualizar:</span><span class="sxs-lookup"><span data-stu-id="d62e8-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="d62e8-288">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-288">Cancel a job</span></span>
<span data-ttu-id="d62e8-289">O recurso trabalhos de Banco de Dados Elástico dá suporte a solicitações de cancelamento de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="d62e8-290">Se o recurso trabalhos de Banco de Dados Elástico detecta uma solicitação de cancelamento de um trabalho que está atualmente em execução, ele tenta interromper o trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="d62e8-291">Há duas maneiras diferentes pelas quais o recurso Trabalhos de Banco de Dados Elástico pode executar um cancelamento:</span><span class="sxs-lookup"><span data-stu-id="d62e8-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="d62e8-292">Cancelar tarefas atualmente em execução: se um cancelamento for detectado enquanto uma tarefa estiver em execução, será realizada uma tentativa de cancelamento no aspecto da tarefa atualmente em execução.</span><span class="sxs-lookup"><span data-stu-id="d62e8-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="d62e8-293">Por exemplo: se houver uma consulta de execução longa sendo executada atualmente, quando houver uma tentativa de cancelamento, haverá também uma tentativa de cancelar a consulta.</span><span class="sxs-lookup"><span data-stu-id="d62e8-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="d62e8-294">Tentativas de cancelar tarefa: se um cancelamento for detectado pelo thread de controle antes de uma tarefa ser iniciada para execução, o thread de controle evitará iniciar a tarefa e declarará a solicitação como cancelada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="d62e8-295">Se for solicitado um cancelamento de trabalho para um trabalho pai, a solicitação de cancelamento será atendida para o trabalho pai e todos os seus trabalhos filho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="d62e8-296">Para enviar uma solicitação de cancelamento, use o cmdlet [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e defina o parâmetro **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="d62e8-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="d62e8-297">Para excluir um trabalho e o histórico do trabalho de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="d62e8-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="d62e8-298">O recurso trabalhos de Banco de Dados Elástico dá suporte à exclusão assíncrona de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="d62e8-299">Um trabalho pode ser marcado para exclusão e o sistema vai excluir o trabalho e todo o seu histórico de trabalho, depois que todas as execuções de trabalho para o trabalho em questão tenham sido concluídas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="d62e8-300">O sistema não cancelará automaticamente execuções de trabalhos ativos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="d62e8-301">Invoque [**Stop AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) para cancelar as execuções do trabalho ativo.</span><span class="sxs-lookup"><span data-stu-id="d62e8-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="d62e8-302">Para disparar a exclusão de trabalho, use o cmdlet [**Remove-AzureSqlJob**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e defina o parâmetro **JobName**.</span><span class="sxs-lookup"><span data-stu-id="d62e8-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="d62e8-303">Para criar um destino de banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="d62e8-303">To create a custom database target</span></span>
<span data-ttu-id="d62e8-304">Você pode definir os destinos de banco de dados personalizado para execução direta ou para inclusão em um grupo de bancos de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="d62e8-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="d62e8-305">Por exemplo, como os **pools elásticos** ainda não têm suporte direto usando as APIs do PowerShell, você pode criar um destino de banco de dados personalizado e um destino de coleção de bancos de dados personalizado que englobe todos os bancos de dados no pool.</span><span class="sxs-lookup"><span data-stu-id="d62e8-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="d62e8-306">Defina as variáveis a seguir para refletirem as informações de banco de dados desejadas:</span><span class="sxs-lookup"><span data-stu-id="d62e8-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="d62e8-307">Para criar um destino para a coleção de bancos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-307">To create a custom database collection target</span></span>
<span data-ttu-id="d62e8-308">Use o cmdlet [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) para definir um destino de coleção de banco de dados personalizada para habilitar a execução em vários destinos de banco de dados definidos.</span><span class="sxs-lookup"><span data-stu-id="d62e8-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="d62e8-309">Após criar um grupo de banco de dados,os bancos de dados podem ser associados ao destino da coleção personalizada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="d62e8-310">Defina as variáveis a seguir para refletir a configuração desejada para destino da coleção personalizada:</span><span class="sxs-lookup"><span data-stu-id="d62e8-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="d62e8-311">Para adicionar bancos de dados a um destino da coleção de bancos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="d62e8-312">Para adicionar um banco de dados a uma coleção personalizada específica, use o cmdlet [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget).</span><span class="sxs-lookup"><span data-stu-id="d62e8-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="d62e8-313">Examinar os bancos de dados contidos em um destino de coleção de bancos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="d62e8-314">Use o cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) para recuperar os bancos de dados filho dentro de um destino de coleção de bancos de dados personalizada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="d62e8-315">Criar um trabalho para executar um script em um destino de coleção de bancos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="d62e8-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="d62e8-316">Use o cmdlet [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) para criar um trabalho para um grupo de bancos de dados definidos por um destino de coleção de bancos de dados personalizada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="d62e8-317">O recurso trabalhos de Banco de Dados Elástico  expandirá o trabalho em vários trabalhos filho, cada um correspondendo a um banco de dados associado ao destino de coleção de bancos de dados personalizada e assegurando que o script seja executado em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="d62e8-318">Novamente, é importante que os scripts sejam idempotentes para que sejam resistentes em relação a novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="d62e8-319">Coleta de dados em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-319">Data collection across databases</span></span>
<span data-ttu-id="d62e8-320">Você pode usar um trabalho para executar uma consulta em um grupo de bancos de dados e enviar os resultados para uma tabela específica.</span><span class="sxs-lookup"><span data-stu-id="d62e8-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="d62e8-321">A tabela pode ser consultada após o fato para ver os resultados da consulta provenientes de cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="d62e8-322">Isso fornece um método assíncrono para executar uma consulta em vários bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="d62e8-323">Tentativas fracassadas são processadas automaticamente por meio de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="d62e8-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="d62e8-324">A tabela de destino especificada será criada automaticamente se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="d62e8-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="d62e8-325">A nova tabela coincide com o esquema do conjunto de resultados retornado.</span><span class="sxs-lookup"><span data-stu-id="d62e8-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="d62e8-326">Se um script retornar vários conjuntos de resultados, o recurso trabalhos de Banco de Dados Elástico enviará somente o primeiro à tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="d62e8-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="d62e8-327">O script de PowerShell a seguir executa um script e coleta os resultados em uma tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="d62e8-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="d62e8-328">Esse script presume que foi criado um script T-SQL, que produz um único conjunto de resultados, e que um destino de coleção de bancos de dados personalizada foi criado.</span><span class="sxs-lookup"><span data-stu-id="d62e8-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="d62e8-329">Esse script usa o cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget).</span><span class="sxs-lookup"><span data-stu-id="d62e8-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="d62e8-330">Defina os parâmetros para script, credenciais e destino de execução:</span><span class="sxs-lookup"><span data-stu-id="d62e8-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="d62e8-331">Para criar e iniciar um trabalho para cenários de coleta de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="d62e8-332">Esse script usa o cmdlet [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution).</span><span class="sxs-lookup"><span data-stu-id="d62e8-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="d62e8-333">Para agendar um gatilho de execução de trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="d62e8-334">O script de PowerShell a seguir pode ser usado para criar uma agenda recorrente.</span><span class="sxs-lookup"><span data-stu-id="d62e8-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="d62e8-335">Esse script usa um intervalo de minutos, mas o [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) também dá suporte aos parâmetros -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="d62e8-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="d62e8-336">Agendas que são executadas apenas uma vez podem ser criadas pela passagem de -OneTime.</span><span class="sxs-lookup"><span data-stu-id="d62e8-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="d62e8-337">Crie uma nova agenda:</span><span class="sxs-lookup"><span data-stu-id="d62e8-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="d62e8-338">Para disparar um trabalho executado em um cronograma</span><span class="sxs-lookup"><span data-stu-id="d62e8-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="d62e8-339">Um gatilho de trabalho pode ser definido para fazer com que um trabalho seja executado segundo um cronograma.</span><span class="sxs-lookup"><span data-stu-id="d62e8-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="d62e8-340">O script de PowerShell a seguir pode ser usado para criar um gatilho de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d62e8-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="d62e8-341">Use o [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e defina as variáveis a seguir para corresponder ao trabalho e à agenda desejados:</span><span class="sxs-lookup"><span data-stu-id="d62e8-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="d62e8-342">Para remover uma associação agendada para impedir o trabalho de ser executado segundo a agenda</span><span class="sxs-lookup"><span data-stu-id="d62e8-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="d62e8-343">Para interromper a execução do trabalho recorrente por meio de um gatilho de trabalho, esse gatilho pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="d62e8-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="d62e8-344">Remova um gatilho de trabalho para impedir que um trabalho seja executado de acordo com um agendamento usando o cmdlet [**Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="d62e8-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="d62e8-345">Recuperar gatilhos de trabalho associados a um cronograma</span><span class="sxs-lookup"><span data-stu-id="d62e8-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="d62e8-346">O seguinte script PowerShell pode ser usado para obter e exibir os gatilhos de trabalho registrados para um horário de agendamento específico.</span><span class="sxs-lookup"><span data-stu-id="d62e8-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="d62e8-347">Para recuperar gatilhos de trabalho associados a um trabalho</span><span class="sxs-lookup"><span data-stu-id="d62e8-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="d62e8-348">Use o [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) para obter e exibir agendas que contenham um trabalho registrado.</span><span class="sxs-lookup"><span data-stu-id="d62e8-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="d62e8-349">Para criar um DACPAC (aplicativo da camada de dados) para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="d62e8-350">Para criar um DACPAC, consulte [Aplicativos de camada de dados](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="d62e8-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="d62e8-351">Para implantar um DACPAC, use o cmdlet [New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="d62e8-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="d62e8-352">O DACPAC deve ser acessado pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="d62e8-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="d62e8-353">É recomendável carregar um DACPAC criado para o Armazenamento do Azure e criar uma [Assinatura de Acesso Compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para o DACPAC.</span><span class="sxs-lookup"><span data-stu-id="d62e8-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="d62e8-354">Para atualizar um DACPAC (aplicativo da camada de dados) para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="d62e8-355">DACPACs existentes registrados em Trabalhos do Banco de Dados Elástico podem ser atualizados para apontar para os novos URIs.</span><span class="sxs-lookup"><span data-stu-id="d62e8-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="d62e8-356">Use o cmdlet [**Set-AzureSqlJobContentDefinition**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) para atualizar o URI do DACPAC em um DACPAC existente registrado:</span><span class="sxs-lookup"><span data-stu-id="d62e8-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="d62e8-357">Para criar um trabalho para aplicar um DACPAC (aplicativo da camada de dados) em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d62e8-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="d62e8-358">Após um DACPAC ter sido criado no recurso trabalhos de Banco de Dados Elástico, um trabalho poderá ser criado para aplicar o DACPAC em um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d62e8-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="d62e8-359">O seguinte script PowerShell pode ser usado para criar um trabalho DACPAC em uma coleção de bancos de dados personalizada:</span><span class="sxs-lookup"><span data-stu-id="d62e8-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
