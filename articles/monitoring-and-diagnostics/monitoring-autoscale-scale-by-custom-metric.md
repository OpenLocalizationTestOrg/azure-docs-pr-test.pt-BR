---
title: "aaaGet iniciado com escala automática por métrica personalizada no Azure | Microsoft Docs"
description: "Saiba como tooscale o recurso por métrica personalizada no Azure."
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
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="f8512-103">Introdução ao dimensionamento automático usando métricas personalizadas no Azure</span><span class="sxs-lookup"><span data-stu-id="f8512-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="f8512-104">Este artigo descreve como tooscale o recurso por uma métrica personalizada no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8512-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="f8512-105">Azure AutoEscala Monitor aplica-se apenas tooVirtual conjuntos de escala de máquina (VMSS), os serviços de nuvem, planos de serviço de aplicativo e ambientes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8512-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="f8512-106">Vamos começar</span><span class="sxs-lookup"><span data-stu-id="f8512-106">Lets get started</span></span>
<span data-ttu-id="f8512-107">Este artigo pressupõe que você tenha um aplicativo Web com o Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="f8512-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="f8512-108">Se ainda não tiver um, você poderá [configurar o Application Insights para seu site do ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="f8512-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="f8512-109">Abra o [portal do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="f8512-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="f8512-110">Clique no ícone de Monitor do Azure no painel de navegação esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="f8512-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="f8512-111">![Inicie o Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="f8512-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="f8512-112">Clique em configuração tooview todos os recursos de saudação automática escala é aplicável, juntamente com seu status atual de dimensionamento automático de dimensionamento automático ![descobrir AutoEscala no monitor do Azure][4]</span><span class="sxs-lookup"><span data-stu-id="f8512-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="f8512-113">Abra a folha de 'dimensionamento automático' no Monitor do Azure e selecione um recurso que você deseja tooscale</span><span class="sxs-lookup"><span data-stu-id="f8512-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="f8512-114">Observação: etapas Olá usam um plano de serviço de aplicativo associado a um aplicativo web que tem informações de aplicativo configuradas.</span><span class="sxs-lookup"><span data-stu-id="f8512-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="f8512-115">Na folha de configuração de escala de Olá para o recurso de hello, observe que a contagem atual de instâncias de saudação é 1.</span><span class="sxs-lookup"><span data-stu-id="f8512-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="f8512-116">Clique em “Habilitar dimensionamento automático”.</span><span class="sxs-lookup"><span data-stu-id="f8512-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="f8512-117">![Configuração de dimensionamento para um novo aplicativo Web][5]</span><span class="sxs-lookup"><span data-stu-id="f8512-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="f8512-118">Forneça um nome para configuração da escala de saudação e hello, clique em "Adicionar uma regra".</span><span class="sxs-lookup"><span data-stu-id="f8512-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="f8512-119">Observe as opções de regra de escala de saudação que é aberto em um painel de contexto no lado direito hello.</span><span class="sxs-lookup"><span data-stu-id="f8512-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="f8512-120">Por padrão, ele define Olá opção tooscale sua instância de contagem em 1 se percetage de CPU de saudação do recurso de saudação exceder 70%.</span><span class="sxs-lookup"><span data-stu-id="f8512-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="f8512-121">Alterar origem métrica de saudação na parte superior da saudação muito "Application Insights", selecione Olá recurso insights de aplicativo hello 'Resource' suspenso e métrica personalizada de hello, em seguida, selecione com base no qual você deseja tooscale.</span><span class="sxs-lookup"><span data-stu-id="f8512-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="f8512-122">![Dimensionamento por métrica personalizada][6]</span><span class="sxs-lookup"><span data-stu-id="f8512-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="f8512-123">Semelhante toohello de etapa anterior, adicione uma regra de escala que ampliar e reduzir a contagem de escala de saudação por 1 se a métrica personalizada Olá estiver abaixo do limite.</span><span class="sxs-lookup"><span data-stu-id="f8512-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="f8512-124">![Dimensionamento com base na CPU][7]</span><span class="sxs-lookup"><span data-stu-id="f8512-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="f8512-125">Definir Olá instância limites.</span><span class="sxs-lookup"><span data-stu-id="f8512-125">Set hello you instance limits.</span></span> <span data-ttu-id="f8512-126">Por exemplo, se você quiser tooscale entre instâncias de 2 a 5 dependendo flutuações de métrica personalizada hello, definir muito '2', 'mínimo' 'máximo' muito '5' e 'default' muito '2'</span><span class="sxs-lookup"><span data-stu-id="f8512-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="f8512-127">Observação: caso há um problema ao ler as métricas de recurso hello e capacidade atual hello está abaixo de capacidade padrão de Olá, em seguida, tooensure disponibilidade de saudação do recurso Olá, AutoEscala será escalável valor padrão de toohello.</span><span class="sxs-lookup"><span data-stu-id="f8512-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="f8512-128">Se a capacidade atual Olá já for maior que a capacidade padrão, dimensionamento automático não será dimensionado em.</span><span class="sxs-lookup"><span data-stu-id="f8512-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="f8512-129">Clique em "Salvar"</span><span class="sxs-lookup"><span data-stu-id="f8512-129">Click on 'Save'</span></span>

<span data-ttu-id="f8512-130">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="f8512-130">Congratulations.</span></span> <span data-ttu-id="f8512-131">Agora, com êxito criado seu tooauto de configuração de escala dimensionar seu aplicativo web com base em uma métrica personalizada.</span><span class="sxs-lookup"><span data-stu-id="f8512-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="f8512-132">Observação: hello mesmas etapas são aplicável tooget iniciado com uma função de serviço VMSS ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f8512-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
