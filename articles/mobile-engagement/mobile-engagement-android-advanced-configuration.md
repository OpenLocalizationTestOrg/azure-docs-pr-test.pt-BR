---
title: "configuração de aaaAdvanced para Android SDK do Azure Mobile Engagement"
description: "Descreve Olá incluindo Olá manifesto do Android com o SDK do Azure Mobile Engagement Android de opções de configuração avançada"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Configuração avançada do SDK do Azure Mobile Engagement para Android
> [!div class="op_single_selector"]
> * [Universal do Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Este procedimento descreve como tooconfigure várias opções de configuração para aplicativos do Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Requisitos de permissão
Algumas opções requerem permissões específicas, que são listadas aqui para referência e em linha no recurso específico de saudação. Adicionar toohello essas permissões AndroidManifest.xml do seu projeto imediatamente antes ou após Olá `<application>` marca.

código de permissão de saudação precisa toolook com hello seguinte, onde você preenche a permissão apropriada Olá da tabela de saudação que segue.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Permissão | Quando usado |
| --- | --- |
| INTERNET |Obrigatório. Para relatório básico |
| ACCESS_NETWORK_STATE |Obrigatório. Para relatório básico |
| RECEIVE_BOOT_COMPLETED |Obrigatório. tooshow a Central de notificações de saudação após a reinicialização do dispositivo |
| WAKE_LOCK |Recomendável. Habilita a coleta de dados ao usar Wi-Fi ou quando a tela estiver desligada |
| VIBRATE |Opcional. Habilita a vibração após o recebimento de notificações |
| DOWNLOAD_WITHOUT_NOTIFICATION |Opcional. Habilita a notificação de visão geral do Android |
| WRITE_EXTERNAL_STORAGE |Opcional. Habilita a notificação de visão geral do Android |
| ACCESS_COARSE_LOCATION |Opcional. Habilita o relatório de local em tempo real |
| ACCESS_FINE_LOCATION |Opcional. Habilita o relatório de local baseado em GPS |

A partir do Android M, [algumas permissões são gerenciadas em tempo de execução](mobile-engagement-android-location-reporting.md#android-m-permissions).

Se você já estiver usando ``ACCESS_FINE_LOCATION``, em seguida, você não precisa tooalso usar ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Opções de configuração do manifesto do Android
### <a name="crash-report"></a>Relatório de falha
relatórios de falha de toodisable, adicione este código entre hello `<application>` e `</application>` marcas:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Limite de intermitência
Por padrão, os relatórios de serviço de contrato de saudação logs em tempo real. Se seus logs de aplicativo de relatório variam de acordo com frequência, é melhor toobuffer Olá logs e tooreport-los todos de uma vez em um base de tempo regulares (chamado de "modo de disparar"). toodo por isso, adicione este código entre hello `<application>` e `</application>` marcas:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Modo intermitente ligeiramente aumenta a vida útil da bateria Olá mas tem um impacto em Olá contrato Monitor: todas as sessões e trabalhos a duração são arredondados toohello intermitência limite (portanto, sessões e menor do que o limite de disparo Olá pode não estar visível de trabalhos). O limite de disparo contínuo não deve ser maior do que 30.000 (30 s).

### <a name="session-timeout"></a>Tempo limite da sessão
 Você pode finalizar uma atividade pressionando Olá **início** ou **novamente** chave, por definição Olá telefone ocioso ou pulando em outro aplicativo. Por padrão, uma sessão será encerrada dez segundos após o término de saudação de sua última atividade. Isso evita uma divisão de sessão cada usuário em tempo de saudação encerrado e retorna o aplicativo toohello rapidamente, que pode acontecer quando o usuário Olá pega uma imagem, verifica uma notificação, etc. Talvez você queira toomodify esse parâmetro. toodo por isso, adicione este código entre hello `<application>` e `</application>` marcas:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Desabilitar o relatório de log
### <a name="using-a-method-call"></a>Usando uma chamada de método
Se você quiser toostop contrato envio de logs, você pode chamar:

    EngagementAgent.getInstance(context).setEnabled(false);

Essa chamada é persistente: ela utiliza um arquivo de preferências compartilhado.

Se o contrato está ativo, quando você chamar essa função, pode levar um minuto para Olá toostop de serviço. No entanto, não é possível abrir serviço Olá Olá todos próxima vez que você iniciar o aplicativo hello.

Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integração em seu próprio `PreferenceActivity`
Em vez de chamar essa função, você também pode integrar esta configuração diretamente em seu arquivo existente `PreferenceActivity`.

Você pode configurar contrato toouse suas preferências de arquivo (com modo desejado de saudação) Olá `AndroidManifest.xml` arquivo com `application meta-data`:

* Olá `engagement:agent:settings:name` chave é usado toodefine Olá nome do arquivo de preferências compartilhadas Olá.
* Olá `engagement:agent:settings:mode` chave é o modo de saudação toodefine usado do arquivo de preferências compartilhadas hello. Use Olá mesmo modo que no seu `PreferenceActivity`. Olá modo deve ser passado como um número: se você estiver usando uma combinação de sinalizadores constantes em seu código, verifique o valor total de saudação.

Contrato sempre usa Olá `engagement:key` booliano chave no arquivo de preferências de saudação para gerenciar essa configuração.

Olá seguindo o exemplo de `AndroidManifest.xml` mostra Olá valores padrão:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

Em seguida, você pode adicionar um `CheckBoxPreference` em seu layout de preferência como Olá seguindo um:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
