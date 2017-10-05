---
title: "Introdução ao dimensionamento automático usando métricas personalizadas no Azure | Microsoft Docs"
description: "Saiba como dimensionar seu recurso usando métricas personalizadas no Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: de8f7acadc282e4b81c657b1723f00fd3e5fd4f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="55182-103">Introdução ao dimensionamento automático usando métricas personalizadas no Azure</span><span class="sxs-lookup"><span data-stu-id="55182-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="55182-104">Este artigo descreve como dimensionar seu recurso usando métricas personalizadas no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55182-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="55182-105">O dimensionamento automático do Azure Monitor se aplica somente aos VMSS (Conjuntos de Dimensionamento da Máquina Virtual), aos serviços de nuvem, aos planos do Serviço de Aplicativo e aos ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55182-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="55182-106">Vamos começar</span><span class="sxs-lookup"><span data-stu-id="55182-106">Lets get started</span></span>
<span data-ttu-id="55182-107">Este artigo pressupõe que você tenha um aplicativo Web com o Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="55182-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="55182-108">Se ainda não tiver um, você poderá [configurar o Application Insights para seu site do ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="55182-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="55182-109">Abra o [portal do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="55182-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="55182-110">Clique no ícone do Azure Monitor no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="55182-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="55182-111">![Inicie o Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="55182-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="55182-112">Clique na configuração do dimensionamento automático para exibir todos os recursos a que ele se aplica, bem como o status de dimensionamento automático atual ![Descobrir o dimensionamento automático no Azure Monitor][4]</span><span class="sxs-lookup"><span data-stu-id="55182-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="55182-113">Abra a folha “Dimensionamento Automático” no Azure Monitor e selecione um recurso que deseja dimensionar</span><span class="sxs-lookup"><span data-stu-id="55182-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="55182-114">Observação: as etapas a seguir usam um plano do serviço de aplicativo associado a um aplicativo Web que tem o Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="55182-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="55182-115">Na folha de configuração de dimensionamento para o recurso, observe que a contagem de instâncias atual é 1.</span><span class="sxs-lookup"><span data-stu-id="55182-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="55182-116">Clique em “Habilitar dimensionamento automático”.</span><span class="sxs-lookup"><span data-stu-id="55182-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="55182-117">![Configuração de dimensionamento para um novo aplicativo Web][5]</span><span class="sxs-lookup"><span data-stu-id="55182-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="55182-118">Forneça um nome para a configuração de dimensionamento e clique em "Adicionar uma regra".</span><span class="sxs-lookup"><span data-stu-id="55182-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="55182-119">Observe as opções de regra de dimensionamento que são abertas como um painel de contexto no lado direito.</span><span class="sxs-lookup"><span data-stu-id="55182-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="55182-120">Por padrão, ele define a opção de dimensionar sua contagem de instâncias em 1 se o percentual de CPU do recurso ultrapassar 70%.</span><span class="sxs-lookup"><span data-stu-id="55182-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="55182-121">Altere a origem da métrica na parte superior para "Application Insights", selecione o recurso do Application Insights na lista suspensa “Recurso” e, em seguida, selecione a métrica personalizada com base na qual você deseja fazer o dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="55182-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="55182-122">![Dimensionamento por métrica personalizada][6]</span><span class="sxs-lookup"><span data-stu-id="55182-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="55182-123">De forma semelhante à etapa anterior, adicione uma regra de dimensionamento que reduzirá horizontalmente e diminuirá a contagem de escala em 1 se a métrica personalizada estiver abaixo do limite.</span><span class="sxs-lookup"><span data-stu-id="55182-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="55182-124">![Dimensionamento com base na CPU][7]</span><span class="sxs-lookup"><span data-stu-id="55182-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="55182-125">Defina os limites de sua instância.</span><span class="sxs-lookup"><span data-stu-id="55182-125">Set the you instance limits.</span></span> <span data-ttu-id="55182-126">Por exemplo, se quiser dimensionar entre 2 e 5 instâncias, dependendo das flutuações da métrica personalizada, defina “mínimo” como “2”, “máximo” como “5” e “padrão” como “2”</span><span class="sxs-lookup"><span data-stu-id="55182-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="55182-127">Observação: caso haja algum problema ao ler as métricas do recurso e a capacidade atual esteja abaixo da capacidade padrão, a fim de garantir a disponibilidade do recurso o dimensionamento automático escalará horizontalmente para o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="55182-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="55182-128">Se a capacidade atual já for maior que a capacidade padrão, o dimensionamento automático não reduzirá horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="55182-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="55182-129">Clique em "Salvar"</span><span class="sxs-lookup"><span data-stu-id="55182-129">Click on 'Save'</span></span>

<span data-ttu-id="55182-130">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="55182-130">Congratulations.</span></span> <span data-ttu-id="55182-131">Você criou com êxito sua configuração de dimensionamento para fazer o dimensionamento automático de seu aplicativo Web com base em uma métrica personalizada.</span><span class="sxs-lookup"><span data-stu-id="55182-131">You now now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="55182-132">Observação: as mesmas etapas são aplicáveis para começar a usar uma função de serviço de nuvem ou VMSS.</span><span class="sxs-lookup"><span data-stu-id="55182-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
