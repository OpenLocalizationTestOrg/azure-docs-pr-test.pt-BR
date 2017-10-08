---
title: "Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo"
description: "Saiba Olá vantagens e desvantagens de dimensionamento do aplicativo no serviço de aplicativo."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, escala, escalonável, plano de serviço de aplicativo, custo de serviço de aplicativo"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Serviço de Aplicativo do Azure: dimensionamento de aplicativos do Serviço de Aplicativo
Aplicativos hospedados no Serviço de Aplicativo do Azure podem [chegar a uma escala enorme](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
No entanto, o dimensionamento de um aplicativo é um problema complexo que não tem uma solução que se aplique a todas as situações. toocorrectly dimensionar seu aplicativo há 3 áreas principais que contribuirão com êxito de aplicativos tooyour:

1. Entender a arquitetura do aplicativo e seus pontos fracos.
   * Seu aplicativo é com estado? Sem estado?
   * O que são todos os componentes de saudação do seu aplicativo?
     * Onde estão os gargalos de saudação no aplicativo hello?
   * Quando a carga for aplicado tooyour aplicativo, o que interromperá primeiro?
2. Saudação de Noções básicas sobre esperado requisitos de carga e desempenho.
   * Aplicativo hello precisa tooserve mil usuários? ou um milhão?
   * O tráfego virá de um único local geográfico ou é global?
   * Há variações sazonais? Picos de tráfego?
   * Rapidez o aplicativo hello deve responder? 1 segundo? 1 milissegundo?
3. Noções básicas sobre corretamente aproveite Olá plataforma e hospedagem de seu aplicativo.
   * O que devem recursos utilizam tooachieve Minhas metas de escala?

Esta seção ajudará você a entender todos os fatores de saudação e ajuda a planejar uma estratégia que tira proveito dos tooachieve de recursos de serviço de aplicativo necessário Olá suas metas de escalabilidade.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

