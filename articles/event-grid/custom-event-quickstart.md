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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="9f20d-103">Criar e encaminhar eventos personalizados com a Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="9f20d-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="9f20d-104">Grade de eventos do Azure é um serviço de eventos para a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f20d-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="9f20d-105">Neste artigo, use Olá CLI do Azure toocreate um tópico personalizado, assinar toohello tópico e disparar o resultado de Olá Olá evento tooview.</span><span class="sxs-lookup"><span data-stu-id="9f20d-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="9f20d-106">Normalmente, você envia o ponto de extremidade de tooan de eventos que responde a eventos toohello, por exemplo, um webhook ou uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f20d-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="9f20d-107">No entanto, toosimplify este artigo, enviar Olá eventos tooa URL que coleta apenas mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f20d-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="9f20d-108">Você cria essa URL usando uma ferramenta de terceiros de software livre chamada [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="9f20d-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="9f20d-109">**RequestBin** é uma ferramenta de software livre que não se destina ao uso com altas taxas de transferência.</span><span class="sxs-lookup"><span data-stu-id="9f20d-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="9f20d-110">Olá uso ferramenta Olá aqui é meramente demonstração.</span><span class="sxs-lookup"><span data-stu-id="9f20d-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="9f20d-111">Se você enviar mais de um evento por vez, talvez você não veja todos os eventos na ferramenta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f20d-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="9f20d-112">Quando tiver terminado, você verá que os dados de evento Olá foi enviados tooan de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9f20d-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Dados de evento](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9f20d-114">Se você escolher tooinstall e usa o hello CLI localmente, este artigo requer que você está executando a versão mais recente de saudação do CLI do Azure (2.0.14 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="9f20d-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="9f20d-115">versão de hello toofind, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9f20d-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="9f20d-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9f20d-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="9f20d-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9f20d-117">Create a resource group</span></span>

<span data-ttu-id="9f20d-118">Os tópicos de Grade de Eventos são recursos do Azure e devem ser colocados em um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f20d-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="9f20d-119">grupo de recursos de saudação é uma coleção lógica na qual Azure recursos são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f20d-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="9f20d-120">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9f20d-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="9f20d-121">Olá, exemplo a seguir cria um grupo de recursos denominado *gridResourceGroup* em Olá *westus2* local.</span><span class="sxs-lookup"><span data-stu-id="9f20d-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="9f20d-122">Criar um tópico personalizado</span><span class="sxs-lookup"><span data-stu-id="9f20d-122">Create a custom topic</span></span>

<span data-ttu-id="9f20d-123">Um tópico fornece um ponto de extremidade definido pelo usuário aonde você posta seus eventos.</span><span class="sxs-lookup"><span data-stu-id="9f20d-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="9f20d-124">Olá exemplo a seguir cria Olá tópico no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9f20d-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="9f20d-125">Substitua `<topic_name>` por um nome exclusivo para o tópico.</span><span class="sxs-lookup"><span data-stu-id="9f20d-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="9f20d-126">nome do tópico Olá deve ser exclusivo, porque ele é representado por uma entrada de DNS.</span><span class="sxs-lookup"><span data-stu-id="9f20d-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="9f20d-127">Versão de visualização hello, oferece suporte a grade de eventos **westus2** e **westcentralus** locais.</span><span class="sxs-lookup"><span data-stu-id="9f20d-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="9f20d-128">Criar um ponto de extremidade de mensagem</span><span class="sxs-lookup"><span data-stu-id="9f20d-128">Create a message endpoint</span></span>

<span data-ttu-id="9f20d-129">Antes de assinar toohello tópico, vamos criar o ponto de extremidade Olá para mensagem de saudação do evento.</span><span class="sxs-lookup"><span data-stu-id="9f20d-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="9f20d-130">Em vez de gravar eventos do código toorespond toohello, vamos criar um ponto de extremidade que coleta mensagens de saudação, portanto, você pode exibi-los.</span><span class="sxs-lookup"><span data-stu-id="9f20d-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="9f20d-131">RequestBin é um software livre, ferramenta de terceiros que permite que você toocreate um ponto de extremidade e exibir as solicitações enviadas tooit.</span><span class="sxs-lookup"><span data-stu-id="9f20d-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="9f20d-132">Vá muito[RequestBin](https://requestb.in/)e clique em **criar um RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="9f20d-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="9f20d-133">Copie Olá bin URL, porque é necessário ao assinar toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="9f20d-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="9f20d-134">Assinar tooa tópico</span><span class="sxs-lookup"><span data-stu-id="9f20d-134">Subscribe tooa topic</span></span>

<span data-ttu-id="9f20d-135">Assinar tooa tópico tootell grade de eventos quais eventos você deseja tootrack.</span><span class="sxs-lookup"><span data-stu-id="9f20d-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="9f20d-136">Olá, exemplo a seguir assina toohello tópico criado e passa a URL de saudação do RequestBin como ponto de extremidade Olá para notificação de eventos.</span><span class="sxs-lookup"><span data-stu-id="9f20d-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="9f20d-137">Substituir `<event_subscription_name>` com um nome exclusivo para a sua assinatura, e `<URL_from_RequestBin>` com valor de saudação da saudação anterior seção.</span><span class="sxs-lookup"><span data-stu-id="9f20d-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="9f20d-138">Especificando um ponto de extremidade ao inscrever-se, grade de eventos manipula Olá roteamento do ponto de extremidade de toothat de eventos.</span><span class="sxs-lookup"><span data-stu-id="9f20d-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="9f20d-139">Para `<topic_name>`, usar valor Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9f20d-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="9f20d-140">Enviar um tópico do evento tooyour</span><span class="sxs-lookup"><span data-stu-id="9f20d-140">Send an event tooyour topic</span></span>

<span data-ttu-id="9f20d-141">Agora, vamos disparar um evento toosee como grade de eventos distribui o ponto de extremidade do hello mensagem tooyour.</span><span class="sxs-lookup"><span data-stu-id="9f20d-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="9f20d-142">Primeiro, vamos obter Olá URL e a chave de tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f20d-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="9f20d-143">Novamente, use o nome do tópico em `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="9f20d-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="9f20d-144">toosimplify neste artigo, configuramos o tópico do exemplo evento dados toosend toohello.</span><span class="sxs-lookup"><span data-stu-id="9f20d-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="9f20d-145">Normalmente, um aplicativo ou serviço do Azure envia dados de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f20d-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="9f20d-146">saudação de exemplo a seguir obtém dados de evento de saudação:</span><span class="sxs-lookup"><span data-stu-id="9f20d-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="9f20d-147">Se você `echo "$body"` você pode ver eventos hello.</span><span class="sxs-lookup"><span data-stu-id="9f20d-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="9f20d-148">Olá `data` elemento Olá JSON é a carga de saudação do evento.</span><span class="sxs-lookup"><span data-stu-id="9f20d-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="9f20d-149">Qualquer JSON bem formado pode ficar nesse campo.</span><span class="sxs-lookup"><span data-stu-id="9f20d-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="9f20d-150">Você também pode usar o campo de assunto Olá para roteamento e filtragem avançadas.</span><span class="sxs-lookup"><span data-stu-id="9f20d-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="9f20d-151">CURL é um utilitário que executa solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f20d-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="9f20d-152">Neste artigo, usamos o tópico de tooour ONDULAÇÃO toosend Olá evento.</span><span class="sxs-lookup"><span data-stu-id="9f20d-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="9f20d-153">Você tem disparou o evento de saudação e grade de eventos enviados Olá mensagem toohello ponto de extremidade configurado ao inscrever-se.</span><span class="sxs-lookup"><span data-stu-id="9f20d-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="9f20d-154">Procure toohello RequestBin URL que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9f20d-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="9f20d-155">Ou clique em Atualizar no navegador do RequestBin aberto.</span><span class="sxs-lookup"><span data-stu-id="9f20d-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="9f20d-156">Você verá o evento de saudação que acabou de ser enviado.</span><span class="sxs-lookup"><span data-stu-id="9f20d-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="9f20d-157">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="9f20d-157">Clean up resources</span></span>
<span data-ttu-id="9f20d-158">Se você planejar toocontinue trabalhar com esse evento, faça não limpar os recursos de saudação criados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9f20d-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="9f20d-159">Se você não planeja toocontinue, use Olá recursos de saudação do comando toodelete criado neste artigo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9f20d-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9f20d-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f20d-160">Next steps</span></span>

<span data-ttu-id="9f20d-161">Agora que você sabe como toocreate tópicos e assinaturas de evento, saiba mais sobre a grade de eventos que pode ajudá-lo:</span><span class="sxs-lookup"><span data-stu-id="9f20d-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="9f20d-162">Sobre a Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="9f20d-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="9f20d-163">Monitorar alterações de máquina virtual com a Grade de Eventos do Azure e os Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="9f20d-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
