---
title: "aaaAzure integração de Universal SDK do Mobile Engagement Windows | Microsoft Docs"
description: "Integração do SDK do Windows Universal para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Integração do SDK do Windows Universal para o Azure Mobile Engagement
Este documento descreve todas Olá integração e configuração de opções disponíveis para Olá SDK Universal do Windows Azure Mobile Engagement.

## <a name="prerequisites"></a>Pré-requisitos
Antes de iniciar este tutorial, você deve primeiro concluir nosso [tutorial de 15 minutos](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Recursos avançados
### <a name="reporting-features"></a>Recursos de relatório
Você pode adicionar esses recursos:

1. [Opções de relatório avançadas](mobile-engagement-windows-store-advanced-reporting.md)
2. [Opções de configuração avançada](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Notificações
[Como toointegrate alcance (notificações) em seu aplicativo Universal do Windows](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Implementação do plano de marca:
[Como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo Universal do Windows](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Notas de versão
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* Aprimoramentos de estabilidade.

Para versões anteriores, consulte Olá [concluir notas de versão](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Se você perdeu várias versões do SDK do hello, você pode ter toofollow vários procedimentos. Consulte Olá completa [procedimentos de atualização](mobile-engagement-windows-store-upgrade-procedure.md). Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.

### <a name="from-330-too340"></a>De 3.3.0 too3.4.0
#### <a name="test-logs"></a>Logs de teste
Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas. toocustomize, atualizar a propriedade de saudação `EngagementAgent.Instance.TestLogEnabled` tooone de valores de saudação disponíveis de saudação `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Recursos
sobreposição de alcance Olá foi aprimorada. Ele faz parte dos recursos de pacote do NuGet do SDK hello.

Durante a atualização toohello nova versão de hello SDK, você pode escolher que se deseja tookeep os arquivos existentes do hello sobreposição de pasta de seus recursos ou não:

* Se sobreposição anterior hello está funcionando para você, ou você estiver integrando Olá `WebView` elementos manualmente, em seguida, você pode decidir tookeep sair de seus arquivos, continuará a funcionar.
* tooupdate toohello nova sobreposição, substituir Olá todo `overlay` pasta de seus recursos com hello um novo pacote do SDK de saudação (aplicativos UWP: após a atualização de hello, você pode obter nova pasta de sobreposição de saudação do % USERPROFILE %\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Usando a sobreposição de novo Olá substitui as personalizações feitas na versão anterior do hello.
> 
> 

### <a name="upgrade-from-older-versions"></a>Atualizar de versões anteriores
Consulte [Procedimentos de atualização](mobile-engagement-windows-store-upgrade-procedure.md)

