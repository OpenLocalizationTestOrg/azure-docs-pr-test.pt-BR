---
title: "Visão geral do SDK Mobile Engagement Windows Phone Silverlight do aaaAzure | Microsoft Docs"
description: "Visão geral da saudação SDK do Windows Phone Silverlight para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Visão geral do SDK do Windows Phone Silverlight para o Azure Mobile Engagement
Comece aqui detalhes de saudação tooget como toointegrate Azure Mobile Engagement em um Windows Phone Silverlight App. Se você quiser toogive ele tentar primeiro, verifique se você concluir nosso [tutorial de 15 minutos](mobile-engagement-windows-phone-get-started.md).

Clique em toosee Olá [conteúdo do SDK](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Procedimentos de integração
1. Comece aqui: [como toointegrate Mobile Engagement em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Para notificações: [como toointegrate alcance (notificações) em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Marca o plano de implementação: [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo do Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Notas de versão
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Parte da saudação *MicrosoftAzure.MobileEngagement* pacote Nuget **v3.4.1**

* Aprimoramentos de estabilidade.

Para a versão anterior, consulte Olá [concluir notas de versão](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação. Consulte Olá completa [procedimentos de atualização](mobile-engagement-windows-phone-upgrade-procedure.md). Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.

### <a name="from-200-too330"></a>De 2.0.0 too3.3.0
#### <a name="test-logs"></a>Logs de teste
Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas. toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Atualizar de versões anteriores
Consulte [Procedimentos de atualização](mobile-engagement-windows-phone-upgrade-procedure.md)

