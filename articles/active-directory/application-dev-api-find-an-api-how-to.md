---
title: "aaaHow toofind uma API específica necessária para um aplicativo personalizado | Microsoft Docs"
description: "Como permissões de saudação tooconfigure necessário tooaccess uma API em particular em personalizados desenvolvidos aplicativo AD do Azure"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Como toofind uma API específica necessária para um aplicativo personalizado

Acesso tooAPIs exigem configuração de funções e escopos de acesso. Se você quiser tooexpose seus aplicativos de tooclient APIs do recurso aplicativo da web, você precisa tooconfigure acesso escopos e funções para Olá API. Se você quiser que um aplicativo de cliente tooaccess uma API da web, você precisa tooconfigure permissões tooaccess Olá API no registro do aplicativo hello.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configurando um recurso aplicativo tooexpose APIs da web

Quando você expõe a API da web, exibido no Olá Olá API **selecionar uma API** ao adicionar um registro de aplicativo tooan permissões de lista. tooadd escopos de acesso, execute as etapas de saudação descritas em [adicionar acesso escopos do aplicativo de recurso tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurando um cliente aplicativo tooaccess APIs da web

Quando você adiciona um registro de aplicativo tooyour permissões, você pode **adicionar acesso à API** tooexposed APIs da web. tooaccess APIs da web, siga etapas Olá descritas em [adicionar tooaccess credenciais ou permissões de APIs da web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Próximas etapas

-   [Integrando aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Noções básicas sobre o manifesto de aplicativo do Active Directory do Azure Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


