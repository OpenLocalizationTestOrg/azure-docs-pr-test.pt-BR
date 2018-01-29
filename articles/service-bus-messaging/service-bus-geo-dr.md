---
title: "Recuperação de desastre em área geográfica do Barramento de Serviço do Azure | Microsoft Docs"
description: "Como usar regiões geográficas para fazer failover e executar a recuperação de desastre no Barramento de Serviço do Azure"
services: service-bus-messaging
documentationcenter: 
author: christianwolf42
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: sethm
ms.openlocfilehash: fdeb9ba55fc8eade95f6fca88f47dd12aa18a480
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2017
---
# <a name="azure-service-bus-geo-disaster-recovery"></a>Recuperação de desastre em área geográfica do Barramento de Serviço do Azure

Quando datacenters ou regiões inteiras do Azure (se nenhuma [zona de disponibilidade](../availability-zones/az-overview.md) for usada) enfrentam tempo de inatividade, é essencial para o processamento de dados continuar a operar em uma região ou datacenter diferente. Como tal, *a recuperação de desastre em área geográfica* e a *replicação geográfica* são recursos importantes para qualquer empresa. O Barramento de Serviço do Azure dá suporte à recuperação de desastre em área geográfica e à replicação geográfica no nível do namespace. 

O recurso de recuperação de desastres em área geográfica fica globalmente disponível para a SKU Premium do Barramento de Serviço. 

## <a name="outages-and-disasters"></a>Interrupções e desastres

É importante observar a diferença entre “falhas” e “desastres”. Uma *interrupção* é uma indisponibilidade temporária do Barramento de Serviço do Azure e pode afetar alguns componentes do serviço, como um repositório de mensagens ou até mesmo o datacenter inteiro. No entanto, depois que o problema for corrigido, o Barramento de Serviço ficará disponível novamente. Normalmente, uma interrupção não causa a perda de mensagens ou de outros dados. Um exemplo de tal interrupção pode ser uma falha de energia no datacenter. Algumas falhas são apenas perdas de conexão curtas devido a problemas de rede ou transitórios. 

Um *desastre* é definido como a perda permanente ou de longo prazo de um cluster do Barramento de Serviço, uma região do Azure ou um datacenter. A região ou o datacenter pode ou não ficar disponível novamente ou pode ficar inativo por horas ou dias. Outros exemplos desses desastres são incêndios, enchentes ou terremoto. Um desastre que se torne permanente pode causar a perda de algumas mensagens, alguns eventos ou outros dados. No entanto, na maioria dos casos, não deve haver perda de dados e as mensagens poderão ser recuperadas depois que do backup do data center.

O recurso de recuperação de desastre em área geográfica do Barramento de Serviço do Azure é uma solução de recuperação de desastre. Os conceitos e o fluxo de trabalho descrito neste artigo se aplicam a cenários de desastre e não a falhas transitórias ou temporárias. Para uma discussão detalhada sobre a recuperação de desastre no Microsoft Azure, consulte [este artigo](/azure/architecture/resiliency/disaster-recovery-azure-applications).   

## <a name="basic-concepts-and-terms"></a>Termos e conceitos básicos

O recurso de recuperação de desastre implementa a recuperação de desastre dos metadados e se baseia em namespaces de recuperação de desastre primário e secundário. Observe que o recurso de recuperação de desastre em área geográfica está disponível somente para a [SKU Premium](service-bus-premium-messaging.md). Você não precisa fazer nenhuma alteração de cadeia de conexão, já que a conexão é feita por meio de um alias.

Os seguintes termos são usados neste artigo:

-  *Alias*: o nome para uma configuração de recuperação de desastres que você configurou. O alias fornece uma única cadeia de conexão estável do FQDN (Nome de Domínio Totalmente Qualificado). Aplicativos usam essa cadeia de conexão de alias para conectarem-se a um namespace. 

-  *Namespace primário/secundário*: os namespaces que correspondem ao alias. O namespace primário é “ativo” e recebe mensagens (que pode ser um namespace existente ou novo). O namespace secundário “passivo” e não recebe mensagens. Os metadados entre os dois estão sincronizados, para que ambos possam aceitar mensagens continuamente sem quaisquer alterações no código do aplicativo ou na cadeia de conexão. Para garantir que apenas o namespace ativo receba mensagens, você deve usar o alias. 

-  *Metadados*: entidades como filas, tópicos e assinaturas; e suas propriedades do serviço que são associadas ao namespace. Observe que somente entidades e suas configurações são replicadas automaticamente. Mensagens não são replicadas. 

-  *Failover*: o processo de ativação do namespace secundário.

## <a name="setup-and-failover-flow"></a>Instalação e fluxo de failover

A seção a seguir é uma visão geral do processo de failover e explica como configurar o failover inicial. 

![1][]

### <a name="setup"></a>Configuração

Primeiro crie ou use um namespace primário existente e um novo namespace secundário, depois emparelhe os dois. Esse emparelhamento fornece um alias que você pode usar para se conectar. Como você usa um alias, não precisa alterar cadeias de conexão. Somente novos namespaces podem ser adicionados ao emparelhamento de failover. Por fim, você deve adicionar um monitoramento para detectar se um failover é necessário. Na maioria dos casos, o serviço é uma parte de um grande ecossistema, assim, failovers automáticos raramente são possíveis, uma vez que failovers devem ser executados em sincronia com o subsistema ou a infraestrutura restante.

### <a name="example"></a>Exemplo

Em um exemplo desse cenário, considere uma solução de ponto de venda (PDV) que emita mensagens ou eventos. O Barramento de Serviço transmite esses eventos para soluções de mapeamento ou reformatação solução, que encaminha dados mapeado para outro sistema para processamento adicional. Nesse ponto, todos esses sistemas podem ser hospedados na mesma região do Azure. A decisão sobre quando fazer o failover e em qual parte depende do fluxo de dados em sua infraestrutura. 

Você pode automatizar o failover tanto com sistemas de monitoramento ou com soluções de monitoramento personalizadas. No entanto, essa automação precisa de planejamento e trabalho adicionais, o que está fora do escopo deste artigo.

### <a name="failover-flow"></a>Fluxo do failover

Se você iniciar o failover, as duas etapas são necessárias:

1. Caso ocorra outra interrupção, você deve ser capaz de fazer failover novamente. Portanto, configure outro namespace passivo e atualize o emparelhamento. 

2. Faça pull das mensagens do namespace primário anterior assim que estiver disponível novamente. Depois disso, use esse namespace para mensagens regulares fora de sua configuração de recuperação geográfica ou exclua o namespace primário antigo.

> [!NOTE]
> Há suporte apenas para semânticas encaminhadas com falha. Nesse cenário, você faz o failover e emparelha novamente com um novo namespace. Não há suporte para failback, em um cluster do SQL por exemplo. 

![2][]

## <a name="management"></a>Gerenciamento

Se você cometeu um erro, por exemplo, emparelhou as regiões erradas durante a configuração inicial, você pode interromper o emparelhamento dos dois namespaces a qualquer momento. Se você quiser usar os namespaces emparelhados como namespaces regulares, exclua o alias.

## <a name="use-existing-namespace-as-alias"></a>Usar namespace existente como alias

Caso tenha um cenário no qual você não pode alterar as conexões de produtores e consumidores, você pode reutilizar o nome do namespace como o nome do alias. Consulte o [exemplo de código no GitHub aqui](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR_existing_namespace_name).

## <a name="samples"></a>Exemplos

Os [exemplos no GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR2) mostram como configurar e iniciar um failover. Esses exemplos demonstram os conceitos a seguir:

- Configurações necessárias no Azure Active Directory para usar o Azure Resource Manager com o Barramento de Serviço. 
- Etapas necessárias para executar o código de exemplo. 
- Envio e recebimento do namespace primário atual. 
- Como usar um namespace existente como alias.

## <a name="considerations"></a>Considerações

Observe as seguintes considerações a serem lembradas desta versão:

1. Em seu planejamento de failover, você também deve considerar o fator tempo. Por exemplo, se você perder a conectividade por mais de 15 a 20 minutos, pode decidir iniciar o failover. 
 
2. O fato de que nenhum dado seja replicado significa que sessões atualmente ativas não são replicadas. Além disso, a detecção duplicada e mensagens programadas podem não funcionar. Novas sessões, mensagens programadas e novas duplicatas funcionarão. 

3. O failover de uma infraestrutura complexa distribuída deve ser [testado](/azure/architecture/resiliency/disaster-recovery-azure-applications#disaster-simulation) pelo menos uma vez. 

4. A sincronização de entidades pode levar algum tempo, cerca de 50 a 100 entidades por minuto. Assinaturas e regras também são contadas como entidades. 

## <a name="next-steps"></a>Próximas etapas

- Consulte a [referência da API REST de recuperação de desastre em área geográfica aqui](/rest/api/servicebus/disasterrecoveryconfigs).
- Execute o [exemplo no GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR2) da recuperação de desastre em área geográfica.
- Consulte o [exemplo que envia mensagens a um alias](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/TestGeoDR/ConsoleApp1) da recuperação de desastre em área geográfica.

Para saber mais sobre as mensagens do Barramento de Serviço, confira os artigos a seguir:

* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Filas, tópicos e assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md)
* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
* [Como usar tópicos e assinaturas do Barramento de Serviço](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* [API REST](/rest/api/servicebus/) 

[1]: ./media/service-bus-geo-dr/geo1.png
[2]: ./media/service-bus-geo-dr/geo2.png
