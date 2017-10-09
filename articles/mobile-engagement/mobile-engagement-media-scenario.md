---
title: "implementação do Mobile Engagement aaaAzure para um aplicativo de mídia"
description: "Tooimplement de cenário de aplicativo de mídia do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Implementar o Mobile Engagement com os Aplicativos de Mídia
## <a name="overview"></a>Visão geral
Pedro é gerente de projetos móveis de uma grande empresa de mídia. Recentemente, ele lançou um novo aplicativo com uma contagem de downloads muito alta. Ele atingiu seus objetivos de download, mas ainda assim seu ROI (Retorno sobre o Investimento) por usuário não atendeu aos seus requisitos. 

Pedro já identificou a causa de seu ROI muito baixo. Com frequência, os usuários param de usar o aplicativo depois de apenas duas semanas e a maioria não volta mais. Ele quer tooincrease retenção de saudação do seu aplicativo.

Depois de alguns testes iniciais, que aprendeu quando ele emprega usuários notificações por push, eles tendem a toocontinue usando seu aplicativo. Também usuários inativos geralmente retornará toohello aplicativo dependendo notificações, que ele envia-los. João decide tooinvest em algum tipo de contrato de programa para seu aplicativo que usa o direcionamento avançado notificações por push.

João recentemente leu Olá [Azure Mobile Engagement - guia de Introdução com as práticas recomendadas](mobile-engagement-getting-started-best-practices.md) e decidiu tooimplement recomendações de saudação do guia de saudação.

## <a name="objectives-and-kpis"></a>Objetivos e KPIs
Há uma reunião com os principais participantes no aplicativo de Pedro. Os negócios são gerados de anúncios à medida que os usuários consomem a mídia. Aumentando o conteúdo consumido por usuário, Pedro aumenta sua receita. Todos os concordarem com um objetivo principal: tooincrease vendas dos anúncios em 25%. Criar unidade e negócios indicadores chave de desempenho (KPIs) toomeasure esse objetivo

* Número de anúncios clicados por usuário
* Quantas páginas de artigo visitadas (por usuário/por sessão/por semana/por mês…)
* Quais são as categorias favoritas

Com base na reunião de Pedro com os participantes principais, ele definiu os KPIs de Negócios. Ele segue parte 1 de saudação [Azure Mobile Engagement - guia de Introdução com as práticas recomendadas](mobile-engagement-getting-started-best-practices.md). 

Em seguida, ele cria Olá tooensure contrato KPIs que são alcançados objetivos a seguir:

* Monitorar a retenção em Olá intervalos a seguir: diária, semanal, quinzenal e mensais.
* Contagens de usuários ativos
* classificação do aplicativo Hello no aplicativo hello armazena

Com base nas recomendações da equipe de TI do hello, Olá KPIs técnica a seguir foram adicionada Olá tooanswer perguntas a seguir:

* Qual é o caminho do meu usuário (qual página é visitada, quanto tempo os usuários passam nela)
* Número de falhas ou erros encontrados por sessão?
* Quais versões de sistema operacional meus usuários estão executando?
* O que é o tamanho médio de saudação da tela para meus usuários?
* Que tipo de conexões com a Internet meus usuários têm?

Para cada KPI, ele classifica dados Olá necessários e ele registra no local adequado Olá sua guia estratégico.

## <a name="engagement-program-and-integration"></a>Integração e programa de envolvimento
Agora que Pedro terminou de definir os KPIs, ele iniciará a fase de estratégia de Envolvimento definindo quatro programas de envolvimento e seus objetivos: ![][1]

Em seguida, Pedro vai mais além, detalhando as notificações por push para cada programa. As notificações por push são definidas por cinco elementos:

1. Objetivo: o que é o objetivo Olá notificação Olá
2. Como objetivo Olá seja atingido
3. Destino: quem receberá notificação Olá?
4. Conteúdo: O que é texto de saudação e o formato de saudação da notificação hello (em App/Out de aplicativo)
5. Quando: o que é Olá melhor toosend do momento em que esta notificação por push
   
    ![][2]

Para obter mais informações, consulte toohello [Guias estratégicos](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

Toocollect e grava sua marca planejar em conjunto com a equipe tooimplement Olá solução de acordo com a parte 2 toohello Olá white paper que João usa toodefine da seção de destino de dados que ele tem. Depois de uma semana de implementação e de testes de aceitação de usuário, Pedro pode finalmente lançar seus programas.

## <a name="program-results"></a>Resultados do programa
Quatro meses depois, Pedro examina o desempenho dos programas. saudação de boas-vindas do programa e hello programa semanal metas sejam atingidas suas. diminui o número de saudação do usuário com apenas uma sessão, mais recursos do aplicativo hello estão sendo usados e Olá número de conexões por semana dobrou.

Olá **programa inativo** está ajudando John entender as tendências de usuário. Parece que 15% de usuários inativos Olá retornam toohello aplicativo. No entanto, a maioria deles não permanece ativa mais de um mês. Pedro prevê uma potencial otimização dessa sequência com notificações adicionais e a expansão de suas opções de conteúdo.

Olá **programa descobrir** não funcionam bem. Ele aumenta entre a venda, mas não há tooreach seus objetivos. João identifica que ele não tem suficiente dados toomake relevantes de direcionamento e propor o conteúdo apropriado. Ele interrompe o programa e se concentra em "notificações por push editoriais" com o Azure Mobile Engagement. Suas jornalistas já tem um notificações por push de toosend de solução CMS e que não querem toochange.

João decide toouse Olá API de alcance que é uma API de REST de HTTP que permite gerenciar campanhas de alcance sem a necessidade de interface de Web AZME toouse. Com essa abordagem, João pode coletar dados de saudação ele precisa e permitir que os seus autores tookeep usando a solução de CMS hello.

tooensure que o recurso funciona corretamente, João faz IT team toobe cuidadoso em Olá pontos a seguir:

1. **Sistemas operacionais** : todos têm suas próprias notificações de push regras tooadministrate, assim, José decide toolist todos os casos e verifica se Olá APIs tratá-la.
   Por exemplo: Sistema Android push permite visão geral que não é o caso de Olá com iOS.
2. **Período de tempo**: João deseja uma API, o qual definir o período de tempo de saudação e definir um toocampaigns final. Ele quer que os usuários toopreserve qualquer limite de notificação de interrupção.
3. **Categorias**: a equipe de marketing prepara o modelo de cada tipo de alerta. João pergunta categorias de tooset de equipe IT dentro Olá API.

Depois de alguns testes, Pedro está satisfeito. Obrigado toothis API, jornalistas ainda podem enviar notificações por push com seus CMS e do Azure Mobile Engagement coleta todos os dados de comportamentos para eles

Depois dos quatro primeiros meses, os resultados refletem um bom desempenho geral e oferece a confiança para Pedro e sua diretoria, o ROI por usuário aumentou em 15% e as vendas móveis representam 17,5% do total de vendas, um aumento de 7,5% em apenas quatro meses.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
