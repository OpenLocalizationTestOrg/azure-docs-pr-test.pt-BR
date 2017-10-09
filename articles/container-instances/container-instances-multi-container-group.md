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
# <a name="deploy-a-container-group"></a>Implantar um grupo de contêineres

Instâncias de contêiner do Azure dar suporte a implantação de saudação de vários contêineres em um único host utilizando um *grupo contêiner*. Isso é útil ao criar um aplicativo secundário para registro em log, monitoramento ou qualquer outra configuração em que um serviço precise de um segundo processo anexado. 

Este documento explica passo a passo como executar uma configuração de sidecar simples de vários contêineres usando um modelo do Azure Resource Manager.

## <a name="configure-hello-template"></a>Configurar o modelo de saudação

Crie um arquivo chamado `azuredeploy.json` e Olá cópia json a seguir para ele. 

Neste exemplo, é definido um grupo de contêineres com dois contêineres e um endereço IP público. primeiro o contêiner do grupo Olá Olá executa um aplicativo voltado para o público da internet. Olá segundo contêiner secundários Olá, torna um aplicativo de web principal de toohello de solicitação HTTP via rede local do grupo de saudação. 

Este exemplo secundários pode ser expandido tootrigger um alerta se ele recebeu um código de resposta HTTP diferente de 200 Okey. 

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

toouse um registro de imagem de contêiner privado, adicionar um documento de json do objeto toohello com hello formato a seguir.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Implante o modelo de saudação

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Implante o modelo de saudação com hello [criar implantação de grupo az](/cli/azure/group/deployment#create) comando.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Em alguns segundos, você receberá uma resposta inicial do Azure. 

## <a name="view-deployment-state"></a>Exibir estado da implantação

estado de saudação tooview de implantação hello, use Olá `az container show` comando. Isso retorna o endereço IP público Olá provisionado pela qual Olá aplicativo pode ser acessado.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Saída:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Exibir logs   

Exibir a saída de log de saudação de um contêiner usando Olá `az container logs` comando. Olá `--container-name` argumento especifica o contêiner de saudação do qual toopull logs. Neste exemplo, o primeiro contêiner de saudação é especificado. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Saída:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

Olá toosee logs para o contêiner de carro lado hello, executar Olá mesmo comando nome do contêiner especificando Olá segundo.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Saída:

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

Como você pode ver, secundários Olá periodicamente está fazendo um aplicativo de web principal de toohello de solicitação HTTP por meio de tooensure de rede local do grupo de saudação que ele está em execução.

## <a name="next-steps"></a>Próximas etapas

Este documento coberto etapas Olá necessárias para implantar um multi-contêiner de instância de contêiner do Azure. Para um tooend final que experiência de instâncias de contêiner do Azure, consulte o tutorial de instâncias de contêiner do Azure de saudação.

> [!div class="nextstepaction"]
> [Tutorial de Instâncias de Contêiner do Azure]: ./container-instances-tutorial-prepare-app.md
