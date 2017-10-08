---
title: aaaIntroduction tooAzure Advisor | Microsoft Docs
description: "Use o Azure Advisor toooptimize as implantações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Introdução tooAzure Advisor

Saiba mais sobre o Supervisor do Azure e seus principais recursos e obter respostas toofrequently perguntas frequentes.

## <a name="what-is-advisor"></a>O que é o Assistente?
O Supervisor é um consultor de nuvem personalizados que ajuda você a segue toooptimize de práticas recomendada as implantações do Azure. Ele analisa a configuração de recurso e telemetria de uso e então recomenda soluções que podem ajudar a melhoram a economia hello, desempenho, alta disponibilidade e segurança de seus recursos do Azure.

Com o Assistente, é possível:
* Obter recomendações de melhores práticas proativas, personalizadas e prontas para uso. 
* Melhore o desempenho hello, segurança e alta disponibilidade de seus recursos, conforme você identificar oportunidades tooreduce gastos do Azure geral.
* Obter recomendações com ações propostas embutidas.

Você pode acessar o Advisor por meio de saudação [portal do Azure](https://aka.ms/azureadvisordashboard). Entrar toohello [portal](https://portal.azure.com), selecione **procurar**e, em seguida, role muito**Advisor Azure**. Painel de Supervisor Olá exibe recomendações personalizadas para uma assinatura selecionada. 

recomendações de saudação são divididas em quatro categorias: 

* **Alta disponibilidade**: tooensure e melhorar a continuidade da saudação de seus aplicativos essenciais aos negócios. Para saber mais, veja [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Recomendações de alta disponibilidade do Advisor).

* **Segurança**: toodetect ameaças e vulnerabilidades que podem levar a falhas de toosecurity. Para saber mais, veja [Advisor Security recommendations](advisor-security-recommendations.md) (Recomendações de segurança do Advisor).

* **Desempenho**: velocidade de saudação tooimprove de seus aplicativos. Para saber mais, veja [Advisor Performance recommendations](advisor-performance-recommendations.md) (Recomendações de desempenho do Advisor).

* **Custo**: toooptimize e reduzir seu Azure geral gastos. Para saber mais, veja [Advisor Cost recommendations](advisor-cost-recommendations.md) (Recomendações de custo do Advisor).

  ![Tipos de recomendação do Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor. Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão. Essa é uma *operação única*. Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.

Você pode clicar em um toolearn recomendação mais sobre ele. Você também pode aprender sobre as ações que você pode executar tootake aproveitar a oportunidade ou resolver um problema. 

O Advisor oferece recomendações com ações embutidas ou links de documentação. Clicando em uma ação embutido leva você através de um "jornada de usuário interativa" tooimplement-lo. Clicar em um link de documentação pontos toodocumentation que descreve como implementar a ação de saudação toomanually. 

O Assistente atualiza as recomendações a cada hora. Se você não pretende tootake uma ação imediata em uma recomendação, você pode adiar a ele por um período de tempo especificado ou descartá-lo. 

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="how-do-i-access-advisor"></a>Como acesso o Advisor?
Você pode acessar o Advisor por meio de saudação [portal do Azure](https://aka.ms/azureadvisordashboard). Entrar toohello [portal](https://portal.azure.com), selecione **procurar**e, em seguida, role muito**Advisor Azure**. Painel de Supervisor Olá exibe recomendações personalizadas para uma assinatura selecionada. 

Você também pode exibir as recomendações do orientador por meio de folha de recursos de máquina virtual de saudação. Escolha uma máquina virtual e, em seguida, role recomendações tooAdvisor no menu de saudação. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>O que fazem permissões preciso tooaccess Advisor?

tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor. Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão. Essa é uma *operação única*. Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.

### <a name="how-often-are-advisor-recommendations-updated"></a>Com que frequência as recomendações do Advisor são atualizadas?

As recomendações do Assistente são atualizadas a cada hora.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Para quais recursos o Advisor fornece recomendações?

O Assistente fornece recomendações para máquinas virtuais, conjuntos de disponibilidade, gateways de aplicativo, Serviços de Aplicativos, SQL Servers, bancos de dados SQL e para o Cache Redis.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>Posso adiar ou descartar uma recomendação?

toosnooze ou ignorar uma recomendação, clique em Olá **adiar** botão ou link. Você pode especificar uma hora de adiamento Períoda ou selecione **nunca** toodismiss Olá recomendação.

## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre recomendações do Advisor, consulte:

* [Introdução ao Advisor](advisor-get-started.md)
* [Recomendações de alta disponibilidade do Advisor](advisor-high-availability-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-security-recommendations.md)
* [Recomendações de desempenho do Advisor](advisor-performance-recommendations.md)
* [Recomendações de custo do Advisor](advisor-cost-recommendations.md)
