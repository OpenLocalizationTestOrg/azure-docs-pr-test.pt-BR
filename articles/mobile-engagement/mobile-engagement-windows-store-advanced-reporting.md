---
title: "aaaWindows Universal avançado relatórios com o contrato de MobileApps"
description: Como tooIntegrate Azure Mobile Engagement com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="97877-103">Relatórios avançados com hello SDK de contrato de aplicativos Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="97877-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97877-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="97877-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="97877-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="97877-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="97877-106">iOS</span><span class="sxs-lookup"><span data-stu-id="97877-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="97877-107">Android</span><span class="sxs-lookup"><span data-stu-id="97877-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="97877-108">Este tópico descreve cenários de relatório adicionais em seu aplicativo universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="97877-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="97877-109">Esses cenários incluem opções que você pode escolher tooapply toohello aplicativo criado no hello [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="97877-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97877-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97877-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="97877-111">Antes de iniciar este tutorial, você deve completar Olá [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, o que é deliberadamente simples e direto.</span><span class="sxs-lookup"><span data-stu-id="97877-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="97877-112">Este tutorial aborda as opções adicionais que você pode escolher.</span><span class="sxs-lookup"><span data-stu-id="97877-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="97877-113">Como especificar a configuração do Engagement em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="97877-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="97877-114">configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto, que é onde ele foi especificado na Olá [Introdução](mobile-engagement-windows-store-dotnet-get-started.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="97877-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="97877-115">Mas você também pode especificá-lo em tempo de execução: você pode chamar hello seguinte método antes da inicialização de agente de contrato hello:</span><span class="sxs-lookup"><span data-stu-id="97877-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="97877-116">Método recomendado: sobrecarregar suas classes `Page`</span><span class="sxs-lookup"><span data-stu-id="97877-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="97877-117">tooactivate Olá relatórios de todos os logs de saudação exigidos pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, faça todas as suas `Page` subclasses herdam a saudação `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="97877-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="97877-118">Este é um exemplo de uma página de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97877-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="97877-119">Você pode fazer Olá igual para todas as páginas do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97877-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="97877-120">Arquivo de código-fonte C#</span><span class="sxs-lookup"><span data-stu-id="97877-120">C# Source file</span></span>
<span data-ttu-id="97877-121">Modifique o arquivo `.xaml.cs` de paginação:</span><span class="sxs-lookup"><span data-stu-id="97877-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="97877-122">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="97877-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="97877-123">Substituir `Page` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="97877-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="97877-124">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97877-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="97877-125">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97877-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="97877-126">Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="97877-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="97877-127">Caso contrário, a atividade de saudação não é informada (Olá `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="97877-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="97877-128">Arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="97877-128">XAML file</span></span>
<span data-ttu-id="97877-129">Modifique o arquivo `.xaml` de paginação:</span><span class="sxs-lookup"><span data-stu-id="97877-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="97877-130">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="97877-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="97877-131">Substituir `Page` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="97877-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="97877-132">**Sem o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97877-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="97877-133">**Com o Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97877-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="97877-134">Substituir o comportamento padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="97877-134">Override hello default behaviour</span></span>
<span data-ttu-id="97877-135">Por padrão, nome de classe de saudação da página de Olá será relatado como nome da atividade hello, com e sem extras.</span><span class="sxs-lookup"><span data-stu-id="97877-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="97877-136">Se a classe Olá usa Olá sufixo "Página", contrato remove.</span><span class="sxs-lookup"><span data-stu-id="97877-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="97877-137">comportamento do toooverride saudação padrão para nome hello, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="97877-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="97877-138">tooreport informações extras com sua atividade, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="97877-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="97877-139">Esses métodos são chamados de dentro de saudação `OnNavigatedTo` método da página.</span><span class="sxs-lookup"><span data-stu-id="97877-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="97877-140">Método alternativo: chame `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="97877-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="97877-141">Se você não pode ou não toooverload seu `Page` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent` métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="97877-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="97877-142">Recomendamos chamar `StartActivity` dentro de seu método `OnNavigatedTo` da sua Página.</span><span class="sxs-lookup"><span data-stu-id="97877-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="97877-143">Certifique-se de encerrar a sua sessão corretamente.</span><span class="sxs-lookup"><span data-stu-id="97877-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="97877-144">Olá SDK Universal do Windows chama automaticamente Olá `EndActivity` método quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="97877-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="97877-145">Portanto, é **altamente** recomendado Olá toocall `StartActivity` sempre que alterar a atividade de saudação do usuário Olá e muito**nunca** chamada hello `EndActivity` método.</span><span class="sxs-lookup"><span data-stu-id="97877-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="97877-146">Este método notifica o servidor de contrato de saudação que usuário Olá atual tiver saído aplicativo hello, que afeta todos os logs de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97877-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="97877-147">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="97877-147">Advanced reporting</span></span>
<span data-ttu-id="97877-148">Opcionalmente, convém eventos específicos de aplicativos de tooreport, erros e trabalhos, toodo assim, use Olá outros métodos encontrados no hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="97877-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="97877-149">Olá contrato de API permite o uso de recursos avançados do contrato de todos os.</span><span class="sxs-lookup"><span data-stu-id="97877-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="97877-150">Para obter mais informações, consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Windows Universal](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="97877-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

