---
title: "aaaAdvanced configuração para Universal aplicativos contrato SDK do Windows"
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
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="97f80-103">Configuração avançada com o SDK do Engagement para aplicativos universais do Windows</span><span class="sxs-lookup"><span data-stu-id="97f80-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97f80-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="97f80-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="97f80-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="97f80-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="97f80-106">iOS</span><span class="sxs-lookup"><span data-stu-id="97f80-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="97f80-107">Android</span><span class="sxs-lookup"><span data-stu-id="97f80-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="97f80-108">Este procedimento descreve como tooconfigure várias opções de configuração para aplicativos do Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="97f80-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97f80-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97f80-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="97f80-110">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="97f80-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="97f80-111">Desabilitar o relatório de falhas automático</span><span class="sxs-lookup"><span data-stu-id="97f80-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="97f80-112">Você pode desabilitar o recurso de contrato de relatório de falha automático do hello.</span><span class="sxs-lookup"><span data-stu-id="97f80-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="97f80-113">Assim, quando uma exceção sem tratamento ocorrer, o Engagement não fará nada.</span><span class="sxs-lookup"><span data-stu-id="97f80-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="97f80-114">Se você desabilitar esse recurso, quando ocorre uma falha sem tratamento em seu aplicativo, contrato não enviar falha Olá **AND** não fecha a sessão de saudação e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="97f80-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="97f80-115">Falha automático toodisable, relatórios, personalizar a configuração dependendo da maneira Olá você declarado:</span><span class="sxs-lookup"><span data-stu-id="97f80-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="97f80-116">No arquivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="97f80-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="97f80-117">Definir o relatório de falhas muito`false` entre `<reportCrash>` e `</reportCrash>` marcas.</span><span class="sxs-lookup"><span data-stu-id="97f80-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="97f80-118">No objeto `EngagementConfiguration` em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="97f80-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="97f80-119">Definir toofalse de falha de relatório usando o objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="97f80-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="97f80-120">Desabilitar relatórios em tempo real</span><span class="sxs-lookup"><span data-stu-id="97f80-120">Disable real time reporting</span></span>
<span data-ttu-id="97f80-121">Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real.</span><span class="sxs-lookup"><span data-stu-id="97f80-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="97f80-122">Se seu aplicativo relatórios logs com frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em uma base de tempo regulares.</span><span class="sxs-lookup"><span data-stu-id="97f80-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="97f80-123">Isso é chamado de "modo de disparo contínuo".</span><span class="sxs-lookup"><span data-stu-id="97f80-123">This is called “burst mode”.</span></span>

<span data-ttu-id="97f80-124">toodo assim, chame o método hello:</span><span class="sxs-lookup"><span data-stu-id="97f80-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="97f80-125">Olá argumento for um valor em **milissegundos**.</span><span class="sxs-lookup"><span data-stu-id="97f80-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="97f80-126">Sempre que quiser que o log em tempo real do tooreactivate Olá, chame o método de saudação sem nenhum parâmetro, ou com valor de saudação 0.</span><span class="sxs-lookup"><span data-stu-id="97f80-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="97f80-127">Modo intermitente ligeiramente aumenta a vida útil da bateria Olá mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração são arredondados toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos).</span><span class="sxs-lookup"><span data-stu-id="97f80-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="97f80-128">Recomendamos usar um limite de disparo contínuo até 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="97f80-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="97f80-129">Logs salvos são itens de too300 limitado.</span><span class="sxs-lookup"><span data-stu-id="97f80-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="97f80-130">Se o envio for muito longo, você poderá perder alguns logs.</span><span class="sxs-lookup"><span data-stu-id="97f80-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="97f80-131">limite de intermitência Olá não pode ser configurado tooa período menos de um segundo.</span><span class="sxs-lookup"><span data-stu-id="97f80-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="97f80-132">Se você fizer isso, Olá SDK mostra um rastreamento com o erro hello e automaticamente redefine o valor padrão de toohello, zero segundos.</span><span class="sxs-lookup"><span data-stu-id="97f80-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="97f80-133">Este gatilhos Olá SDK tooreport Olá fizer logon em tempo real.</span><span class="sxs-lookup"><span data-stu-id="97f80-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
