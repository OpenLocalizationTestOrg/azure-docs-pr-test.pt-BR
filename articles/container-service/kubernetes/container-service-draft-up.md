---
title: "aaaUse rascunho com o serviço de contêiner do Azure e o registro de contêiner do Azure | Microsoft Docs"
description: "Crie um cluster ACS Kubernetes e um registro de contêiner do Azure toocreate seu primeiro aplicativo no Azure com o rascunho."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, Contêineres, microsserviços, Kubernetes, Rascunho, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="ee1e3-104">Use rascunho com toobuild serviço de contêiner do Azure e o registro de contêiner do Azure e implantar um aplicativo tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="ee1e3-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="ee1e3-105">[Rascunho](https://aka.ms/draft) é uma nova ferramenta de código-fonte aberto que torna mais fácil toodevelop com base em contêiner aplicativos e implantá-las tooKubernetes clusters sem saber muito sobre o Docker e Kubernetes – ou até mesmo instalá-los.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="ee1e3-106">Usando ferramentas como o rascunho permitem que você e seu foco equipes compilar o aplicativo hello com Kubernetes, não pagar tooinfrastructure tanta atenção.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="ee1e3-107">Você pode usar o Rascunho com qualquer registro de imagem do Docker e qualquer cluster Kubernetes, incluindo os locais.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="ee1e3-108">Este tutorial mostra como toouse ACS com toocreate Kubernetes ACR e DNS do Azure ao vivo desenvolvedor CI/CD pipeline usando o rascunho.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="ee1e3-109">Criar um Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ee1e3-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="ee1e3-110">Você pode facilmente [criar um novo registro de contêiner do Azure](../../container-registry/container-registry-get-started-azure-cli.md), mas Olá etapas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="ee1e3-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="ee1e3-111">Crie um toomanage do grupo de recursos do Azure ACR do registro e hello Kubernetes cluster no ACS.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="ee1e3-112">Criar um registro de imagem ACR usando [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="ee1e3-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="ee1e3-113">Criar um Serviço de Contêiner do Azure com Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ee1e3-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="ee1e3-114">Agora você está pronto toouse [az acs criar](/cli/azure/acs#create) toocreate um ACS cluster usando Kubernetes Olá `--orchestrator-type` valor.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="ee1e3-115">Como Kubernetes não é um tipo de orchestrator saudação padrão, certifique-se de usar o hello `--orchestrator-type kubernetes` alternar.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="ee1e3-116">saída de Hello quando tem êxito pesquisa a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="ee1e3-117">Agora que você tem um cluster, você pode importar as credenciais de saudação usando Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="ee1e3-118">Agora você tem um arquivo de configuração local para seu cluster, o que é que o comando e rascunho precisam tooget seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="ee1e3-119">Instalar e configurar o Rascunho</span><span class="sxs-lookup"><span data-stu-id="ee1e3-119">Install and configure draft</span></span>
<span data-ttu-id="ee1e3-120">instruções de instalação Olá rascunho estão em Olá [repositório rascunho](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="ee1e3-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="ee1e3-121">Eles são relativamente simples, mas exige alguma configuração, pois ele depende [comando](https://aka.ms/helm) toocreate e implantar um gráfico de comando no cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="ee1e3-122">[Baixe e instale o Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="ee1e3-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="ee1e3-123">Use o comando toosearch para e instale `stable/traefik`e o ingresso controlador tooenable as solicitações para as compilações de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="ee1e3-124">Definir agora um observador Olá `ingress` controlador toocapture Olá IP valor externo quando ele é implantado.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="ee1e3-125">Esse endereço IP será Olá um [mapear domínio de implantação tooyour](#wire-up-deployment-domain) na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="ee1e3-126">Nesse caso, Olá IP externo para o domínio de implantação de saudação é `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="ee1e3-127">Agora você pode mapear o IP de toothat do domínio.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="ee1e3-128">Configurar domínio de implantação</span><span class="sxs-lookup"><span data-stu-id="ee1e3-128">Wire up deployment domain</span></span>

<span data-ttu-id="ee1e3-129">O Rascunho cria uma versão para cada gráfico do Helm criado, ou seja, cada aplicativo em que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="ee1e3-130">Cada um obtém um nome gerado que é usado pelo rascunho como um _subdomínio_ sobre raiz Olá _domínio implantação_ que você controle.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="ee1e3-131">(Neste exemplo, usamos `squillace.io` como domínio de implantação hello.) tooenable esse comportamento de subdomínio, você deve criar um registro a para `'*'` em suas entradas DNS para o domínio de implantação, para que cada gerado subdomínio é roteado toohello Kubernetes controlador de entrada do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="ee1e3-132">Seu próprio provedor de domínio tem seus próprios servidores DNS de tooassign de maneira; muito[delegar tooAzure de nameservers seu domínio DNS](../../dns/dns-delegate-domain-azure-dns.md), levar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee1e3-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="ee1e3-133">Crie um grupo de recursos para a zona.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="ee1e3-134">Crie uma zona DNS para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="ee1e3-135">Saudação de uso [zona de dns de rede az criar](/cli/azure/network/dns/zone#create) comando tooobtain Olá nameservers toodelegate DNS controlar tooAzure DNS para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="ee1e3-136">Adicione servidores DNS Olá que recebem toohello provedor de domínio para seu domínio de implantação, que permite que o toorepoint DNS do Azure toouse seu domínio conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="ee1e3-137">Crie uma entrada de conjunto de registros A para seu toohello de mapeamento de domínio de implantação `ingress` IP da etapa 2 da seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="ee1e3-138">saída de Hello parecida com:</span><span class="sxs-lookup"><span data-stu-id="ee1e3-138">hello output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="ee1e3-139">Configurar o registro de rascunho toouse e criar subdomínios para cada gráfico de comando, que ele cria.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="ee1e3-140">tooconfigure rascunho, você precisa:</span><span class="sxs-lookup"><span data-stu-id="ee1e3-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="ee1e3-141">do nome do Registro de Contêiner do Azure (neste exemplo, `draft`)</span><span class="sxs-lookup"><span data-stu-id="ee1e3-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="ee1e3-142">da chave do registro, ou senha, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="ee1e3-143">domínio de implantação do Hello raiz que você tenha configurado toomap toohello Kubernetes entrada endereço IP externo (aqui, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="ee1e3-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="ee1e3-144">Chamar `draft init` e o processo de configuração de saudação solicitará Olá valores acima.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="ee1e3-145">processo de saudação parece algo seguinte Olá Olá primeira vez você executá-lo.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-145">hello process looks something like hello following hello first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="ee1e3-146">Agora você está pronto toodeploy um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="ee1e3-147">Criar e implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee1e3-147">Build and deploy an application</span></span>

<span data-ttu-id="ee1e3-148">No repositório de rascunho Olá são [seis aplicativos de exemplo simples](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="ee1e3-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="ee1e3-149">Clone o repositório de saudação e vamos usar Olá [exemplo Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="ee1e3-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="ee1e3-150">Alterar para o diretório de exemplos/Python hello e digite `draft create` toobuild aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="ee1e3-151">Deve se parecer com o exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="ee1e3-152">saída de Hello inclui um Dockerfile e um gráfico de comando.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="ee1e3-153">toobuild e implantar, basta digitar `draft up`.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="ee1e3-154">saída de Hello é abrangente, mas começa como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-154">hello output is extensive, but begins like hello following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="ee1e3-155">e quando termina com êxito com algo parecido toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="ee1e3-156">O nome do gráfico é, agora você pode `curl http://gangly-bronco.squillace.io` tooreceive resposta do hello, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee1e3-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee1e3-157">Next steps</span></span>

<span data-ttu-id="ee1e3-158">Agora que você tem um cluster ACS Kubernetes, você pode investigar o uso de [registro de contêiner do Azure](../../container-registry/container-registry-intro.md) toocreate implantações mais e diferentes deste cenário.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="ee1e3-159">Por exemplo, você pode criar um conjunto de registro DNS de domínio de rascunho _basedomain.toplevel_ que controla coisas de um subdomínio mais profundo para implantações específicas do ACS.</span><span class="sxs-lookup"><span data-stu-id="ee1e3-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






