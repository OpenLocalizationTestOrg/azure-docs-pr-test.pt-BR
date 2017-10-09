---
title: "implementação do Mobile Engagement aaaAzure para o aplicativo de jogos"
description: "Jogos tooimplement de cenário de aplicativo do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>Implementar o Mobile Engagement com o Aplicativo de Jogos
## <a name="overview"></a>Visão geral
Uma empresa de jogos em fase inicial lançou um novo aplicativo de jogo de pescar baseado em role-play/estratégia. jogo Olá foi ligado e em execução por 6 meses. Este jogo é um enorme sucesso e tem milhões de downloads e retenção de saudação é muito alta tooother comparados inicialização jogo aplicativos. Reunião de revisão trimestral hello, participantes concordam que precisam tooincrease a receita média por usuário (ARPU). Pacotes de jogo premium estão disponíveis como ofertas especiais. Esses pacotes de jogos permitem a aparência de saudação tooupgrade usuários e o desempenho de suas linhas de pesca e iscas ou soluciona em jogo hello. No entanto, as vendas dos pacotes são muito baixas. Para que eles decidirem tooanalyze Prezado cliente primeira experiência com uma ferramenta de análise e, em seguida, toodevelop um contrato programa tooincrease vendas usando avançados de segmentação.

Com base em Olá [Azure Mobile Engagement - guia de Introdução com as práticas recomendadas](mobile-engagement-getting-started-best-practices.md) que criam uma estratégia de contrato.

## <a name="objectives-and-kpis"></a>Objetivos e KPIs
Atender às principais partes interessadas para jogo hello. Todos têm um objetivo principal - vendas de pacote tooincrease premium 15%. Criar unidade e negócios indicadores chave de desempenho (KPIs) toomeasure esse objetivo

* Em que nível de jogo Olá esses pacotes são comprados?
* O que é a receita Olá por usuário, sessão, semana e por mês?
* Quais são os tipos de compra favorito de Olá?

Parte 1 de saudação [guia de Introdução](mobile-engagement-getting-started-best-practices.md) explica como toodefine Olá objetivos e KPIs. 

Com hello que KPIs da empresa agora estão definidos, Olá Mobile produto Manager cria KPIs contrato toodetermine novas tendências de usuário e de retenção.

* Monitorar a retenção e use em Olá intervalos a seguir: diariamente, cada 2 dias, semanal, mensal e a cada 3 meses
* Contagens de usuários ativos
* classificação do aplicativo Hello em Olá armazenar

Com base nas recomendações da equipe de TI do hello, Olá KPIs técnicas a seguir foram adicionada Olá tooanswer perguntas a seguir:

* Qual é o caminho do meu usuário (qual página é visitada, quanto tempo os usuários passam nela)
* Número de falhas ou erros encontrados por sessão
* Quais versões de sistema operacional meus usuários estão executando?
* O que é o tamanho médio de saudação da tela para meus usuários?
* Que tipo de conectividade com a Internet meus usuários têm?

Para cada KPI Olá Mobile produto Manager Especifica dados de saudação precisa e onde ele está localizado em sua guia estratégico.

## <a name="engagement-program-and-integration"></a>Integração e programa de envolvimento
Antes de criar um programa de contrato avançado, Olá diretor de projeto Mobile responsável por projeto Olá deve ter uma profunda compreensão de como e quando os produtos são consumidos por usuários de saudação.

Depois de 3 meses, Olá diretor de projeto Mobile coletou suficiente tooenhance dados suas vendas de notificação no aplicativo de envio. Ele descobre que:

* primeira compra de saudação geralmente ocorre em nível de saudação 14. Para 90% dos casos, a compra Olá é armas lendária novo para $3.
* Em 80% dos casos, os usuários que compraram, continue com o produto hello e fazer mais compras.
* Os usuários que foram aprovadas nível Olá 20, iniciar toospend mais de US $10/ semana.
* Os usuários tendem a pacotes de premium toobuy no nível 16, 24 e 32.

Obrigado analysis toothis Olá diretor de projeto Mobile decide toocreate push específico notificação sequências tooincrease nas vendas de aplicativo. Ele cria três sequências de push que ele chama de: Programa de Boas-vindas, Programa de Vendas e o Programa Inativo. Para obter mais informações, consulte toohello [Guias estratégicos](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
