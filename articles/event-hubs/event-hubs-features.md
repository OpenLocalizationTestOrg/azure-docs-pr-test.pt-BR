---
title: "Visão geral de recursos aaaAzure Hubs de eventos | Microsoft Docs"
description: "Visão geral e detalhes sobre os recursos de Hubs de Eventos do Azure"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Visão geral dos recursos de Hubs de Eventos

Os Hubs de Evento do Azure é um serviço de processamento de evento escalonável que recebe e processa grandes volumes de eventos e dados, com baixa latência e alta confiabilidade. Consulte [novidades Hubs de eventos?](event-hubs-what-is-event-hubs.md) para uma visão geral do serviço de saudação.

Este artigo é baseado nas informações Olá Olá [visão geral](event-hubs-what-is-event-hubs.md)e fornece detalhes técnicos e implementação sobre recursos e componentes de Hubs de eventos.

## <a name="event-publishers"></a>Editores de eventos

Qualquer entidade que envia o hub de eventos de tooan de dados é um produtor de evento, ou *publicador do evento*. Os editores de eventos podem publicar eventos usando HTTPS ou AMQP 1.0. Editores de eventos usar um tooidentify de token de assinatura de acesso compartilhado (SAS) se tooan hub de eventos e podem ter uma identidade exclusiva ou usar um token SAS comum.

### <a name="publishing-an-event"></a>Publicar um evento

Você pode publicar um evento por meio do AMQP 1.0 ou HTTPS. Hubs de eventos fornecem [bibliotecas de cliente e classes](event-hubs-dotnet-framework-api-overview.md) para publicação de hub de eventos de tooan eventos de clientes .NET. Para outras plataformas e tempos de execução, você pode usar qualquer cliente AMQP 1.0, como o [Apache Qpid](http://qpid.apache.org/). Você pode publicar eventos individualmente ou em lotes. Uma única publicação (instância de dados do evento) tem um limite de 256 KB, independentemente de ser um único evento ou um lote. Publicar eventos maiores que esse limite resulta em erro. É uma prática recomendada para Publicadores toobe ciente das partições no hub de eventos hello e tooonly especificar um *chave de partição* (introduzido na próxima seção, Olá), ou sua identidade por meio de seu token SAS.

Olá escolha toouse AMQP ou HTTPS é o cenário de uso toohello específico. AMQP requer o estabelecimento de saudação de um soquete bidirecional persistente na adição tootransport nível TLS (segurança) ou SSL/TLS. AMQP possui custos mais altos de rede durante a inicialização de sessão hello, porém HTTPS requer SSL adicional de sobrecarga para cada solicitação. O AMQP tem um melhor desempenho para editores frequentes.

![Hubs de Eventos](./media/event-hubs-features/partition_keys.png)

Hubs de eventos garante que todos os eventos que compartilham um valor de chave de partição sejam entregues em ordem e toohello mesma partição. Se forem usadas chaves de partição com as políticas do publicador, Olá, em seguida, a identidade do publicador hello e valor Olá Olá chave de partição deve corresponder. Caso contrário, ocorrerá um erro.

### <a name="publisher-policy"></a>Política de editor

Os Hubs de Eventos permitem um controle granular sobre os editores de eventos por meio de *políticas do editor*. As políticas do publicador são recursos de tempo de execução projetados toofacilitate grandes números de editores de eventos independentes. Com as políticas do publicador, cada publicador usa seu próprio identificador exclusivo ao publicar o hub de eventos de tooan de eventos, usando Olá mecanismo a seguir:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Você não tem nomes de fornecedores toocreate antecipadamente, mas eles devem coincidir com o token SAS Olá usado ao publicar um evento, em identidades do publicador independentes tooensure ordem. Ao usar as políticas do publicador, Olá **PartitionKey** valor é definido o nome do publicador toohello. toowork adequadamente, esses valores devem corresponder.

## <a name="capture"></a>Captura

[Hubs de evento captura](event-hubs-capture-overview.md) permite tooautomatically captura Olá fluxo de dados em Hubs de eventos e salvá-lo tooyour escolha de uma conta de armazenamento de Blob ou uma conta de serviço do Azure Data Lake. Você pode habilitar a captura de saudação portal do Azure e especificar um tamanho mínimo e a captura de saudação de tooperform de janela de tempo. Usando a captura de Hubs de eventos, você especificar sua própria conta de armazenamento de BLOBs do Azure e o contêiner ou conta de serviço do Azure Data Lake, que é usado toostore Olá os dados capturados. Os dados capturados são gravados em formato do Apache Avro hello.

## <a name="partitions"></a>Partições

Hubs de eventos fornecem por meio de um padrão de consumidor particionado no qual cada consumidor lê somente um subconjunto específico ou partição do fluxo de mensagem de saudação de transmissão de mensagens. Esse padrão permite a escala horizontal para processamento de eventos e fornece outros recursos centrados no fluxo que não estão disponíveis em filas e tópicos.

Uma partição é uma sequência ordenada de eventos que é mantida em um hub de eventos. Conforme novos eventos chegam, eles são adicionados toohello final dessa sequência. Uma partição pode ser pensada como "log de confirmação".

![Hubs de Eventos](./media/event-hubs-features/partition.png)

Hubs de eventos retém dados por um período de retenção configurado que se aplica a todas as partições no hub de eventos de saudação. Eventos expiram periodicamente; não é possível excluí-los explicitamente. Como as partições são independentes e contêm sua própria sequência de dados, elas geralmente crescem a taxas diferentes.

![Hubs de Eventos](./media/event-hubs-features/multiple_partitions.png)

número de saudação de partições é especificado no momento da criação e deve estar entre 2 e 32. Contagem de partição de saudação não é mutável, portanto você deve considerar a longo prazo escala quando a contagem de partição de configuração. As partições são um mecanismo de organização de dados que relaciona toohello paralelismo de downstream necessário em aplicativos de consumo. Olá número de partições em um hub de eventos está diretamente relacionada toohello número de leitores simultâneos esperado toohave. Você pode aumentar o número de saudação de partições além 32 entrando em contato com a equipe de Hubs de eventos de saudação.

Enquanto partições identificadas e podem ser enviadas toodirectly, não é recomendável enviar diretamente tooa partição. Em vez disso, você pode usar construções de nível superior, introduzidas no hello [publicador do evento](#event-publishers) e [capacidade](#capacity) seções. 

As partições são preenchidas com uma sequência de dados de evento que contém o corpo de saudação do evento hello, um recipiente de propriedades definidas pelo usuário e metadados, como seu deslocamento na partição hello e seu número de sequência de fluxo de saudação.

Para obter mais informações sobre partições e compensação de saudação entre disponibilidade e confiabilidade, consulte Olá [guia de programação de Hubs de eventos](event-hubs-programming-guide.md#partition-key) e hello [disponibilidade e a consistência nos Hubs de eventos](event-hubs-availability-and-consistency.md) artigo .

### <a name="partition-key"></a>Chave de partição

Você pode usar um [chave de partição](event-hubs-programming-guide.md#partition-key) toomap dados de eventos recebidos em partições específicas para finalidade de saudação da organização de dados. chave de partição de saudação é um valor fornecido pelo remetente passado para um hub de eventos. Ela é processada por meio de uma função de hash estática, que cria a atribuição de partição hello. Se você não especificar uma chave de partição ao publicar um evento, uma atribuição de round robin será usada.

publicador do evento Olá só está ciente da sua chave de partição não Olá partição toowhich Olá eventos são publicados. Essa desassociação de partição e chave separa o remetente de saudação da necessidade tooknow muito sobre processamento de downstream hello. Um por dispositivo ou usuário exclusivo identidade faz com que uma chave de partição boa, mas outros atributos, como geografia também podem ser usado toogroup eventos relacionados em uma única partição.

## <a name="sas-tokens"></a>Tokens SAS

Hubs de eventos usa *assinaturas de acesso compartilhado*, que estão disponível no nível de hub de namespace e o evento de saudação. Um token SAS é gerado a partir de uma chave de SAS e é um hash SHA de uma URL, codificado em um formato específico. Usando o nome de saudação da chave hello (política) e token Olá, Hubs de eventos pode regenerar o hash de saudação e se autenticarem remetente hello. Normalmente, os tokens SAS para editores de eventos são criados apenas com privilégios de **enviar** em um hub de eventos específico. Esse mecanismo de URL de token SAS é a base de saudação para identificação de Publicadores introduzidos na política de publicador hello. Para saber mais sobre como trabalhar com SAS, confira [Autenticação de assinatura de acesso compartilhado com o Barramento de Serviço](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Consumidores de evento

Qualquer entidade que lê dados de evento de um hub de eventos é um *consumidor de eventos*. Todos os consumidores de Hubs de eventos se conectar por meio da sessão de saudação AMQP 1.0 e eventos são entregues por meio de sessão Olá assim que estiverem disponíveis. Olá cliente não necessita de toopoll para disponibilidade de dados.

### <a name="consumer-groups"></a>Grupos de consumidores

mecanismo de publicação/assinatura Olá dos Hubs de eventos é habilitado por meio de *grupos de consumidores*. Um grupo de consumidores é uma exibição (estado, posição ou deslocamento) de todo um hub de eventos. Grupos de consumidores permitem que vários aplicativos de consumo tooeach tem uma exibição separada de fluxo de eventos hello e fluxo de saudação tooread independentemente em seu próprio ritmo e com seus próprio deslocamentos.

Em um arquitetura de processamento de fluxo, cada aplicativo de downstream equivale tooa grupo de consumidores. Se desejar que o armazenamento de termo toolong de dados de evento toowrite, esse aplicativo do gravador de armazenamento é um grupo de consumidores. O processamento de eventos complexos pode então ser executado por outro grupo separado de consumidores. Você pode acessar partições somente por meio de um grupo de consumidores. Pode haver no máximo cinco leitores simultâneos em uma partição por grupo de consumidores. No entanto **recomenda-se que haja apenas um receptor ativo em uma partição por grupo de consumidores**. Sempre há um grupo de consumidores padrão em um hub de eventos, e você pode criar os grupos de consumidor too20 para um hub de eventos de camada padrão.

Olá seguem exemplos de convenção de URI do grupo de consumidor de saudação:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Olá figura a seguir mostra arquitetura de processamento de fluxo Olá Hubs de eventos:

![Hubs de Eventos](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Deslocamentos de fluxo

Um *deslocamento* é Olá posição de um evento dentro de uma partição. Você pode pensar em um deslocamento como um cursor do lado do cliente. Olá, deslocamento é um byte numeração de evento hello. Esse deslocamento permite que um consumidor (leitor) de evento toospecify um ponto no fluxo de eventos de saudação do qual eles desejam toobegin ler eventos. Você pode especificar o deslocamento de saudação como um carimbo de hora ou como um valor de deslocamento. Os consumidores são responsáveis por armazenar seu próprios valores de deslocamento fora Olá serviço de Hubs de eventos. Dentro de uma partição, cada evento inclui um deslocamento.

![Hubs de evento](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Ponto de verificação

*Ponto de verificação* é um processo pelo qual os leitores marcam ou confirmam sua posição em uma sequência de eventos da partição. Ponto de verificação é responsabilidade de saudação do consumidor hello e ocorre em uma base por partição dentro de um grupo de consumidores. Essa responsabilidade significa que para cada grupo de consumidores, cada leitor de partição deve manter o controle de sua posição atual no fluxo de eventos Olá e pode informar o serviço hello quando considera que o fluxo de dados Olá concluída.

Se um leitor se desconectar de uma partição, quando ele se reconectar e começar a ler no ponto de verificação de saudação que foi anteriormente enviado pelo Olá último leitor dessa partição nesse grupo de consumidores. Quando a saudação leitor se conecta, ele passa esse deslocamento toohello evento hub toospecify Olá local no qual a leitura toostart. Dessa forma, você pode usar eventos do ponto de verificação tooboth marcados como "Concluir" por aplicativos de downstream e ocorre tooprovide resiliência se um failover entre leitores em execução em máquinas diferentes. É possível tooreturn tooolder dados especificando um deslocamento inferior desse processo de ponto de verificação. Por meio desse mecanismo, o ponto de verificação permite resiliência de failover e reprodução de fluxo de eventos.

### <a name="common-consumer-tasks"></a>Tarefas comuns do consumidor

Todos os consumidores de Hubs de Eventos se conectam por meio de uma sessão do AMQP 1.0, um canal de comunicação bidirecional com reconhecimento de estado. Cada partição tem uma sessão do AMQP 1.0 que facilita o transporte de saudação de eventos separados por partição.

#### <a name="connect-tooa-partition"></a>Conecte-se a partição tooa

Ao conectar-se toopartitions, é comum toouse prática uma concessão de partições de toospecific de conexões do mecanismo toocoordinate leitor. Dessa forma, é possível para cada partição em um consumidor grupo toohave apenas um leitor ativo. Ponto de verificação, aluguel e gerenciamento leitores são simplificados pelo uso Olá [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) classe para clientes do .NET. Olá Host de processador de eventos é um agente de cliente inteligente.

#### <a name="read-events"></a>Ler eventos

Depois que uma sessão do AMQP 1.0 e o link é aberto para uma partição específica, os eventos são entregues cliente toohello AMQP 1.0 pelo Olá serviço de Hubs de eventos. Esse mecanismo de entrega permite uma maior taxa de transferência e menor latência que mecanismos baseado em pull, como HTTP GET. Como os eventos são enviados toohello cliente, cada instância de dados do evento contém metadados importantes como o número de deslocamento e de sequência de saudação que são pontos de verificação toofacilitate usada na sequência de eventos de saudação.

Dados de evento:
* Deslocamento
* Número de sequência
* Corpo
* Propriedades do usuário
* Propriedades do sistema

É o deslocamento de saudação toomanage responsabilidade.

## <a name="capacity"></a>Capacity

Hubs de eventos tem uma arquitetura paralela altamente dimensionável e há várias tooconsider fatores importantes ao dimensionar.

### <a name="throughput-units"></a>Unidades de transferência

capacidade de rendimento Olá dos Hubs de eventos é controlada pelo *unidades de taxa de transferência*. As unidades de taxa de transferência são unidades de capacidade pré-adquiridas. Uma unidade única de taxa de transferência inclui Olá capacidade a seguir:

* Entrada: backup too1 MB por segundo ou 1000 eventos por segundo (o que vier primeiro)
* Saída: backup too2 MB por segundo

Além da capacidade de saudação do hello adquirido unidades de taxa de transferência, a entrada está limitada e um [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) é retornado. Saída não gera exceções de limitação, mas é a capacidade de toohello ainda limitado de saudação adquirida unidades de taxa de transferência. Se você receber exceções de taxa de publicação ou esperava saída superior toosee, ser toocheck se quantas unidades de taxa de transferência você comprou para o namespace de saudação. Você pode gerenciar as unidades de taxa de transferência em Olá **escala** folha de namespaces Olá Olá [portal do Azure](https://portal.azure.com). Você também pode gerenciar unidades de taxa de transferência programaticamente usando Olá [APIs de Hubs de evento](event-hubs-api-overview.md).

As unidades de taxa de transferência são cobradas por hora e são pré-adquiridas. Depois de adquiridas, as unidades de taxa de transferência são cobradas por um mínimo de uma hora. Backup too20 unidades de taxa de transferência podem ser adquiridas para um namespace de Hubs de eventos em são compartilhadas entre todos os Hubs de eventos no namespace de saudação.

Mais unidades de taxa de transferência podem ser compradas em blocos de 20 unidades de taxa de transferência too100, entrando em contato com o suporte do Azure. Além disso, você também pode comprar blocos de 100 unidades de transferência.

É recomendável que você equilibre a taxa de transferência partições e unidades tooachieve dimensionamento ideal. Uma única partição tem uma escala máxima de uma unidade de transferência. Olá número de unidades de taxa de transferência deve ser menor ou igual toohello número de partições em um hub de eventos.

Para obter informações detalhadas sobre o preço de Hubs de Eventos, consulte [Preço de Hubs de Eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Hubs de eventos, visite Olá links a seguir:

* Introdução com um [Tutorial de Hubs de Eventos][Event Hubs tutorial]
* [Guia de programação dos Hubs de Eventos](event-hubs-programming-guide.md)
* [Disponibilidade e consistência nos Hubs de Eventos](event-hubs-availability-and-consistency.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)
* [Exemplos de Hubs de Eventos][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Exemplos de Hubs de Eventos]: https://github.com/Azure/azure-event-hubs/tree/master/samples
