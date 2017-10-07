---
title: "Olá aaaUnderstand linguagem de consulta do Azure IoT Hub | Microsoft Docs"
description: "Guia do desenvolvedor - descrição da linguagem de consulta do tipo SQL IoT Hub Olá usado tooretrieve informações sobre trabalhos do seu hub IoT e twins do dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Referência – linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens

IoT Hub informa uma poderosa linguagem SQL tooretrieve sobre [twins dispositivo] [ lnk-twins] e [trabalhos][lnk-jobs]e [roteamento de mensagens][lnk-devguide-messaging-routes]. Este artigo apresenta:

* Uma introdução toohello principais recursos de linguagem de consulta de IoT Hub de hello e
* Olá descrição detalhada do idioma de saudação.

## <a name="get-started-with-device-twin-queries"></a>Introdução às consultas com dispositivos gêmeos
Os [dispositivos gêmeos][lnk-twins] podem conter objetos JSON arbitrários como tags e propriedades. IoT Hub permite tooquery twins de dispositivo como um único documento JSON que contém todas as informações do dispositivo duas.
Por exemplo, suponha que seu twins de dispositivo do hub IoT Olá estrutura a seguir:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT Hub expõe twins de dispositivo hello como uma coleção de documento chamada **dispositivos**.
Portanto Olá consulta a seguir recupera todo o conjunto de saudação do twins do dispositivo:

```sql
SELECT * FROM devices
```

> [!NOTE]
> Os [SDKs do Hub IoT][lnk-hub-sdks] dão suporte à paginação de resultados grandes.

IoT Hub permite twins de dispositivo tooretrieve filtragem com condições arbitrárias. Por exemplo,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

recupera Olá twins de dispositivo com hello **location.region** marca definido muito**EUA**.
Os operadores boolianos e as comparações aritméticas também têm suporte, por exemplo,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

recupera todos os twins dispositivos localizados em Olá nos configurado toosend telemetria menor geralmente a cada minuto. Como uma conveniência, também é possível toouse constantes de matriz com hello **na** e **login** operadores (não em). Por exemplo,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

recupera todos os dispositivos gêmeos que relataram conectividade WiFi ou com fio. Ele é geralmente necessário tooidentify todos os twins de dispositivo que contém uma propriedade específica. IoT Hub dá suporte a função hello `is_defined()` para essa finalidade. Por exemplo,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

recuperar todos os twins de dispositivo que definem Olá `connectivity` relatados de propriedade. Consulte toohello [cláusula WHERE] [ lnk-query-where] seção para referência completa Olá Olá recursos de filtragem.

Também há suporte para agrupamento e agregações. Por exemplo,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Retorna a contagem de saudação de dispositivos de saudação em cada status de configuração de telemetria.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Olá, exemplo acima ilustra uma situação onde três dispositivos relatado configuração bem-sucedida, dois ainda estiver aplicando a configuração hello e um relatou um erro.

### <a name="c-example"></a>Exemplo de C#
funcionalidade de consulta Olá é exposta pelo Olá [c# SDK do serviço] [ lnk-hub-sdks] em Olá **RegistryManager** classe.
Aqui está um exemplo de uma consulta simples:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Observe como Olá **consulta** objeto é instanciado com um tamanho de página (até too1000) e, em seguida, várias páginas podem ser recuperadas pela chamada hello **GetNextAsTwinAsync** métodos várias vezes.
Observe que esse objeto de consulta Olá expõe várias **próximo\***, dependendo de opção de desserialização Olá exigida por consulta hello, como objetos de duas ou trabalho do dispositivo, ou simples toobe JSON usado ao usar projeções.

### <a name="nodejs-example"></a>Exemplo do Node.js
funcionalidade de consulta Olá é exposta pelo Olá [serviço IoT do Azure SDK para Node.js] [ lnk-hub-sdks] em Olá **registro** objeto.
Aqui está um exemplo de uma consulta simples:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Observe como Olá **consulta** objeto é instanciado com um tamanho de página (até too1000) e, em seguida, várias páginas podem ser recuperadas pela chamada hello **nextAsTwin** métodos várias vezes.
Observe que esse objeto de consulta Olá expõe várias **próximo\***, dependendo de opção de desserialização Olá exigida por consulta hello, como objetos de duas ou trabalho do dispositivo, ou simples toobe JSON usado ao usar projeções.

### <a name="limitations"></a>Limitações
> [!IMPORTANT]
> Resultados da consulta podem ter alguns minutos de atraso com respeito toohello mais recentes valores no twins do dispositivo. Se consultar twins dispositivo individual por id, sempre é preferível toouse Olá recuperar duas API do dispositivo, que sempre contém valores mais recentes hello e tem limites de limitação superior.

Atualmente, há suporte para as comparações apenas entre tipos primitivos (sem objetos), por exemplo `... WHERE properties.desired.config = properties.reported.config` tem suporte apenas se essas propriedades tiverem valores primitivos.

## <a name="get-started-with-jobs-queries"></a>Introdução às consultas de trabalhos
[Trabalhos] [ lnk-jobs] fornecem uma maneira tooexecute operações em conjuntos de dispositivos. Duas cada dispositivo contém informações de saudação de trabalhos de saudação do qual faz parte de uma coleção chamada **trabalhos**.
Logicamente,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Atualmente, essa coleção é passível de consulta como **devices.jobs** em Olá linguagem de consulta de IoT Hub.

> [!IMPORTANT]
> No momento, a propriedade de trabalhos Olá nunca é retornada ao consultar twins de dispositivo (ou seja, consultas que contém 'de dispositivos'). Ela só pode ser acessada diretamente com consultas usando `FROM devices.jobs`.
>
>

Por exemplo, tooget todos os trabalhos (últimos e agendados) que afetam um único dispositivo, você pode usar o hello consulta a seguir:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Observe como esta consulta fornece o status de dispositivo específico hello (e possivelmente Olá método direto resposta) de cada trabalho retornado.
Também é possível toofilter com condições Boolianas arbitrárias em todas as propriedades do objeto no hello **devices.jobs** coleção.
Olá, por exemplo, a seguinte consulta:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

recupera todos os trabalhos de atualização do dispositivo gêmeo concluídos para o dispositivo **myDeviceId** que foram criados depois de setembro de 2016.

Também é possível tooretrieve Olá por dispositivo resultados um único trabalho.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Limitações
No momento, as consultas em **devices.jobs** não dão suporte a:

* Projeções, portanto, apenas `SELECT *` é possível.
* Condições que fazem referência a duas de dispositivo toohello nas propriedades de toojob de adição (consulte Olá anterior seção).
* Realização de agregações, tal como count, avg e group by.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Começar a usar expressões de consulta de rotas de mensagem do dispositivo para a nuvem

Usando [rotas de dispositivo para nuvem][lnk-devguide-messaging-routes], você pode configurar o IoT Hub mensagens de dispositivo para nuvem toodispatch toodifferent pontos de extremidade com base em expressões avaliadas em relação a mensagens individuais.

rota de saudação [condição] [ lnk-query-expressions] usa Olá a mesma linguagem de consulta de IoT Hub como condições em duas consultas de trabalho. Condições de rota são avaliadas no corpo e cabeçalhos de mensagem de saudação. A expressão de consulta de roteamento pode envolver somente cabeçalhos das mensagens, apenas Olá corpo da mensagem, ou em cabeçalhos de mensagem e corpo da mensagem. IoT Hub pressupõe um esquema específico para cabeçalhos de saudação e corpo de mensagem em mensagens de ordem de tooroute e Olá seções a seguir descreve o que é necessário para a rota do IoT Hub tooproperly:

### <a name="routing-on-message-headers"></a>Encaminhamento em cabeçalhos de mensagens

IoT Hub assume Olá representação JSON de cabeçalhos de mensagem para roteamento de mensagens a seguir:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Propriedades do sistema de mensagens são prefixadas com hello `'$'` símbolo.
As propriedades do usuário sempre serão acessadas com seu nome. Se um nome de propriedade do usuário acontece toocoincide com uma propriedade do sistema (como `$to`), propriedade de saudação do usuário será recuperada com hello `$to` expressão.
Você sempre pode acessar a propriedade do sistema hello usando colchetes `{}`: por exemplo, você pode usar a expressão de saudação `{$to}` tooaccess Olá propriedade sistema `to`. Nomes de propriedade entre colchetes sempre recuperam a propriedade de sistema correspondentes hello.

Lembre-se que os nomes de propriedade não diferenciam maiúsculas de minúsculas.

> [!NOTE]
> Todas as propriedades de mensagem são cadeias de caracteres. Propriedades do sistema, conforme descrito em Olá [guia desenvolvedor][lnk-devguide-messaging-format], não estão atualmente disponível toouse em consultas.
>

Por exemplo, se você usar um `messageType` propriedade, talvez você queira tooroute todos os ponto de extremidade de tooone de telemetria e o ponto de extremidade do todos os alertas tooanother. Você pode escrever Olá telemetria de saudação tooroute expressão a seguir:

```sql
messageType = 'telemetry'
```

E Olá mensagens de alerta tooroute Olá expressão a seguir:

```sql
messageType = 'alert'
```

Também há suporte para expressões e funções boolianas. Esse recurso permite que você toodistinguish entre o nível de gravidade, por exemplo:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Consulte toohello [expressão e condições] [ lnk-query-expressions] seção para a lista completa de saudação de funções e operadores com suporte.

### <a name="routing-on-message-bodies"></a>Encaminhamento em corpos de mensagem

IoT Hub só pode rotear com base no corpo da mensagem conteúdo se o corpo da mensagem de saudação está corretamente formado JSON codificado em UTF-8, UTF-16 e UTF-32. Você deve definir o tipo de conteúdo de saudação da mensagem de saudação muito`application/json` e Olá tooone de codificação de conteúdo de saudação suporte UTF codificações em tooallow de cabeçalhos de mensagem de saudação mensagem de saudação do IoT Hub tooroute com base no conteúdo do corpo de saudação. Se qualquer um dos cabeçalhos de saudação não for especificado, IoT Hub não tentará tooevaluate qualquer expressão de consulta que envolvem o corpo de saudação em relação a mensagem de saudação. Se a mensagem não é uma mensagem JSON, ou se a mensagem de saudação não especificar o tipo de conteúdo hello e codificação de conteúdo, você ainda pode usar mensagem de saudação tooroute com base em cabeçalhos de mensagem de saudação de roteamento de mensagens.

Você pode usar `$body` na mensagem de saudação do hello consulta expressão tooroute. Você pode usar uma referência de corpo simples, referência de matriz de corpo ou várias referências de corpo na expressão de consulta hello. A expressão de consulta também pode combinar uma referência de corpo a uma referência de cabeçalho de mensagem. Por exemplo, Olá seguem todas as expressões de consulta válida:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Noções básicas de uma consulta de Hub IoT
Todas as consultas de Hub IoT são compostas por cláusulas SELECT e FROM cláusulas WHERE e GROUP BY opcionais. Cada consulta é executada em uma coleção de documentos JSON, por exemplo, dispositivos gêmeos. cláusula FROM de saudação indica Olá documento coleção toobe iterada em (**dispositivos** ou **devices.jobs**). Em seguida, Olá filtro no hello onde cláusula é aplicada. Com agregações, resultados de saudação desta etapa serão agrupados como Olá especificado na cláusula GROUP BY e, para cada grupo, uma linha é gerada como especificado na cláusula SELECT hello.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Cláusula FROM
Olá **de < from_specification >** cláusula pode assumir somente dois valores: **de dispositivos**, tooquery twins do dispositivo, ou **de devices.jobs**, trabalho de tooquery por dispositivo detalhes.

## <a name="where-clause"></a>Cláusula WHERE
Olá **onde < filter_condition >** cláusula é opcional. Especifica uma ou mais condições que os documentos JSON Olá na coleção de FROM Olá devem atender toobe incluído como parte do resultado de saudação. Qualquer documento JSON deve ser avaliada Olá especificado condições muito "true" toobe incluído no resultado de saudação.

Olá permitido condições são descritas na seção [expressões e condições][lnk-query-expressions].

## <a name="select-clause"></a>Cláusula SELECT
cláusula SELECT Hello (**selecione < select_list >**) é obrigatório e especifica quais valores são recuperados da consulta de saudação. Ele especifica Olá JSON valores toobe usado toogenerate novos objetos JSON.
Para cada elemento de Olá subconjunto filtrado (e, opcionalmente, agrupado) da coleção de FROM hello, a fase de projeção hello gera um novo objeto JSON, construído com valores hello especificados na cláusula SELECT hello.

Gramática de saudação da cláusula SELECT Olá é do seguinte:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

onde **attribute_name** refere-se a propriedade tooany de documento JSON Olá na coleção de FROM hello. Alguns exemplos de cláusulas SELECT podem ser encontrados no hello [guia de Introdução com consultas de duas dispositivo] [ lnk-query-getstarted] seção.

No momento, as cláusulas de seleção diferentes de **SELECT \*** têm suporte apenas em consultas de agregação em dispositivos gêmeos.

## <a name="group-by-clause"></a>Cláusula GROUP BY
Olá **GROUP BY < group_specification >** cláusula é uma etapa opcional que pode ser executada depois de filtro de saudação especificado em Olá cláusula WHERE e antes de projeção de saudação especificada no hello selecionar. Ela agrupa documentos com base no valor de saudação de um atributo. Esses grupos são usados toogenerate agregado valores conforme especificado na cláusula SELECT hello.

Um exemplo de uma consulta usando GROUP BY é:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

a sintaxe formal Olá para GROUP BY é:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

onde **attribute_name** refere-se a propriedade tooany de documento JSON Olá na coleção de FROM hello.

Atualmente, a cláusula GROUP BY da saudação só tem suporte ao consultar twins do dispositivo.

## <a name="expressions-and-conditions"></a>Expressões e condições
Em um alto nível, uma *expressão*:

* Avalia tooan instância de um tipo JSON (como booleano, número, cadeia de caracteres, matriz ou objeto), e
* É definido pela manipulação de dados provenientes do documento JSON de dispositivo hello e constantes usando funções e operadores internos.

*Condições* são expressões que avaliam tooa booliano. Qualquer constante diferente de booliano **true** é considerado como **false** (incluindo **nulo**, **indefinido**, qualquer instância de objeto ou matriz qualquer cadeia de caracteres e claramente saudação booliano **false**).

saudação de sintaxe para expressões é:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

onde:

| Símbolo | Definição |
| --- | --- |
| attribute_name | Qualquer propriedade de documento JSON Olá Olá **FROM** coleção. |
| binary_operator | Qualquer operador binário listados no hello [operadores](#operators) seção. |
| function_name| Todas as funções listadas na Olá [funções](#functions) seção. |
| decimal_literal |Um float expresso em notação decimal. |
| hexadecimal_literal |Um número expresso pela cadeia de caracteres de saudação '0x' seguido por uma cadeia de caracteres de dígitos hexadecimais. |
| string_literal |Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape. As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: "). Escapes permitidos: `\'`, `\"`, `\\`, `\uXXXX` para caracteres Unicode definidos por quatro dígitos hexadecimais. |

### <a name="operators"></a>Operadores
Olá operadores a seguir têm suporte:

| Família | Operadores |
| --- | --- |
| Aritmético |+,-,*,/,% |
| Lógico |AND, OR, NOT |
| Comparação |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Funções
Ao consultar Olá twins e trabalhos só tem suportada a função é:

| Função | Descrição |
| -------- | ----------- |
| IS_DEFINED(propriedade) | Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor (incluindo `null`). |

Em condições de rotas, Olá funções matemáticas a seguir têm suporte:

| Função | Descrição |
| -------- | ----------- |
| ABS(x) | Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica. |
| EXP(x) | Retorna um valor Olá exponencial de saudação especificado expressão numérica (e ^ x). |
| POWER(x,y) | Retorna Olá Olá especificado valor toohello da expressão especificada power (x ^ y).|
| SQUARE(x) | Saudação de retorna quadrada de saudação especificado valor numérico. |
| CEILING(x) | Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada. |
| FLOOR(x) | Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica. |
| SIGN(x) | Retorna Olá positivo (+ 1), zero (0), ou sinal de negativo (-1) de saudação especificado expressão numérica.|
| SQRT(x) | Saudação de retorna quadrada de saudação especificado valor numérico. |

Em condições de rotas, Olá Verificando e funções de conversão de tipo a seguir têm suporte:

| Função | Descrição |
| -------- | ----------- |
| AS_NUMBER | Converte o número de tooa de cadeia de caracteres de entrada hello. `noop` se a entrada for um número; `Undefined` se a cadeia de caracteres não representar um número.|
| IS_ARRAY | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma matriz. |
| IS_BOOL | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um valor booleano. |
| IS_DEFINED | Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor. |
| IS_NULL | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é nulo. |
| IS_NUMBER | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um número. |
| IS_OBJECT | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um objeto JSON. |
| IS_PRIMITIVE | Retorna um valor booliano que indica se o tipo de saudação do hello especificado de expressão é um primitivo (cadeia de caracteres, booleano, numérico ou `null`). |
| IS_STRING | Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma cadeia de caracteres. |

Em condições de rotas, Olá funções de cadeia de caracteres a seguir têm suporte:

| Função | Descrição |
| -------- | ----------- |
| CONCAT(x, …) | Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres. |
| LENGTH(x) | Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres.|
| LOWER(x) | Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados. |
| UPPER(x) | Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados. |
| SUBSTRING(cadeia de caracteres, início [, tamanho]) | Retorna parte de uma expressão de cadeia de caracteres começando em Olá especificado a posição do caractere com base em zero e continua toohello especificado comprimento ou toohello final da cadeia de caracteres de saudação. |
| INDEX_OF (cadeia de caracteres, fragmento) | Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada.|
| STARTS_WITH(x, y) | Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello começa com hello segundo. |
| ENDS_WITH(x, y) | Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo. |
| CONTAINS(x,y) | Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo. |

## <a name="next-steps"></a>Próximas etapas
Saiba como as consultas em seus aplicativos usando tooexecute [SDKs do Azure IoT][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
