---
title: "aaaOverview de conceitos básicos do barramento de serviço do Azure | Microsoft Docs"
description: "Uma introdução toousing barramento de serviço tooconnect software de tooother de aplicativos do Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Barramento de Serviço do Azure

Se um aplicativo ou serviço é executado na nuvem hello ou no local, é preciso geralmente toointeract com outros aplicativos ou serviços. tooprovide toodo uma maneira útil em larga escala, oferecidos pelo Microsoft Azure Service Bus. Este artigo aborda essa tecnologia, que descreve o que é e por que você pode toouse-lo.

## <a name="service-bus-fundamentals"></a>Conceitos fundamentais do barramento de serviço

Situações diferentes pedem estilos diferentes de comunicação. Às vezes, permitindo que aplicativos enviem e recebam mensagens por meio de uma fila simple é a melhor solução de saudação. Em outras situações, uma fila comum não é suficiente; uma fila com um mecanismo de publicação e assinatura é melhor. Em alguns casos, tudo que realmente é preciso é uma conexão entre aplicativos; as filas não são necessárias. Barramento de serviço fornece todas as três opções, permitindo que toointeract seus aplicativos de várias maneiras diferentes.

Barramento de serviço é um serviço de nuvem multilocatário, o que significa que o serviço de saudação é compartilhado por vários usuários. Cada usuário, como um desenvolvedor de aplicativos, cria um *namespace*, define os mecanismos de comunicação Olá necessários dentro desse namespace. A Figura 1 mostra a aparência dessa arquitetura.

![][1]

**Figura 1: O barramento de serviço fornece um serviço de multilocatário para conexão de aplicativos por meio da nuvem de saudação.**

Dentro de um namespace, você pode usar uma ou mais instâncias de três mecanismos de comunicação diferentes, cada um deles conecta aplicativos de uma maneira diferente. Olá opções são:

* *Filas de*, que permitem a comunicação de um-direcional. Cada fila atua como um intermediário (às vezes chamado de um *agente*) que armazena mensagens enviadas até que eles são recebidos. Cada mensagem é recebida por um único destinatário.
* *Tópicos*, que fornecem uma comunicação unidirecional usando *assinaturas* - um único tópico pode ter várias assinaturas. Como uma fila, um tópico atua como um agente, mas cada assinatura, opcionalmente, pode usar um filtro tooreceive apenas as mensagens que correspondem a critérios específicos.
* *Retransmissões*, que fornece comunicação bidirecional. Ao contrário das filas e dos tópicos, uma retransmissão não armazena as mensagens em trânsito. Ela não é um agente. Em vez disso, ela apenas transmite-los no aplicativo de destino toohello.

Ao criar uma fila, um tópico ou uma retransmissão, você atribui um nome a ele/ela. Esse nome combinado com qualquer você chamou o seu namespace, cria um identificador exclusivo para o objeto de saudação. Aplicativos podem fornecer esse nome tooService barramento e depois usar essa fila, tópico ou retransmissão toocommunicate uns com os outros. 

toouse qualquer um desses objetos no cenário de retransmissão hello, aplicativos do Windows podem usar Windows Communication Foundation (WCF). Esse serviço é conhecido como [Retransmissão WCF](../service-bus-relay/relay-what-is-it.md). Para as filas e os tópicos, os aplicativos do Windows podem usar as APIs de mensagens definidas pelo Barramento de Serviço. toomake esses objetos toouse mais fácil de aplicativos não-Windows, a Microsoft fornece SDKs para Java, Node.js e outras linguagens. Você também pode acessar as filas e os tópicos usando as [APIs REST](/rest/api/servicebus/) no(s) HTTP(s). 

É importante toounderstand que mesmo que os serviço de barramento em si é executado na nuvem de hello (ou seja, em datacenters do Azure da Microsoft), os aplicativos que o utilizam podem ser executados em qualquer lugar. Você pode usar aplicativos de tooconnect de barramento de serviço em execução no Azure, por exemplo, ou aplicativos em execução dentro de seu próprio data center. Você também pode usar isso tooconnect um aplicativo em execução no Azure ou em outra plataforma de nuvem com um aplicativo local ou tablets e telefones. É aparelhos domésticos tooconnect possível, sensores e outros aplicativos de central de tooa de dispositivos ou tooone outros. Barramento de serviço é um mecanismo de comunicação na nuvem de saudação que é acessível de praticamente qualquer lugar. Como você usa depende do que seus aplicativos precisam toodo.

## <a name="queues"></a>Filas

Suponha que você decidir tooconnect dois aplicativos usando uma fila do barramento de serviço. A Figura 2 ilustra essa opção.

![][2]

**Figura 2: Filas do Barramento de Serviço fornecem o enfileiramento de mensagens assíncronas unidirecional.**

Olá processo é simples: um remetente envia uma fila de barramento de serviço tooa mensagens e um destinatário pega a mensagem em algum momento mais tarde. Uma fila pode ter apenas um único destinatário, como a Figura 2 mostra. Ou então, vários aplicativos podem ler de saudação mesma fila. Situação de último hello, cada mensagem é lida por apenas um destinatário. Para um serviço de vários casts, você deve usar um tópico.

Cada mensagem tem duas partes: um conjunto de propriedades, cada um par chave/valor e uma carga de mensagem. carga Olá pode ser o mesmo XML, texto ou binário. Como eles são usados depende de um aplicativo que está tentando toodo. Por exemplo, um aplicativo enviar uma mensagem sobre uma venda recente pode incluir propriedades Olá **vendedor = "&"** e **quantidade = 10000**. corpo da mensagem de saudação pode conter uma imagem digitalizada do contrato assinado da venda hello ou, se não houver uma, permanecer em branco.

Um receptor pode ler uma mensagem de uma fila do Service Bus de duas maneiras diferentes. Olá a primeira opção, chamada  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, remove uma mensagem da fila de saudação e exclui-lo imediatamente. Essa opção é simple, mas se o receptor Olá falhar antes de terminar de processar a mensagem de saudação, mensagem de saudação será perdida. Porque eles foram removidos da fila de saudação, nenhum outro receptor pode acessá-lo. 

Olá a segunda opção,  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, destina-se toohelp com esse problema. Como **ReceiveAndDelete**, um **PeekLock** leitura remove uma mensagem da fila de saudação. No entanto ela não exclui a mensagem de saudação. Em vez disso, ele bloqueia a mensagem de saudação, tornando invisível tooother receptores, em seguida, aguarda até que um dos três eventos:

* Se os processos de destinatário Olá Olá mensagem com êxito, ele chama [Complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), e a fila de saudação exclui a mensagem de saudação. 
* Se o destinatário Olá decide que não pode processar a mensagem de saudação com êxito, ele chama [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). fila Olá remove bloqueio de saudação da mensagem de saudação e torna disponível tooother receptores.
* Se o receptor Olá chamadas nenhum desses métodos dentro de um período configurável (por padrão, 60 segundos), fila Olá pressupõe receptor Olá falhou. Nesse caso, ele se comporta como se tivesse chamado receptor Olá **abandonar**, tornando Olá receptores tooother disponíveis.

Observe que pode acontecer aqui: hello mesma mensagem pode ser entregue duas vezes, talvez tootwo destinatários diferentes. Os aplicativos que usam filas do Barramento de Serviço devem estar preparados para isso. toomake detecção de duplicidades mais fácil, cada mensagem tem uma única [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriedade que, por padrão, fica Olá mesmo, independentemente de quantas vezes a mensagem de saudação é lido de uma fila. 

Filas são úteis em algumas situações. Elas permitem que aplicativos toocommunicate mesmo quando ambos não são executados em Olá a mesma hora, algo que é especialmente útil com aplicativos móveis e de lote. Uma fila com vários receptores também fornece balanceamento de carga automático, desde que as mensagens enviadas sejam distribuídas entre esses receptores.

## <a name="topics"></a>Tópicos

Útil como estão, filas não são sempre solução certa hello. Às vezes, os tópicos do Barramento de Serviço são melhores. Figura 3 ilustra a ideia.

![][3]

**Figura 3: Com base no filtro de saudação que especifica um aplicativo de assinatura, ela pode receber algumas ou todas as mensagens de saudação enviadas tooa tópico de barramento de serviço.**

Um *tópico* é semelhante na fila de tooa muitas maneiras. Remetentes enviar tópico tooa mensagens Olá mesma forma que eles enviam a fila de mensagens de tooa e procure essas mensagens Olá mesmo assim como acontece com filas. Olá diferença é que tópicos permitem cada toocreate aplicativo receptor seu próprio *assinatura* definindo um *filtro*. Um assinante, em seguida, vê somente as mensagens de saudação que correspondem a esse filtro. Por exemplo, a Figura 3 mostra um remetente e um tópico com três assinantes, cada um com seu próprio filtro:

* Assinante 1 recebe somente mensagens que contêm a propriedade Olá *vendedor = "&"*.
* Assinante 2 recebe mensagens que contêm a propriedade Olá *vendedor = "Ruby"* e/ou conter um *quantidade* propriedade cujo valor é maior que 100.000. Talvez Ruby é gerente de vendas hello, portanto ela deseja toosee próprias vendas e todas as vendas grandes, independentemente de quem faz com que sejam.
* Assinante 3 definiu seu filtro muito*True*, o que significa que ele recebe todas as mensagens. Por exemplo, este aplicativo pode ser responsável por manter uma trilha de auditoria e, portanto, é necessário toosee todas as mensagens de saudação.

Como com filas, o tópico de tooa assinantes pode ler mensagens usando [ReceiveAndDelete ou PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). Ao contrário das filas, no entanto, uma única mensagem enviada tooa tópico pode ser recebido por várias assinaturas. Essa abordagem, normalmente chamada *publicar e assinar* (ou *pub/sub*), é útil sempre que vários aplicativos estão interessados em Olá mensagens mesmo. Definindo o filtro de saudação à direita, cada assinante pode tocar em apenas parte de saudação do fluxo de mensagem de saudação que precisa de toosee.

## <a name="relays"></a>Retransmissão

As filas e os tópicos fornecem uma comunicação unidirecional assíncrona por meio de um agente. O tráfego flui em apenas uma direção, e não há nenhuma conexão direta entre remetentes e receptores. Mas e se você não quiser essa conexão? Suponha que os aplicativos precisam tooboth enviar e receber mensagens, ou talvez você deseja um vínculo direto entre eles e mensagens toostore broker não é necessário. cenários de tooaddress como este, barramento de serviço fornece *retransmite*, como mostra a Figura 4.

![][4]

**Figura 4: a retransmissão do Barramento de Serviço fornece comunicação bidirecional síncrona entre os aplicativos.**

Hello tooask pergunta óbvia sobre retransmissões é: por que usar um? Mesmo se não preciso de filas, por que aplicativos se comunicam por meio de um serviço de nuvem em vez de apenas interagir diretamente? resposta de saudação é que se comunicando diretamente pode ser mais difícil que você imagina.

Suponha que você queira tooconnect dois aplicativos locais, tanto em execução nos data centers corporativos. Cada um desses aplicativos fica atrás de um firewall, e cada centro de dados provavelmente usará a conversão de endereços de rede (NAT). blocos de firewall Olá os dados de entrada em todas, exceto alguns portas e NAT implica em cada aplicativo está em execução no computador Olá não tem um endereço IP fixo que você pode acessar diretamente do datacenter de saudação fora. Sem alguma ajuda extra, conectando esses aplicativos pela Olá internet pública é problemático.

Uma retransmissão do Barramento de Serviço pode ajudar. toocommunicate bidirecional por meio de uma retransmissão, cada aplicativo estabelece uma conexão de TCP de saída com o barramento de serviço, em seguida, ele mantém aberto. Toda a comunicação entre dois aplicativos de saudação percorram essas conexões. Porque cada conexão foi estabelecida de dentro do datacenter hello, firewall Olá permite entrada tráfego tooeach aplicativo sem abrir novas portas. Essa abordagem também obtém problema do NAT hello, porque cada aplicativo tem um ponto de extremidade consistente na nuvem de saudação em toda a comunicação de saudação. Trocando dados por meio de retransmissão hello, aplicativos Olá podem evitar problemas de saudação que seriam caso contrário dificultam a comunicação. 

retransmissões de barramento de serviço toouse, os aplicativos dependem de saudação Windows Communication Foundation (WCF). Barramento de serviço fornece associações do WCF que tornam mais fácil para toointeract de aplicativos do Windows via retransmissões. Aplicativos que já usam o WCF normalmente podem especificar um essas associações e fale tooeach outros por meio de uma retransmissão. Ao contrário das filas e dos tópicos, no entanto, usar as retransmissões de aplicativos não Windows, ao mesmo tempo possível, requer o algum esforço de programação; Não há bibliotecas padrão são fornecidas.

Ao contrário das filas e dos tópicos, aplicativos não criam explicitamente retransmissões. Em vez disso, quando um aplicativo que deseja tooreceive mensagens estabelece uma conexão TCP com o barramento de serviço, uma retransmissão é criada automaticamente. Quando a conexão Olá é descartado, retransmissão Olá é excluído. tooenable uma retransmissão de saudação do aplicativo toofind criada por um ouvinte específico, barramento de serviço fornece um registro que permite que aplicativos toolocate uma retransmissão específica por nome.

As retransmissões são solução certa hello quando precisar de comunicação direta entre aplicativos. Por exemplo, considere um sistema de reservas de viagens em execução em um data center local que deve ser acessado de outros computadores, dispositivos móveis e quiosques de check-in. Aplicativos em execução em todos esses sistemas podiam confiar na retransmissões de barramento de serviço no hello toocommunicate de nuvem, independentemente de onde eles podem estar em execução.

## <a name="summary"></a>Resumo

Conectando aplicativos sempre foi parte da criação de soluções completas e intervalo de saudação de cenários que exigem a aplicativos e serviços toocommunicate com o outro é definido tooincrease como mais aplicativos e dispositivos são toohello conectado à internet. Fornecendo tecnologias baseadas em nuvem para a obtenção de comunicação por meio de filas, tópicos e retransmissões, barramento de serviço visa toomake este tooimplement de função essencial mais fácil e mais amplamente disponíveis.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu os fundamentos de saudação do barramento de serviço do Azure, siga essas toolearn links mais.

* Como toouse [filas do barramento de serviço](service-bus-dotnet-get-started-with-queues.md)
* Como toouse [tópicos do barramento de serviço](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Como toouse [retransmissão de barramento de serviço](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Exemplos do Barramento de Serviço](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
