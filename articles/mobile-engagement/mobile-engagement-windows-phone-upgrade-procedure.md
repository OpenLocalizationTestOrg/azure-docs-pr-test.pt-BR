---
title: "Procedimentos de atualização do SDK do Windows Phone Silverlight"
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
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="53583-103">Procedimentos de atualização do SDK do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="53583-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="53583-104">Se você já tiver integrado uma versão anterior do SDK no seu aplicativo, você deve considerar os seguintes pontos ao atualizar o SDK.</span><span class="sxs-lookup"><span data-stu-id="53583-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="53583-105">Você precisará seguir vários procedimentos se perdeu várias versões do SDK.</span><span class="sxs-lookup"><span data-stu-id="53583-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="53583-106">Por exemplo, se você migrar do 0.10.1 para 0.11.0 você tem que primeiro seguir o procedimento "de 0.9.0 a 0.10.1” e depois o procedimento "de 0.10.1 a 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="53583-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="53583-107">De 2.0.0 a 3.3.0</span><span class="sxs-lookup"><span data-stu-id="53583-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="53583-108">Logs de teste</span><span class="sxs-lookup"><span data-stu-id="53583-108">Test logs</span></span>
<span data-ttu-id="53583-109">Agora, os logs do console produzidos pelo SDK podem ser habilitados/desabilitados/filtrados.</span><span class="sxs-lookup"><span data-stu-id="53583-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="53583-110">Para personalizar esse recurso, atualize a propriedade `EngagementAgent.Instance.TestLogEnabled` para um dos valores disponíveis na enumeração `EngagementTestLogLevel`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="53583-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="53583-111">De 1.1.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="53583-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="53583-112">O seguinte descreve como migrar uma integração do SDK do serviço Capptain oferecido pelo Capptain SAS em um aplicativo acionado pelo Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="53583-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="53583-113">O Capptain e o Mobile Engagement não são os mesmos serviços e o procedimento fornecido abaixo destaca apenas como migrar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="53583-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="53583-114">Migrar o SDK no aplicativo NÃO migrará os dados dos servidores Capptain para os servidores do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="53583-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="53583-115">Se você estiver migrando de uma versão anterior, consulte o site do Capptain para migrar primeiro para a 1.1.1 e depois aplicar o procedimento a seguir</span><span class="sxs-lookup"><span data-stu-id="53583-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="53583-116">Pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="53583-116">Nuget package</span></span>
<span data-ttu-id="53583-117">Substitua **Capptain.WindowsPhone** pelo pacote Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="53583-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="53583-118">Aplicando o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="53583-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="53583-119">O SDK usa o termo `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="53583-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="53583-120">Você precisa atualizar seu projeto para corresponder a esta alteração.</span><span class="sxs-lookup"><span data-stu-id="53583-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="53583-121">Você precisa desinstalar o pacote nuget do Capptain atual.</span><span class="sxs-lookup"><span data-stu-id="53583-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="53583-122">Considere que todas as alterações na pasta de recursos Capptain serão removidas.</span><span class="sxs-lookup"><span data-stu-id="53583-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="53583-123">Se você quiser manter esses arquivos, então faça uma cópia deles.</span><span class="sxs-lookup"><span data-stu-id="53583-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="53583-124">Depois disso, instale o novo pacote nuget do Engagement do Microsoft Azure em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="53583-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="53583-125">Você pode encontrá-lo diretamente no [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="53583-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="53583-126">Essa ação substitui todos os arquivos de recursos usados pelo Engagement e adiciona a nova DLL do Engagement às suas referências do projeto.</span><span class="sxs-lookup"><span data-stu-id="53583-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="53583-127">Você precisa limpar as referências do projeto, excluindo as referências de Capptain DLL.</span><span class="sxs-lookup"><span data-stu-id="53583-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="53583-128">Se você não fizer isso, a versão do Capptain entrará em conflito e ocorrerão erros.</span><span class="sxs-lookup"><span data-stu-id="53583-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="53583-129">Se você personalizou os recursos do Capptain, copie o conteúdo de arquivos antigos e cole-os em novos arquivos do Engagement.</span><span class="sxs-lookup"><span data-stu-id="53583-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="53583-130">Observe que os arquivos xaml e cs devem ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="53583-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="53583-131">Quando essas etapas forem concluídas, você só precisará substituir as referências antigas do Capptain por novas referências do Engagement.</span><span class="sxs-lookup"><span data-stu-id="53583-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="53583-132">Todos os namespaces Capptain precisam ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="53583-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="53583-133">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="53583-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="53583-134">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="53583-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="53583-135">Todas as classes Capptain que contêm "Capptain" devem conter “Engagement".</span><span class="sxs-lookup"><span data-stu-id="53583-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="53583-136">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="53583-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="53583-137">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="53583-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="53583-138">Para os arquivos xaml o namespace e atributos Capptain também se alteram.</span><span class="sxs-lookup"><span data-stu-id="53583-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="53583-139">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="53583-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="53583-140">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="53583-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="53583-141">Para outros recursos como as imagens do Capptain, observe que eles também foram renomeados para usar “Engagement".</span><span class="sxs-lookup"><span data-stu-id="53583-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="53583-142">ID do aplicativo / chave do SDK</span><span class="sxs-lookup"><span data-stu-id="53583-142">Application ID / SDK Key</span></span>
<span data-ttu-id="53583-143">O Engagement usa uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="53583-143">Engagement uses a connection string.</span></span> <span data-ttu-id="53583-144">Você não precisa especificar uma ID de aplicativo e uma chave do SDK com o Mobile Engagement, você só precisa especificar uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="53583-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="53583-145">Você pode configurá-la em seu arquivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="53583-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="53583-146">A configuração do Engagement pode ser definida no arquivo `Resources\EngagementConfiguration.xml` do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="53583-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="53583-147">Edite esse arquivo para especificar:</span><span class="sxs-lookup"><span data-stu-id="53583-147">Edit this file to specify:</span></span>

* <span data-ttu-id="53583-148">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="53583-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="53583-149">Se você quiser especificá-lo em tempo de execução, você pode chamar o método a seguir antes da inicialização do agente do Engagement:</span><span class="sxs-lookup"><span data-stu-id="53583-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="53583-150">A cadeia de conexão do seu aplicativo é exibida no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="53583-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="53583-151">Alteração do nome de itens</span><span class="sxs-lookup"><span data-stu-id="53583-151">Items name change</span></span>
<span data-ttu-id="53583-152">Todos os itens chamados *capptain* foram nomeados como *engagement*.</span><span class="sxs-lookup"><span data-stu-id="53583-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="53583-153">Da mesma forma de *Capptain* para *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="53583-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="53583-154">Exemplos de itens do Capptain usados normalmente :</span><span class="sxs-lookup"><span data-stu-id="53583-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="53583-155">CapptainConfiguration agora denominado EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="53583-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="53583-156">CapptainAgent agora denominado EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="53583-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="53583-157">CapptainReach agora denominado EngagementReach</span><span class="sxs-lookup"><span data-stu-id="53583-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="53583-158">CapptainHttpConfig agora denominado EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="53583-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="53583-159">GetCapptainPageName agora denominado GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="53583-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="53583-160">Observe que renomear também afeta métodos substituídos.</span><span class="sxs-lookup"><span data-stu-id="53583-160">Note that rename also affects overridden methods.</span></span>

