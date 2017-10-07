---
title: "aaaEmbed um relatório no Azure Power BI inserido | Microsoft Docs"
description: "Saiba como tooembed um relatório no Power BI inserido em seu aplicativo."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Inserir um relatório em um Power BI Embedded

Saiba como tooembed um relatório no Power BI inserido em seu aplicativo.

Veremos como tooactually inserir um relatório em seu aplicativo. Isso presume que você já tenha um relatório que existe dentro de um espaço de trabalho em sua coleção de espaço de trabalho. Se você ainda não fez essa etapa, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).

Você pode usar o hello .NET (c#) ou o SDK do Node. js, juntamente com JavaScript, tooeasily criar seu aplicativo com o Power BI inserido. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Usando toouse de chaves de acesso Olá APIs REST

Na saudação de toocall ordem API REST, você pode passar chave de acesso de saudação que você pode obter de saudação portal do Azure para uma coleção de espaço de trabalho fornecido. Para obter mais informações, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Obter uma ID de relatório

Cada token de acesso se baseia em um relatório. Você precisará Olá tooget id de relatório fornecida para relatório de saudação que você deseja tooembed. Isso pode ser feito com base em chamadas toohello [obter relatórios](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST. Isso retornará relatório Olá id e hello inserem a url. Isso pode ser feito usando Olá SDK .NET do Power BI ou chamar hello API REST diretamente.

### <a name="using-hello-power-bi-net-sdk"></a>Usando Olá SDK .NET do Power BI

Ao usar o hello .NET SDK, você precisará toocreate uma credencial de token que se baseia a chave de acesso Olá obtido Olá portal do Azure. Isso requer que você instale Olá [pacote NuGet de API do Power BI](https://www.nuget.org/profiles/powerbi).

**Instalar o pacote NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Código C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Chamar hello API REST diretamente

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Criar um token de acesso

O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC. Olá tokens são assinados com a chave de acesso Olá da coleção de espaço de trabalho do Azure Power BI inserido. Inserir tokens, por padrão, são usada tooprovide ler apenas acesso tooa tooembed de relatório em um aplicativo. Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.

Tokens de acesso devem ser criados no servidor de saudação como chaves de acesso hello são usadas toosign/criptografar tokens de saudação. Para obter informações sobre como toocreate um token de acesso, consulte [autenticando e autorizar com o Power BI Embedded](power-bi-embedded-app-token-flow.md). Você também pode analisar Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método. Aqui está um exemplo de como isso seria usando o SDK .NET de saudação do Power BI.

Você usará a id de relatório de saudação que você recuperou anteriormente. Depois de inserir Olá token é criado, usará token Olá de toogenerate chave de acesso de saudação que você pode usar do ponto de vista do hello javascript. Olá *PowerBIToken classe* exige que você instale Olá [NuGut do pacote do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalar o pacote NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Código C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Adicionando tokens de tooembed de escopos de permissão

Ao usar tokens de inserção, talvez você queira toorestrict de uso dos recursos de saudação que concedem acesso ao. Por esse motivo, você pode gerar um token com as permissões no escopo. Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>Inserir usando JavaScript

Depois de ter o token de acesso de saudação e a id de relatório hello, podemos pode inserir relatório hello usando JavaScript. Isso requer que você instalar o nuget Olá [pacote Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Olá embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Você pode usar o hello [JavaScript relatório incorporar exemplo](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade. Ele também fornece exemplos de código para operações diferentes de saudação que estão disponíveis.

**Instalar o pacote NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Código JavaScript**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>Tamanho de saudação do conjunto de elementos inseridos

relatório de saudação será inserido automaticamente com base no tamanho de saudação de seu contêiner. tamanho de padrão de saudação toooverride de saudação incorpora simplesmente adicionar um estilos CSS de embutido ou atributo de classe de largura e altura.

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Pacote JavaScript do Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Pacote NuGet da API do Power BI](https://www.nuget.org/profiles/powerbi)
[Pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Repositório de Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repositório de Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)
