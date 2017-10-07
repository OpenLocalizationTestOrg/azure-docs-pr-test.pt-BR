---
title: "associações de aplicativos móveis de funções aaaAzure | Microsoft Docs"
description: "Entender como associações de aplicativos do Azure Mobile toouse em funções do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Associações de Aplicativos Móveis do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e código [aplicativos móveis do Azure](../app-service-mobile/app-service-mobile-value-prop.md) associações em funções do Azure. O Azure Functions dá suporte a associações de entrada e saída para os Aplicativos Móveis.

Hello aplicativos móveis de entrada e saída associações permitem [de leitura e gravação tabelas toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) em seu aplicativo móvel.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Associação de entrada dos Aplicativos Móveis
Olá associação de entrada de aplicativos móveis carrega um registro de um ponto de extremidade móvel de tabela e o transmite para sua função. Em c# e F # funções, qualquer registro de toohello as alterações feitas serão enviados automaticamente toohello back tabela quando a função hello encerrada com êxito.

função tooa usa Olá seguinte objeto JSON na saudação de entrada Hello aplicativos móveis `bindings` matriz de function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Observe o seguinte hello:

* `id`pode ser estático, ou ele pode ser baseado em gatilho Olá que invoca a função hello. Por exemplo, se você usar um [gatilho fila]() para sua função, em seguida, `"id": "{queueTrigger}"` usa Olá valor de cadeia de caracteres de mensagem da fila de saudação como Olá tooretrieve de ID de registro.
* `connection`deve conter o nome de saudação de uma configuração de aplicativo em seu aplicativo de função, que por sua vez, contém Olá URL do seu aplicativo móvel. função Hello usa operações REST URL tooconstruct Olá necessárias em relação a seu aplicativo móvel. Você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a URL do seu aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`), em seguida, especifique o nome de saudação de configuração do aplicativo hello no hello `connection` propriedade na associação de entrada. 
* Você precisa toospecify `apiKey` se você [implementar uma chave de API em seu back-end de aplicativo móvel Node. js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implementar uma chave de API em seu back-end de aplicativo móvel .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo isso, você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a chave de API de saudação, em seguida, adicione Olá `apiKey` propriedade em sua associação de entrada com o nome da saudação de configuração do aplicativo hello. 
  
  > [!IMPORTANT]
  > Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel. Ele deve ser apenas clientes distribuídos do lado do tooservice com segurança, como funções do Azure. 
  > 
  > [!NOTE]
  > O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte. Isso protege as informações confidenciais.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entrada
Esta seção mostra como toouse seus aplicativos móveis de entrada em seu código de função de associação. 

Quando registro Olá com hello especificado ID de tabela e o registro for encontrado, ele é passado para Olá denominado [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parâmetro (ou, no Node. js, que é transmitido Olá `context.bindings.<name>` objeto). Quando o registro de saudação não for encontrado, parâmetro hello é `null`. 

Em c# e F # funções, as alterações feitas toohello entrada do registro (parâmetro de entrada) é enviado automaticamente back toohello tabela de aplicativos móveis quando a função hello encerrada com êxito. Em funções do Node. js, use `context.bindings.<name>` tooaccess Olá registro de entrada. Não é possível modificar um registro no Node.js.

<a name="inputsample"></a>

## <a name="input-sample"></a>Amostra de entrada
Suponha que você tenha Olá function.json a seguir, que recupera um registro da tabela de aplicativos móveis com a id de saudação da mensagem de saudação do gatilho de fila:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Consulte Olá específico do idioma exemplo que usa o registro de entrada hello da associação de saudação. exemplos de c# e F # Olá também modificam do registro Olá `text` propriedade.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Exemplo de entrada em C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Amostra de entrada no Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Associação de saída dos Aplicativos Móveis
Use Olá aplicativos móveis saída associação toowrite um ponto de extremidade de tabela de aplicativos móveis tooa registro novo.  

Olá aplicativos móveis de saída para uma função usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Observe o seguinte hello:

* `connection`deve conter o nome de saudação de uma configuração de aplicativo em seu aplicativo de função, que por sua vez, contém Olá URL do seu aplicativo móvel. função Hello usa operações REST URL tooconstruct Olá necessárias em relação a seu aplicativo móvel. Você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a URL do seu aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`), em seguida, especifique o nome de saudação de configuração do aplicativo hello no hello `connection` propriedade na associação de entrada. 
* Você precisa toospecify `apiKey` se você [implementar uma chave de API em seu back-end de aplicativo móvel Node. js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implementar uma chave de API em seu back-end de aplicativo móvel .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo isso, você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a chave de API de saudação, em seguida, adicione Olá `apiKey` propriedade em sua associação de entrada com o nome da saudação de configuração do aplicativo hello. 
  
  > [!IMPORTANT]
  > Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel. Ele deve ser apenas clientes distribuídos do lado do tooservice com segurança, como funções do Azure. 
  > 
  > [!NOTE]
  > O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte. Isso protege as informações confidenciais.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de saída
Esta seção mostra como toouse seus aplicativos móveis de saída de associação no seu código de função. 

Em c# funções, use um parâmetro de saída nomeado do tipo `out object` tooaccess Olá registro de saída. Em funções do Node. js, use `context.bindings.<name>` tooaccess Olá registro de saída.

<a name="outputsample"></a>

## <a name="output-sample"></a>Amostra de saída
Suponha que você tenha Olá function.json a seguir, que define um gatilho de fila e uma saída de aplicativos móveis:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Consulte Olá específico do idioma exemplo que cria um registro no ponto de extremidade de tabela de aplicativos móveis a saudação com conteúdo de saudação de mensagem da fila de saudação.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Amostra de saída em C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Amostra de saída no Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

