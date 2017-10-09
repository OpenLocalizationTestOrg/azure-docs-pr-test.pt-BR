---
title: "Perguntas frequentes (FAQ) do barramento de serviço do aaaAzure | Microsoft Docs"
description: "Responde a algumas perguntas frequentes sobre o Barramento de Serviço do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Perguntas frequentes sobre o Barramento de Serviço
Este artigo responde a algumas perguntas frequentes sobre o Barramento de Serviço do Microsoft Azure. Você também pode visitar Olá [perguntas frequentes de suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para informações gerais de suporte e preços do Azure.

## <a name="general-questions-about-azure-service-bus"></a>Perguntas gerais sobre o Barramento de Serviço do Azure
### <a name="what-is-azure-service-bus"></a>O que é o Barramento de Serviço do Azure?
[Barramento de serviço do Azure](service-bus-messaging-overview.md) é uma plataforma de nuvem de mensagens assíncronas que permite que você toosend dados entre sistemas separados. A Microsoft oferece esse recurso como um serviço, o que significa que você não precisa toohost algum hardware em ordem toouse-lo.

### <a name="what-is-a-service-bus-namespace"></a>O que é um namespace do Barramento de Serviço?
Um [namespace](service-bus-create-namespace-portal.md) fornece um contêiner de escopo para endereçar recursos do barramento de serviço dentro de seu aplicativo. Criando um é necessário toouse barramento de serviço e deve ser um dos Olá primeiras etapas no guia de Introdução.

### <a name="what-is-an-azure-service-bus-queue"></a>O que é uma fila do Barramento de Serviço do Azure?
A [Fila do Barramento de Serviço](service-bus-queues-topics-subscriptions.md) é uma entidade na qual as mensagens são armazenadas. Filas são particularmente úteis quando você tiver vários aplicativos ou várias partes de um aplicativo distribuído que precise toocommunicate uns com os outros. fila de saudação é semelhante Centro de distribuição de tooa vários produtos (mensagens) são recebidos e, em seguida, enviados daquele local.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>O que são os tópicos e as assinaturas do Barramento de Serviço do Azure?
Um tópico pode ser visualizado como uma fila e ao usar várias assinaturas, ele se torna um modelo mais abrangente de mensagens; essencialmente, uma ferramenta de comunicação de um-para-muitos. Esse modelo de publicação/assinatura (ou *pub/sub*) permite que um aplicativo que envia essa mensagem recebida por vários aplicativos de um tópico de mensagem de tooa com vários toohave de assinaturas.

### <a name="what-is-a-partitioned-entity"></a>O que é uma entidade particionada?
Uma fila ou um tópico convencional é manipulado por um único agente de mensagem e armazenado em um repositório de mensagens. Uma [fila ou um tópico particionado](service-bus-partitioning.md) é manipulada por vários agentes de mensagens e armazenada em vários repositórios de mensagens. Isso significa que Olá taxa de transferência geral de uma fila ou tópico particionados não é limitada pelo desempenho de saudação de um único agente de mensagens ou repositório de mensagens. Além disso, uma interrupção temporária de um repositório de mensagens não torna uma fila ou um tópico particionado indisponível.

Observe que a ordenação não é garantida ao usar o particionamento de entidades. No evento de saudação que uma partição não está disponível, você ainda pode enviar e receber mensagens de saudação outras partições.

## <a name="best-practices"></a>Práticas recomendadas
### <a name="what-are-some-azure-service-bus-best-practices"></a>Quais são algumas das práticas recomendadas do Barramento de Serviço do Azure?
* [Práticas recomendadas para melhorias de desempenho usando o barramento de serviço] [ Best practices for performance improvements using Service Bus] – este artigo descreve como toooptimize desempenho durante a troca de mensagens.

### <a name="what-should-i-know-before-creating-entities"></a>O que devo saber antes de criar entidades?
saudação de propriedades de uma fila e tópico a seguir é imutável. Leve isso em conta ao provisionar suas entidades, já que isso não pode ser modificado sem criar uma nova entidade de substituição.

* Tamanho
* Particionamento
* Sessões
* Detecção de duplicidade
* Entidade expressa

## <a name="pricing"></a>Preços
Esta seção respostas a algumas perguntas frequentes sobre a estrutura de preços de barramento de serviço hello.

Olá [preços e faturamento do barramento do serviço](service-bus-pricing-billing.md) artigo explica metros de cobrança Olá no barramento de serviço e para obter informações sobre opções de preços de barramento de serviço, consulte [detalhes de preços de barramento de serviço](https://azure.microsoft.com/pricing/details/service-bus/).

Você também pode visitar Olá [perguntas frequentes sobre o suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) geral Azure informações sobre preços. 

### <a name="how-do-you-charge-for-service-bus"></a>Como é cobrado o Barramento de Serviço?
Para saber mais sobre o preço do Barramento de Serviço, veja [Detalhes de preço do Barramento de Serviço][Pricing overview]. Além disso toohello preços observado, você será cobrado por transferências de dados para egresso fora Olá data center em que seu aplicativo é provisionado.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>O uso do barramento de serviço é o assunto de transferência de toodata? O que é não está?
Todas as transferências de dados dentro de uma determinada região do Azure são feitas gratuitamente, bem como qualquer transferência de dados recebida. Transferência de dados fora de uma região é encargos de tooegress de entidade que podem ser encontrados [aqui](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>O Barramento de Serviço cobra pelo armazenamento?
Não, o Barramento de Serviço não cobra pelo armazenamento. No entanto, há uma cota limitação Olá quantidade máxima de dados que podem persistir por fila/tópico. Consulte a próxima FAQ de saudação.

## <a name="quotas"></a>Cotas

Para obter uma lista de cotas e limites de barramento de serviço, consulte Olá [visão geral sobre cotas de barramento de serviço][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>O Barramento de Serviço tem cotas de uso?
Por padrão, para qualquer serviço de nuvem, a Microsoft define uma cota de uso mensal agregado calculada entre todas as assinaturas de um cliente. Como compreendemos que talvez seja necessário usar mais do que esses limites, contate o atendimento ao cliente a qualquer momento para que possamos entender as suas necessidades e ajustar esses limites adequadamente. Barramento de serviço, a cota de uso de agregação de saudação é 5 bilhões de mensagens por mês.

Embora nos reservemos Olá direito toodisable uma conta de cliente que tenha excedido suas cotas de uso em um determinado mês, vamos fornecer notificação por email e fazer várias toocontact de tentativas de um cliente antes de realizar qualquer ação. Os clientes que excederem essas cotas ainda serão responsáveis pelas cobranças que excederem Olá cotas.

Assim como acontece com outros serviços no Azure, barramento de serviço aplica um conjunto de cotas específicas tooensure que há um uso justo de recursos. Você pode encontrar mais detalhes sobre essas cotas no hello [visão geral sobre cotas de barramento de serviço][Quotas overview].

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>O que são exceções Olá geradas pelas APIs de barramento de serviço do Azure e suas ações sugeridas?
Para obter uma lista de exceções possíveis do Barramento de Serviço, confira [Visão geral das exceções][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>O que é uma Assinatura de Acesso Compartilhado e quais idiomas oferecem suporte para a geração de uma assinatura?
As Assinaturas de Acesso Compartilhado são um mecanismo de autenticação com base em hashes seguros SHA-256 ou URIs. Para obter informações sobre como toogenerate suas próprias assinaturas no nó, PHP, Java e C\#, consulte Olá [assinaturas de acesso compartilhado] [ Shared Access Signatures] artigo.

## <a name="subscription-and-namespace-management"></a>Gerenciamento de assinaturas e de namespaces
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Como migrar um namespace tooanother assinatura do Azure?

Você pode mover um namespace de tooanother de uma assinatura do Azure, usando qualquer Olá [portal do Azure](https://portal.azure.com) ou comandos do PowerShell. Na operação de saudação do pedido tooexecute, Olá namespace já deve estar ativo. usuário Olá executando comandos Olá deve ser um administrador em ambos os fonte hello e assinaturas de destino.

#### <a name="portal"></a>Portal

Olá toouse assinatura de tooanother namespaces do barramento de serviço toomigrate portal do Azure, siga as instruções de saudação [aqui](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Olá sequência de comandos do PowerShell a seguir move um namespace de um tooanother de assinatura do Azure. tooexecute essa operação, Olá namespace já deve estar ativo e usuário Olá executando comandos do PowerShell Olá deve ser um administrador em ambas as assinaturas de origem e destino hello.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o barramento de serviço, consulte Olá tópicos a seguir.

* [Introdução ao Barramento de Serviço Premium do Azure (postagem de blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introdução ao Barramento de Serviço Premium do Azure (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Visão geral do Barramento de Serviço](service-bus-messaging-overview.md)
* [Visão geral da arquitetura de Barramento de Serviço do Azure](service-bus-fundamentals-hybrid-solutions.md)
* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
