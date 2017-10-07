---
title: "aplicativos do Azure Service Bus aaaInsulating contra interrupções e desastres | Microsoft Docs"
description: "Descreve técnicas que você pode usar tooprotect aplicativos contra uma interrupção potencial do barramento de serviço."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Práticas recomendadas para isolar aplicativos contra interrupções e desastres do Barramento de Serviço
Aplicativos de missão crítica devem operar continuamente, mesmo na presença de saudação de falhas inesperadas ou desastres. Este tópico descreve técnicas que você pode usar os aplicativos do barramento de serviço tooprotect contra uma potencial interrupção do serviço ou um desastre.

Uma interrupção é definida como indisponibilidade temporária de saudação do barramento de serviço do Azure. Falha de saudação pode afetar alguns componentes do barramento de serviço, como um repositório de mensagens ou o datacenter inteiro Olá mesmo. Depois de corrigir o problema de saudação, barramento de serviço ficar disponível novamente. Normalmente, uma interrupção não causa a perda de mensagens ou de outros dados. Um exemplo de uma falha do componente é indisponibilidade de saudação de um repositório de mensagens específico. Um exemplo de uma interrupção de todo o datacenter é uma falha de energia de datacenter hello, ou um comutador de rede do datacenter com falha. Uma falha pode durar de alguns tooa de minutos a alguns dias.

Um desastre é definido como perda permanente de saudação de uma unidade de escala de barramento de serviço ou datacenter. Olá datacenter pode ou não pode ficar disponível novamente. Normalmente, um desastre causa perda de algumas ou de todas as mensagens ou de outros dados. Exemplos de desastres são incêndios, enchentes ou terremoto.

## <a name="current-architecture"></a>Arquitetura atual
Barramento de serviço usa vários repositórios toostore mensagens enviadas tooqueues ou tópicos. Uma fila não particionado ou tópico é atribuído tooone repositório de mensagens. Se esse repositório de mensagens não estiver disponível, todas as operações na fila ou no tópico falharão.

Todas as entidades de mensagens do Barramento de Serviço (filas, tópicos, retransmissões) residem em um namespace de serviço, que está associado a um datacenter. Barramento de serviço não habilitar a replicação geográfica automática de dados, ele também não permite um namespace toospan vários datacenters.

## <a name="protecting-against-acs-outages"></a>Proteção contra interrupções do ACS
Se você estiver usando as credenciais do ACS e ele ficar indisponível, os clientes não poderão mais obter tokens. Os clientes que possuem um token no tempo de saudação que ACS cair podem continuar toouse barramento de serviço até a data de expiração de tokens de saudação. vida útil do token padrão Olá é de 3 horas.

tooprotect contra falhas do ACS, use tokens de assinatura de acesso compartilhado (SAS). Nesse caso, Olá autentica diretamente com o barramento do serviço Assinando um token sem uso com uma chave secreta. TooACS chamadas não são mais necessários. Para saber mais sobre tokens SAS, confira [Autenticação do Barramento de Serviço][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Protegendo filas e tópicos contra falhas do repositório de mensagens
Uma fila não particionado ou tópico é atribuído tooone repositório de mensagens. Se esse repositório de mensagens não estiver disponível, todas as operações na fila ou no tópico falharão. Um particionada fila, Olá outro lado, consiste em vários fragmentos. Cada fragmento é armazenado em um repositório de mensagens diferente. Quando uma mensagem é enviada tooa fila ou tópico particionado, o barramento de serviço atribui tooone de mensagem de saudação de fragmentos de saudação. Se o repositório de mensagens correspondente Olá estiver indisponível, o barramento de serviço grava fragmento diferente de saudação mensagem tooa, se possível. Para obter mais informações sobre entidades particionadas, veja as [Entidades de Mensagens Particionadas][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Proteção contra interrupções ou desastres de datacenter
tooallow para um failover entre dois datacenters, você pode criar um namespace de serviço do barramento de serviço em cada datacenter. Por exemplo, Olá namespace de serviço do barramento de serviço **Contosoprimario.ServiceBus.Windows.NET** pode estar localizada na região/Centro-Norte dos Estados Unidos hello e **Contososecundario.ServiceBus.Windows.NET**pode estar localizada na região do hello nos Sul/Central. Se uma entidade de mensagens do Service Bus deverá permanecer acessível na presença de saudação de uma interrupção do datacenter, você pode criar essa entidade em ambos os namespaces.

Para obter mais informações, consulte hello "Falha do barramento de serviço em um datacenter do Azure" seção [assíncrona de alta disponibilidade e padrões de mensagens][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Protegendo pontos de extremidade de retransmissão contra interrupções ou desastres
A replicação geográfica de pontos de extremidade de retransmissão permite que um serviço que expõe um toobe de ponto de extremidade de retransmissão acessível na presença de saudação de interrupções de barramento de serviço. tooachieve replicação geográfica, o serviço de saudação deve criar dois pontos de extremidade de retransmissão em namespaces diferentes. Olá namespaces devem residir em datacenters diferentes e dois pontos de extremidade de saudação devem ter nomes diferentes. Por exemplo, um ponto de extremidade primário pode ser acessado em **contosoPrimary.servicebus.windows.net/myPrimaryService**, enquanto seu equivalente secundário pode ser acessado em **contosoSecondary.servicebus.windows.net/mySecondaryService**.

Olá serviço escuta ambos os pontos de extremidade e um cliente pode invocar o serviço Olá por meio de um ponto de extremidade. Um aplicativo cliente aleatoriamente escolhe uma saudação retransmissões como Olá ponto de extremidade primário e envia seu ponto de extremidade solicitação toohello ativo. Se a operação de saudação falhará com um código de erro, essa falha indica que esse ponto de extremidade de retransmissão Olá não está disponível. aplicativo Hello abre um ponto de extremidade canal toohello backup e emite novamente a solicitação de saudação. Nesse momento, hello ativo e pontos de extremidade de backup Olá alternam funções: aplicativo de cliente hello considera Olá antigo ponto de extremidade ativo toobe Olá novo ponto de extremidade de backup e toobe de ponto de extremidade de backup antigos Olá Olá novo ponto de extremidade ativo. Se ambos envio falharem, funções de saudação de duas entidades de saudação permanecem inalteradas e um erro será retornado.

Olá [replicação geográfica com o barramento de serviço retransmitidas mensagens] [ Geo-replication with Service Bus relayed Messages] demonstra como tooreplicate retransmissões.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Protegendo filas e tópicos contra interrupções ou desastres do datacenter
tooachieve resiliência contra falhas do datacenter ao usar mensagens orientadas, barramento de serviço oferece suporte a duas abordagens: *active* e *passivo* replicação. Para cada abordagem, se uma determinada fila ou tópico precisar permanecer acessível na presença de saudação de uma interrupção do datacenter, você pode criá-lo nos dois namespaces. Ambas as entidades podem ter Olá mesmo nome. Por exemplo, uma fila primária pode ser acessada em **contosoPrimary.servicebus.windows.net/myQueue**, enquanto sua equivalente secundária pode ser acessada em **contosoSecondary.servicebus.windows.net/myQueue**.

Se o aplicativo hello não requer comunicação permanente do remetente e o receptor, o aplicativo hello pode implementar uma fila durável do lado do cliente tooprevent perda e tooshield Olá remetente da mensagem de quaisquer erros transitórios de barramento de serviço.

## <a name="active-replication"></a>Replicação ativa
A replicação ativa usa entidades em ambos os namespaces para todas as operações. Qualquer cliente que envia uma mensagem envia duas cópias da saudação mesma mensagem. Olá primeira cópia é enviada a entidade principal toohello (por exemplo, **contosoPrimary.servicebus.windows.net/sales**), e a segunda cópia saudação da mensagem de saudação é enviada a entidade secundária toohello (por exemplo,  **contosoSecondary.servicebus.windows.net/sales**).

Um cliente recebe mensagens de ambas as filas. processos de destinatário Olá Olá primeira cópia de uma mensagem e Olá segunda cópia é suprimida. toosuppress de mensagens duplicadas, o remetente Olá deve marcar cada mensagem com um identificador exclusivo. Ambas as cópias da mensagem de saudação devem ser marcadas com hello mesmo identificador. Você pode usar o hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] ou [BrokeredMessage.Label] [ BrokeredMessage.Label] propriedades ou saudação de tootag uma propriedade personalizada Mensagem. receptor de saudação deve manter uma lista de mensagens que ele recebeu.

Olá [replicação geográfica com mensagens orientadas do barramento do serviço] [ Geo-replication with Service Bus Brokered Messages] demonstra a replicação ativa de entidades de mensagens.

> [!NOTE]
> abordagem de replicação ativa Olá dobra o número de saudação de operações, portanto essa abordagem pode gerar toohigher custo.
> 
> 

## <a name="passive-replication"></a>Replicação passiva
No caso sem falhas hello, a replicação passiva usa apenas uma das duas entidades de mensagens de saudação. Um cliente envia a entidade ativa de toohello de mensagem de saudação. Se a operação de saudação entidade ativa Olá falhará com um código de erro que indica o datacenter Olá que a entidade ativa de saudação de hosts pode estar indisponível, cliente Olá envia uma cópia da entidade de backup do toohello de mensagem de saudação. Nesse momento, hello ativa e entidades de backup Olá alternam funções: cliente remetente Olá considera Olá antiga entidade ativa toobe Olá nova entidade de backup e Olá antigo backup entidade é Olá novo ativo. Se ambos envio falharem, funções de saudação de duas entidades de saudação permanecem inalteradas e um erro será retornado.

Um cliente recebe mensagens de ambas as filas. Porque há uma possibilidade de que Olá recebe duas cópias da saudação a mesma mensagem, hello receptor deve suprimir mensagens duplicadas. Você pode suprimir duplicatas no hello mesma forma descrita para a replicação ativa.

Em geral, a replicação passiva é mais econômica do que a replicação ativa porque, na maioria dos casos, somente uma operação é executada. Latência, a taxa de transferência e os custos monetários são idênticos toohello não replicado cenário.

Ao usar replicação passiva, em hello mensagens de cenários a seguir podem ser perdidas ou recebidas duas vezes:

* **Perda ou atraso de mensagens**: pressupõem que o remetente Olá enviadas com êxito uma fila do mensagem m1 toohello primário e fila Olá torna-se indisponível antes Olá recebe m1. remetente Olá envia fila secundária do m2 toohello uma mensagem subsequente. Se a fila primária hello está temporariamente indisponível, o receptor Olá recebe m1 depois Olá fila ficar disponível novamente. Em caso de desastre, o receptor de saudação pode nunca receber m1.
* **Recebimento duplicado**: suponha que esse remetente Olá envia uma fila principal de toohello mensagem m. Barramento de serviço com êxito processa m, mas falhar toosend uma resposta. Depois Olá enviar operação expirar, o remetente de Olá envia uma cópia idêntica de fila secundária do toohello m. Se receptor Olá for capaz de tooreceive Olá primeira cópia de m antes de fila primária Olá fica indisponível, Olá recebe ambas as cópias de m em aproximadamente Olá simultaneamente. Se receptor Olá não é capaz de tooreceive Olá primeira cópia de m antes de fila primária Olá fica indisponível, receptor Olá inicialmente recebe apenas Olá segunda cópia de m, mas, em seguida, recebe uma segunda cópia de m quando a fila primária Olá fica disponível.

Olá [replicação geográfica com o barramento de serviço orientado a mensagens] [ Geo-replication with Service Bus Brokered Messages] demonstra a replicação passiva de entidades de mensagens.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a recuperação de desastres, consulte estes artigos:

* [Continuidade dos negócios no Banco de dados SQL do Azure][Azure SQL Database Business Continuity]
* [Projetando aplicativos resilientes para Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
