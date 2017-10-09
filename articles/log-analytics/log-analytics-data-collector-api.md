---
title: "API de coletor de dados de HTTP de análise de aaaLog | Microsoft Docs"
description: "Você pode usar o hello API do coletor de dados do Log Analytics HTTP tooadd POST JSON toohello análise de Log repositório de dados de qualquer cliente que pode chamar a API REST de saudação. Este artigo descreve como toouse Olá API e tem exemplos de como toopublish dados usando linguagens de programação diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Enviar dados tooLog análise com hello API de coletor de dados HTTP
Este artigo mostra como toouse Olá API de coletor de dados HTTP toosend dados tooLog análise de um cliente de API REST.  Ele descreve como tooformat dados coletados pelo seu script ou aplicativo, incluí-lo em uma solicitação e ter essa solicitação autorizada pela análise de Log.  Os exemplos são fornecidos para PowerShell, C# e Python.

## <a name="concepts"></a>Conceitos
Você pode usar o hello API de coletor de dados HTTP toosend dados tooLog análise de qualquer cliente que pode chamar uma API REST.  Isso pode ser um runbook na automação do Azure que o gerenciamento de coleta dados do Azure ou outra nuvem ou podem ser um sistema de gerenciamento alternativo que usa análise de Log tooconsolidate e analisar dados.

Todos os dados no repositório de análise de Log de saudação é armazenado como um registro com um tipo de registro específico.  Você pode formatar seu toohello toosend de dados API de coletor de dados HTTP como vários registros em JSON.  Quando você envia dados hello, um registro individual é criado no repositório de saudação para cada registro na carga de solicitação de saudação.


![Visão geral do Coletor de Dados HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Criar uma solicitação
API de coletor de dados do toouse Olá HTTP, você criar uma solicitação POST que inclui Olá dados toosend na notação JSON (JavaScript Object).  Olá três tabelas lista Olá atributos que são necessários para cada solicitação. Descrevemos cada atributo em mais detalhes posteriormente neste artigo hello.

### <a name="request-uri"></a>URI da solicitação
| Atributo | Propriedade |
|:--- |:--- |
| Método |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Tipo de conteúdo |aplicativo/json |

### <a name="request-uri-parameters"></a>Solicitar parâmetros de URI (Uniform Resource Identifier)
| Parâmetro | Descrição |
|:--- |:--- |
| CustomerID |Olá identificador exclusivo para o espaço de trabalho do hello Microsoft Operations Management Suite. |
| Recurso |nome do recurso Olá API: api/logs. |
| Versão da API |versão de saudação do hello API toouse com esta solicitação. Atualmente, ela é 2016-04-01. |

### <a name="request-headers"></a>Cabeçalhos da solicitação
| Cabeçalho | Descrição |
|:--- |:--- |
| Autorização |assinatura de autorização de saudação. Artigo hello, você pode ler sobre como cabeçalho toocreate um HMAC-SHA256. |
| Log-Type |Especifica o tipo de registro de saudação de dados de saudação que está sendo enviados. Atualmente, o tipo de log Olá dá suporte a somente caracteres alfa. Ele não dá suporte a caracteres alfanuméricos ou caracteres especiais. |
| x-ms-date |Data de saudação solicitação Olá foi processada, no formato RFC 1123. |
| time-generated-field |nome de saudação de um campo nos dados de saudação que contém o carimbo de hora Olá Olá do item de dados. Se você especificar um campo, seu conteúdo será usado para **TimeGenerated**. Se esse campo não for especificado, Olá padrão para **TimeGenerated** é tempo de saudação que hello mensagem está incluída. conteúdo de saudação do campo de mensagem de saudação deve seguir o formato de saudação ISO 8601 aaaa-MM-ddTHH. |

## <a name="authorization"></a>Autorização
Qualquer API de coletor de dados de HTTP de análise de Log de toohello de solicitação deve incluir um cabeçalho de autorização. tooauthenticate uma solicitação, você deve assinar a solicitação de saudação com hello primário ou a chave secundária Olá para espaço de trabalho de saudação que está fazendo a solicitação de saudação. Em seguida, passe essa assinatura como parte da solicitação de saudação.   

Aqui é o formato de saudação do cabeçalho de autorização de saudação:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* é o identificador exclusivo de saudação do espaço de trabalho do hello Operations Management Suite. *Assinatura* é um [baseadas em Hash HMAC Message Authentication Code ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que é construído a partir de solicitação hello e, em seguida, computado usando Olá [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Em seguida, você o codifica usando a codificação Base64.

Use este Olá tooencode de formato **SharedKey** cadeia de caracteres de assinatura:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Aqui está um exemplo de uma cadeia de caracteres de assinatura:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Quando há uma cadeia de caracteres de assinatura hello, codificá-lo usando Olá algoritmo HMAC-SHA256 na Olá cadeia de caracteres codificados em UTF-8 e, em seguida, codificar o resultado de saudação como Base64. Use este formato:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

exemplos de saudação nas seções próximos Olá têm toohelp de código de exemplo, crie um cabeçalho de autorização.

## <a name="request-body"></a>Corpo da solicitação
corpo de saudação de mensagem de saudação deve estar em JSON. Ele deve incluir um ou mais registros com pares de nome e valor da propriedade Olá neste formato:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Você pode processar em lotes vários registros em uma única solicitação usando Olá formato a seguir. Todos os registros de saudação devem ser Olá mesmo tipo de registro.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Propriedades e o tipo de registro
Você definir um tipo de registro personalizadas ao enviar dados por meio de saudação API de coletor de dados de HTTP de análise de Log. No momento, você não pode gravar dados tooexisting tipos de registros que foram criados por outros tipos de dados e soluções. Análise de log lê os dados de entrada hello e, em seguida, cria propriedades que correspondem a tipos de dados de saudação de valores de saudação que você inserir.

Cada toohello solicitação API de análise de Log deve incluir um **tipo de Log** cabeçalho com nome Olá Olá ao tipo de registro. sufixo de saudação **_CL** é acrescentada automaticamente toohello nome toodistinguish do log de outros tipos como um log personalizado. Por exemplo, se você inserir o nome da saudação **MyNewRecordType**, análise de Log cria um registro com tipo hello **MyNewRecordType_CL**. Isso ajuda a garantir que não haja nenhum conflito entre os nomes de tipo criados pelo usuário e aqueles fornecidos nas soluções atuais ou futuras da Microsoft.

tooidentify de tipo de dados de uma propriedade, a análise de Log adiciona um nome de propriedade toohello sufixo. Se uma propriedade contiver um valor nulo, a propriedade de saudação não está incluída no registro. Esta tabela lista o tipo de dados de propriedade hello e sufixo correspondente:

| Tipo de dados de propriedade | Suffix |
|:--- |:--- |
| Cadeia de caracteres |_s |
| Booliano |_b |
| Duplo |_d |
| Data/hora |_t |
| GUID |_g |

tipo de dados de saudação que usa análise de Log para cada propriedade depende se o tipo de registro de saudação para novo registro de saudação já existe.

* Se o tipo de registro de saudação não existir, a análise de Log cria um novo. Análise de log usa Olá JSON inferência toodetermine Olá tipo de dados para cada propriedade para o novo registro de saudação.
* Se o tipo de registro Olá existir, análise de Log tentativas toocreate um novo registro com base nas propriedades existentes. Se hello tipo de dados para uma propriedade no novo registro de saudação não corresponder e não pode ser convertido toohello existente do tipo ou se hello registro inclui uma propriedade que não existe, a análise de Log cria uma nova propriedade que tem o sufixo relevantes hello.

Por exemplo, esta entrada de envio criaria um registro com três propriedades, **number_d**, **boolean_b** e **string_s**:

![Registro de exemplo 1](media/log-analytics-data-collector-api/record-01.png)

Se você, em seguida, enviar essa próxima entrada, com todos os valores formatados como cadeias de caracteres, propriedades de saudação não seriam alterado. Esses valores podem ser convertidos tooexisting tipos de dados:

![Registro de exemplo 2](media/log-analytics-data-collector-api/record-02.png)

Mas, se você fez, em seguida, o próximo envio, análise de Log cria Olá novas propriedades **boolean_d** e **string_d**. Esses valores não podem ser convertidos:

![Registro de exemplo 3](media/log-analytics-data-collector-api/record-03.png)

Se você, então, enviadas Olá seguinte entrada, antes de tipo de registro de saudação foi criado, a análise de Log criaria um registro com três propriedades, **núm_s**, **boolean_s**, e **string_s**. Nesta entrada, cada um dos valores de saudação inicial é formatada como uma cadeia de caracteres:

![Registro de exemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Limites de dados
Há algumas restrições em torno dos dados Olá postadas toohello coleta de dados de análise de Log de API.

* Máximo de 30 MB por post tooLog API do coletor de dados de análise. Este é um limite de tamanho para um único post. Se dados de saudação de uma postagem único que excede 30 MB, você deve dividi-Olá dados toosmaller dimensionado blocos e enviá-los simultaneamente.
* Limite máximo de 32 KB para valores de campo. Se o valor do campo Olá é maior do que 32 KB, dados saudação serão truncados.
* O número máximo recomendado de campos para um determinado tipo é 50. Este é um limite prático de uma perspectiva de experiência de pesquisa e usabilidade.  

## <a name="return-codes"></a>Códigos de retorno
Olá o código de status HTTP 200 significa que essa solicitação Olá foi recebida para processamento. Isso indica que essa operação Olá foi concluída com êxito.

Esta tabela lista o conjunto completo de saudação de códigos de status que serviço Olá pode retornar:

| Código | Status | Código do erro | Descrição |
|:--- |:--- |:--- |:--- |
| 200 |OK | |solicitação de saudação aceita com êxito. |
| 400 |Solicitação incorreta |InactiveCustomer |espaço de trabalho de saudação foi fechado. |
| 400 |Solicitação incorreta |InvalidApiVersion |versão de API de saudação especificado não foi reconhecido pelo serviço de saudação. |
| 400 |Solicitação incorreta |InvalidCustomerId |ID do espaço de trabalho Olá especificado é inválido. |
| 400 |Solicitação incorreta |InvalidDataFormat |JSON inválido foi enviado. corpo da resposta Olá pode conter mais informações sobre como tooresolve Olá erro. |
| 400 |Solicitação incorreta |InvalidLogType |tipo de log Olá especificado independentes caracteres especiais ou valores numéricos. |
| 400 |Solicitação incorreta |MissingApiVersion |versão da API Olá não foi especificado. |
| 400 |Solicitação incorreta |MissingContentType |tipo de conteúdo de saudação não foi especificado. |
| 400 |Solicitação incorreta |MissingLogType |Olá necessário o tipo de valor de log não foi especificado. |
| 400 |Solicitação incorreta |UnsupportedContentType |tipo de conteúdo de saudação não foi definido muito**aplicativo/json**. |
| 403 |Proibido |InvalidAuthorization |solicitação de saudação tooauthenticate falha do serviço de saudação. Verifique se essa chave de ID e a conexão de espaço de trabalho Olá são válidos. |
| 404 |Não encontrado | | Ou Olá URL fornecida está incorreta ou solicitação de saudação é muito grande. |
| 429 |Número Excessivo de Solicitações | | serviço de saudação está apresentando um alto volume de dados de sua conta. Tente novamente a solicitação hello mais tarde. |
| 500 |Erro interno do servidor |UnspecifiedError |serviço de saudação encontrou um erro interno. Tente novamente a solicitação de saudação. |
| 503 |Serviço indisponível |ServiceUnavailable |Atualmente, o serviço de saudação é solicitações tooreceive não está disponível. Tente novamente a sua solicitação. |

## <a name="query-data"></a>Consultar dados
tooquery dados enviados pelo Olá API análise de Log HTTP dados coletor, procurar registros com **tipo** que é igual toohello **LogType** valor que você especificou, concatenado com **_CL**. Por exemplo, se você usou **MyCustomLog**, você poderia retornar todos os registros com **Type=MyCustomLog_CL**.

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Solicitações de exemplo
Nas seções de Avançar hello, você encontrará exemplos de como toosubmit dados toohello API de coletor de dados de HTTP de análise de Log usando as linguagens de programação diferentes.

Para cada exemplo, siga estas etapas tooset variáveis de saudação do cabeçalho de autorização de saudação:

1. No portal do Operations Management Suite hello, selecione Olá **configurações** lado a lado e, em seguida, selecione Olá **fontes conectadas** guia.
2. toohello à direita do **ID do espaço de trabalho**, selecione o ícone para copiar Olá e, em seguida, cole a ID de hello como valor de saudação do hello **Customer ID** variável.
3. toohello à direita do **chave primária**, selecione o ícone para copiar Olá e, em seguida, cole a ID de hello como valor de saudação do hello **chave compartilhada** variável.

Como alternativa, você pode alterar variáveis Olá Olá tipo de log e dados JSON.

### <a name="powershell-sample"></a>Exemplo do PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Exemplo de C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Exemplo de Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Próximas etapas
- Saudação de uso [API de pesquisa de Log](log-analytics-log-search-api.md) tooretrieve dados do repositório de análise de Log de saudação.
