---
title: "aaaAzure integração do Mobile Engagement Android SDK"
description: "Atualizações e procedimentos mais recentes para o SDK do Android do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Notas de versão

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Corrigir uma falha que raramente pode acontecer ao chamar `EngagementAgentUtils.isInDedicatedEngagementProcess`, que também é usado por Olá `EngagementApplication` classe.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Suporte de 8 Android (versões anteriores do hello SDK não funcionarão no Android 8).
* Não há mais dependência da biblioteca de suporte.
* Remover classe `EngagementFragmentActivity`.
* Vencimento muito[limites de execução do plano de fundo](https://developer.android.com/preview/features/background.html) no Android 8, logs no plano de fundo podem ser atrasados até que o usuário Olá interage com o dispositivo de saudação, isso terá um impacto na campanha de Push **entregues** e **Notificação do sistema exibida** estatísticas atrasadas se dispositivo Olá foi suspenso (Olá notificação ainda será exibida, será de anel e Vibrar em tempo real sem problemas).
* Vencimento muito[limites de local do plano de fundo](https://developer.android.com/preview/features/background-location-limits.html), local Olá em tempo real no plano de fundo não será atualizada com frequência no Android 8.

## <a name="424-03302017"></a>4.2.4 (30/03/2017)
* Corrija a notificação no aplicativo cores de texto no Android 7 toobe Olá mesmo que as versões mais antigas de Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Nenhum outro bloqueio de WIFI.
* Corrige um deadlock ao chamar getDeviceId antes de init (bug introduzido na versão 4.2.0).

## <a name="422-05172016"></a>4.2.2 (17/05/2016)
* Aprimoramentos de estabilidade.

## <a name="421-05102016"></a>4.2.1 (10/05/2016)
* Segurança: desabilite o acesso de arquivo local de exibição na Web.
* Segurança: remova a classe `EngagementPreferenceActivity` que estende a classe `PreferenceActivity` obsoleta e não segura.
* Segurança: alcance atividades agora estão documentados toouse `exported="false"`, esse sinalizador também pode ser usado em versões anteriores do SDK.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Olá SDK está licenciado sob MIT.
* Permita a especificação de um identificador de dispositivo personalizado no momento de inicialização do SDK.

## <a name="415-02012016"></a>4.1.5 (01/02/2016)
* Aprimoramentos de estabilidade.

## <a name="414-01262016"></a>4.1.4 (26/01/2016)
* Aprimoramentos de estabilidade.

## <a name="413-1292015"></a>4.1.3 (09/12/2015)
* Aprimoramentos de estabilidade.

## <a name="412-11252015"></a>4.1.2 (25/11/2015)
* Aprimoramentos de estabilidade.

## <a name="411-11042015"></a>4.1.1 (04/11/2015)
* Aprimoramentos de estabilidade.

## <a name="410-08252015"></a>4.1.0 (25/08/2015)
* Lidar com o novo modelo de permissão para Android M.
* Agora é possível configurar os recursos de localização no tempo de execução em vez de usar o `AndroidManifest.xml`.
* Corrija um bug de permissão: se você usar `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` não será mais necessário.
* Aprimoramentos de estabilidade.

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* Protocolo interno altera toomake análise e mais confiável de envio.
* Envio por push nativo (GCM/ADM) agora também é usado para em notificações de aplicativo para que você deve configurar credenciais de push nativo Olá para qualquer tipo de campanha de push.
* Corrigir a notificação de visão geral: foram exibidas somente 10s depois de enviadas.
* Corrigir um bug no modo de exibição da web: clicar em um link também estava executando Olá a URL da ação padrão.
* Corrigir uma falha rara relacionados ao gerenciamento de armazenamento toolocal.
* Corrigir o gerenciamento de cadeia de caracteres de configuração dinâmica.
* Atualizar EULA.

## <a name="300-02172015"></a>3.0.0 (17/02/2015)
* Versão Inicial do Azure Mobile Engagement
* A configuração do appId é substituída por uma configuração de cadeia de conexão.
* Removido toosend de API e receber mensagens XMPP arbitrárias de entidades XMPP arbitrárias.
* Removido toosend de API e receber mensagens entre dispositivos.
* Aprimoramentos de segurança.
* Acompanhamento do Google Play e SmartAd removido.

