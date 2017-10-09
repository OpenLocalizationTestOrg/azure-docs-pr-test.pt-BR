---
title: "aaaAzure instâncias de contêiner - multi-contêiner grupo | Documentos do Azure"
description: "Instâncias de Contêiner do Azure – grupo de vários contêineres"
services: container-instances
documentationcenter: 
author: neilpeterson
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="08ccc-103">Implantar um grupo de contêineres</span><span class="sxs-lookup"><span data-stu-id="08ccc-103">Deploy a container group</span></span>

<span data-ttu-id="08ccc-104">Instâncias de contêiner do Azure dar suporte a implantação de saudação de vários contêineres em um único host utilizando um *grupo contêiner*.</span><span class="sxs-lookup"><span data-stu-id="08ccc-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="08ccc-105">Isso é útil ao criar um aplicativo secundário para registro em log, monitoramento ou qualquer outra configuração em que um serviço precise de um segundo processo anexado.</span><span class="sxs-lookup"><span data-stu-id="08ccc-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="08ccc-106">Este documento explica passo a passo como executar uma configuração de sidecar simples de vários contêineres usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08ccc-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="08ccc-107">Configurar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="08ccc-107">Configure hello template</span></span>

<span data-ttu-id="08ccc-108">Crie um arquivo chamado `azuredeploy.json` e Olá cópia json a seguir para ele.</span><span class="sxs-lookup"><span data-stu-id="08ccc-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="08ccc-109">Neste exemplo, é definido um grupo de contêineres com dois contêineres e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="08ccc-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="08ccc-110">primeiro o contêiner do grupo Olá Olá executa um aplicativo voltado para o público da internet.</span><span class="sxs-lookup"><span data-stu-id="08ccc-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="08ccc-111">Olá segundo contêiner secundários Olá, torna um aplicativo de web principal de toohello de solicitação HTTP via rede local do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="08ccc-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="08ccc-112">Este exemplo secundários pode ser expandido tootrigger um alerta se ele recebeu um código de resposta HTTP diferente de 200 Okey.</span><span class="sxs-lookup"><span data-stu-id="08ccc-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="08ccc-113">toouse um registro de imagem de contêiner privado, adicionar um documento de json do objeto toohello com hello formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="08ccc-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="08ccc-114">Implante o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="08ccc-114">Deploy hello template</span></span>

<span data-ttu-id="08ccc-115">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="08ccc-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="08ccc-116">Implante o modelo de saudação com hello [criar implantação de grupo az](/cli/azure/group/deployment#create) comando.</span><span class="sxs-lookup"><span data-stu-id="08ccc-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="08ccc-117">Em alguns segundos, você receberá uma resposta inicial do Azure.</span><span class="sxs-lookup"><span data-stu-id="08ccc-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="08ccc-118">Exibir estado da implantação</span><span class="sxs-lookup"><span data-stu-id="08ccc-118">View deployment state</span></span>

<span data-ttu-id="08ccc-119">estado de saudação tooview de implantação hello, use Olá `az container show` comando.</span><span class="sxs-lookup"><span data-stu-id="08ccc-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="08ccc-120">Isso retorna o endereço IP público Olá provisionado pela qual Olá aplicativo pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="08ccc-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="08ccc-121">Saída:</span><span class="sxs-lookup"><span data-stu-id="08ccc-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="08ccc-122">Exibir logs</span><span class="sxs-lookup"><span data-stu-id="08ccc-122">View logs</span></span>   

<span data-ttu-id="08ccc-123">Exibir a saída de log de saudação de um contêiner usando Olá `az container logs` comando.</span><span class="sxs-lookup"><span data-stu-id="08ccc-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="08ccc-124">Olá `--container-name` argumento especifica o contêiner de saudação do qual toopull logs.</span><span class="sxs-lookup"><span data-stu-id="08ccc-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="08ccc-125">Neste exemplo, o primeiro contêiner de saudação é especificado.</span><span class="sxs-lookup"><span data-stu-id="08ccc-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="08ccc-126">Saída:</span><span class="sxs-lookup"><span data-stu-id="08ccc-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="08ccc-127">Olá toosee logs para o contêiner de carro lado hello, executar Olá mesmo comando nome do contêiner especificando Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="08ccc-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="08ccc-128">Saída:</span><span class="sxs-lookup"><span data-stu-id="08ccc-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="08ccc-129">Como você pode ver, secundários Olá periodicamente está fazendo um aplicativo de web principal de toohello de solicitação HTTP por meio de tooensure de rede local do grupo de saudação que ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="08ccc-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ccc-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08ccc-130">Next steps</span></span>

<span data-ttu-id="08ccc-131">Este documento coberto etapas Olá necessárias para implantar um multi-contêiner de instância de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="08ccc-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="08ccc-132">Para um tooend final que experiência de instâncias de contêiner do Azure, consulte o tutorial de instâncias de contêiner do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="08ccc-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="08ccc-133">[Tutorial de Instâncias de Contêiner do Azure]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="08ccc-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
