---
title: "aaaOverview dos padrões comuns de dimensionamento automático | Microsoft Docs"
description: "Saiba que algumas tooauto de padrões comuns de saudação dimensionar seus recursos no Azure."
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="439d7-103">Visão geral dos padrões comuns de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="439d7-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="439d7-104">Este artigo descreve alguns dos tooscale de padrões comuns de saudação seus recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="439d7-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="439d7-105">Azure AutoEscala Monitor aplica-se apenas tooVirtual conjuntos de escala de máquina (VMSS), os serviços de nuvem, planos de serviço de aplicativo e ambientes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="439d7-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="439d7-106">Vamos começar</span><span class="sxs-lookup"><span data-stu-id="439d7-106">Lets get started</span></span>

<span data-ttu-id="439d7-107">Este artigo pressupõe que você esteja familiarizado com o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="439d7-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="439d7-108">Você pode [obter Introdução tooscale aqui o recurso][1].</span><span class="sxs-lookup"><span data-stu-id="439d7-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="439d7-109">Olá seguem alguns dos padrões comuns de escala hello.</span><span class="sxs-lookup"><span data-stu-id="439d7-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="439d7-110">Dimensionamento com base na CPU</span><span class="sxs-lookup"><span data-stu-id="439d7-110">Scale based on CPU</span></span>

<span data-ttu-id="439d7-111">Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e</span><span class="sxs-lookup"><span data-stu-id="439d7-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="439d7-112">Você deseja tooscale out/escala com base na CPU.</span><span class="sxs-lookup"><span data-stu-id="439d7-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="439d7-113">Além disso, você deseja tooensure há um número mínimo de instâncias.</span><span class="sxs-lookup"><span data-stu-id="439d7-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="439d7-114">Além disso, você deseja tooensure que você definir um número de toohello limite máximo de instâncias para que pode ser dimensionado.</span><span class="sxs-lookup"><span data-stu-id="439d7-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Dimensionamento com base na CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="439d7-116">Dimensionamento diferente em finais de semana e dias da semana</span><span class="sxs-lookup"><span data-stu-id="439d7-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="439d7-117">Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e</span><span class="sxs-lookup"><span data-stu-id="439d7-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="439d7-118">Você deseja três instâncias por padrão (em dias da semana)</span><span class="sxs-lookup"><span data-stu-id="439d7-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="439d7-119">Você não espera que o tráfego nos finais de semana e, portanto, você deseja tooscale para baixo too1 instância nos finais de semana.</span><span class="sxs-lookup"><span data-stu-id="439d7-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Dimensionamento diferente em finais de semana e dias da semana][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="439d7-121">Dimensionamento diferente durante feriados</span><span class="sxs-lookup"><span data-stu-id="439d7-121">Scale differently during holidays</span></span>

<span data-ttu-id="439d7-122">Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e</span><span class="sxs-lookup"><span data-stu-id="439d7-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="439d7-123">Você deseja tooscale para cima/para baixo com base no uso da CPU por padrão</span><span class="sxs-lookup"><span data-stu-id="439d7-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="439d7-124">No entanto, durante a temporada (ou dias específicos que são importantes para seu negócio) você deseja toooverride Olá padrões e têm mais capacidade à sua disposição.</span><span class="sxs-lookup"><span data-stu-id="439d7-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Dimensionamento diferente em feriados][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="439d7-126">Dimensionamento baseado em métrica personalizada</span><span class="sxs-lookup"><span data-stu-id="439d7-126">Scale based on custom metric</span></span>

<span data-ttu-id="439d7-127">Você tem um front-end da web e uma camada de API que se comunica com hello back-end.</span><span class="sxs-lookup"><span data-stu-id="439d7-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="439d7-128">Você deseja tooscale da camada de API de saudação com base em eventos personalizados no front-end hello (exemplo: você deseja tooscale o processo de check-out com base no número de saudação de itens no carrinho de compras de saudação)</span><span class="sxs-lookup"><span data-stu-id="439d7-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Dimensionamento baseado em métrica personalizada][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png