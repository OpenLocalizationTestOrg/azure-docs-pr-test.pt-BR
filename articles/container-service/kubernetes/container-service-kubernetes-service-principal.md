---
title: aaaService principal para o cluster do Azure Kubernetes | Microsoft Docs
description: "Criar e gerenciar uma entidade de serviço do Azure Active Directory para um cluster Kubernetes no Serviço de Contêiner do Azure"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Configurar uma entidade de serviço do Azure AD para um cluster Kubernetes no contêiner de serviço


No serviço de contêiner do Azure, um cluster Kubernetes requer um [entidade de serviço do Active Directory do Azure](../../active-directory/develop/active-directory-application-objects.md) toointeract com APIs do Azure. Olá entidade de serviço é necessário toodynamically gerenciar recursos, como [rotas definidas pelo usuário](../../virtual-network/virtual-networks-udr-overview.md) e hello [balanceador de carga do Azure de 4 de camada](../../load-balancer/load-balancer-overview.md). 


Este artigo mostra diferentes opções tooset o serviço principal para o cluster Kubernetes. Por exemplo, se você instalou e configurar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2), você pode executar Olá [ `az acs create` ](/cli/azure/acs#create) saudação do comando toocreate Kubernetes no principal no hello de serviço de cluster e hello simultaneamente.


## <a name="requirements-for-hello-service-principal"></a>Requisitos para a entidade de serviço Olá

Você pode usar uma entidade de serviço do AD do Azure existente que atende Olá seguindo os requisitos ou crie um novo.

* **Escopo**: grupo de recursos de saudação na assinatura Olá usado cluster do toodeploy Olá Kubernetes ou (menos restrictively) assinatura Olá toodeploy cluster de saudação.

* **Função**: **Colaborador**

* **Segredo do cliente**: deve ser uma senha. Atualmente, é possível usar uma entidade de serviço configurada para autenticação de certificado.

> [!IMPORTANT] 
> toocreate uma entidade de serviço, você deve ter permissões tooregister um aplicativo com seu locatário do AD do Azure e sua função de tooa tooassign Olá aplicativo em sua assinatura. toosee se você tiver permissões de saudação necessária [check-in Olá Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Opção 1: criar uma entidade de serviço no Azure AD

Se você quiser toocreate uma entidade de serviço do AD do Azure antes de implantar o cluster Kubernetes, o Azure fornece vários métodos. 

Olá comandos de exemplo a seguir mostra como toodo com hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Você também pode criar uma entidade de serviço usando [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), Olá [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), ou outros métodos.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

O resultado é semelhante seguinte toohello (mostrados aqui redigida):

![Criar uma entidade de serviço](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Estão realçados Olá **ID do cliente** (`appId`) e hello **segredo do cliente** (`password`) que são usados como parâmetros de serviço principal para a implantação de cluster.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Especifique a entidade de serviço durante a criação de cluster de Kubernetes Olá

Fornecer Olá **ID do cliente** (também chamado de hello `appId`, para a ID de aplicativo) e **segredo do cliente** (`password`) de um serviço existente principal como parâmetros quando você cria Olá Cluster Kubernetes. Certifique-se de entidade de serviço Olá atende aos requisitos de saudação em hello a partir deste artigo.

Você pode especificar esses parâmetros durante a implantação de cluster de Kubernetes hello usando Olá [Azure Interface de linha de comando (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portal do Azure](../dcos-swarm/container-service-deployment.md), ou outros métodos.

>[!TIP] 
>Ao especificar Olá **ID do cliente**, ser Olá de toouse se `appId`, Olá não `ObjectId`, da entidade de serviço hello.
>

Hello exemplo a seguir mostra uma maneira toopass parâmetros Olá Olá 2.0 do CLI do Azure. Este exemplo usa Olá [Kubernetes quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Baixar](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) arquivo de parâmetros de modelo Olá `azuredeploy.parameters.json` do GitHub.

2. serviço de saudação toospecify principal, digite os valores para `servicePrincipalClientId` e `servicePrincipalClientSecret` no arquivo hello. (Você também precisa tooprovide seus próprios valores para `dnsNamePrefix` e `sshRSAPublicKey`. Olá último é cluster de Olá Olá SSH tooaccess de chave pública). Salve o arquivo hello.

    ![Passar parâmetros de entidade de serviço](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Olá executar comando a seguir, o uso de `--parameters` tooset Olá caminho toohello azuredeploy.parameters.json arquivo de. Esse comando implanta Olá em um grupo de recursos que você criar chamado `myResourceGroup` na região Oeste dos EUA de saudação.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Opção 2: Gerar uma entidade de serviço durante a criação de cluster Olá com`az acs create`

Se você executar Olá [ `az acs create` ](/cli/azure/acs#create) toocreate comando Olá Kubernetes cluster, você terá Olá opção toogenerate uma entidade de serviço automaticamente.

Como ocorre com outras opções de criação do cluster Kubernetes, você pode especificar parâmetros para uma entidade de serviço existente quando executa `az acs create`. No entanto, quando você omite esses parâmetros, Olá CLI do Azure cria um automaticamente para uso com o serviço de contêiner. Isso ocorre transparente durante a implantação de saudação. 

Olá comando a seguir cria um cluster Kubernetes e gera as chaves de SSH e credenciais de serviço principal:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Se sua conta não tiver hello Azure AD e assinatura permissões toocreate uma entidade de serviço, o comando hello gera um erro semelhante muito`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Considerações adicionais

* Se você não tiver permissões toocreate uma entidade de serviço em sua assinatura, talvez seja necessário tooask AD do Azure ou assinatura administrador tooassign Olá permissões necessárias ou peça para um toouse principal do serviço com o serviço de contêiner do Azure. 

* entidade de serviço Olá para Kubernetes é uma parte da configuração de cluster de saudação. No entanto, não use o cluster de Olá Olá identidade toodeploy.

* Cada entidade de serviço é associada a um aplicativo Azure AD. Olá entidade de serviço para um cluster Kubernetes pode ser associada a qualquer válida do Azure nome do aplicativo do AD (por exemplo: `https://www.contoso.org/example`). Olá URL para o aplicativo hello não tem um ponto de extremidade real do toobe.

* Ao especificar a entidade de serviço Olá **ID do cliente**, você pode usar o valor Olá Olá `appId` (conforme mostrado neste artigo) ou da entidade de serviço correspondente Olá `name` (por exemplo,`https://www.contoso.org/example`).

* Em mestre hello e agente de VMs no cluster de Kubernetes hello, credenciais de entidade de serviço Olá são armazenadas em Olá arquivo /etc/kubernetes/azure.json.

* Quando você usa Olá `az acs create` comando entidade de serviço toogenerate Olá automaticamente, credenciais de entidade de serviço Olá são gravadas toohello arquivo ~/.azure/acsServicePrincipal.json na máquina de saudação usada toorun comando de saudação. 

* Quando você usa Olá `az acs create` command entidade de serviço toogenerate Olá automaticamente, a entidade de serviço Olá também pode se autenticar com um [registro de contêiner do Azure](../../container-registry/container-registry-intro.md) criado no hello mesmo assinatura.




## <a name="next-steps"></a>Próximas etapas

* [Introdução ao Kubernetes](container-service-kubernetes-walkthrough.md) em seu cluster de serviço de contêiner.

* tootroubleshoot Olá entidade de serviço para Kubernetes, consulte Olá [documentação do mecanismo de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


