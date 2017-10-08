---
title: "registro de contêiner de Docker particular do aaaCreate - CLI do Azure | Microsoft Docs"
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello 2.0 do CLI do Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Criar um registro de contêiner do Docker privado usando Olá 2.0 do CLI do Azure
Usar os comandos Olá [2.0 do CLI do Azure](https://github.com/Azure/azure-cli) toocreate um registro de contêiner e gerenciar as configurações do seu computador Linux, Mac ou Windows. Você também pode criar e gerenciar registros de contêiner usando Olá [portal do Azure](container-registry-get-started-portal.md) ou programaticamente com hello registro de contêiner [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md)
* Para obter ajuda sobre comandos do contêiner do registro (`az acr` comandos), passar Olá `-h` comando de tooany do parâmetro.


## <a name="prerequisites"></a>Pré-requisitos
* **2.0 do CLI do Azure**: tooinstall e começar com hello CLI 2.0, consulte Olá [instruções de instalação](/cli/azure/install-azure-cli). Faça logon no tooyour assinatura do Azure executando `az login`. Para obter mais informações, consulte [começar com hello CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Grupo de recursos**: crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de criar um registro de contêiner ou usar um grupo de recursos existente. Verifique se o grupo de recursos hello está em um local onde está o serviço de registro de contêiner de saudação [disponível](https://azure.microsoft.com/regions/services/). toocreate um grupo de recursos usando Olá CLI 2.0, consulte [Olá referência CLI 2.0](/cli/azure/group).
* **Conta de armazenamento** (opcional): criar um padrão Azure [conta de armazenamento](../storage/common/storage-introduction.md) tooback registro de contêiner de saudação em Olá mesmo local. Se você não especificar uma conta de armazenamento ao criar um registro com `az acr create`, comando Olá criará um para você. toocreate um armazenamento de conta usando Olá CLI 2.0, consulte [Olá referência CLI 2.0](/cli/azure/storage/account). Atualmente, não há suporte para o Armazenamento Premium.
* **Entidade de serviço** (opcional): quando você cria um registro com hello CLI, por padrão ele não é configurado para acesso. Dependendo de suas necessidades, você pode atribuir um registro de tooa principal de serviço existente do Active Directory do Azure (ou criar e atribuir um novo), ou habilite a conta de usuário admin do registro hello. Consulte as seções Olá posteriormente neste artigo. Para obter mais informações sobre o acesso de registro, consulte [autenticar com o registro de contêiner Olá](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Criar um registro de contêiner
Executar Olá `az acr create` comando toocreate um registro de contêiner.

> [!TIP]
> Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números. nome do registro de saudação nos exemplos de saudação é `myRegistry1`, mas substitua um nome exclusivo.
>
>

Olá usa Olá registro de contêiner toocreate mínimo de parâmetros de comando a seguir `myRegistry1` no grupo de recursos de saudação `myResourceGroup`e usando Olá *básica* sku:

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` é opcional. Se não for especificado, uma conta de armazenamento é criada com um nome que consiste do nome do registro de saudação e um carimbo de hora Olá especificado o grupo de recursos.

Quando Olá registro é criado, a saída de hello é a seguir toohello semelhante:

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Observe particularmente:

* `id`-Identificador para registro de saudação em sua assinatura, que é necessário se você quiser tooassign uma entidade de serviço.
* `loginServer`-nome totalmente qualificado de saudação especificado muito[toohello registro de log](container-registry-authentication.md). Neste exemplo, o nome de saudação é `myregistry1.exp.azurecr.io` (todas as minúsculas).

## <a name="assign-a-service-principal"></a>Atribuir uma entidade de serviço
Use comandos de CLI 2.0 tooassign um registro de tooa principal de serviço do Active Directory do Azure. Hello entidade de serviço nesses exemplos é designada como Olá proprietário, mas você pode atribuir [outras funções](../active-directory/role-based-access-control-configure.md) se desejar.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Criar uma entidade de serviço e atribuir toohello acessar o registro
Olá comando a seguir, uma nova entidade de serviço é atribuída identificador de registro de toohello do proprietário função acesso passado com hello `--scopes` parâmetro. Especifique uma senha forte com hello `--password` parâmetro.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Atribuir uma entidade de serviço existente
Se você já tiver uma entidade de serviço e deseja tooassign-proprietário função acessar toohello o registro, execute um toohello semelhante do comando exemplo a seguir. Passar o ID do aplicativo principal de serviço hello usando Olá `--assignee` parâmetro:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Gerenciar credenciais de administrador
Uma conta de administrador é automaticamente criada para cada registro de contêiner e é desabilitada por padrão. Olá a seguir mostram exemplos `az acr` CLI comandos toomanage credenciais de administrador Olá para o registro de contêiner.

### <a name="obtain-admin-user-credentials"></a>Obter credenciais de usuário administrador
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Habilitar o usuário administrador para um registro existente
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Desabilitar o usuário administrador para um registro existente
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Listar imagens e marcas
Saudação de uso `az acr` CLI comandos de imagens de saudação tooquery marcas em um repositório.

> [!NOTE]
> Atualmente, registro de contêiner não dá suporte a saudação `docker search` tooquery de comando para imagens e marcas.


### <a name="list-repositories"></a>Listar repositórios
Olá, exemplo a seguir lista os repositórios de saudação em um registro, no formato JSON (JavaScript Object Notation):

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Listar marcas
Olá, exemplo a seguir lista as marcas de Olá Olá **exemplos/nginx** repositório, no formato JSON:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Próximas etapas
* [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
