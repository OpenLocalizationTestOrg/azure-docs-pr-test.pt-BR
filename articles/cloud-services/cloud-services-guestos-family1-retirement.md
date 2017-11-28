---
title: "Aviso de desativação da família 1 de SOs convidados | Microsoft Docs"
description: "Fornece informações sobre quando ocorreu a desativação da família 1 sistemas operacionais convidados do Azure e determinar se você foi afetado"
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
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="7aecd-103">Aviso de desativação da família 1 de SO convidados</span><span class="sxs-lookup"><span data-stu-id="7aecd-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="7aecd-104">A desativação da família 1 do sistema operacional foi anunciada em 1º de junho de 2013.</span><span class="sxs-lookup"><span data-stu-id="7aecd-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="7aecd-105">**2 de setembro de 2014** A família 1.x do sistema operacional convidado do Azure (SO convidado), que se baseia no sistema operacional Windows Server 2008, foi oficialmente desativada.</span><span class="sxs-lookup"><span data-stu-id="7aecd-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="7aecd-106">Todas as tentativas para implantar novos serviços ou atualizar serviços existentes usando a família 1 falharão com uma mensagem de erro informando que a família 1 dos sistemas operacionais convidados foi desativada.</span><span class="sxs-lookup"><span data-stu-id="7aecd-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="7aecd-107">**3 de novembro de 2014** O suporte estendido para a família 1 dos sistemas operacionais convidados terminou e está totalmente desativado.</span><span class="sxs-lookup"><span data-stu-id="7aecd-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="7aecd-108">Todos os serviços que ainda estão na família 1 serão afetados.</span><span class="sxs-lookup"><span data-stu-id="7aecd-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="7aecd-109">Podemos interromper esses serviços a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="7aecd-109">We may stop those services at any time.</span></span> <span data-ttu-id="7aecd-110">Não há nenhuma garantia de que seus serviços continuarão sendo executados, a menos que você os atualize manualmente por conta própria.</span><span class="sxs-lookup"><span data-stu-id="7aecd-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="7aecd-111">Se você tiver outras dúvidas, visite os [Fóruns dos Serviços de Nuvem](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [entre em contato com o suporte do Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="7aecd-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="7aecd-112">Você foi afetado?</span><span class="sxs-lookup"><span data-stu-id="7aecd-112">Are you affected?</span></span>
<span data-ttu-id="7aecd-113">Os Serviços de Nuvem são afetados se qualquer uma das opções a seguir se aplicar:</span><span class="sxs-lookup"><span data-stu-id="7aecd-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="7aecd-114">Você tem um valor de "osFamily = "1" explicitamente especificado no arquivo ServiceConfiguration.cscfg para seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7aecd-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="7aecd-115">Você não tem um valor para osFamily especificado explicitamente no arquivo ServiceConfiguration.cscfg para seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7aecd-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="7aecd-116">Atualmente, o sistema usa o valor padrão de "1" nesse caso.</span><span class="sxs-lookup"><span data-stu-id="7aecd-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="7aecd-117">O Portal do Azure lista o valor da família do Sistema Operacional Convidado como "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="7aecd-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="7aecd-118">Para definir quais dos serviços de nuvem estão executando qual família de SO, execute o script a seguir no Azure PowerShell, embora você deva [configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) primeiro.</span><span class="sxs-lookup"><span data-stu-id="7aecd-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="7aecd-119">Para saber mais sobre o script, consulte [Fim da vida útil da família 1 dos sistemas operacionais convidados do Azure: junho de 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="7aecd-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="7aecd-120">Os serviços de nuvem serão afetados pela desativação da família 1 do sistema operacional se a coluna osFamily na saída do script estiver vazia ou contiver um "1".</span><span class="sxs-lookup"><span data-stu-id="7aecd-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="7aecd-121">Recomendações se você for afetado</span><span class="sxs-lookup"><span data-stu-id="7aecd-121">Recommendations if you are affected</span></span>
<span data-ttu-id="7aecd-122">Recomendamos que você migre suas funções de serviço de nuvem para uma das famílias dos sistemas operacionais convidados com suporte:</span><span class="sxs-lookup"><span data-stu-id="7aecd-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="7aecd-123">**Família 4.x dos SOs convidados** - Windows Server 2012 R2 *(recomendado)*</span><span class="sxs-lookup"><span data-stu-id="7aecd-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="7aecd-124">Certifique-se de que seu aplicativo esteja usando o SDK 2.1 ou posterior com o .NET Framework 4.0, 4.5 ou 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="7aecd-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="7aecd-125">Defina o atributo osFamily para "4" no arquivo ServiceConfiguration.cscfg e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7aecd-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7aecd-126">**Família 3.x dos SOs convidados** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7aecd-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="7aecd-127">Certifique-se de que seu aplicativo esteja usando o SDK 1.8 ou posterior com o .NET Framework 4.0 ou 4.5.</span><span class="sxs-lookup"><span data-stu-id="7aecd-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="7aecd-128">Defina o atributo osFamily como "3" no arquivo ServiceConfiguration.cscfg e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7aecd-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7aecd-129">**Família 2.x dos SOs convidados** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7aecd-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="7aecd-130">Certifique-se de que seu aplicativo esteja usando o SDK 1.3 e posterior com o .NET Framework 3.5 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="7aecd-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="7aecd-131">Defina o atributo osFamily para "2" no arquivo ServiceConfiguration.cscfg e reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7aecd-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="7aecd-132">O suporte estendido para a Família 1 dos sistemas operacionais convidados terminou em 3 de novembro de 2014</span><span class="sxs-lookup"><span data-stu-id="7aecd-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="7aecd-133">Não há mais suporte para serviços de nuvem na família 1 dos sistemas operacionais convidados.</span><span class="sxs-lookup"><span data-stu-id="7aecd-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="7aecd-134">Migre da família 1 assim que possível para evitar a interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="7aecd-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7aecd-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7aecd-135">Next steps</span></span>
<span data-ttu-id="7aecd-136">Examine as últimas [versões do SO convidado](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="7aecd-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
