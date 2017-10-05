---
title: "Associação de tabela externa do Azure Functions (versão prévia) | Microsoft Docs"
description: "Usar as associações de tabela externa no Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="ef8cf-103">Associação de tabela externa do Azure Functions (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="ef8cf-104">Este artigo mostra como manipular dados tabulares em provedores de SaaS (por exemplo, Sharepoint, Dynamics) com sua função com associações internas.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="ef8cf-105">O Azure Functions dá suporte a associações de entrada e saída para tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="ef8cf-106">Conexões de API</span><span class="sxs-lookup"><span data-stu-id="ef8cf-106">API Connections</span></span>

<span data-ttu-id="ef8cf-107">As associações de tabela aproveitam conexões de API externas para autenticar com provedores de SaaS terceirizados.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="ef8cf-108">Ao atribuir uma associação você pode criar uma nova conexão de API ou usar uma conexão de API existente dentro do mesmo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ef8cf-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="ef8cf-109">Conexões de API com suporte (Tabela)s</span><span class="sxs-lookup"><span data-stu-id="ef8cf-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="ef8cf-110">Conector</span><span class="sxs-lookup"><span data-stu-id="ef8cf-110">Connector</span></span>|<span data-ttu-id="ef8cf-111">Gatilho</span><span class="sxs-lookup"><span data-stu-id="ef8cf-111">Trigger</span></span>|<span data-ttu-id="ef8cf-112">Entrada</span><span class="sxs-lookup"><span data-stu-id="ef8cf-112">Input</span></span>|<span data-ttu-id="ef8cf-113">Saída</span><span class="sxs-lookup"><span data-stu-id="ef8cf-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="ef8cf-114">DB2</span><span class="sxs-lookup"><span data-stu-id="ef8cf-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="ef8cf-115">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-115">x</span></span>|<span data-ttu-id="ef8cf-116">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-116">x</span></span>
|[<span data-ttu-id="ef8cf-117">Dynamics 365 para Operações</span><span class="sxs-lookup"><span data-stu-id="ef8cf-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="ef8cf-118">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-118">x</span></span>|<span data-ttu-id="ef8cf-119">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-119">x</span></span>
|[<span data-ttu-id="ef8cf-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="ef8cf-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="ef8cf-121">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-121">x</span></span>|<span data-ttu-id="ef8cf-122">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-122">x</span></span>
|[<span data-ttu-id="ef8cf-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="ef8cf-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="ef8cf-124">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-124">x</span></span>|<span data-ttu-id="ef8cf-125">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-125">x</span></span>
|[<span data-ttu-id="ef8cf-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="ef8cf-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="ef8cf-127">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-127">x</span></span>|<span data-ttu-id="ef8cf-128">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-128">x</span></span>
|[<span data-ttu-id="ef8cf-129">Informix</span><span class="sxs-lookup"><span data-stu-id="ef8cf-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="ef8cf-130">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-130">x</span></span>|<span data-ttu-id="ef8cf-131">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-131">x</span></span>
|[<span data-ttu-id="ef8cf-132">Dynamics 365 para Finanças</span><span class="sxs-lookup"><span data-stu-id="ef8cf-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="ef8cf-133">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-133">x</span></span>|<span data-ttu-id="ef8cf-134">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-134">x</span></span>
|[<span data-ttu-id="ef8cf-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="ef8cf-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="ef8cf-136">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-136">x</span></span>|<span data-ttu-id="ef8cf-137">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-137">x</span></span>
|[<span data-ttu-id="ef8cf-138">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="ef8cf-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="ef8cf-139">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-139">x</span></span>|<span data-ttu-id="ef8cf-140">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-140">x</span></span>
|[<span data-ttu-id="ef8cf-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="ef8cf-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="ef8cf-142">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-142">x</span></span>|<span data-ttu-id="ef8cf-143">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-143">x</span></span>
|[<span data-ttu-id="ef8cf-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ef8cf-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="ef8cf-145">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-145">x</span></span>|<span data-ttu-id="ef8cf-146">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-146">x</span></span>
|[<span data-ttu-id="ef8cf-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ef8cf-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="ef8cf-148">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-148">x</span></span>|<span data-ttu-id="ef8cf-149">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-149">x</span></span>
|[<span data-ttu-id="ef8cf-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ef8cf-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="ef8cf-151">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-151">x</span></span>|<span data-ttu-id="ef8cf-152">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-152">x</span></span>
|[<span data-ttu-id="ef8cf-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="ef8cf-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="ef8cf-154">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-154">x</span></span>|<span data-ttu-id="ef8cf-155">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-155">x</span></span>
|<span data-ttu-id="ef8cf-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="ef8cf-156">UserVoice</span></span>||<span data-ttu-id="ef8cf-157">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-157">x</span></span>|<span data-ttu-id="ef8cf-158">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-158">x</span></span>
|<span data-ttu-id="ef8cf-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="ef8cf-159">Zendesk</span></span>||<span data-ttu-id="ef8cf-160">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-160">x</span></span>|<span data-ttu-id="ef8cf-161">x</span><span class="sxs-lookup"><span data-stu-id="ef8cf-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="ef8cf-162">Conexões de tabela externa também podem ser usadas nos [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="ef8cf-163">Criar uma conexão de API: passo a passo</span><span class="sxs-lookup"><span data-stu-id="ef8cf-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="ef8cf-164">Criar uma função > função personalizada ![Criar uma função personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="ef8cf-165">Modelo `Experimental` > `ExternalTable-CSharp` de cenário > Criar uma nova `External Table connection`
![Escolher modelo de entrada de tabela](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="ef8cf-166">Escolha seu provedor de SaaS > escolha/crie uma conexão ![Configurar conexão de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="ef8cf-167">Selecione sua conexão de API > crie a função ![Criar função de tabela](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="ef8cf-168">Selecionar `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="ef8cf-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="ef8cf-169">Configure a conexão para usar sua tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="ef8cf-170">Essas configurações irão variar entre provedores de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="ef8cf-171">Elas estão destacados abaixo nas [configurações de fonte de dados](#datasourcesettings)
![Configurar tabela](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="ef8cf-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="ef8cf-172">Uso</span><span class="sxs-lookup"><span data-stu-id="ef8cf-172">Usage</span></span>

<span data-ttu-id="ef8cf-173">Este exemplo conecta a uma tabela denominada "Contato" com as colunas Id, Nome e Sobrenome.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="ef8cf-174">O código lista as entidades de contato na tabela e registra os nomes e sobrenomes.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="ef8cf-175">Associações</span><span class="sxs-lookup"><span data-stu-id="ef8cf-175">Bindings</span></span>
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
<span data-ttu-id="ef8cf-176">`entityId` deve estar vazia para associações de tabela.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="ef8cf-177">`ConnectionAppSettingsKey` identifica a configuração de aplicativo que armazena a sequência da conexão da API.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="ef8cf-178">A configuração do aplicativo é criada automaticamente quando você adiciona uma conexão de API à interface de usuário integrada.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="ef8cf-179">Um conector tabular fornece conjuntos de dados e cada conjunto de dados contém tabelas.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="ef8cf-180">O nome do conjunto de dados padrão é “padrão”.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="ef8cf-181">Os títulos de um conjunto de dados e uma tabela em vários provedores de SaaS estão listados abaixo:</span><span class="sxs-lookup"><span data-stu-id="ef8cf-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="ef8cf-182">Conector</span><span class="sxs-lookup"><span data-stu-id="ef8cf-182">Connector</span></span>|<span data-ttu-id="ef8cf-183">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ef8cf-183">Dataset</span></span>|<span data-ttu-id="ef8cf-184">Tabela</span><span class="sxs-lookup"><span data-stu-id="ef8cf-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="ef8cf-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ef8cf-185">**SharePoint**</span></span>|<span data-ttu-id="ef8cf-186">Site</span><span class="sxs-lookup"><span data-stu-id="ef8cf-186">Site</span></span>|<span data-ttu-id="ef8cf-187">Lista do SharePoint</span><span class="sxs-lookup"><span data-stu-id="ef8cf-187">SharePoint List</span></span>
|<span data-ttu-id="ef8cf-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ef8cf-188">**SQL**</span></span>|<span data-ttu-id="ef8cf-189">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="ef8cf-189">Database</span></span>|<span data-ttu-id="ef8cf-190">Tabela</span><span class="sxs-lookup"><span data-stu-id="ef8cf-190">Table</span></span> 
|<span data-ttu-id="ef8cf-191">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="ef8cf-191">**Google Sheet**</span></span>|<span data-ttu-id="ef8cf-192">Planilha</span><span class="sxs-lookup"><span data-stu-id="ef8cf-192">Spreadsheet</span></span>|<span data-ttu-id="ef8cf-193">Planilha</span><span class="sxs-lookup"><span data-stu-id="ef8cf-193">Worksheet</span></span> 
|<span data-ttu-id="ef8cf-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="ef8cf-194">**Excel**</span></span>|<span data-ttu-id="ef8cf-195">Arquivo do Excel</span><span class="sxs-lookup"><span data-stu-id="ef8cf-195">Excel file</span></span>|<span data-ttu-id="ef8cf-196">Folha</span><span class="sxs-lookup"><span data-stu-id="ef8cf-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="ef8cf-197">Uso em C#</span><span class="sxs-lookup"><span data-stu-id="ef8cf-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<span data-ttu-id="ef8cf-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Configurações de Fonte de Dados</span><span class="sxs-lookup"><span data-stu-id="ef8cf-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="ef8cf-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ef8cf-199">SQL Server</span></span>

<span data-ttu-id="ef8cf-200">O script para criar e preencher a tabela Contato pode ser encontrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="ef8cf-201">dataSetName é “padrão”.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-201">dataSetName is “default.”</span></span>

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a><span data-ttu-id="ef8cf-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="ef8cf-202">Google Sheets</span></span>
<span data-ttu-id="ef8cf-203">No Google Docs, crie uma planilha com uma planilha chamada `Contact`.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="ef8cf-204">O conector não pode usar o nome de exibição da planilha.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="ef8cf-205">O nome interno (em negrito) precisa ser usado como dataSetName, por exemplo: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** adicione os nomes de coluna `Id`, `LastName`, `FirstName` à primeira linha e, em seguida, preencha os dados nas linhas seguintes.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="ef8cf-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ef8cf-206">Salesforce</span></span>
<span data-ttu-id="ef8cf-207">dataSetName é “padrão”.</span><span class="sxs-lookup"><span data-stu-id="ef8cf-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef8cf-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef8cf-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
