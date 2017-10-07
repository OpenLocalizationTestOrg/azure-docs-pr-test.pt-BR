---
title: "aaaTroubleshooting instâncias de contêiner do Azure"
description: "Saiba como tootroubleshoot problemas com instâncias de contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="6314a-103">Solucionar problemas de implantação com as Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="6314a-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="6314a-104">Este artigo mostra como tootroubleshoot problemas ao implantar contêineres tooAzure instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="6314a-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="6314a-105">Ele também descreve alguns dos problemas comuns hello, que você pode encontrar.</span><span class="sxs-lookup"><span data-stu-id="6314a-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="6314a-106">Obtendo eventos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="6314a-106">Getting diagnostic events</span></span>

<span data-ttu-id="6314a-107">logs de tooview do seu código de aplicativo em um contêiner, você pode usar o hello [az contêiner logs](/cli/azure/container#logs) comando.</span><span class="sxs-lookup"><span data-stu-id="6314a-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="6314a-108">Mas se o contêiner não implantar com êxito, você precisa de informações de diagnóstico de saudação do tooreview fornecidas pelo provedor de recursos de instâncias de contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6314a-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="6314a-109">eventos de saudação tooview para seu contêiner, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6314a-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="6314a-110">saída de Hello inclui propriedades básicas de saudação do seu contêiner, juntamente com eventos de implantação:</span><span class="sxs-lookup"><span data-stu-id="6314a-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="6314a-111">Tarefas de implantação comuns</span><span class="sxs-lookup"><span data-stu-id="6314a-111">Common deployment issues</span></span>

<span data-ttu-id="6314a-112">Há alguns problemas comuns responsáveis pela maioria dos erros na implantação.</span><span class="sxs-lookup"><span data-stu-id="6314a-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="6314a-113">Não é possível toopull imagem</span><span class="sxs-lookup"><span data-stu-id="6314a-113">Unable toopull image</span></span>

<span data-ttu-id="6314a-114">Se instâncias de contêiner do Azure é não é possível toopull sua imagem inicialmente, ele tenta novamente por um período antes da falha eventualmente.</span><span class="sxs-lookup"><span data-stu-id="6314a-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="6314a-115">Se a imagem de saudação não pode ser extraída, eventos como Olá a seguir são mostrados:</span><span class="sxs-lookup"><span data-stu-id="6314a-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="6314a-116">tooresolve, excluir o contêiner de saudação e repita a sua implantação, pagante atenção se você digitou o nome de imagem Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="6314a-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="6314a-117">Contêiner sai e reinicia continuamente</span><span class="sxs-lookup"><span data-stu-id="6314a-117">Container continually exits and restarts</span></span>

<span data-ttu-id="6314a-118">Atualmente, o Instâncias de Contêiner do Azure dá suporte apenas a serviços de execução longa.</span><span class="sxs-lookup"><span data-stu-id="6314a-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="6314a-119">Se o contêiner executa toocompletion e fecha, ele automaticamente reinicia e executa novamente.</span><span class="sxs-lookup"><span data-stu-id="6314a-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="6314a-120">Se isso acontecer, eventos como os mostrados a seguir serão mostrados.</span><span class="sxs-lookup"><span data-stu-id="6314a-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="6314a-121">Observe o contêiner Olá for iniciada com êxito, em seguida, reinicia rapidamente.</span><span class="sxs-lookup"><span data-stu-id="6314a-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="6314a-122">Olá API de instâncias de contêiner inclui um `retryCount` reiniciou propriedade que mostra quantas vezes um contêiner específico.</span><span class="sxs-lookup"><span data-stu-id="6314a-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="6314a-123">A maioria das imagens de contêiner para as distribuições de Linux definido um shell, como bash, como o comando de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6314a-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="6314a-124">Já que um shell por si só não é um serviço de execução longa, esses contêineres saem imediatamente e entram em um loop de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="6314a-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="6314a-125">Contêiner leva um tempo longo toostart</span><span class="sxs-lookup"><span data-stu-id="6314a-125">Container takes a long time toostart</span></span>

<span data-ttu-id="6314a-126">Se o contêiner usa toostart um longo tempo, mas eventualmente tiver êxito, inicie examinando o tamanho de saudação da sua imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="6314a-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="6314a-127">Como instâncias de contêiner do Azure recebe sua imagem de contêiner sob demanda, terá de tempo de inicialização de saudação é tooits está diretamente relacionado tamanho.</span><span class="sxs-lookup"><span data-stu-id="6314a-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="6314a-128">Você pode exibir o tamanho de saudação da sua imagem de contêiner usando Olá CLI do Docker:</span><span class="sxs-lookup"><span data-stu-id="6314a-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="6314a-129">Saída:</span><span class="sxs-lookup"><span data-stu-id="6314a-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="6314a-130">tamanhos de imagem tookeeping chave Olá pequenos é garantir que sua imagem final não contém tudo o que não é necessário em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6314a-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="6314a-131">Uma maneira toodo com [compilações de vários estágios](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="6314a-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="6314a-132">Compilações de vários estágios tornam fácil tooensure que imagem final Olá contém somente artefatos de saudação é necessário para seu aplicativo e não os Olá extra de conteúdo que foi necessária no momento da compilação.</span><span class="sxs-lookup"><span data-stu-id="6314a-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="6314a-133">Hello, outros impacto maneira tooreduce Olá Olá pull de imagem em tempo de inicialização do contêiner é toohost imagem de contêiner de saudação usando Olá registro de contêiner do Azure no hello mesma região em que você pretende toouse instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6314a-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="6314a-134">Isso reduz o caminho de rede Olá Olá tootravel de necessidades de imagem de contêiner, reduzindo significativamente o tempo de download de saudação.</span><span class="sxs-lookup"><span data-stu-id="6314a-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
