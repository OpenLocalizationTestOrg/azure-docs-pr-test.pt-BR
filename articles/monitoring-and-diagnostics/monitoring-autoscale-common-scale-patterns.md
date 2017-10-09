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
# <a name="overview-of-common-autoscale-patterns"></a>Visão geral dos padrões comuns de dimensionamento automático
Este artigo descreve alguns dos tooscale de padrões comuns de saudação seus recursos no Azure.

Azure AutoEscala Monitor aplica-se apenas tooVirtual conjuntos de escala de máquina (VMSS), os serviços de nuvem, planos de serviço de aplicativo e ambientes de serviço de aplicativo. 

# <a name="lets-get-started"></a>Vamos começar

Este artigo pressupõe que você esteja familiarizado com o dimensionamento automático. Você pode [obter Introdução tooscale aqui o recurso][1]. Olá seguem alguns dos padrões comuns de escala hello.

## <a name="scale-based-on-cpu"></a>Dimensionamento com base na CPU

Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e 

- Você deseja tooscale out/escala com base na CPU.
- Além disso, você deseja tooensure há um número mínimo de instâncias. 
- Além disso, você deseja tooensure que você definir um número de toohello limite máximo de instâncias para que pode ser dimensionado.

![Dimensionamento com base na CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Dimensionamento diferente em finais de semana e dias da semana

Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e

- Você deseja três instâncias por padrão (em dias da semana)
- Você não espera que o tráfego nos finais de semana e, portanto, você deseja tooscale para baixo too1 instância nos finais de semana.

![Dimensionamento diferente em finais de semana e dias da semana][3]

## <a name="scale-differently-during-holidays"></a>Dimensionamento diferente durante feriados

Você tem um aplicativo Web (/VMSS/função de serviço de nuvem) e 

- Você deseja tooscale para cima/para baixo com base no uso da CPU por padrão
- No entanto, durante a temporada (ou dias específicos que são importantes para seu negócio) você deseja toooverride Olá padrões e têm mais capacidade à sua disposição.

![Dimensionamento diferente em feriados][4]

## <a name="scale-based-on-custom-metric"></a>Dimensionamento baseado em métrica personalizada

Você tem um front-end da web e uma camada de API que se comunica com hello back-end. 

- Você deseja tooscale da camada de API de saudação com base em eventos personalizados no front-end hello (exemplo: você deseja tooscale o processo de check-out com base no número de saudação de itens no carrinho de compras de saudação)

![Dimensionamento baseado em métrica personalizada][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png