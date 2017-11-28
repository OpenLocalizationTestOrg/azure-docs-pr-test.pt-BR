---
title: "associação de tabela externa de funções aaaAzure (visualização) | Microsoft Docs"
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
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="3730e-103">Associação de tabela externa do Azure Functions (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="3730e-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="3730e-104">Este artigo mostra como dados de tabela toomanipulate nos provedores de SaaS (por exemplo, Sharepoint, Dynamics) dentro de sua função com ligações internas.</span><span class="sxs-lookup"><span data-stu-id="3730e-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="3730e-105">O Azure Functions dá suporte a associações de entrada e saída para tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="3730e-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="3730e-106">Conexões de API</span><span class="sxs-lookup"><span data-stu-id="3730e-106">API Connections</span></span>

<span data-ttu-id="3730e-107">Associações de tabela aproveitam tooauthenticate de conexões de API externa com provedores de SaaS 3ª parte.</span><span class="sxs-lookup"><span data-stu-id="3730e-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="3730e-108">Ao atribuir uma associação você pode criar uma nova conexão de API ou usar uma conexão existente de API em Olá mesmo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3730e-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="3730e-109">Conexões de API com suporte (Tabela)s</span><span class="sxs-lookup"><span data-stu-id="3730e-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="3730e-110">Conector</span><span class="sxs-lookup"><span data-stu-id="3730e-110">Connector</span></span>|<span data-ttu-id="3730e-111">Gatilho</span><span class="sxs-lookup"><span data-stu-id="3730e-111">Trigger</span></span>|<span data-ttu-id="3730e-112">Entrada</span><span class="sxs-lookup"><span data-stu-id="3730e-112">Input</span></span>|<span data-ttu-id="3730e-113">Saída</span><span class="sxs-lookup"><span data-stu-id="3730e-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="3730e-114">DB2</span><span class="sxs-lookup"><span data-stu-id="3730e-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="3730e-115">x</span><span class="sxs-lookup"><span data-stu-id="3730e-115">x</span></span>|<span data-ttu-id="3730e-116">x</span><span class="sxs-lookup"><span data-stu-id="3730e-116">x</span></span>
|[<span data-ttu-id="3730e-117">Dynamics 365 para Operações</span><span class="sxs-lookup"><span data-stu-id="3730e-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="3730e-118">x</span><span class="sxs-lookup"><span data-stu-id="3730e-118">x</span></span>|<span data-ttu-id="3730e-119">x</span><span class="sxs-lookup"><span data-stu-id="3730e-119">x</span></span>
|[<span data-ttu-id="3730e-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="3730e-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="3730e-121">x</span><span class="sxs-lookup"><span data-stu-id="3730e-121">x</span></span>|<span data-ttu-id="3730e-122">x</span><span class="sxs-lookup"><span data-stu-id="3730e-122">x</span></span>
|[<span data-ttu-id="3730e-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="3730e-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="3730e-124">x</span><span class="sxs-lookup"><span data-stu-id="3730e-124">x</span></span>|<span data-ttu-id="3730e-125">x</span><span class="sxs-lookup"><span data-stu-id="3730e-125">x</span></span>
|[<span data-ttu-id="3730e-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="3730e-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="3730e-127">x</span><span class="sxs-lookup"><span data-stu-id="3730e-127">x</span></span>|<span data-ttu-id="3730e-128">x</span><span class="sxs-lookup"><span data-stu-id="3730e-128">x</span></span>
|[<span data-ttu-id="3730e-129">Informix</span><span class="sxs-lookup"><span data-stu-id="3730e-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="3730e-130">x</span><span class="sxs-lookup"><span data-stu-id="3730e-130">x</span></span>|<span data-ttu-id="3730e-131">x</span><span class="sxs-lookup"><span data-stu-id="3730e-131">x</span></span>
|[<span data-ttu-id="3730e-132">Dynamics 365 para Finanças</span><span class="sxs-lookup"><span data-stu-id="3730e-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="3730e-133">x</span><span class="sxs-lookup"><span data-stu-id="3730e-133">x</span></span>|<span data-ttu-id="3730e-134">x</span><span class="sxs-lookup"><span data-stu-id="3730e-134">x</span></span>
|[<span data-ttu-id="3730e-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="3730e-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="3730e-136">x</span><span class="sxs-lookup"><span data-stu-id="3730e-136">x</span></span>|<span data-ttu-id="3730e-137">x</span><span class="sxs-lookup"><span data-stu-id="3730e-137">x</span></span>
|[<span data-ttu-id="3730e-138">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="3730e-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="3730e-139">x</span><span class="sxs-lookup"><span data-stu-id="3730e-139">x</span></span>|<span data-ttu-id="3730e-140">x</span><span class="sxs-lookup"><span data-stu-id="3730e-140">x</span></span>
|[<span data-ttu-id="3730e-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="3730e-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="3730e-142">x</span><span class="sxs-lookup"><span data-stu-id="3730e-142">x</span></span>|<span data-ttu-id="3730e-143">x</span><span class="sxs-lookup"><span data-stu-id="3730e-143">x</span></span>
|[<span data-ttu-id="3730e-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="3730e-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="3730e-145">x</span><span class="sxs-lookup"><span data-stu-id="3730e-145">x</span></span>|<span data-ttu-id="3730e-146">x</span><span class="sxs-lookup"><span data-stu-id="3730e-146">x</span></span>
|[<span data-ttu-id="3730e-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="3730e-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="3730e-148">x</span><span class="sxs-lookup"><span data-stu-id="3730e-148">x</span></span>|<span data-ttu-id="3730e-149">x</span><span class="sxs-lookup"><span data-stu-id="3730e-149">x</span></span>
|[<span data-ttu-id="3730e-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3730e-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="3730e-151">x</span><span class="sxs-lookup"><span data-stu-id="3730e-151">x</span></span>|<span data-ttu-id="3730e-152">x</span><span class="sxs-lookup"><span data-stu-id="3730e-152">x</span></span>
|[<span data-ttu-id="3730e-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="3730e-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="3730e-154">x</span><span class="sxs-lookup"><span data-stu-id="3730e-154">x</span></span>|<span data-ttu-id="3730e-155">x</span><span class="sxs-lookup"><span data-stu-id="3730e-155">x</span></span>
|<span data-ttu-id="3730e-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="3730e-156">UserVoice</span></span>||<span data-ttu-id="3730e-157">x</span><span class="sxs-lookup"><span data-stu-id="3730e-157">x</span></span>|<span data-ttu-id="3730e-158">x</span><span class="sxs-lookup"><span data-stu-id="3730e-158">x</span></span>
|<span data-ttu-id="3730e-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="3730e-159">Zendesk</span></span>||<span data-ttu-id="3730e-160">x</span><span class="sxs-lookup"><span data-stu-id="3730e-160">x</span></span>|<span data-ttu-id="3730e-161">x</span><span class="sxs-lookup"><span data-stu-id="3730e-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="3730e-162">Conexões de tabela externa também podem ser usadas nos [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="3730e-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="3730e-163">Criar uma conexão de API: passo a passo</span><span class="sxs-lookup"><span data-stu-id="3730e-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="3730e-164">Criar uma função > função personalizada ![Criar uma função personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="3730e-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="3730e-165">Modelo `Experimental` > `ExternalTable-CSharp` de cenário > Criar uma nova `External Table connection`
![Escolher modelo de entrada de tabela](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="3730e-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="3730e-166">Escolha seu provedor de SaaS > escolha/crie uma conexão ![Configurar conexão de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="3730e-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="3730e-167">Selecione a conexão da API > Criar função hello ![Criar função de tabela](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="3730e-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="3730e-168">Selecionar `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="3730e-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="3730e-169">Configure Olá conexão toouse sua tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="3730e-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="3730e-170">Essas configurações irão variar entre provedores de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3730e-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="3730e-171">Elas estão destacados abaixo nas [configurações de fonte de dados](#datasourcesettings)
![Configurar tabela](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="3730e-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="3730e-172">Uso</span><span class="sxs-lookup"><span data-stu-id="3730e-172">Usage</span></span>

<span data-ttu-id="3730e-173">Este exemplo conecta-se a tabela tooa chamada "Contato" com colunas FirstName, LastName e Id.</span><span class="sxs-lookup"><span data-stu-id="3730e-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="3730e-174">código Olá lista as entidades de contato de saudação na tabela hello e logs Olá nomes e sobrenomes.</span><span class="sxs-lookup"><span data-stu-id="3730e-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="3730e-175">Associações</span><span class="sxs-lookup"><span data-stu-id="3730e-175">Bindings</span></span>
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
<span data-ttu-id="3730e-176">`entityId` deve estar vazia para associações de tabela.</span><span class="sxs-lookup"><span data-stu-id="3730e-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="3730e-177">`ConnectionAppSettingsKey`identifica a configuração do aplicativo hello que armazena a cadeia de caracteres de conexão do hello API.</span><span class="sxs-lookup"><span data-stu-id="3730e-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="3730e-178">Hello configuração do aplicativo é criada automaticamente quando você adiciona uma API de conexão no hello integrar a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="3730e-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="3730e-179">Um conector tabular fornece conjuntos de dados e cada conjunto de dados contém tabelas.</span><span class="sxs-lookup"><span data-stu-id="3730e-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="3730e-180">nome de Olá Olá padrão do conjunto de dados é "padrão".</span><span class="sxs-lookup"><span data-stu-id="3730e-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="3730e-181">títulos de saudação para um conjunto de dados e uma tabela em vários provedores de SaaS são listados abaixo:</span><span class="sxs-lookup"><span data-stu-id="3730e-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="3730e-182">Conector</span><span class="sxs-lookup"><span data-stu-id="3730e-182">Connector</span></span>|<span data-ttu-id="3730e-183">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="3730e-183">Dataset</span></span>|<span data-ttu-id="3730e-184">Tabela</span><span class="sxs-lookup"><span data-stu-id="3730e-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="3730e-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="3730e-185">**SharePoint**</span></span>|<span data-ttu-id="3730e-186">Site</span><span class="sxs-lookup"><span data-stu-id="3730e-186">Site</span></span>|<span data-ttu-id="3730e-187">Lista do SharePoint</span><span class="sxs-lookup"><span data-stu-id="3730e-187">SharePoint List</span></span>
|<span data-ttu-id="3730e-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="3730e-188">**SQL**</span></span>|<span data-ttu-id="3730e-189">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="3730e-189">Database</span></span>|<span data-ttu-id="3730e-190">Tabela</span><span class="sxs-lookup"><span data-stu-id="3730e-190">Table</span></span> 
|<span data-ttu-id="3730e-191">**Google Sheet**</span><span class="sxs-lookup"><span data-stu-id="3730e-191">**Google Sheet**</span></span>|<span data-ttu-id="3730e-192">Planilha</span><span class="sxs-lookup"><span data-stu-id="3730e-192">Spreadsheet</span></span>|<span data-ttu-id="3730e-193">Planilha</span><span class="sxs-lookup"><span data-stu-id="3730e-193">Worksheet</span></span> 
|<span data-ttu-id="3730e-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="3730e-194">**Excel**</span></span>|<span data-ttu-id="3730e-195">Arquivo do Excel</span><span class="sxs-lookup"><span data-stu-id="3730e-195">Excel file</span></span>|<span data-ttu-id="3730e-196">Folha</span><span class="sxs-lookup"><span data-stu-id="3730e-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="3730e-197">Uso em C#</span><span class="sxs-lookup"><span data-stu-id="3730e-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
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

<span data-ttu-id="3730e-198"><!--
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
## Configurações de Fonte de Dados</span><span class="sxs-lookup"><span data-stu-id="3730e-198"><!--
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

### <a name="sql-server"></a><span data-ttu-id="3730e-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3730e-199">SQL Server</span></span>

<span data-ttu-id="3730e-200">Olá toocreate de script e popular tabela de contato hello está abaixo.</span><span class="sxs-lookup"><span data-stu-id="3730e-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="3730e-201">dataSetName é “padrão”.</span><span class="sxs-lookup"><span data-stu-id="3730e-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="3730e-202">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="3730e-202">Google Sheets</span></span>
<span data-ttu-id="3730e-203">No Google Docs, crie uma planilha com uma planilha chamada `Contact`.</span><span class="sxs-lookup"><span data-stu-id="3730e-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="3730e-204">conector de saudação não pode usar o nome de exibição de planilha de saudação.</span><span class="sxs-lookup"><span data-stu-id="3730e-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="3730e-205">nome interno da saudação (em negrito) precisa toobe usado como dataSetName, por exemplo: `docs.google.com/spreadsheets/d/` ** `1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0` ** adicionar nomes de coluna Olá `Id`, `LastName`, `FirstName` toohello primeira linha, em seguida, popular dados em linhas subsequentes.</span><span class="sxs-lookup"><span data-stu-id="3730e-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="3730e-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="3730e-206">Salesforce</span></span>
<span data-ttu-id="3730e-207">dataSetName é “padrão”.</span><span class="sxs-lookup"><span data-stu-id="3730e-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="3730e-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3730e-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
