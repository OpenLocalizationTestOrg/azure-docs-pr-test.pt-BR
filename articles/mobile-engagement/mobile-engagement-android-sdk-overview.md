---
title: "Integração do SDK do Android para Azure Mobile Engagement"
description: Descreve como integrar o SDK do Azure Mobile Engagement em aplicativos Android
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
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="18740-103">Integração do Android SDK para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="18740-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18740-104">Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="18740-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="18740-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="18740-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="18740-106">iOS</span><span class="sxs-lookup"><span data-stu-id="18740-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="18740-107">Android</span><span class="sxs-lookup"><span data-stu-id="18740-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="18740-108">Este documento descreve todas as opções de integração e configuração disponíveis para o SDK do Azure Mobile Engagement para Android.</span><span class="sxs-lookup"><span data-stu-id="18740-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18740-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="18740-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="18740-110">Recursos avançados</span><span class="sxs-lookup"><span data-stu-id="18740-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="18740-111">Recursos de relatório</span><span class="sxs-lookup"><span data-stu-id="18740-111">Reporting Features</span></span>
<span data-ttu-id="18740-112">Você pode adicionar esses recursos:</span><span class="sxs-lookup"><span data-stu-id="18740-112">You can add these features:</span></span>

1. [<span data-ttu-id="18740-113">Opções de relatório avançadas</span><span class="sxs-lookup"><span data-stu-id="18740-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="18740-114">Opções de relatório de localização</span><span class="sxs-lookup"><span data-stu-id="18740-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="18740-115">Opções de configuração avançada</span><span class="sxs-lookup"><span data-stu-id="18740-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="18740-116">Notificações:</span><span class="sxs-lookup"><span data-stu-id="18740-116">Notifications:</span></span>
[<span data-ttu-id="18740-117">Como integrar o Reach (notificações) em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="18740-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="18740-118">GCM (Google Cloud Messaging): [como integrar o GCM com o Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="18740-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="18740-119">ADM (Amazon Device Messaging): [como integrar o ADM com o Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="18740-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="18740-120">Implementação do plano de marca:</span><span class="sxs-lookup"><span data-stu-id="18740-120">Tag plan implementation:</span></span>
[<span data-ttu-id="18740-121">Como usar a API de marcação avançada do Mobile Engagement em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="18740-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="18740-122">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="18740-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="18740-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="18740-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="18740-124">Corrigir uma falha que raramente poderia acontecer ao chamar `EngagementAgentUtils.isInDedicatedEngagementProcess`, que também é usado pela classe `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="18740-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="18740-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="18740-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="18740-126">Suporte para Android 8 (versões anteriores do SDK não funcionarão em Android 8).</span><span class="sxs-lookup"><span data-stu-id="18740-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="18740-127">Não há mais dependência da biblioteca de suporte.</span><span class="sxs-lookup"><span data-stu-id="18740-127">No more dependency on support library.</span></span>
* <span data-ttu-id="18740-128">Remover classe `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="18740-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="18740-129">Devido a [Limites de Execução em Segundo de Fundo](https://developer.android.com/preview/features/background.html) no Android 8, logs no segundo plano podem ser atrasados até que o usuário interaja com o dispositivo. Isso terá um impacto sobre Campanha de Push **Entregue** e estatísticas de **Notificação do sistema exibida** sendo atrasadas no caso de dispositivo estar em suspensão (a notificação ainda será exibida, tocará e vibrará em tempo real sem problemas).</span><span class="sxs-lookup"><span data-stu-id="18740-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="18740-130">Devido a [Limites de Local do Segundo Plano](https://developer.android.com/preview/features/background-location-limits.html), o local em tempo real em segundo plano não será atualizado com frequência no Android 8.</span><span class="sxs-lookup"><span data-stu-id="18740-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="18740-131">Para todas as versões, consulte as [notas de versão completas](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="18740-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="18740-132">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="18740-132">Upgrade procedures</span></span>
<span data-ttu-id="18740-133">Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, consulte os [Procedimentos de atualização](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="18740-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

