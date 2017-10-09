---
title: "aaaData variáveis de sistema e funções da fábrica | Microsoft Docs"
description: "Fornece uma lista de funções do Azure Data Factory e variáveis do sistema"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="6064f-103">Azure Data Factory - Funções e Variáveis do Sistema</span><span class="sxs-lookup"><span data-stu-id="6064f-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="6064f-104">Este artigo fornece informações sobre funções e variáveis com suporte no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6064f-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="6064f-105">Variáveis do sistema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="6064f-105">Data Factory system variables</span></span>
| <span data-ttu-id="6064f-106">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="6064f-106">Variable Name</span></span> | <span data-ttu-id="6064f-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="6064f-107">Description</span></span> | <span data-ttu-id="6064f-108">Escopo do objeto</span><span class="sxs-lookup"><span data-stu-id="6064f-108">Object Scope</span></span> | <span data-ttu-id="6064f-109">Escopo JSON e casos de uso</span><span class="sxs-lookup"><span data-stu-id="6064f-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6064f-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="6064f-110">WindowStart</span></span> |<span data-ttu-id="6064f-111">Início do intervalo de tempo para a janela da execução de atividade atual</span><span class="sxs-lookup"><span data-stu-id="6064f-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="6064f-112">atividade</span><span class="sxs-lookup"><span data-stu-id="6064f-112">activity</span></span> |<ol><li><span data-ttu-id="6064f-113">Especifica consultas de seleção de dados.</span><span class="sxs-lookup"><span data-stu-id="6064f-113">Specify data selection queries.</span></span> <span data-ttu-id="6064f-114">Consulte os artigos de conector referenciados em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6064f-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="6064f-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="6064f-115">WindowEnd</span></span> |<span data-ttu-id="6064f-116">Fim do intervalo de tempo para a janela da execução de atividade atual</span><span class="sxs-lookup"><span data-stu-id="6064f-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="6064f-117">atividade</span><span class="sxs-lookup"><span data-stu-id="6064f-117">activity</span></span> |<span data-ttu-id="6064f-118">igual a WindowStart.</span><span class="sxs-lookup"><span data-stu-id="6064f-118">same as WindowStart.</span></span> |
| <span data-ttu-id="6064f-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="6064f-119">SliceStart</span></span> |<span data-ttu-id="6064f-120">Início do intervalo de tempo para a fatia de dados sendo gerada</span><span class="sxs-lookup"><span data-stu-id="6064f-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="6064f-121">atividade</span><span class="sxs-lookup"><span data-stu-id="6064f-121">activity</span></span><br/><span data-ttu-id="6064f-122">conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6064f-122">dataset</span></span> |<ol><li><span data-ttu-id="6064f-123">Especifique caminhos de pasta dinâmicos e nomes de arquivos enquanto estiver trabalhando com o [Blob do Azure](data-factory-azure-blob-connector.md) e [Conjuntos de dados do sistema de arquivos](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6064f-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="6064f-124">Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.</span><span class="sxs-lookup"><span data-stu-id="6064f-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="6064f-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="6064f-125">SliceEnd</span></span> |<span data-ttu-id="6064f-126">Fim do intervalo de tempo da fatia de dados atual.</span><span class="sxs-lookup"><span data-stu-id="6064f-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="6064f-127">atividade</span><span class="sxs-lookup"><span data-stu-id="6064f-127">activity</span></span><br/><span data-ttu-id="6064f-128">dataset</span><span class="sxs-lookup"><span data-stu-id="6064f-128">dataset</span></span> |<span data-ttu-id="6064f-129">o mesmo que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="6064f-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="6064f-130">No momento fábrica de dados requer que Olá agendar Olá especificado na atividade corresponde exatamente a agenda de saudação especificada na disponibilidade do conjunto de dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="6064f-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="6064f-131">Portanto, WindowStart, WindowEnd e SliceStart e SliceEnd sempre mapeiam toohello período e uma fatia de saída única a mesma hora.</span><span class="sxs-lookup"><span data-stu-id="6064f-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="6064f-132">Exemplo para usar uma variável de sistema</span><span class="sxs-lookup"><span data-stu-id="6064f-132">Example for using a system variable</span></span>
<span data-ttu-id="6064f-133">Em Olá seguindo o exemplo, ano, mês, dia e hora do **SliceStart** são extraídos em variáveis separadas que são usadas por **folderPath** e **fileName** propriedades.</span><span class="sxs-lookup"><span data-stu-id="6064f-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="6064f-134">Funções do Data Factory</span><span class="sxs-lookup"><span data-stu-id="6064f-134">Data Factory functions</span></span>
<span data-ttu-id="6064f-135">Você pode usar as funções na fábrica de dados juntamente com variáveis de sistema para Olá propósitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6064f-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="6064f-136">Especificando consultas de seleção de dados (consulte os artigos de conector referenciados por Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6064f-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="6064f-137">Olá tooinvoke sintaxe é uma função da fábrica de dados:  **$$ <function>**  para consultas de seleção de dados e outras propriedades na atividade hello e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="6064f-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="6064f-138">Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.</span><span class="sxs-lookup"><span data-stu-id="6064f-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="6064f-139">$$ não é necessário para especificar expressões de dependência de entrada.</span><span class="sxs-lookup"><span data-stu-id="6064f-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="6064f-140">Em Olá seguindo a amostra, **sqlReaderQuery** propriedade em um arquivo JSON é atribuída o valor de tooa retornado por Olá `Text.Format` função.</span><span class="sxs-lookup"><span data-stu-id="6064f-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="6064f-141">Este exemplo também usa uma variável de sistema chamada **WindowStart**, que representa a hora de início de saudação da janela de execução da atividade hello.</span><span class="sxs-lookup"><span data-stu-id="6064f-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="6064f-142">Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa).</span><span class="sxs-lookup"><span data-stu-id="6064f-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="6064f-143">Funções</span><span class="sxs-lookup"><span data-stu-id="6064f-143">Functions</span></span>
<span data-ttu-id="6064f-144">Olá tabelas a seguir lista todas as funções hello na fábrica de dados do Azure:</span><span class="sxs-lookup"><span data-stu-id="6064f-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="6064f-145">Categoria</span><span class="sxs-lookup"><span data-stu-id="6064f-145">Category</span></span> | <span data-ttu-id="6064f-146">Função</span><span class="sxs-lookup"><span data-stu-id="6064f-146">Function</span></span> | <span data-ttu-id="6064f-147">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6064f-147">Parameters</span></span> | <span data-ttu-id="6064f-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="6064f-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6064f-149">Hora</span><span class="sxs-lookup"><span data-stu-id="6064f-149">Time</span></span> |<span data-ttu-id="6064f-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-150">AddHours(X,Y)</span></span> |<span data-ttu-id="6064f-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="6064f-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-152">Y: int</span></span> |<span data-ttu-id="6064f-153">Adiciona Y horas toohello momento X.</span><span class="sxs-lookup"><span data-stu-id="6064f-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="6064f-154">Exemplo: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="6064f-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="6064f-155">Hora</span><span class="sxs-lookup"><span data-stu-id="6064f-155">Time</span></span> |<span data-ttu-id="6064f-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="6064f-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="6064f-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-158">Y: int</span></span> |<span data-ttu-id="6064f-159">Adiciona Y minutos tooX.</span><span class="sxs-lookup"><span data-stu-id="6064f-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="6064f-160">Exemplo: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="6064f-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="6064f-161">Hora</span><span class="sxs-lookup"><span data-stu-id="6064f-161">Time</span></span> |<span data-ttu-id="6064f-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-162">StartOfHour(X)</span></span> |<span data-ttu-id="6064f-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-163">X: Datetime</span></span> |<span data-ttu-id="6064f-164">Obtém Olá hora inicial da hora Olá representada pelo componente de hora de saudação do X.</span><span class="sxs-lookup"><span data-stu-id="6064f-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="6064f-165">Exemplo: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="6064f-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="6064f-166">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-166">Date</span></span> |<span data-ttu-id="6064f-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-167">AddDays(X,Y)</span></span> |<span data-ttu-id="6064f-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-168">X: DateTime</span></span><br/><br/><span data-ttu-id="6064f-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-169">Y: int</span></span> |<span data-ttu-id="6064f-170">Adiciona Y dias tooX.</span><span class="sxs-lookup"><span data-stu-id="6064f-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="6064f-171">Exemplo: 15/9/2013 12:00:00 + 2 dias = 17/9/2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="6064f-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="6064f-172">Você pode subtrair dias também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="6064f-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="6064f-173">Exemplo: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="6064f-174">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-174">Date</span></span> |<span data-ttu-id="6064f-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="6064f-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-176">X: DateTime</span></span><br/><br/><span data-ttu-id="6064f-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-177">Y: int</span></span> |<span data-ttu-id="6064f-178">Adiciona Y meses tooX.</span><span class="sxs-lookup"><span data-stu-id="6064f-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="6064f-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="6064f-180">Você pode subtrair meses também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="6064f-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="6064f-181">Exemplo: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="6064f-182">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-182">Date</span></span> |<span data-ttu-id="6064f-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="6064f-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="6064f-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-185">Y: int</span></span> |<span data-ttu-id="6064f-186">Adiciona Y * 3 meses tooX.</span><span class="sxs-lookup"><span data-stu-id="6064f-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="6064f-187">Exemplo: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="6064f-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="6064f-188">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-188">Date</span></span> |<span data-ttu-id="6064f-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="6064f-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-190">X: DateTime</span></span><br/><br/><span data-ttu-id="6064f-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-191">Y: int</span></span> |<span data-ttu-id="6064f-192">Adiciona Y * 7 dias tooX</span><span class="sxs-lookup"><span data-stu-id="6064f-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="6064f-193">Exemplo: 15/9/2013 12:00:00 + 1 semana = 22/9/2013 12:00:00</span><span class="sxs-lookup"><span data-stu-id="6064f-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="6064f-194">Você pode subtrair semanas também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="6064f-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="6064f-195">Exemplo: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="6064f-196">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-196">Date</span></span> |<span data-ttu-id="6064f-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="6064f-197">AddYears(X,Y)</span></span> |<span data-ttu-id="6064f-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-198">X: DateTime</span></span><br/><br/><span data-ttu-id="6064f-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="6064f-199">Y: int</span></span> |<span data-ttu-id="6064f-200">Adiciona Y anos tooX.</span><span class="sxs-lookup"><span data-stu-id="6064f-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="6064f-201">Você pode subtrair anos também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="6064f-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="6064f-202">Exemplo: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="6064f-203">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-203">Date</span></span> |<span data-ttu-id="6064f-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-204">Day(X)</span></span> |<span data-ttu-id="6064f-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-205">X: DateTime</span></span> |<span data-ttu-id="6064f-206">Obtém o componente de dia de saudação do X.</span><span class="sxs-lookup"><span data-stu-id="6064f-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="6064f-207">Exemplo: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="6064f-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="6064f-208">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-208">Date</span></span> |<span data-ttu-id="6064f-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-209">DayOfWeek(X)</span></span> |<span data-ttu-id="6064f-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-210">X: DateTime</span></span> |<span data-ttu-id="6064f-211">Obtém o dia de saudação do componente de semana de X.</span><span class="sxs-lookup"><span data-stu-id="6064f-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="6064f-212">Exemplo: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="6064f-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="6064f-213">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-213">Date</span></span> |<span data-ttu-id="6064f-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-214">DayOfYear(X)</span></span> |<span data-ttu-id="6064f-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-215">X: DateTime</span></span> |<span data-ttu-id="6064f-216">Obtém Olá dia no ano Olá representado pelo componente de ano de saudação do X.</span><span class="sxs-lookup"><span data-stu-id="6064f-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="6064f-217">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="6064f-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="6064f-218">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-218">Date</span></span> |<span data-ttu-id="6064f-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-219">DaysInMonth(X)</span></span> |<span data-ttu-id="6064f-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-220">X: DateTime</span></span> |<span data-ttu-id="6064f-221">Obtém os dias de saudação do mês de saudação representado pelo componente de mês de saudação do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="6064f-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="6064f-222">Exemplo: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="6064f-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="6064f-223">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-223">Date</span></span> |<span data-ttu-id="6064f-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-224">EndOfDay(X)</span></span> |<span data-ttu-id="6064f-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-225">X: DateTime</span></span> |<span data-ttu-id="6064f-226">Obtém a data e hora Olá que representa o fim de saudação do dia de saudação (componente do dia) de X.</span><span class="sxs-lookup"><span data-stu-id="6064f-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="6064f-227">Exemplo: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="6064f-228">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-228">Date</span></span> |<span data-ttu-id="6064f-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-229">EndOfMonth(X)</span></span> |<span data-ttu-id="6064f-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-230">X: DateTime</span></span> |<span data-ttu-id="6064f-231">Obtém a fim de saudação do mês de saudação representado pelo componente de mês do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="6064f-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="6064f-232">Exemplo: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data que representa a fim de saudação do mês de setembro)</span><span class="sxs-lookup"><span data-stu-id="6064f-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="6064f-233">Data</span><span class="sxs-lookup"><span data-stu-id="6064f-233">Date</span></span> |<span data-ttu-id="6064f-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-234">StartOfDay(X)</span></span> |<span data-ttu-id="6064f-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-235">X: DateTime</span></span> |<span data-ttu-id="6064f-236">Obtém o início de saudação do dia Olá representado pelo componente de dia de saudação do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="6064f-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="6064f-237">Exemplo: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="6064f-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="6064f-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="6064f-238">DateTime</span></span> |<span data-ttu-id="6064f-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-239">From(X)</span></span> |<span data-ttu-id="6064f-240">X: Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6064f-240">X: String</span></span> |<span data-ttu-id="6064f-241">Analise a cadeia de caracteres X tooa data hora.</span><span class="sxs-lookup"><span data-stu-id="6064f-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="6064f-242">Datetime</span><span class="sxs-lookup"><span data-stu-id="6064f-242">DateTime</span></span> |<span data-ttu-id="6064f-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-243">Ticks(X)</span></span> |<span data-ttu-id="6064f-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="6064f-244">X: DateTime</span></span> |<span data-ttu-id="6064f-245">Obtém tiques Olá propriedade Olá parâmetro X. Um tique é igual a 100 nanossegundos.</span><span class="sxs-lookup"><span data-stu-id="6064f-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="6064f-246">valor Olá dessa propriedade representa o número de saudação de tiques que passaram desde 12:00:00 meia-noite de 1 de janeiro, 0001.</span><span class="sxs-lookup"><span data-stu-id="6064f-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="6064f-247">Texto</span><span class="sxs-lookup"><span data-stu-id="6064f-247">Text</span></span> |<span data-ttu-id="6064f-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="6064f-248">Format(X)</span></span> |<span data-ttu-id="6064f-249">X: variável de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6064f-249">X: String variable</span></span> |<span data-ttu-id="6064f-250">Olá de formatos de texto (use `\\'` tooescape combinação `'` caractere).</span><span class="sxs-lookup"><span data-stu-id="6064f-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="6064f-251">Ao usar uma função dentro de outra função, não é necessário toouse  **$$**  prefixo para a função interna de saudação.</span><span class="sxs-lookup"><span data-stu-id="6064f-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="6064f-252">Por exemplo: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' e RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="6064f-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="6064f-253">Neste exemplo, observe que  **$$**  prefixo não é usado para Olá **Time.AddHours** função.</span><span class="sxs-lookup"><span data-stu-id="6064f-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="6064f-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6064f-254">Example</span></span>
<span data-ttu-id="6064f-255">Olá seguintes parâmetros de exemplo, a entrada e saída para a atividade de Hive Olá são determinados usando Olá `Text.Format` funções e variáveis de sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="6064f-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="6064f-256">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="6064f-256">Example 2</span></span>

<span data-ttu-id="6064f-257">Em Olá exemplo a seguir, Olá parâmetro DateTime hello que atividade de procedimento armazenado é determinada pelo texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="6064f-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="6064f-258">Formatar a função e Olá SliceStart variável.</span><span class="sxs-lookup"><span data-stu-id="6064f-258">Format function and hello SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="6064f-259">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="6064f-259">Example 3</span></span>
<span data-ttu-id="6064f-260">tooread dados do dia anterior em vez de dia representado pelo Olá SliceStart, use a função de AddDays de saudação conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="6064f-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="6064f-261">Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa).</span><span class="sxs-lookup"><span data-stu-id="6064f-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

