---
title: "aaaAutoscaling e v1 do ambiente de serviço de aplicativo"
description: "Dimensionamento automático e Ambiente de Serviço de Aplicativo"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="cdf59-103">Dimensionamento automático e Ambiente de Serviço de Aplicativo v1</span><span class="sxs-lookup"><span data-stu-id="cdf59-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="cdf59-104">Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdf59-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="cdf59-105">Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada.</span><span class="sxs-lookup"><span data-stu-id="cdf59-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="cdf59-106">toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="cdf59-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="cdf59-107">Os ambientes de Serviço de Aplicativo do Azure dão suporte ao *dimensionamento automático*.</span><span class="sxs-lookup"><span data-stu-id="cdf59-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="cdf59-108">Você pode dimensionar automaticamente pools de trabalho individuais com base em métricas ou na agenda.</span><span class="sxs-lookup"><span data-stu-id="cdf59-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opções de dimensionamento automático para um pool de trabalho.][intro]

<span data-ttu-id="cdf59-110">Dimensionamento automático otimiza a utilização de recursos automaticamente ampliando e reduzindo uma toofit do ambiente de serviço de aplicativo seu perfil de alocação e a carga.</span><span class="sxs-lookup"><span data-stu-id="cdf59-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="cdf59-111">Configurar o dimensionamento automático de pool de trabalho</span><span class="sxs-lookup"><span data-stu-id="cdf59-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="cdf59-112">Você pode acessar a funcionalidade de dimensionamento automático de saudação do hello **configurações** guia de pool do trabalhador hello.</span><span class="sxs-lookup"><span data-stu-id="cdf59-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Guia de configurações do pool do trabalhador hello.][settings-scale]

<span data-ttu-id="cdf59-114">A partir daí, Olá interface deve ser bastante familiar, pois ele é hello planejar experiência mesmo que você vê quando você dimensionar um aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="cdf59-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![Configurações manuais de escala.][scale-manual]

<span data-ttu-id="cdf59-116">Você também pode configurar um perfil de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="cdf59-116">You can also configure an autoscale profile.</span></span>

![Configurações de dimensionamento automático.][scale-profile]

<span data-ttu-id="cdf59-118">Perfis de AutoEscala são os limites de tooset úteis em sua escala.</span><span class="sxs-lookup"><span data-stu-id="cdf59-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="cdf59-119">Dessa forma, você pode ter uma experiência de desempenho consistente, definindo um valor de escala de limite inferior (1) e um limite de gastos previsível, definindo um limite superior (2).</span><span class="sxs-lookup"><span data-stu-id="cdf59-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Configurações de escala no perfil.][scale-profile2]

<span data-ttu-id="cdf59-121">Depois de definir um perfil, você pode adicionar tooscale de regras de dimensionamento automático para cima ou para baixo número de saudação de instâncias no pool do trabalhador hello dentro dos limites de saudação definidas pelo perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdf59-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="cdf59-122">As regras de dimensionamento automático se baseiam em métricas.</span><span class="sxs-lookup"><span data-stu-id="cdf59-122">Autoscale rules are based on metrics.</span></span>

![Regra de escala.][scale-rule]

 <span data-ttu-id="cdf59-124">Nenhum pool de trabalho ou a métrica de front-end pode ser usado toodefine regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="cdf59-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="cdf59-125">Essas métricas são Olá mesmas métricas, você pode monitorar nos gráficos de folha de recursos de saudação ou definir alertas para o.</span><span class="sxs-lookup"><span data-stu-id="cdf59-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="cdf59-126">Exemplo de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="cdf59-126">Autoscale example</span></span>
<span data-ttu-id="cdf59-127">O dimensionamento automático de um ambiente de Serviço de Aplicativo pode ser melhor ilustrado examinando um cenário.</span><span class="sxs-lookup"><span data-stu-id="cdf59-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="cdf59-128">Este artigo explica todas as considerações de saudação necessário ao configurar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="cdf59-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="cdf59-129">Olá artigo o orienta por meio de saudação interações que entram em reproduzir quando fatores de dimensionamento automático ambientes de serviço de aplicativo que são hospedadas em ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdf59-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="cdf59-130">Introdução ao cenário</span><span class="sxs-lookup"><span data-stu-id="cdf59-130">Scenario introduction</span></span>
<span data-ttu-id="cdf59-131">Frank é um sysadmin para uma empresa que foi migrado de uma parte de cargas de trabalho de saudação que gerencia o tooan ambiente de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdf59-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="cdf59-132">Olá ambiente do serviço de aplicativo toomanual dimensionamento configurado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cdf59-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="cdf59-133">**Front-ends:** 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-133">**Front ends:** 3</span></span>
* <span data-ttu-id="cdf59-134">**Pool de trabalho 1**: 10</span><span class="sxs-lookup"><span data-stu-id="cdf59-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="cdf59-135">**Pool de trabalho 2:**5</span><span class="sxs-lookup"><span data-stu-id="cdf59-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="cdf59-136">**Pool de trabalho 3:**5</span><span class="sxs-lookup"><span data-stu-id="cdf59-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="cdf59-137">O pool de trabalho 1 é usado para cargas de trabalho de produção, embora o pool de trabalho 2 e o pool de trabalho 3 sejam usados para garantia de qualidade (QA) e cargas de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="cdf59-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="cdf59-138">Olá aplicativo planos de serviço para controle de qualidade e desenvolvimento são configurados toomanual escala.</span><span class="sxs-lookup"><span data-stu-id="cdf59-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="cdf59-139">plano de serviço de aplicativo de produção de Hello é definida toodeal tooautoscale com variações de carga e o tráfego.</span><span class="sxs-lookup"><span data-stu-id="cdf59-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="cdf59-140">Frank esteja familiarizado com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cdf59-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="cdf59-141">Ele conhece o horário de pico de saudação de carga é entre 9:00 AM e 6:00 PM porque este é um aplicativo de (LOB) de linha de negócios que os funcionários usam enquanto estiverem no escritório de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdf59-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="cdf59-142">O uso é reduzido depois disso, quando os usuários param de trabalhar naquele dia.</span><span class="sxs-lookup"><span data-stu-id="cdf59-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="cdf59-143">Fora do horário de pico, ainda há alguma carga porque os usuários podem acessar o aplicativo hello remotamente usando seus dispositivos móveis ou computadores domésticos.</span><span class="sxs-lookup"><span data-stu-id="cdf59-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="cdf59-144">produção de Hello plano de serviço de aplicativo já está configurado tooautoscale com base no uso da CPU com hello regras a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdf59-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![Configurações específicas para o aplicativo LOB.][asp-scale]

| <span data-ttu-id="cdf59-146">**Perfil de dimensionamento automático – Dias da semana – plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="cdf59-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="cdf59-147">**Perfil de dimensionamento automático – Finais de semana – plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="cdf59-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="cdf59-148">**Nome:** Perfil de dia da semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="cdf59-149">**Nome:** Perfil de final de semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="cdf59-150">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="cdf59-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="cdf59-151">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="cdf59-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="cdf59-152">**Perfil:** Dias da semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="cdf59-153">**Perfil:** Final de semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="cdf59-154">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="cdf59-154">**Type:** Recurrence</span></span> |<span data-ttu-id="cdf59-155">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="cdf59-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="cdf59-156">**Intervalo de destino:** 5 instâncias too20</span><span class="sxs-lookup"><span data-stu-id="cdf59-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="cdf59-157">**Intervalo de destino:** 3 instâncias too10</span><span class="sxs-lookup"><span data-stu-id="cdf59-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="cdf59-158">**Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira</span><span class="sxs-lookup"><span data-stu-id="cdf59-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="cdf59-159">**Dias:** sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="cdf59-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="cdf59-160">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="cdf59-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="cdf59-161">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="cdf59-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="cdf59-162">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="cdf59-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="cdf59-163">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="cdf59-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="cdf59-164">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="cdf59-165">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="cdf59-166">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="cdf59-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="cdf59-167">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="cdf59-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="cdf59-168">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-168">**Metric:** CPU %</span></span> |<span data-ttu-id="cdf59-169">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="cdf59-170">**Operação:** Mais de 60%</span><span class="sxs-lookup"><span data-stu-id="cdf59-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="cdf59-171">**Operação:** Mais de 80%</span><span class="sxs-lookup"><span data-stu-id="cdf59-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="cdf59-172">**Duração:** 5 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="cdf59-173">**Duração:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="cdf59-174">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="cdf59-175">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-176">**Ação:** Aumentar a contagem em 2</span><span class="sxs-lookup"><span data-stu-id="cdf59-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="cdf59-177">**Ação:** Aumentar a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="cdf59-178">**Tempo de resfriamento (minutos):** 15</span><span class="sxs-lookup"><span data-stu-id="cdf59-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="cdf59-179">**Tempo de resfriamento (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="cdf59-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="cdf59-180">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="cdf59-181">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="cdf59-182">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="cdf59-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="cdf59-183">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="cdf59-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="cdf59-184">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-184">**Metric:** CPU %</span></span> |<span data-ttu-id="cdf59-185">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="cdf59-186">**Operação:** Menos de 30%</span><span class="sxs-lookup"><span data-stu-id="cdf59-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="cdf59-187">**Operação:** Menos de 20%</span><span class="sxs-lookup"><span data-stu-id="cdf59-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="cdf59-188">**Duração:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="cdf59-189">**Duração:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="cdf59-190">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="cdf59-191">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-192">**Ação:** Reduzir a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="cdf59-193">**Ação:** Reduzir a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="cdf59-194">**Tempo de resfriamento (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="cdf59-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="cdf59-195">**Tempo de resfriamento (minutos):** 10</span><span class="sxs-lookup"><span data-stu-id="cdf59-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="cdf59-196">Taxa de inflação do plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cdf59-196">App Service plan inflation rate</span></span>
<span data-ttu-id="cdf59-197">Planos de serviço de aplicativo configurado tooautoscale fazê-lo a uma taxa máxima por hora.</span><span class="sxs-lookup"><span data-stu-id="cdf59-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="cdf59-198">Essa taxa pode ser calculada com base em valores de saudação fornecidos na regra de dimensionamento automático hello.</span><span class="sxs-lookup"><span data-stu-id="cdf59-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="cdf59-199">Compreendendo e calcular Olá *taxa de inflação do plano de serviço de aplicativo* é importante para dimensionamento automático do ambiente do serviço de aplicativo porque o pool de trabalho de tooa de alterações de escala não são instantâneos.</span><span class="sxs-lookup"><span data-stu-id="cdf59-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="cdf59-200">Olá taxa de inflação do plano de serviço de aplicativo é calculada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cdf59-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![Cálculo da taxa de inflação do plano do Serviço de Aplicativo.][ASP-Inflation]

<span data-ttu-id="cdf59-202">Com base em Olá AutoEscala – escala a regra para o perfil de dia da semana de saudação do plano de serviço de aplicativo de produção de hello:</span><span class="sxs-lookup"><span data-stu-id="cdf59-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation1]

<span data-ttu-id="cdf59-204">No caso de saudação de saudação AutoEscala – regra aumentar para perfil de fim de semana de saudação de plano de serviço de aplicativo de produção de hello fórmula Olá deve resolver para:</span><span class="sxs-lookup"><span data-stu-id="cdf59-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para finais de semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation2]

<span data-ttu-id="cdf59-206">Esse valor também pode ser calculado para operações de redução.</span><span class="sxs-lookup"><span data-stu-id="cdf59-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="cdf59-207">Com base em Olá AutoEscala – regra de escala para baixo para o perfil de dia da semana de saudação de produção de hello plano de serviço de aplicativo, isso seria semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="cdf59-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation3]

<span data-ttu-id="cdf59-209">No caso de saudação de saudação AutoEscala – regra de escala para baixo para o perfil de fim de semana de saudação de plano de serviço de aplicativo de produção de hello fórmula Olá deve resolver para:</span><span class="sxs-lookup"><span data-stu-id="cdf59-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![Taxa de inflação de plano do Serviço de Aplicativo para fins de semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation4]

<span data-ttu-id="cdf59-211">plano de serviço de aplicativo de produção de Hello pode crescer em uma taxa máxima de oito instâncias por hora durante a semana hello e quatro instâncias por hora durante a fim de semana de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdf59-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="cdf59-212">Ele pode liberar instâncias em uma taxa máxima de quatro instâncias por hora durante a semana hello e seis instâncias por hora durante a semana.</span><span class="sxs-lookup"><span data-stu-id="cdf59-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="cdf59-213">Se vários planos de serviço de aplicativo estão hospedados em um pool de trabalho, você terá Olá toocalculate *taxa total de inflação* como soma Olá Olá inflação da taxa de saudação todos os planos de serviço de aplicativo que estão sendo hospedagem nesse pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cdf59-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![Cálculo da taxa total de inflação para vários planos do Serviço de Aplicativo hospedados em um pool de trabalho.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="cdf59-215">Saudação de uso do serviço de aplicativo planejar as regras de AutoEscala pool de trabalho toodefine taxa de inflação</span><span class="sxs-lookup"><span data-stu-id="cdf59-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="cdf59-216">Pools de trabalho que hospedam planos de serviço de aplicativo tooautoscale configurado necessário para alocar um buffer de capacidade.</span><span class="sxs-lookup"><span data-stu-id="cdf59-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="cdf59-217">buffer de saudação permite Olá toogrow de operações de dimensionamento automático e reduzir o plano de serviço de aplicativo, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="cdf59-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="cdf59-218">buffer mínimo Olá seria Olá calculado aplicativo serviço planejar inflação taxa Total.</span><span class="sxs-lookup"><span data-stu-id="cdf59-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="cdf59-219">Como as operações de dimensionamento de ambiente de serviço de aplicativo levam algum tempo tooapply, qualquer alteração deve levar em consideração para outras alterações de demanda que podem acontecer enquanto uma operação em escala está em andamento.</span><span class="sxs-lookup"><span data-stu-id="cdf59-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="cdf59-220">tooaccommodate essa latência, recomendamos que você use Olá calculado aplicativo serviço planejar inflação taxa Total como o número mínimo de saudação de instâncias que são adicionados para cada operação de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="cdf59-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="cdf59-221">Com essas informações, Frank pode definir Olá perfil de AutoEscala e regras a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdf59-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![Regras de perfil de dimensionamento automático para o exemplo LOB.][Worker-Pool-Scale]

| <span data-ttu-id="cdf59-223">**Perfil de dimensionamento automático – Dias da semana**</span><span class="sxs-lookup"><span data-stu-id="cdf59-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="cdf59-224">**Perfil de dimensionamento automático – Finais de semana**</span><span class="sxs-lookup"><span data-stu-id="cdf59-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="cdf59-225">**Nome:** Perfil de dia da semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="cdf59-226">**Nome:** Perfil de final de semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="cdf59-227">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="cdf59-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="cdf59-228">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="cdf59-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="cdf59-229">**Perfil:** Dias da semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="cdf59-230">**Perfil:** Final de semana</span><span class="sxs-lookup"><span data-stu-id="cdf59-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="cdf59-231">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="cdf59-231">**Type:** Recurrence</span></span> |<span data-ttu-id="cdf59-232">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="cdf59-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="cdf59-233">**Intervalo de destino:** 13 instâncias too25</span><span class="sxs-lookup"><span data-stu-id="cdf59-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="cdf59-234">**Intervalo de destino:** 6 instâncias too15</span><span class="sxs-lookup"><span data-stu-id="cdf59-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="cdf59-235">**Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira</span><span class="sxs-lookup"><span data-stu-id="cdf59-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="cdf59-236">**Dias:** sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="cdf59-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="cdf59-237">**Hora de início:** 7:00</span><span class="sxs-lookup"><span data-stu-id="cdf59-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="cdf59-238">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="cdf59-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="cdf59-239">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="cdf59-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="cdf59-240">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="cdf59-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="cdf59-241">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="cdf59-242">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="cdf59-243">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="cdf59-244">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="cdf59-245">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="cdf59-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="cdf59-246">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="cdf59-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="cdf59-247">**Operação:** menos de 8</span><span class="sxs-lookup"><span data-stu-id="cdf59-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="cdf59-248">**Operação:** menos de 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="cdf59-249">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="cdf59-250">**Duração:** 30 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="cdf59-251">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="cdf59-252">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-253">**Ação:** Aumentar a contagem em 8</span><span class="sxs-lookup"><span data-stu-id="cdf59-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="cdf59-254">**Ação:** Aumentar a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="cdf59-255">**Tempo de resfriamento (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="cdf59-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="cdf59-256">**Tempo de resfriamento (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="cdf59-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="cdf59-257">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="cdf59-258">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="cdf59-259">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="cdf59-260">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="cdf59-261">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="cdf59-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="cdf59-262">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="cdf59-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="cdf59-263">**Operação:** maior que 8</span><span class="sxs-lookup"><span data-stu-id="cdf59-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="cdf59-264">**Operação:** maior que 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="cdf59-265">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="cdf59-266">**Duração:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="cdf59-267">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="cdf59-268">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-269">**Ação:** Diminuir a contagem em 2</span><span class="sxs-lookup"><span data-stu-id="cdf59-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="cdf59-270">**Ação:** Diminuir a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="cdf59-271">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="cdf59-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="cdf59-272">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="cdf59-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="cdf59-273">Olá definido no perfil de saudação do intervalo de destino é calculado com instâncias de mínimo Olá definidas no perfil de saudação plano de serviço de aplicativo + buffer.</span><span class="sxs-lookup"><span data-stu-id="cdf59-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="cdf59-274">intervalo máximo de saudação seria soma de saudação de todos os intervalos de saudação máximo de todos os planos de serviço de aplicativo hospedados no pool do trabalhador hello.</span><span class="sxs-lookup"><span data-stu-id="cdf59-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="cdf59-275">Olá contagem de aumento de escala Olá as regras de deve ser conjunto tooat pelo menos 1 X a taxa de inflação de plano de serviço aplicativo para escala para cima.</span><span class="sxs-lookup"><span data-stu-id="cdf59-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="cdf59-276">Contagem de redução pode ser ajustada toosomething entre 1/2 X ou 1 X Olá planejar taxa de inflação de serviço de aplicativo para a escala para baixo.</span><span class="sxs-lookup"><span data-stu-id="cdf59-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="cdf59-277">Dimensionamento automático para o pool de front-end</span><span class="sxs-lookup"><span data-stu-id="cdf59-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="cdf59-278">As regras de dimensionamento automático de front-end são mais simples para pools de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cdf59-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="cdf59-279">Basicamente, você deve</span><span class="sxs-lookup"><span data-stu-id="cdf59-279">Primarily, you should</span></span>  
<span data-ttu-id="cdf59-280">Certifique-se de que duração de medida de saudação e temporizadores de cooldown Olá considerar que as operações de escala em um plano de serviço de aplicativo não são instantâneas.</span><span class="sxs-lookup"><span data-stu-id="cdf59-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="cdf59-281">Para este cenário, Frank sabe que a taxa de erro Olá aumenta após front-ends atingir 80% de utilização da CPU e define Olá AutoEscala instâncias de tooincrease regra da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cdf59-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![Configurações de dimensionamento automático para o pool de front-end.][Front-End-Scale]

| <span data-ttu-id="cdf59-283">**Perfil de dimensionamento automático – Front-ends**</span><span class="sxs-lookup"><span data-stu-id="cdf59-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="cdf59-284">**Nome:** Dimensionamento automático – Front-ends</span><span class="sxs-lookup"><span data-stu-id="cdf59-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="cdf59-285">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="cdf59-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="cdf59-286">**Perfil:** Todos os dias</span><span class="sxs-lookup"><span data-stu-id="cdf59-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="cdf59-287">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="cdf59-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="cdf59-288">**Intervalo de destino:** 3 instâncias too10</span><span class="sxs-lookup"><span data-stu-id="cdf59-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="cdf59-289">**Dias:** Todos os dias</span><span class="sxs-lookup"><span data-stu-id="cdf59-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="cdf59-290">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="cdf59-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="cdf59-291">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="cdf59-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="cdf59-292">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="cdf59-293">**Recurso:** Pool de front-end</span><span class="sxs-lookup"><span data-stu-id="cdf59-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="cdf59-294">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="cdf59-295">**Operação:** Mais de 60%</span><span class="sxs-lookup"><span data-stu-id="cdf59-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="cdf59-296">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="cdf59-297">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-298">**Ação:** Aumentar a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="cdf59-299">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="cdf59-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="cdf59-300">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="cdf59-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="cdf59-301">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="cdf59-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="cdf59-302">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="cdf59-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="cdf59-303">**Operação:** Menos de 30%</span><span class="sxs-lookup"><span data-stu-id="cdf59-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="cdf59-304">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="cdf59-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="cdf59-305">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="cdf59-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="cdf59-306">**Ação:** Diminuir a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="cdf59-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="cdf59-307">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="cdf59-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
