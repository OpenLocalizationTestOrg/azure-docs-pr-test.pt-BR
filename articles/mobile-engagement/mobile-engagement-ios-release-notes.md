---
title: "aaaAzure iOS Mobile Engagement notas de versão do SDK | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="07148-103">Notas de versão do SDK do iOS no Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="07148-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="07148-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="07148-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="07148-105">Corrigidas as notificações apagadas na tela de fundo.</span><span class="sxs-lookup"><span data-stu-id="07148-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="07148-106">Corrigidos os avisos no XCode 9 sobre as APIs não chamadas na fila principal.</span><span class="sxs-lookup"><span data-stu-id="07148-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="07148-107">Corrigida uma perda de memória em pesquisas Reach.</span><span class="sxs-lookup"><span data-stu-id="07148-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="07148-108">Removido o suporte para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="07148-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="07148-109">A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos o iOS 7.</span><span class="sxs-lookup"><span data-stu-id="07148-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="07148-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="07148-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="07148-111">Melhor entrega de log em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="07148-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="07148-112">4.0.0 (12/09/2016)</span><span class="sxs-lookup"><span data-stu-id="07148-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="07148-113">Notificação fixa não acionada em dispositivos com iOS 10.</span><span class="sxs-lookup"><span data-stu-id="07148-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="07148-114">Substituir o XCode 7.</span><span class="sxs-lookup"><span data-stu-id="07148-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="07148-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="07148-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="07148-116">Agregação fixa entre logs técnicos e outros logs.</span><span class="sxs-lookup"><span data-stu-id="07148-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="07148-117">3.2.3 (07/06/2016)</span><span class="sxs-lookup"><span data-stu-id="07148-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="07148-118">Bug Olá fixa onde comentários de entrega não é relatado quando o aplicativo está no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07148-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="07148-119">Otimização Olá envio de logs técnicas.</span><span class="sxs-lookup"><span data-stu-id="07148-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="07148-120">3.2.2 (07/04/2016)</span><span class="sxs-lookup"><span data-stu-id="07148-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="07148-121">Correção do bug no cancelamento de solicitação HTTP que, às vezes, leva toocrash.</span><span class="sxs-lookup"><span data-stu-id="07148-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="07148-122">3.2.1 (11/12/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="07148-123">Atraso de saudação fixo quando uma nova instância do aplicativo é disparada por uma notificação com links profundos</span><span class="sxs-lookup"><span data-stu-id="07148-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="07148-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="07148-125">Habilitado Bitcode em Olá SDK toomake ele funciona com **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="07148-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="07148-126">Bugs corrigidos relacionadas a notificações de aplicativo tooin.</span><span class="sxs-lookup"><span data-stu-id="07148-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="07148-127">As notificações no aplicativo de saudação feitas mais confiável no caso de bateria fraca e outros esses cenários.</span><span class="sxs-lookup"><span data-stu-id="07148-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="07148-128">Removidos logs do console extra gerados pela biblioteca de terceiros.</span><span class="sxs-lookup"><span data-stu-id="07148-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="07148-129">3.1.0 (26/08/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="07148-130">Corrija o bug de compatibilidade do iOS 9 com uma biblioteca de terceiros.</span><span class="sxs-lookup"><span data-stu-id="07148-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="07148-131">Ele estava causando falhas ao enviar resultados de pesquisas, informações do aplicativo ou dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="07148-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="07148-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="07148-133">O Mobile Engagement usa notificações por push silenciosas.</span><span class="sxs-lookup"><span data-stu-id="07148-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="07148-134">Suporte removido para iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="07148-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="07148-135">A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos 6 do iOS.</span><span class="sxs-lookup"><span data-stu-id="07148-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="07148-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="07148-137">id do dispositivo do Mobile Engagement Olá para dispositivos < iOS 6 agora se baseia em um GUID gerado no momento da instalação.</span><span class="sxs-lookup"><span data-stu-id="07148-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="07148-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="07148-139">Compatibilidade com Swift adicionada.</span><span class="sxs-lookup"><span data-stu-id="07148-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="07148-140">Ao clicar em uma notificação, ação Olá que URL agora é executada à direita depois que o aplicativo hello é aberto.</span><span class="sxs-lookup"><span data-stu-id="07148-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="07148-141">Arquivo de cabeçalho ausente adicionado no pacote SDK.</span><span class="sxs-lookup"><span data-stu-id="07148-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="07148-142">Corrigido um problema quando Relator de travamento do Mobile Engagement Olá foi desabilitado.</span><span class="sxs-lookup"><span data-stu-id="07148-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="07148-143">2.0.0 (17/02/2015)</span><span class="sxs-lookup"><span data-stu-id="07148-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="07148-144">Versão Inicial do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="07148-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="07148-145">A configuração appId/sdkKey é substituída por uma configuração de cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="07148-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="07148-146">Removido toosend de API e receber mensagens XMPP arbitrárias de entidades XMPP arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="07148-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="07148-147">Removido toosend de API e receber mensagens entre dispositivos.</span><span class="sxs-lookup"><span data-stu-id="07148-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="07148-148">Aprimoramentos de segurança.</span><span class="sxs-lookup"><span data-stu-id="07148-148">Security improvements.</span></span>
* <span data-ttu-id="07148-149">Controle SmartAd removido.</span><span class="sxs-lookup"><span data-stu-id="07148-149">SmartAd tracking removed.</span></span>
