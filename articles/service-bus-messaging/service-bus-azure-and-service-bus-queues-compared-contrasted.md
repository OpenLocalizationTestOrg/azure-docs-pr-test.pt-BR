---
title: "filas de armazenamento aaaAzure e filas do barramento de serviço – semelhanças e diferenças | Microsoft Docs"
description: "Analisa diferenças e semelhanças entre dois tipos de fila oferecidos pelo Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Filas do Armazenamento e filas do Barramento de Serviço — comparações e contrastes
Este artigo analisa as diferenças de saudação e as semelhanças entre Olá dois tipos de filas oferecidos pelo Microsoft Azure atualmente: filas de armazenamento e filas do barramento de serviço. Usando essas informações, comparar e contrastar respectivas tecnologias de saudação e ser capaz de toomake uma decisão mais informada sobre a solução que melhor atenda às suas necessidades.

## <a name="introduction"></a>Introdução
O Azure dá suporte a dois tipos de mecanismo de fila: **filas do Armazenamento** e **filas do Barramento de Serviço**.

**Filas de armazenamento**, que fazem parte da saudação [armazenamento do Azure](https://azure.microsoft.com/services/storage/) infraestrutura, o recurso de uma interface baseada em REST GET/PUT/PEEK simples, oferecendo mensagens confiáveis e persistentes dentro e entre serviços.

**As filas do Barramento de Serviço** fazem parte de uma infraestrutura mais ampla do [sistema de mensagens do Azure](https://azure.microsoft.com/services/service-bus/), que dá suporte ao enfileiramento, bem como a publicação/assinatura e outros padrões de integração avançados. Para obter mais informações sobre o barramento de serviço filas, tópicos/assinaturas, consulte Olá [visão geral do barramento de serviço](service-bus-messaging-overview.md).

Embora ambas as tecnologias de enfileiramento coexistam, as filas do Armazenamento foram introduzidas primeiro, como um mecanismo de armazenamento de filas dedicado criado com base nos serviços de armazenamento do Azure Storage. Filas do barramento de serviço criadas sobre hello mais ampla de "mensagens" infra-estrutura projetada toointegrate aplicativos ou componentes de aplicativos que podem abranger vários protocolos de comunicação, contratos de dados, domínios de confiança e/ou ambientes de rede.

## <a name="technology-selection-considerations"></a>Considerações de seleção da tecnologia
Filas de armazenamento e filas do barramento de serviço são implementações de mensagem de saudação atualmente oferecido no Microsoft Azure do serviço de enfileiramento de mensagens. Cada um tem um conjunto de recursos ligeiramente diferente, o que significa que você pode escolher uma ou Olá outros ou usar ambas, dependendo das necessidades de saudação de sua solução específica ou um problema comercial/técnico que está resolvendo.

Ao determinar qual tecnologia de enfileiramento é adequada Olá propósito de uma determinada solução, os desenvolvedores e arquitetos de solução devem considerar as recomendações de saudação abaixo. Para obter mais detalhes, consulte Olá próxima seção.

Como arquiteto/desenvolvedor de soluções, **você deve considerar o uso das filas do Armazenamento** quando:

* Seu aplicativo precisa armazenar mais de 80 GB de mensagens em uma fila, onde as mensagens de saudação têm um tempo de vida menor do que 7 dias.
* Seu aplicativo deseja tootrack progresso para processar uma mensagem dentro da fila de saudação. Isso é útil se o trabalho de saudação processar uma mensagem falhar. Um trabalho subsequente pode usar toocontinue que informações de onde Olá anterior parou.
* Você precisa de logs do servidor de todas as transações de saudação executadas em suas filas.

Como arquiteto/desenvolvedor de soluções, **você deve considerar o uso das filas do Barramento de Serviço** quando:

* Sua solução deve ser capaz de tooreceive mensagens sem a necessidade de fila de saudação toopoll. Com o barramento de serviço, isso pode ser feito por meio de saudação uso de sondagem longa Olá receber operação usando protocolos baseados em TCP Olá que dá suporte ao barramento de serviço.
* Sua solução requer Olá fila tooprovide um garantida primeiro-na-first-out (PEPS) a entrega ordenada.
* Você desejar uma experiência simétrica no Azure e no Windows Server (nuvem privada). Para obter mais informações, confira [Barramento de Serviço para Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* Sua solução deve ser capaz de toosupport detecção automática de duplicidades.
* Você deseja que suas mensagens de tooprocess de aplicativo como fluxos de longa execução paralelas (mensagens associados a um fluxo usando Olá [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriedade na mensagem de saudação). Nesse modelo, cada nó no hello aplicativo de consumo compete por fluxos, como toomessages contrário. Quando um fluxo é dado tooa consumindo nó, o nó de Olá pode examinar o estado Olá Olá fluxo do estado do aplicativo usando transações.
* Sua solução exigir comportamento transacional e atomicidade ao enviar ou receber várias mensagens de uma fila.
* característica de (vida útil TTL) Olá tempo de vida de carga de trabalho do hello específicas do aplicativo pode exceder o período de 7 dias hello.
* Seu aplicativo manipula mensagens que podem exceder 64 KB, mas será provavelmente não abordagem Olá limite de 256 KB.
* Lidar com um requisito tooprovide um toohello de modelo de acesso baseado em função de filas e direitos/permissões diferentes para remetentes e destinatários.
* O tamanho da fila não for exceder 80 GB.
* Você deseja toouse Olá protocolo AMQP 1.0 baseado em padrões mensagens. Para obter mais informações sobre AMQP, confira [Visão geral do AMQP do Barramento de Serviço](service-bus-amqp-overview.md).
* Você pode prever uma migração eventual de ponto a ponto com base em fila comunicação tooa exchange padrão de mensagem que permite a integração perfeita de destinatários adicionais (assinantes), cada um dos quais recebe cópias independentes de algumas ou todas as mensagens enviadas toohello fila. Olá último refere-se o recurso de publicação/assinatura de toohello nativamente fornecido pelo barramento de serviço.
* Sua solução de mensagens deve ser capaz de toosupport garantia de entrega de hello "no-máximo uma vez" sem necessidade de saudação para que os componentes de infraestrutura adicional Olá toobuild.
* Deseja toopublish capaz de toobe e consumir lotes de mensagens.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Comparando as filas do Armazenamento e as filas do Barramento de Serviço
tabelas Olá Olá seções a seguir fornecem um agrupamento lógico de recursos de fila e permitem que você compare imediatamente Olá recursos disponíveis em filas de armazenamento e filas do barramento de serviço.

## <a name="foundational-capabilities"></a>Recursos básicos
Esta seção compara alguns dos Olá recursos básicos de enfileiramento de mensagens fornecidos por filas de armazenamento e filas do barramento de serviço.

| Critérios de comparação | Filas de armazenamento | Filas de barramento de serviço |
| --- | --- | --- |
| Garantia de ordenação |**Não** <br/><br>Para obter mais informações, consulte a primeira anotação Olá Olá seção "Informações adicionais".</br> |**Sim - Primeiro a Entrar, Primeiro a Sair (PEPS)**<br/><br>(por meio do uso de saudação de sessões de mensagens) |
| Garantia de entrega |**Pelo menos uma vez** |**Pelo menos uma vez**<br/><br/>**No máximo uma vez** |
| Suporte à operação atômica |**Não** |**Sim**<br/><br/> |
| Comportamento de recebimento |**Sem bloqueio**<br/><br/>(conclusão imediata se nenhuma mensagem nova for encontrada) |**Bloqueio com/sem tempo limite**<br/><br/>(oferece sondagem longa ou Olá ["Técnica Comet"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Sem bloqueio**<br/><br/>(por meio de saudação uso de .NET API somente gerenciado) |
| API de estilo push |**Não** |**Sim**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) e sessões **OnMessage** API .NET. |
| Modo de recebimento |**Inspecionar e Conceder** |**Inspecionar e bloquear**<br/><br/>**Receber e excluir** |
| Modo de acesso exclusivo |**Com base em concessão** |**Com base em bloqueio** |
| Duração da concessão/do bloqueio |**30 segundos (padrão)**<br/><br/>**7 dias (máximo)** (você pode renovar ou liberar uma concessão de mensagem usando Olá [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 segundos (padrão)**<br/><br/>Você pode renovar um bloqueio de mensagem usando Olá [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Precisão da concessão/do bloqueio |**Nível da mensagem**<br/><br/>(cada mensagem pode ter um valor de tempo limite diferente, que, em seguida, você pode atualizar conforme necessário durante o processamento de mensagem de saudação usando Olá [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Nível da fila**<br/><br/>(cada fila tem um tooall de precisão aplicado bloqueio suas mensagens, mas você pode renovar o bloqueio de saudação usando Olá [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Recebimento em lote |**Sim**<br/><br/>(especificando explicitamente a contagem de mensagens ao recuperar mensagens, backup tooa no máximo 32 mensagens) |**Sim**<br/><br/>(implicitamente habilitando uma propriedade de pré-busca ou explicitamente por meio da saudação usar de transações) |
| Envio em lote |**Não** |**Sim**<br/><br/>(por meio do uso de saudação de transações ou lotes no lado do cliente) |

### <a name="additional-information"></a>Informações adicionais
* Geralmente, as mensagens nas filas do Armazenamento são do tipo PEPS, mas, às vezes, elas podem estar fora de ordem; por exemplo, quando a duração do tempo limite da visibilidade de uma mensagem expirar (por exemplo, como resultado de um travamento do aplicativo cliente durante o processamento). Quando o tempo limite de visibilidade de saudação expira, mensagem de saudação se torna visível novamente na fila de saudação para outro toodequeue de trabalho-lo. Nesse ponto, mensagem de saudação visível pode ser colocada na fila de saudação (toobe retirada da fila novamente) após uma mensagem que foi originalmente enfileirado depois dele.
* Olá garantia padrão FIFO em filas do barramento de serviço requer o uso de saudação de sessões de mensagens. Em Olá evento Olá aplicativo falha ao processar uma mensagem recebida no hello **espiada e bloqueio &** modo, Olá próxima vez que um destinatário da fila aceitar uma sessão de mensagens, começa com a mensagem de saudação com falha após seu tempo de vida (TTL) expirar.
* Filas de armazenamento são toosupport projetado cenários de filas padrão, como desacoplamento escalabilidade de tooincrease de componentes de aplicativo e tolerância a falhas, nivelamento de carga e construir fluxos de trabalho de processo.
* As filas do barramento de serviço oferecem suporte a Olá *At-Least-Once* garantia de entrega. Além disso, Olá *única na maioria* semântica pode ser suportados usando o estado do aplicativo hello estado toostore da sessão e usando transações tooatomically receber mensagens e atualizar o estado de sessão hello.
* As filas do Armazenamento fornecem um modelo de programação uniforme e consistente entre filas, tabelas e Blobs, para desenvolvedores e equipes de operações.
* Filas do barramento de serviço oferecem suporte para transações locais no contexto de saudação de uma única fila.
* Olá **receber e excluir** modo com suporte pelo barramento de serviço fornece Olá Olá de tooreduce de capacidade de mensagens a contagem de operação (e o custo associado) em troca de menor garantia de entrega.
* Filas de armazenamento oferecem concessões com concessões de Olá Olá capacidade tooextend para mensagens. Isso permite que os trabalhadores de saudação concessões curtas toomaintain mensagens. Portanto, se um trabalho falhar, mensagem de saudação poderá ser rapidamente processada novamente por outro trabalho. Além disso, um trabalho pode estender a concessão de saudação em uma mensagem se precisar tooprocess-tempo de concessão mais que Olá atual.
* As filas de armazenamento oferecem um tempo limite de visibilidade que você pode definir ao enfileirar hello ou removê-la fila de uma mensagem. Além disso, você pode atualizar uma mensagem com valores de concessão em tempo de execução e atualizar diferente valores entre as mensagens de saudação mesma fila. Tempos limite de bloqueio de barramento de serviço é definido nos metadados de fila Olá; No entanto, você pode renovar o bloqueio hello, Olá chamada [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) método.
* Olá máximo de tempo limite de bloqueio de uma operação de recebimento em filas do barramento de serviço é de 24 dias. No entanto, os tempos limite baseados em REST têm um valor máximo de 55 segundos.
* O envio em lote do lado do cliente fornecido pelo barramento de serviço permite um toobatch de cliente de fila várias mensagens em uma única operação de envio. O envio em lote está disponível apenas para operações de envio assíncronas.
* Recursos como o limite de 200 TB de saudação de filas de armazenamento (mais quando você virtualiza contas) e filas ilimitadas tornam uma plataforma ideal para provedores de SaaS.
* As filas do Armazenamento fornecem um mecanismo de controle de acesso flexível e delegado ao desempenho.

## <a name="advanced-capabilities"></a>Recursos avançados
Esta seção compara recursos avançados fornecidos pelas filas do Armazenamento e do Barramento de Serviço.

| Critérios de comparação | Filas de armazenamento | Filas de barramento de serviço |
| --- | --- | --- |
| Entrega agendada |**Sim** |**Sim** |
| Mensagens mortas automáticas |**Não** |**Sim** |
| Aumentando o valor da vida útil da fila |**Sim**<br/><br/>(por meio da atualização in-loco do tempo limite de visibilidade) |**Sim**<br/><br/>(fornecido por uma função de API dedicada) |
| Suporte a mensagens suspeitas |**Sim** |**Sim** |
| Atualização in-loco |**Sim** |**Sim** |
| Log de transações do servidor |**Sim** |**Não** |
| Métricas de armazenamento |**Sim**<br/><br/>**Métricas de Minuto**: fornecem métricas em tempo real para disponibilidade, TPS, contagens de chamada de API, contagens de erros e muito mais, tudo em tempo real (agregados por minuto e relatados poucos minutos após o que acabou de acontecer em produção). Para obter mais informações, confira [Sobre as Métricas de Analítica de Armazenamento](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Sim**<br/><br/>(consultas em massa chamando [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Gerenciamento de estado |**Não** |**Sim**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Encaminhamento automático de mensagem |**Não** |**Sim** |
| Função Limpar fila |**Sim** |**Não** |
| Grupos de mensagens |**Não** |**Sim**<br/><br/>(por meio do uso de saudação de sessões de mensagens) |
| Estado do aplicativo por grupo de mensagens |**Não** |**Sim** |
| Detecção de duplicidade |**Não** |**Sim**<br/><br/>(configurável no lado do remetente Olá) |
| Procurando grupos de mensagens |**Não** |**Sim** |
| Buscando sessões de mensagem por ID |**Não** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* Ambas as tecnologias de enfileiramento de mensagens permitem um toobe mensagem agendada para entrega posteriormente.
* Encaminhamento automático de fila permite que milhares de filas tooauto encaminhar mensagens tooa única fila, de qual aplicativo de recebimento Olá consome a mensagem de saudação. Você pode usar esse mecanismo tooachieve segurança, fluxo de controle e isolar armazenamento entre cada editor de mensagem.
* As filas do Armazenamento dão suporte à atualização do conteúdo da mensagem. Você pode usar essa funcionalidade para informações de estado persistentes e atualizações incrementais de progresso na mensagem de saudação para que possam ser processadas de saudação último ponto de verificação conhecido, em vez de começar do zero. Com as filas do barramento de serviço, você pode habilitar Olá mesmo cenário por meio do uso de saudação de sessões de mensagens. Sessões permitem que você toosave e recuperar o estado de processamento do aplicativo hello (usando [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) e [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Mensagens Dead](service-bus-dead-letter-queues.md), que só há suporte para as filas do barramento de serviço, pode ser útil para isolar as mensagens que não podem ser processadas com êxito pelo aplicativo de recebimento de saudação ou quando as mensagens não podem chegar ao seu destino devido tooan expirado propriedade time-to-live de (vida útil TTL). Olá valor de TTL especifica quanto tempo uma mensagem permanece na fila de saudação. Com barramento de serviço, a mensagem de saudação será movido tooa fila especial chamada $DeadLetterQueue quando Olá TTL expirar.
* toofind de mensagens "suspeitas" em filas de armazenamento, quando um aplicativo hello de mensagem removê-la fila examina Olá  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  propriedade de mensagem de saudação. Se **DequeueCount** é maior do que um determinado limite, aplicativo hello move Olá mensagem tooan definidas por aplicativos "" fila de mensagens mortas.
* Filas de armazenamento permitem que você tooobtain um log detalhado de todas as transações de saudação executadas na fila hello, bem como agregados métricas. Essas duas opções são úteis para depurar e entender como o aplicativo usa as filas do Armazenamento. Eles também são úteis para seu aplicativo de ajuste de desempenho e reduzir os custos de saudação do uso de filas.
* conceito de saudação de "sessões de mensagens" com suporte pelo barramento de serviço permite que as mensagens que pertencem a tooa determinado toobe grupo lógico associado a um destinatário específico, que por sua vez, cria uma afinidade de sessão entre as mensagens e seus respectivos destinatários. Você pode habilitar essa funcionalidade avançada no barramento de serviço por configuração Olá [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propriedade em uma mensagem. Receptores podem escutar em uma ID de sessão específica e receber mensagens que compartilham Olá especificado identificador de sessão.
* Olá funcionalidade de detecção de duplicidades com suporte pelas filas do barramento de serviço automaticamente remove mensagens duplicadas enviadas tooa fila ou tópico, com base no valor de saudação do hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriedade.

## <a name="capacity-and-quotas"></a>Capacidade e cotas
Esta seção compara as filas de armazenamento e filas do barramento de serviço do ponto de vista de saudação do [capacidade e cotas](service-bus-quotas.md) que podem ser aplicadas.

| Critérios de comparação | Filas de armazenamento | Filas de barramento de serviço |
| --- | --- | --- |
| Tamanho máximo da fila |**500 TB**<br/><br/>(limitado tooa [único capacidade da conta de armazenamento](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(definido na criação de uma fila e [ativar particionamento](service-bus-partitioning.md) – consulte Olá seção "Informações adicionais") |
| Tamanho máximo da mensagem |**64 KB**<br/><br/>(48 KB ao usar a codificação **Base64**)<br/><br/>O Azure suporta mensagens grandes combinando filas e blobs, no ponto em que você pode enfileirar o too200GB para um único item. |**256 KB** ou **1 MB**<br/><br/>(incluindo cabeçalho e corpo, tamanho máximo do cabeçalho: 64 KB).<br/><br/>Depende de saudação [camada de serviço](service-bus-premium-messaging.md). |
| TTL máxima da mensagem |**7 dias** |**`TimeSpan.Max`** |
| Número máximo de filas |**Ilimitado** |**10,000**<br/><br/>(por namespace de serviço, pode ser aumentado) |
| Número máximo de clientes simultâneos |**Ilimitado** |**Ilimitado**<br/><br/>(limite de conexão simultânea 100 se aplica somente a comunicação baseada no protocolo tooTCP) |

### <a name="additional-information"></a>Informações adicionais
* O Barramento de Serviço impõe limites de tamanho de fila. tamanho máximo da fila de saudação é especificado na criação da fila de saudação e pode ter um valor entre 1 e 80 GB. Se o valor de tamanho de fila Olá definido na criação da fila de saudação for atingido, mensagens de entrada adicionais serão rejeitadas e uma exceção será recebida pelo Olá código de chamada. Para obter mais informações sobre cotas no Barramento de Serviço, confira [Cotas do Barramento de Serviço](service-bus-quotas.md).
* Em Olá [camada padrão](service-bus-premium-messaging.md), você pode criar filas do barramento de serviço em tamanhos de 1, 2, 3, 4 ou 5 GB (o padrão de saudação é de 1 GB). Na camada de Premium Olá, você pode criar filas de too80 GB de tamanho. No padrão da camada, com o particionamento habilitado (que é o padrão de saudação), barramento de serviço cria 16 partições para cada GB que você especificar. Dessa forma, se você criar uma fila que é de 5 GB de tamanho, com 16 partições tamanho máximo da fila de saudação torna-se (5 * 16) = 80 GB. Você pode ver o tamanho máximo de saudação de sua fila ou tópico particionado examinando sua entrada no hello [portal do Azure][Azure portal]. Na camada Premium Olá somente 2 partições são criadas por fila.
* Com as filas de armazenamento, se hello conteúdo da mensagem de saudação não for XML seguro, ele deve ser **Base64** codificado. Se você **Base64**-codificar a mensagem de saudação, carga de saudação do usuário pode ser o too48 KB, em vez de 64 KB.
* Com as filas do Barramento de Serviço, cada mensagem armazenada em uma fila é composta por duas partes: um cabeçalho e um corpo. tamanho total de saudação de mensagem de saudação não pode exceder o máximo de mensagem hello tamanho suportado pela camada de serviço de saudação.
* Quando os clientes se comunicam com filas do barramento de serviço por Olá protocolo TCP, o número máximo de saudação de fila de barramento de serviço único tooa conexões simultâneas é limitado too100. Esse número é compartilhado entre remetentes e receptores. Se essa cota for atingida, as solicitações subsequentes de conexões adicionais serão rejeitadas e uma exceção será recebida pelo Olá código de chamada. Esse limite não é imposto em clientes que se conectam toohello filas usando a API baseada em REST.
* Se você precisar de mais de 10.000 filas em um único namespace de barramento de serviço, pode entrar em contato com a equipe de suporte do Azure hello e solicitar um aumento. tooscale além de 10.000 filas com o barramento de serviço, você também pode criar namespaces adicionais usando Olá [portal do Azure][Azure portal].

## <a name="management-and-operations"></a>Gerenciamento e operações
Esta seção compara recursos de gerenciamento de Olá oferecidos por filas de armazenamento e filas do barramento de serviço.

| Critérios de comparação | Filas de armazenamento | Filas do Barramento de Serviço |
| --- | --- | --- |
| Protocolo de gerenciamento |**REST sobre HTTP/HTTPS** |**REST sobre HTTPS** |
| Protocolo de tempo de execução |**REST sobre HTTP/HTTPS** |**REST sobre HTTPS**<br/><br/>**AMQP 1.0 Standard (TCP com TLS)** |
| API do .NET |**Sim**<br/><br/>(API do Cliente de Armazenamento .NET) |**Sim**<br/><br/>(API do Barramento de serviço do .NET) |
| C++ nativo |**Sim** |**Sim** |
| API Java |**Sim** |**Sim** |
| API PHP |**Sim** |**Sim** |
| API Node.js |**Sim** |**Sim** |
| Suporte a metadados arbitrários |**Sim** |**Não** |
| Regras de nomenclatura da fila |**Backup too63 caracteres**<br/><br/>(As letras em um nome de fila devem estar em minúsculas.) |**Backup too260 caracteres**<br/><br/>(Nomes e caminhos de fila não diferenciam maiúsculas de minúsculas.) |
| Função Obter tamanho da fila |**Sim**<br/><br/>(Valor aproximado se as mensagens expirarem além Olá TTL sem que sejam excluídas.) |**Sim**<br/><br/>(Valor exato, pontual.) |
| Função Inspecionar |**Sim** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* Filas de armazenamento oferecem suporte a atributos arbitrários que podem ser aplicadas toohello descrição da fila, na forma de saudação de pares nome/valor.
* As duas tecnologias oferecem Olá capacidade toopeek uma mensagem sem ter que toolock it, que pode ser útil ao implementar uma ferramenta de Gerenciador/navegador de filas.
* Olá .NET do barramento de serviço orientado a mensagens APIs aproveite full duplex conexões TCP para melhorar o desempenho quando comparado tooREST via HTTP e oferecem suporte a protocolo padrão Olá AMQP 1.0.
* Os nomes das filas do Armazenamento podem ter de 3 a 63 caracteres e podem conter letras minúsculas, número e hifens. Para obter mais informações, confira [Nomeando filas e metadados](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Nomes de fila do barramento de serviço podem ser a too260 caracteres e ter regras de nomenclatura menos restritivas. Os nomes de fila do Barramento de Serviço podem conter letras, números, pontos, hifens e sublinhados.

## <a name="authentication-and-authorization"></a>Autenticação e autorização
Esta seção discute os recursos de autenticação e autorização de saudação filas de armazenamento e filas do barramento de serviço com suporte.

| Critérios de comparação | Filas de armazenamento | Filas de barramento de serviço |
| --- | --- | --- |
| Autenticação |**Chave simétrica** |**Chave simétrica** |
| Modelo de segurança |Acesso delegado via tokens de SAS. |SAS |
| Federação do provedor de identidade |**Não** |**Sim** |

### <a name="additional-information"></a>Informações adicionais
* Tooeither cada solicitação de tecnologias de enfileiramento de mensagens de saudação deve ser autenticada. Não há suporte para filas públicas com acesso anônimo. Usando [SAS](service-bus-sas.md), você pode tratar esse cenário publicando uma SAS somente gravação, SAS somente leitura ou até mesmo uma SAS de acesso completo.
* Hello esquema de autenticação fornecido pelo armazenamento filas envolve o uso de saudação de uma chave simétrica, que é um baseadas em hash HMAC Message Authentication Code (), computado com o algoritmo de saudação SHA-256 e codificado como uma **Base64** cadeia de caracteres. Para obter mais informações sobre o protocolo respectivo hello, consulte [autenticação para Olá serviços de armazenamento do Azure](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). As filas do Barramento de Serviço oferecem suporte a um modelo semelhante usando chaves simétricas. Para obter mais informações, confira [Autenticação de Assinatura de Acesso Compartilhado com Barramento de Serviço](service-bus-sas.md).

## <a name="conclusion"></a>Conclusão
Obtendo uma compreensão mais profunda das tecnologias de saudação dois, você vai ser capaz de toomake uma decisão mais informada sobre qual tecnologia toouse da fila e quando. Olá decisão sobre quando toouse filas de armazenamento ou barramento de serviço filas claramente depende de vários fatores. Esses fatores podem depender consideravelmente necessidades individuais de saudação do seu aplicativo e sua arquitetura. Se seu aplicativo já utiliza recursos de núcleo de saudação do Microsoft Azure, você pode preferir toochoose filas de armazenamento, especialmente se você precisar de comunicação básica e mensagens entre serviços ou necessidade de filas que podem ser maiores do que 80 GB de tamanho.

Como as filas do Barramento de Serviço fornecem vários recursos avançados, como sessões, transações, detecção de duplicidade, mensagens mortas automáticas e recursos de publicação/assinatura duráveis, elas podem ser uma opção melhor se você estiver criando um aplicativo híbrido ou se seu aplicativo de alguma forma exigir esses recursos.

## <a name="next-steps"></a>Próximas etapas
Olá artigos a seguir fornece mais informações sobre como usar filas de armazenamento ou filas do barramento de serviço e diretrizes.

* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
* [Como tooUse Olá serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Práticas recomendadas para melhorias de desempenho usando o sistema de mensagens agenciado do Barramento de Serviço](service-bus-performance-improvements.md)
* [Introdução a filas e tópicos no Barramento de Serviço do Azure (postagem de blog)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Olá tooService de guia do desenvolvedor barramento](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Usando o serviço de enfileiramento de mensagens de saudação no Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

