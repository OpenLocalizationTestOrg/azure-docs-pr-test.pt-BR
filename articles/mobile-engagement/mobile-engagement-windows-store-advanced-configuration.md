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
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Configuração avançada com o SDK do Engagement para aplicativos universais do Windows
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Este procedimento descreve como tooconfigure várias opções de configuração para aplicativos do Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Configuração avançada
### <a name="disable-automatic-crash-reporting"></a>Desabilitar o relatório de falhas automático
Você pode desabilitar o recurso de contrato de relatório de falha automático do hello. Assim, quando uma exceção sem tratamento ocorrer, o Engagement não fará nada.

> [!WARNING]
> Se você desabilitar esse recurso, quando ocorre uma falha sem tratamento em seu aplicativo, contrato não enviar falha Olá **AND** não fecha a sessão de saudação e trabalhos.
> 
> 

Falha automático toodisable, relatórios, personalizar a configuração dependendo da maneira Olá você declarado:

#### <a name="from-engagementconfigurationxml-file"></a>No arquivo `EngagementConfiguration.xml`
Definir o relatório de falhas muito`false` entre `<reportCrash>` e `</reportCrash>` marcas.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>No objeto `EngagementConfiguration` em tempo de execução
Definir toofalse de falha de relatório usando o objeto EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Desabilitar relatórios em tempo real
Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real. Se seu aplicativo relatórios logs com frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em uma base de tempo regulares. Isso é chamado de "modo de disparo contínuo".

toodo assim, chame o método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Olá argumento for um valor em **milissegundos**. Sempre que quiser que o log em tempo real do tooreactivate Olá, chame o método de saudação sem nenhum parâmetro, ou com valor de saudação 0.

Modo intermitente ligeiramente aumenta a vida útil da bateria Olá mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração são arredondados toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos). Recomendamos usar um limite de disparo contínuo até 30000 (30s). Logs salvos são itens de too300 limitado. Se o envio for muito longo, você poderá perder alguns logs.

> [!WARNING]
> limite de intermitência Olá não pode ser configurado tooa período menos de um segundo. Se você fizer isso, Olá SDK mostra um rastreamento com o erro hello e automaticamente redefine o valor padrão de toohello, zero segundos. Este gatilhos Olá SDK tooreport Olá fizer logon em tempo real.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
