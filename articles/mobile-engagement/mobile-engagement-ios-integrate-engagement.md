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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="97eab-103">Como tooIntegrate contrato no iOS</span><span class="sxs-lookup"><span data-stu-id="97eab-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97eab-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="97eab-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="97eab-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="97eab-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="97eab-106">iOS</span><span class="sxs-lookup"><span data-stu-id="97eab-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="97eab-107">Android</span><span class="sxs-lookup"><span data-stu-id="97eab-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="97eab-108">Este procedimento descreve hello mais simples maneira tooactivate contrato análise e monitoramento de funções em seu aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="97eab-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="97eab-109">Olá contrato SDK requer iOS7 + e Xcode 8 +: destino de implantação de saudação do seu aplicativo deve ter pelo menos o iOS 7.</span><span class="sxs-lookup"><span data-stu-id="97eab-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="97eab-110">Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="97eab-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="97eab-111">Há um bug conhecido no módulo de alcance Olá desta versão anterior durante a execução em dispositivos iOS 10, consulte [Olá integração do módulo de alcance](mobile-engagement-ios-integrate-engagement-reach.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="97eab-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="97eab-112">Se você escolher toouse Olá SDK v3.2.4, simplesmente ignore Olá `UserNotifications.framework` importar na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="97eab-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="97eab-113">Olá, as etapas a seguir é que suficientes relatório de saudação tooactivate dos logs necessário toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e Technicals.</span><span class="sxs-lookup"><span data-stu-id="97eab-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="97eab-114">Olá relatório dos logs necessário toocompute outras estatísticas como trabalhos, erros e eventos devem ser feitos manualmente usando Olá contrato de API (consulte [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo iOS](mobile-engagement-ios-use-engagement-api.md) desde essas estatísticas aplicativo são dependentes.</span><span class="sxs-lookup"><span data-stu-id="97eab-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="97eab-115">Inserir saudação contrato SDK em seu projeto do iOS</span><span class="sxs-lookup"><span data-stu-id="97eab-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="97eab-116">Baixar o SDK do iOS de saudação do [aqui](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="97eab-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="97eab-117">Projeto de iOS adicionar Olá SDK Engagement tooyour: no Xcode, clique com botão direito no projeto e selecione **"Adicionar arquivos muito …"** e escolha Olá `EngagementSDK` pasta.</span><span class="sxs-lookup"><span data-stu-id="97eab-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="97eab-118">Contrato requer toowork estruturas adicionais: no Explorador de projeto hello, abra o painel de projeto e selecione Olá destino correto.</span><span class="sxs-lookup"><span data-stu-id="97eab-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="97eab-119">Em seguida, abra Olá **"Fases de compilação"** guia e na Olá **"Binário com bibliotecas de vínculo"** menu, adicionar essas estruturas:</span><span class="sxs-lookup"><span data-stu-id="97eab-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="97eab-120">`UserNotifications.framework`-Definir Olá link como`Optional`</span><span class="sxs-lookup"><span data-stu-id="97eab-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="97eab-121">`AdSupport.framework`-Definir Olá link como`Optional`</span><span class="sxs-lookup"><span data-stu-id="97eab-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="97eab-122">estrutura de AdSupport Olá pode ser removida.</span><span class="sxs-lookup"><span data-stu-id="97eab-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="97eab-123">Contrato precisa Olá de toocollect essa estrutura IDFA.</span><span class="sxs-lookup"><span data-stu-id="97eab-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="97eab-124">No entanto, a coleção de IDFA pode ser desabilitada \<ios sdk-contrato idfa\> toocomply com nova política de Apple Olá sobre essa ID.</span><span class="sxs-lookup"><span data-stu-id="97eab-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="97eab-125">Inicializar Olá contrato SDK</span><span class="sxs-lookup"><span data-stu-id="97eab-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="97eab-126">É necessário toomodify seu representante do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="97eab-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="97eab-127">Na parte superior de saudação do seu arquivo de implementação, importe o agente de contrato hello:</span><span class="sxs-lookup"><span data-stu-id="97eab-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="97eab-128">Inicializar o contrato dentro do método hello '**applicationDidFinishLaunching:**'ou'**application: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="97eab-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="97eab-129">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="97eab-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="97eab-130">Método recomendado: sobrecarregar suas classes `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="97eab-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="97eab-131">No relatório de saudação tooactivate de ordem de todos os logs de saudação exigido pelo contrato toocompute usuários, sessões, atividades, falhas e estatísticas técnicas, você pode simplesmente fazer todas as suas `UIViewController` subclasses herdam Olá `EngagementViewController` classes (mesma regra para `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="97eab-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="97eab-132">**Sem o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="97eab-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="97eab-133">**Com o Engagement :**</span><span class="sxs-lookup"><span data-stu-id="97eab-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="97eab-134">Método alternativo: chame `startActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="97eab-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="97eab-135">Se você não pode ou não toooverload seu `UIViewController` classes, em vez disso, você pode iniciar suas atividades chamando `EngagementAgent`do métodos diretamente.</span><span class="sxs-lookup"><span data-stu-id="97eab-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97eab-136">SDK do iOS Olá chama automaticamente Olá `endActivity()` método quando o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="97eab-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="97eab-137">Assim, é *altamente* recomendado Olá toocall `startActivity` método sempre que alterar a atividade de saudação do usuário Olá e muito*nunca* chamada hello `endActivity` método, desde que chama esse método força Olá toobe da sessão atual foi encerrado.</span><span class="sxs-lookup"><span data-stu-id="97eab-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="97eab-138">Relatórios de local</span><span class="sxs-lookup"><span data-stu-id="97eab-138">Location reporting</span></span>
<span data-ttu-id="97eab-139">Apple termos de serviço não permitem que aplicativos toouse local controle apenas a fins de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="97eab-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="97eab-140">Portanto, é recomendável tooenable local relatórios apenas se seu aplicativo usar também o local de saudação controle por outro motivo.</span><span class="sxs-lookup"><span data-stu-id="97eab-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="97eab-141">A partir do iOS 8, você deve fornecer uma descrição de como seu aplicativo usa serviços de localização, definindo uma cadeia de caracteres para a chave de saudação [NSLocationWhenInUseUsageDescription] ou [NSLocationAlwaysUsageDescription]no arquivo de info. plist do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97eab-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="97eab-142">Se você quiser tooreport local no plano de fundo de saudação com contrato, adicione chave de Olá NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="97eab-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="97eab-143">Em todos os outros casos, adicione a chave de saudação NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="97eab-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="97eab-144">Observe que você precisa de local de plano de fundo do tooreport NSLocationAlwaysAndWhenInUseUsageDescription e NSLocationWhenInUseUsageDescription iOS 11.</span><span class="sxs-lookup"><span data-stu-id="97eab-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="97eab-145">Relatórios de local de área lenta</span><span class="sxs-lookup"><span data-stu-id="97eab-145">Lazy area location reporting</span></span>
<span data-ttu-id="97eab-146">Relatório de local de área lento permite país de saudação tooreport, região e localidade associados toodevices.</span><span class="sxs-lookup"><span data-stu-id="97eab-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="97eab-147">Esse tipo de relatório de local usa apenas os locais de rede (com base na ID da célula ou WIFI).</span><span class="sxs-lookup"><span data-stu-id="97eab-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="97eab-148">Olá dispositivo é relatada no máximo uma vez por sessão.</span><span class="sxs-lookup"><span data-stu-id="97eab-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="97eab-149">Olá GPS nunca é usado e, portanto, esse tipo de relatório local tem poucos (não toosay nenhuma) impacto na bateria hello.</span><span class="sxs-lookup"><span data-stu-id="97eab-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="97eab-150">Relatado áreas são estatísticas de geográfica toocompute usado sobre usuários, sessões, eventos e erros.</span><span class="sxs-lookup"><span data-stu-id="97eab-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="97eab-151">Elas também podem ser usadas como critério nas campanhas do Reach.</span><span class="sxs-lookup"><span data-stu-id="97eab-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="97eab-152">Olá conhecido última área relatada para um dispositivo pode ser recuperado Obrigado toohello [API do dispositivo].</span><span class="sxs-lookup"><span data-stu-id="97eab-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="97eab-153">local de área lento tooenable reporting, adicione Olá seguinte linha após a inicialização do agente de contrato hello:</span><span class="sxs-lookup"><span data-stu-id="97eab-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="97eab-154">Relatórios de local em tempo real</span><span class="sxs-lookup"><span data-stu-id="97eab-154">Real time location reporting</span></span>
<span data-ttu-id="97eab-155">Relatório de local em tempo real permite latitude de saudação do tooreport e a longitude associada toodevices.</span><span class="sxs-lookup"><span data-stu-id="97eab-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="97eab-156">Por padrão, esse tipo de relatório local usa apenas os locais de rede (com base na ID de célula ou Wi-Fi) e reporting Olá somente estará ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="97eab-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="97eab-157">Locais de tempo real são *não* usado toocompute estatísticas.</span><span class="sxs-lookup"><span data-stu-id="97eab-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="97eab-158">Seu único propósito é o uso de saudação do tooallow de geoinstalação em tempo real \<alcance-público-o isolamento geográfico\> critério de campanhas de alcance.</span><span class="sxs-lookup"><span data-stu-id="97eab-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="97eab-159">local em tempo real tooenable reporting, adicione Olá seguinte linha após a inicialização do agente de contrato hello:</span><span class="sxs-lookup"><span data-stu-id="97eab-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="97eab-160">Relatórios com base em GPS</span><span class="sxs-lookup"><span data-stu-id="97eab-160">GPS based reporting</span></span>
<span data-ttu-id="97eab-161">Por padrão, os relatórios de local em tempo real usam apenas locais com base em rede.</span><span class="sxs-lookup"><span data-stu-id="97eab-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="97eab-162">uso de saudação do tooenable de GPS com base em locais (que são muito mais precisas), adicione:</span><span class="sxs-lookup"><span data-stu-id="97eab-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="97eab-163">Relatório de segundo plano</span><span class="sxs-lookup"><span data-stu-id="97eab-163">Background reporting</span></span>
<span data-ttu-id="97eab-164">Por padrão, relatórios de local em tempo real só está ativo quando o aplicativo hello é executado em primeiro plano (ou seja, durante uma sessão).</span><span class="sxs-lookup"><span data-stu-id="97eab-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="97eab-165">Olá tooenable relatórios também no plano de fundo, adicione:</span><span class="sxs-lookup"><span data-stu-id="97eab-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="97eab-166">Quando o aplicativo hello é executado em segundo plano, locais de rede com base somente são relatados, mesmo se você tiver habilitado Olá GPS.</span><span class="sxs-lookup"><span data-stu-id="97eab-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="97eab-167">Implementação dessa função chamará [startMonitoringSignificantLocationChanges] quando o aplicativo entra em plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="97eab-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="97eab-168">Lembre-se de que ele automaticamente reiniciar seu aplicativo no plano de fundo de saudação se chega um novo evento local.</span><span class="sxs-lookup"><span data-stu-id="97eab-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="97eab-169">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="97eab-169">Advanced reporting</span></span>
<span data-ttu-id="97eab-170">Opcionalmente, se você quiser trabalhos, erros e eventos específicos do aplicativo tooreport, você precisa toouse Olá contrato de API por meio de métodos de saudação do hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="97eab-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="97eab-171">Um objeto dessa classe pode ser recuperado por chamada hello `[EngagementAgent shared]` método estático.</span><span class="sxs-lookup"><span data-stu-id="97eab-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="97eab-172">Olá contrato API permite que toouse todos os recursos avançados do contrato e é detalhado no hello como tooUse a API de contrato no iOS (bem como na documentação técnica Olá Olá `EngagementAgent` classe).</span><span class="sxs-lookup"><span data-stu-id="97eab-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="97eab-173">Desabilitar a coleta de IDFA</span><span class="sxs-lookup"><span data-stu-id="97eab-173">Disable IDFA collection</span></span>
<span data-ttu-id="97eab-174">Por padrão, o contrato usará Olá [IDFA] toouniquely identificar um usuário.</span><span class="sxs-lookup"><span data-stu-id="97eab-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="97eab-175">Mas se você não estiver usando anúncios em outro lugar no aplicativo hello, poderão ser rejeitadas por Olá processo de revisão da App Store.</span><span class="sxs-lookup"><span data-stu-id="97eab-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="97eab-176">Coleção de IDFA pode ser desabilitada pela adição de macro de pré-processador Olá `ENGAGEMENT_DISABLE_IDFA` no arquivo pch (ou em Olá `Build Settings` do seu aplicativo).</span><span class="sxs-lookup"><span data-stu-id="97eab-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="97eab-177">Isso irá garantir que não há nenhuma referência muito`ASIdentifierManager`, `advertisingIdentifier` ou `isAdvertisingTrackingEnabled` na compilação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="97eab-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="97eab-178">Integração no hello **prefix.pch** arquivo:</span><span class="sxs-lookup"><span data-stu-id="97eab-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="97eab-179">Você pode verificar a coleção de IDFA Olá corretamente está desabilitada em seu aplicativo verificando os logs de teste de contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="97eab-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="97eab-180">Consulte Olá integração de teste\<ios-sdk-contrato-teste-idfa\> documentação para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="97eab-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="97eab-181">Desabilitar o relatório de log</span><span class="sxs-lookup"><span data-stu-id="97eab-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="97eab-182">Usando uma chamada de método</span><span class="sxs-lookup"><span data-stu-id="97eab-182">Using a method call</span></span>
<span data-ttu-id="97eab-183">Se você quiser toostop contrato envio de logs, você pode chamar:</span><span class="sxs-lookup"><span data-stu-id="97eab-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="97eab-184">Esta chamada é persistente: usa `NSUserDefaults` toostore informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="97eab-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="97eab-185">Você pode habilitar o log de relatórios novamente chamando Olá a mesma função com `YES`.</span><span class="sxs-lookup"><span data-stu-id="97eab-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="97eab-186">Integração no pacote de configurações</span><span class="sxs-lookup"><span data-stu-id="97eab-186">Integration in your settings bundle</span></span>
<span data-ttu-id="97eab-187">Em vez de chamar essa função, você também pode integrar essa configuração diretamente no seu arquivo `Settings.bundle` .</span><span class="sxs-lookup"><span data-stu-id="97eab-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="97eab-188">Olá a cadeia de caracteres `engagement_agent_enabled` deve ser usado como um identificador de preferência hello e deve ser associado tooa alternância switch (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="97eab-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="97eab-189">Olá seguindo o exemplo de `Settings.bundle` mostra como tooimplement-lo:</span><span class="sxs-lookup"><span data-stu-id="97eab-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
