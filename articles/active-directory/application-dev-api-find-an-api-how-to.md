---
title: "Como localizar uma API específica necessária para um aplicativo personalizado | Microsoft Docs"
description: "Como configurar as permissões que você precisa para acessar uma API em particular em seu aplicativo personalizado do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a>Como localizar uma API específica necessária para um aplicativo personalizado

O acesso às APIs exigem configuração de escopos de acesso e funções. Se você quiser expor suas APIs web do aplicativo de recursos para aplicativos cliente, precisará configurar escopos de acesso e funções da API. Se desejar que um aplicativo cliente acesse uma API web, você precisará configurar permissões para acessar a API no registro de aplicativo.

## <a name="configuring-a-resource-application-to-expose-web-apis"></a>Configurando um aplicativo de recurso para expor APIs Web

Quando você expõe sua API web, a API é exibida na lista **Selecionar uma API** ao adicionar permissões a um registro de aplicativo. Para adicionar escopos de acesso, siga as etapas descritas em [Adicionando escopos de acesso ao seu aplicativo de recurso](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-to-access-web-apis"></a>Configurando um aplicativo cliente para acessar APIs Web

Quando você adiciona permissões em seu registro de aplicativo, você pode **Adicionar acesso à API** para APIs web expostas. Para acessar APIs web, siga as etapas descritas em [Adicionar credenciais ou permissões para acessar APIs web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Próximas etapas

-   [Integrando aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Noções básicas sobre o manifesto de aplicativo do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


