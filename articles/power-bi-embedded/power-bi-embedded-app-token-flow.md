---
title: Autenticando e autorizando com o Power BI Embedded
description: Autenticando e autorizando com o Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Autenticando e autorizando com o Power BI Embedded

O serviço Power BI Embedded usa **Chaves** e **Tokens de Aplicativo** para autenticação e autorização, em vez de usar autenticação explícita do usuário final. Nesse modelo, seu aplicativo gerencia a autenticação e autorização para os usuários finais. Quando necessário, seu aplicativo cria e envia os Tokens de Aplicativo que dizem ao nosso serviço para renderizar o relatório solicitado. Esse design não requer que o aplicativo use o Azure Active Directory para autorização e autenticação de usuário, embora você possa fazer isso.

## <a name="two-ways-to-authenticate"></a>Duas maneiras de autenticar

**Chave** - você pode usar chaves para todas as chamadas à API de REST do Power BI Embedded. As chaves podem ser encontradas no **Portal do Azure** clicando em **Todas as configurações** e **Chaves de acesso**. Sempre use a chave como se fosse uma senha. Essas chaves têm permissões para fazer qualquer chamada à API REST em uma coleção de espaço de trabalho específica.

Para usar uma chave em uma chamada REST, adicione o seguinte cabeçalho de autorização:            

    Authorization: AppKey {your key}

**Token de aplicativo** - tokens de aplicativo são usados para todas as solicitações de inserção. Eles são projetados para serem executados no lado do cliente e, portanto, estão restritos a um único relatório. É uma prática recomendada definir um tempo de expiração.

Os tokens de aplicativo são um JWT (Token Web JSON) assinado por uma das suas chaves.

O token de seu aplicativo pode conter as seguintes declarações:

| Declaração | Descrição |
| --- | --- |
| **ver** |A versão do token do aplicativo. A versão atual é 0.2.0. |
| **aud** |O destinatário pretendido do token. Para uso do Power BI Embedded: "https://analysis.windows.net/powerbi/api". |
| **iss** |Uma cadeia de caracteres que indica o aplicativo que emitiu o token. |
| **tipo** |O tipo de token do aplicativo que está sendo criado. O único tipo com suporte atualmente é **incorporar**. |
| **wcn** |Nome da coleção de espaços de trabalho para o qual o token foi emitido. |
| **wid** |ID do espaço de trabalho para o qual o token foi emitido. |
| **rid** |ID ddo relatório para o qual o token foi emitido. |
| **nome de usuário** (opcional) |Usado com RLS, é uma cadeia de caracteres que pode ser usada para ajudar a identificar o usuário ao aplicar regras RLS. |
| **funções** (opcional) |Uma cadeia de caracteres que contém as funções a selecionar ao aplicar regras de segurança em nível de linha. Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres. |
| **SCP** (opcional) |Uma cadeia de caracteres que contém os escopos de permissões. Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres. |
| **exp** (opcional) |Indica a hora em que o token irá expirar. Elas devem ser transmitidas como carimbos de data/hora do Unix. |
| **nbf** (opcional) |Indica a hora em que o token começa a valer. Elas devem ser transmitidas como carimbos de data/hora do Unix. |

Um token do aplicativo de exemplo terá esta aparência:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Quando decodificado, ele terá esta aparência:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Há métodos disponíveis dentro dos SDKs que facilitam a criação de tokens de aplicativo. Por exemplo, para .NET, você pode examinar a classe [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) e os métodos [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).

Para o SDK do .NET, você pode consultar [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Escopos

Ao usar os tokens de inserção, convém restringir o uso de recursos aos quais você concede acesso. Por esse motivo, você pode gerar um token com as permissões no escopo.

A seguir estão os escopos disponíveis para o Power BI Embedded.

|Escopo|Descrição|
|---|---|
|Dataset.Read|Fornece permissão para ler o conjunto de dados especificado.|
|Dataset.Write|Fornece permissão para gravar o conjunto de dados especificado.|
|Dataset.ReadWrite|Fornece permissão para leitura e gravação do conjunto de dados especificado.|
|Report.Read|Fornece permissão para exibir o relatório especificado.|
|Report.ReadWrite|Fornece permissão para exibir e editar o relatório especificado.|
|Workspace.Report.Create|Fornece permissão para criar um novo relatório no espaço de trabalho especificado.|
|Workspace.Report.Copy|Fornece permissão para clonar um relatório existente no espaço de trabalho especificado.|

Você pode fornecer vários escopos usando um espaço entre os escopos semelhante ao que segue.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Declarações necessárias - escopos**

scp: {scopesClaim} scopesClaim pode ser uma cadeia de caracteres ou uma matriz de cadeias de caracteres, observando as permissões permitidas para recursos do espaço de trabalho (relatório, conjunto de dados, etc.)

Um token decodificado, com escopos definidos, seria semelhante ao seguinte.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Operações e escopos

|Operação|Recurso de destino|Permissões de token|
|---|---|---|
|Criar (na memória) um novo relatório com base em um conjunto de dados.|Conjunto de dados|Dataset.Read|
|Criar (na memória) um novo relatório com base em um conjunto de dados e salvar o relatório.|Conjunto de dados|* Dataset.Read<br>* Workspace.Report.Create|
|Exibir e explorar/Editar (na memória) um relatório existente. Report.Read implica Dataset.Read. Isso não lhe dará permissões para salvar as edições.|Relatório|Report.Read|
|Editar e salvar um relatório existente.|Relatório|Report.ReadWrite|
|Salvar uma cópia de um relatório (Salvar como).|Relatório|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-the-flow-works"></a>Como funciona o fluxo
1. Copie as chaves de API para o seu aplicativo. Você pode obter as chaves no **Portal do Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. O token faz a asserção de uma declaração e tem uma data de validade.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. O token é assinado com uma chave de acesso de API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Solicitações do usuário para exibir um relatório.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. O token é validado com uma chave de acesso de API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. O Power BI Embedded envia um relatório para o usuário.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Após o **Power BI Embedded** enviar um relatório para o usuário, o usuário pode exibir o relatório em seu aplicativo personalizado. Por exemplo, se você importou o [exemplo de PBIX Analisando Dados de Vendas](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), o aplicativo Web de exemplo teria essa aparência:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Consulte também

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Introdução ao exemplo do Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Cenários comuns do Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introdução ao Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Repositório de Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
Mais perguntas? [Experimentar a comunidade do Power BI](http://community.powerbi.com/)

