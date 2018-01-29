---
title: Eventos personalizados para a Grade de Eventos do Azure com o PowerShell | Microsoft Docs
description: "Use a Grade de Eventos do Azure e o PowerShell para publicar um tópico e assinar esse evento."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 10/11/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 89c71194c2ef3c34b3356040c2e252fc09ba09c3
ms.sourcegitcommit: 4ed3fe11c138eeed19aef0315a4f470f447eac0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2017
---
# <a name="create-and-route-custom-events-with-azure-powershell-and-event-grid"></a>Criar e encaminhar eventos personalizados com o Azure PowerShell e a Grade de Eventos do Azure

A Grade de Eventos do Azure é um serviço de eventos para a nuvem. Neste artigo, você pode usar o Azure PowerShell para criar um tópico personalizado, assinar o tópico e disparar o evento para exibir o resultado. Normalmente, você envia eventos para um ponto de extremidade que responde ao evento, como um webhook ou uma Função do Azure. No entanto, para simplificar este artigo, você envia os eventos para uma URL que apenas coleta as mensagens. Você cria essa URL usando uma ferramenta de terceiros de software livre chamada [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** é uma ferramenta de software livre que não se destina ao uso com altas taxas de transferência. O uso da ferramenta aqui é meramente demonstrativo. Se você efetuar push de mais de um evento por vez, talvez não veja todos os eventos na ferramenta.

Quando tiver concluído, você verá que os dados do evento foram enviados para um ponto de extremidade.

![Dados de evento](./media/custom-event-quickstart-powershell/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

Este artigo requer que você esteja executando a versão mais recente do Azure PowerShell. Se você precisa instalar ou atualizar, confira [Instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Os tópicos de Grade de Eventos são recursos do Azure e devem ser colocados em um grupo de recursos do Azure. O grupo de recursos do Azure é uma coleção lógica na qual os recursos do Azure são implantados e gerenciados.

Crie um grupo de recursos com o comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).

O exemplo a seguir cria um grupo de recursos chamado *gridResourceGroup* no local *westus2*.

```powershell
New-AzureRmResourceGroup -Name gridResourceGroup -Location westus2
```

## <a name="create-a-custom-topic"></a>Criar um tópico personalizado

Um tópico fornece um ponto de extremidade definido pelo usuário aonde você posta seus eventos. O exemplo a seguir o tópico no seu grupo de recursos. Substitua `<topic_name>` por um nome exclusivo para o tópico. O nome do tópico deve ser exclusivo, pois é representado por uma entrada DNS. Para a versão prévia, a Grade de Eventos dá suporte às localizações **westus2** e **westcentralus**.

```powershell
New-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Location westus2 -Name <topic_name>
```

## <a name="create-a-message-endpoint"></a>Criar um ponto de extremidade de mensagem

Antes de assinar o tópico, vamos criar o ponto de extremidade para a mensagem do evento. Em vez de escrever código para responder ao evento, vamos criar um ponto de extremidade que coleta as mensagens, para que você possa exibi-las. O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele. Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**.  Copie a URL do compartimento, pois você precisará dela para assinar o tópico.

## <a name="subscribe-to-a-topic"></a>Assinar um tópico

Assine um tópico para indicar à Grade de Eventos quais eventos você deseja acompanhar. O exemplo a seguir assina o tópico que você criou e transmite a URL do RequestBin como o ponto de extremidade para notificação de eventos. Substitua `<event_subscription_name>` por um nome exclusivo para a sua assinatura e `<URL_from_RequestBin>` pelo valor da seção anterior. A especificação de um ponto de extremidade durante a assinatura faz com que a Grade de Eventos manipule o roteamento de eventos para esse ponto de extremidade. Em `<topic_name>`, use o valor que você criou anteriormente.

```powershell
New-AzureRmEventGridSubscription -EventSubscriptionName <event_subscription_name> -Endpoint <URL_from_RequestBin> -ResourceGroupName gridResourceGroup -TopicName <topic_name>
```

## <a name="send-an-event-to-your-topic"></a>Enviar um evento para o tópico

Agora, vamos disparar um evento para ver como a Grade de Eventos distribui a mensagem para o ponto de extremidade. Primeiro, vamos obter a URL e a chave para o tópico. Novamente, use o nome do tópico em `<topic_name>`.

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

Para simplificar este artigo, configure dados de evento de exemplo para enviar ao tópico. Normalmente, um aplicativo ou serviço do Azure enviaria os dados de evento. O exemplo abaixo obtém os dados do evento:

```powershell
$eventID = Get-Random 99999
$eventDate = Get-Date -Format s

$body = "[{`"id`": `"$eventID`",`"eventType`": `"recordInserted`",`"subject`": `"myapp/vehicles/motorcycles`",`"eventTime`": `"$eventDate`",`"data`":{`"make`": `"Ducati`",`"model`": `"Monster`"}}]"
```

Se você exibir `$body`, verá o evento completo. O elemento `data` do JSON é a carga do evento. Qualquer JSON bem formado pode ficar nesse campo. Você também pode usar o campo de assunto para roteamento e filtragem avançados.

Agora, envie o evento para o tópico.

```powershell
Invoke-WebRequest -Uri $endpoint -Method POST -Body $body -Headers @{"aeg-sas-key" = $keys.Key1}
```

Você disparou o evento e a Grade de Eventos enviou a mensagem para o ponto de extremidade configurado durante a assinatura. Navegue até a URL do RequestBin que você criou anteriormente. Ou clique em Atualizar no navegador do RequestBin aberto. Você verá o evento que acabou de ser enviado.

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>Limpar recursos

Se você planeja continuar a trabalhar com esse evento, não limpe os recursos criados neste artigo. Caso contrário, use os comandos a seguir para excluir os recursos criados por você neste artigo.

```powershell
Remove-AzureRmResourceGroup -Name gridResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Agora que você sabe como criar tópicos e assinaturas de evento, saiba mais sobre como a Grade de Eventos pode ajudá-lo:

- [Sobre a Grade de Eventos](overview.md)
- [Rotear eventos do Armazenamento de Blobs para um ponto de extremidade da Web personalizado](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)
- [Monitorar alterações de máquina virtual com a Grade de Eventos do Azure e os Aplicativos Lógicos](monitor-virtual-machine-changes-event-grid-logic-app.md)
- [Transmitir Big Data para um data warehouse](event-grid-event-hubs-integration.md)
