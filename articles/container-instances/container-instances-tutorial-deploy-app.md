---
title: "tutorial de instâncias de contêiner aaaAzure - implantar aplicativo | Microsoft Docs"
description: "Tutorial de Instâncias de Contêiner do Azure – implantar aplicativo"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Implantar um contêiner tooAzure instâncias de contêiner

Isso é hello última de um tutorial de três partes. Nas seções anteriores, [uma imagem de contêiner foi criada](container-instances-tutorial-prepare-app.md) e [enviada por push tooan registro de contêiner do Azure](container-instances-tutorial-prepare-acr.md). Esta seção conclui o tutorial Olá Implantando Olá contêiner tooAzure instâncias de contêiner. As etapas concluídas incluem:

> [!div class="checklist"]
> * Definição de um grupo de contêiner usando um modelo do Azure Resource Manager
> * Implantar grupo de contêiner hello usando Olá CLI do Azure
> * Exibição de logs de contêiner

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Implantar o contêiner de saudação usando Olá CLI do Azure

Olá CLI do Azure permite a implantação de um contêiner de tooAzure instâncias de contêiner em um único comando. Desde que a imagem de contêiner hello está hospedada no hello privada registro de contêiner do Azure, você deve incluir Olá credenciais necessário tooaccess-lo. Se necessário, você pode consultá-las conforme mostrado abaixo.

Servidor de logon do registro de contêiner (atualize com seu nome de registro):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Senha de registro de contêiner:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy sua imagem de contêiner do registro de contêiner de saudação com um recurso de solicitação de 1 núcleo de CPU e 1GB de memória, execute Olá comando a seguir:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

Em alguns segundos, você receberá uma resposta inicial do Azure Resource Manager. estado de saudação tooview de implantação hello, use:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Podemos continuar a execução desse comando até que o estado de saudação muda de *pendente* muito*executando*. Então, poderemos continuar.

## <a name="view-hello-application-and-container-logs"></a>Exibir logs de aplicativo e o contêiner de saudação

Depois que a implantação de saudação for bem-sucedida, abra seu endereço IP do navegador toohello mostrado na saída Olá Olá comando a seguir:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Olá mundo aplicativo no navegador Olá][aci-app-browser]

Você também pode exibir a saída do log de saudação do contêiner de saudação:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Saída:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você concluiu o processo de saudação de implantação de seu tooAzure contêineres instâncias de contêiner. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Implantando o contêiner de saudação do registro de contêiner do Azure usando o Olá Olá CLI do Azure
> * Exibindo o aplicativo hello no navegador Olá
> * Exibindo registros de contêiner de saudação

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
