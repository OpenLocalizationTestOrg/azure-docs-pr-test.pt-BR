---
title: "aplicativo personalizado aaaHow toogrant permissões tooa | Microsoft Docs"
description: "Como toogrant permissões tooyour personalizado usando o aplicativo hello portal do AD do Azure ou um parâmetro de URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Como toogrant permissões tooa personalizado aplicativo

Se quiser toogrant consentimento preventivamente no seu aplicativo ou em execução em um erro se você não tiver consentido tooan aplicativo, tente essas etapas abaixo.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Como tooperform consentimento do administrador para seu aplicativo

Isso tem o efeito de saudação de concessão de autorização toohello aplicativo para todos os usuários em sua organização.

1. Navegue toohello **registros do aplicativo** folha como uma **administrador global**, em seguida, selecione aplicativo hello.

2. Selecione **permissões necessárias**e finalmente chegar Olá **conceder permissões** botão na parte superior de saudação da folha de saudação.

Como alternativa, você pode construir uma solicitação muito*login.microsoftonline.com* com suas configurações de aplicativo e acrescente em *& prompt = admin\_consentimento*. Depois de entrar com credenciais de administrador, Olá aplicativo recebeu consentimento para todos os usuários.

## <a name="how-tooforce-user-consent-for-your-application"></a>Como tooforce consentimento do usuário para seu aplicativo

* Acrescentar para solicitações de autenticação *& prompt = consentimento* que exigir que os usuários finais tooconsent cada vez que eles se autenticam.

## <a name="next-steps"></a>Próximas etapas

[TooAzureAD consentimento e integração de aplicativos](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Consentimento e permissão para aplicativos convergidos do AzureAD v2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[StackOverflow do AzureAD](http://stackoverflow.com/questions/tagged/azure-active-directory)
