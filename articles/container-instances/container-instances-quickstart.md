---
title: "aaaCreate o primeiro contêiner de instâncias de contêiner do Azure | Documentos do Azure"
description: "Implantar e começar a trabalhar com as Instâncias de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Criar o primeiro contêiner nas Instâncias de Contêiner do Azure

Instâncias de contêiner do Azure torna fácil toocreate e gerenciar contêineres no Azure. Esse início rápido, você criar um contêiner no Azure e expô-lo toohello internet com um endereço IP público. Essa operação é concluída com um único comando. Em poucos segundos, você verá o seguinte em seu navegador:

![Os aplicativos implantados usando Instâncias de Contêiner do Azure são exibidos no navegador][aci-app-browser]

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.12 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

As Instâncias de Contêiner do Azure são recursos do Azure e devem ser colocadas em um grupo de recursos do Azure, um conjunto lógico no qual os recursos do Azure são implantados e gerenciados.

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Criar um contêiner

Você pode criar um contêiner fornecendo um nome, uma imagem do Docker e um grupo de recursos do Azure. Opcionalmente, você pode expor Olá contêiner toohello internet com um endereço IP público. Nesse caso, vamos usar um contêiner que hospeda um aplicativo Web muito simples escrito em [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Em alguns segundos, você deve obter uma solicitação de tooyour de resposta. Inicialmente, o contêiner Olá estará em um **criando** estado, mas ele deve começar em alguns segundos. Você pode verificar o status de saudação usando Olá `show` comando:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

Na parte inferior de saudação da saída de hello, você verá o estado de provisionamento do contêiner hello e seu endereço IP:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Depois que o contêiner de saudação move toohello **êxito** estado, você puder alcançá-lo no navegador hello usando o endereço IP hello fornecido. 

![Os aplicativos implantados usando Instâncias de Contêiner do Azure são exibidos no navegador][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Pull Olá contêiner logs

Você pode extrair os logs de saudação do contêiner de saudação criadas usando Olá `logs` comando:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Saída:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Excluir contêiner Olá

Quando tiver terminado com contêiner hello, você poderá removê-lo usando Olá `delete` comando:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Todos os de saudação de código para o contêiner de saudação usado nesse início rápido está disponível [no GitHub][app-github-repo], juntamente com seu Dockerfile. Se você desejar tootry compilá-lo e implantá-la tooAzure instâncias de contêiner usando Olá registro de contêiner do Azure, continue toohello tutorial de instâncias de contêiner do Azure.

> [!div class="nextstepaction"]
> [Tutoriais sobre Instâncias de Contêiner do Azure](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png