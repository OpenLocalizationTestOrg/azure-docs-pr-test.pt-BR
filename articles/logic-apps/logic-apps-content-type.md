---
title: "tipos de conteúdo aaaHandle - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como os aplicativos lógicos do Azure lidam com tipos de conteúdo em tempo de execução e de design"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Gerenciamento de tipos de conteúdo em aplicativos lógicos

JSON, XML, arquivos simples e dados binários são alguns dos diversos tipos de conteúdo que podem fluir em um aplicativo lógico. Enquanto o hello lógica aplicativos mecanismo dá suporte a todos os tipos de conteúdo, algumas nativamente são entendidas pelo Olá lógica de mecanismo de aplicativos. Outros podem exigir transmissões ou conversões conforme necessário. Este artigo descreve como o mecanismo de saudação lida com diferentes tipos de conteúdo e como toocorrectly tratar desses tipos, quando necessário.

## <a name="content-type-header"></a>Cabeçalho Content-Type

toostart basicamente, vejamos Olá dois `Content-Types` que não exigem conversão ou conversão que você pode usar em um aplicativo lógico: `application/json` e `text/plain`.

## <a name="applicationjson"></a>Aplicativo/JSON

mecanismo de fluxo de trabalho Olá depende Olá `Content-Type` cabeçalho de HTTP chama o tratamento do toodetermine Olá apropriado. Qualquer solicitação com o tipo de conteúdo Olá `application/json` são armazenados e manipulados como um objeto JSON. Além disso, o conteúdo JSON pode ser analisado por padrão sem a necessidade de conversão. 

Por exemplo, você poderia analisar uma solicitação que tem o cabeçalho de tipo de conteúdo de saudação `application/json ` em um fluxo de trabalho usando uma expressão como `@body('myAction')['foo'][0]` valor de saudação tooget `bar` nesse caso:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Nenhuma conversão adicional é necessária. Se você estiver trabalhando com dados JSON mas não tinham um cabeçalho especificado, você pode manualmente convertê-lo tooJSON usando Olá `@json()` funcionar, por exemplo: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Esquema e gerador de esquema

Olá gatilho de solicitação permite que você tooenter um esquema JSON para carga Olá esperado tooreceive. Esse esquema permite que o designer Olá gerar tokens para que você poder consumir conteúdo de saudação da solicitação de saudação. Se você não tiver um esquema pronto, selecione **esquema de toogenerate de carga de exemplo de uso**, portanto, você pode gerar um esquema JSON de uma carga de exemplo.

![Esquema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Ação "Parse JSON"

Olá `Parse JSON` ação lhe permite analisar o conteúdo JSON em tokens amigáveis para o consumo lógica de aplicativo. Gatilho de solicitação toohello semelhante, esta ação permite que você insira ou gere um esquema JSON para Olá conteúdo que você deseja tooparse. Essa ferramenta facilita grande parte do consumo de dados do Barramento de Serviço, do Azure Cosmos DB e assim por diante.

![Analisar o JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

Semelhante muito`application/json`, mensagens HTTP recebidas com hello `Content-Type` cabeçalho de `text/plain` são armazenados em formato bruto. Além disso, se essas mensagens são incluídas em ações subsequentes sem conversão, essas solicitações saem com o cabeçalho `Content-Type`: `text/plain`. Por exemplo, ao trabalhar com um arquivo simples, você pode obter esse conteúdo HTTP como `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Se na ação de Avançar hello, enviar solicitação hello como corpo de saudação da outra solicitação (`@body('flatfile')`), solicitação Olá teria um `text/plain` cabeçalho Content-Type. Se você estiver trabalhando com dados que é um texto sem formatação, mas não tinham um cabeçalho especificado, você pode converter manualmente Olá dados tootext usando Olá `@string()` funcionar, por exemplo: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml e Application/octet-stream e funções de conversor

Olá lógica aplicativos mecanismo sempre preserva Olá `Content-Type` que foi recebido no hello HTTP solicitação ou resposta. Portanto, se o mecanismo de saudação recebe o conteúdo com hello `Content-Type` de `application/octet-stream`, e você incluir que conteúdo em uma ação subsequente sem conversão, solicitação de saída de hello tem `Content-Type`: `application/octet-stream`. Dessa forma, mecanismo de saudação pode garantir a dados não sejam perdidos durante a movimentação por meio do fluxo de trabalho de saudação. No entanto, o estado de ação de saudação (entradas e saídas) é armazenado em um objeto JSON como Olá move estado por meio do fluxo de trabalho de saudação. Portanto toopreserve converte alguns tipos de dados, o mecanismo de Olá Olá tooa conteúdo binário codificado na base64 cadeia de caracteres com os metadados apropriados que preserva as `$content` e `$content-type`, que são automaticamente ser convertido. 

* `@json()`-Converte dados muito`application/json`
* `@xml()`-Converte dados muito`application/xml`
* `@binary()`-Converte dados muito`application/octet-stream`
* `@string()`-Converte dados muito`text/plain`
* `@base64()`-Converte a cadeia de caracteres de base64 tooa conteúdo
* `@base64toString()`-Converte uma cadeia de caracteres codificada em base64 muito`text/plain`
* `@base64toBinary()`-Converte uma cadeia de caracteres codificada em base64 muito`application/octet-stream`
* `@encodeDataUri()` - codifica uma cadeia de caracteres como uma matriz de bytes dataUri
* `@decodeDataUri()` - decodifica uma dataUri em uma matriz de bytes

Por exemplo, caso tenha recebido uma solicitação HTTP com `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Você pode converter e usar mais tarde com algo como `@xml(triggerBody())`, ou em uma função como `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Outros tipos de conteúdo

Outros tipos de conteúdo são suportados e trabalhar com aplicativos lógicos, mas pode exigir o corpo da mensagem de saudação recuperar manualmente decodificando Olá `$content`. Por exemplo, suponha que você acionar uma `application/x-www-url-formencoded` solicitação onde `$content` é carga Olá codificado como uma toopreserve de cadeia de caracteres base64 todos os dados:

```
CustomerName=Frank&Address=123+Avenue
```

Porque a solicitação de saudação não for texto sem formatação ou JSON, Olá armazenado na ação de saudação da seguinte maneira:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Atualmente, não existe uma função nativa para dados do formulário, para que você ainda pode usar esses dados em um fluxo de trabalho manualmente acessando dados Olá com uma função, como `@string(body('formdataAction'))`. Se você quisesse Olá solicitação de saída tooalso ter Olá `application/x-www-url-formencoded` cabeçalho de tipo de conteúdo, você pode adicionar o corpo de ação de toohello Olá solicitação sem qualquer conversão como `@body('formdataAction')`. No entanto, esse método funciona somente se o corpo Olá é parâmetro somente Olá Olá `body` entrada. Se você tentar toouse `@body('formdataAction')` em um `application/json` solicitar, você obtém um erro de tempo de execução porque o corpo da saudação codificado é enviado.

