---
title: "esquema de linguagem de definição de aaaWorkflow - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Definir fluxos de trabalho com base no esquema de definição de fluxo de trabalho Olá para os aplicativos lógicos do Azure"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Esquema de linguagem de definição de fluxo de trabalho para Aplicativo Lógico do Azure

Uma definição de fluxo de trabalho contém lógica real de saudação que é executado como parte de seu aplicativo lógico. Esta definição inclui um ou mais disparadores que iniciar o aplicativo de lógica de saudação e uma ou mais ações para Olá lógica aplicativo tootake.  
  
## <a name="basic-workflow-definition-structure"></a>Estrutura da definição de fluxo de trabalho básico

Aqui está a estrutura básica de saudação de uma definição de fluxo de trabalho:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Olá [API de REST de gerenciamento de fluxo de trabalho](https://docs.microsoft.com/rest/api/logic/workflows) documentação contém informações sobre como toocreate e gerenciar fluxos de trabalho de aplicativo lógica.
  
|Nome do elemento|Obrigatório|Descrição|  
|------------------|--------------|-----------------|  
|$schema|Não|Especifica o local de saudação do arquivo de esquema do hello JSON que descreve a versão de saudação da linguagem de definição de saudação. Esse local é necessário quando você faz referência a uma definição externamente. Neste documento, o local de saudação é: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|Não|Especifica a versão de definição de saudação. Quando você implanta um fluxo de trabalho usando a definição de saudação, você pode usar este toomake de valor se a definição de saudação à direita é usada.|  
|parâmetros|Não|Especifica parâmetros usados tooinput dados na definição de saudação. Podem ser definidos no máximo 50 parâmetros.|  
|gatilhos|Não|Especifica informações sobre gatilhos de saudação que iniciar o fluxo de trabalho de saudação. Podem ser definidos no máximo 10 gatilhos.|  
|Ações|Não|Especifica as ações executadas durante a execução do fluxo de saudação. Podem ser definidas no máximo 250 ações.|  
|outputs|Não|Especifica informações sobre o recurso de saudação implantado. Podem ser definidas no máximo 10 saídas.|  
  
## <a name="parameters"></a>parâmetros

Esta seção especifica todos os parâmetros de saudação que são usados na definição de fluxo de trabalho Olá no momento da implantação. Todos os parâmetros devem ser declarados nesta seção antes de eles podem ser usados em outras seções da definição de saudação.  
  
Olá exemplo a seguir mostra a estrutura de saudação de uma definição de parâmetro:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Nome do elemento|Obrigatório|Descrição|  
|------------------|--------------|-----------------|  
|type|Sim|**Tipo**: string <p> **Declaração**: `"parameters": {"parameter1": {"type": "string"}` <p> **Especificação**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: securestring <p> **Declaração**: `"parameters": {"parameter1": {"type": "securestring"}}` <p> **Especificação**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: int <p> **Declaração**: `"parameters": {"parameter1": {"type": "int"}}` <p> **Especificação**: `"parameters": {"parameter1": {"value" : 5}}` <p> **Tipo**: bool <p> **Declaração**: `"parameters": {"parameter1": {"type": "bool"}}` <p> **Especificação**: `"parameters": {"parameter1": { "value": true }}` <p> **Tipo**: array <p> **Declaração**: `"parameters": {"parameter1": {"type": "array"}}` <p> **Especificação**: `"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Tipo**: object <p> **Declaração**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Especificação**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Tipo**: secureobject <p> **Declaração**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Especificação**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Observação:** Olá `securestring` e `secureobject` tipos não são retornados em `GET` operações. Todas as senhas, chaves e segredos devem usar esse tipo.|  
|defaultValue|Não|Especifica o valor de padrão de saudação para o parâmetro hello quando nenhum valor é especificado no momento de Olá Olá recurso for criado.|  
|allowedValues|Não|Especifica uma matriz de valores permitidos para o parâmetro hello.|  
|metadata|Não|Especifica informações adicionais sobre o parâmetro hello, como uma descrição legível ou dados de tempo de design usados pelo Visual Studio ou outras ferramentas.|  
  
Este exemplo mostra como você pode usar um parâmetro na seção de corpo de saudação de uma ação:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Os parâmetros também podem ser usados em saídas.  
  
## <a name="triggers-and-actions"></a>Gatilhos e ações  

Gatilhos e ações especificam chamadas Olá que podem participar na execução de fluxo de trabalho. Para obter detalhes sobre esta seção, consulte [Gatilhos e ações do fluxo de trabalho](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>outputs  

As saídas especificam informações que podem ser retornadas de uma execução de fluxo de trabalho. Por exemplo, se você tiver um status específico ou um valor que você deseja tootrack para cada execução, você pode incluir dados em Olá executar saídas. dados de saudação aparecem na hello API REST de gerenciamento para que executam e em gerenciamento de saudação da interface do usuário para que executam em Olá portal do Azure. Você também pode fluir desses sistemas externos de tooother saídas como o Power BI para a criação de painéis. Saídas são *não* usado toorespond tooincoming solicitações em Olá API REST do serviço. toorespond tooan solicitação de entrada usando Olá `response` tipo de ação, aqui está um exemplo:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Nome do elemento|Obrigatório|Descrição|  
|------------------|--------------|-----------------|  
|key1|Sim|Especifica o identificador de chave Olá para saída de hello. Substituir **key1** com um nome que deseja que a saída de hello tooidentify toouse.|  
|valor|Sim|Especifica o valor de saudação da saída de hello.|  
|type|Sim|Especifica o tipo de saudação para valor de saudação que foi especificado. Os tipos de valores possíveis são: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Expressões  

Valores JSON na definição de saudação podem ser literal ou podem ser expressões que são avaliadas quando Olá definição é usada. Por exemplo:  
  
```json
"name": "value"
```

 ou o  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Algumas expressões obtêm seus valores de ações de tempo de execução que talvez não exista no início de saudação da execução de saudação. Você pode usar **funções** toohelp recuperar alguns desses valores.  
  
As expressões podem aparecer em qualquer lugar em um valor de cadeia de caracteres JSON e sempre retornam outro valor JSON. Quando um valor JSON for determinado toobe uma expressão, corpo Olá da expressão de saudação é extraído, removendo Olá arroba (@). Se for necessária uma cadeia de caracteres literal que comece com @, essa cadeia de caracteres deve ser substituída usando @@. Olá exemplos a seguir mostram como as expressões são avaliadas.  
  
|Valor JSON|Result|  
|----------------|------------|  
|"parameters"|Olá caracteres 'parameters' são retornados.|  
|"parameters[1]"|Olá caracteres "parameters [1]" são retornados.|  
|"@@"|Uma cadeia de caracteres de 1 caractere que contém '@' será retornada.|  
|" @"|Uma cadeia de caracteres de 2 caracteres que contém ' @' será retornada.|  
  
Com *interpolação de cadeia de caracteres*, as expressões também podem aparecer dentro de cadeias de caracteres onde as expressões são encapsuladas em `@{ ... }`. Por exemplo: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

resultado de saudação sempre é uma cadeia de caracteres, o que torna essa toohello semelhante de recurso `concat` função. Suponha que você definiu `myNumber` como `42` e `myString` como `sampleString`:  
  
|Valor JSON|Result|  
|----------------|------------|  
|"@parameters('myString')"|Retorna `sampleString` como uma cadeia de caracteres.|  
|"@{parameters('myString')}"|Retorna `sampleString` como uma cadeia de caracteres.|  
|"@parameters('myNumber')"|Retorna `42` como um *número*.|  
|"@{parameters('myNumber')}"|Retorna `42` como uma *cadeia de caracteres*.|  
|"A resposta é: @{parameters('myNumber')}"|Olá retorna a cadeia de caracteres `Answer is: 42`.|  
|"@concat('A resposta é: ', string(parameters('myNumber')))"|Olá retorna a cadeia de caracteres`Answer is: 42`|  
|"A resposta é: @@{parameters('myNumber')}"|Olá retorna a cadeia de caracteres `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operadores  

Os operadores são caracteres de saudação que pode ser usado dentro de expressões ou funções. 
  
|operador|Descrição|  
|--------------|-----------------|  
|.|operador de ponto de saudação permite tooreference propriedades de um objeto|  
|?|operador de ponto de interrogação Olá lhe permite fazer referência a propriedades nulo de um objeto sem um erro de tempo de execução. Por exemplo, você pode usar este null de toohandle expressão disparar saídas: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|Olá aspas é literais de cadeia de caracteres para Olá somente modo toowrap. Você não pode usar aspas duplas dentro de expressões porque essa pontuação está em conflito com aspas JSON Olá que encapsula a expressão de inteiro de saudação.|  
|[]|Olá colchetes pode ser usado tooget um valor de uma matriz com um índice específico. Por exemplo, se você tem uma ação que passa `range(0,10)`na toohello `forEach` função, você pode usar a função tooget itens fora de matrizes:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Funções  

Você também pode chamar funções dentro de expressões. Olá tabela a seguir mostra as funções de saudação que podem ser usadas em uma expressão.  
  
|Expression|Avaliação|  
|----------------|----------------|  
|"@function('Hello')"|Chamadas Olá membro da função da definição de saudação com a cadeia de caracteres hello literal Hello como primeiro parâmetro de saudação.|  
|"@function('É incrível!')"|Chama o membro da função de saudação da definição de saudação com a cadeia de caracteres literal hello "It's Cool!' como o primeiro parâmetro de saudação|  
|"@function().prop1"|Retorna o valor da propriedade prop1 Olá Olá de Olá `myfunction` membro de definição de saudação.|  
|"@function('Hello').prop1"|Chamadas Olá membro da função da definição de saudação com a cadeia de caracteres hello literal "Hello" como Olá primeiro parâmetro e retorna Olá propriedade prop1 do objeto hello.|  
|"@function(parameters('Hello'))"|Avalia o parâmetro de saudação hello e passa Olá valor toofunction|  
  
### <a name="referencing-functions"></a>Referenciando funções  

Você pode usar essas saídas de tooreference funções de outras ações no aplicativo de lógica de saudação ou valores passados durante a saudação lógica aplicativo foi criado. Por exemplo, você pode referenciar dados saudação de uma etapa toouse-lo em outro.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|parâmetros|Retorna um valor de parâmetro que é definido na definição de saudação. <p>`parameters('password')` <p> **Número do parâmetro**: 1 <p> **Nome**: Parâmetro <p> **Descrição**: Obrigatório. nome de saudação do parâmetro hello cujos valores você deseja.|  
|ação|Permite que uma expressão tooderive seu valor de outro nome JSON e pares de valor ou saída de saudação de ação de tempo de execução atual de saudação. propriedade Olá representada por propertyPath no exemplo a seguir de saudação é opcional. Se propertyPath não for especificado, a referência de Olá é objeto de ação todo toohello. Essa função só pode ser usada sob as condições “do-until” de uma ação. <p>`action().outputs.body.propertyPath`|  
|Ações|Permite que uma expressão tooderive seu valor de outro nome JSON e pares de valor ou saída de saudação da ação de tempo de execução de saudação. Essas expressões declaram explicitamente que uma ação depende de outra ação. propriedade Olá representada por propertyPath no exemplo a seguir de saudação é opcional. Se propertyPath não for especificado, a referência de Olá é objeto de ação todo toohello. Você pode usar qualquer esse elemento ou Olá condições dependências do elemento toospecify, mas não é necessário toouse ambos para Olá mesmo recurso dependente. <p>`actions('myAction').outputs.body.propertyPath` <p> **Número do parâmetro**: 1 <p> **Nome**: Nome da ação <p> **Descrição**: Obrigatório. nome de saudação da ação de saudação cujos valores você deseja. <p> As propriedades disponíveis no objeto de ação de saudação são: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Consulte Olá [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850646) para obter detalhes sobre essas propriedades.|
|gatilho|Permite que uma expressão tooderive seu valor de outro nome JSON e pares de valor ou saída de saudação do gatilho de tempo de execução de saudação. propriedade Olá representada por propertyPath no exemplo a seguir de saudação é opcional. Se propertyPath não for especificado, a referência de saudação é toohello objeto de gatilho inteiro. <p>`trigger().outputs.body.propertyPath` <p>Quando usado dentro de entradas do gatilho, função hello retorna saídas de saudação da execução anterior hello. No entanto, quando usada dentro de condição do disparador, Olá `trigger` função retorna as saídas de saudação da execução atual de saudação. <p> As propriedades disponíveis no objeto de gatilho Olá são: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Consulte Olá [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850644) para obter detalhes sobre essas propriedades.|
|actionOutputs|Essa é uma função abreviada para `actions('actionName').outputs` <p> **Número do parâmetro**: 1 <p> **Nome**: Nome da ação <p> **Descrição**: Obrigatório. nome de saudação da ação de saudação cujos valores você deseja.|  
|actionBody e body|Essas são funções abreviadas para `actions('actionName').outputs.body` <p> **Número do parâmetro**: 1 <p> **Nome**: Nome da ação <p> **Descrição**: Obrigatório. nome de saudação da ação de saudação cujos valores você deseja.|  
|triggerOutputs|Essa é uma função abreviada para `trigger().outputs`|  
|triggerBody|Essa é uma função abreviada para `trigger().outputs.body`|  
|item|Quando usado dentro de uma ação de repetição, essa função retorna o item Olá na matriz de saudação para essa iteração de ação de saudação. Por exemplo, se você tiver uma ação que é executada para cada item de uma matriz de mensagens, você pode usar esta sintaxe: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Funções de coleção  

Essas funções operam em coleções e aplicam geralmente tooArrays, cadeias de caracteres e, às vezes, os dicionários.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|contains|Retorna true se o dicionário contém uma chave, se a lista contém um valor ou a cadeia de caracteres contém uma subcadeia de caracteres. Por exemplo, essa função retornará `true`: <p>`contains('abacaba','aca')` <p> **Número do parâmetro**: 1 <p> **Nome**: Dentro da coleção <p> **Descrição**: Obrigatório. Olá toosearch de coleção dentro. <p> **Número do parâmetro**: 2 <p> **Nome**: Encontrar objeto <p> **Descrição**: Obrigatório. Olá toofind de objeto dentro de saudação **na coleção**.|  
|length|Retorna Olá número de elementos em uma matriz ou uma cadeia de caracteres. Por exemplo, essa função retornará `3`:  <p>`length('abc')` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. coleção de Olá para o comprimento de saudação tooget.|  
|empty|Retornará true se o objeto, matriz ou cadeia de caracteres estiverem vazios. Por exemplo, essa função retornará `true`: <p>`empty('')` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. Olá coleção toocheck se ela estiver vazia.|  
|interseção|Retorna uma única matriz ou objeto que tem elementos comuns entre matrizes ou objetos passados. Por exemplo, essa função retornará `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>parâmetros de saudação para função hello podem ser um conjunto de objetos ou um conjunto de matrizes (não uma mistura de ambos). Se houver dois objetos com hello mesmo nome, último objeto Olá com esse nome é exibido no objeto final hello. <p> **Número do parâmetro**: 1 ... *n* <p> **Nome**: Coleção *n* <p> **Descrição**: Obrigatório. Olá tooevaluate de coleções. Um objeto deve estar no passado tooappear no resultado de saudação de todas as coleções.|  
|union|Retorna uma matriz ou objeto com todos os elementos de saudação que estão em uma matriz ou objeto passado toothis função. Por exemplo, essa função retornará `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>parâmetros de saudação para função hello podem ser um conjunto de objetos ou um conjunto de matrizes (não uma combinação delas). Se houver dois objetos com o mesmo nome de saudação na saída final Olá, último objeto Olá com esse nome é exibido no objeto final hello. <p> **Número do parâmetro**: 1 ... *n* <p> **Nome**: Coleção *n* <p> **Descrição**: Obrigatório. Olá tooevaluate de coleções. Um objeto que aparece em qualquer uma das coleções de saudação também aparece no resultado de saudação.|  
|first|Retorna Olá primeiro elemento na matriz de saudação ou cadeia de caracteres transmitida. Por exemplo, essa função retornará `0`: <p>`first([0,2,3])` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. Olá tootake Olá primeiro objeto da coleção de.|  
|last|Retorna Olá último elemento na matriz de saudação ou cadeia de caracteres transmitida. Por exemplo, essa função retornará `3`: <p>`last('0123')` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. Olá tootake Olá último objeto de coleção do.|  
|take|Retorna primeiro Olá **contagem** elementos de matriz de saudação ou cadeia de caracteres passada. Por exemplo, essa função retornará `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. coleção de saudação do onde tootake Olá primeiro **contagem** objetos. <p> **Número do parâmetro**: 2 <p> **Nome**: Contagem <p> **Descrição**: Obrigatório. Olá o número de objetos tootake de saudação **coleção**. Deve ser um número inteiro positivo.|  
|skip|Retorna Olá elementos na matriz de saudação começando no índice **contagem**. Por exemplo, essa função retornará `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção <p> **Descrição**: Obrigatório. Olá Olá de tooskip coleção primeiro **contagem** objetos. <p> **Número do parâmetro**: 2 <p> **Nome**: Contagem <p> **Descrição**: Obrigatório. Olá o número de objetos tooremove na frente de saudação do **coleção**. Deve ser um número inteiro positivo.|  
|join|Retorna uma cadeia de caracteres com cada item de uma matriz unida por um delimitador, por exemplo, isso retorna `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Coleção<br /><br /> **Descrição**: Obrigatório. itens de toojoin de coleta de saudação do.<br /><br /> **Número do parâmetro**: 2<br /><br /> **Nome**: Delimitador<br /><br /> **Descrição**: Obrigatório. itens de toodelimit de cadeia de caracteres de saudação com.|  
  
### <a name="string-functions"></a>Funções de cadeia de caracteres

Olá, somente as funções a seguir se aplicam a toostrings. Você também pode usar algumas funções de coleção em cadeias de caracteres.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|concat|Combina qualquer número de cadeias de caracteres. Por exemplo, se o parâmetro 1 é `p1`, essa função retorna `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Número do parâmetro**: 1 ... *n* <p> **Nome**: cadeia de caracteres *n* <p> **Descrição**: Obrigatório. Olá toocombine de cadeias de caracteres em uma única cadeia de caracteres.|  
|substring|Retorna um subconjunto de caracteres de uma cadeia de caracteres. Por exemplo, essa função retornará `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres de saudação do qual Olá subcadeia de caracteres é feita. <p> **Número do parâmetro**: 2 <p> **Nome**: Índice inicial <p> **Descrição**: Obrigatório. índice de saudação do onde a subcadeia de caracteres hello começa no parâmetro 1. <p> **Número do parâmetro**: 3 <p> **Nome**: Comprimento <p> **Descrição**: Obrigatório. comprimento de saudação da subcadeia de caracteres de saudação.|  
|substitui|Substitui uma cadeia de caracteres por uma determinada sequência de caracteres. Por exemplo, essa função retornará `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Número do parâmetro**: 1 <p> **Nome**: cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que é pesquisada para o parâmetro 2 e atualizada com o parâmetro 3, quando o parâmetro 2 é encontrado no parâmetro 1. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres antiga <p> **Descrição**: Obrigatório. Olá tooreplace de cadeia de caracteres com o parâmetro 3, quando uma correspondência for encontrada no parâmetro 1 <p> **Número do parâmetro**: 3 <p> **Nome**: Cadeia de caracteres nova <p> **Descrição**: Obrigatório. saudação de cadeia de caracteres que é usada tooreplace Olá cadeia de caracteres no parâmetro 2 quando uma correspondência for encontrada no parâmetro 1.|  
|GUID|Essa função gera uma cadeia de caracteres de identificador global exclusiva (GUID). Por exemplo, essa função pode gerar esse GUID:`c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Número do parâmetro**: 1 <p> **Nome**: Formato <p> **Descrição**: Opcional. Um especificador de formato único que indica [como tooformat Olá valor esse Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). o parâmetro de formato Olá pode ser "N", "D", "B", "P" ou "X". Se o formato não for fornecido, "D" é usado.|  
|toLower|Converte uma cadeia de caracteres toolowercase. Por exemplo, essa função retornará `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. maiusculas e minúsculas toolower saudação do tooconvert cadeia de caracteres. Se um caractere na cadeia de caracteres de saudação não tem um equivalente em letras minúsculas, caracteres hello está incluído inalterada no hello retornada uma cadeia.|  
|toUpper|Converte uma cadeia de caracteres toouppercase. Por exemplo, essa função retornará `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. maiusculas e minúsculas tooupper saudação do tooconvert cadeia de caracteres. Se um caractere na cadeia de caracteres de saudação não tem um equivalente em letras maiusculas, caracteres hello está incluído inalterada no hello retornada uma cadeia.|  
|indexof|Localize o índice de saudação de um valor dentro de um caso de cadeia de caracteres e minúscula. Por exemplo, essa função retornará `7`: <p>`indexof('hello, world.', 'world')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que pode conter o valor de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. índice de Olá Olá valor toosearch do.|  
|lastindexof|Encontre o último índice de um valor dentro de um caso de cadeia de caracteres de saudação e minúscula. Por exemplo, essa função retornará `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que pode conter o valor de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. índice de Olá Olá valor toosearch do.|  
|startswith|Verifica se Olá cadeia será iniciada com um caso de valor e minúscula. Por exemplo, essa função retornará `true`: <p>`startswith('hello, world', 'hello')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que pode conter o valor de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres Hello valor Olá pode começar com.|  
|endswith|Verifica se Olá cadeia de caracteres termina com um caso de valor e minúscula. Por exemplo, essa função retornará `true`: <p>`endswith('hello, world', 'world')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que pode conter o valor de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres Hello valor Olá pode terminar com.|  
|split|Divide a cadeia de caracteres de saudação usando um separador. Por exemplo, essa função retornará `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá cadeia de caracteres que será dividida. <p> **Número do parâmetro**: 2 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. separador de saudação.|  
  
### <a name="logical-functions"></a>Funções lógicas  

Essas funções são úteis em condições e podem ser qualquer tipo de lógica de tooevaluate usado.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|equals|Retorna true se dois valores são iguais. Por exemplo, se parameter1 é someValue, essa função retorna `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Número do parâmetro**: 1 <p> **Nome**: Objeto 1 <p> **Descrição**: Obrigatório. Olá objeto toocompare muito**2 do objeto**. <p> **Número do parâmetro**: 2 <p> **Nome**: Objeto 2 <p> **Descrição**: Obrigatório. Olá objeto toocompare muito**1 objeto**.|  
|less|Retorna VERDADEIRO se Olá primeiro argumento for menor do que Olá segundo. Observe que os valores só podem ser do tipo inteiro, float ou cadeia de caracteres. Por exemplo, essa função retornará `true`: <p>`less(10,100)` <p> **Número do parâmetro**: 1 <p> **Nome**: Objeto 1 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for menor que **2 do objeto**. <p> **Número do parâmetro**: 2 <p> **Nome**: Objeto 2 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for maior que **1 objeto**.|  
|lessOrEquals|Retorna VERDADEIRO se Olá primeiro argumento for menor que ou igual a toohello segundo. Observe que os valores só podem ser do tipo inteiro, float ou cadeia de caracteres. Por exemplo, essa função retornará `true`: <p>`lessOrEquals(10,10)` <p> **Número do parâmetro**: 1 <p> **Nome**: Objeto 1 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for menor ou igual a muito**2 do objeto**. <p> **Número do parâmetro**: 2 <p> **Nome**: Objeto 2 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for maior que ou igual a muito**1 objeto**.|  
|greater|Retorna VERDADEIRO se Olá primeiro argumento for maior que Olá segundo. Observe que os valores só podem ser do tipo inteiro, float ou cadeia de caracteres. Por exemplo, essa função retornará `false`:  <p>`greater(10,10)` <p> **Número do parâmetro**: 1 <p> **Nome**: Objeto 1 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for maior que **2 do objeto**. <p> **Número do parâmetro**: 2 <p> **Nome**: Objeto 2 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for menor que **1 objeto**.|  
|greaterOrEquals|Retorna VERDADEIRO se Olá primeiro argumento for maior que ou igual toohello segundo. Observe que os valores só podem ser do tipo inteiro, float ou cadeia de caracteres. Por exemplo, essa função retornará `false`: <p>`greaterOrEquals(10,100)` <p> **Número do parâmetro**: 1 <p> **Nome**: Objeto 1 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for maior que ou igual a muito**2 do objeto**. <p> **Número do parâmetro**: 2 <p> **Nome**: Objeto 2 <p> **Descrição**: Obrigatório. Olá toocheck de objeto se ele for menor ou igual muito**1 objeto**.|  
|e|Retorna true se ambos os parâmetros forem verdadeiros. Ambos os argumentos precisam toobe booleanos. Por exemplo, essa função retornará `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Número do parâmetro**: 1 <p> **Nome**: Booliano 1 <p> **Descrição**: Obrigatório. Olá primeiro argumento deve ser `true`. <p> **Número do parâmetro**: 2 <p> **Nome**: Booliano 2 <p> **Descrição**: Obrigatório. Olá segundo argumento deve ser `true`.|  
|ou o|Retorna true se o parâmetro for verdadeiro. Ambos os argumentos precisam toobe booleanos. Por exemplo, essa função retornará `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Número do parâmetro**: 1 <p> **Nome**: Booliano 1 <p> **Descrição**: Obrigatório. Olá primeiro argumento pode ser `true`. <p> **Número do parâmetro**: 2 <p> **Nome**: Booliano 2 <p> **Descrição**: Obrigatório. Olá segundo argumento pode ser `true`.|  
|não|Retorna VERDADEIRO se Olá parâmetros são `false`. Ambos os argumentos precisam toobe booleanos. Por exemplo, essa função retornará `true`: <p>`not(contains('200 Success','Fail'))` <p> **Número do parâmetro**: 1 <p> **Nome**: Booliano <p> **Descrição**: retornará true se o hello parâmetros são `false`. Ambos os argumentos precisam toobe booleanos. Adicione esta função a `true`:  `not(contains('200 Success','Fail'))`|  
|if|Retorna um valor especificado, com base em se a expressão Olá resultou em `true` ou `false`.  Por exemplo, essa função retornará `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Número do parâmetro**: 1 <p> **Nome**: Expressão <p> **Descrição**: Obrigatório. Deve retornar um valor booliano que determina quais expressão de saudação do valor. <p> **Número do parâmetro**: 2 <p> **Nome**: Verdadeiro <p> **Descrição**: Obrigatório. Olá tooreturn valor se a expressão de saudação é `true`. <p> **Número do parâmetro**: 3 <p> **Nome**: Falso <p> **Descrição**: Obrigatório. Olá tooreturn valor se a expressão de saudação é `false`.|  
  
### <a name="conversion-functions"></a>Funções de conversão  

Essas funções são tooconvert usado entre cada um dos tipos nativos de saudação no idioma hello:  
  
- string  
  
- inteiro  
  
- flutuante  
  
- Booliano  
  
- matrizes  
  
- dicionários  

-   formulários  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|int|Converta inteiro de tooan parâmetro hello. Por exemplo, essa função retorna 100 como um número, em vez de uma cadeia de caracteres: <p>`int('100')` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. Olá valor inteiro convertido tooan.|  
|string|Converta a cadeia de caracteres hello parâmetro tooa. Por exemplo, essa função retornará `'10'`: <p>`string(10)` <p>Você também pode converter uma cadeia de caracteres do objeto tooa. Por exemplo, se hello `myPar` parâmetro é um objeto com uma propriedade `abc : xyz`, essa função retornará `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. Olá valor que é a cadeia de caracteres tooa convertido.|  
|json|Converter o valor de tipo JSON do hello parâmetro tooa e é hello oposto de `string()`. Por exemplo, essa função retorna `[1,2,3]` como uma matriz, em vez de uma cadeia de caracteres: <p>`json('[1,2,3]')` <p>Da mesma forma, você pode converter um objeto de tooan de cadeia de caracteres. Por exemplo, essa função retornará `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. saudação de cadeia de caracteres que é convertido tooa valor de tipo nativo. <p>Olá `json()` função oferece suporte a XML de entrada muito. Olá, por exemplo, o valor de parâmetro: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>é convertido toothis JSON: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|flutuante|Converta o número de ponto flutuante do hello parâmetro argumento tooa. Por exemplo, essa função retornará `10.333`: <p>`float('10.333')` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. Olá valor que é o número de ponto flutuante tooa convertido.|  
|bool|Converta Olá parâmetro tooa booliano. Por exemplo, essa função retornará `false`: <p>`bool(0)` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. Olá valor convertido tooa booliano.|  
|coalesce|Retorna Olá primeiro nulos objeto argumentos Olá passados. **Observação**: Uma cadeia de caracteres vazia não é nula. Por exemplo, se os parâmetros 1 e 2 não forem definidos, essa função retornará `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Número do parâmetro**: 1 ... *n* <p> **Nome**: Objeto*n* <p> **Descrição**: Obrigatório. Olá toocheck de objetos para null.|  
|base64|Retorna Olá representação de cadeia de caracteres de entrada hello base 64. Por exemplo, essa função retornará `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres 1 <p> **Descrição**: Obrigatório. Olá tooencode de cadeia de caracteres em representação em base64.|  
|base64ToBinary|Retorna uma representação binária de uma cadeia de caracteres codificada em base64. Por exemplo, essa função retorna a representação binária de saudação do `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres codificada de base64 Hello.|  
|base64ToString|Retorna uma representação de cadeia de caracteres de uma cadeia de caracteres codificada em base64. Por exemplo, essa função retornará `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres codificada de base64 Hello.|  
|Binário|Retorna uma representação binária de um valor.  Por exemplo, esta função retorna uma representação binária de `some string`: <p>`binary('some string')` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. Olá valor toobinary convertido.|  
|dataUriToBinary|Retorna uma representação binária de um URI de dados. Por exemplo, essa função retorna a representação binária de saudação do `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. dados de saudação representação do URI tooconvert toobinary.|  
|dataUriToString|Retorna uma representação de cadeia de caracteres de um URI de dados. Por exemplo, essa função retornará `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres<p> **Descrição**: Obrigatório. dados de saudação representação do URI tooconvert tooString.|  
|dataUri|Retorna um URI de dados de um valor. Por exemplo, essa função retornará o seguinte URI de dados `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Número do parâmetro**: 1<p> **Nome**: Valor<p> **Descrição**: Obrigatório. Olá valor tooconvert toodata URI.|  
|decodeBase64|Retorna uma representação de cadeia de caracteres de uma cadeia de caracteres com entrada baseada em base64. Por exemplo, essa função retornará `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Retorna uma representação de cadeia de caracteres de uma cadeia de caracteres com entrada baseada em base64.|  
|encodeUriComponent|Escapes de URL Olá cadeia de caracteres que é transmitida. Por exemplo, essa função retornará `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá tooescape URL unsafe caracteres do.|  
|decodeUriComponent|Escapes de URL Cancelar Olá cadeia de caracteres que é transmitida. Por exemplo, essa função retornará `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá toodecode Olá URL unsafe caracteres do.|  
|decodeDataUri|Retorna uma representação binária de uma cadeia de caracteres de URI de dados de entrada. Por exemplo, essa função retorna a representação binária de saudação do `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. Olá dataURI toodecode em uma representação binária.|  
|uriComponent|Retorna uma representação codificada de URI de um valor. Por exemplo, essa função retornará `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Número do parâmetro**: 1<p> **Nome**: Cadeia de caracteres <p> **Descrição**: Obrigatório. cadeia de caracteres de saudação toobe URI codificado.|  
|uriComponentToBinary|Retorna uma representação binária de uma cadeia de caracteres codificada em URI. Por exemplo, esta função retorna uma representação binária de `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Número do parâmetro**: 1 <p> **Nome**: Cadeia de caracteres<p> **Descrição**: Obrigatório. Olá URI de cadeia de caracteres codificada.|  
|uriComponentToString|Retorna uma representação de cadeia de caracteres de uma cadeia de caracteres codificada em URI. Por exemplo, essa função retornará `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Número do parâmetro**: 1<p> **Nome**: Cadeia de caracteres<p> **Descrição**: Obrigatório. Olá URI de cadeia de caracteres codificada.|  
|xml|Retorna uma representação XML de valor de saudação. Por exemplo, essa função retorna o conteúdo XML representado por `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Olá `xml()` função aceita um objeto JSON de entrada muito. Por exemplo, Olá parâmetro `{ "abc": "xyz" }` é convertido tooXML conteúdo:`\<abc>xyz\</abc>` <p> **Número do parâmetro**: 1<p> **Nome**: Valor<p> **Descrição**: Obrigatório. Olá valor tooconvert tooXML.|  
|xpath|Retorna uma matriz de nós XML correspondência da expressão xpath Olá Olá xpath expressão é avaliada como um valor. <p> **Exemplo 1** <p>Suponha que o valor de saudação do parâmetro `p1` é uma representação de cadeia de caracteres desse XML: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Esse código: `xpath(xml(parameters('p1'), '/lab/robot/name')` <p>retorna <p>`[ <name>R1</name>, <name>R2</name> ]` <p>enquanto esse código: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>retorna <p>`13` <p> <p> **Exemplo 2** <p>Olá determinado conteúdo XML a seguir: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Esse código: `@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>ou esse código: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>retorna <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>E esse código: `@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>retorna <p>``xyz`` <p> **Número do parâmetro**: 1 <p> **Nome**: Xml <p> **Descrição**: Obrigatório. Olá XML no qual tooevaluate Olá XPath expressão. <p> **Número do parâmetro**: 2 <p> **Nome**: XPath <p> **Descrição**: Obrigatório. Olá tooevaluate de expressão XPath.|  
|array|Converta a matriz de tooan parâmetro hello. Por exemplo, essa função retornará `["abc"]`: <p>`array('abc')` <p> **Número do parâmetro**: 1 <p> **Nome**: Valor <p> **Descrição**: Obrigatório. valor de saudação que é convertido tooan matriz.|
|createArray|Cria uma matriz de parâmetros de saudação. Por exemplo, essa função retornará `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Número do parâmetro**: 1 ... *n* <p> **Nome**: Qualquer *n* <p> **Descrição**: Obrigatório. Olá toocombine de valores em uma matriz.|
|triggerFormDataValue|Retorna um único valor correspondente Olá nome de chave de dados de formulário ou a saída de gatilho codificados por formulário.  Se houver várias correspondências ocorrerá um erro.  Por exemplo, a seguinte Olá retornará `bar`:`triggerFormDataValue('foo')`<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Nome da chave<br /><br />**Descrição**: Obrigatório. nome da chave Olá de saudação tooreturn de valor de dados de formulário.|
|triggerFormDataMultiValues|Retorna uma matriz de valores correspondentes ao nome de chave Olá dados de formulário ou a saída de gatilho codificados por formulário.  Por exemplo, a seguinte Olá retornará `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Nome da chave<br /><br />**Descrição**: Obrigatório. nome da chave Olá Olá de dados do formulário valores tooreturn.|
|triggerMultipartBody|Retorna Olá corpo de uma parte em uma saída de várias partes de gatilho hello.<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Índice<br /><br />**Descrição**: Obrigatório. índice de saudação do hello parte tooretrieve.|
|formDataValue|Retorna um único valor correspondente Olá nome de chave de dados de formulário ou saída codificados por formulário de ação.  Se houver várias correspondências ocorrerá um erro.  Por exemplo, a seguinte Olá retornará `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Nome da ação<br /><br />**Descrição**: Obrigatório. nome de saudação da ação de saudação com dados de formulário ou resposta codificados por formulário.<br /><br />**Número do parâmetro**: 2<br /><br />**Nome**: Nome da chave<br /><br />**Descrição**: Obrigatório. nome da chave Olá de saudação tooreturn de valor de dados de formulário.|
|formDataMultiValues|Retorna uma matriz de valores correspondentes ao nome de chave de saudação de dados de formulário ou saída codificados por formulário de ação.  Por exemplo, a seguinte Olá retornará `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Nome da ação<br /><br />**Descrição**: Obrigatório. nome de saudação da ação de saudação com dados de formulário ou resposta codificados por formulário.<br /><br />**Número do parâmetro**: 2<br /><br />**Nome**: Nome da chave<br /><br />**Descrição**: Obrigatório. nome da chave Olá Olá de dados do formulário valores tooreturn.|
|multipartBody|Retorna Olá corpo de uma parte de uma saída de várias partes de uma ação.<br /><br />**Número do parâmetro**: 1<br /><br />**Nome**: Nome da ação<br /><br />**Descrição**: Obrigatório. nome de saudação da ação de saudação com uma resposta com diversas partes.<br /><br />**Número do parâmetro**: 2<br /><br />**Nome**: Índice<br /><br />**Descrição**: Obrigatório. índice de saudação do hello parte tooretrieve.|

### <a name="math-functions"></a>Funções matemáticas  

Essas funções podem ser usadas para qualquer um dos tipos de números: **inteiros** e **floats**.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|adicionar|Retorna o resultado de saudação de adicionar Olá dois números. Por exemplo, essa função retornará `20.333`: <p>`add(10,10.333)` <p> **Número do parâmetro**: 1 <p> **Nome**: Soma 1 <p> **Descrição**: Obrigatório. Olá número tooadd muito**soma 2**. <p> **Número do parâmetro**: 2 <p> **Nome**: Soma 2 <p> **Descrição**: Obrigatório. Olá número tooadd muito**soma 1**.|  
|sub|Retorna o resultado de saudação da subtração de dois números. Por exemplo, essa função retornará `-0.333`: <p>`sub(10,10.333)` <p> **Número do parâmetro**: 1 <p> **Nome**: Minuendo <p> **Descrição**: Obrigatório. saudação de número que **Subtraendo** é removido. <p> **Número do parâmetro**: 2 <p> **Nome**: Subtraendo <p> **Descrição**: Obrigatório. Olá tooremove número de saudação **Minuendo**.|  
|mul|Retorna o resultado de saudação de multiplicar dois números de saudação. Por exemplo, essa função retornará `103.33`: <p>`mul(10,10.333)` <p> **Número do parâmetro**: 1 <p> **Nome**: Multiplicando 1 <p> **Descrição**: Obrigatório. Olá número toomultiply **multiplicando 2** com. <p> **Número do parâmetro**: 2 <p> **Nome**: Multiplicando 2 <p> **Descrição**: Obrigatório. Olá número toomultiply **multiplicando 1** com.|  
|div|Retorna o resultado de saudação de divisão de saudação dois números. Por exemplo, essa função retornará `1.0333`: <p>`div(10.333,10)` <p> **Número do parâmetro**: 1 <p> **Nome**: Dividendo <p> **Descrição**: Obrigatório. Olá número toodivide por Olá **Divisor**. <p> **Número do parâmetro**: 2 <p> **Nome**: Divisor <p> **Descrição**: Obrigatório. Olá número toodivide Olá **dividendo** por.|  
|mod|Retorna o resto de saudação após dividir dois números hello (módulo). Por exemplo, essa função retornará `2`: <p>`mod(10,4)` <p> **Número do parâmetro**: 1 <p> **Nome**: Dividendo <p> **Descrição**: Obrigatório. Olá número toodivide por Olá **Divisor**. <p> **Número do parâmetro**: 2 <p> **Nome**: Divisor <p> **Descrição**: Obrigatório. Olá número toodivide Olá **dividendo** por. Após a divisão de saudação restante Olá é obtido.|  
|Min|Há dois padrões diferentes para chamar essa função. <p>Aqui `min` pega uma matriz, e a função hello retorna `0`: <p>`min([0,1,2])` <p>Como alternativa, essa função pode conter uma lista separada por vírgulas de valores e também retorna `0`: <p>`min(0,1,2)` <p> **Observação**: todos os valores devem ser números, portanto, se o parâmetro hello é uma matriz, matriz Olá tem tooonly ter números. <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção ou Valor <p> **Descrição**: Obrigatório. Ou uma matriz de valores toofind Olá valor mínimo ou Olá primeiro valor de um conjunto. <p> **Número do parâmetro**: 2 ... *n* <p> **Nome**: Valor *n* <p> **Descrição**: Opcional. Se Olá primeiro parâmetro é um valor, em seguida, você pode passar valores adicionais e hello mínimo de todos os valores passados será retornado.|  
|max|Há dois padrões diferentes para chamar essa função. <p>Aqui `max` pega uma matriz, e a função hello retorna `2`: <p>`max([0,1,2])` <p>Como alternativa, essa função pode conter uma lista separada por vírgulas de valores e também retorna `2`: <p>`max(0,1,2)` <p> **Observação**: todos os valores devem ser números, portanto, se o parâmetro hello é uma matriz, matriz Olá tem tooonly ter números. <p> **Número do parâmetro**: 1 <p> **Nome**: Coleção ou Valor <p> **Descrição**: Obrigatório. Ou uma matriz de valores toofind Olá valor máximo ou Olá primeiro valor de um conjunto. <p> **Número do parâmetro**: 2 ... *n* <p> **Nome**: Valor *n* <p> **Descrição**: Opcional. Se Olá primeiro parâmetro é um valor, em seguida, você pode passar valores adicionais e hello máximo de todos os valores passados será retornado.|  
|range|Gera uma matriz de inteiros a partir de um determinado número. Você defina Olá Olá retornado de matriz. <p>Por exemplo, essa função retornará `[3,4,5,6]`: <p>`range(3,4)` <p> **Número do parâmetro**: 1 <p> **Nome**: Índice inicial <p> **Descrição**: Obrigatório. primeiro inteiro na matriz Olá Olá. <p> **Número do parâmetro**: 2 <p> **Nome**: Contagem <p> **Descrição**: Obrigatório. Esse valor é o número de saudação de inteiros que está na matriz de saudação.|  
|rand|Gera um aleatório inteiro dentro Olá especificado intervalo (inclusivo somente no final do primeiro). Por exemplo, essa função pode retornar `0` ou '1': <p>`rand(0,2)` <p> **Número do parâmetro**: 1 <p> **Nome**: Mínimo <p> **Descrição**: Obrigatório. Olá menor número inteiro que pode ser retornado. <p> **Número do parâmetro**: 2 <p> **Nome**: Máximo <p> **Descrição**: Obrigatório. Esse valor é o próximo número inteiro de saudação após o número inteiro mais alto Olá pode ser retornado.|  
  
### <a name="date-functions"></a>Funções de data  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|utcnow|Retorna Olá timestamp atual como uma cadeia de caracteres, por exemplo: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Número do parâmetro**: 1 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|addseconds|Adiciona um número inteiro de carimbo de cadeia de caracteres de tooa segundos passado. número de saudação de segundos pode ser positivo ou negativo. Por padrão, Olá resultado é uma cadeia de caracteres ISO 8601 formatar ("o"), a menos que um especificador de formato é fornecido. Por exemplo: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Número do parâmetro**: 1 <p> **Nome**: Carimbo de data/hora <p> **Descrição**: Obrigatório. Uma cadeia de caracteres que contém o tempo de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Segundos <p> **Descrição**: Obrigatório. número de saudação do tooadd segundos. Pode ser negativo toosubtract segundos. <p> **Número do parâmetro**: 3 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|addminutes|Adiciona um número inteiro de carimbo de cadeia de caracteres tooa de minutos passado. número de saudação de minutos pode ser positivo ou negativo. Por padrão, Olá resultado é uma cadeia de caracteres ISO 8601 formatar ("o"), a menos que um especificador de formato é fornecido. Por exemplo: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Número do parâmetro**: 1 <p> **Nome**: Carimbo de data/hora <p> **Descrição**: Obrigatório. Uma cadeia de caracteres que contém o tempo de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Minutos <p> **Descrição**: Obrigatório. número de saudação de tooadd minutos. Pode ser negativo toosubtract minutos. <p> **Número do parâmetro**: 3 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|addhours|Adiciona um número inteiro de carimbo de cadeia de caracteres de tooa horas passado. número de saudação de horas pode ser positivo ou negativo. Por padrão, Olá resultado é uma cadeia de caracteres ISO 8601 formatar ("o"), a menos que um especificador de formato é fornecido. Por exemplo: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Número do parâmetro**: 1 <p> **Nome**: Carimbo de data/hora <p> **Descrição**: Obrigatório. Uma cadeia de caracteres que contém o tempo de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Horas <p> **Descrição**: Obrigatório. número de saudação de tooadd horas. Pode ser negativo toosubtract horas. <p> **Número do parâmetro**: 3 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|adddays|Adiciona um número inteiro de carimbo de cadeia de caracteres tooa dias passado. número de saudação de dias pode ser positivo ou negativo. Por padrão, Olá resultado é uma cadeia de caracteres ISO 8601 formatar ("o"), a menos que um especificador de formato é fornecido. Por exemplo: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Número do parâmetro**: 1 <p> **Nome**: Carimbo de data/hora <p> **Descrição**: Obrigatório. Uma cadeia de caracteres que contém o tempo de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Dias <p> **Descrição**: Obrigatório. número de saudação do tooadd dias. Pode ser negativo toosubtract dias. <p> **Número do parâmetro**: 3 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|formatDateTime|Retorna uma cadeia de caracteres no formato de data. Por padrão, Olá resultado é uma cadeia de caracteres ISO 8601 formatar ("o"), a menos que um especificador de formato é fornecido. Por exemplo: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Número do parâmetro**: 1 <p> **Nome**: Data <p> **Descrição**: Obrigatório. Uma cadeia de caracteres que contém a data de saudação. <p> **Número do parâmetro**: 2 <p> **Nome**: Formato <p> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|startOfHour|Olá retorna Iniciar do hello hora tooa cadeia timestamp passado. Por exemplo `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.<br /><br />**Número do parâmetro**: 2<br /><br /> **Nome**: Formato<br /><br /> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.|  
|startOfDay|Olá retorna Iniciar do hello dia tooa cadeia timestamp passado. Por exemplo `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.<br /><br />**Número do parâmetro**: 2<br /><br /> **Nome**: Formato<br /><br /> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.| 
|startOfMonth|Olá retorna Iniciar do hello mês tooa cadeia timestamp passado. Por exemplo `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.<br /><br />**Número do parâmetro**: 2<br /><br /> **Nome**: Formato<br /><br /> **Descrição**: Opcional. Qualquer um [um único caractere de especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou um [padrões de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica como tooformat Olá valor esse carimbo. Se o formato não for fornecido, o formato de saudação ISO 8601 ("o") é usado.| 
|dayOfWeek|Retorna Olá dia de componente de semana de um carimbo de hora de cadeia de caracteres.  O domingo é 0, a segunda-feira é 1 e assim por diante. Por exemplo `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.| 
|dayOfMonth|Retorna Olá dia de componente de mês de um carimbo de hora de cadeia de caracteres. Por exemplo `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.| 
|dayOfYear|Retorna Olá dia de componente de ano de um carimbo de hora de cadeia de caracteres. Por exemplo `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.| 
|ticks|Olá retorna tiques a propriedade de um carimbo de hora de cadeia de caracteres. Por exemplo `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Número do parâmetro**: 1<br /><br /> **Nome**: Carimbo de data/hora<br /><br /> **Descrição**: Obrigatório. Isso é uma cadeia de caracteres que contém o tempo de saudação.| 
  
### <a name="workflow-functions"></a>Funções de fluxo de trabalho  

Essas funções ajudam a obter informações sobre Olá próprio fluxo de trabalho em tempo de execução.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|listCallbackUrl|Retorna um gatilho de saudação de tooinvoke de toocall de cadeia de caracteres ou uma ação. <p> **Observação**: Essa função só pode ser usada em uma **httpWebhook** e **apiConnectionWebhook**, não em uma **manual**, **recorrência**, **http**, ou **apiConnection**. <p>Por exemplo, Olá `listCallbackUrl()` função retorna: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|fluxo de trabalho|Essa função fornece todos os detalhes de saudação para Olá próprio fluxo de trabalho em tempo de execução de saudação. <p> As propriedades disponíveis no objeto de fluxo de trabalho de saudação são: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> Olá valor Olá `run` propriedade é um objeto com as seguintes propriedades: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Consulte Olá [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=525617) para obter detalhes sobre essas propriedades.<p> Por exemplo, tooget Olá nome da saudação atual executar, use Olá `"@workflow().run.name"` expressão. |

## <a name="next-steps"></a>Próximas etapas

[Gatilhos e ações do fluxo de trabalho](logic-apps-workflow-actions-triggers.md)
