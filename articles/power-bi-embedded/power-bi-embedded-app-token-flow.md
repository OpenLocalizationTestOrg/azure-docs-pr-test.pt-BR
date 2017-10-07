---
title: aaaAuthenticating e autorizar com o Power BI Embedded
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Autenticando e autorizando com o Power BI Embedded

Olá serviço Power BI inserido usa **chaves** e **Tokens do aplicativo** para autenticação e autorização, em vez da autenticação explícita do usuário final. Nesse modelo, seu aplicativo gerencia a autenticação e autorização para os usuários finais. Quando necessário, seu aplicativo cria e envia os Tokens de aplicativo hello que informa ao nosso serviço toorender Olá relatório solicitado. Esse design não requer toouse seu aplicativo do Azure Active Directory para autenticação e autorização, embora você ainda pode.

## <a name="two-ways-tooauthenticate"></a>Duas maneiras tooauthenticate

**Chave** - você pode usar chaves para todas as chamadas à API de REST do Power BI Embedded. Olá chaves podem ser encontradas no hello **portal do Azure** clicando em **todas as configurações** e **chaves de acesso**. Sempre use a chave como se fosse uma senha. Essas chaves têm permissões toomake chamar qualquer API REST em uma coleção de espaço de trabalho específico.

toouse uma chave em uma chamada REST, adicione Olá cabeçalho de autorização a seguir:            

    Authorization: AppKey {your key}

**Token de aplicativo** - tokens de aplicativo são usados para todas as solicitações de inserção. Elas são projetadas toobe executado no cliente, para que eles sejam restritos tooa único relatório e suas tooset de prática recomendada de um tempo de expiração.

Os tokens de aplicativo são um JWT (Token Web JSON) assinado por uma das suas chaves.

O token de seu aplicativo pode conter Olá declarações a seguir:

| Declaração | Descrição |
| --- | --- |
| **ver** |versão de saudação do token de aplicativo hello. 0.2.0 é a versão atual do hello. |
| **aud** |Olá destinatário do token de saudação. Para uso do Power BI Embedded: "https://analysis.windows.net/powerbi/api". |
| **iss** |Uma cadeia de caracteres que indica o aplicativo hello que emitiu o token de saudação. |
| **tipo** |tipo de saudação do token de aplicativo que está sendo criado. Tipo de saudação só tem suportada atual é **inserir**. |
| **wcn** |Token de saudação do nome de coleção do espaço de trabalho está sendo emitido para. |
| **wid** |Token de saudação de ID do espaço de trabalho está sendo emitido para. |
| **rid** |Token de saudação do ID de relatório está sendo emitido para. |
| **nome de usuário** (opcional) |Usado com a RLS, isso é uma cadeia de caracteres que pode ajudar a identificar o usuário Olá ao aplicar regras RLS. |
| **funções** (opcional) |Uma cadeia de caracteres que contém a saudação funções tooselect ao aplicar regras de segurança em nível de linha. Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres. |
| **SCP** (opcional) |Uma cadeia de caracteres que contém escopos de permissões de saudação. Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres. |
| **exp** (opcional) |Indica o tempo de saudação na qual Olá token irá expirar. Elas devem ser transmitidas como carimbos de data/hora do Unix. |
| **nbf** (opcional) |Indica o tempo de saudação na qual Olá token inicia válido. Elas devem ser transmitidas como carimbos de data/hora do Unix. |

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

Há métodos disponíveis no hello SDKs que facilitam a criação de apptokens. Por exemplo, para .NET você pode examinar Olá [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.

Para Olá .NET SDK, consulte muito[escopos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Escopos

Ao usar tokens de inserção, talvez você queira toorestrict de uso dos recursos de saudação que concedem acesso ao. Por esse motivo, você pode gerar um token com as permissões no escopo.

Olá seguem escopos disponíveis de saudação para Power BI inserido.

|Escopo|Descrição|
|---|---|
|Dataset.Read|Fornece permissão tooread Olá especificado o conjunto de dados.|
|Dataset.Write|Fornece permissão toowrite toohello especificado conjunto de dados.|
|Dataset.ReadWrite|Fornece permissão tooread e gravação toohello especificado conjunto de dados.|
|Report.Read|Fornece permissão tooview Olá especificado de relatório.|
|Report.ReadWrite|Fornece a edição e a permissão tooview Olá relatório especificado.|
|Workspace.Report.Create|Fornece permissão toocreate um novo relatório em Olá especificado espaço de trabalho.|
|Workspace.Report.Copy|Fornece um relatório existente dentro de saudação especificado de permissão tooclone espaço de trabalho.|

Você pode fornecer vários escopos usando um espaço entre escopos hello como Olá seguinte.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Declarações necessárias - escopos**

SCP: scopesClaim {scopesClaim} pode ser uma cadeia de caracteres ou uma matriz de cadeias de caracteres, observando Olá permitido permissões tooworkspace recursos (relatório, conjunto de dados, etc.)

Um token decodificado, com escopos definidos, seria a seguir toohello semelhante.

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
|Criar um novo relatório com base em um conjunto de dados a (na memória) e salve o relatório de saudação.|Conjunto de dados|* Dataset.Read<br>* Workspace.Report.Create|
|Exibir e explorar/Editar (na memória) um relatório existente. Report.Read implica Dataset.Read. Isso não permitirá que permissões toosave edições.|Relatório|Report.Read|
|Editar e salvar um relatório existente.|Relatório|Report.ReadWrite|
|Salvar uma cópia de um relatório (Salvar como).|Relatório|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Como funciona o fluxo de saudação
1. Copie o aplicativo de tooyour de chaves de API hello. Você pode obter chaves de saudação em **Portal do Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. O token faz a asserção de uma declaração e tem uma data de validade.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. O token é assinado com uma chave de acesso de API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Usuário solicita tooview um relatório.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. O token é validado com uma chave de acesso de API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI inserido envia um relatório toouser.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Depois de **Power BI inserido** envia um usuário do relatório toohello, usuário Olá pode exibir o relatório de saudação em seu aplicativo personalizado. Por exemplo, se você importou Olá [exemplo PBIX de dados de vendas analisando](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicativo de web de exemplo hello teria esta aparência:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Consulte também

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Introdução ao exemplo do Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Cenários comuns do Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introdução ao Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Repositório de Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

