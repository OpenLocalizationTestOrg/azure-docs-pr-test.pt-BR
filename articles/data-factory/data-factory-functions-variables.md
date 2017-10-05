---
title: "Funções do Data Factory e Variáveis do Sistema | Microsoft Docs"
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
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="2fc29-103">Azure Data Factory - Funções e Variáveis do Sistema</span><span class="sxs-lookup"><span data-stu-id="2fc29-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="2fc29-104">Este artigo fornece informações sobre funções e variáveis com suporte no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2fc29-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="2fc29-105">Variáveis do sistema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="2fc29-105">Data Factory system variables</span></span>
| <span data-ttu-id="2fc29-106">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="2fc29-106">Variable Name</span></span> | <span data-ttu-id="2fc29-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="2fc29-107">Description</span></span> | <span data-ttu-id="2fc29-108">Escopo do objeto</span><span class="sxs-lookup"><span data-stu-id="2fc29-108">Object Scope</span></span> | <span data-ttu-id="2fc29-109">Escopo JSON e casos de uso</span><span class="sxs-lookup"><span data-stu-id="2fc29-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fc29-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="2fc29-110">WindowStart</span></span> |<span data-ttu-id="2fc29-111">Início do intervalo de tempo para a janela da execução de atividade atual</span><span class="sxs-lookup"><span data-stu-id="2fc29-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="2fc29-112">atividade</span><span class="sxs-lookup"><span data-stu-id="2fc29-112">activity</span></span> |<ol><li><span data-ttu-id="2fc29-113">Especifica consultas de seleção de dados.</span><span class="sxs-lookup"><span data-stu-id="2fc29-113">Specify data selection queries.</span></span> <span data-ttu-id="2fc29-114">Veja os artigos sobre o conector referenciados no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="2fc29-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="2fc29-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="2fc29-115">WindowEnd</span></span> |<span data-ttu-id="2fc29-116">Fim do intervalo de tempo para a janela da execução de atividade atual</span><span class="sxs-lookup"><span data-stu-id="2fc29-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="2fc29-117">atividade</span><span class="sxs-lookup"><span data-stu-id="2fc29-117">activity</span></span> |<span data-ttu-id="2fc29-118">igual a WindowStart.</span><span class="sxs-lookup"><span data-stu-id="2fc29-118">same as WindowStart.</span></span> |
| <span data-ttu-id="2fc29-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="2fc29-119">SliceStart</span></span> |<span data-ttu-id="2fc29-120">Início do intervalo de tempo para a fatia de dados sendo gerada</span><span class="sxs-lookup"><span data-stu-id="2fc29-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="2fc29-121">atividade</span><span class="sxs-lookup"><span data-stu-id="2fc29-121">activity</span></span><br/><span data-ttu-id="2fc29-122">conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="2fc29-122">dataset</span></span> |<ol><li><span data-ttu-id="2fc29-123">Especifique caminhos de pasta dinâmicos e nomes de arquivos enquanto estiver trabalhando com o [Blob do Azure](data-factory-azure-blob-connector.md) e [Conjuntos de dados do sistema de arquivos](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="2fc29-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="2fc29-124">Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.</span><span class="sxs-lookup"><span data-stu-id="2fc29-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="2fc29-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="2fc29-125">SliceEnd</span></span> |<span data-ttu-id="2fc29-126">Fim do intervalo de tempo da fatia de dados atual.</span><span class="sxs-lookup"><span data-stu-id="2fc29-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="2fc29-127">atividade</span><span class="sxs-lookup"><span data-stu-id="2fc29-127">activity</span></span><br/><span data-ttu-id="2fc29-128">dataset</span><span class="sxs-lookup"><span data-stu-id="2fc29-128">dataset</span></span> |<span data-ttu-id="2fc29-129">o mesmo que SliceStart.</span><span class="sxs-lookup"><span data-stu-id="2fc29-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="2fc29-130">Atualmente, o data factory exige que o agendamento especificado na atividade corresponda exatamente ao agendamento especificado na disponibilidade do conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="2fc29-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="2fc29-131">Portanto, WindowStart, WindowEnd, SliceStart e SliceEnd sempre são mapeados para o mesmo período de tempo e uma única fatia de saída.</span><span class="sxs-lookup"><span data-stu-id="2fc29-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="2fc29-132">Exemplo para usar uma variável de sistema</span><span class="sxs-lookup"><span data-stu-id="2fc29-132">Example for using a system variable</span></span>
<span data-ttu-id="2fc29-133">No exemplo a seguir, o ano, o mês, o dia e a hora de **SliceStart** são extraídos em variáveis separadas que são usadas pelas propriedades **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="2fc29-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="2fc29-134">Funções do Data Factory</span><span class="sxs-lookup"><span data-stu-id="2fc29-134">Data Factory functions</span></span>
<span data-ttu-id="2fc29-135">Você pode usar funções no Data Factory junto com as variáveis do sistema para as seguintes finalidades:</span><span class="sxs-lookup"><span data-stu-id="2fc29-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="2fc29-136">Especificando consultas de seleção de dados (veja os artigos sobre o conector referenciados no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="2fc29-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="2fc29-137">A sintaxe para invocar uma função do Data Factory é: **$$<function>** para consultas de seleção de dados e outras propriedades na atividade e nos conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="2fc29-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="2fc29-138">Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.</span><span class="sxs-lookup"><span data-stu-id="2fc29-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="2fc29-139">$$ não é necessário para especificar expressões de dependência de entrada.</span><span class="sxs-lookup"><span data-stu-id="2fc29-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="2fc29-140">No exemplo a seguir, a propriedade **sqlReaderQuery** em um arquivo JSON é atribuída a um valor retornado pela função `Text.Format`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="2fc29-141">Este exemplo também usa uma variável de sistema chamada **WindowStart**, que representa a hora de início da janela de execução de atividade.</span><span class="sxs-lookup"><span data-stu-id="2fc29-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="2fc29-142">Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa).</span><span class="sxs-lookup"><span data-stu-id="2fc29-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="2fc29-143">Funções</span><span class="sxs-lookup"><span data-stu-id="2fc29-143">Functions</span></span>
<span data-ttu-id="2fc29-144">As tabelas a seguir listam todas as funções no Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="2fc29-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="2fc29-145">Categoria</span><span class="sxs-lookup"><span data-stu-id="2fc29-145">Category</span></span> | <span data-ttu-id="2fc29-146">Função</span><span class="sxs-lookup"><span data-stu-id="2fc29-146">Function</span></span> | <span data-ttu-id="2fc29-147">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2fc29-147">Parameters</span></span> | <span data-ttu-id="2fc29-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="2fc29-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2fc29-149">Hora</span><span class="sxs-lookup"><span data-stu-id="2fc29-149">Time</span></span> |<span data-ttu-id="2fc29-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-150">AddHours(X,Y)</span></span> |<span data-ttu-id="2fc29-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="2fc29-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-152">Y: int</span></span> |<span data-ttu-id="2fc29-153">Adiciona Y horas até o momento X determinado.</span><span class="sxs-lookup"><span data-stu-id="2fc29-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="2fc29-154">Exemplo: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="2fc29-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="2fc29-155">Hora</span><span class="sxs-lookup"><span data-stu-id="2fc29-155">Time</span></span> |<span data-ttu-id="2fc29-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="2fc29-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="2fc29-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-158">Y: int</span></span> |<span data-ttu-id="2fc29-159">Adiciona Y minutos a X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="2fc29-160">Exemplo: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="2fc29-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="2fc29-161">Hora</span><span class="sxs-lookup"><span data-stu-id="2fc29-161">Time</span></span> |<span data-ttu-id="2fc29-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-162">StartOfHour(X)</span></span> |<span data-ttu-id="2fc29-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-163">X: Datetime</span></span> |<span data-ttu-id="2fc29-164">Obtém a hora de início para a hora representada pelo componente de hora do X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="2fc29-165">Exemplo: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="2fc29-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="2fc29-166">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-166">Date</span></span> |<span data-ttu-id="2fc29-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-167">AddDays(X,Y)</span></span> |<span data-ttu-id="2fc29-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-168">X: DateTime</span></span><br/><br/><span data-ttu-id="2fc29-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-169">Y: int</span></span> |<span data-ttu-id="2fc29-170">Adiciona Y dias a X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="2fc29-171">Exemplo: 15/9/2013 12:00:00 + 2 dias = 17/9/2013 12:00:00.</span><span class="sxs-lookup"><span data-stu-id="2fc29-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="2fc29-172">Você pode subtrair dias também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="2fc29-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="2fc29-173">Exemplo: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="2fc29-174">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-174">Date</span></span> |<span data-ttu-id="2fc29-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="2fc29-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-176">X: DateTime</span></span><br/><br/><span data-ttu-id="2fc29-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-177">Y: int</span></span> |<span data-ttu-id="2fc29-178">Adiciona Y meses a X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="2fc29-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="2fc29-180">Você pode subtrair meses também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="2fc29-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="2fc29-181">Exemplo: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="2fc29-182">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-182">Date</span></span> |<span data-ttu-id="2fc29-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="2fc29-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="2fc29-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-185">Y: int</span></span> |<span data-ttu-id="2fc29-186">Adiciona Y * 3 meses a X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="2fc29-187">Exemplo: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="2fc29-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="2fc29-188">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-188">Date</span></span> |<span data-ttu-id="2fc29-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="2fc29-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-190">X: DateTime</span></span><br/><br/><span data-ttu-id="2fc29-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-191">Y: int</span></span> |<span data-ttu-id="2fc29-192">Adiciona Y * 7 dias a X</span><span class="sxs-lookup"><span data-stu-id="2fc29-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="2fc29-193">Exemplo: 15/9/2013 12:00:00 + 1 semana = 22/9/2013 12:00:00</span><span class="sxs-lookup"><span data-stu-id="2fc29-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="2fc29-194">Você pode subtrair semanas também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="2fc29-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="2fc29-195">Exemplo: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="2fc29-196">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-196">Date</span></span> |<span data-ttu-id="2fc29-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="2fc29-197">AddYears(X,Y)</span></span> |<span data-ttu-id="2fc29-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-198">X: DateTime</span></span><br/><br/><span data-ttu-id="2fc29-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="2fc29-199">Y: int</span></span> |<span data-ttu-id="2fc29-200">Adiciona Y dias a X</span><span class="sxs-lookup"><span data-stu-id="2fc29-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="2fc29-201">Você pode subtrair anos também, especificando Y como um número negativo.</span><span class="sxs-lookup"><span data-stu-id="2fc29-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="2fc29-202">Exemplo: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="2fc29-203">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-203">Date</span></span> |<span data-ttu-id="2fc29-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-204">Day(X)</span></span> |<span data-ttu-id="2fc29-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-205">X: DateTime</span></span> |<span data-ttu-id="2fc29-206">Obtém o componente de dia de X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="2fc29-207">Exemplo: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="2fc29-208">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-208">Date</span></span> |<span data-ttu-id="2fc29-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-209">DayOfWeek(X)</span></span> |<span data-ttu-id="2fc29-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-210">X: DateTime</span></span> |<span data-ttu-id="2fc29-211">Obtém o componente de dia da semana de X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="2fc29-212">Exemplo: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="2fc29-213">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-213">Date</span></span> |<span data-ttu-id="2fc29-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-214">DayOfYear(X)</span></span> |<span data-ttu-id="2fc29-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-215">X: DateTime</span></span> |<span data-ttu-id="2fc29-216">Obtém o dia do ano que representa o componente de ano de X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="2fc29-217">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="2fc29-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="2fc29-218">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-218">Date</span></span> |<span data-ttu-id="2fc29-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-219">DaysInMonth(X)</span></span> |<span data-ttu-id="2fc29-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-220">X: DateTime</span></span> |<span data-ttu-id="2fc29-221">Obtém os dias do mês representados pelo componente de mês do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="2fc29-222">Exemplo: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="2fc29-223">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-223">Date</span></span> |<span data-ttu-id="2fc29-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-224">EndOfDay(X)</span></span> |<span data-ttu-id="2fc29-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-225">X: DateTime</span></span> |<span data-ttu-id="2fc29-226">Obtém a data e hora que representam o fim do dia (componente do dia) do X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="2fc29-227">Exemplo: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="2fc29-228">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-228">Date</span></span> |<span data-ttu-id="2fc29-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-229">EndOfMonth(X)</span></span> |<span data-ttu-id="2fc29-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-230">X: DateTime</span></span> |<span data-ttu-id="2fc29-231">Obtém o fim do mês representado pelo componente de mês do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="2fc29-232">Exemplo: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data/hora que representa o fim do mês de setembro)</span><span class="sxs-lookup"><span data-stu-id="2fc29-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="2fc29-233">Data</span><span class="sxs-lookup"><span data-stu-id="2fc29-233">Date</span></span> |<span data-ttu-id="2fc29-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-234">StartOfDay(X)</span></span> |<span data-ttu-id="2fc29-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-235">X: DateTime</span></span> |<span data-ttu-id="2fc29-236">Obtém o início do dia representado pelo componente dia do parâmetro X.</span><span class="sxs-lookup"><span data-stu-id="2fc29-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="2fc29-237">Exemplo: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="2fc29-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="2fc29-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="2fc29-238">DateTime</span></span> |<span data-ttu-id="2fc29-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-239">From(X)</span></span> |<span data-ttu-id="2fc29-240">X: Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2fc29-240">X: String</span></span> |<span data-ttu-id="2fc29-241">Analise a cadeia de caracteres X para um valor de data e hora.</span><span class="sxs-lookup"><span data-stu-id="2fc29-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="2fc29-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="2fc29-242">DateTime</span></span> |<span data-ttu-id="2fc29-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-243">Ticks(X)</span></span> |<span data-ttu-id="2fc29-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="2fc29-244">X: DateTime</span></span> |<span data-ttu-id="2fc29-245">Obtém os tiques de propriedade do parâmetro X. Um tique é igual a 100 nanossegundos.</span><span class="sxs-lookup"><span data-stu-id="2fc29-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="2fc29-246">O valor dessa propriedade representa o número de tiques que se passaram desde 0h, meia-noite de 1º de janeiro de 0001.</span><span class="sxs-lookup"><span data-stu-id="2fc29-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="2fc29-247">Texto</span><span class="sxs-lookup"><span data-stu-id="2fc29-247">Text</span></span> |<span data-ttu-id="2fc29-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="2fc29-248">Format(X)</span></span> |<span data-ttu-id="2fc29-249">X: variável de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2fc29-249">X: String variable</span></span> |<span data-ttu-id="2fc29-250">Formata o texto (use a combinação `\\'` para escapar o caractere `'`).</span><span class="sxs-lookup"><span data-stu-id="2fc29-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="2fc29-251">Ao usar uma função dentro de outra função, você não precisa usar o prefixo **$$** para a função interna.</span><span class="sxs-lookup"><span data-stu-id="2fc29-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="2fc29-252">Por exemplo: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' e RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="2fc29-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="2fc29-253">Neste exemplo, observe que o prefixo **$$** não é usado para a função **Time.AddHours**.</span><span class="sxs-lookup"><span data-stu-id="2fc29-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="2fc29-254">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2fc29-254">Example</span></span>
<span data-ttu-id="2fc29-255">No exemplo a seguir, os parâmetros de entrada e saída da atividade do Hive são determinados com o uso da função `Text.Format` e da variável do sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="2fc29-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="2fc29-256">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="2fc29-256">Example 2</span></span>

<span data-ttu-id="2fc29-257">No exemplo a seguir, o parâmetro DateTime da Atividade de Procedimento Armazenado é determinado com o uso de Text.</span><span class="sxs-lookup"><span data-stu-id="2fc29-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="2fc29-258">Format e da variável SliceStart.</span><span class="sxs-lookup"><span data-stu-id="2fc29-258">Format function and the SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="2fc29-259">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="2fc29-259">Example 3</span></span>
<span data-ttu-id="2fc29-260">Para ler dados do dia anterior em vez do dia representado pelo SliceStart, use a função AddDays conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fc29-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

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

<span data-ttu-id="2fc29-261">Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa).</span><span class="sxs-lookup"><span data-stu-id="2fc29-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

