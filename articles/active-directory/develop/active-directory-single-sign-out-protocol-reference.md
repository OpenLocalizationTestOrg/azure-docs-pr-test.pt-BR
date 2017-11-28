---
title: "aaaAzure único protocolo de logon Out SAML | Microsoft Docs"
description: "Este artigo descreve Olá único protocolo SAML de saída no Active Directory do Azure"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Protocolo SAML de Logout Único
Azure Active Directory (AD do Azure) oferece suporte a saudação SAML 2.0 web navegador único perfil de saída. Para toowork logout único corretamente, Olá **LogoutURL** para o aplicativo hello deve ser explicitamente registrado com o Azure AD durante o registro do aplicativo. AD do Azure usa os usuários do hello LogoutURL tooredirect depois que estão desconectados.

Este diagrama mostra o fluxo de trabalho de saudação do processo de logout único Olá AD do Azure.

![Fluxo de trabalho do Logout Único](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Olá serviço de nuvem envia um `LogoutRequest` mensagem tooAzure AD tooindicate que uma sessão foi encerrada. Olá, trecho a seguir mostra um exemplo `LogoutRequest` elemento.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Olá `LogoutRequest` tooAzure elemento enviado AD requer Olá seguintes atributos:

* `ID`: Isso identifica a solicitação de saída de hello. Olá valor `ID` não deve começar com um número. Olá a prática comum é tooappend **id** toohello representação de cadeia de caracteres de um GUID.
* `Version`: Defina Olá valor desse elemento muito**2.0**. Esse valor é obrigatório.
* `IssueInstant` : esta é uma cadeia de caracteres `DateTime` com um valor de UTC (Tempo Universal Coordenado) e [formato de ida e volta ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). O Azure AD espera um valor desse tipo, mas não é obrigatório.

### Emissor
Olá `Issuer` elemento em um `LogoutRequest` devem corresponder exatamente a um Olá **ServicePrincipalNames** no serviço de nuvem Olá no AD do Azure. Normalmente, isso é definido toohello **URI da ID do aplicativo** que é especificado durante o registro do aplicativo.

### NameID
Olá valor Olá `NameID` elemento deve corresponder exatamente ao Olá `NameID` saudação do usuário de que está sendo desconectado.

## LogoutResponse
Envios de AD do Azure uma `LogoutResponse` na resposta tooa `LogoutRequest` elemento. Olá, trecho a seguir mostra um exemplo de `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
O AD do Azure define Olá `ID`, `Version` e `IssueInstant` valores hello `LogoutResponse` elemento. Também define Olá `InResponseTo` valor do elemento toohello de saudação `ID` atributo de saudação `LogoutRequest` que induziu a resposta de saudação.

### Emissor
O AD do Azure define esse valor muito`https://login.microsoftonline.com/<TenantIdGUID>/` onde <TenantIdGUID> é ID de locatário de saudação do locatário de saudação do AD do Azure.

valor tooevaluate Olá Olá `Issuer` elemento, o valor do Olá Olá uso **URI da ID do aplicativo** fornecido durante o registro do aplicativo.

### Status
O AD do Azure usa Olá `StatusCode` elemento Olá `Status` sucesso de saudação do elemento tooindicate ou fracasso de saída. Quando Olá logout tentativa falhar, hello `StatusCode` elemento também pode conter mensagens de erro personalizadas.
