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
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Notas de versão do SDK do iOS no Azure Mobile Engagement

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Corrigidas as notificações apagadas na tela de fundo.
* Corrigidos os avisos no XCode 9 sobre as APIs não chamadas na fila principal.
* Corrigida uma perda de memória em pesquisas Reach.
* Removido o suporte para iOS 6.X. A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos o iOS 7.

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* Melhor entrega de log em segundo plano.

## <a name="400-09122016"></a>4.0.0 (12/09/2016)
* Notificação fixa não acionada em dispositivos com iOS 10.
* Substituir o XCode 7.

## <a name="324-06302016"></a>3.2.4 (30/06/2016)
* Agregação fixa entre logs técnicos e outros logs.

## <a name="323-06072016"></a>3.2.3 (07/06/2016)
* Bug Olá fixa onde comentários de entrega não é relatado quando o aplicativo está no plano de fundo de saudação.
* Otimização Olá envio de logs técnicas.

## <a name="322-04072016"></a>3.2.2 (07/04/2016)
* Correção do bug no cancelamento de solicitação HTTP que, às vezes, leva toocrash.

## <a name="321-12112015"></a>3.2.1 (11/12/2015)
* Atraso de saudação fixo quando uma nova instância do aplicativo é disparada por uma notificação com links profundos

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Habilitado Bitcode em Olá SDK toomake ele funciona com **Xcode 7**.
* Bugs corrigidos relacionadas a notificações de aplicativo tooin.
* As notificações no aplicativo de saudação feitas mais confiável no caso de bateria fraca e outros esses cenários.
* Removidos logs do console extra gerados pela biblioteca de terceiros.

## <a name="310-08262015"></a>3.1.0 (26/08/2015)
* Corrija o bug de compatibilidade do iOS 9 com uma biblioteca de terceiros. Ele estava causando falhas ao enviar resultados de pesquisas, informações do aplicativo ou dados adicionais.

## <a name="300-06192015"></a>3.0.0 (06/19/2015)
* O Mobile Engagement usa notificações por push silenciosas.
* Suporte removido para iOS 4.X. A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos 6 do iOS.

## <a name="220-05212015"></a>2.2.0 (05/21/2015)
* id do dispositivo do Mobile Engagement Olá para dispositivos < iOS 6 agora se baseia em um GUID gerado no momento da instalação.

## <a name="210-04242015"></a>2.1.0 (24/04/2015)
* Compatibilidade com Swift adicionada.
* Ao clicar em uma notificação, ação Olá que URL agora é executada à direita depois que o aplicativo hello é aberto.
* Arquivo de cabeçalho ausente adicionado no pacote SDK.
* Corrigido um problema quando Relator de travamento do Mobile Engagement Olá foi desabilitado.

## <a name="200-02172015"></a>2.0.0 (17/02/2015)
* Versão Inicial do Azure Mobile Engagement
* A configuração appId/sdkKey é substituída por uma configuração de cadeia de conexão.
* Removido toosend de API e receber mensagens XMPP arbitrárias de entidades XMPP arbitrárias.
* Removido toosend de API e receber mensagens entre dispositivos.
* Aprimoramentos de segurança.
* Controle SmartAd removido.
