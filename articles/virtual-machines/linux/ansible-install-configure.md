---
title: "aaaInstall e configurar Ansible para uso com máquinas virtuais do Azure | Microsoft Docs"
description: Saiba como tooinstall e configurar Ansible para gerenciar recursos do Azure no Ubuntu, CentOS e SLES
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Instalar e configurar Ansible toomanage VMs no Azure
Este artigo fornece detalhes sobre como tooinstall Ansible e módulos do Azure SDK de Python necessários para alguns dos Olá distribuições de Linux mais comuns. Você pode instalar Ansible em outras distribuições ajustando Olá instalado pacotes toofit sua plataforma específica. toocreate Azure recursos de uma maneira segura, você saiba também como toocreate e definir as credenciais para Ansible toouse. 

Para obter mais opções de instalação e etapas para outras plataformas, consulte Olá [Ansible guia de instalação](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Instalar o Ansible
Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAnsible* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Agora crie uma VM e instalar Ansible para uma saudação distribuições a seguir:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Criar as credenciais do Azure
O Ansible comunica-se com o Azure usando um nome de usuário e uma senha ou uma entidade de serviço. Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Ansible. Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure. segurança de tooimprove por apenas fornecer um nome de usuário e uma senha, este exemplo cria um serviço básico principal.

Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que Ansible precisa:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Um exemplo da saída de hello de saudação anterior comandos é o seguinte:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, você também precisa tooobtain ID de sua assinatura do Azure com [Mostrar de conta az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Use saída Olá desses dois comandos na próxima etapa de saudação.


## <a name="create-ansible-credentials-file"></a>Criar arquivo de credenciais do Ansible
tooprovide credenciais tooAnsible, defina as variáveis de ambiente ou criar um arquivo de credenciais locais. Para obter mais informações sobre como toodefine Ansible credenciais, consulte [tooAzure fornecendo credenciais módulos](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Para um ambiente de desenvolvimento, crie um arquivo de *credenciais* para o Ansible em sua VM host da seguinte maneira:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Olá *credenciais* próprio arquivo combina Olá ID da assinatura com a saída de saudação de criação de uma entidade de serviço. Saída de hello anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesmo ordem conforme necessário para *client_id*, *segredo*, e *locatário* . Olá seguindo exemplo *credenciais* arquivo mostra esses valores correspondentes a saída anterior hello. Insira seus próprios valores da seguinte maneira:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Usar variáveis de ambiente Ansible
Se você for toouse ferramentas como torre Ansible ou Jenkins, você pode definir variáveis de ambiente da seguinte maneira. Essas variáveis combinam Olá ID da assinatura com a saída de saudação de criação de um serviço principal. Saída da saudação anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesma ordem conforme necessário para *AZURE_CLIENT_ID*, *AZURE_SECRET*, e *AZURE_ LOCATÁRIO*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Próximas etapas
Agora você tem Ansible e Olá necessários módulos do Azure SDK de Python instalados e as credenciais definidas para Ansible toouse. Saiba como muito[criar uma VM com Ansible](ansible-create-vm.md). Você também pode aprender como muito[criar uma VM do Azure concluída e suporte a recursos com Ansible](ansible-create-complete-vm.md).
