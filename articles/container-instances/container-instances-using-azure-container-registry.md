---
title: "aaaDeploy tooAzure instâncias de contêiner de saudação do registro de contêiner do Azure | Documentos do Azure"
description: "Implantar instâncias de contêiner de tooAzure de saudação do registro de contêiner do Azure"
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Implantar instâncias de contêiner de tooAzure de saudação do registro de contêiner do Azure

Olá registro de contêiner do Azure é um registro baseado no Azure, em particular, para imagens de contêiner do Docker. Este artigo aborda como imagens de contêiner toodeploy armazenados em Olá registro de contêiner do Azure tooAzure instâncias de contêiner.

## <a name="using-hello-azure-cli"></a>Usando Olá CLI do Azure

Olá CLI do Azure inclui comandos para criar e gerenciar contêineres em instâncias de contêiner do Azure. Se você especificar uma imagem privada na Olá `create` de comando, você também pode especificar Olá tooauthenticate de senha necessária de registro de imagem com o registro de contêiner de saudação.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Olá `create` comando também dá suporte à especificação de saudação `registry-login-server` e `registry-username`. No entanto, o servidor de logon de saudação de saudação do registro de contêiner do Azure é sempre *registryname*. nome de usuário padrão azurecr.io e hello é *registryname*, portanto, esses valores são inferidos do nome da imagem Olá se não é explicitamente fornecido.

## <a name="using-an-azure-resource-manager-template"></a>Usando um modelo do Azure Resource Manager

Você pode especificar propriedades de saudação do registro de contêiner do Azure em um modelo do Gerenciador de recursos do Azure, incluindo Olá `imageRegistryCredentials` propriedade na definição de grupo de contêiner hello:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid armazenar sua senha de registro de contêiner diretamente no modelo de hello, recomendamos que você armazená-lo como um segredo no [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) e referenciá-lo no modelo Olá Olá [integração nativa entre Olá Gerenciador de recursos do Azure e o Cofre de chaves](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Usando Olá portal do Azure

Se você mantiver as imagens de contêiner de saudação do registro de contêiner do Azure, você pode facilmente criar um contêiner em instâncias de contêiner do Azure usando Olá portal do Azure.

1. No portal do Azure de Olá, navegue tooyour registro de contêiner.

2. Escolha Repositórios.

    ![menu de registro de contêiner do Azure Olá Olá portal do Azure][acr-menu]

3. Escolha o repositório de saudação que você deseja toodeploy do.

4. Clique com botão direito marca Olá para imagem de contêiner Olá deseja toodeploy.

    ![Menu de contexto para iniciar o contêiner com Instâncias de Contêiner do Azure][acr-runinstance-contextmenu]

5. Insira um nome para o contêiner de saudação e um nome para o grupo de recursos de saudação. Você também pode alterar os valores padrão de saudação se desejar.

    ![Criar menu para Instâncias de Contêiner do Azure][acr-create-deeplink]

6. Após a conclusão da implantação Olá, você pode navegar toohello o grupo de contêiner de saudação notificações painel toofind seu endereço IP e outras propriedades.

    ![Exibição de detalhes de grupo de contêineres das Instâncias de Contêiner do Azure][aci-detailsview]

## <a name="next-steps"></a>Próximas etapas

Saiba como contêineres toobuild, enviá-las do registro de contêiner privado tooa e implantá-los em instâncias de contêiner tooAzure por [concluir Olá tutorial](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
