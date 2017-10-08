---
title: "APIs de aaaSecure usando a autenticação de certificado de cliente no gerenciamento de API - gerenciamento de API do Azure | Microsoft Docs"
description: Saiba como toosecure acessar tooAPIs usando certificados de cliente
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Como toosecure APIs usando o cliente de certificado autenticação no gerenciamento de API

Gerenciamento de API fornece Olá recurso toosecure acesso tooAPIs (ou seja, cliente tooAPI gerenciamento) usando certificados de cliente. No momento, você pode verificar a impressão digital de saudação de um certificado de cliente com um valor desejado. Você também pode verificar a impressão digital de saudação em certificados existentes carregado tooAPI gerenciamento.  

Para obter informações sobre como proteger o acesso toohello serviço de back-end de uma API usando certificados de cliente (ou seja, gerenciamento de API tooback-end), consulte [como toosecure serviços de back-end usando o cliente de autenticação de certificado](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Verificando a data de expiração de saudação

Abaixo políticas pode ser configurado toocheck se Olá certificado expirou:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Verificação de assunto e emissor Olá

Abaixo políticas pode ser configurado toocheck Olá emissor e assunto de um certificado de cliente:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Verificando a impressão digital de saudação

Abaixo políticas pode ser configurado toocheck impressão digital de saudação de um certificado de cliente:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>Verificar uma impressão digital em certificados carregados tooAPI gerenciamento

Olá exemplo a seguir mostra como a impressão digital de saudação toocheck de um certificado de cliente em relação a certificados carregado tooAPI gerenciamento: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Próxima etapa

*  [Como toosecure serviços de back-end usando o cliente de autenticação de certificado](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Como os certificados tooupload](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

