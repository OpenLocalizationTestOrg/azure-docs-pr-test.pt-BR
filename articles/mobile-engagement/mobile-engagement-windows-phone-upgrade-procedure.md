---
title: "aaaWindows procedimentos de atualização do SDK Phone Silverlight"
description: "Procedimentos de atualização do SDK do Windows Phone Silverlight para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="036c8-103">Procedimentos de atualização do SDK do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="036c8-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="036c8-104">Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="036c8-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="036c8-105">Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="036c8-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="036c8-106">Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.</span><span class="sxs-lookup"><span data-stu-id="036c8-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="036c8-107">De 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="036c8-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="036c8-108">Logs de teste</span><span class="sxs-lookup"><span data-stu-id="036c8-108">Test logs</span></span>
<span data-ttu-id="036c8-109">Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas.</span><span class="sxs-lookup"><span data-stu-id="036c8-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="036c8-110">toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="036c8-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="036c8-111">De 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="036c8-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="036c8-112">Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="036c8-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="036c8-113">Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="036c8-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="036c8-114">Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores</span><span class="sxs-lookup"><span data-stu-id="036c8-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="036c8-115">Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too1.1.1 primeiro e aplicar Olá procedimento</span><span class="sxs-lookup"><span data-stu-id="036c8-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="036c8-116">Pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="036c8-116">Nuget package</span></span>
<span data-ttu-id="036c8-117">Substitua **Capptain.WindowsPhone** pelo pacote Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="036c8-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="036c8-118">Aplicando o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="036c8-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="036c8-119">Olá SDK usa o termo Olá `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="036c8-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="036c8-120">Você precisa tooupdate toomatch seu projeto essa alteração.</span><span class="sxs-lookup"><span data-stu-id="036c8-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="036c8-121">É necessário toouninstall seu pacote do nuget Capptain atual.</span><span class="sxs-lookup"><span data-stu-id="036c8-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="036c8-122">Considere que todas as alterações na pasta de recursos Capptain serão removidas.</span><span class="sxs-lookup"><span data-stu-id="036c8-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="036c8-123">Se você quiser tookeep esses arquivos, em seguida, faça uma cópia deles.</span><span class="sxs-lookup"><span data-stu-id="036c8-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="036c8-124">Depois disso, instale o novo pacote de nuget de contrato do Microsoft Azure Olá no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="036c8-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="036c8-125">Você pode encontrá-lo diretamente no [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="036c8-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="036c8-126">Substitui essa ação, todos os arquivos de recursos usado pelo contrato e adiciona Olá novo contrato DLL tooyour referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="036c8-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="036c8-127">Você tem as referências do projeto tooclean excluindo referências Capptain DLL.</span><span class="sxs-lookup"><span data-stu-id="036c8-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="036c8-128">Se você não fizer isso, versão de saudação do Capptain entrarão em conflito e ocorrerão erros.</span><span class="sxs-lookup"><span data-stu-id="036c8-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="036c8-129">Se você tiver personalizado Capptain recursos, copie o conteúdo de arquivos antigos e colá-los em novos arquivos de contrato hello.</span><span class="sxs-lookup"><span data-stu-id="036c8-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="036c8-130">Observe que os arquivos xaml e o cs toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="036c8-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="036c8-131">Quando essas etapas forem concluídas, você só tem referências antigas de Capptain tooreplace por novas referências de contrato hello.</span><span class="sxs-lookup"><span data-stu-id="036c8-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="036c8-132">Todos os namespaces Capptain ter toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="036c8-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="036c8-133">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="036c8-134">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="036c8-135">Todas as classes Capptain que contêm "Capptain" devem conter “Engagement".</span><span class="sxs-lookup"><span data-stu-id="036c8-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="036c8-136">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="036c8-137">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="036c8-138">Para os arquivos xaml o namespace e atributos Capptain também se alteram.</span><span class="sxs-lookup"><span data-stu-id="036c8-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="036c8-139">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="036c8-140">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="036c8-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="036c8-141">Para Olá a outros recursos, como imagens Capptain, observe que eles foram renomeado toouse "Contrato".</span><span class="sxs-lookup"><span data-stu-id="036c8-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="036c8-142">ID do aplicativo / chave do SDK</span><span class="sxs-lookup"><span data-stu-id="036c8-142">Application ID / SDK Key</span></span>
<span data-ttu-id="036c8-143">O Engagement usa uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="036c8-143">Engagement uses a connection string.</span></span> <span data-ttu-id="036c8-144">Você não tem toospecify uma ID de aplicativo e uma chave do SDK com o Mobile Engagement, tiver apenas toospecify uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="036c8-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="036c8-145">Você pode configurá-la em seu arquivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="036c8-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="036c8-146">configuração do contrato Olá pode ser definida em sua `Resources\EngagementConfiguration.xml` arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="036c8-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="036c8-147">Edite esse arquivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="036c8-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="036c8-148">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="036c8-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="036c8-149">Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:</span><span class="sxs-lookup"><span data-stu-id="036c8-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="036c8-150">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no hello Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="036c8-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="036c8-151">Alteração do nome de itens</span><span class="sxs-lookup"><span data-stu-id="036c8-151">Items name change</span></span>
<span data-ttu-id="036c8-152">Todos os itens chamados *capptain* foram nomeados como *engagement*.</span><span class="sxs-lookup"><span data-stu-id="036c8-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="036c8-153">Da mesma forma para *Capptain* muito*contrato*.</span><span class="sxs-lookup"><span data-stu-id="036c8-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="036c8-154">Exemplos de itens do Capptain usados normalmente :</span><span class="sxs-lookup"><span data-stu-id="036c8-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="036c8-155">CapptainConfiguration agora denominado EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="036c8-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="036c8-156">CapptainAgent agora denominado EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="036c8-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="036c8-157">CapptainReach agora denominado EngagementReach</span><span class="sxs-lookup"><span data-stu-id="036c8-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="036c8-158">CapptainHttpConfig agora denominado EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="036c8-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="036c8-159">GetCapptainPageName agora denominado GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="036c8-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="036c8-160">Observe que renomear também afeta métodos substituídos.</span><span class="sxs-lookup"><span data-stu-id="036c8-160">Note that rename also affects overridden methods.</span></span>

