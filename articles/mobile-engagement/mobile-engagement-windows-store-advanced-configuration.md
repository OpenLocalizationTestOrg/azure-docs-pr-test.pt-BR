---
title: "Configuração avançada com o SDK do Engagement para aplicativos universais do Windows"
description: "Opções de configuração avançadas para o Azure Mobile Engagement com os aplicativos universais do Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="d869e-103">Configuração avançada com o SDK do Engagement para aplicativos universais do Windows</span><span class="sxs-lookup"><span data-stu-id="d869e-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d869e-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="d869e-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="d869e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d869e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d869e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d869e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d869e-107">Android</span><span class="sxs-lookup"><span data-stu-id="d869e-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="d869e-108">Este procedimento descreve como definir várias opções de configuração para aplicativos Azure Mobile Engagement do Android.</span><span class="sxs-lookup"><span data-stu-id="d869e-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d869e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d869e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="d869e-110">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="d869e-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="d869e-111">Desabilitar o relatório de falhas automático</span><span class="sxs-lookup"><span data-stu-id="d869e-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="d869e-112">Você pode desabilitar a recurso relatório de falhas automático do Engagement.</span><span class="sxs-lookup"><span data-stu-id="d869e-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="d869e-113">Assim, quando uma exceção sem tratamento ocorrer, o Engagement não fará nada.</span><span class="sxs-lookup"><span data-stu-id="d869e-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="d869e-114">Se você desabilitar esse recurso, quando uma falha sem tratamento ocorrer em seu aplicativo, o Engagement não enviará a falha **E** não fechará a sessão e os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d869e-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="d869e-115">Para desabilitar o relatório de falhas automático, personalize a configuração dependendo de como você o tiver declarado:</span><span class="sxs-lookup"><span data-stu-id="d869e-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="d869e-116">No arquivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="d869e-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="d869e-117">Defina a falha do relatório para `false` entre as marcas `<reportCrash>` e `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="d869e-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="d869e-118">No objeto `EngagementConfiguration` em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="d869e-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="d869e-119">Defina a falha do relatório como false usando o objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d869e-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="d869e-120">Desabilitar relatórios em tempo real</span><span class="sxs-lookup"><span data-stu-id="d869e-120">Disable real time reporting</span></span>
<span data-ttu-id="d869e-121">Por padrão, o serviço Engagement reporta logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d869e-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="d869e-122">Se seu aplicativo reporta logs com muita frequência, é melhor armazenar os logs em buffer e relatá-los todos de uma vez em uma base de tempo normal.</span><span class="sxs-lookup"><span data-stu-id="d869e-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="d869e-123">Isso é chamado de "modo de disparo contínuo".</span><span class="sxs-lookup"><span data-stu-id="d869e-123">This is called “burst mode”.</span></span>

<span data-ttu-id="d869e-124">Para fazer isso, chame o método:</span><span class="sxs-lookup"><span data-stu-id="d869e-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="d869e-125">O argumento é um valor em **milissegundos**.</span><span class="sxs-lookup"><span data-stu-id="d869e-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="d869e-126">Sempre que você quiser reativar o registro em log em tempo real, chame o método sem nenhum parâmetro, ou com o valor 0.</span><span class="sxs-lookup"><span data-stu-id="d869e-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="d869e-127">O modo de disparo contínuo aumenta ligeiramente a vida útil da bateria, mas tem um impacto no Monitor do Engagement: a duração de todas as sessões e trabalhos será arredondada para o limite de intermitência (portanto, as sessões e trabalhos mais curtos do que o limite de intermitência podem não estar visíveis).</span><span class="sxs-lookup"><span data-stu-id="d869e-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="d869e-128">Recomendamos usar um limite de disparo contínuo até 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="d869e-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="d869e-129">Logs salvos são limitados a 300 itens.</span><span class="sxs-lookup"><span data-stu-id="d869e-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="d869e-130">Se o envio for muito longo, você poderá perder alguns logs.</span><span class="sxs-lookup"><span data-stu-id="d869e-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="d869e-131">O limite de disparo contínuo não pode ser configurado com um período inferior a um segundo.</span><span class="sxs-lookup"><span data-stu-id="d869e-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="d869e-132">Se você fizer isso, o SDK mostrará um rastreamento com o erro e será redefinido automaticamente como o valor padrão, zero segundos.</span><span class="sxs-lookup"><span data-stu-id="d869e-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="d869e-133">Isso disparará o SDK para relatar os logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d869e-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
