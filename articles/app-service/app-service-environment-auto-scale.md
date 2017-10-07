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
# <a name="autoscaling-and-app-service-environment-v1"></a>Dimensionamento automático e Ambiente de Serviço de Aplicativo v1

> [!NOTE]
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo.  Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
> 

Os ambientes de Serviço de Aplicativo do Azure dão suporte ao *dimensionamento automático*. Você pode dimensionar automaticamente pools de trabalho individuais com base em métricas ou na agenda.

![Opções de dimensionamento automático para um pool de trabalho.][intro]

Dimensionamento automático otimiza a utilização de recursos automaticamente ampliando e reduzindo uma toofit do ambiente de serviço de aplicativo seu perfil de alocação e a carga.

## <a name="configure-worker-pool-autoscale"></a>Configurar o dimensionamento automático de pool de trabalho
Você pode acessar a funcionalidade de dimensionamento automático de saudação do hello **configurações** guia de pool do trabalhador hello.

![Guia de configurações do pool do trabalhador hello.][settings-scale]

A partir daí, Olá interface deve ser bastante familiar, pois ele é hello planejar experiência mesmo que você vê quando você dimensionar um aplicativo de serviço. 

![Configurações manuais de escala.][scale-manual]

Você também pode configurar um perfil de dimensionamento automático.

![Configurações de dimensionamento automático.][scale-profile]

Perfis de AutoEscala são os limites de tooset úteis em sua escala. Dessa forma, você pode ter uma experiência de desempenho consistente, definindo um valor de escala de limite inferior (1) e um limite de gastos previsível, definindo um limite superior (2).

![Configurações de escala no perfil.][scale-profile2]

Depois de definir um perfil, você pode adicionar tooscale de regras de dimensionamento automático para cima ou para baixo número de saudação de instâncias no pool do trabalhador hello dentro dos limites de saudação definidas pelo perfil de saudação. As regras de dimensionamento automático se baseiam em métricas.

![Regra de escala.][scale-rule]

 Nenhum pool de trabalho ou a métrica de front-end pode ser usado toodefine regras de dimensionamento automático. Essas métricas são Olá mesmas métricas, você pode monitorar nos gráficos de folha de recursos de saudação ou definir alertas para o.

## <a name="autoscale-example"></a>Exemplo de dimensionamento automático
O dimensionamento automático de um ambiente de Serviço de Aplicativo pode ser melhor ilustrado examinando um cenário.

Este artigo explica todas as considerações de saudação necessário ao configurar o dimensionamento automático. Olá artigo o orienta por meio de saudação interações que entram em reproduzir quando fatores de dimensionamento automático ambientes de serviço de aplicativo que são hospedadas em ambiente de serviço de aplicativo.

### <a name="scenario-introduction"></a>Introdução ao cenário
Frank é um sysadmin para uma empresa que foi migrado de uma parte de cargas de trabalho de saudação que gerencia o tooan ambiente de serviço de aplicativo.

Olá ambiente do serviço de aplicativo toomanual dimensionamento configurado da seguinte maneira:

* **Front-ends:** 3
* **Pool de trabalho 1**: 10
* **Pool de trabalho 2:**5
* **Pool de trabalho 3:**5

O pool de trabalho 1 é usado para cargas de trabalho de produção, embora o pool de trabalho 2 e o pool de trabalho 3 sejam usados para garantia de qualidade (QA) e cargas de trabalho de desenvolvimento.

Olá aplicativo planos de serviço para controle de qualidade e desenvolvimento são configurados toomanual escala. plano de serviço de aplicativo de produção de Hello é definida toodeal tooautoscale com variações de carga e o tráfego.

Frank esteja familiarizado com o aplicativo hello. Ele conhece o horário de pico de saudação de carga é entre 9:00 AM e 6:00 PM porque este é um aplicativo de (LOB) de linha de negócios que os funcionários usam enquanto estiverem no escritório de saudação. O uso é reduzido depois disso, quando os usuários param de trabalhar naquele dia. Fora do horário de pico, ainda há alguma carga porque os usuários podem acessar o aplicativo hello remotamente usando seus dispositivos móveis ou computadores domésticos. produção de Hello plano de serviço de aplicativo já está configurado tooautoscale com base no uso da CPU com hello regras a seguir:

![Configurações específicas para o aplicativo LOB.][asp-scale]

| **Perfil de dimensionamento automático – Dias da semana – plano do Serviço de Aplicativo** | **Perfil de dimensionamento automático – Finais de semana – plano do Serviço de Aplicativo** |
| --- | --- |
| **Nome:** Perfil de dia da semana |**Nome:** Perfil de final de semana |
| **Dimensionar por:** Regras de agendamento e desempenho |**Dimensionar por:** Regras de agendamento e desempenho |
| **Perfil:** Dias da semana |**Perfil:** Final de semana |
| **Tipo:** Recorrência |**Tipo:** Recorrência |
| **Intervalo de destino:** 5 instâncias too20 |**Intervalo de destino:** 3 instâncias too10 |
| **Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira |**Dias:** sábado e domingo |
| **Hora de início:** 9:00 |**Hora de início:** 9:00 |
| **Fuso horário:** UTC-08 |**Fuso horário:** UTC-08 |
|  | |
| **Regra de dimensionamento automático (Escalar Verticalmente)** |**Regra de dimensionamento automático (Escalar Verticalmente)** |
| **Recurso:** Produção (ambiente de Serviço de Aplicativo) |**Recurso:** Produção (ambiente de Serviço de Aplicativo) |
| **Métrica:** % da CPU |**Métrica:** % da CPU |
| **Operação:** Mais de 60% |**Operação:** Mais de 80% |
| **Duração:** 5 minutos |**Duração:** 10 minutos |
| **Agregação de tempo:** Média |**Agregação de tempo:** Média |
| **Ação:** Aumentar a contagem em 2 |**Ação:** Aumentar a contagem em 1 |
| **Tempo de resfriamento (minutos):** 15 |**Tempo de resfriamento (minutos):** 20 |
|  | |
| **Regra de dimensionamento automático (Reduzir Verticalmente)** |**Regra de dimensionamento automático (Reduzir Verticalmente)** |
| **Recurso:** Produção (ambiente de Serviço de Aplicativo) |**Recurso:** Produção (ambiente de Serviço de Aplicativo) |
| **Métrica:** % da CPU |**Métrica:** % da CPU |
| **Operação:** Menos de 30% |**Operação:** Menos de 20% |
| **Duração:** 10 minutos |**Duração:** 15 minutos |
| **Agregação de tempo:** Média |**Agregação de tempo:** Média |
| **Ação:** Reduzir a contagem em 1 |**Ação:** Reduzir a contagem em 1 |
| **Tempo de resfriamento (minutos):** 20 |**Tempo de resfriamento (minutos):** 10 |

### <a name="app-service-plan-inflation-rate"></a>Taxa de inflação do plano do Serviço de Aplicativo
Planos de serviço de aplicativo configurado tooautoscale fazê-lo a uma taxa máxima por hora. Essa taxa pode ser calculada com base em valores de saudação fornecidos na regra de dimensionamento automático hello.

Compreendendo e calcular Olá *taxa de inflação do plano de serviço de aplicativo* é importante para dimensionamento automático do ambiente do serviço de aplicativo porque o pool de trabalho de tooa de alterações de escala não são instantâneos.

Olá taxa de inflação do plano de serviço de aplicativo é calculada da seguinte maneira:

![Cálculo da taxa de inflação do plano do Serviço de Aplicativo.][ASP-Inflation]

Com base em Olá AutoEscala – escala a regra para o perfil de dia da semana de saudação do plano de serviço de aplicativo de produção de hello:

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation1]

No caso de saudação de saudação AutoEscala – regra aumentar para perfil de fim de semana de saudação de plano de serviço de aplicativo de produção de hello fórmula Olá deve resolver para:

![Taxa de inflação de plano do Serviço de Aplicativo para finais de semana com base em Dimensionamento automático – regra Escalar Verticalmente.][Equation2]

Esse valor também pode ser calculado para operações de redução.

Com base em Olá AutoEscala – regra de escala para baixo para o perfil de dia da semana de saudação de produção de hello plano de serviço de aplicativo, isso seria semelhante ao seguinte:

![Taxa de inflação de plano do Serviço de Aplicativo para dias da semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation3]

No caso de saudação de saudação AutoEscala – regra de escala para baixo para o perfil de fim de semana de saudação de plano de serviço de aplicativo de produção de hello fórmula Olá deve resolver para:  

![Taxa de inflação de plano do Serviço de Aplicativo para fins de semana com base em Dimensionamento automático – regra Reduzir Verticalmente.][Equation4]

plano de serviço de aplicativo de produção de Hello pode crescer em uma taxa máxima de oito instâncias por hora durante a semana hello e quatro instâncias por hora durante a fim de semana de saudação. Ele pode liberar instâncias em uma taxa máxima de quatro instâncias por hora durante a semana hello e seis instâncias por hora durante a semana.

Se vários planos de serviço de aplicativo estão hospedados em um pool de trabalho, você terá Olá toocalculate *taxa total de inflação* como soma Olá Olá inflação da taxa de saudação todos os planos de serviço de aplicativo que estão sendo hospedagem nesse pool de trabalho.

![Cálculo da taxa total de inflação para vários planos do Serviço de Aplicativo hospedados em um pool de trabalho.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Saudação de uso do serviço de aplicativo planejar as regras de AutoEscala pool de trabalho toodefine taxa de inflação
Pools de trabalho que hospedam planos de serviço de aplicativo tooautoscale configurado necessário para alocar um buffer de capacidade. buffer de saudação permite Olá toogrow de operações de dimensionamento automático e reduzir o plano de serviço de aplicativo, conforme necessário. buffer mínimo Olá seria Olá calculado aplicativo serviço planejar inflação taxa Total.

Como as operações de dimensionamento de ambiente de serviço de aplicativo levam algum tempo tooapply, qualquer alteração deve levar em consideração para outras alterações de demanda que podem acontecer enquanto uma operação em escala está em andamento. tooaccommodate essa latência, recomendamos que você use Olá calculado aplicativo serviço planejar inflação taxa Total como o número mínimo de saudação de instâncias que são adicionados para cada operação de dimensionamento automático.

Com essas informações, Frank pode definir Olá perfil de AutoEscala e regras a seguir:

![Regras de perfil de dimensionamento automático para o exemplo LOB.][Worker-Pool-Scale]

| **Perfil de dimensionamento automático – Dias da semana** | **Perfil de dimensionamento automático – Finais de semana** |
| --- | --- |
| **Nome:** Perfil de dia da semana |**Nome:** Perfil de final de semana |
| **Dimensionar por:** Regras de agendamento e desempenho |**Dimensionar por:** Regras de agendamento e desempenho |
| **Perfil:** Dias da semana |**Perfil:** Final de semana |
| **Tipo:** Recorrência |**Tipo:** Recorrência |
| **Intervalo de destino:** 13 instâncias too25 |**Intervalo de destino:** 6 instâncias too15 |
| **Dias:** segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira |**Dias:** sábado e domingo |
| **Hora de início:** 7:00 |**Hora de início:** 9:00 |
| **Fuso horário:** UTC-08 |**Fuso horário:** UTC-08 |
|  | |
| **Regra de dimensionamento automático (Escalar Verticalmente)** |**Regra de dimensionamento automático (Escalar Verticalmente)** |
| **Recurso:** Pool de trabalho 1 |**Recurso:** Pool de trabalho 1 |
| **Métrica:** WorkersAvailable |**Métrica:** WorkersAvailable |
| **Operação:** menos de 8 |**Operação:** menos de 3 |
| **Duração:** 20 minutos |**Duração:** 30 minutos |
| **Agregação de tempo:** Média |**Agregação de tempo:** Média |
| **Ação:** Aumentar a contagem em 8 |**Ação:** Aumentar a contagem em 3 |
| **Tempo de resfriamento (minutos):** 180 |**Tempo de resfriamento (minutos):** 180 |
|  | |
| **Regra de dimensionamento automático (Reduzir Verticalmente)** |**Regra de dimensionamento automático (Reduzir Verticalmente)** |
| **Recurso:** Pool de trabalho 1 |**Recurso:** Pool de trabalho 1 |
| **Métrica:** WorkersAvailable |**Métrica:** WorkersAvailable |
| **Operação:** maior que 8 |**Operação:** maior que 3 |
| **Duração:** 20 minutos |**Duração:** 15 minutos |
| **Agregação de tempo:** Média |**Agregação de tempo:** Média |
| **Ação:** Diminuir a contagem em 2 |**Ação:** Diminuir a contagem em 3 |
| **Tempo de resfriamento (minutos):** 120 |**Tempo de resfriamento (minutos):** 120 |

Olá definido no perfil de saudação do intervalo de destino é calculado com instâncias de mínimo Olá definidas no perfil de saudação plano de serviço de aplicativo + buffer.

intervalo máximo de saudação seria soma de saudação de todos os intervalos de saudação máximo de todos os planos de serviço de aplicativo hospedados no pool do trabalhador hello.

Olá contagem de aumento de escala Olá as regras de deve ser conjunto tooat pelo menos 1 X a taxa de inflação de plano de serviço aplicativo para escala para cima.

Contagem de redução pode ser ajustada toosomething entre 1/2 X ou 1 X Olá planejar taxa de inflação de serviço de aplicativo para a escala para baixo.

### <a name="autoscale-for-front-end-pool"></a>Dimensionamento automático para o pool de front-end
As regras de dimensionamento automático de front-end são mais simples para pools de trabalho. Basicamente, você deve  
Certifique-se de que duração de medida de saudação e temporizadores de cooldown Olá considerar que as operações de escala em um plano de serviço de aplicativo não são instantâneas.

Para este cenário, Frank sabe que a taxa de erro Olá aumenta após front-ends atingir 80% de utilização da CPU e define Olá AutoEscala instâncias de tooincrease regra da seguinte maneira:

![Configurações de dimensionamento automático para o pool de front-end.][Front-End-Scale]

| **Perfil de dimensionamento automático – Front-ends** |
| --- |
| **Nome:** Dimensionamento automático – Front-ends |
| **Dimensionar por:** Regras de agendamento e desempenho |
| **Perfil:** Todos os dias |
| **Tipo:** Recorrência |
| **Intervalo de destino:** 3 instâncias too10 |
| **Dias:** Todos os dias |
| **Hora de início:** 9:00 |
| **Fuso horário:** UTC-08 |
|  |
| **Regra de dimensionamento automático (Escalar Verticalmente)** |
| **Recurso:** Pool de front-end |
| **Métrica:** % da CPU |
| **Operação:** Mais de 60% |
| **Duração:** 20 minutos |
| **Agregação de tempo:** Média |
| **Ação:** Aumentar a contagem em 3 |
| **Tempo de resfriamento (minutos):** 120 |
|  |
| **Regra de dimensionamento automático (Reduzir Verticalmente)** |
| **Recurso:** Pool de trabalho 1 |
| **Métrica:** % da CPU |
| **Operação:** Menos de 30% |
| **Duração:** 20 minutos |
| **Agregação de tempo:** Média |
| **Ação:** Diminuir a contagem em 3 |
| **Tempo de resfriamento (minutos):** 120 |

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
