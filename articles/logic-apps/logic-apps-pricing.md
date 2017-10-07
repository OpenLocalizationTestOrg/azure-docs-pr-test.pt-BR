---
title: "aaaPricing & cobrança - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Saiba como os preços e a cobrança funcionam para Aplicativos Lógicos do Azure."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Modelo de preços de Aplicativos Lógicos
Aplicativos lógicos do Azure permite tooscale e executar fluxos de trabalho de integração na nuvem hello.  São os seguintes detalhes Olá cobrança e planos de preços para os aplicativos lógicos.
## <a name="consumption-pricing"></a>Preço por consumo
Aplicativos Lógicos recém-criado usam um plano de consumo. Com hello aplicativos lógicos consumo modelo de preços, você só paga pelo que usa.  Os Aplicativos Lógicos não sofrem limitações ao usar um plano de consumo.
Todas as ações executadas em uma execução de uma instância de aplicativo lógico são limitadas.
### <a name="what-are-action-executions"></a>O que são execuções de ação?
Cada etapa em uma definição de aplicativo lógica é uma ação, que inclui gatilhos, etapas do fluxo de controle como condições de escopos, loops for each, até loops, chama tooconnectors e chamadas de ações de toonative.
Os gatilhos são ações especiais que são projetado tooinstantiate uma nova instância de um aplicativo de lógica quando ocorre um evento específico.  Há vários comportamentos diferentes para gatilhos, o que podem afetar como Olá lógica aplicativo é monitorado.
* **Gatilho de sondagem** – esse gatilho sonda continuamente um ponto de extremidade até receber uma mensagem que satisfaz os critérios de Olá para criar uma instância de um aplicativo lógico.  intervalo de sondagem Olá pode ser configurado no gatilho Olá Olá Designer de lógica do aplicativo.  Cada solicitação de sondagem, mesmo se não criar uma instância de um aplicativo lógico, contará como uma execução da ação.
* **Gatilho de Webhook** – esse gatilho aguarda um cliente toosend-uma solicitação em um ponto de extremidade específico.  Cada solicitação enviada ponto de extremidade de webhook toohello contará como uma execução de ação. Olá solicitação e hello HTTP Webhook gatilho são ambos os gatilhos de webhook.
* **Gatilho de recorrência** – esse gatilho cria uma instância do aplicativo de lógica de saudação com base no intervalo de recorrência de saudação configurado no disparador hello.  Por exemplo, um gatilho de recorrência pode ser configurado toorun a cada três dias ou até mesmo a cada minuto.

Execuções de gatilho podem ser vistas na folha de recursos de aplicativos lógicos Olá no hello parte do histórico de gatilho.

Todas as ações executadas, bem-sucedidas ou não, são limitadas como uma execução de ação.  As ações que foram ignoradas devido a condição de tooa não estão sendo atendida ou ações que não foi executada porque o aplicativo de lógica de saudação encerrado antes da conclusão não são contadas como execuções de ação.

Ações executadas em loops são contadas por iteração do loop de saudação.  Por exemplo, uma única ação em um loop for each iteração por meio de uma lista de 10 itens são contados como número de saudação de itens na lista de saudação (10) multiplicado pelo número de saudação de ações no loop de saudação (1) mais um iniciação de saudação do loop de saudação de , que, neste exemplo, seria (10 * 1) + 1 = 11 execuções de ação.
Os Aplicativos Lógicos desabilitados não podem ter novas instâncias criadas e, portanto, não serão cobrados durante o tempo em que estiverem desabilitados.  Lembre-se de que depois de desabilitar um lógica de aplicativo pode levar algum tempo para Olá instâncias tooquiesce antes que está sendo desativado completamente.
### <a name="integration-account-usage"></a>Uso da conta de integração
Incluído no uso de consumo é um [conta integration](logic-apps-enterprise-integration-create-integration-account.md) para exploração, permitindo que você toouse Olá para fins de teste e desenvolvimento [B2B/EDI](logic-apps-enterprise-integration-b2b.md) e [processamento de XML](logic-apps-enterprise-integration-xml.md)recursos de aplicativos lógicos sem custo adicional. Você está toocreate capaz de um máximo de uma conta por região e armazena até too10 contratos e mapas de 25. Parceiros, certificados e esquemas não têm limites e você pode carregar quantos forem necessários.

Além disso toohello inclusão das contas de integração com o consumo, você pode também criar integração padrão contas sem esses limites e com nosso SLA de aplicativos lógica padrão. Para saber mais, veja [Preços do Azure](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>Planos do Serviço de Aplicativo
Aplicativos de lógica criados anteriormente fazendo referência a um plano de serviço de aplicativo continua toobehave como antes. Dependendo do plano de saudação escolhido, são acelerados depois hello prescritas execuções diárias são excedidas, mas são cobradas usando Olá medidor de execução de ação.
Os clientes EA que têm um plano de serviço de aplicativo em sua assinatura, que não tem toobe explicitamente associado à saudação lógica de aplicativo, terá o benefício de quantidades de saudação incluído.  Por exemplo, se você tiver um plano de serviço de aplicativo padrão em sua assinatura de EA e um aplicativo lógico em Olá a mesma assinatura e você não é cobrados de 10.000 execuções de ação por dia (consulte a tabela a seguir). 

Planos do Serviço de Aplicativo e suas execuções diária de ação permitida:
|  | Gratuito/Compartilhado/Básico | Standard | Premium |
| --- | --- | --- | --- |
| Execuções de ação por dia |200 |10.000 |50.000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Converter de plano de serviço de aplicativo preços tooConsumption
toochange um aplicativo de lógica que tem um plano de serviço de aplicativo associados a ele tooa modelo de consumo, remover Olá referência toohello plano do serviço de aplicativo na definição do aplicativo lógico hello.  Essa alteração pode ser feita com um cmdlet do PowerShell chamada tooa:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Preços
Para obter detalhes sobre preços, confira [Preços de Aplicativos Lógicos](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Próximas etapas
* [Uma visão geral dos Aplicativos Lógicos][whatis]
* [Criar seu primeiro aplicativo lógico][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

