---
title: aaaDeploy tooAzure OpenShift origem | Microsoft Docs
description: "Saiba mais máquinas virtuais do toodeploy OpenShift origem tooAzure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Implantar origem OpenShift tooAzure máquinas virtuais 

[OpenShift Origin](https://www.openshift.org/) é uma plataforma de contêiner de software livre criada em [Kubernetes](https://kubernetes.io/). Ele simplifica o processo de saudação da implantação, escala e operação de aplicativos de multilocação. 

Este guia descreve como toodeploy OpenShift origem em máquinas virtuais do Azure usando Olá CLI do Azure e modelos do Gerenciador de recursos do Azure. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Crie um toomanage KeyVault chaves SSH para cluster de OpenShift hello.
> * Implante um cluster OpenShift em VMs do Azure. 
> * Instalar e configurar Olá [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage cluster de saudação.
> * Personalize a implantação de OpenShift hello.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este guia rápido requer Olá CLI do Azure versão 2.0.8 ou posterior. versão de hello toofind, execute `az --version`. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Faça logon no tooAzure 
Login tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela ou clique em **Experimente** toouse Shell de nuvem.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Criar um cofre de chaves
Criar uma saudação de toostore KeyVault chaves SSH para cluster Olá com hello [keyvault az criar](/cli/azure/keyvault#create) comando.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Criar uma chave SSH 
Uma chave SSH é necessário toosecure acesso toohello cluster OpenShift origem. Criar um par de chaves SSH usando Olá `ssh-keygen` comando. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Olá par de chaves SSH, você cria não deve ter uma senha.

Para obter mais informações sobre as chaves de SSH no Windows, [como chaves de toocreate SSH no Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Armazenar chave privada SSH no Key Vault
Olá OpenShift implantação usa chave SSH Olá criados acesso toosecure toohello OpenShift mestre. tooenable Olá implantação toosecurely recuperar a chave SSH hello, chave de saudação do repositório no cofre de chaves usando o comando a seguir de saudação.

# <a name="enabled-for-template-deployment"></a>Habilitado para implantação de modelo
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Criar uma entidade de serviço 
O OpenShift se comunica com o Azure usando um nome de usuário e i,a senha ou uma entidade de serviço. Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o OpenShift. Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure. segurança de tooimprove por apenas fornecer um nome de usuário e uma senha, este exemplo cria um serviço básico principal.

Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que OpenShift precisa:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Tome nota da saudação appId propriedade retornada pelo comando hello.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Não crie uma senha não segura.  Execute a orientação [Restrições e regras de senha do Azure AD](/azure/active-directory/active-directory-passwords-policy).

Para obter mais informações sobre entidades de serviço, confira [Criar entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Implantar Olá modelo de origem OpenShift
Em seguida, implante o OpenShift Origin usando um modelo do Azure Resource Manager. 

> [!NOTE] 
> comando a seguir Hello requer az CLI 2.0.8 ou posterior. Você pode verificar Olá az CLI versão com hello `az --version` comando. Olá tooupdate versão CLI, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

Saudação de uso `appId` valor da entidade de serviço Olá criado anteriormente para Olá `aadClientId` parâmetro.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
implantação de saudação pode levar too20 toocomplete de minutos. Olá URL do console de OpenShift hello e o nome DNS do hello OpenShift mestre é impressa toohello terminal quando Olá implantação seja concluída.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Conecte-se toohello OpenShift cluster
Quando a conclusão da implantação hello, conecte-se toohello OpenShift console usando o navegador hello usando Olá `OpenShift Console Uri`. Como alternativa, você pode conectar toohello OpenShift mestre usando o comando a seguir de saudação.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Limpar recursos
Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster OpenShift e recursos todos relacionados.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, vimos como:
> [!div class="checklist"]
> * Crie um toomanage KeyVault chaves SSH para cluster de OpenShift hello.
> * Implante um cluster OpenShift em VMs do Azure. 
> * Instalar e configurar Olá [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage cluster de saudação.

Agora esse cluster de origem OpenShift é implantado. Você pode seguir OpenShift tutoriais toolearn como toodeploy seu primeiro aplicativo e use Olá OpenShift ferramentas. Consulte [Introdução à origem OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget iniciado. 
