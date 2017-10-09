---
title: "aaaAndroid integração SDK para o Azure Mobile Engagement"
description: Descreve como toointegrate SDK do Azure Mobile Engagement em aplicativos Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="93d1e-103">Integração do SDK do Android para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="93d1e-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93d1e-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="93d1e-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="93d1e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="93d1e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="93d1e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="93d1e-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="93d1e-107">Android</span><span class="sxs-lookup"><span data-stu-id="93d1e-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="93d1e-108">Este documento descreve todas as Olá integração e configuração de opções disponíveis para o Android SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="93d1e-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d1e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93d1e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="93d1e-110">Recursos avançados</span><span class="sxs-lookup"><span data-stu-id="93d1e-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="93d1e-111">Recursos de relatório</span><span class="sxs-lookup"><span data-stu-id="93d1e-111">Reporting Features</span></span>
<span data-ttu-id="93d1e-112">Você pode adicionar esses recursos:</span><span class="sxs-lookup"><span data-stu-id="93d1e-112">You can add these features:</span></span>

1. [<span data-ttu-id="93d1e-113">Opções de relatório avançadas</span><span class="sxs-lookup"><span data-stu-id="93d1e-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="93d1e-114">Opções de relatório de localização</span><span class="sxs-lookup"><span data-stu-id="93d1e-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="93d1e-115">Opções de configuração avançada</span><span class="sxs-lookup"><span data-stu-id="93d1e-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="93d1e-116">Notificações:</span><span class="sxs-lookup"><span data-stu-id="93d1e-116">Notifications:</span></span>
[<span data-ttu-id="93d1e-117">Como toointegrate alcance (notificações) em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="93d1e-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="93d1e-118">Google Cloud Messaging (GCM): [como tooIntegrate GCM com o Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="93d1e-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="93d1e-119">Mensagens de dispositivo da Amazon (ADM): [como tooIntegrate ADM com o Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="93d1e-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="93d1e-120">Implementação do plano de marca:</span><span class="sxs-lookup"><span data-stu-id="93d1e-120">Tag plan implementation:</span></span>
[<span data-ttu-id="93d1e-121">Como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="93d1e-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="93d1e-122">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="93d1e-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="93d1e-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="93d1e-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="93d1e-124">Corrigir uma falha que raramente pode acontecer ao chamar `EngagementAgentUtils.isInDedicatedEngagementProcess`, que também é usado por Olá `EngagementApplication` classe.</span><span class="sxs-lookup"><span data-stu-id="93d1e-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="93d1e-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="93d1e-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="93d1e-126">Suporte de 8 Android (versões anteriores do hello SDK não funcionarão no Android 8).</span><span class="sxs-lookup"><span data-stu-id="93d1e-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="93d1e-127">Não há mais dependência da biblioteca de suporte.</span><span class="sxs-lookup"><span data-stu-id="93d1e-127">No more dependency on support library.</span></span>
* <span data-ttu-id="93d1e-128">Remover classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="93d1e-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="93d1e-129">Vencimento muito[limites de execução do plano de fundo](https://developer.android.com/preview/features/background.html) no Android 8, logs no plano de fundo podem ser atrasados até que o usuário Olá interage com o dispositivo de saudação, isso terá um impacto na campanha de Push **entregues** e **Notificação do sistema exibida** estatísticas atrasadas se dispositivo Olá foi suspenso (Olá notificação ainda será exibida, será de anel e Vibrar em tempo real sem problemas).</span><span class="sxs-lookup"><span data-stu-id="93d1e-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="93d1e-130">Vencimento muito[limites de local do plano de fundo](https://developer.android.com/preview/features/background-location-limits.html), local Olá em tempo real no plano de fundo não será atualizada com frequência no Android 8.</span><span class="sxs-lookup"><span data-stu-id="93d1e-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="93d1e-131">Para todas as versões, consulte Olá [concluir notas de versão](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="93d1e-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="93d1e-132">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="93d1e-132">Upgrade procedures</span></span>
<span data-ttu-id="93d1e-133">Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, consulte os [Procedimentos de atualização](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="93d1e-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

