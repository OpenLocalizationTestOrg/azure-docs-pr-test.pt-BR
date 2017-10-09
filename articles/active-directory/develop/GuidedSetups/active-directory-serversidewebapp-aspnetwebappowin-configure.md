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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="396eb-103">Criar um aplicativo (Expresso)</span><span class="sxs-lookup"><span data-stu-id="396eb-103">Create an application (Express)</span></span>
<span data-ttu-id="396eb-104">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="396eb-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="396eb-105">Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="396eb-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="396eb-106">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="396eb-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="396eb-107">Verifique se a opção Olá para a instalação interativa está marcada</span><span class="sxs-lookup"><span data-stu-id="396eb-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="396eb-108">Siga as instruções de saudação tooadd um aplicativo de tooyour URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="396eb-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="396eb-109">Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)</span><span class="sxs-lookup"><span data-stu-id="396eb-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="396eb-110">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="396eb-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="396eb-111">Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo</span><span class="sxs-lookup"><span data-stu-id="396eb-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="396eb-112">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="396eb-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="396eb-113">Verifique se a opção Olá para a instalação interativa está desmarcada</span><span class="sxs-lookup"><span data-stu-id="396eb-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="396eb-114">Clique em `Add Platform` e selecione `Web`</span><span class="sxs-lookup"><span data-stu-id="396eb-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="396eb-115">Voltar tooVisual Studio e, no Gerenciador de soluções, selecione o projeto de saudação e examinar a janela de propriedades de saudação (se você não vir uma janela de propriedades, pressione F4)</span><span class="sxs-lookup"><span data-stu-id="396eb-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="396eb-116">Alterar também o SSL habilitado`True`</span><span class="sxs-lookup"><span data-stu-id="396eb-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="396eb-117">Copiar URL de SSL da saudação e adicionar esta lista de toohello URL de URLs de redirecionamento lista do Portal de registro Olá de URLs de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="396eb-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="396eb-119">Adicione a seguinte Olá em `web.config` localizado na pasta raiz de saudação na seção Olá `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="396eb-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="396eb-120">Substituir `ClientId` com hello Id de aplicativo que você acabou de registrar</span><span class="sxs-lookup"><span data-stu-id="396eb-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="396eb-121">Substituir `redirectUri` com hello SSL URL de seu projeto</span><span class="sxs-lookup"><span data-stu-id="396eb-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
