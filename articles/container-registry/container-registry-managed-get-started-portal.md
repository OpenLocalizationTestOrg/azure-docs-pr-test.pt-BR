---
title: registro de Docker privado aaaCreate - portal do Azure | Microsoft Docs
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello portal do Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Criar um registro de contêiner gerenciado usando Olá portal do Azure

O Registro de Contêiner do Azure é um serviço de registro de contêiner Docker gerenciado usado para armazenar imagens de contêiner de Docker particulares. Esses detalhes de guia criando uma instância gerenciada do registro de contêiner do Azure usando Olá portal do Azure.

Os registros de contêiner gerenciados do Azure estão em versão prévia e não estão disponíveis em todas as regiões.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Faça logon em toohello portal do Azure em http://portal.azure.com.

## <a name="create-a-container-registry"></a>Criar um registro de contêiner

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Marketplace de saudação de pesquisa para **registro de contêiner do Azure** e selecioná-lo.

3. Clique em **criar** que abrirá a folha de criação de ACR hello.

    ![Configurações de registro de contêiner](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. Em Olá **registro de contêiner do Azure** folha, digite Olá informações a seguir. Clique em **Criar** quando terminar.

    a. **Nome do registro**: um nome de domínio de nível superior exclusivo para o registro específico. Neste exemplo, o nome de registro de saudação é *myAzureContainerRegistry1*, mas substitua um nome exclusivo. nome de saudação pode conter apenas letras e números.

    b. **Grupo de recursos**: selecione uma existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.

    c. **Local**: selecione um local de data center do Azure onde está o serviço Olá [disponível](https://azure.microsoft.com/regions/services/), como **Centro Sul dos EUA**.

    d. **O usuário administrador**: se desejar, habilite um registro de saudação de tooaccess de usuário admin. Você pode alterar essa configuração após a criação do registro de saudação.

    e. **Registro gerenciado Use**: selecione Sim toohave ACR automaticamente gerenciar armazenamento de registro hello, use webhooks e usar a autenticação do AAD.

    f. **Tipo de Preço**: selecione um tipo de preço, veja aqui os preços do ACR para saber mais.

## <a name="log-in-tooacr-instance"></a>Faça logon na instância de tooACR

Antes de enviar por push e pull imagens de contêiner, você deve fazer logon na instância ACR toohello. 

Assim, o toodo usar Olá 2.0 do CLI do Azure. Primeiro, se necessário, faça logon no Azure usando Olá [logon az](/cli/azure/#login) comando. 

```azurecli
az login
```

Em seguida, use Olá [logon de acr az](/cli/azure/acr#login) comando toolog em toohello do registro de contêiner do Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

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

Esse início rápido, você criou uma instância gerenciada do registro de contêiner do Azure usando Olá portal do Azure.

> [!div class="nextstepaction"]
> [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
