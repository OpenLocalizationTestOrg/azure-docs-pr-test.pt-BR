---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - Config | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="ed149-103">Configurar seu aplicativo da Web ASP.NET com informações de registro do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ed149-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="ed149-104">Nesta etapa, você irá configurar seu projeto toouse SSL e use Olá SSL URL tooconfigure informações de registro do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed149-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="ed149-105">Depois disso, adicionar o aplicativo hello' solução de tooyour de informações de registro por meio de *Web. config*.</span><span class="sxs-lookup"><span data-stu-id="ed149-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="ed149-106">No Solution Explorer, selecione o projeto hello e observe Olá `Properties` janela (se você não vir uma janela de propriedades, pressione F4)</span><span class="sxs-lookup"><span data-stu-id="ed149-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="ed149-107">Alterar `SSL Enabled` muito`True`</span><span class="sxs-lookup"><span data-stu-id="ed149-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="ed149-108">Copie o valor de saudação do `SSL URL` acima e cole-o no hello `Redirect URL` campo na parte superior da saudação desta página, clique em *atualização*:</span><span class="sxs-lookup"><span data-stu-id="ed149-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="ed149-109">![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="ed149-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="ed149-110">Adicione a seguinte Olá em `web.config` arquivo localizado na pasta da raiz, na seção `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="ed149-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
