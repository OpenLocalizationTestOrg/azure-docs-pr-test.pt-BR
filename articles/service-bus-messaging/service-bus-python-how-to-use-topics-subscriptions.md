---
title: "tópicos de barramento de serviço do Azure toouse aaaHow com Python | Microsoft Docs"
description: "Saiba como toouse Azure Service Bus tópicos e assinaturas do Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Como toouse Service Bus tópicos e assinaturas com Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artigo descreve como toouse Service Bus tópicos e assinaturas. exemplos de saudação são escritos em Python e usar Olá [pacote do Azure SDK de Python][Azure Python package]. Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**. Para obter mais informações sobre tópicos e assinaturas, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Se você precisar tooinstall Python ou Olá [pacote do Azure Python][Azure Python package], consulte Olá [guia de instalação do Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>Criar um tópico
Olá **ServiceBusService** objeto permite que você toowork com tópicos. Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically barramento de serviço:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Olá código a seguir cria um **ServiceBusService** objeto. Substitua `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` pelo namespace real e pelo nome e valor da chave de SAS (Assinatura de Acesso Compartilhado).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Você pode obter valores de saudação para o nome da chave SAS hello e valor de Olá [portal do Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Olá `create_topic` método também oferece suporte a opções adicionais, que permitem que você toooverride configurações do tópico como tamanho de tópico toolive ou máximo de tempo de mensagem. Olá exemplo a seguir define Olá máximo do tópico tamanho too5 GB e um valor de (vida útil TTL) toolive tempo de 1 minuto:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Criar assinaturas
Assinaturas tootopics também são criados com hello **ServiceBusService** objeto. As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens entregues a fila virtual toohello da assinatura.

> [!NOTE]
> Assinaturas são persistentes e continuarão tooexist até a eles ou hello toowhich tópico se inscreveu, serão excluídas.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma assinatura com o filtro saudação padrão (MatchAll)
Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada. Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas em fila virtual da assinatura hello. Olá, exemplo a seguir cria uma assinatura chamada `AllMessages` e usa Olá padrão **MatchAll** filtro.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Criar assinaturas com os filtros
Você também pode definir filtros que permitem que você toospecify quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.

Hello mais flexível o tipo de filtro de assinaturas com suporte é um **SqlFilter**, que implementa um subconjunto do SQL92. Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico. Para obter mais informações sobre expressões de saudação que pode ser usado com um filtro SQL, consulte Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.

Você pode adicionar filtros tooa assinatura usando Olá **criar\_regra** método hello **ServiceBusService** objeto. Esse método permite que você tooadd novos filtros tooan assinatura existente.

> [!NOTE]
> Porque o saudação padrão filtro será aplicado automaticamente tooall novas assinaturas, você deve primeiro remover o filtro de padrão de saudação ou hello **MatchAll** substituirá os outros filtros que você pode especificar. Você pode remover a regra padrão de saudação usando Olá `delete_rule` método hello **ServiceBusService** objeto.
> 
> 

Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um personalizado `messagenumber` propriedade maior que 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um **SqlFilter** que seleciona somente as mensagens que têm um `messagenumber` propriedade menor ou igual too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Agora, quando uma mensagem é enviada muito`mytopic` toohello tooreceivers inscrito sempre é fornecida **AllMessages** assinatura de tópico e tooreceivers seletivamente entregue inscrito toohello **HighMessages**  e **LowMessages** assinaturas de tópico (dependendo do conteúdo da mensagem de saudação).

## <a name="send-messages-tooa-topic"></a>Enviar tópico tooa de mensagens
toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo deve usar Olá `send_topic_message` método hello **ServiceBusService** objeto.

Olá exemplo a seguir demonstra como teste toosend cinco mensagens muito`mytopic`. Observe que Olá `messagenumber` varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (Isso determina quais assinaturas recebem-lo):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite de tamanho total Olá mensagens de saudação mantidos por um tópico. O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB. Para saber mais sobre cotas, confira [Service Bus quotas][Service Bus quotas] (Cotas do Barramento de Serviço).

## <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma assinatura
As mensagens são recebidas de uma assinatura usando Olá `receive_subscription_message` método hello **ServiceBusService** objeto:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

As mensagens serão excluídas da assinatura Olá conforme elas são de leitura quando Olá parâmetro `peek_lock` está definido muito**False**. Você pode ler (pico) e bloquear a mensagem de saudação sem excluí-la da fila de saudação pelo parâmetro de saudação configuração `peek_lock` muito**True**.

Olá comportamento de leitura e excluindo mensagem de saudação como parte da saudação de operação de recebimento é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Se hello `peek_lock` parâmetro está definido muito**True**, Olá recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando `delete` método hello **mensagem** objeto. Olá `delete` método marca a mensagem de saudação como sendo consumida e remove da assinatura de saudação.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello `unlock` método hello **mensagem** objeto. Isso causar a mensagem de saudação do barramento de serviço toounlock de assinatura do hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada em assinatura hello e se a mensagem de saudação tooprocess antes de falha de aplicativo hello Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e a mensagem de saudação desbloqueia o barramento de serviço automaticamente e o torna disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação `delete` método é chamado, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *, pelo menos, após processamento*, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá **MessageId** propriedade da mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Excluir tópicos e assinaturas
Tópicos e assinaturas são persistentes e deve ser explicitamente excluídos por meio de saudação [portal do Azure] [ Azure portal] ou programaticamente. Olá exemplo a seguir mostra como o tópico de saudação toodelete chamado `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Excluir um tópico também exclui qualquer assinatura que é registrada com o tópico de saudação. As assinaturas também podem ser excluídas de forma independente. Olá código a seguir mostra como toodelete uma assinatura chamada `HighMessages` de saudação `mytopic` tópico:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de tópicos do barramento de serviço, siga essas toolearn links mais.

* Confira [Filas, tópicos e assinaturas][Queues, topics, and subscriptions].
* Referência para [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
