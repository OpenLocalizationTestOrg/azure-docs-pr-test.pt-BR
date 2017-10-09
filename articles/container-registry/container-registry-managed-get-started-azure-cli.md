---
title: "registro de contêiner de Docker particular do aaaCreate - CLI do Azure | Microsoft Docs"
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello 2.0 do CLI do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Criar um registro de contêiner gerenciado usando Olá CLI do Azure

O Registro de Contêiner do Azure é um serviço de registro de contêiner Docker gerenciado usado para armazenar imagens de contêiner de Docker particulares. Esses detalhes de guia criando uma instância gerenciada do registro de contêiner do Azure usando Olá CLI do Azure.

Os registros de contêiner gerenciados do Azure estão em versão prévia e não estão disponíveis em todas as regiões.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westcentralus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Criar um registro de contêiner

Criar uma instância ACR usando Olá [criar acr az](/cli/azure/acr#create) comando.

> [!NOTE]
> Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números.

 nome do registro de saudação no exemplo hello é *myContainerRegistry1*, substituir um nome exclusivo.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Quando Olá registro é criado, a saída de hello é a seguir toohello semelhante:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Faça logon na instância de tooACR

Antes de enviar por push e pull imagens de contêiner, você deve fazer logon na instância ACR toohello. toodo assim, use Olá [logon de acr az](/cli/azure/acr#login) comando.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.

## <a name="use-azure-container-registry"></a>Usar o Registro de Contêiner do Azure

### <a name="list-container-images"></a>Listar imagens de contêiner

Saudação de uso `az acr` CLI comandos de imagens de saudação tooquery marcas em um repositório.

> [!NOTE]
> Atualmente, registro de contêiner não dá suporte a saudação `docker search` tooquery de comando para imagens e marcas.

### <a name="list-repositories"></a>Listar repositórios

Olá, exemplo a seguir lista os repositórios de saudação em um registro, no formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Listar marcas

Olá, exemplo a seguir lista as marcas de Olá Olá **exemplos/nginx** repositório, no formato JSON:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Próximas etapas

Esse início rápido, você criou uma instância gerenciada do registro de contêiner do Azure usando Olá CLI do Azure.

> [!div class="nextstepaction"]
> [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
