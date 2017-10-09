---
title: "as funções definidas pelo usuário aaaAzure Stream Analytics JavaScript | Microsoft Docs"
description: "Executar o mecanismo de consulta avançada com funções definidas pelo usuário do JavaScript"
keywords: "javascript, funções definidas pelo usuário, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Funções definidas pelo usuário do JavaScript do Stream Analytics do Azure
O Stream Analytics do Azure dá suporte a funções definidas pelo usuário gravadas em JavaScript. Com um conjunto avançado de saudação do **cadeia de caracteres**, **RegExp**, **matemática**, **matriz**, e **data** métodos que Transformações de dados complexos com trabalhos do Stream Analytics fornece JavaScript, se tornam mais fácil toocreate.

## <a name="javascript-user-defined-functions"></a>Funções definidas pelo usuário de JavaScript
As funções definidas pelo usuário de JavaScript dão suporte a funções escalares sem monitoração de estado somente para computação que não requerem conectividade externa. Olá retornar o valor de uma função só pode ser um valor escalar (único). Depois de adicionar um trabalho de tooa de função definida pelo usuário de JavaScript, você pode usar função hello em qualquer lugar na consulta hello, como uma função escalar interna.

Aqui estão alguns cenários nos quais as funções definidas pelo usuário JavaScript podem ser úteis:
* Análise e manipulação de cadeia de caracteres com funções de expressão regular, por exemplo, **Regexp_Replace()** e **Regexp_Extract()**
* Decodificação e codificação de dados, por exemplo, conversão de binário em hexadecimal
* Executando cálculos matemáticos com funções **Matemáticas** do JavaScript
* Executando operações de matriz como classificar, juntar, localizar e preencher

Aqui estão ações que não podem ser realizadas com uma função definida pelo usuário do JavaScript no Stream Analytics:
* Chamar pontos de extremidade REST externos, por exemplo, executando pesquisa inversa de IP ou extração de dados de referência de uma fonte externa
* Executar serialização ou desserialização de formato de evento personalizado em entradas/saídas
* Criar agregações personalizadas

Embora funções como **Date.GetDate()** ou **Math** não são bloqueadas na definição de funções hello, evite usá-los. Essas funções **não** retorno Olá mesmo resultado sempre que você chamá-las e Olá serviço Azure Stream Analytics não manter um diário de chamadas de função e retornou resultados. Se uma função retorna resultados diferentes em Olá mesmos eventos, capacidade de repetição não é garantida quando um trabalho for reiniciado por você ou pelo serviço de análise de fluxo de saudação.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Adicionar uma função definida pelo usuário do JavaScript no hello portal do Azure
toocreate uma função JavaScript simples de definida pelo usuário, em um trabalho de análise de fluxo existente, siga estas etapas:

1.  Em Olá portal do Azure, localize o trabalho do Stream Analytics.
2.  Em **TOPOLOGIA DO TRABALHO**, selecione sua função. Uma lista vazia de funções é exibida.
3.  toocreate uma nova função definida pelo usuário, selecione **adicionar**.
4.  Em Olá **nova função** folha, para **tipo de função**, selecione **JavaScript**. Um modelo de função padrão aparece no editor de saudação.
5.  Para Olá **alias UDF**, digite **hex2Int**e alterar a implementação da função hello da seguinte maneira:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Selecione **Salvar**. A função aparece na lista de saudação de funções.
7.  Selecione Olá novo **hex2Int** de função e verifique a definição da função hello. Todas as funções têm um **UDF** alias de função do prefixo toohello adicionado. É necessário muito*incluir Olá prefixo* quando você chama a função hello em sua consulta de análise de fluxo. Nesse caso, você chama **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Chamar uma função definida pelo usuário do JavaScript em uma consulta

1. Em Olá editor de consultas, em **trabalho topologia**, selecione **consulta**.
2.  Editar a consulta e, em seguida, chamar hello-função definida pelo usuário, como este:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  arquivo de dados de exemplo tooupload hello, com o botão direito Olá trabalho entrada.
4.  tootest sua consulta, selecione **teste**.


## <a name="supported-javascript-objects"></a>Objetos JavaScript com suporte
As funções definidas pelo usuário do JavaScript do Stream Analytics do Azure dão suporte a objetos JavaScript internos e padrão. Para obter uma lista desses objetos, consulte [Objetos Globais](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Conversão de tipo do Stream Analytics e JavaScript

Há diferenças nos tipos de saudação que dão suporte a linguagem de consulta do Stream Analytics hello e JavaScript. Esta tabela lista os mapeamentos de conversão de saudação entre hello dois:

Stream Analytics | JavaScript
--- | ---
bigint | Número (JavaScript apenas pode representar inteiros de tooprecisely 2 ^ 53)
Datetime | Data (o JavaScript dá suporte somente a milissegundos)
double | Número
nvarchar(MAX) | Cadeia de caracteres
Registro | Objeto
Matriz | Matriz
NULO | Nulo


Aqui estão as conversões de JavaScript para Stream Analytics:


JavaScript | Análise de fluxo
--- | ---
Número | Bigint (se o número de saudação é round e entre longa. MinValue e long. MaxValue; Caso contrário, é double)
Data | DateTime
Cadeia de caracteres | nvarchar(MAX)
Objeto | Registro
Matriz | Matriz
Null, Undefined | NULO
Qualquer outro tipo (por exemplo, uma função ou um erro) | Sem suporte (resulta em erro de tempo de execução)

## <a name="troubleshooting"></a>Solucionar problemas
Erros de tempo de execução do JavaScript são considerados fatais e são apresentados por meio do log de atividades de saudação. tooretrieve Olá login, Olá portal do Azure, vá tooyour trabalho e selecione **log de atividades**.


## <a name="other-javascript-user-defined-function-patterns"></a>Outros padrões de função definida pelo usuário do JavaScript

### <a name="write-nested-json-toooutput"></a>Gravar toooutput aninhada de JSON
Se você tiver uma etapa de processamento de acompanhamento que usa um trabalho de análise de fluxo de saída como entrada, e requer um formato JSON, você pode escrever um toooutput de cadeia de caracteres JSON. Olá próximo exemplo chama Olá **JSON.stringify()** toopack todos os pares de nome/valor de saudação de entrada e, em seguida, gravação-los como um valor de cadeia de caracteres único na saída de função.

**Definição de funções definidas pelo usuário de JavaScript:**

```
function main(x) {
return JSON.stringify(x);
}
```

**Consulta de exemplo:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Obter ajuda
Para obter ajuda adicional, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do gerenciamento do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
