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
# <a name="azure-functions-external-table-binding-preview"></a>Associação de tabela externa do Azure Functions (versão prévia)
Este artigo mostra como dados de tabela toomanipulate nos provedores de SaaS (por exemplo, Sharepoint, Dynamics) dentro de sua função com ligações internas. O Azure Functions dá suporte a associações de entrada e saída para tabelas externas.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>Conexões de API

Associações de tabela aproveitam tooauthenticate de conexões de API externa com provedores de SaaS 3ª parte. 

Ao atribuir uma associação você pode criar uma nova conexão de API ou usar uma conexão existente de API em Olá mesmo grupo de recursos

### <a name="supported-api-connections-tables"></a>Conexões de API com suporte (Tabela)s

|Conector|Gatilho|Entrada|Saída|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 para Operações](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google Sheets](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 para Finanças](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Banco de dados Oracle](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> Conexões de tabela externa também podem ser usadas nos [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)

### <a name="creating-an-api-connection-step-by-step"></a>Criar uma conexão de API: passo a passo

1. Criar uma função > função personalizada ![Criar uma função personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Modelo `Experimental` > `ExternalTable-CSharp` de cenário > Criar uma nova `External Table connection`
![Escolher modelo de entrada de tabela](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Escolha seu provedor de SaaS > escolha/crie uma conexão ![Configurar conexão de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Selecione a conexão da API > Criar função hello ![Criar função de tabela](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Selecionar `Integrate` > `External Table`
    1. Configure Olá conexão toouse sua tabela de destino. Essas configurações irão variar entre provedores de SaaS. Elas estão destacados abaixo nas [configurações de fonte de dados](#datasourcesettings)
![Configurar tabela](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Uso

Este exemplo conecta-se a tabela tooa chamada "Contato" com colunas FirstName, LastName e Id. código Olá lista as entidades de contato de saudação na tabela hello e logs Olá nomes e sobrenomes.

### <a name="bindings"></a>Associações
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
`entityId` deve estar vazia para associações de tabela.

`ConnectionAppSettingsKey`identifica a configuração do aplicativo hello que armazena a cadeia de caracteres de conexão do hello API. Hello configuração do aplicativo é criada automaticamente quando você adiciona uma API de conexão no hello integrar a interface do usuário.

Um conector tabular fornece conjuntos de dados e cada conjunto de dados contém tabelas. nome de Olá Olá padrão do conjunto de dados é "padrão". títulos de saudação para um conjunto de dados e uma tabela em vários provedores de SaaS são listados abaixo:

|Conector|Conjunto de dados|Tabela|
|:-----|:---|:---| 
|**SharePoint**|Site|Lista do SharePoint
|**SQL**|Banco de dados|Tabela 
|**Google Sheet**|Planilha|Planilha 
|**Excel**|Arquivo do Excel|Folha 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Uso em C# #

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

<!--
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
## Configurações de Fonte de Dados

### <a name="sql-server"></a>SQL Server

Olá toocreate de script e popular tabela de contato hello está abaixo. dataSetName é “padrão”.

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

### <a name="google-sheets"></a>Google Sheets
No Google Docs, crie uma planilha com uma planilha chamada `Contact`. conector de saudação não pode usar o nome de exibição de planilha de saudação. nome interno da saudação (em negrito) precisa toobe usado como dataSetName, por exemplo: `docs.google.com/spreadsheets/d/` ** `1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0` ** adicionar nomes de coluna Olá `Id`, `LastName`, `FirstName` toohello primeira linha, em seguida, popular dados em linhas subsequentes.

### <a name="salesforce"></a>Salesforce
dataSetName é “padrão”.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
