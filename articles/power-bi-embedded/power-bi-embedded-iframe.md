---
title: aaaHow toouse Power BI inserido com REST | Microsoft Docs
description: 'Saiba como toouse Power BI inserido com REST '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Como toouse Power BI inserido com REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: o que é e para que serve

Uma visão geral do Power BI inserido é descrita em oficial Olá [site Power BI inserido](https://azure.microsoft.com/services/power-bi-embedded/), mas vamos dar uma olhada rápida antes de entrarmos em detalhes de saudação sobre usá-lo com REST.

Ele é realmente bem simples. Talvez você queira toouse visualizações de dados dinâmicos de saudação do [Power BI](https://powerbi.microsoft.com) em seu próprio aplicativo.

A maioria dos aplicativos personalizada precisa toodeliver dados de saudação para seus próprios clientes, não necessariamente usuários em sua própria organização. Por exemplo, se você estiver entregando algum serviço para a empresa e a empresa B, os usuários na empresa A deverão ver apenas dados de sua empresa A. Ou seja, multilocação Olá é necessária para a entrega de saudação.

aplicativo personalizado Hello também pode oferecer seus próprios métodos de autenticação, como autenticação de formulários, autenticação básica, etc... Em seguida, Olá incorporação de solução deve colaborar com segurança com esse método de autenticação existente. Também é necessário para os usuários toobe capaz de toouse os aplicativos ISV sem Olá extra compra ou licenciamento de uma assinatura do Power BI.

 O **Power BI Embedded** foi desenvolvido exatamente para esses tipos de cenários. Portanto, agora que temos Introdução rápida fora do modo de Olá, vamos falar alguns detalhes

Você pode usar o .NET Olá \(c#) ou Node. js SDK, tooeasily criar seu aplicativo com o Power BI inserido. Mas, neste artigo, explicaremos sobre o fluxo do HTTP \(incluindo AuthN) do Power BI sem SDKs. Noções básicas sobre este fluxo, você pode criar seu aplicativo **com qualquer linguagem de programação**, e você pode entender profundamente essência de saudação do Power BI inserido.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Criar a coleção de espaços de trabalho do Power BI e obter tecla de acesso \(provisionamento)

Power BI inserido é uma saudação em serviços do Azure. Olá somente ISV que usa o Portal do Azure é cobrado por taxas de uso \(por sessão de usuário por hora), e o usuário Olá que o relatório de saudação de modos de exibição não é carregada ou até mesmo exigir uma assinatura do Azure.
Antes de iniciar o nosso desenvolvimento de aplicativo, é necessário criar hello **coleta de espaço de trabalho do Power BI** usando o Portal do Azure.

Cada espaço de trabalho do Power BI inserido é o espaço de trabalho de saudação para cada cliente (Locatário) e adicionamos vários espaços de trabalho em cada coleção de espaço de trabalho. Olá a mesma chave de acesso é usado em cada coleção de espaço de trabalho. Em vigor, coleta de espaço de trabalho de saudação é o limite de segurança de saudação do Power BI inserido.

![](media/power-bi-embedded-iframe/create-workspace.png)

Quando concluir a criação de coleção de espaço de trabalho hello, copie a chave de acesso de saudação do Portal do Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Também podemos provisionar a coleção de espaço de trabalho hello e obter a chave de acesso por meio da API REST. mais, consulte toolearn [APIs de provedor de recursos do Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Criar o arquivo .pbix com o Power BI Desktop

Em seguida, devemos criar conexão de dados hello e toobe relatórios inseridos.
Para essa tarefa, não há programação nem código. Vamos usar apenas o Power BI Desktop.
Neste artigo, não entraremos detalhes Olá sobre como toouse Power BI Desktop. Se precisar de ajuda aqui, confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). Para nosso exemplo, usaremos Olá [exemplo de análise de varejo](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Criar um espaço de trabalho do Power BI

Agora que o provisionamento de saudação é feito, vamos começar a criar espaço de trabalho do cliente na coleção de espaço de trabalho Olá por meio de APIs REST. Olá seguir HTTP POST de solicitação (REST) é criar novo espaço de trabalho de saudação no nosso conjunto de espaço de trabalho existente. Isso é hello [API do espaço de trabalho de POST](https://msdn.microsoft.com/library/azure/mt711503.aspx). Em nosso exemplo, o nome da coleção de espaço de trabalho Olá é **mypbiapp**. Que acabamos de definir chave de acesso hello, que são copiados anteriormente, como **AppKey**. A autenticação é muito simples!

**Solicitação HTTP**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**Resposta HTTP**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Olá retornado **workspaceId** é usado para Olá chamadas API subsequentes a seguir. Nosso aplicativo deve manter esse valor.

## <a name="import-pbix-file-into-hello-workspace"></a>Importar o arquivo. pbix no espaço de trabalho de saudação

Cada relatório em um espaço de trabalho corresponde tooa único arquivo de área de trabalho do Power BI com um conjunto de dados \(incluindo as configurações de fonte de dados). Podemos importar nosso espaço de toohello do arquivo. pbix conforme mostrado no código de saudação abaixo. Como você pode ver, podemos carregar binário de saudação do arquivo. pbix usando MIME de partes múltiplas em http.

o fragmento de uri de saudação **32960a09-6366-4208-a8bb-9e0678cdbb9d** é workspaceId Olá e parâmetro de consulta **datasetDisplayName** é Olá toocreate de nome de conjunto de dados. Olá criado conjunto de dados contém todos os dados relacionados artefatos no arquivo. pbix como dados importados, Olá fonte de dados do ponteiro toohello, etc...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

A execução dessa tarefa de importação pode demorar um pouco. Ao concluir, nosso aplicativo pode solicitar o status da tarefa hello usando uma id de importação. Em nosso exemplo, a id de importação de saudação é **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

a seguir Hello está solicitando status com essa id de importação:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Se a tarefa de saudação não for concluída, Olá resposta HTTP poderia ser assim:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Se Olá tarefa estiver concluída, Olá resposta HTTP pode ser mais parecida com isto:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Conectividade da fonte de dados \(e multilocação de dados)

Enquanto quase todos os artefatos de saudação no arquivo. pbix são importados para nosso espaço de trabalho, Olá para fontes de dados não são credenciais. Como resultado, ao usar **o modo DirectQuery**, hello incorporados não podem ser exibidos corretamente. Mas, ao usar **modo de importação**, é possível exibir o relatório de hello usando dados importados existentes de saudação. Nesse caso, é necessário definir as credenciais de Olá usando as etapas a seguir por meio de chamadas REST de saudação.

Primeiro, devemos obter Olá gateway datasource. Sabemos que o conjunto de dados de saudação **id** é Olá anteriormente retornado id.

**Solicitação HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**Resposta HTTP**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

Usando hello retornadas id de gateway e id de fonte de dados \(consulte Olá anterior **gatewayId** e **id** Olá retornou resultados), é possível alterar a credencial de saudação desta fonte de dados da seguinte maneira:

**Solicitação HTTP**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**Resposta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

Em produção, também podemos definir cadeia de caracteres de conexão diferentes de saudação para cada espaço de trabalho usando a API REST. \(ou seja, poderá Separamos banco de dados de saudação para cada cliente.)

seguir Hello está mudando a cadeia de caracteres de conexão de saudação da fonte de dados por meio do REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Ou, podemos usar segurança em nível de linha no Power BI inserido e é possível separar dados de Olá para cada usuário em um relatório. Consequentemente, podemos provisionar cada relatório de cliente com o mesmo .pbix \(interface de usuário etc.) e diferentes fontes de dados.

> [!NOTE]
> Se você estiver usando **modo de importação** em vez de **o modo DirectQuery**, não há nenhum modelo de toorefresh de maneira por meio da API. As fontes de dados locais por meio do gateway do Power BI ainda não têm suporte no Power BI Embedded. No entanto, você vai realmente deseja tookeep atento Olá [blog do Power BI](https://powerbi.microsoft.com/blog/) para os quais são as novidades e quais são as novidades em futuras versões.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Autenticação e hospedagem (inserção) de relatórios em nossa página da Web

Em Olá anterior API de REST, podemos usar chave de acesso Olá **AppKey** a próprio como cabeçalho de autorização de saudação. Como essas chamadas podem ser tratadas no lado do servidor de back-end Olá, é seguro.

Mas, quando é inserir o relatório de saudação em nossa página da web, esse tipo de informação de segurança deve ser manipulado usando JavaScript \(front-end). Em seguida, o valor de cabeçalho de autorização Olá deve ser protegido. Se nossa tecla de acesso for descoberta por um usuário ou código mal-intencionado, eles poderão chamar qualquer operação usando essa chave.

Quando podemos inserir o relatório de saudação em nossa página da web, devem usar token computada Olá em vez de chave de acesso **AppKey**. Nosso aplicativo crie Olá OAuth Json Web Token \(JWT) que consiste em declarações hello e assinatura digital computada de saudação. Conforme ilustrado abaixo, este JWT OAuth são tokens de cadeia de caracteres codificados delimitados por ponto.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

Primeiro, é necessário preparar o valor de entrada hello, que é assinado posteriormente. Esse valor é cadeia de caracteres do hello base64 codificados de url (rfc4648) de saudação json a seguir, e esses são delimitadas por ponto Olá \(.) caracteres. Posteriormente, explicaremos como tooget Olá id do relatório.

> [!NOTE]
> Se quisermos toouse linha nível RLS (segurança) com o Power BI inserido, podemos também deve especificar **username** e **funções** em declarações de saudação.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Em seguida, é necessário criar a cadeia de caracteres codificada em base64 de Olá de HMAC \(assinatura Olá) com o algoritmo SHA256. Esse valor com sinal de entrada é cadeia de caracteres de saudação anterior.

Por último, podemos deve combinar o valor de entrada hello e cadeia de caracteres de assinatura usando o período \(.) caracteres. cadeia de caracteres de saudação concluída é token de aplicativo Olá Olá incorporação de relatório. Mesmo se o token de aplicativo hello for descoberto por um usuário mal-intencionado, eles não é possível obter a chave de acesso original hello. Esse token de aplicativo vai expirar rapidamente.

Veja um exemplo de PHP para essas etapas:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Por fim, inserir o relatório de saudação na página da web de saudação

Para inserir nosso relatório, devemos obter Olá inserir a url e o relatório **id** usando Olá API REST a seguir.

**Solicitação HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**Resposta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

Podemos pode inserir o relatório de saudação em nosso aplicativo web usando o token de aplicativo anterior Olá.
Se observarmos próximo código de exemplo hello, parte anterior Olá é Olá igual ao exemplo anterior hello. Na última parte de hello, este exemplo mostra Olá **embedUrl** \(consulte resultado anterior Olá) Olá iframe e está enviando o token de aplicativo hello em Olá iframe.

> [!NOTE]
> Você precisará toochange Olá relatório id valor tooone de sua preferência. Além disso, devido a erro de tooa em nosso sistema de gerenciamento de conteúdo, marca iframe de saudação no exemplo de código Olá é leitura literalmente. Remova o texto de saudação limitado de marca de saudação se você copiar e colar esse código de exemplo.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

Aqui está nosso resultado:

![](media/power-bi-embedded-iframe/view-report.png)

Neste momento, Power BI inserido mostra apenas relatório Olá em Olá iframe. Mas, fique atento Olá [Blog do Power BI](https://powerbi.microsoft.com/blog/). Melhorias futuras podem usar o novo cliente APIs que será vamos enviar informações em iframe Olá além de transmitir informações. Algo bem interessante!

## <a name="see-also"></a>Confira também
* [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)

Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

