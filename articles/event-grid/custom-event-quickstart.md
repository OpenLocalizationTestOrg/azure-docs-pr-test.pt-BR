---
title: Eventos personalizados para a Grade de Eventos do Azure | Microsoft Docs
description: "Use a Grade de Eventos do Azure para publicar um tópico e assinar esse evento."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="11729-103">Criar e encaminhar eventos personalizados com a Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="11729-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="11729-104">A Grade de Eventos do Azure é um serviço de eventos para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="11729-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="11729-105">Neste artigo, você pode usar a CLI do Azure para criar um tópico personalizado, assinar o tópico e disparar o evento para exibir o resultado.</span><span class="sxs-lookup"><span data-stu-id="11729-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="11729-106">Normalmente, você envia eventos para um ponto de extremidade que responde ao evento, como um webhook ou uma Função do Azure.</span><span class="sxs-lookup"><span data-stu-id="11729-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="11729-107">No entanto, para simplificar este artigo, você envia os eventos para uma URL que apenas coleta as mensagens.</span><span class="sxs-lookup"><span data-stu-id="11729-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="11729-108">Você cria essa URL usando uma ferramenta de terceiros de software livre chamada [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="11729-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="11729-109">**RequestBin** é uma ferramenta de software livre que não se destina ao uso com altas taxas de transferência.</span><span class="sxs-lookup"><span data-stu-id="11729-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="11729-110">O uso da ferramenta aqui é meramente demonstrativo.</span><span class="sxs-lookup"><span data-stu-id="11729-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="11729-111">Se você efetuar push de mais de um evento por vez, talvez não veja todos os eventos na ferramenta.</span><span class="sxs-lookup"><span data-stu-id="11729-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="11729-112">Quando tiver concluído, você verá que os dados do evento foram enviados para um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="11729-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Dados de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="11729-114">Se você optar por instalar e usar a CLI localmente, este artigo exigirá que você esteja executando versão da CLI do Azure mais recente (2.0.14 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="11729-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="11729-115">Para saber qual é a versão, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="11729-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="11729-116">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="11729-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="11729-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="11729-117">Create a resource group</span></span>

<span data-ttu-id="11729-118">Os tópicos de Grade de Eventos são recursos do Azure e devem ser colocados em um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="11729-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="11729-119">O grupo de recursos do Azure é uma coleção lógica na qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="11729-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="11729-120">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="11729-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="11729-121">O exemplo a seguir cria um grupo de recursos chamado *gridResourceGroup* no local *westus2*.</span><span class="sxs-lookup"><span data-stu-id="11729-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="11729-122">Criar um tópico personalizado</span><span class="sxs-lookup"><span data-stu-id="11729-122">Create a custom topic</span></span>

<span data-ttu-id="11729-123">Um tópico fornece um ponto de extremidade definido pelo usuário aonde você posta seus eventos.</span><span class="sxs-lookup"><span data-stu-id="11729-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="11729-124">O exemplo a seguir o tópico no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="11729-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="11729-125">Substitua `<topic_name>` por um nome exclusivo para o tópico.</span><span class="sxs-lookup"><span data-stu-id="11729-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="11729-126">O nome do tópico deve ser exclusivo, pois é representado por uma entrada DNS.</span><span class="sxs-lookup"><span data-stu-id="11729-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="11729-127">Para a versão prévia, a Grade de Eventos dá suporte às localizações **westus2** e **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="11729-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="11729-128">Criar um ponto de extremidade de mensagem</span><span class="sxs-lookup"><span data-stu-id="11729-128">Create a message endpoint</span></span>

<span data-ttu-id="11729-129">Antes de assinar o tópico, vamos criar o ponto de extremidade para a mensagem do evento.</span><span class="sxs-lookup"><span data-stu-id="11729-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="11729-130">Em vez de escrever código para responder ao evento, vamos criar um ponto de extremidade que coleta as mensagens, para que você possa exibi-las.</span><span class="sxs-lookup"><span data-stu-id="11729-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="11729-131">O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele.</span><span class="sxs-lookup"><span data-stu-id="11729-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="11729-132">Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="11729-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="11729-133">Copie a URL do compartimento, pois você precisará dela para assinar o tópico.</span><span class="sxs-lookup"><span data-stu-id="11729-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="11729-134">Assinar um tópico</span><span class="sxs-lookup"><span data-stu-id="11729-134">Subscribe to a topic</span></span>

<span data-ttu-id="11729-135">Assine um tópico para indicar à Grade de Eventos quais eventos você deseja acompanhar. O exemplo a seguir assina o tópico que você criou e transmite a URL do RequestBin como o ponto de extremidade para notificação de eventos.</span><span class="sxs-lookup"><span data-stu-id="11729-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="11729-136">Substitua `<event_subscription_name>` por um nome exclusivo para a sua assinatura e `<URL_from_RequestBin>` pelo valor da seção anterior.</span><span class="sxs-lookup"><span data-stu-id="11729-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="11729-137">A especificação de um ponto de extremidade durante a assinatura faz com que a Grade de Eventos manipule o roteamento de eventos para esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="11729-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="11729-138">Em `<topic_name>`, use o valor que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="11729-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="11729-139">Enviar um evento para o tópico</span><span class="sxs-lookup"><span data-stu-id="11729-139">Send an event to your topic</span></span>

<span data-ttu-id="11729-140">Agora, vamos disparar um evento para ver como a Grade de Eventos distribui a mensagem para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="11729-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="11729-141">Primeiro, vamos obter a URL e a chave para o tópico.</span><span class="sxs-lookup"><span data-stu-id="11729-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="11729-142">Novamente, use o nome do tópico em `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="11729-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="11729-143">Para simplificar este artigo, configuramos dados de evento de exemplo para enviar ao tópico.</span><span class="sxs-lookup"><span data-stu-id="11729-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="11729-144">Normalmente, um aplicativo ou serviço do Azure enviaria os dados de evento.</span><span class="sxs-lookup"><span data-stu-id="11729-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="11729-145">O exemplo abaixo obtém os dados do evento:</span><span class="sxs-lookup"><span data-stu-id="11729-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="11729-146">Se você `echo "$body"`, pode ver o evento completo.</span><span class="sxs-lookup"><span data-stu-id="11729-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="11729-147">O elemento `data` do JSON é a carga do evento.</span><span class="sxs-lookup"><span data-stu-id="11729-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="11729-148">Qualquer JSON bem formado pode ficar nesse campo.</span><span class="sxs-lookup"><span data-stu-id="11729-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="11729-149">Você também pode usar o campo de assunto para roteamento e filtragem avançados.</span><span class="sxs-lookup"><span data-stu-id="11729-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="11729-150">CURL é um utilitário que executa solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="11729-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="11729-151">Neste artigo, usamos o CURL para enviar o evento ao nosso tópico.</span><span class="sxs-lookup"><span data-stu-id="11729-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="11729-152">Você disparou o evento e a Grade de Eventos enviou a mensagem para o ponto de extremidade configurado durante a assinatura.</span><span class="sxs-lookup"><span data-stu-id="11729-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="11729-153">Navegue até a URL do RequestBin que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="11729-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="11729-154">Ou clique em Atualizar no navegador do RequestBin aberto.</span><span class="sxs-lookup"><span data-stu-id="11729-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="11729-155">Você verá o evento que acabou de ser enviado.</span><span class="sxs-lookup"><span data-stu-id="11729-155">You see the event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="11729-156">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="11729-156">Clean up resources</span></span>
<span data-ttu-id="11729-157">Se você planeja continuar a trabalhar com esse evento, não limpe os recursos criados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="11729-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="11729-158">Caso contrário, use os comandos a seguir para excluir os recursos criados por você neste artigo.</span><span class="sxs-lookup"><span data-stu-id="11729-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="11729-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11729-159">Next steps</span></span>

<span data-ttu-id="11729-160">Agora que você sabe como criar tópicos e assinaturas de evento, saiba mais sobre como a Grade de Eventos pode ajudá-lo:</span><span class="sxs-lookup"><span data-stu-id="11729-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="11729-161">Sobre a Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="11729-161">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="11729-162">Monitorar alterações de máquina virtual com a Grade de Eventos do Azure e os Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="11729-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
