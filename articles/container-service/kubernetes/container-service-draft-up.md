---
title: "Usar Rascunho com o Serviço de Contêiner do Azure e Registro de Contêiner do Azure | Microsoft Docs"
description: "Crie um cluster Kubernetes ACS e um Registro de Contêiner do Azure para criar seu primeiro aplicativo no Azure com o Rascunho."
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="b588b-104">Use o Rascunho com o Serviço de Contêiner do Azure e o Registro de Contêiner do Azure para criar e implantar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b588b-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="b588b-105">[Rascunho](https://aka.ms/draft) é uma nova ferramenta de software livre que facilita o desenvolvimento de aplicativos baseados em contêiner e a implantação em clusters Kubernetes sem saber muito sobre Docker e Kubernetes, ou até mesmo sem instalá-los.</span><span class="sxs-lookup"><span data-stu-id="b588b-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="b588b-106">O uso de ferramentas como o Rascunho permite que você e sua equipe se concentrem na criação do aplicativo com Kubernetes sem prestar muita atenção à infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="b588b-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="b588b-107">Você pode usar o Rascunho com qualquer registro de imagem do Docker e qualquer cluster Kubernetes, incluindo os locais.</span><span class="sxs-lookup"><span data-stu-id="b588b-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="b588b-108">Este tutorial mostra como usar o ACS com Kubernetes, ACR e DNS do Azure para criar um pipeline de desenvolvedor CI/CD ativo usando o Rascunho.</span><span class="sxs-lookup"><span data-stu-id="b588b-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="b588b-109">Criar um Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b588b-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="b588b-110">Você pode [criar um novo Registro de Contêiner do Azure](../../container-registry/container-registry-get-started-azure-cli.md) facilmente, mas as etapas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="b588b-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="b588b-111">Crie um grupo de recursos do Azure para gerenciar o registro ACR e o cluster Kubernetes no ACS.</span><span class="sxs-lookup"><span data-stu-id="b588b-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="b588b-112">Criar um registro de imagem ACR usando [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="b588b-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="b588b-113">Criar um Serviço de Contêiner do Azure com Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b588b-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="b588b-114">Agora você está pronto para usar [az acs create](/cli/azure/acs#create) a fim de criar um cluster ACS usando Kubernetes como o valor `--orchestrator-type`.</span><span class="sxs-lookup"><span data-stu-id="b588b-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="b588b-115">Como Kubernetes não é o tipo de orquestrador padrão, use a opção `--orchestrator-type kubernetes`.</span><span class="sxs-lookup"><span data-stu-id="b588b-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="b588b-116">A saída, quando bem-sucedida, fica mais ou menos assim.</span><span class="sxs-lookup"><span data-stu-id="b588b-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="b588b-117">Agora que você tem um cluster, pode importar as credenciais usando o comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="b588b-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="b588b-118">Agora você tem um arquivo de configuração local para seu cluster, que é que o Helm e o Rascunho precisam para concluir o trabalho.</span><span class="sxs-lookup"><span data-stu-id="b588b-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="b588b-119">Instalar e configurar o Rascunho</span><span class="sxs-lookup"><span data-stu-id="b588b-119">Install and configure draft</span></span>
<span data-ttu-id="b588b-120">As instruções de instalação do Rascunho estão no [repositório do Rascunho](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="b588b-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="b588b-121">Elas são relativamente simples, mas exigem alguma configuração, pois ela depende do [Helm](https://aka.ms/helm) para criar e implantar um gráfico Helm no cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b588b-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="b588b-122">[Baixe e instale o Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="b588b-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="b588b-123">Use o Helm para procurar e instalar `stable/traefik` e o controlador de entrada para permitir solicitações de entrada para as builds.</span><span class="sxs-lookup"><span data-stu-id="b588b-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="b588b-124">Agora, defina um observador no controlador `ingress` para capturar o valor de IP externo quando for implantado.</span><span class="sxs-lookup"><span data-stu-id="b588b-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="b588b-125">Esse endereço IP será o que é [mapeado para seu domínio de implantação](#wire-up-deployment-domain) na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="b588b-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="b588b-126">Neste caso, o IP externo para o domínio de implantação é `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="b588b-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="b588b-127">Agora, você pode mapear seu domínio para esse IP.</span><span class="sxs-lookup"><span data-stu-id="b588b-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="b588b-128">Configurar domínio de implantação</span><span class="sxs-lookup"><span data-stu-id="b588b-128">Wire up deployment domain</span></span>

<span data-ttu-id="b588b-129">O Rascunho cria uma versão para cada gráfico do Helm criado, ou seja, cada aplicativo em que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="b588b-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="b588b-130">Cada um obtém um nome gerado que é usado pelo Rascunho como um _subdomínio_ acima do _domínio de implantação_ raiz que você controla.</span><span class="sxs-lookup"><span data-stu-id="b588b-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="b588b-131">(Neste exemplo, usamos `squillace.io` como o domínio de implantação.) Para habilitar esse comportamento de subdomínio, você deve criar um registro a para `'*'` nas entradas DNS do seu domínio de implantação, para que cada subdomínio gerado seja roteado para o controlador de entrada do cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b588b-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="b588b-132">Seu próprio provedor de domínio tem sua própria maneira de atribuir servidores DNS: para [delegar nameservers para seu domínio DNS do Azure](../../dns/dns-delegate-domain-azure-dns.md), execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b588b-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="b588b-133">Crie um grupo de recursos para a zona.</span><span class="sxs-lookup"><span data-stu-id="b588b-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="b588b-134">Crie uma zona DNS para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="b588b-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="b588b-135">Use o comando [az network dns zone create](/cli/azure/network/dns/zone#create) para obter os nameservers e delegar o controle DNS para o DNS do Azure em relação ao seu domínio.</span><span class="sxs-lookup"><span data-stu-id="b588b-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="b588b-136">Adicione os servidores DNS recebidos ao provedor de domínio do seu domínio de implantação, o que permite que você use o DNS do Azure para realinhar seu domínio da maneira desejada.</span><span class="sxs-lookup"><span data-stu-id="b588b-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="b588b-137">Crie uma entrada de conjunto de registros A para o mapeamento do domínio de implantação para o IP `ingress` da etapa 2 da seção anterior.</span><span class="sxs-lookup"><span data-stu-id="b588b-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="b588b-138">A saída se parece com:</span><span class="sxs-lookup"><span data-stu-id="b588b-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="b588b-139">Configure o Rascunho para usar seu registro e crie subdomínios para cada gráfico do Helm criado.</span><span class="sxs-lookup"><span data-stu-id="b588b-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="b588b-140">Para configurar o Rascunho, você precisará:</span><span class="sxs-lookup"><span data-stu-id="b588b-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="b588b-141">do nome do Registro de Contêiner do Azure (neste exemplo, `draft`)</span><span class="sxs-lookup"><span data-stu-id="b588b-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="b588b-142">da chave do registro, ou senha, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="b588b-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="b588b-143">do domínio raiz da implantação que você configurou para mapear para o endereço IP externo de entrada do Kubernetes (aqui, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="b588b-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="b588b-144">Chame `draft init` e o processo de configuração solicitará os valores acima.</span><span class="sxs-lookup"><span data-stu-id="b588b-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="b588b-145">O processo ficará mais ou menos assim na primeira vez que você executá-lo.</span><span class="sxs-lookup"><span data-stu-id="b588b-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="b588b-146">Agora você está pronto para implantar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b588b-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="b588b-147">Criar e implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="b588b-147">Build and deploy an application</span></span>

<span data-ttu-id="b588b-148">No repositório do Rascunho, existem [seis aplicativos de exemplo simples](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="b588b-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="b588b-149">Clone o repositório e vamos usar o [exemplo do Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="b588b-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="b588b-150">Mude para o diretório de exemplos/Python e digite `draft create` para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b588b-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="b588b-151">Ele deve ficar parecido com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b588b-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="b588b-152">A saída inclui um Dockerfile e um gráfico do Helm.</span><span class="sxs-lookup"><span data-stu-id="b588b-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="b588b-153">Para criar e implantar, basta digitar `draft up`.</span><span class="sxs-lookup"><span data-stu-id="b588b-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="b588b-154">A saída é abrangente, mas começa como o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b588b-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="b588b-155">e quando bem-sucedida, termina com algo semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b588b-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="b588b-156">Seja qual for o nome do gráfico, agora você pode `curl http://gangly-bronco.squillace.io` para receber a resposta `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="b588b-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b588b-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b588b-157">Next steps</span></span>

<span data-ttu-id="b588b-158">Agora que você tem um cluster ACS Kubernetes, pode investigar o uso do [Registro de Contêiner do Azure](../../container-registry/container-registry-intro.md) para criar outras implantações diferentes deste cenário.</span><span class="sxs-lookup"><span data-stu-id="b588b-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="b588b-159">Por exemplo, você pode criar um conjunto de registro DNS de domínio de rascunho _basedomain.toplevel_ que controla coisas de um subdomínio mais profundo para implantações específicas do ACS.</span><span class="sxs-lookup"><span data-stu-id="b588b-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






