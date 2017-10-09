---
title: "aaaAzure iOS Mobile Engagement integração SDK | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Como tooIntegrate contrato no iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo iOS.

Olá contrato SDK requer iOS7 + e Xcode 8 +: destino de implantação de saudação do seu aplicativo deve ter pelo menos o iOS 7.

> [!NOTE]
> Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh). Há um bug conhecido no módulo de alcance Olá desta versão anterior durante a execução em dispositivos iOS 10, consulte [Olá integração do módulo de alcance](mobile-engagement-ios-integrate-engagement-reach.md) para obter mais detalhes. Se você escolher toouse Olá SDK v3.2.4, simplesmente ignore Olá `UserNotifications.framework` importar na próxima etapa do hello.
>
>

Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals. Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo iOS](mobile-engagement-ios-use-engagement-api.md) desde essas estatísticas aplicativo são dependentes.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Inserir saudação contrato SDK em seu projeto do iOS
* Baixar o SDK do iOS de saudação do [aqui](http://aka.ms/qk2rnj).
* Projeto de iOS adicionar Olá SDK Engagement tooyour: no Xcode, clique com botão direito no projeto e selecione **"Adicionar arquivos muito …"** e escolha Olá `EngagementSDK` pasta.
* Contrato requer toowork estruturas adicionais: no Explorador de projeto hello, abra o painel de projeto e selecione Olá destino correto. Em seguida, abra Olá **"Fases de compilação"** guia e na Olá **"Binário com bibliotecas de vínculo"** menu, adicionar essas estruturas:

  * `UserNotifications.framework`-Definir Olá link como`Optional`
  * `AdSupport.framework`-Definir Olá link como`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> estrutura de AdSupport Olá pode ser removida. Contrato precisa Olá de toocollect essa estrutura IDFA. No entanto, a coleção de IDFA pode ser desabilitada \<ios sdk-contrato idfa\> toocomply com nova política de Apple Olá sobre essa ID.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Olá contrato SDK
É necessário toomodify seu representante do aplicativo:

* Na parte superior de saudação do seu arquivo de implementação, importe o agente de contrato hello:

      [...]
      #import "EngagementAgent.h"
* Inicializar o contrato dentro do método hello '**applicationDidFinishLaunching:**'ou'**application: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Relatórios básicos
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Método recomendado: sobrecarregar suas classes `UIViewController`
No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `UIViewController` subclasses herdam Olá `EngagementViewController` classes (mesma regra para `UITableViewController`  - \> `EngagementTableViewController`).

**Sem o Engagement :**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Com o Engagement :**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: chame `startActivity()` manualmente
Se você não pode ou não toooverload seu `UIViewController` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent`do métodos diretamente.

> [!IMPORTANT]
> SDK do iOS Olá chama automaticamente Olá `endActivity()` método quando o aplicativo hello está fechado. Assim, é *altamente* recomendado Olá toocall `startActivity` método sempre que alterar a atividade de saudação do usuário Olá e muito*nunca* chamada hello `endActivity` método, desde que chama esse método força Olá toobe da sessão atual foi encerrado.
>
>

## <a name="location-reporting"></a>Relatórios de local
Apple termos de serviço não permitem que aplicativos toouse local controle apenas a fins de estatísticas. Portanto, é recomendável tooenable local relatórios apenas se seu aplicativo usar também o local de saudação controle por outro motivo.

A partir do iOS 8, você deve fornecer uma descrição de como seu aplicativo usa serviços de localização, definindo uma cadeia de caracteres para a chave de saudação [NSLocationWhenInUseUsageDescription] ou [NSLocationAlwaysUsageDescription]no arquivo de info. plist do aplicativo. Se você quiser tooreport local no plano de fundo de saudação com contrato, adicione chave de Olá NSLocationAlwaysUsageDescription. Em todos os outros casos, adicione a chave de saudação NSLocationWhenInUseUsageDescription. Observe que você precisa de local de plano de fundo do tooreport NSLocationAlwaysAndWhenInUseUsageDescription e NSLocationWhenInUseUsageDescription iOS 11.

### <a name="lazy-area-location-reporting"></a>Relatórios de local de área lenta
Relatório de local de área lento permite país de saudação tooreport, região e localidade associados toodevices. Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI). Olá dispositivo é relatada no máximo uma vez por sessão. Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem poucos (não toosay nenhuma) impacto na bateria hello.

Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros. Elas também podem ser usadas como critério nas campanhas do Reach. Olá conhecido última área relatada para um dispositivo pode ser recuperado Obrigado toohello [API do dispositivo].

local de área lento tooenable reporting, adicione Olá seguinte linha após a inicialização do agente de contrato hello:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Relatórios de local em tempo real
Relatório de local em tempo real permite latitude de saudação do tooreport e a longitude associada toodevices. Por padrão, esse tipo de relatório local usa apenas os locais de rede (com base na ID de célula ou Wi-Fi) e reporting Olá somente estará ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).

Locais de tempo real são *não* usado toocompute estatísticas. Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.

local em tempo real tooenable reporting, adicione Olá seguinte linha após a inicialização do agente de contrato hello:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Relatórios com base em GPS
Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede. uso de saudação do tooenable de GPS com base em locais (que são muito mais precisas), adicione:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Relatório de segundo plano
Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão). Olá tooenable relatórios também no plano de fundo, adicione:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Quando o aplicativo hello é executado em segundo plano, locais de rede com base somente são relatados, mesmo se você tiver habilitado Olá GPS.
>
>

Implementação dessa função chamará [startMonitoringSignificantLocationChanges] quando o aplicativo entra em plano de fundo de saudação. Lembre-se de que ele automaticamente reiniciar seu aplicativo no plano de fundo de saudação se chega um novo evento local.

## <a name="advanced-reporting"></a>Relatórios avançados
Opcionalmente, se você quiser trabalhos, erros e eventos específicos do aplicativo tooreport, você precisa toouse Olá contrato de API por meio de métodos de saudação do hello `EngagementAgent` classe. Um objeto dessa classe pode ser recuperado por chamada hello `[EngagementAgent shared]` método estático.

Olá contrato API permite que toouse todos os recursos avançados do contrato e é detalhado no hello como tooUse a API de contrato no iOS (bem como na documentação técnica Olá Olá `EngagementAgent` classe).

## <a name="disable-idfa-collection"></a>Desabilitar a coleta de IDFA
Por padrão, o contrato usará Olá [IDFA] toouniquely identificar um usuário. Mas se você não estiver usando anúncios em outro lugar no aplicativo hello, poderão ser rejeitadas por Olá processo de revisão da App Store. Coleção de IDFA pode ser desabilitada pela adição de macro de pré-processador Olá `ENGAGEMENT_DISABLE_IDFA` no arquivo pch (ou em Olá `Build Settings` do seu aplicativo). Isso irá garantir que não há nenhuma referência muito`ASIdentifierManager`, `advertisingIdentifier` ou `isAdvertisingTrackingEnabled` na compilação do aplicativo hello.

Integração no hello **prefix.pch** arquivo:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Você pode verificar a coleção de IDFA Olá corretamente está desabilitada em seu aplicativo verificando os logs de teste de contrato de saudação. Consulte Olá integração de teste\<ios-sdk-contrato-teste-idfa\> documentação para obter mais informações.

## <a name="disable-log-reporting"></a>Desabilitar o relatório de log
### <a name="using-a-method-call"></a>Usando uma chamada de método
Se você quiser toostop contrato envio de logs, você pode chamar:

    [[EngagementAgent shared] setEnabled:NO];

Esta chamada é persistente: usa `NSUserDefaults` toostore informações de saudação.

Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `YES`.

### <a name="integration-in-your-settings-bundle"></a>Integração no pacote de configurações
Em vez de chamar essa função, você também pode integrar essa configuração diretamente no seu arquivo `Settings.bundle` . Olá a cadeia de caracteres `engagement_agent_enabled` deve ser usado como um identificador de preferência hello e deve ser associado tooa alternância switch (`PSToggleSwitchSpecifier`).

Olá seguindo o exemplo de `Settings.bundle` mostra como tooimplement-lo:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[API do dispositivo]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
