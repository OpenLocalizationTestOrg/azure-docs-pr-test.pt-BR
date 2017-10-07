---
title: aaaInstall MongoDB em uma VM do Linux com hello CLI do Azure | Microsoft Docs
description: "Saiba como tooinstall e configurar o MongoDB em uma saudação de iusing de máquina virtual Linux 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Como tooinstall e configurar o MongoDB em uma VM do Linux
[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho. Este artigo mostra como tooinstall e configurar o MongoDB em uma VM do Linux com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](install-mongodb-nodejs.md). São mostrados exemplos que explicam em detalhes como:

* [Instalar e configurar uma instância básica do MongoDB manualmente](#manually-install-and-configure-mongodb-on-a-vm)
* [Criar uma instância básica do MongoDB usando um Modelo do Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Criar um cluster fragmentado complexo MongoDB com conjuntos de réplicas usando um modelo do Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Instalar e configurar manualmente o MongoDB em uma VM
O MongoDB [fornece instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuições de Linux incluindo Red Hat/CentOS, SUSE, Ubuntu e Debian. Olá exemplo a seguir cria um *CentOS* VM. toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVM* com um usuário chamado *azureuser* usando a autenticação de chave pública SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM usando seu próprio nome de usuário e a saudação `publicIpAddress` listados na saída de saudação da etapa anterior hello:

```bash
ssh azureuser@<publicIpAddress>
```

fontes de instalação tooadd Olá para o MongoDB, criar um **yum** arquivo de repositório da seguinte maneira:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Abra o arquivo de repositório de MongoDB Olá para edição. Adicione Olá linhas seguintes:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Instale o MongoDB usando o **yum** da seguinte maneira:

```bash
sudo yum install -y mongodb-org
```

Por padrão, SELinux é imposto nas imagens do CentOS que impedem que você acesse o MongoDB. Instalar ferramentas de gerenciamento de política e configure SELinux tooallow MongoDB toooperate na porta TCP padrão 27017 da seguinte maneira:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Inicie serviço de MongoDB de saudação da seguinte maneira:

```bash
sudo service mongod start
```

Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente:

```bash
mongo
```

Agora teste instância do MongoDB Olá por adicionar alguns dados e, em seguida, pesquisa:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Se desejar, configure o MongoDB toostart automaticamente durante uma reinicialização do sistema:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Criar uma instância básica do MongoDB em CentOS usando um modelo
Você pode criar uma instância do MongoDB básico em uma única VM CentOS usando Olá seguindo o modelo de início rápido do Azure do GitHub. Este modelo usa a extensão de Script personalizado de saudação para Linux tooadd um **yum** repositório tooyour recém-criada em VM CentOS e, em seguida, instale o MongoDB.

* [Instância básica do MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login). Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

Em seguida, implante o modelo do MongoDB Olá com [criar implantação de grupo az](/cli/azure/group/deployment#create). Defina seus próprios nomes e tamanhos de recurso quando necessário, como para *newStorageAccountName*, *virtualNetworkName* e *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Faça logon no toohello VM usando o endereço DNS público Olá da VM. Você pode exibir o endereço DNS público Olá com [Mostrar de vm az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM usando seu próprio nome de usuário e o endereço DNS público:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente da seguinte maneira:

```bash
mongo
```

Agora teste instância Olá por adicionar alguns dados e a pesquisa da seguinte maneira:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Criar um Cluster Fragmentado MongoDB complexo no CentOS usando um modelo
Você pode criar um cluster de fragmentados MongoDB complexas usando Olá seguindo o modelo de início rápido do Azure do GitHub. Este modelo segue Olá [práticas recomendadas para clusters fragmentados MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide alta disponibilidade e redundância. modelo de saudação cria dois fragmentos, com três nós em cada conjunto de réplicas. Uma réplica de servidor de configuração definido com três nós também é criada, e dois **mongos** roteador servidores tooprovide consistência tooapplications de entre fragmentos hello.

* [Cluster Fragmentado MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Implantar este cluster fragmentado do MongoDB complexo requer mais de 20 núcleos, que normalmente é saudação padrão contagem de núcleos por região para uma assinatura. Abra um tooincrease de solicitação de suporte do Azure em sua contagem de núcleos.

toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login). Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

Em seguida, implante o modelo do MongoDB Olá com [criar implantação de grupo az](/cli/azure/group/deployment#create). Defina seus próprios nomes e tamanhos de recurso quando necessário, como para *mongoAdminUsername*, *sizeOfDataDiskInGB* e *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Esta implantação pode assumir um toodeploy de hora e configurar todas as instâncias VM hello. Olá `--no-wait` sinalizador é usado no final de saudação do hello precede o prompt de comando do comando tooreturn controle toohello depois que a implantação de modelo Olá foi aceita pelo Olá plataforma Windows Azure. Você pode exibir o status de implantação de saudação com [Mostrar de implantação de grupo az](/cli/azure/group/deployment#show). exibições de exemplo a seguir Olá Olá status Olá *myMongoDBCluster* implantação em Olá *myResourceGroup* grupo de recursos:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Próximas etapas
Nestes exemplos, você se conectar toohello MongoDB instância local do hello VM. Se você desejar tooconnect toohello MongoDB instância da outra VM ou de rede, certifique-se de saudação apropriada [são criadas regras de grupo de segurança de rede](nsg-quickstart.md).

Esses exemplos implantar ambiente de MongoDB core Olá para fins de desenvolvimento. Aplica opções de configuração de segurança Olá necessários para seu ambiente. Para obter mais informações, consulte Olá [documentos de segurança do MongoDB](https://docs.mongodb.com/manual/security/).

Para obter mais informações sobre como criar modelos de uso, consulte Olá [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).

modelos do Azure Resource Manager Olá usam toodownload de extensão de Script personalizado hello e executar scripts em suas VMs. Para obter mais informações, consulte [hello usando extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).

