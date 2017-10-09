---
title: eventos de aaaCustom para grade de eventos do Azure | Microsoft Docs
description: "Use a grade de eventos do Azure toopublish um tópico e assinar o evento toothat."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Criar e encaminhar eventos personalizados com a Grade de Eventos do Azure

Grade de eventos do Azure é um serviço de eventos para a nuvem de saudação. Neste artigo, use Olá CLI do Azure toocreate um tópico personalizado, assinar toohello tópico e disparar o resultado de Olá Olá evento tooview. Normalmente, você envia o ponto de extremidade de tooan de eventos que responde a eventos toohello, por exemplo, um webhook ou uma função do Azure. No entanto, toosimplify este artigo, enviar Olá eventos tooa URL que coleta apenas mensagens de saudação. Você cria essa URL usando uma ferramenta de terceiros de software livre chamada [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** é uma ferramenta de software livre que não se destina ao uso com altas taxas de transferência. Olá uso ferramenta Olá aqui é meramente demonstração. Se você enviar mais de um evento por vez, talvez você não veja todos os eventos na ferramenta de saudação.

Quando tiver terminado, você verá que os dados de evento Olá foi enviados tooan de ponto de extremidade.

![Dados de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este artigo requer que você está executando a versão mais recente de saudação do CLI do Azure (2.0.14 ou posterior). versão de hello toofind, execute `az --version`. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Os tópicos de Grade de Eventos são recursos do Azure e devem ser colocados em um grupo de recursos do Azure. grupo de recursos de saudação é uma coleção lógica na qual Azure recursos são implantados e gerenciados.

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. 

Olá, exemplo a seguir cria um grupo de recursos denominado *gridResourceGroup* em Olá *westus2* local.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Criar um tópico personalizado

Um tópico fornece um ponto de extremidade definido pelo usuário aonde você posta seus eventos. Olá exemplo a seguir cria Olá tópico no seu grupo de recursos. Substitua `<topic_name>` por um nome exclusivo para o tópico. nome do tópico Olá deve ser exclusivo, porque ele é representado por uma entrada de DNS. Versão de visualização hello, oferece suporte a grade de eventos **westus2** e **westcentralus** locais.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Criar um ponto de extremidade de mensagem

Antes de assinar toohello tópico, vamos criar o ponto de extremidade Olá para mensagem de saudação do evento. Em vez de gravar eventos do código toorespond toohello, vamos criar um ponto de extremidade que coleta mensagens de saudação, portanto, você pode exibi-los. RequestBin é um software livre, ferramenta de terceiros que permite que você toocreate um ponto de extremidade e exibir as solicitações enviadas tooit. Vá muito[RequestBin](https://requestb.in/)e clique em **criar um RequestBin**.  Copie Olá bin URL, porque é necessário ao assinar toohello tópico.

## <a name="subscribe-tooa-topic"></a>Assinar tooa tópico

Assinar tooa tópico tootell grade de eventos quais eventos você deseja tootrack. Olá, exemplo a seguir assina toohello tópico criado e passa a URL de saudação do RequestBin como ponto de extremidade Olá para notificação de eventos. Substituir `<event_subscription_name>` com um nome exclusivo para a sua assinatura, e `<URL_from_RequestBin>` com valor de saudação da saudação anterior seção. Especificando um ponto de extremidade ao inscrever-se, grade de eventos manipula Olá roteamento do ponto de extremidade de toothat de eventos. Para `<topic_name>`, usar valor Olá criado anteriormente. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Enviar um tópico do evento tooyour

Agora, vamos disparar um evento toosee como grade de eventos distribui o ponto de extremidade do hello mensagem tooyour. Primeiro, vamos obter Olá URL e a chave de tópico de saudação. Novamente, use o nome do tópico em `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify neste artigo, configuramos o tópico do exemplo evento dados toosend toohello. Normalmente, um aplicativo ou serviço do Azure envia dados de evento de saudação. saudação de exemplo a seguir obtém dados de evento de saudação:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Se você `echo "$body"` você pode ver eventos hello. Olá `data` elemento Olá JSON é a carga de saudação do evento. Qualquer JSON bem formado pode ficar nesse campo. Você também pode usar o campo de assunto Olá para roteamento e filtragem avançadas.

CURL é um utilitário que executa solicitações HTTP. Neste artigo, usamos o tópico de tooour ONDULAÇÃO toosend Olá evento. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Você tem disparou o evento de saudação e grade de eventos enviados Olá mensagem toohello ponto de extremidade configurado ao inscrever-se. Procure toohello RequestBin URL que você criou anteriormente. Ou clique em Atualizar no navegador do RequestBin aberto. Você verá o evento de saudação que acabou de ser enviado. 

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
Se você planejar toocontinue trabalhar com esse evento, faça não limpar os recursos de saudação criados neste artigo. Se você não planeja toocontinue, use Olá recursos de saudação do comando toodelete criado neste artigo a seguir.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Agora que você sabe como toocreate tópicos e assinaturas de evento, saiba mais sobre a grade de eventos que pode ajudá-lo:

- [Sobre a Grade de Eventos](overview.md)
- [Monitorar alterações de máquina virtual com a Grade de Eventos do Azure e os Aplicativos Lógicos](monitor-virtual-machine-changes-event-grid-logic-app.md)
