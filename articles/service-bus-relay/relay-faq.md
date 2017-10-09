---
title: "aaaAzure perguntas frequentes de retransmissão | Microsoft Docs"
description: "Obtenha respostas toosome perguntas frequentes sobre o Azure retransmissão."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Perguntas frequentes sobre Retransmissão do Azure

Este artigo responde a algumas perguntas frequentes sobre a [Retransmissão do Azure](https://azure.microsoft.com/services/service-bus/). Para informações gerais sobre preço e suporte do Azure, consulte [Perguntas frequentes sobre suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Perguntas gerais
### <a name="what-is-azure-relay"></a>O que é Retransmissão do Azure?
Olá [serviço de retransmissão do Azure](relay-what-is-it.md) facilita a seus aplicativos híbridos ajudá-lo a expor serviços que residem em uma nuvem pública de toohello de rede corporativos com mais segurança. Você pode expor serviços Olá sem abrir uma conexão do firewall e sem a necessidade de infraestrutura de rede corporativa tooa alterações intrusiva.

### <a name="what-is-a-relay-namespace"></a>O que é um namespace de Retransmissão?
Um [namespace](relay-create-namespace-portal.md) é um contêiner de escopo que você pode usar os recursos de retransmissão de tooaddress dentro de seu aplicativo. Você deve criar uma retransmissão de toouse do namespace. Esta é uma das primeiras etapas Olá no guia de Introdução.

### <a name="what-happened-tooservice-bus-relay-service"></a>Quais tooService com serviço de retransmissão de barramento?
Olá anteriormente chamado serviço de retransmissão de barramento de serviço agora é chamado de retransmissão do WCF. Você pode continuar toouse esse serviço como de costume. recurso de conexões híbridas Olá é uma versão atualizada de um serviço que é foi transplanted de Serviços BizTalk do Azure. Retransmissão do WCF e conexões híbridas continuam toobe com suporte.

## <a name="pricing"></a>Preços
Essas respostas mostram em seção algumas perguntas frequentes sobre Olá retransmissão estrutura de preços. Você também pode ver [Perguntas frequentes sobre o suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para obter informações gerais de preço do Azure. Para obter informações completas sobre o preço da Retransmissão, consulte [Detalhes de preço do Barramento de Serviço][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Como são cobradas as Conexões Híbridas e a Retransmissão do WCF?
Para obter informações completas sobre os preços de retransmissão, consulte Olá [conexões híbridas e retransmissões WCF] [ Pricing overview] tabela na página de detalhes de preços do hello barramento de serviço. Além disso toohello preços observado nessa página, você será cobrado por transferências de dados para egresso fora Olá datacenter no qual o aplicativo é provisionado.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Como sou cobrado por Conexões Híbridas?
Aqui estão três exemplos de cenários de cobrança para Conexões Híbridas:

*   Cenário 1:
    *   Você tem um ouvinte único, como uma instância do hello Gerenciador de conexões híbridas instalado e em execução continuamente para o mês inteiro hello.
    *   Você enviar 3 GB de dados pela conexão Olá durante o mês de saudação. 
    *   O encargo total é de US$ 5.
*   Cenário 2:
    *   Você tem um ouvinte único, como uma instância do hello Gerenciador de conexões híbridas instalado e em execução continuamente para o mês inteiro hello.
    *   Você pode enviar 10 GB de dados pela conexão Olá durante o mês de saudação.
    *   O encargo total é de US$ 7,50. US $5 por conexão hello e primeiros 5 GB + US $2,50 para Olá adicional 5 GB de dados.
*   Cenário 3:
    *   Você tem duas instâncias, A e B, de saudação Gerenciador de conexões híbridas instalado e em execução continuamente para o mês inteiro hello.
    *   Você enviar 3 GB de dados pela conexão de um mês de saudação.
    *   Você enviar 6 GB de dados pela conexão B durante o mês de saudação.
    *   O encargo total é de US$ 10,50. Que é de US $5 para conexão A + US $5 por conexão B + US $0,50 (por gigabyte sexto de saudação na conexão B).

Observe que preços Olá usados nos exemplos de saudação são aplicáveis somente durante o período de visualização de conexões híbridas hello. Os preços são toochange de assunto na disponibilidade geral de conexões híbridas.

### <a name="how-are-hours-calculated-for-relay"></a>Como as horas são calculadas para Retransmissão?

A Retransmissão do WCF está disponível apenas nos namespaces da camada Standard. Preços e [cotas de conexão](../service-bus-messaging/service-bus-quotas.md) para retransmissões não mudaram em outros aspectos. Isso significa que as retransmissões continuam toobe cobradas com base no número de saudação de mensagens (não operações) e horas de retransmissão. Para obter mais informações, consulte Olá ["Híbrida conexões e WCF retransmissões"](https://azure.microsoft.com/pricing/details/service-bus/) tabela na página de detalhes de preços de saudação.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>E se eu tiver mais de um ouvinte conectado tooa específico de retransmissão?
Em alguns casos, uma única retransmissão pode ter vários ouvintes conectados. Uma retransmissão é considerada aberta quando pelo menos um ouvinte de retransmissão é tooit conectado. Adicionando resultados de retransmissão aberta tooan ouvintes nas horas de retransmissão adicionais. Olá número de retransmissão remetentes (clientes que chamam ou enviar mensagens toorelays) que estão conectados tooa retransmissão não afeta o cálculo de saudação de horas de retransmissão.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Como o medidor de mensagens de saudação é calculado para o WCF retransmissões?
(**Isso se aplica apenas tooWCF retransmissões. As mensagens não são um custo para Conexões Híbridas.**)

Em geral, mensagens cobráveis para retransmissões são calculadas usando Olá mesmo método que é usado para orientadas entidades (filas, tópicos e assinaturas), descritas anteriormente. No entanto, há algumas diferenças importantes.

Enviar uma retransmissão de barramento de serviço de tooa da mensagem é tratado como um "completo por meio de" envia toohello ouvinte de retransmissão que recebe a mensagem de saudação. Ele não é tratado como um retransmissor envio operação toohello barramento de serviço, seguido por um ouvinte de retransmissão de toohello de entrega. Uma invocação de serviço do estilo de solicitação-resposta (de até too64 KB) em relação a um resultados de ouvinte de retransmissão em duas mensagens cobráveis: uma mensagem cobrável para a solicitação de saudação e uma mensagem cobrável para a resposta de saudação (supondo que a resposta de saudação também é 64 KB ou menor). Isso é diferente de usar um toomediate de fila entre um cliente e um serviço. Se você usar um toomediate de fila entre um cliente e um serviço, hello mesmo padrão solicitação-resposta requer uma fila de toohello de envio de solicitação, seguida por uma remoção da fila/entrega do serviço de toohello de fila de saudação. Isso é seguido por uma fila de tooanother de envio de resposta e uma remoção da fila/entrega desse cliente de toohello de fila. Usando o mesmo tamanho suposições (backup too64 KB) de hello, Olá mediado fila padrão resultará em 4 mensagens cobráveis. Você será cobrado por Olá dobro de saudação do tooimplement mensagens que mesmo padrão que pode ser feito usando a retransmissão. Obviamente, existem benefícios toousing filas tooachieve esse padrão, como durabilidade e nivelamento de carga. Esses benefícios podem justificar a despesa adicional hello.

Retransmissões abertas usando Olá **netTCPRelay** associação WCF tratam as mensagens não como mensagens individuais, mas como um fluxo de dados por meio do sistema de saudação. Quando você usa essa associação, apenas hello remetente e o ouvinte têm visibilidade de enquadramento Olá individuais das mensagens de saudação enviadas e recebidas. Para retransmissões que usam Olá **netTCPRelay** de associação, todos os dados é tratado como um fluxo para o cálculo das mensagens cobráveis. Nesse caso, o barramento de serviço calcula a quantidade total de saudação de dados enviados ou recebidos através de cada retransmissão individual em uma base de 5 minutos. Em seguida, divide essa quantidade total de dados pelo número de saudação toodetermine 64 KB de mensagens cobráveis para essa retransmissão durante esse período de tempo.

## <a name="quotas"></a>Cotas
| Nome da cota | Escopo | Tipo | Comportamento quando excedido | Valor |
| --- | --- | --- | --- | --- |
| Ouvintes simultâneos em uma retransmissão |Entidade |estático |As solicitações subsequentes de conexões adicionais serão rejeitadas e uma exceção será recebida pelo Olá chamando código. |25 |
| Ouvintes simultâneos da retransmissão |Todo o sistema |estático |As solicitações subsequentes de conexões adicionais serão rejeitadas e uma exceção será recebida pelo Olá chamando código. |2.000 |
| Conexões de retransmissão simultâneas por todos os pontos de extremidade de retransmissão em um namespace de serviço |Todo o sistema |estático |- |5.000 |
| Pontos de extremidade de retransmissão por namespace de serviço |Todo o sistema |estático |- |10.000 |
| Tamanho de mensagem para retransmissões [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) e [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) |Todo o sistema |estático |As mensagens recebidas que excederem essas cotas serão rejeitadas e uma exceção será recebida pelo Olá chamando código. |64 KB |
| Tamanho de mensagem para retransmissões [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) e [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) |Todo o sistema |estático |- |Ilimitado |

### <a name="does-relay-have-any-usage-quotas"></a>A retransmissão tem alguma cota de uso?
Por padrão, para qualquer serviço de nuvem, a Microsoft define uma cota de uso mensal agregada que é calculada para todas as assinaturas de um cliente. Sabemos que, às vezes, suas necessidades podem exceder esses limites. Você pode contatar o atendimento ao cliente a qualquer momento para que possamos compreender suas necessidades e ajustar esses limites adequadamente. Barramento de serviço, cotas de uso de agregação de saudação são:

* 5 bilhões de mensagens
* 2 milhões de horas de retransmissão

Embora reservamos Olá direito toodisable uma conta que excede suas cotas de uso mensal, podemos fornecer notificação por email e podemos fazer várias tentativas toocontact Prezado cliente antes de realizar qualquer ação. Os clientes que excedem essas cotas ainda são responsáveis por encargos em excesso.

### <a name="naming-restrictions"></a>Restrições de nomenclatura
Um nome de namespace de Retransmissão deve ter entre 6 e 50 caracteres.

## <a name="subscription-and-namespace-management"></a>Gerenciamento de assinaturas e de namespaces
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Como migrar um namespace tooanother assinatura do Azure?

toomove um namespace de uma assinatura de tooanother de assinatura do Azure, você pode hello ou use [portal do Azure](https://portal.azure.com) ou usar comandos do PowerShell. toomove uma assinatura do namespace tooanother, Olá namespace já deve estar ativo. usuário Olá executando comandos Olá deve ser um usuário de administrador em ambas as assinaturas de origem e destino hello.

#### <a name="azure-portal"></a>Portal do Azure

Olá toouse toomigrate portal do Azure Azure retransmissão namespaces de assinatura de tooanother de uma assinatura, consulte [mover recursos tooa novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove um namespace de assinatura de tooanother de uma assinatura do Azure, use Olá sequência de comandos a seguir. tooexecute essa operação, Olá namespace já deve estar ativo e usuário Olá executando comandos do PowerShell Olá deve ser um usuário de administrador em ambas as assinaturas de origem e destino hello.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Quais são algumas das exceções Olá gerados por APIs de retransmissão do Azure e sugerido ações?
Para obter uma descrição de exceções comuns e ações sugeridas que você executar, consulte [Exceções de retransmissão][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>O que é uma assinatura de acesso compartilhado e quais idiomas posso usar toogenerate uma assinatura?
As SAS (Assinaturas de Acesso Compartilhado) são um mecanismo de autenticação com base em hashes seguros SHA-256 ou URIs. Para obter informações sobre como toogenerate suas próprias assinaturas no nó, PHP, Java, C e c#, consulte [autenticação do barramento de serviço com assinaturas de acesso compartilhado][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>É possível toowhitelist pontos de extremidade de retransmissão?
Sim. cliente de retransmissão Olá faz conexões toohello serviço de retransmissão do Azure usando nomes de domínio totalmente qualificado. Os clientes podem adicionar uma entrada para `*.servicebus.windows.net` nos firewalls que dão suporte à lista de permissões de DNS.

## <a name="next-steps"></a>Próximas etapas
* [Criar um namespace](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md