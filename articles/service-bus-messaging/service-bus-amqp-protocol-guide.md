---
title: "aaaAMQP 1.0 no guia de protocolo do barramento de serviço do Azure e Hubs de eventos | Microsoft Docs"
description: "Protocolo guia tooexpressions e a descrição do AMQP 1.0 no barramento de serviço do Azure e Hubs de eventos"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# AMQP 1.0 no guia de protocolo do Barramento de Serviço e dos Hubs de Eventos do Azure

Olá Advanced Message Queueing protocolo 1.0 é um protocolo de enquadramento e transferência padronizado para transferir mensagens de forma assíncrona, segura e confiável entre duas partes. É protocolo primário Olá mensagens do barramento de serviço do Azure e Hubs de eventos do Azure. Ambos os serviços também oferecem suporte a HTTPS. protocolo SBMP proprietário Olá que também é suportado está sendo desativado em favor do AMQP.

AMQP 1.0 é resultado de saudação de colaboração do setor que reuniu fornecedores de middleware, como Microsoft e Red Hat, com muitos usuários de middleware de mensagens como JP Morgan Chase representando o setor de serviços financeiros hello. Fórum de padronização técnica Olá para especificações de protocolo e a extensão do AMQP Olá é OASIS, e ele obteve aprovação formal como um padrão internacional como ISO/IEC 19494.

## Metas

Este artigo resume os conceitos básicos de saudação da especificação de mensagens de saudação AMQP 1.0 junto com um pequeno conjunto de especificações de extensão de rascunho que estão atualmente sendo finalizado no comitê técnico do OASIS AMQP Olá rapidamente e explica como o Azure Service Bus implementa e cria nessas especificações.

meta de saudação é para qualquer desenvolvedor usando qualquer pilha de cliente existente do AMQP 1.0 em qualquer toobe de plataforma capaz de toointeract com o barramento de serviço do Azure por meio do AMQP 1.0.

As pilhas de finalidade geral comuns do AMQP 1.0, como o Apache Proton ou o AMQP.NET Lite, já implementam todos os gestos principais do AMQP 1.0. Esses gestos fundamentais, às vezes, são encapsulados com uma API de nível superior; Proton do Apache mesmo oferece dois, Olá API fundamental do Messenger e Olá API de reator reativa.

Olá discussão a seguir, vamos supor que o gerenciamento de Olá de links e hello manipulação de transferências de quadro e controle de fluxo, sessões e conexões AMQP são tratados pela pilha de respectivos hello (como o Apache Proton-C) e não exigem muito se houver específico atenção de desenvolvedores de aplicativos. Abstrata pressupomos existência Olá alguns primitivos de API como Olá capacidade tooconnect e toocreate alguma forma de *remetente* e *receptor* objetos de abstração, que, em seguida, têm alguma forma de `send()`e `receive()` operações, respectivamente.

Ao discutir os recursos avançados do Barramento de Serviço do Azure, como a procura de mensagens ou o gerenciamento de sessões, eles são explicados nos termos do AMQP, mas também como uma pseudoimplementação em camadas sobre essa abstração de API assumida.

## O que é AMQP?

AMQP é um protocolo de enquadramento e transferência. O enquadramento significa que ele fornece a estrutura para fluxos de dados binários que fluem em qualquer direção de uma conexão de rede. estrutura Olá fornece delineação para diferentes blocos de dados, chamado *quadros*, toobe trocadas entre partes Olá conectado. capacidade de transferência Olá Certifique-se de que ambas as partes da comunicação podem estabelecer uma compreensão geral sobre quando quadros devem ser transferidos e quando transferências devem ser consideradas concluídas.

Ao contrário das anteriormente expiradas rascunho versões produzidas pelo grupo de trabalho do AMQP Olá que ainda estão em uso por alguns agentes de mensagens, o protocolo AMQP 1.0 final e padronizado do grupo de trabalho Olá não estabelece presença de saudação de qualquer topologia específica ou um agente de mensagens para entidades dentro de um agente de mensagens.

protocolo de saudação pode ser usado para comunicação ponto a ponto simétrica para interação com os agentes de mensagens que oferecem suporte a filas e entidades de publicação/assinatura, como o Azure Service Bus. Ele também pode ser usado para interação com a infraestrutura de mensagens onde padrões de interação de saudação são diferentes das filas regulares, como Olá caso com Hubs de eventos do Azure. Um Hub de eventos atua como uma fila quando tooit os eventos são enviados, mas mais atua como um serviço de armazenamento serial quando os eventos são lidos a partir dela; ele é um pouco semelhante a uma unidade de fita. cliente Olá escolhe um deslocamento no fluxo de dados disponíveis hello e, em seguida, é fornecido a todos os eventos desse deslocamento toohello mais recente disponível.

Olá protocolo AMQP 1.0 é projetado toobe extensíveis, permitindo mais especificações tooenhance seus recursos. especificações de extensão três Olá abordadas neste documento ilustram isso. Para comunicação HTTPS para o WebSocket infraestrutura onde pode ser difícil configurar portas de TCP AMQP nativo hello, uma especificação de associação define como toolayer AMQP por meio de WebSockets. Para interagir com a infraestrutura de mensagens de saudação em uma solicitação/resposta maneira para fins de gerenciamento ou funcionalidade tooprovide avançado, especificação de gerenciamento do AMQP Olá define Olá necessária interação básica primitivos. Para a integração de modelo de autorização federado, Olá especificações de segurança com base em declarações AMQP define como tooassociate e renovação de tokens de autorização associados links.

## Cenários básicos de AMQP

Esta seção explica o uso básico de saudação do AMQP 1.0 com o barramento de serviço do Azure, que inclui a criação de conexões, sessões e links e a transferência de mensagens tooand de entidades do barramento de serviço, como filas, tópicos e assinaturas.

Olá toolearn de fonte autoritativa mais sobre como funciona o AMQP é a especificação de saudação AMQP 1.0, mas a especificação de saudação foi gravada tooprecisely implementação de guia e o protocolo de saudação do tooteach. Esta seção se concentra na introdução da terminologia necessária para descrever como o Barramento de Serviço usa o AMQP 1.0. Para um tooAMQP introdução mais abrangente, bem como uma discussão mais ampla do AMQP 1.0, você pode examinar [deste curso de vídeo][this video course].

### Conexões e sessões

Saudação de chamadas AMQP comunicação programas *contêineres*; esses contêm *nós*, que Olá comunicando entidades dentro desses contêineres. Uma fila pode ser um nó assim. AMQP permite multiplexação, para que uma única conexão possa ser usada para vários caminhos de comunicação entre nós. Por exemplo, um cliente de aplicativo simultaneamente receber uma fila e enviar tooanother sobre Olá mesma conexão de rede.

![][1]

conexão de rede Hello, portanto, está ancorado no contêiner de saudação. Ele é iniciado pelo contêiner Olá na função de saudação do cliente fazendo um saída contêiner de tooa de conexão de soquete TCP na função de destinatário hello, que escuta e aceita conexões TCP de entrada. handshake de conexão de saudação inclui negociar a versão do protocolo hello, declarando ou negociar uso Olá de segurança em nível de transporte (TLS/SSL) e um handshake de autenticação/autorização no escopo da conexão Olá se baseia em SASL.

Barramento de serviço do Azure requer o uso de saudação de TLS em todos os momentos. Ele oferece suporte a conexões pela porta TCP 5671, por meio da qual hello conexão TCP primeiro sobreposto com TLS antes de inserir o handshake do protocolo AMQP Olá e também oferece suporte a conexões pela porta TCP 5672 no qual o servidor de saudação imediatamente dá uma atualização obrigatória de tooTLS de conexão usando Olá prescrita AMQP modelo. associação de WebSockets do AMQP Olá cria um túnel pela porta TCP 443 é então 5671 conexões tooAMQP equivalente.

Depois de configurar a conexão de saudação e TLS, o barramento de serviço oferece duas opções de mecanismo SASL:

* SASL simples normalmente é usado para transmitir o servidor de tooa de credenciais de nome de usuário e senha. O Barramento de Serviço não tem contas, mas [regras de Segurança de Acesso Compartilhado](service-bus-sas.md) nomeadas, que conferem direitos e estão associadas com uma chave. nome de saudação de uma regra é usado como nome de usuário de saudação e a chave de saudação (como o texto de codificado na base64) é usado como senha hello. direitos de saudação associados Olá escolhido regra dirigem as operações de saudação permitidas na conexão de saudação.
* SASL ANÔNIMA é usada para ignorar a autorização de SASL quando o cliente Olá quer toouse Olá segurança com base em declarações (CBS) modelo é descrito posteriormente. Com essa opção, uma conexão de cliente pode ser estabelecido anonimamente para um curto período de tempo durante o qual Olá cliente só pode interagir com o ponto de extremidade do hello CBS e handshake CBS Olá deve concluir.

Depois de estabelecida a conexão de transporte Olá, contêineres de saudação cada declarar tamanho máximo do quadro de saudação são disposto toohandle e, após um tempo limite de ociosidade eles forma unilateral serão desconectar se não houver nenhuma atividade na conexão hello.

Eles também declararam quantos canais simultâneos têm suporte. Um canal é um caminho de transferência unidirecional, saída, virtual sobre conexão hello. Uma sessão usa um canal de cada caminho de comunicação do hello contêineres interconectadas tooform espelhamento bidirecional.

Sessões têm um modelo de controle de fluxo baseado na janela; Quando uma sessão é criada, cada parte declara quantos quadros tooaccept disposto em sua janela de recebimento. Como hello partes quadros do exchange, transferidos quadros preencher a janela e transferências de interromper quando a janela hello está cheio e até que a janela Olá é redefinida ou expandido usando Olá *fluxo performative* (*performative*é Olá AMQP termo para gestos de nível de protocolo trocadas entre partes Olá duas).

Esse modelo baseado no Windows é quase análoga toohello conceito TCP de controle de fluxo baseado no Windows, mas no nível de sessão hello dentro de soquete hello. Olá conceito do protocolo de permitir que várias sessões simultâneas existe para que o tráfego de alta prioridade pode ser com pressa após tráfego normal limitado, como em uma rota expressa de estrada.

Atualmente, o Barramento de Serviço do Azure usa exatamente uma sessão para cada conexão. Olá quadro-tamanho máximo de barramento de serviço é 262.144 bytes (256 K bytes) para o padrão de barramento de serviço e Hubs de eventos. Ele é de 1.048.576 (1 MB) para o Barramento de Serviço Premium. Barramento de serviço não impõe qualquer janela de limitação de nível de sessão específica, mas redefinições Olá janela regularmente como parte do controle de fluxo de nível de link (consulte [Olá próxima seção](#links)).

As conexões, os canais e as sessões são efêmeros. Se a conexão subjacente Olá recolhe, conexões, o túnel TLS, o contexto de autorização SASL e sessões devem ser restabelecidas.

### Links

O AMQP transfere mensagens sobre links. Um link é um caminho de comunicação criado em uma sessão que permite transferir mensagens em uma direção; negociação de status de transferência de saudação é link hello e bidirecionais entre as partes de saudação conectada.

![][2]

Links podem ser criados por um contêiner a qualquer momento e em uma sessão existente, o que torna o AMQP diferente de muitos outros protocolos, incluindo HTTP e MQTT, onde a iniciação de saudação de transferência e o caminho de transferência é um privilégio exclusivo da parte Olá criando conexão de soquete Hello.

contêiner de link da inicialização Olá solicita Olá oposta contêiner tooaccept um link e escolhe uma função do remetente ou destinatário. Portanto, o contêiner pode iniciar a criação unidirecional ou caminhos de comunicação bidirecional, com hello último modelada como pares de links.

Os links são nomeados e associados a nós. Conforme mencionado no início de hello, os nós são Olá comunicação entidades dentro de um contêiner.

No barramento de serviço, um nó é diretamente equivalente tooa fila, um tópico, uma assinatura ou uma subfila de mensagens mortas de uma fila ou assinatura. Portanto, o nome do nó de Olá usado em AMQP é nome relativo do hello da entidade hello dentro do namespace de barramento de serviço hello. Se uma fila for chamada de **myqueue**, esse também será o nome do nó AMQP. Uma assinatura de tópico segue a convenção de API HTTP de saudação por que estão sendo classificadas em uma coleção de recursos "assinaturas" e, assim, uma assinatura **sub** ou um tópico **mytopic** tem o nome do nó Olá AMQP **assinaturas/mytopic/sub**.

cliente conectado Olá também é necessário toouse um nome de nó local para criar links; Barramento de serviço não é prescritivo sobre esses nomes de nó e não interpretá-los. Pilhas de cliente do AMQP 1.0 geralmente usam um tooassure esquema esses nomes de nó efêmera são exclusivos no escopo de saudação do cliente hello.

### Transferências

Após o estabelecimento de um link, as mensagens podem ser transferidas sobre esse link. AMQP, uma transferência é executada com um gesto de protocolo explícita (Olá *transferência* performative) que move uma mensagem de remetente tooreceiver em um link. Uma transferência é concluída quando ele é "estabelecido", que significa que ambas as partes tiveram estabelecido uma compreensão de resultado de saudação dessa transferência.

![][3]

No caso mais simples de hello, remetente Olá pode escolher toosend mensagens "previamente estabelecidas", que significa que o cliente Olá não estiver interessado em resultado hello e receptor Olá não fornece nenhum feedback sobre o resultado de saudação da operação de saudação. Esse modo é suportado pela barramento de serviço Olá nível de protocolo AMQP, mas não exposto em qualquer uma das APIs de cliente hello.

Hello caso regular é que as mensagens estão sendo enviadas em vez e receptor hello, indica a aceitação ou rejeição usando Olá *disposição* performative. Rejeição ocorre quando o receptor Olá não pode aceitar a mensagem de saudação por qualquer motivo, e rejeição mensagem contém informações sobre o motivo de saudação, que é uma estrutura de erro definido por AMQP. Se as mensagens são rejeitadas devido a erros de toointernal dentro de barramento de serviço, o serviço de saudação retornará informações extras dentro de estrutura que pode ser usada para fornecer o diagnóstico pessoal de toosupport dicas, se você estiver preenchendo as solicitações de suporte. Posteriormente, você aprenderá mais detalhes sobre os erros.

Uma forma especial de rejeição é hello *liberado* de estado, que não indica que esse destinatário Olá tem nenhuma transferência de toohello dúvida técnica, mas também não interesse em Resolvendo Olá transferência. Que caso haja, por exemplo, quando uma mensagem é entregue tooa cliente de barramento de serviço e cliente Olá escolhe muito "abandonar" mensagem de saudação porque ele não é possível executar o trabalho de saudação resultante do processamento de mensagem de saudação; entrega de mensagens de saudação em si não está com defeito. Uma variação do estado é hello *modificado* estado, o que permite que a mensagem de toohello alterações como ele será liberado. Esse estado não é usado pelo Barramento de Serviço no momento.

Olá especificação AMQP 1.0 define uma disposição adicional estado chamado *recebido*, que ajuda especificamente toohandle recuperação de link. Link de recuperação permite a reorganização de estado de saudação de um link e pendentes entregas na parte superior de uma nova conexão e a sessão, quando a conexão anterior hello e sessão foram perdidas.

Barramento de serviço não oferece suporte à recuperação de link; Se cliente Olá Olá conexão tooService barramento com uma mensagem em vez de perder transferir pendente, essa transferência de mensagem é perdida e cliente Olá deve se reconectar, restabelecer o link de saudação e tente novamente transferência hello.

Como tal, barramento de serviço e Hubs de eventos oferecem suporte a "pelo menos uma vez" transferências onde remetente Olá pode ser garantido para mensagem de saudação ter foram armazenados e aceita, mas não oferecem suporte a "exatamente uma vez" transferências em Olá nível AMQP, onde o sistema Olá tentaria toorecover Olá link e continuar a eliminação de duplicação do toonegotiate Olá entrega estado tooavoid da transferência de mensagem de saudação.

envia toocompensate para duplicata, barramento de serviço oferece suporte a detecção de duplicidades como um recurso opcional em filas e tópicos. Registros de detecção de duplicidades Olá IDs de mensagem de todas as mensagens de entrada durante uma janela de tempo definido pelo usuário e, em seguida, silenciosamente descarta com que todas as mensagens enviadas hello IDs de mensagem mesmo durante a mesma janela.

### Controle de fluxo

Além de controle de fluxo de nível de sessão toohello modelo abordado anteriormente, cada link tem seu próprio modelo de controle de fluxo. Controle de fluxo de nível de sessão impede que o contêiner de saudação tendo toohandle muitos quadros em uma vez, o controle de fluxo de nível de link coloca o aplicativo hello responsável por quantas mensagens ele deseja toohandle de um link e quando.

![][4]

Em um link, transferências só podem acontecer quando hello remetente tem suficiente *link crédito*. Crédito de link é um contador definido pelo destinatário hello usando Olá *fluxo* performative, que está no escopo do link de tooa. Quando o remetente Olá recebe o crédito de link, ele tenta toouse backup que crédito pela entrega de mensagens. Cada diminui de entrega de mensagem hello crédito restante do link de 1. Quando o crédito de link Olá estiver cheio, parar de entregas.

Quando o barramento de serviço está na função de destinatário do hello, ele instantaneamente fornece remetente Olá crédito suficiente link, para que as mensagens podem ser enviadas imediatamente. Como link crédito é usado, o barramento de serviço envia um *fluxo* saldo de crédito toohello performative remetente tooupdate Olá link.

Na função de remetente hello, barramento de serviço envia mensagens toouse o crédito qualquer link pendentes.

Uma chamada de "recebimento" no nível de API de saudação se traduz em uma *fluxo* performative sendo enviados tooService consome barramento pelo cliente hello e barramento de serviço que crédito por colocar Olá primeiro disponíveis, desbloqueada mensagem da fila hello, bloqueá-lo, e transferi-lo. Se não houver nenhuma mensagem prontamente disponíveis para entrega, qualquer crédito pendente por qualquer link estabelecida com determinada entidade permanece registrada na ordem de chegada, e mensagens estão bloqueadas e transferidos conforme elas se tornam disponíveis, toouse qualquer crédito pendente.

bloqueio de saudação em uma mensagem é liberado quando a transferência Olá é estabelecida em um dos Estados de terminal Olá *aceita*, *rejeitadas*, ou *liberado*. mensagem de saudação é removida do barramento de serviço quando o estado terminal Olá é *aceita*. Ela permanece no barramento de serviço e é entregue toohello próximo receptor quando a transferência de saudação atinge qualquer Olá outros estados. Barramento de serviço move automaticamente mensagem de saudação na fila de mensagens mortas da entidade hello quando chega a contagem máxima de entregas de saudação permitida para a entidade Olá devido toorepeated rejeições ou de versões.

Embora Olá APIs do barramento de serviço não expor diretamente tal opção hoje, um cliente de protocolo do AMQP de nível inferior pode usar Olá link crédito modelo tooturn Olá "estilo pull" interação de emissão de uma unidade de crédito para cada solicitação de recebimento em um modelo de "estilo push" emitindo um grande número de link créditos e receber mensagens assim que estiverem disponíveis sem qualquer interação adicional. Push tem suporte por meio de saudação [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) ou [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) as configurações de propriedade. Quando eles forem diferentes de zero, o cliente do AMQP Olá a usa como crédito de link de saudação.

Nesse contexto, é importante toounderstand que Olá relógio de expiração de saudação de bloqueio de saudação na mensagem de saudação dentro da entidade de saudação inicia quando hello mensagem é obtida da entidade hello, não quando a mensagem de saudação é colocada em transmissão hello. Sempre que o cliente Olá indica as mensagens de tooreceive de preparação emitindo o crédito de link, é, portanto, toobe esperado ativamente recebendo mensagens pela rede hello e ser toohandle pronto-los. Caso contrário, o bloqueio de mensagem de saudação pode ter expirado antes de mensagem de saudação do mesmo é entregue. use Olá link-fluxo de controle de crédito diretamente deve refletir Olá preparação imediata toodeal com mensagens disponíveis despachadas toohello receptor.

Em resumo, hello seções a seguir fornecem uma visão geral esquemática fluxo performative Olá durante as interações de API diferentes. Cada seção descreve uma operação lógica diferente. Algumas dessas interações podem ser "lentas", o que significa que elas só podem ser executadas quando for necessário. Criar um remetente da mensagem não pode causar uma interação de rede até que a primeira mensagem de saudação é enviada ou solicitada.

setas de saudação em Olá a tabela a seguir mostram a direção de fluxo performative hello.

#### Criar receptor da mensagem

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={entity name},<br/>target={client link id}<br/>) |Cliente anexa tooentity como destinatário |
| Anexar o fim de link de saudação de respostas de barramento de serviço |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={entity name},<br/>target={client link id}<br/>) |

#### Criar remetente da mensagem

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |Nenhuma ação |
| Nenhuma ação |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={client link id},<br/>target={entity name}<br/>) |

#### Criar remetente da mensagem (erro)

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |Nenhuma ação |
| Nenhuma ação |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={numeric handle},<br/>closed=**true**,<br/>error={error info}<br/>) |

#### Fechar receptor/remetente da mensagem

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |Nenhuma ação |
| Nenhuma ação |<-- detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |

#### Enviar (êxito)

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Nenhuma ação |
| Nenhuma ação |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### Enviar (erro)

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Nenhuma ação |
| Nenhuma ação |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={error info}<br/>)<br/>) |

#### Receber

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |Nenhuma ação |
| Nenhuma ação |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Nenhuma ação |

#### Receber várias mensagens

| Cliente | BARRAMENTO DE SERVIÇO |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |Nenhuma ação |
| Nenhuma ação |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Nenhuma ação |< transfer(<br/>delivery-id={numeric handle+1},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Nenhuma ação |< transfer(<br/>delivery-id={numeric handle+2},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Nenhuma ação |

### Mensagens

Olá seções a seguir explicam quais propriedades de seções de mensagem do AMQP padrão hello são usadas pelo barramento de serviço e como eles serão mapeados toohello conjunto de API do barramento de serviço.

#### cabeçalho

| Nome do campo | Uso | Nome da API |
| --- | --- | --- |
| durável |- |- |
| prioridade |- |- |
| ttl |Tempo toolive para esta mensagem |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| primeiro comprador |- |- |
| Contagem de entrega |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### propriedades

| Nome do campo | Uso | Nome da API |
| --- | --- | --- |
| message-id |Identificador de forma livre definido pelo aplicativo para esta mensagem. Usado para detecção de duplicidade. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |Identificador de usuário definido pelo aplicativo, não interpretado pelo Barramento de Serviço. |Não é acessível por meio de saudação API do barramento de serviço. |
| muito|Identificador de destino definido pelo aplicativo, não é interpretado pelo Barramento de Serviço. |[Para](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| subject |Identificador de finalidade de mensagem definido pelo aplicativo, não é interpretado pelo Barramento de Serviço. |[Rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| resposta muito|Identificador reply-path definido pelo aplicativo, não é interpretado pelo Barramento de Serviço. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |Identificador de correlação definido pelo aplicativo, não é interpretado pelo Barramento de Serviço. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| content-type |Indicador de tipo de conteúdo definido pelo aplicativo para corpo hello, não interpretado pelo barramento de serviço. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |Definido pelo aplicativo codificação de conteúdo de indicador de corpo hello, não interpretado pelo barramento de serviço. |Não é acessível por meio de saudação API do barramento de serviço. |
| absolute-expiry-time |Declara na qual Olá instantânea absoluto mensagem expira. Ignorado na entrada (a vida útil do cabeçalho é observada), autoritativo na saída. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |Declara no qual Olá tempo mensagem foi criada. Não é usado pelo Barramento de Serviço |Não é acessível por meio de saudação API do barramento de serviço. |
| group-id |Identificador definido pelo aplicativo para um conjunto relacionado de mensagens. Usado para sessões do Barramento de Serviço. |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |Identifica o número de sequência relativa de saudação de mensagem de saudação dentro de uma sessão de contador. Ignorado pelo Barramento de Serviço. |Não é acessível por meio de saudação API do barramento de serviço. |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Recursos avançados do Barramento de Serviço

Esta seção aborda os recursos avançados do barramento de serviço do Azure que se baseiam no rascunho extensões tooAMQP, sendo desenvolvida em Olá Comitê técnico OASIS para AMQP. Barramento de serviço implementa as versões mais recentes desses rascunhos hello e adota as alterações introduzidas como esses rascunhos alcançar o status padrão.

> [!NOTE]
> As operações avançadas de Mensagens do Barramento de Serviço têm suporte por meio de um padrão de solicitação/resposta. detalhes de saudação dessas operações são descritos no documento de saudação [AMQP 1.0 no barramento de serviço: operações com base em solicitação-resposta](service-bus-amqp-request-response.md).
> 
> 

### Gerenciamento de AMQP

Olá especificação de gerenciamento AMQP é hello primeiro das extensões de rascunho Olá discutidas aqui. Essa especificação define um conjunto de gestos de protocolo em camadas sobre Olá protocolo AMQP permitir interações de gerenciamento com hello infra-estrutura de mensagens em AMQP. especificação de saudação define operações genéricas como *criar*, *ler*, *atualizar*, e *excluir* para gerenciar entidades dentro de um infraestrutura de mensagens e um conjunto de operações de consulta.

Todos esses gestos exigem uma interação de solicitação/resposta entre o cliente hello e infraestrutura de mensagens de saudação e, portanto, a especificação de saudação define como toomodel interação padrão na parte superior do AMQP: Olá cliente conecta-se toohello de mensagens infraestrutura, inicia uma sessão e, em seguida, cria um par de links. Em um link, cliente Olá atua como remetente e em outros Olá atua como um destinatário, criando assim um par de links que podem atuar como um canal bidirecional.

| Operação Lógica | Cliente | Barramento de Serviço |
| --- | --- | --- |
| Criar caminho de resposta de solicitação |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=**null**,<br/>target=”myentity/$management”<br/>) |Nenhuma ação |
| Criar caminho de resposta de solicitação |Nenhuma ação |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=null,<br/>target=”myentity”<br/>) |
| Criar caminho de resposta de solicitação |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=”myentity/$management”,<br/>target=”myclient$id”<br/>) | |
| Criar caminho de resposta de solicitação |Nenhuma ação |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=”myentity”,<br/>target=”myclient$id”<br/>) |

Ter esse par de links em vigor, a implementação de solicitação/resposta Olá é simples: uma solicitação é uma mensagem enviada tooan entidade dentro da infraestrutura de mensagens de saudação que reconheça esse padrão. Na mensagem solicitação, Olá *responder* campo Olá *propriedades* seção está definida toohello *destino* identificador Olá link no qual resposta de saudação toodeliver. Olá tratamento entidade processa a solicitação de saudação e oferece Olá resposta sobre Olá vincule cujo *destino* identificador corresponde Olá indicado *responder* identificador.

padrão de saudação obviamente exige que contêiner de cliente hello e identificador de saudação gerado pelo cliente para o destino de resposta de saudação são exclusivas em todos os clientes e, por motivos de segurança, também é difícil toopredict.

trocas de mensagens de saudação usada para o protocolo de gerenciamento de saudação em todos os outros protocolos que Olá use ocorrer mesmo padrão no nível do aplicativo hello; eles não definem novos gestos de nível de protocolo AMQP. Isso é intencional para que os aplicativos possam aproveitar imediatamente essas extensões com pilhas AMQP 1.0 compatíveis.

Barramento de serviço não implementa qualquer um dos recursos de núcleo Olá da especificação de gerenciamento Olá no momento, mas o padrão de solicitação/resposta Olá definida pela especificação de gerenciamento de saudação é fundamental para o recurso de segurança com base em declarações hello e para quase todos os Olá discutidos nas seções a seguir de saudação de recursos avançados.

### Autorização baseada em declarações

rascunho de especificação de autorização com base em declarações do AMQP (CBS) Olá se baseia no padrão de solicitação/resposta de especificação de gerenciamento hello e descreve um modelo generalizado para como toouse federado tokens de segurança com AMQP.

modelo de segurança de padrão de saudação do AMQP discutido na introdução de saudação baseia SASL e integra-se com o handshake da conexão AMQP hello. Usar SASL tem a vantagem de saudação que ele fornece um modelo extensível para a qual um conjunto de mecanismos foi definido de que qualquer protocolo que apresenta formalmente SASL pode se beneficiar. Entre esses mecanismos estão "Simples" para a transferência de nomes de usuário e senhas, segurança em nível de tooTLS toobind "Externo", "Anônimo" ausência de saudação tooexpress de autenticação/autorização explícita e uma ampla variedade de mecanismos adicionais que permitem passando as credenciais de autenticação ou autorização ou tokens.

A integração do SASL do AMQP tem duas desvantagens:

* Todas as credenciais e tokens são toohello no escopo de conexão. Uma infraestrutura de mensagens seja tooprovide diferenciado de controle de acesso em uma base por entidade; Por exemplo, permitindo portador de saudação de um token toosend tooqueue um, mas não tooqueue B. Com o contexto de autorização Olá ancorado na conexão Olá, é toouse não é possível uma conexão única e ainda usar tokens de acesso diferentes para a fila A e B.
* Os tokens de acesso geralmente só são válidos por um período limitado. Essa validade requer Olá usuário tooperiodically readquirir tokens e fornece uma oportunidade toohello emissor de token toorefuse que emitindo um token de segurança atualizada se permissões de acesso do usuário Olá foram alterados. As conexões AMQP podem durar por longos períodos. Hello modelo SASL fornece apenas uma chance tooset um token em tempo de conexão, o que significa que Olá infraestrutura de mensagens ou tem o cliente de saudação do toodisconnect quando Olá token expirar ou precisa tooaccept Olá risco comunicação contínua com um cliente que tem direitos de acesso podem ter sido revogados em Olá intermediários.

Olá especificação AMQP CBS, implementado pelo barramento de serviço permite que uma solução alternativa elegante de ambos esses problemas: permite que um cliente de tokens de acesso tooassociate com cada nó e tooupdate os tokens antes de expirarem, sem interromper o fluxo de mensagens de saudação.

CBS define um nó de gerenciamento virtual, denominado *$cbs*, toobe fornecida pela infraestrutura de mensagens de saudação. nó de gerenciamento de saudação aceita tokens em nome de qualquer outro nó na infra-estrutura de mensagens de saudação.

gesto de protocolo Hello é uma troca de solicitação/resposta, conforme definido pela especificação de gerenciamento de saudação. Significa Olá cliente estabelece um par de links com hello *$cbs* nó e, em seguida, transmite uma solicitação de link de saída e, em seguida, aguarda a resposta Olá Olá em Olá link de entrada.

mensagem de solicitação de saudação tem Olá propriedades do aplicativo a seguir:

| Chave | Opcional | Tipo de valor | Conteúdo de valor |
| --- | --- | --- | --- |
| operation |Não |string |**put-token** |
| type |Não |string |tipo de saudação do token de saudação sendo inserido. |
| name |Não |string |token de Olá Olá "público" toowhich se aplica. |
| expiração |Sim |timestamp |tempo de expiração de saudação do token de saudação. |

Olá *nome* propriedade identifica a entidade de saudação com quais Olá token deve ser associado. No Service Bus-lo da assinatura/tópico ou fila do hello caminho toohello. Olá *tipo* propriedade identifica o tipo de token hello:

| Tipo de token | Descrição do token | Tipo de corpo | Observações |
| --- | --- | --- | --- |
| amqp:jwt |JWT (Token Web JSON) |Valor de AMQP (cadeia de caracteres) |Ainda não está disponível. |
| amqp:swt |SWT (Token Web Simples) |Valor de AMQP (cadeia de caracteres) |Só tem suporte para tokens SWT emitidos pelo AAD/ACS |
| servicebus.windows.net:sastoken |Token SAS do barramento de serviço |Valor de AMQP (cadeia de caracteres) |- |

Os tokens conferem direitos. O Barramento de Serviço conhece três direitos fundamentais: "Enviar", permite o envio, "Ouvir", permite o recebimento, e "Gerenciar", permite a manipulação de entidades. Os tokens SWT emitidos pelo ACS/AAD incluem explicitamente esses direitos como declarações. Tokens SAS do barramento de serviço Consulte toorules configurada no namespace de saudação ou entidade, e essas regras são configuradas com direitos. Assim, o token de assinatura Olá com chave Olá associado a essa regra torna respectivos direitos do Olá Olá express token. símbolo de saudação associado a uma entidade usando *put token* permite Olá conectado toointeract de cliente com a entidade Olá por direitos token hello. Um link em que o cliente de saudação realiza em hello *remetente* função requer hello "Envio" à direita; fazendo em Olá *receptor* função requer o direito de "Escutar" hello.

Olá, a mensagem de resposta tem Olá seguintes *propriedades do aplicativo* valores

| Chave | Opcional | Tipo de valor | Conteúdo de valor |
| --- | --- | --- | --- |
| status-code |Não |int |Código de resposta HTTP **[RFC2616]**. |
| status-description |Sim |string |Descrição do status de saudação. |

Olá cliente pode chamar *put token* repetidamente e para qualquer entidade na infraestrutura de mensagens de saudação. tokens de saudação são toohello no escopo atual do cliente e ancoradas na conexão atual hello, significado Olá server descarta todos os tokens retidos quando conexão Olá cai.

implementação de barramento de serviço atual Olá permite apenas CBS em conjunto com hello método SASL "Anônimo". Uma conexão SSL/TLS sempre deve existir o handshake SASL toohello anterior.

Olá mecanismo anônimo, portanto, deve ter suporte Olá escolhido o cliente do AMQP 1.0. Significa que o acesso anônimo que Olá handshake de conexão inicial, incluindo a criação da sessão inicial Olá ocorre sem saber quem está criando uma conexão de saudação do barramento de serviço.

Após o estabelecimento de conexão hello e sessão, anexar Olá links toohello *$cbs* nó e enviando Olá *put token* solicitação são Olá somente operações permitidas. Um token válido deve ser definido com êxito usando um *put token* solicitação para um nó de entidade em 20 segundos após o estabelecimento de conexão hello, caso contrário, conexão Olá forma unilateral descartada pelo barramento de serviço.

cliente Olá é subsequentemente responsável por manter o controle de expiração do token. Quando um token expira, o barramento de serviço imediatamente descarta todos os links na respectiva entidade do hello conexão toohello. tooprevent, Olá cliente poderá substituir o token Olá para o nó de saudação com um novo a qualquer momento por meio de saudação virtual *$cbs* Olá do nó de gerenciamento com o mesmo *put token* gestos e sem entrar Olá modo de carga de saudação do tráfego que em links diferentes.

## Próximas etapas

toolearn mais sobre AMQP, visite Olá links a seguir:

* [Visão geral do Barramento de Serviço para AMQP]
* [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]
* [AMQP no Barramento de Serviço para Windows Server]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Visão geral do Barramento de Serviço para AMQP]: service-bus-amqp-overview.md
[Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP no Barramento de Serviço para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
