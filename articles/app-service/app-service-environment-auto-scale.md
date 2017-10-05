---
title: "Dimensionamento automático e Ambiente de Serviço de Aplicativo v1"
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
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="d66a0-103">Dimensionamento automático e Ambiente de Serviço de Aplicativo v1</span><span class="sxs-lookup"><span data-stu-id="d66a0-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="d66a0-104">Este artigo é sobre o Ambiente do Serviço de Aplicativo v1.</span><span class="sxs-lookup"><span data-stu-id="d66a0-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="d66a0-105">Há uma versão mais recente do Ambiente do Serviço de Aplicativo que é mais fácil de usar e é executada em infraestrutura mais avançada.</span><span class="sxs-lookup"><span data-stu-id="d66a0-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="d66a0-106">Para saber mais sobre o novo início de versão com o [Introdução ao Ambiente do Serviço de Aplicativo](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="d66a0-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="d66a0-107">Os ambientes de Serviço de Aplicativo do Azure dão suporte ao *dimensionamento automático*.</span><span class="sxs-lookup"><span data-stu-id="d66a0-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="d66a0-108">Você pode dimensionar automaticamente pools de trabalho individuais com base em métricas ou na agenda.</span><span class="sxs-lookup"><span data-stu-id="d66a0-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Opções de dimensionamento automático para um pool de trabalho.][intro]

<span data-ttu-id="d66a0-110">O dimensionamento automático otimiza a utilização de recursos, escalar e reduzir verticalmente um ambiente de Serviço de Aplicativo de forma automática para ajustar seu orçamento e/ou perfil de carregamento.</span><span class="sxs-lookup"><span data-stu-id="d66a0-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="d66a0-111">Configurar o dimensionamento automático de pool de trabalho</span><span class="sxs-lookup"><span data-stu-id="d66a0-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="d66a0-112">Você pode acessar a funcionalidade de dimensionamento automático na guia **Configurações** do pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d66a0-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Guia de configurações do pool de trabalho.][settings-scale]

<span data-ttu-id="d66a0-114">A partir daí, a interface deve ser bastante familiar, já que é a mesma experiência que você vê quando dimensiona um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d66a0-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![Configurações manuais de escala.][scale-manual]

<span data-ttu-id="d66a0-116">Você também pode configurar um perfil de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d66a0-116">You can also configure an autoscale profile.</span></span>

![Configurações de dimensionamento automático.][scale-profile]

<span data-ttu-id="d66a0-118">Os perfis de dimensionamento automático são úteis para definir limites na sua escala.</span><span class="sxs-lookup"><span data-stu-id="d66a0-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="d66a0-119">Dessa forma, você pode ter uma experiência de desempenho consistente, definindo um valor de escala de limite inferior (1) e um limite de gastos previsível, definindo um limite superior (2).</span><span class="sxs-lookup"><span data-stu-id="d66a0-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Configurações de escala no perfil.][scale-profile2]

<span data-ttu-id="d66a0-121">Depois de definir um perfil, você pode adicionar regras de dimensionamento automático para aumentar ou reduzir o número de instâncias no pool de trabalho dentro dos limites definidos pelo perfil.</span><span class="sxs-lookup"><span data-stu-id="d66a0-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="d66a0-122">As regras de dimensionamento automático se baseiam em métricas.</span><span class="sxs-lookup"><span data-stu-id="d66a0-122">Autoscale rules are based on metrics.</span></span>

![Regra de escala.][scale-rule]

 <span data-ttu-id="d66a0-124">Qualquer métrica de pool de trabalho ou de front-end pode ser usada para definir regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d66a0-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="d66a0-125">Essas métricas são as mesmas que você pode monitorar nos gráficos de folha de recursos e para as quais pode definir alertas.</span><span class="sxs-lookup"><span data-stu-id="d66a0-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="d66a0-126">Exemplo de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="d66a0-126">Autoscale example</span></span>
<span data-ttu-id="d66a0-127">O dimensionamento automático de um ambiente de Serviço de Aplicativo pode ser melhor ilustrado examinando um cenário.</span><span class="sxs-lookup"><span data-stu-id="d66a0-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="d66a0-128">Este artigo explica todas as considerações necessárias ao configurar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d66a0-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="d66a0-129">Este artigo aborda as interações que entram em jogo quando você fatora em ambientes de Serviço de Aplicativo de dimensionamento automático hospedados no Ambiente de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d66a0-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="d66a0-130">Introdução ao cenário</span><span class="sxs-lookup"><span data-stu-id="d66a0-130">Scenario introduction</span></span>
<span data-ttu-id="d66a0-131">Matheus é um SysAdmin de uma empresa que migrou uma parte das cargas de trabalho que ele gerencia para um ambiente de Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d66a0-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="d66a0-132">O ambiente do Serviço de Aplicativo está configurado para a escala manual da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d66a0-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="d66a0-133">**Front-ends:** 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-133">**Front ends:** 3</span></span>
* <span data-ttu-id="d66a0-134">**Pool de trabalho 1**: 10</span><span class="sxs-lookup"><span data-stu-id="d66a0-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="d66a0-135">**Pool de trabalho 2:**5</span><span class="sxs-lookup"><span data-stu-id="d66a0-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="d66a0-136">**Pool de trabalho 3:**5</span><span class="sxs-lookup"><span data-stu-id="d66a0-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="d66a0-137">O pool de trabalho 1 é usado para cargas de trabalho de produção, embora o pool de trabalho 2 e o pool de trabalho 3 sejam usados para garantia de qualidade (QA) e cargas de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d66a0-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="d66a0-138">Os Planos do Serviço de Aplicativo para controle de qualidade e desenvolvimento são configurados para escala manual.</span><span class="sxs-lookup"><span data-stu-id="d66a0-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="d66a0-139">O Plano do Serviço de Aplicativo de produção é definido para dimensionamento automático para lidar com variações de carga e tráfego.</span><span class="sxs-lookup"><span data-stu-id="d66a0-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="d66a0-140">Matheus está familiarizado com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d66a0-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="d66a0-141">Ele sabe que as horas de pico de carga ocorrem entre 9:00 e 18:00, porque este é um aplicativo de linha de negócios (LOB) que os funcionários usam enquanto estão no escritório.</span><span class="sxs-lookup"><span data-stu-id="d66a0-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="d66a0-142">O uso é reduzido depois disso, quando os usuários param de trabalhar naquele dia.</span><span class="sxs-lookup"><span data-stu-id="d66a0-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="d66a0-143">Fora do horário de pico, ainda há alguma carga porque os usuários podem acessar o aplicativo remotamente, usando seus dispositivos móveis ou computadores domésticos.</span><span class="sxs-lookup"><span data-stu-id="d66a0-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="d66a0-144">O plano do Serviço de Aplicativo de produção já está configurado para dimensionamento automático com base no uso de CPU com as seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="d66a0-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![Configurações específicas para o aplicativo LOB.][asp-scale]

| <span data-ttu-id="d66a0-146">**Perfil de dimensionamento automático – Dias da semana – plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="d66a0-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="d66a0-147">**Perfil de dimensionamento automático – Finais de semana – plano do Serviço de Aplicativo**</span><span class="sxs-lookup"><span data-stu-id="d66a0-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="d66a0-148">**Nome:** Perfil de dia da semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="d66a0-149">**Nome:** Perfil de final de semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="d66a0-150">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="d66a0-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="d66a0-151">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="d66a0-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="d66a0-152">**Perfil:** Dias da semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="d66a0-153">**Perfil:** Final de semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="d66a0-154">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="d66a0-154">**Type:** Recurrence</span></span> |<span data-ttu-id="d66a0-155">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="d66a0-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="d66a0-156">**Intervalo de destino:** 5 a 20 instâncias</span><span class="sxs-lookup"><span data-stu-id="d66a0-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="d66a0-157">**Intervalo de destino:** 3 a 10 instâncias</span><span class="sxs-lookup"><span data-stu-id="d66a0-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="d66a0-158">**Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira</span><span class="sxs-lookup"><span data-stu-id="d66a0-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="d66a0-159">**Dias:** sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="d66a0-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="d66a0-160">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="d66a0-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="d66a0-161">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="d66a0-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="d66a0-162">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="d66a0-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="d66a0-163">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="d66a0-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="d66a0-164">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="d66a0-165">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="d66a0-166">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="d66a0-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="d66a0-167">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="d66a0-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="d66a0-168">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-168">**Metric:** CPU %</span></span> |<span data-ttu-id="d66a0-169">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="d66a0-170">**Operação:** Mais de 60%</span><span class="sxs-lookup"><span data-stu-id="d66a0-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="d66a0-171">**Operação:** Mais de 80%</span><span class="sxs-lookup"><span data-stu-id="d66a0-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="d66a0-172">**Duração:** 5 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="d66a0-173">**Duração:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="d66a0-174">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="d66a0-175">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-176">**Ação:** Aumentar a contagem em 2</span><span class="sxs-lookup"><span data-stu-id="d66a0-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="d66a0-177">**Ação:** Aumentar a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="d66a0-178">**Tempo de resfriamento (minutos):** 15</span><span class="sxs-lookup"><span data-stu-id="d66a0-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="d66a0-179">**Tempo de resfriamento (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="d66a0-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="d66a0-180">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="d66a0-181">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="d66a0-182">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="d66a0-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="d66a0-183">**Recurso:** Produção (ambiente de Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="d66a0-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="d66a0-184">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-184">**Metric:** CPU %</span></span> |<span data-ttu-id="d66a0-185">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="d66a0-186">**Operação:** Menos de 30%</span><span class="sxs-lookup"><span data-stu-id="d66a0-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="d66a0-187">**Operação:** Menos de 20%</span><span class="sxs-lookup"><span data-stu-id="d66a0-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="d66a0-188">**Duração:** 10 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="d66a0-189">**Duração:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="d66a0-190">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="d66a0-191">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-192">**Ação:** Reduzir a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="d66a0-193">**Ação:** Reduzir a contagem em 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="d66a0-194">**Tempo de resfriamento (minutos):** 20</span><span class="sxs-lookup"><span data-stu-id="d66a0-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="d66a0-195">**Tempo de resfriamento (minutos):** 10</span><span class="sxs-lookup"><span data-stu-id="d66a0-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="d66a0-196">Taxa de inflação do plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d66a0-196">App Service plan inflation rate</span></span>
<span data-ttu-id="d66a0-197">Os planos do Serviço de Aplicativo configurados para dimensionamento automático o fazem a uma taxa máxima por hora.</span><span class="sxs-lookup"><span data-stu-id="d66a0-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="d66a0-198">Essa taxa pode ser calculada com base nos valores fornecidos na regra de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d66a0-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="d66a0-199">Compreender e calcular a *taxa de inflação do plano do Serviço de Aplicativo* é importante para o dimensionamento automático do ambiente de Serviço de Aplicativo, já que as alterações de escala em um pool de trabalho não são instantâneas.</span><span class="sxs-lookup"><span data-stu-id="d66a0-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="d66a0-200">A taxa de inflação do plano do Serviço de Aplicativo é calculada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d66a0-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Cálculo da taxa de inflação do plano do Serviço de Aplicativo.][ASP-Inflation]

<span data-ttu-id="d66a0-202">Com base na regra Dimensionamento automático – Escalar verticalmente para o perfil de Dia da semana do Plano do Serviço de Aplicativo de produção:</span><span class="sxs-lookup"><span data-stu-id="d66a0-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation1]

<span data-ttu-id="d66a0-204">No caso da regra Dimensionamento automático - Escalar verticalmente do perfil Finais de semana do plano do Serviço de Aplicativo de produção, a fórmula resolveria para:</span><span class="sxs-lookup"><span data-stu-id="d66a0-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para finais de semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation2]

<span data-ttu-id="d66a0-206">Esse valor também pode ser calculado para operações de redução.</span><span class="sxs-lookup"><span data-stu-id="d66a0-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="d66a0-207">Com base na regra Dimensionamento automático - Reduzir verticalmente do perfil dia da semana perfil do plano do Serviço de Aplicativo de produção, seria semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="d66a0-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation3]

<span data-ttu-id="d66a0-209">No caso da regra Dimensionamento automático - Reduzir verticalmente do perfil Finais de semana do plano do Serviço de Aplicativo de produção, a fórmula resolveria para:</span><span class="sxs-lookup"><span data-stu-id="d66a0-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Taxa de inflação de plano do Serviço de Aplicativo para fins de semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation4]

<span data-ttu-id="d66a0-211">O Plano do Serviço de Aplicativo de produção pode crescer em uma taxa máxima de oito instâncias/hora durante a semana e quatro instâncias/hora durante o fim de semana.</span><span class="sxs-lookup"><span data-stu-id="d66a0-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="d66a0-212">Ele pode liberar instâncias em uma taxa máxima de quatro instâncias/hora durante a semana e seis instâncias/hora durante os finais de semana.</span><span class="sxs-lookup"><span data-stu-id="d66a0-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="d66a0-213">Se vários planos do Serviço de Aplicativo estiverem sendo hospedados em um pool de trabalho, você precisará calcular a *taxa total de inflação* como a soma da taxa de inflação de todos os planos do Serviço de Aplicativo hospedados nesse pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d66a0-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Cálculo da taxa total de inflação para vários planos do Serviço de Aplicativo hospedados em um pool de trabalho.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="d66a0-215">Usar a taxa de inflação do plano do Serviço de Aplicativo para definir regras de dimensionamento automático do pool de trabalho</span><span class="sxs-lookup"><span data-stu-id="d66a0-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="d66a0-216">Os pools de trabalho que hospedam Planos do Serviço de Aplicativo configurados para o dimensionamento automático precisam ter um buffer de capacidade alocado.</span><span class="sxs-lookup"><span data-stu-id="d66a0-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="d66a0-217">O buffer permite que as operações de dimensionamento automático aumentem ou reduzam o plano do Serviço de Aplicativo, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d66a0-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="d66a0-218">O buffer mínimo seria a Taxa de Inflação Total do Plano do Serviço de Aplicativo calculada.</span><span class="sxs-lookup"><span data-stu-id="d66a0-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="d66a0-219">Como as operações de dimensionamento do ambiente de Serviço de Aplicativo demoram algum tempo para serem aplicadas, qualquer alteração deve levar em consideração outras alterações sob demanda que poderiam acontecer enquanto uma operação de escala está em andamento.</span><span class="sxs-lookup"><span data-stu-id="d66a0-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="d66a0-220">Para acomodar essa latência, recomendamos que você use a Taxa de Inflação do Plano do Serviço de Aplicativo Total como o número mínimo de instâncias adicionadas para cada operação de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d66a0-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="d66a0-221">Com essas informações, Matheus pode definir o seguinte perfil e regras de dimensionamento automático:</span><span class="sxs-lookup"><span data-stu-id="d66a0-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![Regras de perfil de dimensionamento automático para o exemplo LOB.][Worker-Pool-Scale]

| <span data-ttu-id="d66a0-223">**Perfil de dimensionamento automático – Dias da semana**</span><span class="sxs-lookup"><span data-stu-id="d66a0-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="d66a0-224">**Perfil de dimensionamento automático – Finais de semana**</span><span class="sxs-lookup"><span data-stu-id="d66a0-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="d66a0-225">**Nome:** Perfil de dia da semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="d66a0-226">**Nome:** Perfil de final de semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="d66a0-227">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="d66a0-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="d66a0-228">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="d66a0-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="d66a0-229">**Perfil:** Dias da semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="d66a0-230">**Perfil:** Final de semana</span><span class="sxs-lookup"><span data-stu-id="d66a0-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="d66a0-231">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="d66a0-231">**Type:** Recurrence</span></span> |<span data-ttu-id="d66a0-232">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="d66a0-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="d66a0-233">**Intervalo de destino:** 13 a 25 instâncias</span><span class="sxs-lookup"><span data-stu-id="d66a0-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="d66a0-234">**Intervalo de destino:** 6 a 15 instâncias</span><span class="sxs-lookup"><span data-stu-id="d66a0-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="d66a0-235">**Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira</span><span class="sxs-lookup"><span data-stu-id="d66a0-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="d66a0-236">**Dias:** sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="d66a0-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="d66a0-237">**Hora de início:** 7:00</span><span class="sxs-lookup"><span data-stu-id="d66a0-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="d66a0-238">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="d66a0-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="d66a0-239">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="d66a0-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="d66a0-240">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="d66a0-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="d66a0-241">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="d66a0-242">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="d66a0-243">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="d66a0-244">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="d66a0-245">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="d66a0-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="d66a0-246">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="d66a0-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="d66a0-247">**Operação:** menos de 8</span><span class="sxs-lookup"><span data-stu-id="d66a0-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="d66a0-248">**Operação:** menos de 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="d66a0-249">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="d66a0-250">**Duração:** 30 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="d66a0-251">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="d66a0-252">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-253">**Ação:** Aumentar a contagem em 8</span><span class="sxs-lookup"><span data-stu-id="d66a0-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="d66a0-254">**Ação:** Aumentar a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="d66a0-255">**Tempo de resfriamento (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="d66a0-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="d66a0-256">**Tempo de resfriamento (minutos):** 180</span><span class="sxs-lookup"><span data-stu-id="d66a0-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="d66a0-257">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="d66a0-258">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="d66a0-259">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="d66a0-260">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="d66a0-261">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="d66a0-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="d66a0-262">**Métrica:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="d66a0-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="d66a0-263">**Operação:** maior que 8</span><span class="sxs-lookup"><span data-stu-id="d66a0-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="d66a0-264">**Operação:** maior que 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="d66a0-265">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="d66a0-266">**Duração:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="d66a0-267">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="d66a0-268">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-269">**Ação:** Diminuir a contagem em 2</span><span class="sxs-lookup"><span data-stu-id="d66a0-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="d66a0-270">**Ação:** Diminuir a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="d66a0-271">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="d66a0-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="d66a0-272">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="d66a0-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="d66a0-273">O intervalo de Destino definido no perfil é calculado pelas instâncias do mínimas definidas no perfil para o plano do Serviço de Aplicativo + buffer.</span><span class="sxs-lookup"><span data-stu-id="d66a0-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="d66a0-274">O intervalo Máximo seria a soma de todos os intervalos máximos de todos os planos do Serviço de Aplicativo hospedados no pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d66a0-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="d66a0-275">A contagem de Aumento das regras de escala vertical deve ser definida como, pelo menos, 1X a Taxa de Inflação do Plano do Serviço de Aplicativo para a escala vertical.</span><span class="sxs-lookup"><span data-stu-id="d66a0-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="d66a0-276">A contagem de redução pode ser ajustada para algo entre 1/2x ou 1x a taxa de inflação do plano do Serviço de Aplicativo para reduzir verticalmente.</span><span class="sxs-lookup"><span data-stu-id="d66a0-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="d66a0-277">Dimensionamento automático para o pool de front-end</span><span class="sxs-lookup"><span data-stu-id="d66a0-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="d66a0-278">As regras de dimensionamento automático de front-end são mais simples para pools de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d66a0-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="d66a0-279">Basicamente, você deve</span><span class="sxs-lookup"><span data-stu-id="d66a0-279">Primarily, you should</span></span>  
<span data-ttu-id="d66a0-280">verifique se a duração da medição e se os temporizadores de resfriamento consideram que as operações de escala em um Plano do Serviço de Aplicativo não são instantâneas.</span><span class="sxs-lookup"><span data-stu-id="d66a0-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="d66a0-281">Para este cenário, Frank sabe que a taxa de erro aumenta depois que os front-ends alcançam 80% de utilização de CPU e define a regra de dimensionamento automático para aumentar o número de instâncias da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d66a0-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Configurações de dimensionamento automático para o pool de front-end.][Front-End-Scale]

| <span data-ttu-id="d66a0-283">**Perfil de dimensionamento automático – Front-ends**</span><span class="sxs-lookup"><span data-stu-id="d66a0-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="d66a0-284">**Nome:** Dimensionamento automático – Front-ends</span><span class="sxs-lookup"><span data-stu-id="d66a0-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="d66a0-285">**Dimensionar por:** Regras de agendamento e desempenho</span><span class="sxs-lookup"><span data-stu-id="d66a0-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="d66a0-286">**Perfil:** Todos os dias</span><span class="sxs-lookup"><span data-stu-id="d66a0-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="d66a0-287">**Tipo:** Recorrência</span><span class="sxs-lookup"><span data-stu-id="d66a0-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="d66a0-288">**Intervalo de destino:** 3 a 10 instâncias</span><span class="sxs-lookup"><span data-stu-id="d66a0-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="d66a0-289">**Dias:** Todos os dias</span><span class="sxs-lookup"><span data-stu-id="d66a0-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="d66a0-290">**Hora de início:** 9:00</span><span class="sxs-lookup"><span data-stu-id="d66a0-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="d66a0-291">**Fuso horário:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="d66a0-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="d66a0-292">**Regra de dimensionamento automático (Escalar Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="d66a0-293">**Recurso:** Pool de front-end</span><span class="sxs-lookup"><span data-stu-id="d66a0-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="d66a0-294">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="d66a0-295">**Operação:** Mais de 60%</span><span class="sxs-lookup"><span data-stu-id="d66a0-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="d66a0-296">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="d66a0-297">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-298">**Ação:** Aumentar a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="d66a0-299">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="d66a0-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="d66a0-300">**Regra de dimensionamento automático (Reduzir Verticalmente)**</span><span class="sxs-lookup"><span data-stu-id="d66a0-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="d66a0-301">**Recurso:** Pool de trabalho 1</span><span class="sxs-lookup"><span data-stu-id="d66a0-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="d66a0-302">**Métrica:** % da CPU</span><span class="sxs-lookup"><span data-stu-id="d66a0-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="d66a0-303">**Operação:** Menos de 30%</span><span class="sxs-lookup"><span data-stu-id="d66a0-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="d66a0-304">**Duração:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="d66a0-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="d66a0-305">**Agregação de tempo:** Média</span><span class="sxs-lookup"><span data-stu-id="d66a0-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="d66a0-306">**Ação:** Diminuir a contagem em 3</span><span class="sxs-lookup"><span data-stu-id="d66a0-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="d66a0-307">**Tempo de resfriamento (minutos):** 120</span><span class="sxs-lookup"><span data-stu-id="d66a0-307">**Cool down (minutes):** 120</span></span> |

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
