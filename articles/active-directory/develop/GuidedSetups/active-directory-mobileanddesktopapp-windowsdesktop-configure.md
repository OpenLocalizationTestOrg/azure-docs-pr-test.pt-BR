---
title: "aaaAzure AD v2 Windows Desktop Introdução - Config | Microsoft Docs"
description: "Como um aplicativo .NET da Área de Trabalho do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto de extremidade do Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar um aplicativo (Expresso)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Insira um nome para o aplicativo e seu email
3.  Verifique se a opção Olá para a instalação interativa está marcada
4.  Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo
2. Insira um nome para o aplicativo e seu email 
3. Verifique se a opção Olá para a instalação interativa está desmarcada
4. Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em Salvar
5. Copiar Olá GUID na ID de aplicativo, volte tooVisual Studio, abra `App.xaml.cs` e substitua `your_client_id_here` com hello ID de aplicativo que você acabou de registrar:

```csharp
private static string ClientId = "your_application_id_here";
```
