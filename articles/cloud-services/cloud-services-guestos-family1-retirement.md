---
title: "aaaGuest sistema operacional família 1 desativação Observe | Microsoft Docs"
description: "Fornece informações sobre quando a desativação de hello Azure SO convidado família 1 aconteceu e como toodetermine se você for afetado"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="508fa-103">Aviso de desativação da família 1 de SO convidados</span><span class="sxs-lookup"><span data-stu-id="508fa-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="508fa-104">desativação de saudação da família 1 do SO foi anunciada em 1 de junho de 2013.</span><span class="sxs-lookup"><span data-stu-id="508fa-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="508fa-105">**2 de setembro de 2014** Olá o sistema operacional de convidado do Azure (SO convidado) família 1. x, que é baseado no sistema operacional de saudação do Windows Server 2008, foi oficialmente desativado.</span><span class="sxs-lookup"><span data-stu-id="508fa-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="508fa-106">Todas as tentativas toodeploy novos serviços ou atualizações serviços existentes usando a família 1 falharão com uma mensagem de erro informando que Olá que SO convidado família 1 foi desativado.</span><span class="sxs-lookup"><span data-stu-id="508fa-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="508fa-107">**3 de novembro de 2014** O suporte estendido para a família 1 dos sistemas operacionais convidados terminou e está totalmente desativado.</span><span class="sxs-lookup"><span data-stu-id="508fa-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="508fa-108">Todos os serviços que ainda estão na família 1 serão afetados.</span><span class="sxs-lookup"><span data-stu-id="508fa-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="508fa-109">Podemos interromper esses serviços a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="508fa-109">We may stop those services at any time.</span></span> <span data-ttu-id="508fa-110">Não há nenhuma garantia que os serviços continuarão toorun, a menos que você atualize-os manualmente por conta própria.</span><span class="sxs-lookup"><span data-stu-id="508fa-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="508fa-111">Se você tiver outras perguntas, visite Olá [fóruns de serviços de nuvem](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [entre em contato com o suporte do Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="508fa-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="508fa-112">Você foi afetado?</span><span class="sxs-lookup"><span data-stu-id="508fa-112">Are you affected?</span></span>
<span data-ttu-id="508fa-113">Os serviços de nuvem são afetados se qualquer um dos seguintes Olá se aplica:</span><span class="sxs-lookup"><span data-stu-id="508fa-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="508fa-114">Você tem um valor de "osFamily ="1"explicitamente especificado no arquivo ServiceConfiguration cscfg Olá para seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="508fa-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="508fa-115">Você não tem um valor de osFamily especificado explicitamente no arquivo ServiceConfiguration cscfg Olá para seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="508fa-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="508fa-116">Atualmente, sistema Olá usa saudação padrão valor de "1" neste caso.</span><span class="sxs-lookup"><span data-stu-id="508fa-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="508fa-117">Olá portal do Azure lista o valor da família do sistema operacional convidado como "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="508fa-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="508fa-118">toofind quais dos seus serviços de nuvem estão executando quais famílias de sistema operacional, você pode executar Olá seguinte script do PowerShell do Azure, embora você deva [configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) primeiro.</span><span class="sxs-lookup"><span data-stu-id="508fa-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="508fa-119">Para obter mais informações sobre o script hello, consulte [Azure convidado sistema operacional família 1 fim da vida útil: junho de 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="508fa-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="508fa-120">Os serviços de nuvem serão afetados pela desativação da família 1 do SO se a coluna de osFamily Olá na saída do script hello está vazia ou contém um "1".</span><span class="sxs-lookup"><span data-stu-id="508fa-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="508fa-121">Recomendações se você for afetado</span><span class="sxs-lookup"><span data-stu-id="508fa-121">Recommendations if you are affected</span></span>
<span data-ttu-id="508fa-122">Recomendamos que você migre seu tooone de funções de serviço de nuvem de famílias de SO convidado Olá com suporte:</span><span class="sxs-lookup"><span data-stu-id="508fa-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="508fa-123">**Família 4.x dos SOs convidados** - Windows Server 2012 R2 *(recomendado)*</span><span class="sxs-lookup"><span data-stu-id="508fa-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="508fa-124">Certifique-se de que seu aplicativo esteja usando o SDK 2.1 ou posterior com o .NET Framework 4.0, 4.5 ou 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="508fa-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="508fa-125">Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "4" hello em e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="508fa-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="508fa-126">**Família 3.x dos SOs convidados** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="508fa-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="508fa-127">Certifique-se de que seu aplicativo esteja usando o SDK 1.8 ou posterior com o .NET Framework 4.0 ou 4.5.</span><span class="sxs-lookup"><span data-stu-id="508fa-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="508fa-128">Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "3" hello em e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="508fa-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="508fa-129">**Família 2.x dos SOs convidados** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="508fa-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="508fa-130">Certifique-se de que seu aplicativo esteja usando o SDK 1.3 e posterior com o .NET Framework 3.5 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="508fa-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="508fa-131">Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "2" hello em e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="508fa-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="508fa-132">O suporte estendido para a Família 1 dos sistemas operacionais convidados terminou em 3 de novembro de 2014</span><span class="sxs-lookup"><span data-stu-id="508fa-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="508fa-133">Não há mais suporte para serviços de nuvem na família 1 dos sistemas operacionais convidados.</span><span class="sxs-lookup"><span data-stu-id="508fa-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="508fa-134">Migre da família 1 assim tooavoid possíveis interrupções de serviço.</span><span class="sxs-lookup"><span data-stu-id="508fa-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="508fa-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="508fa-135">Next steps</span></span>
<span data-ttu-id="508fa-136">Saudação de revisão mais recente [versões de sistema operacional convidado](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="508fa-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
