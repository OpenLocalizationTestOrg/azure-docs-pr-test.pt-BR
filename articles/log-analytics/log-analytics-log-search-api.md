---
title: "pesquisa de log de análise de aaaLog API REST | Microsoft Docs"
description: "Este guia fornece um tutorial básico que descreve como você pode usar o hello REST API de pesquisa de análise de Log em Olá Operations Management Suite (OMS) e fornece exemplos que mostram como comandos de saudação toouse."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>API REST de pesquisa de log do Log Analytics
Este guia fornece um tutorial básico, incluindo exemplos de como você pode usar o hello API de REST de pesquisa de análise de Log. Análise de log é parte da saudação Operations Management Suite (OMS).

> [!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você deve continuar a linguagem de consulta herdados de saudação do toouse com a API de pesquisa de log de saudação conforme descrito neste artigo.  Uma nova API será liberada para espaços de trabalho atualizados e documentação hello será atualizada no momento. 

> [!NOTE]
> Análise de log foi chamada anteriormente os Insights operacionais, por isso é o nome de saudação usado no provedor de recursos de saudação.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Visão geral da API de REST de pesquisa de Log de saudação
Olá API de REST de pesquisa de análise de Log é RESTful e pode ser acessado via Olá API do Gerenciador de recursos do Azure. Este artigo fornece exemplos de como acessar por meio da API Olá [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação Olá API do Gerenciador de recursos do Azure. uso de saudação do cliente do ARM é um dos muitos Olá de tooaccess opções API de pesquisa de análise de Log. Outra opção é toouse hello Azure PowerShell para OperationalInsights, que inclui cmdlets para acessar a pesquisa. Com essas ferramentas, você pode utilizar Olá API do Gerenciador de recursos do Azure toomake chamadas tooOMS espaços de trabalho e executar comandos de pesquisa dentro deles. Olá API produz resultados da pesquisa no formato JSON, permitindo que você resultados da pesquisa Olá toouse de diferentes maneiras por meio de programação.

Hello Azure Resource Manager pode ser usado por meio de um [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) e hello [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn mais, examine a páginas da web de saudação vinculada.

> [!NOTE]
> Se você usar um comando de agregação, como `|measure count()` ou `distinct`, cada chamada toosearch pode retornar até 500.000 registros. Pesquisas que não incluem um comando de agregação retornam até 5.000 registros.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Tutorial básico da API REST de Pesquisa do Log Analytics
### <a name="toouse-armclient"></a>toouse ARMClient
1. Instale o [Chocolatey](https://chocolatey.org/), que é um gerenciador de pacotes de software livre para Windows. Abra uma janela de prompt de comando como administrador e execute Olá comando a seguir:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Instale o cliente do ARM executando Olá comando a seguir:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform uma pesquisa usando o ARMClient
1. Entre usando a conta da Microsoft ou sua conta corporativa ou de estudante:

    ```
    armclient login
    ```

    Um logon bem-sucedido lista todas as toohello assinaturas vinculadas dado conta:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Obter espaços de trabalho do hello Operations Management Suite:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Uma chamada Get bem-sucedida geraria que todos os espaços de trabalho vinculado toohello assinatura:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Crie sua variável de pesquisa:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Pesquise usando sua nova variável de pesquisa:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Exemplos de referência da API REST de Pesquisa do Log Analytics
Olá exemplos a seguir mostra como você pode usar o hello API de pesquisa.

### <a name="search---actionread"></a>Pesquisa - ação/leitura
**Url de exemplo:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Solicitação:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.

| **Propriedade** | **Descrição** |
| --- | --- |
| top |número máximo de saudação do tooreturn de resultados. |
| highlight |Contém parâmetros anteriores e subsequentes, geralmente usados para realçar campos correspondentes |
| pre |Prefixos Olá fornecido campos de tooyour correspondida de cadeia de caracteres. |
| post |Acrescenta Olá fornecido campos de tooyour correspondida de cadeia de caracteres. |
| query |consulta de pesquisa Olá usado toocollect e retornar resultados. |
| iniciar |partir do Olá Olá da janela de tempo que você deseja toobe resultados encontrado. |
| end |fim de Olá Olá da janela de tempo que você deseja toobe resultados encontrado. |

**Resposta:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Pesquisa/{ID} - ação/leitura
**Olá o conteúdo da solicitação de uma pesquisa salva:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Se a pesquisa de saudação retornar com um status 'Pendente', resultados de saudação atualizado de sondagem podem ser feitos por essa API. Após 6 minutos, Olá resultado da pesquisa de saudação será eliminado do cache de saudação e HTTP Gone será retornado. Se a solicitação inicial de pesquisa de saudação retorna um status 'Bem-sucedido' imediatamente, resultados de saudação não são adicionados toohello cache causando esse tooreturn API HTTP Gone se consultada. conteúdo de saudação de um resultado de HTTP 200 está no mesmo formato que a solicitação inicial de pesquisa de saudação apenas com valores atualizados de saudação.
>
>

### <a name="saved-searches"></a>Pesquisas salvas
**Solicite a lista de pesquisas salvas:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Métodos com suporte: GET, PUT e DELETE

Métodos de coleção com suporte: GET

Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.

| Propriedade | Descrição |
| --- | --- |
| ID |Identificador exclusivo da saudação. |
| Etag |**Obrigatório para o Patch**. Atualizado pelo servidor em cada gravação. O valor deve ser o valor armazenado atual de toohello igual ou ' *' tooupdate. 409 retornado para valores antigos ou inválidos. |
| properties.query |**Obrigatório**. consulta de pesquisa de saudação. |
| properties.displayName |**Obrigatório**. nome para exibição definidos pelo usuário Olá de consulta de saudação. |
| properties.category |**Obrigatório**. categoria definida pelo usuário Olá de consulta de saudação. |

> [!NOTE]
> Olá API de pesquisa de análise de Log atualmente retorna criados pelo usuário pesquisas salvas quando sondada para pesquisas salvas em um espaço de trabalho. Olá API não retornará pesquisas salvas fornecidas por soluções.
>
>

### <a name="create-saved-searches"></a>Criar pesquisas salvas
**Solicitação:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.

### <a name="delete-saved-searches"></a>Excluir pesquisas salvas
**Solicitação:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Atualizar pesquisas salvas
 **Solicitação:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metadados - somente JSON
Aqui está um campos do modo toosee Olá para todos os tipos de log para dados de saudação coletados em seu espaço de trabalho. Por exemplo, se você quiser que saber se o tipo de evento de saudação tem um campo chamado computador, essa consulta é uma maneira toocheck.

**Solicitação por campos:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Resposta:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.

| **Propriedade** | **Descrição** |
| --- | --- |
| name |Nome do campo. |
| displayName |Olá exibir nome do campo de saudação. |
| type |Tipo de valor de campo de saudação do Hello. |
| facetable |Combinação das propriedades 'indexed', 'stored' e 'facet' atuais. |
| display |Propriedade 'display' atual. True se o campo está visível na pesquisa. |
| ownerType |Tipos de tooonly reduzido que pertencem a endereços IP tooonboarded. |

## <a name="optional-parameters"></a>Parâmetros opcionais
Olá informações a seguir descreve os parâmetros opcionais disponíveis.

### <a name="highlighting"></a>Realce
Olá "Highlight" é um parâmetro opcional que você pode usar o subsistema da pesquisa toorequest Olá inclua um conjunto de marcadores em sua resposta.

Esses marcadores indicam Olá início e término do texto realçado que coincide com os termos de saudação fornecidos na consulta de pesquisa.
Você pode especificar o início de saudação e terminar marcadores que são usados por um termo da pesquisa toowrap Olá realçado.

**Exemplo de consulta de pesquisa**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Resultado de exemplo:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Observe que Olá resultado acima contém uma mensagem de erro que o prefixo e anexada.

## <a name="computer-groups"></a>Grupos de computadores
Grupos de computadores são pesquisas especiais salvas que retornam um conjunto de computadores.  Você pode usar um grupo de computadores em outros computadores consultas toolimit Olá resultados toohello no grupo de saudação.  Um grupo de computadores é implementado como uma pesquisa salva com uma marca de Grupo com um valor de Computador.

A seguir está um exemplo de resposta para um grupo de computadores.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Recuperando grupos de computadores
ID de um grupo de computadores, use Olá método Get com grupo hello. tooretrieve

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Criar ou atualizar um grupo de computadores
toocreate um grupo de computadores, use Olá método Put com uma ID de pesquisa salva exclusivo. Se você usar uma ID de grupo de computador existente, ela será modificada. Quando você cria um grupo de computadores no portal de análise de Log hello, Olá ID é criado de nome e grupo de saudação.

consulta Olá usada para definição de grupo Olá deve retornar um conjunto de computadores para Olá grupo toofunction corretamente.  É recomendável que você encerrar sua consulta com `| Distinct Computer` tooensure Olá correto de dados são retornados.

definição de saudação do hello pesquisa salva deve incluir uma marca chamada grupo com um valor de computador para Olá pesquisa toobe classificado como um grupo de computadores.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Excluindo grupos de computadores
ID de um grupo de computadores, use Olá método Delete com grupo hello. toodelete

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toobuild consultas usando campos personalizados para os critérios.
