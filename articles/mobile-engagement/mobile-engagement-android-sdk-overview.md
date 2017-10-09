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
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Integração do SDK do Android para Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Este documento descreve todas as Olá integração e configuração de opções disponíveis para o Android SDK do Azure Mobile Engagement.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Recursos avançados
### <a name="reporting-features"></a>Recursos de relatório
Você pode adicionar esses recursos:

1. [Opções de relatório avançadas](mobile-engagement-android-advanced-reporting.md)
2. [Opções de relatório de localização](mobile-engagement-android-location-reporting.md)
3. [Opções de configuração avançada](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Notificações:
[Como toointegrate alcance (notificações) em seu aplicativo Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [como tooIntegrate GCM com o Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Mensagens de dispositivo da Amazon (ADM): [como tooIntegrate ADM com o Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Implementação do plano de marca:
[Como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Android](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Notas de versão

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Corrigir uma falha que raramente pode acontecer ao chamar `EngagementAgentUtils.isInDedicatedEngagementProcess`, que também é usado por Olá `EngagementApplication` classe.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Suporte de 8 Android (versões anteriores do hello SDK não funcionarão no Android 8).
* Não há mais dependência da biblioteca de suporte.
* Remover classe `EngagementFragmentActivity`.
* Vencimento muito[limites de execução do plano de fundo](https://developer.android.com/preview/features/background.html) no Android 8, logs no plano de fundo podem ser atrasados até que o usuário Olá interage com o dispositivo de saudação, isso terá um impacto na campanha de Push **entregues** e **Notificação do sistema exibida** estatísticas atrasadas se dispositivo Olá foi suspenso (Olá notificação ainda será exibida, será de anel e Vibrar em tempo real sem problemas).
* Vencimento muito[limites de local do plano de fundo](https://developer.android.com/preview/features/background-location-limits.html), local Olá em tempo real no plano de fundo não será atualizada com frequência no Android 8.

Para todas as versões, consulte Olá [concluir notas de versão](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, consulte os [Procedimentos de atualização](mobile-engagement-android-upgrade-procedure.md).

