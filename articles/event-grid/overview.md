---
title: "Visão geral de grade de eventos aaaAzure"
description: Descreve a Grade de Eventos do Azure e seus conceitos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Uma grade de eventos de tooAzure de Introdução

Grade de eventos do Azure permite que você tooeasily na criação de aplicativos com as arquiteturas de evento. Selecione o hello recursos do Azure, você deseja toosubscribe para e dar o manipulador de eventos hello ou WebHook ponto de extremidade toosend Olá evento. A Grade de Eventos tem suporte interno para eventos provenientes de serviços do Azure, como blobs de armazenamento e grupos de recursos. A Grade de Eventos também tem suporte personalizado para eventos de aplicativo e de terceiros, usando webhooks e tópicos personalizados. 

Você pode usar filtros tooroute eventos específicos toodifferent pontos de extremidade, pontos de extremidade toomultiple multicast e verifique se que os eventos são distribuídos de forma confiável. A Grade de Eventos também tem suporte interno para eventos personalizados e de terceiros.

Versão de visualização hello, oferece suporte a grade de eventos **westus2** e **westcentralus** locais. Outras regiões serão adicionadas.

Este artigo fornece uma visão geral da Grade de Eventos do Azure. Se você quiser tooget iniciado com a grade de eventos, consulte [rota e criar eventos personalizados com a grade de eventos do Azure](custom-event-quickstart.md).

![Modelo funcional da Grade de Eventos](./media/overview/event-grid-functional-model.png)

Atualmente, o Armazenamento de Blobs não está disponível publicamente como um publicador.

## <a name="concepts"></a>Conceitos

Há cinco conceitos na Grade de Eventos do Azure para sua utilização:

* **Eventos**: o que aconteceu.
* **Fontes de evento/editores** - onde o evento Olá ocorreu.
* **Tópicos** -Olá onde Publicadores enviam eventos de ponto de extremidade.
* **Assinaturas de evento** -eventos de tooroute de mecanismo de ponto de extremidade ou interna de hello, às vezes, toomultiple manipuladores. As assinaturas também são usadas pelos eventos de entrada manipuladores toointelligently filtro.
* **Manipuladores de eventos** - Olá aplicativo ou serviço reagindo toohello eventos.

Para saber mais sobre esses conceitos, confira [Conceitos na Grade de Eventos do Azure](concepts.md).

## <a name="capabilities"></a>Funcionalidades

Aqui estão alguns dos principais recursos Olá da grade de eventos do Azure:

* **Simplicidade** -ponto e clique em eventos de tooaim do seu manipulador de eventos de tooany de recursos do Azure ou o ponto de extremidade.
* **Filtragem avançada** -filtro de evento de tipo ou evento publicar caminho tooensure manipuladores de eventos somente recebem eventos relevantes.
* **Fan-out** -assinar toohello de vários pontos de extremidade toosend do mesmo evento copia de saudação evento tooas em muitos lugares conforme necessário.
* **Confiabilidade** -utilizar 24 horas de repetição com retirada exponencial tooensure eventos são entregues.
* **Pagamento por evento** - pagar apenas para a quantidade de saudação você usar a grade de eventos.
* **Alta taxa de transferência**: crie cargas de trabalho de alto volume na Grade de Eventos com suporte para milhões de eventos por segundo.
* **Eventos internos**: comece a executar rapidamente com eventos internos definidos pelo recurso.
* **Eventos personalizados**: use eventos personalizados de rota, filtro e entrega confiável da de Grade de Eventos em seu aplicativo.

## <a name="built-in-publisher-and-handler-integration"></a>Integração interna entre publicador e manipulador

O Azure oferece suporte interno a eventos usando vários serviços, incluindo publicadores e manipuladores.

### <a name="publishers"></a>Publicadores

No momento, hello seguintes serviços do Azure tem suporte do publicador internos para grade de eventos:

* Grupos de recursos (operações de gerenciamento)
* Assinaturas do Azure (operações de gerenciamento)
* Hubs de Eventos
* Tópicos personalizados

Outros serviços do Azure serão adicionados neste ano.

### <a name="handlers"></a>Manipuladores

No momento, hello seguintes serviços do Azure tem suporte para grade de eventos internos do manipulador: 

* Funções do Azure
* Aplicativos Lógicos
* Automação do Azure
* WebHooks

Outros serviços do Azure serão adicionados neste ano.

## <a name="what-can-i-do-with-event-grid"></a>O que posso fazer com a Grade de Eventos?

A Grade de Eventos do Azure fornece vários recursos que melhoram muito o trabalho sem servidor, de automação de operações e de integração: 

### <a name="serverless-application-architectures"></a>Arquiteturas de aplicativo sem servidor

![Aplicativo sem servidor](./media/overview/serverless_web_app.png)

A Grade de Eventos conecta fontes de dados e manipuladores de eventos. Por exemplo, o gatilho do evento grade tooinstantly use uma análise de imagem de toorun função sem servidor cada vez que uma nova foto é adicionado tooa contêiner de armazenamento de blob. 

### <a name="ops-automation"></a>Automação de operações

![Automação de operações](./media/overview/Ops_automation.png)

Grade de eventos permite automação toospeed e simplificar a imposição de política. Por exemplo, a Grade de Eventos pode notificar a Automação do Azure quando uma máquina virtual é criada ou um Banco de Dados SQL é criado. Esses eventos podem ser usados tooautomatically Verifique se as configurações de serviço são compatíveis, colocar metadados em ferramentas de operações, máquinas virtuais de marca ou itens de trabalho do arquivo.

### <a name="application-integration"></a>Integração de aplicativos

![Integração de aplicativos](./media/overview/app_integration.png)

A Grade de Eventos conecta seu aplicativo a outros serviços. Por exemplo, criar um tópico personalizado toosend tooEvent de dados de eventos do aplicativo grade e aproveitar sua entrega confiável, avançada de roteamento e a integração direta com o Azure. Como alternativa, você pode usar a grade de eventos com os dados de tooprocess aplicativos lógicos em qualquer lugar, sem escrever código. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Qual é a diferente entre a Grade de Eventos e outros serviços de integração do Azure?

A Grade de Eventos é um backplane de eventos que permite a programação reativa e controlada por evento. Ela está profundamente integrada aos serviços do Azure e pode ser integrada aos serviços de terceiros. mensagem de saudação do evento contém informações de saudação necessárias toochanges tooreact em serviços e aplicativos. Grade de eventos não é um pipeline de dados e não fornecer Olá real do objeto que foi atualizado.

O Barramento de Serviço é adequado para aplicativos corporativos tradicionais que exigem transações, ordenação, detecção de duplicidades e consistência instantânea. A Grade de Eventos foi desenvolvida para proporcionar velocidade, escala, amplitude e baixo custo em um modelo reativo. É mais adequado tooserverless arquitetura.

A Grade de Eventos complementa outros serviços do Azure como Aplicativos Lógicos e Hubs de Eventos. Os disparadores de evento grade Olá lógica aplicativo toobegin seu fluxo de trabalho. Hubs de evento funciona com a grade de eventos, permitindo que você tooevents tooreact de Hubs de evento captura e pipelines de ingresso e transformação de dados de compilação.

## <a name="how-much-does-event-grid-cost"></a>Quanto custa a Grade de Eventos?

A Grade de Eventos do Azure usa um modelo de preço de pagamento por evento, para que você pague só pelo que usa.

Grade de eventos custa US $0,60 por milhão de operações (US $0,30 durante a visualização) e Olá primeiro 100.000 operação por mês são gratuitos. As operações são definidas como ingresso de evento, correspondência avançada, tentativa de entrega e chamadas de gerenciamento.  Mais detalhes podem ser encontrados em Olá [página de preços](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Próximas etapas

* [Criar e assinar eventos toocustom](custom-event-quickstart.md) imediatamente e começar a enviar seu próprio ponto de extremidade de tooany eventos personalizados usando o início rápido do hello grade de eventos do Azure.
* [Usando a lógica de aplicativos como um manipulador de eventos](monitor-virtual-machine-changes-event-grid-logic-app.md) um tutorial sobre como criar um aplicativo usando aplicativos lógicos tooreact tooevents enviada por grade de eventos.
* [Referência da API REST da Grade de Eventos](/rest/api/eventgrid)  
  Fornece mais informações técnicas sobre Olá grade de eventos do Azure e uma referência para o gerenciamento de assinaturas de evento de roteamento e filtragem.
