---
title: "Introdução ao servidor Web ASP.NET no Azure AD v2 – Configuração | Microsoft Docs"
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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="1dca6-103">Configurar o aplicativo Web ASP.NET com informações de registro do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1dca6-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="1dca6-104">Nesta etapa, você configurará seu projeto para usar o SSL e, em seguida, usará a URL do SSL para configurar as informações de registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1dca6-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="1dca6-105">Depois disso, adicione as informações de registro do aplicativo à sua solução por meio do *web.config*.</span><span class="sxs-lookup"><span data-stu-id="1dca6-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="1dca6-106">No Gerenciador de Soluções, selecione o projeto e examine a janela `Properties` (se uma janela Propriedades não for exibida, pressione F4)</span><span class="sxs-lookup"><span data-stu-id="1dca6-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="1dca6-107">Altere `SSL Enabled` para `True`</span><span class="sxs-lookup"><span data-stu-id="1dca6-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="1dca6-108">Copie o valor de `SSL URL` acima e cole-o no campo `Redirect URL` na parte superior desta página e, depois, clique em *Atualizar*:</span><span class="sxs-lookup"><span data-stu-id="1dca6-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="1dca6-109">![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="1dca6-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="1dca6-110">Adicione o seguinte ao arquivo `web.config` localizado na pasta da raiz, na seção `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="1dca6-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
