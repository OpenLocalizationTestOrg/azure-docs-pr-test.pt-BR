---
title: "aaaWorkflow ações e gatilhos - os aplicativos lógicos do Azure | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Ações do fluxo de trabalho e gatilhos para os Aplicativos Lógicos do Azure

Os aplicativos lógicos são compostos por gatilhos e ações. Há seis tipos de gatilhos. Cada tipo tem um comportamento e interface diferentes. Você também pode saber sobre outros detalhes examinando os detalhes de saudação do hello [linguagem de definição de fluxo de trabalho](logic-apps-workflow-definition-language.md).  
  
Ler em toolearn mais informações sobre gatilhos e ações e como você pode usá-los toobuild lógica aplicativos tooimprove seus processos de negócios e fluxos de trabalho.  
  
### <a name="triggers"></a>Gatilhos  

Um gatilho Especifica chamadas de saudação que podem iniciar uma execução de fluxo de trabalho de aplicativo sua lógica. Aqui estão duas maneiras diferentes de saudação tooinitiate uma execução do fluxo de trabalho:  
  
-   Gatilho de sondagem  

-   Um disparador de envio - por chamada hello [API REST do serviço de fluxo de trabalho](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Todos os gatilhos contêm estes elementos de alto nível:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Tipos de gatilho e suas entradas  

Você pode usar estes tipos de gatilhos:
  
-   **Solicitar** \- torna o aplicativo de lógica de saudação um ponto de extremidade para você toocall  
  
-   **Recorrência** \- é acionado com base em um agendamento definido  
  
-   **HTTP** \- sonda um ponto de extremidade HTTP da Web. ponto de extremidade Olá HTTP deve estar em conformidade tooa contrato específica de disparo \- usando um 202\-padrão assíncrono, ou retornando uma matriz  
  
-   **ApiConnection** \- disparam sondagens como Olá HTTP, no entanto, se beneficia do hello [APIs gerenciada pela Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- abre um ponto de extremidade, semelhante toohello gatilho Manual, no entanto, ele também chama tooa especificado tooregister de URL e cancelar o registro  
  
-   **ApiConnectionWebhook** \- opera como Olá HTTPWebhook gatilho aproveitando Olá APIs gerenciada pela Microsoft       
    Cada tipo de gatilho tem um conjunto diferente de **entradas** que define seu comportamento.  
  
## <a name="request-trigger"></a>Gatilho de solicitação  

Esse gatilho serve como um ponto de extremidade que você chamar por meio de uma solicitação HTTP tooinvoke seu aplicativo lógico. Um gatilho de solicitação é semelhante a este exemplo:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Há também uma propriedade opcional denominada **esquema**:  
  
|Nome do elemento|Obrigatório|Descrição|  
|----------------|------------|---------------|  
|schema|Não|Um esquema JSON que valida a solicitação de entrada hello. Útil para ajudar a saber quais propriedades tooreference etapas subsequentes do fluxo de trabalho.|

tooinvoke esse ponto de extremidade, você precisa Olá toocall *listCallbackUrl* API. Consulte [API REST do Serviço do Fluxo de Trabalho](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Gatilho de recorrência  

Um gatilho de Recorrência é aquele executado com base em um agendamento definido. Tal gatilho pode parecer com este exemplo:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Como você pode ver, é uma maneira simples de toorun um fluxo de trabalho.  
  
|Nome do elemento|Obrigatório|Descrição|  
|----------------|------------|---------------|  
|frequência|Sim|Frequência hello gatilho é executado. Use apenas um desses valores possíveis: segundo, minuto, hora, dia, semana, mês ou ano|  
|intervalo|Sim|Intervalo de saudação atribuído a frequência de recorrência Olá|  
|startTime|Não|Se um startTime for fornecido sem uma diferença UTC, o fuso horário será usado.|  
|timeZone|não|Se um startTime for fornecido sem uma diferença UTC, o fuso horário será usado.|  
  
Você também pode agendar uma execução de gatilho toostart em algum momento no futuro de saudação. Por exemplo, se você quiser toostart toda segunda-feira de relatório de uma semana você pode agendar Olá lógica aplicativo toostart toda segunda-feira, criando Olá gatilho a seguir:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Gatilho HTTP  

Gatilhos HTTP sondagem um ponto de extremidade especificado e verifique Olá resposta toodetermine se o fluxo de trabalho Olá deve ser executado. objeto de entradas de saudação usa o conjunto de saudação de parâmetros necessários tooconstruct uma chamada HTTP:  
  
|Nome do elemento|Obrigatório|Descrição|Tipo|  
|----------------|------------|---------------|--------|  
|estático|sim|Pode ser uma saudação seguindo os métodos HTTP: GET, POST, PUT, DELETE, PATCH ou HEAD|Cadeia de caracteres|  
|uri|sim|Olá ponto de extremidade http ou https que é chamado. Máximo de 2 quilobytes.|Cadeia de caracteres|  
|consultas|Não|Um objeto que representa a URL do hello consulta parâmetros tooadd toohello. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|Objeto|  
|headers|Não|Um objeto que representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Objeto|  
|body|Não|Um objeto que representa a carga de saudação que é enviada toohello de ponto de extremidade.|Objeto|  
|retryPolicy|Não|Um objeto que permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.|Objeto|  
|autenticação|Não|Método hello representa que Olá solicitação deve ser autenticado. Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Além do Agendador, há mais uma propriedade com suporte: `authority` por padrão, esse valor é `https://login.windows.net` quando não especificado, mas você pode usar um público diferente como `https://login.windows\-ppe.net`|Objeto|  
  
gatilho HTTP Olá requer Olá API HTTP tooconform com toowork um padrão específico bem com seu aplicativo lógico. Ele requer Olá campos a seguir:  
  
|Resposta|Descrição|  
|------------|---------------|  
|Código de status|Código de status 200 \(Okey\) toocause uma execução. Qualquer outro código de status não provoca uma execução.|  
|Repetir\-após o cabeçalho|Número de segundos até que o aplicativo de lógica de saudação controla o ponto de extremidade Olá novamente.|  
|Cabeçalho do local|Olá toocall de URL no próximo intervalo de sondagem hello. Se não for especificado, a URL original Olá é usado.|  
  
Aqui estão alguns exemplos de comportamentos diferentes para diferentes tipos de solicitações:  
  
|Código de resposta|Repetir\-Após|Comportamento|  
|-----------------|----------------|------------|  
|200|\(nenhum\)|Não válido disparador, repetição\-após mecanismo Olá necessária, caso contrário nunca é sondagens para a próxima solicitação de saudação.|  
|202|60|Não disparar o fluxo de trabalho de saudação. próxima tentativa de saudação ocorre em um minuto.|  
|200|10|Executar o fluxo de trabalho hello e verificar novamente para o conteúdo de mais de 10 segundos.|  
|400|\(nenhum\)|Solicitação incorreta, não execute o fluxo de trabalho de saudação. Se não houver nenhum **política de repetição** definido, então a saudação padrão política é usada. Depois que o número de saudação de novas tentativas foi atingido, gatilho Olá não é mais válido.|  
|500|\(nenhum\)|Erro de servidor, não são executados fluxo de trabalho de saudação.  Se não houver nenhum **política de repetição** definido, então a saudação padrão política é usada. Depois que o número de saudação de novas tentativas foi atingido, gatilho Olá não é mais válido.|  
  
saídas de saudação de um gatilho HTTP se parecer com este exemplo:  
  
|Nome do elemento|Descrição|Tipo|  
|----------------|---------------|--------|  
|headers|cabeçalhos de saudação de resposta de http hello.|Objeto|  
|body|corpo de saudação de resposta de http hello.|Objeto|  
  
## <a name="api-connection-trigger"></a>Gatilho de conexão da API  

Olá API conexão gatilho é semelhante toohello HTTP em sua funcionalidade básica. No entanto, os parâmetros de saudação para identificar a ação de saudação são diferentes. Aqui está um exemplo:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Nome do elemento|Obrigatório|Tipo|Descrição|  
|----------------|------------|--------|---------------|  
|host|Sim||Olá ApiApp hospedado gateway e id.|  
|estático|Sim|Cadeia de caracteres|Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**|  
|consultas|Não|Objeto|Toobe de parâmetros de consulta representa Olá adicionado toohello URL. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|  
|headers|Não|Objeto|Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Não|Objeto|Representa a carga de saudação que é enviada toohello de ponto de extremidade.|  
|retryPolicy|Não|Objeto|Permite a você o comportamento de repetição de saudação toocustomize erros 4xx ou 5xx.|  
|Autenticação|Não|Objeto|Método hello representa que Olá solicitação deve ser autenticado. Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
Propriedades de saudação de host são:  
  
|Nome do elemento|Obrigatório|Descrição|  
|----------------|------------|---------------|  
|api runtimeUrl|Sim|ponto de extremidade de saudação do hello API gerenciada.|  
|nome da conexão||Deve ser um parâmetro de referência tooa chamado `$connection` e é o nome da saudação de conexão de API Olá gerenciado que Olá usos de fluxo de trabalho.|
  
saídas de saudação de um gatilho de conexão de API são:
  
|Nome do elemento|Tipo|Descrição|  
|----------------|--------|---------------|  
|headers|Objeto|cabeçalhos de saudação de resposta de http hello.|  
|body|Objeto|corpo de saudação de resposta de http hello.|  
  
## <a name="httpwebhook-trigger"></a>Gatilho HTTPWebhook  

Aberturas de gatilho HTTPWebhook Olá um ponto de extremidade, gatilho manual de toohello semelhantes, mas Olá HTTPWebhook gatilho também chama tooa especificada URL tooregister e cancelar o registro. Aqui está um exemplo de como um gatilho HTTPWebhook pode ser:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Muitas dessas seções são opcionais e comportamento Olá Olá Webhook depende de quais seções são fornecidas ou omitidas.  
Propriedades de saudação de um Webhook são da seguinte maneira:  
  
|Nome do elemento|Obrigatório|Descrição|  
|----------------|------------|---------------|  
|assinar|Não|saudação de solicitação que é chamada quando o gatilho de saudação é criado e executa o registro inicial Olá de saída.|  
|cancelar assinatura|Não|saudação de solicitação de saída quando Olá gatilho é excluído.|  
  
-   **Assinar** é Olá chamada que fez toostart tooevents de escuta de saída. Essa chamada começa com saudação mesmo conjunto de parâmetros que Olá normais ações de HTTP. Esta chamada de saída é feita qualquer Olá tempo alterações de fluxo de trabalho de qualquer forma, por exemplo, sempre que as credenciais de saudação serão revertidas, ou alterar parâmetros de entrada do gatilho de saudação.
  
    toosupport chamar, há uma nova função: `@listCallbackUrl()`. Esta função retorna uma URL exclusiva para esse gatilho específico neste fluxo de trabalho. Ele representa o identificador exclusivo de saudação para pontos de extremidade de saudação que usam Olá serviço REST.  
  
-   **Cancelar assinatura** é chamado quando uma operação apresenta o gatilho como inválido, incluindo:  
  
    -   Excluir ou desabilitar o gatilho Olá  
  
    -   Excluir ou desabilitar o fluxo de trabalho Olá  
  
    -   Excluir ou desabilitar a assinatura de saudação  
  
    Olá lógica aplicativo chama automaticamente Olá cancelar a assinatura de ação. parâmetros de saudação toothis função são Olá mesmo como Olá HTTP.  
  
    Olá, saídas de gatilho de HTTPWebhook Olá são Olá conteúdo da solicitação de entrada hello:  
  
|Nome do elemento|Tipo|Descrição|  
|-----------------|--------|---------------|  
|headers|Objeto|cabeçalhos de saudação de solicitação de http hello.|  
|body|Objeto|corpo de saudação de solicitação de http hello.|  

Limites de uma ação de webhook podem ser especificados em Olá exatamente como [limites assíncronos HTTP](#asynchronous-limits).
  

## <a name="conditions"></a>Condições  

Para qualquer gatilho, você pode usar toodetermine de condições de uma ou mais se o fluxo de trabalho Olá deve ser executado ou não. Por exemplo:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Nesse caso, Olá gatilhos somente de relatório do fluxo de trabalho Olá `sendReports` parâmetro for definido tootrue. Por fim, condições podem fazer referência a código de status de saudação do gatilho de saudação. Por exemplo, você poderia iniciar um fluxo de trabalho somente quando seu site retornasse um código de status 500, como a seguir:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Quando qualquer expressão referencia o código de status de saudação do gatilho de saudação \(de qualquer forma\), Olá comportamento padrão \(gatilho apenas em 200 \(Okey\) \) é substituído. Por exemplo, se você quiser tootrigger no código de status 200 e o código de status 201, ter tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` como sua condição.  
  
## <a name="start-multiple-runs-for-a-request"></a>Iniciar várias execuções para uma solicitação

tookick desativar várias execuções para uma única solicitação, `splitOn` é útil, por exemplo, quando você deseja toopoll um ponto de extremidade que pode ter vários novos itens entre os intervalos de sondagem.
  
Com `splitOn`, você especifica a propriedade hello dentro Olá carga de resposta que contém a matriz de saudação de itens, cada um dos quais você deseja toouse toostart uma execução de gatilho hello. Por exemplo, imagine que você tem uma API que retorna Olá resposta a seguir:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Sua lógica de aplicativo só precisa conteúdo de linhas de saudação, portanto você pode construir seu gatilho semelhante a este exemplo:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Em seguida, na definição de fluxo de trabalho hello, `@triggerBody().name` retorna `mycoolrow` para Olá executado pela primeira vez, e `another row` para execução segundo hello. Olá gatilho saídas aparência semelhante a este exemplo:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Portanto, se você usar `SplitOn`, não é possível obter propriedades de saudação que estão fora da matriz de hello, nesse caso, Olá `Status` campo.  
  
> [!NOTE]  
> Neste exemplo, usamos Olá `?` tooavoid do operador toobe capaz de uma falha se hello `Rows` propriedade não está presente. 
  
## <a name="single-run-instance"></a>Instância de execução única

Você pode configurar os gatilhos que têm um incêndio de tooonly de propriedade de recorrência se tem concluído todas as execuções ativas. Se uma recorrência agendada ocorrer enquanto houver uma execução em andamento, gatilho Olá ignora e aguarda até Olá próxima recorrência agendado intervalo toocheck novamente.

Você pode configurar essa configuração por meio de opções de operação hello:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Tipos e entradas  

Há muitos tipos de ações, cada um com um comportamento exclusivo. As ações de coleção podem conter muitas outras ações em si.

### <a name="standard-actions"></a>Ações padrão  

-   **HTTP** esta ação chama um ponto de extremidade HTTP da Web.  
  
-   **ApiConnection** \- essa ação se comporta como Olá ação HTTP, mas usa Olá APIs gerenciada pela Microsoft.  
  
-   **ApiConnectionWebhook** \- como HTTPWebhook, mas usa Olá APIs gerenciada pela Microsoft.  
  
-   **Resposta** \- esta ação define uma resposta para uma chamada de entrada.  
  
-   **Aguardar** \- esta ação simples aguarda um período fixo de tempo ou até uma hora específica.  
  
-   **Fluxo de trabalho** \- esta ação representa um fluxo de trabalho aninhado.  

-   **Função** \- essa ação representa uma função do Azure.

### <a name="collection-actions"></a>Ações de coleção

-   **Escopo** \- esta ação é um agrupamento lógico de outras ações.

-   **Condição** \- essa ação avalia uma expressão e executa a ramificação de resultado correspondente hello.

-   **ForEach** \- esta ação de loop itera uma matriz e executa as ações internas de cada item.

-   **Até** \- esta ação loop executa ações internas até que uma condição tootrue os resultados.
  
Cada tipo de ação tem um conjunto diferente de **entradas** que definem o comportamento de uma ação.  
  
## <a name="http-action"></a>Ação HTTP  

Ações de HTTP chamar um ponto de extremidade especificado e verifique Olá resposta toodetermine se o fluxo de trabalho Olá deve ser executado. Olá **entradas** objeto usa o conjunto de saudação de parâmetros necessários tooconstruct Olá HTTP chamada:  
  
|Nome do elemento|Obrigatório|Tipo|Descrição|  
|----------------|------------|--------|---------------|  
|estático|Sim|Cadeia de caracteres|Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**|  
|uri|Sim|Cadeia de caracteres|Olá ponto de extremidade http ou https que é chamado. O comprimento máximo é 2 quilobytes.|  
|consultas|Não|Objeto|Representa Olá consulta parâmetros tooadd toohello URL. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|  
|headers|Não|Objeto|Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Não|Objeto|Representa a carga de saudação que é enviada toohello de ponto de extremidade.|  
|retryPolicy|Não|Objeto|Permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.|  
|operationsOptions|Não|Cadeia de caracteres|Define o conjunto de saudação do toooverride comportamentos especiais.|  
|Autenticação|Não|Objeto|Método hello representa que Olá solicitação deve ser autenticado. Para obter detalhes sobre esse objeto, consulte [Autenticação de Saída do Agendador](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Além do agendador, há mais uma propriedade com suporte: `authority`. Por padrão, isto é `https://login.windows.net` quando não especificado, mas você pode usar um público diferente como`https://login.windows\-ppe.net`|  
  
As ações HTTP \(e as ações de Conexão da API\) têm suporte para as políticas de repetição. Uma política de repetição se aplica a toointermittent falhas, caracterizadas como status do HTTP 408 429 e 5xx em exceções de conectividade de tooany de adição de códigos. Essa política é descrita usando Olá *retryPolicy* objeto definido como mostrado aqui:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
intervalo de repetição de saudação é especificado no formato de saudação ISO 8601. Esse intervalo tem um padrão e o valor mínimo de 20 segundos, enquanto o valor máximo de saudação é de uma hora. saudação padrão e máximo de contagem de repetição é de quatro horas. Se a definição de política de repetição de saudação não for especificada, um `fixed` estratégia é usada com valores de contagem e o intervalo de repetição padrão. política de repetição de saudação toodisable, defina seu tipo muito`None`.  
  
Por exemplo, hello ação a seguir repete as notícias mais recentes do busca Olá duas vezes, se houver falhas intermitentes, para um total de execuções de três, com um atraso de 30 segundos entre cada tentativa de:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Padrões assíncronos

Por padrão, todas as ações com base em HTTP oferece suporte a padrões de operação assíncrona padrão de saudação. Portanto, se o servidor remoto Olá indica que a solicitação Olá é aceita para processamento com um 202 \(aceito\) resposta, o mecanismo de aplicativos lógicos Olá mantém sondagem Olá URL especificado no cabeçalho de local da resposta Olá até atingir um terminal estado \(não\-resposta 202\).  
  
comportamento assíncrono do toodisable Olá anteriormente descrito, defina um `DisableAsyncPattern` opção em entradas de ação de saudação. Nesse caso, a saída de hello da ação de saudação é baseada na resposta 202 inicial de saudação do servidor de saudação.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Limites Assíncronos

Um padrão assíncrono pode ser limitado no intervalo de tempo específico de tooa sua duração.  Se o intervalo de tempo de saudação expira sem atingir um estado terminal, status de saudação de ação de saudação serão marcadas `Cancelled` com um código de `ActionTimedOut`.  tempo limite de limite de saudação é especificado no formato ISO 8601.  Limites podem ser especificados com hello sintaxe a seguir:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>Conexão da API  

A Conexão da API é uma ação que se refere a um conector gerenciado pela Microsoft.
Essa ação requer uma conexão válida do tooa de referência e informações sobre Olá API e os parâmetros necessários.

|Nome do elemento|Obrigatório|Tipo|Descrição|  
|----------------|------------|--------|---------------|  
|host|Sim|Objeto|Representa informações de conector hello como objeto de conexão de toohello de runtimeUrl e referência de saudação|
|estático|Sim|Cadeia de caracteres|Pode ser uma saudação métodos HTTP a seguir: **obter**, **POST**, **colocar**, **excluir**, **PATCH**, ou  **CABEÇALHO**|  
|path|Sim|Cadeia de caracteres|caminho de saudação da operação de saudação API.|  
|consultas|Não|Objeto|Representa Olá consulta parâmetros tooadd toohello URL. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|  
|headers|Não|Objeto|Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Não|Objeto|Representa a carga de saudação que é enviada toohello de ponto de extremidade.|  
|retryPolicy|Não|Objeto|Permite que você personalize o comportamento de repetição de saudação erros 4xx ou 5xx.|  
|operationsOptions|Não|Cadeia de caracteres|Define o conjunto de saudação do toooverride comportamentos especiais.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Ação do webhook de Conexão da API

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Limites de uma ação de webhook podem ser especificados em Olá exatamente como [limites assíncronos HTTP](#asynchronous-limits).
  
## <a name="response-action"></a>Ação de resposta  

Esse tipo de ação contém Olá carga de resposta inteira de uma solicitação HTTP e inclui um statusCode, corpo e cabeçalhos:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
ação de resposta Olá tem restrições especiais que não se aplicam a tooother ações. Especificamente:  
  
-   Ações de resposta não podem ser paralelas em uma definição porque é necessária uma solicitação de entrada toohello resposta determinística.  
  
-   Se uma ação de resposta é atingida depois de solicitação de entrada hello recebeu uma resposta, a ação de saudação é considerada falha \(conflito\), e como resultado, a saudação executar é `Failed`.  
  
-   Um fluxo de trabalho com ações de Resposta não pode ter um `splitOn` em seu gatilho porque uma chamada provoca muitas execuções. Como resultado, isso deve ser validado quando o fluxo de saudação é PUT e causa uma solicitação incorreta.  
  
## <a name="wait-action"></a>Ação para aguardar  

Olá `wait` ação suspende a execução do fluxo de trabalho para o intervalo especificado de saudação. Por exemplo, toowait 15 minutos, você pode usar este trecho de código:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
Como alternativa, toowait até um momento específico, você pode usar este exemplo:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> duração de espera de saudação pode ser especificada usando Olá **intervalo** objeto ou hello **até** objeto, mas não ambos.  
  
|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|intervalo|Não|Objeto|com base na quantidade de tempo de duração de espera de saudação.|  
|unidade do intervalo|Sim|Cadeia de caracteres|Um destes intervalos: segundo, minuto, hora, dia, semana, mês, ano.|  
|contagem do intervalo|Sim|Cadeia de caracteres|Duração com base em Olá fornecido unidade interna.|  
|until|Não|Objeto|com base em um ponto no tempo de duração de espera de saudação.|  
|until carimbo data/hora|Sim|Cadeia de caracteres|Cadeia de caracteres &#124; Olá pontual em UTC quando Olá espera expira.|  

## <a name="query-action"></a>Ação de consulta

Olá `query` ação permite que uma matriz com base em uma condição de filtro. Por exemplo, números de tooselect maiores que 2, você pode usar:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Olá saída de hello `query` ação é uma matriz com os elementos da matriz de entrada hello que satisfazem a condição de saudação.

> [!NOTE]
> Se nenhum valor satisfazer Olá `where` condição, hello, resultado é uma matriz vazia.

|Nome|Obrigatório|Tipo|Descrição|
|--------|------------|--------|---------------|
|Da|Sim|Matriz|matriz de origem Hello.|
|onde|Sim|Cadeia de caracteres|Olá condição tooapply tooeach elemento de matriz de origem hello.|

## <a name="select-action"></a>Ação selecionar

Olá `select` ação permite que cada elemento de uma matriz de projeto em um novo valor.
Por exemplo, tooconvert uma matriz de números em uma matriz de objetos, você pode usar:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Olá saída de hello `select` ação é uma matriz que tem Olá cardinalidade mesmo como Olá a matriz de entrada, com cada elemento transformado conforme definida pelo Olá `select` propriedade. Se a entrada de saudação é uma matriz vazia, a saída de hello também é uma matriz vazia.

|Nome|Obrigatório|Tipo|Descrição|
|--------|------------|--------|---------------|
|Da|Sim|Matriz|matriz de origem Hello.|
|selecionar|Sim|Qualquer|Olá projeção tooapply tooeach elemento de matriz de origem hello.|

## <a name="terminate-action"></a>Ação para finalizar

Olá terminar ação interrompe a execução de saudação fluxo de trabalho executar, anulando todas as ações em curso e ignorar as ações restantes. Por exemplo, tooterminate uma execução com status **falha**, você pode usar o hello trecho de código a seguir:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Ações concluídas já não são afetadas por Olá encerrar a ação.

|Nome|Obrigatório|Tipo|Descrição|
|--------|------------|--------|---------------|
|runStatus|Sim|Cadeia de caracteres|destino de saudação status de execução. **Falha** ou **Cancelado**.|
|runError|Não|Objeto|detalhes do erro Hello. Só há suporte para quando **runStatus** está definido muito**falha**.|
|código runError|Não|Cadeia de caracteres|Olá executar código de erro.|
|mensagem runError|Não|Cadeia de caracteres|Olá executar a mensagem de erro.|

## <a name="compose-action"></a>Ação para compor

Olá redigir ação permite que você construir um objeto arbitrário. saída de saudação do hello compor a ação é Olá resultado da avaliação de suas entradas. Por exemplo, você pode usar o hello compor saídas de toomerge ação várias ações:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Olá **redigir** ação pode ser usado tooconstruct qualquer saída, incluindo objetos, matrizes e qualquer outro tipo com suporte nativo aplicativos lógicos como XML e binário.

## <a name="table-action"></a>Ação tabela

Olá `table` permite que você tooconvert uma matriz de itens em uma **CSV** ou **HTML** tabela.

Suponha que @triggerBody() seja

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

E permitir que a ação de saudação ser definida como

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Olá acima produziria

<table><thead><tr><th>ID</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>apples</td></tr><tr><td>1</td><td>oranges</td></tr></tbody></table>"

Na tabela de saudação do toocustomize ordem, você pode especificar colunas Olá explicitamente. Por exemplo:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Olá acima produziria

<table><thead><tr><th>produce id</th><th>description</th></tr></thead><tbody><tr><td>0</td><td>fresh apples</td></tr><tr><td>1</td><td>fresh oranges</td></tr></tbody></table>"

Se hello `from` valor da propriedade é uma matriz vazia, a saída de hello é uma tabela vazia.

|Nome|Obrigatório|Tipo|Descrição|
|--------|------------|--------|---------------|
|Da|Sim|Matriz|matriz de origem Hello.|
|formato|Sim|Cadeia de caracteres|Olá formato, ou **CSV** ou **HTML**.|
|colunas|Não|Matriz|colunas de saudação. Permite que a forma do toooverride saudação padrão da tabela de saudação.|
|cabeçalho de coluna|Não|Cadeia de caracteres|cabeçalho de saudação da coluna de saudação.|
|valor da coluna|Sim|Cadeia de caracteres|valor de saudação da coluna de saudação.|

## <a name="workflow-action"></a>Ação do fluxo de trabalho   

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|id do host|Sim|Cadeia de caracteres|ID do recurso de fluxo de trabalho de saudação que você deseja toocall Hello.|  
|triggerName do host|Sim|Cadeia de caracteres|nome de saudação do gatilho de saudação que você deseja tooinvoke.|  
|consultas|Não|Objeto|Representa Olá consulta parâmetros tooadd toohello URL. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|  
|headers|Não|Objeto|Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, tooset Olá idioma e o tipo em uma solicitação:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Não|Objeto|Representa a carga de saudação enviada toohello de ponto de extremidade.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Uma verificação de acesso é feita no fluxo de trabalho Olá \(mais especificamente, o gatilho Olá\), ou seja, você precisará de acesso toohello de fluxo de trabalho.  
  
Olá saídas de saudação `workflow` ação baseiam-se no que foi definido no hello `response` ação no fluxo de trabalho do hello filho. Se você não definiu nenhum `response` ação, em seguida, Olá saídas estão vazios.  

## <a name="function-action"></a>Ação de função   

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|Id de Função|Sim|Cadeia de caracteres|ID de recurso de saudação do função hello que você deseja tooinvoke.|  
|estático|Não|Cadeia de caracteres|Olá método HTTP usado tooinvoke função de saudação. Por padrão, ele é `POST` quando não especificada.|  
|consultas|Não|Objeto|Representa Olá consulta parâmetros tooadd toohello URL. Por exemplo, `"queries" : { "api-version": "2015-02-01" }` adiciona `?api-version=2015-02-01` toohello URL.|  
|headers|Não|Objeto|Representa cada um dos cabeçalhos de saudação toohello solicitação é enviada. Por exemplo, o idioma de saudação do tooset e o tipo em uma solicitação: `"headers" : { "Accept-Language": "en-us" }`.|  
|body|Não|Objeto|Representa a carga de saudação enviada toohello de ponto de extremidade.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Quando você salvar o aplicativo lógico de hello, podemos executar algumas verificações na função hello referenciada:
-   Você precisa de função de toohello toohave access.
-   Apenas o gatilho HTTP padrão ou gatilho de webhook JSON genérico é permitido.
-   Ele não deve ter nenhuma rota definida.
-   Apenas "função" e o nível de autorização "anônimo" é permitido.

URL do gatilho Olá é recuperado, armazenado em cache e usado em tempo de execução. Portanto, se qualquer operação invalida URL Olá armazenado em cache, ação Olá falhará em tempo de execução. toowork como alternativa, salve Olá aplicativo lógico novamente, fazer com que a lógica aplicativo tooretrieve e URL do gatilho de saudação do cache novamente.

## <a name="collection-actions-scopes-and-loops"></a>Ações da coleção (escopos e loops)

Alguns tipos de ação podem conter ações em si. Ações de referência em uma coleção podem ser referenciadas fora de coleção de saudação. Se você definiu `http` em um escopo, `@body('http')` ainda será válido em qualquer lugar em um fluxo de trabalho. As ações dentro de uma coleção podem `runAfter` apenas outras ações em Olá mesma coleção.

## <a name="scope-action"></a>Ação de escopo

Olá `scope` ação permite que você logicamente agrupar ações em um fluxo de trabalho.

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|Ações|Sim|Objeto|Ações interna tooexecute dentro do escopo de saudação|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Ação ForEach

Esta ação de loop itera uma matriz e executa as ações internas de cada item. Por padrão, o loop de foreach Olá é executado em paralelo (20 execuções em paralelo em um momento). Você pode definir regras de execução usando Olá `operationOptions` parâmetro.

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|Ações|Sim|Objeto|Ações interna tooexecute em loop Olá|
|foreach|Sim|string|Olá matriz tooiterate sobre|
|operationOptions|não|string|Quaisquer opções de operação para o comportamento. Atualmente só dá suporte a `sequential` tooexecute iterações sequencialmente (o comportamento padrão é paralelo)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Ação Until

Esta ação de loop executa ações internas até que uma condição tootrue os resultados.

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|Ações|Sim|Objeto|Ações interna tooexecute em loop Olá|
|expressão|Sim|string|Olá expressão tooevaluate após cada iteração|
|limite|sim|Objeto|limites de saudação para loop Olá - pelo menos um limite devem ser definidos|
|count|não|int|Olá limitar toohello o número de iterações que podem ser executadas|
|Tempo limite|não|string|Olá tempo limite de quanto tempo ele deve executar um loop.  Formato ISO 8601|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Condições - Ação If

Olá `If` ação permite que você avalie uma condição e executar uma ramificação com base em se Olá avalia muito`true`.

|Nome|Obrigatório|Tipo|Descrição|  
|--------|------------|--------|---------------|  
|Ações|Sim|Objeto|Ações interna tooexecute quando a expressão é avaliada muito`true`|
|expressão|Sim|string|Olá expressão tooevaluate|
|else|não|Objeto|Ações interna tooexecute quando a expressão é avaliada muito`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Olá tabela a seguir mostra exemplos de como as condições podem usar expressões em uma ação:  
  
|Valor JSON|Result|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Qualquer valor que seria avaliado tootrue faz com que essa condição toopass. Apenas as expressões boolianas têm suporte. tooconvert outros tipos de tooBoolean, use funções `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Há suporte para as funções de comparação. Por exemplo hello aqui, Olá ação será executada somente quando a saída de saudação do act1 é maior que o limite de saudação.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Funções lógicas também são suportado toocreate aninhados expressões Boolianas. Nesse caso, a ação de saudação executa quando a saída de saudação do act1 está acima do limite de saudação ou abaixo de 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Você pode usar a matriz funções toocheck se uma matriz tem todos os itens. Nesse caso, a ação de saudação executa quando Olá erros matriz está vazia.| 
|`"expression": "parameters('hasSpecialAction')"`|Erro - não é uma condição válida porque @ é necessário para as condições.|  
  
Se uma condição for avaliada com êxito, a condição de saudação está marcada como `Succeeded`. Ações em qualquer Olá `actions` ou `else` objetos avaliar muito`Succeeded` quando executada e foi bem-sucedida, `Failed` quando executada e falha, ou `Skipped` quando essa ramificação não será executada.

## <a name="next-steps"></a>Próximas etapas

[API REST do Serviço de Fluxo de Trabalho](https://docs.microsoft.com/rest/api/logic/workflows)
