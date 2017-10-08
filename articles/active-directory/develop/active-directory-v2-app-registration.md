---
title: "um aplicativo com o ponto de extremidade de v 2.0 de saudação do AD do Azure usando o portal de saudação do aaaRegister | Microsoft Docs"
description: Como tooregister um aplicativo com a Microsoft para habilitar entrar e acessar o Microsoft services usando o ponto de extremidade do hello v 2.0
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Como tooregister um aplicativo com o ponto de extremidade do hello v 2.0
toobuild um aplicativo que aceita MSA & AD do Azure entrar, primeiro será necessário tooregister um aplicativo com a Microsoft.  Neste momento, você não ser capaz de toouse quaisquer aplicativos existentes que você possa ter com o AD do Azure ou MSA - você precisará toocreate uma nova marca.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Visite o portal de registro de aplicativo hello Microsoft
Coisas mais importantes primeiro - navegue muito[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Este é o novo portal de registro de aplicativos em que você pode gerenciar todos os seus aplicativos Microsoft.

Entrar com uma conta da Microsoft pessoal, profissional ou escolar.  Se você não tiver uma, inscreva-se para uma nova conta pessoal. Vá em frente, não vai demorar muito. Vamos aguardar aqui.

Pronto? Você deve agora estar olhando a lista de aplicativos da Microsoft, que provavelmente está vazia.  Vamos mudar isso.

Clique em **Adicionar um aplicativo**e dê um nome a ele.  portal de saudação atribuirá seu aplicativo uma Id globalmente exclusiva do aplicativo que você usará posteriormente no seu código.  Se seu aplicativo inclui um componente do lado do servidor que precisam de tokens de acesso para chamadas APIs (pense: Office, Azure ou sua própria API da web), você desejará toocreate um **segredo do aplicativo** aqui também.

Em seguida, adicione Olá plataformas que seu aplicativo usará.

* Para aplicativos baseados na Web, forneça um **URI de Redirecionamento** em que é possível enviar mensagens de entrada.
* Para aplicativos móveis, cópia inativo padrão Olá redirecione o uri criado automaticamente para você.

Opcionalmente, você pode personalizar Olá aparência de sua página de entrada hello perfil.  Certifique-se de que tooclick **salvar** antes de continuar.

> [!NOTE]
> Quando você cria um aplicativo usando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), aplicativo hello será registrado no locatário de saudação inicial da conta de saudação que você use toosign no portal de saudação.  Isso significa que não é possível registrar um aplicativo no seu locatário do Azure AD usando uma conta pessoal da Microsoft.  Se você explicitamente tooregister um aplicativo em um locatário específico, entre com uma conta que criou originalmente no locatário.
> 
> 

## <a name="build-a-quick-start-app"></a>Compilar um aplicativo de início rápido
Agora que você tem um aplicativo da Microsoft, poderá concluir um dos nossos tutoriais de início rápido da v2.0.  Aqui estão algumas recomendações:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

