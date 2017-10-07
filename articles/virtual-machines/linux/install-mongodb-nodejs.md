---
title: "aaaInstall MongoDB em uma VM do Linux usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooinstall e configurar o MongoDB em uma máquina virtual do Linux no Azure usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Como tooinstall e configurar o MongoDB em uma VM do Linux usando Olá 1.0 da CLI do Azure
[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho. Este artigo mostra como tooinstall e configurar o MongoDB em uma VM do Linux no Azure usando o modelo de implantação do Gerenciador de recursos de saudação. São mostrados exemplos que explicam em detalhes como:

* [Instalar e configurar uma instância básica do MongoDB manualmente](#manually-install-and-configure-mongodb-on-a-vm)
* [Criar uma instância básica do MongoDB usando um Modelo do Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Criar um cluster fragmentado complexo MongoDB com conjuntos de réplicas usando um modelo do Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- CLI do Azure 1.0 – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](create-cli-complete-nodejs.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Instalar e configurar manualmente o MongoDB em uma VM
O MongoDB [fornece instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuições de Linux incluindo Red Hat/CentOS, SUSE, Ubuntu e Debian. Olá exemplo a seguir cria um *CentOS* VM usando uma chave SSH armazenada em *~/.ssh/id_rsa.pub*. Saudação de resposta solicita nome da conta de armazenamento, o nome DNS e credenciais de administrador:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Faça logon no toohello VM usando o endereço IP público Olá exibido final Olá Olá anterior da etapa de criação da VM:

```bash
ssh azureuser@40.78.23.145
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

Por padrão, SELinux é imposto nas imagens do CentOS que impedem que você acesse o MongoDB. Instalar ferramentas de gerenciamento de política e configure SELinux tooallow MongoDB toooperate na porta TCP padrão 27017 da seguinte maneira. 

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
Você pode criar uma instância do MongoDB básico em uma única VM CentOS usando Olá seguindo o modelo de início rápido do Azure do GitHub. Este modelo usa a extensão de Script personalizado de saudação para Linux tooadd um `yum` tooyour repositório recém-criada em VM CentOS e, em seguida, instale o MongoDB.

* [Instância básica do MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Olá exemplo a seguir cria um grupo de recursos com o nome da saudação `myResourceGroup` em Olá `eastus` região. Insira seus próprios valores da seguinte maneira:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Olá CLI do Azure retorna tooa prompt dentro de alguns segundos de criação de implantação hello, mas a instalação hello e configuração pega toocomplete de alguns minutos. Verificar o status de saudação da implantação de saudação com `azure group deployment show myResourceGroup`, inserir o nome de saudação do seu grupo de recursos adequadamente. Aguarde até que a saudação **ProvisioningState** mostra *êxito* antes de tentar tooSSH toohello VM.

Depois que a implantação Olá é concluída, SSH toohello VM. Obter endereço IP de saudação da VM usando Olá `azure vm show` comando como Olá exemplo a seguir:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Final Olá da saída de hello, endereço IP público de saudação é exibido. SSH tooyour VM com o endereço IP de saudação da VM:

```bash
ssh azureuser@138.91.149.74
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

Olá exemplo a seguir cria um grupo de recursos com o nome da saudação *myResourceGroup* em Olá *eastus* região. Insira seus próprios valores da seguinte maneira:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Olá CLI do Azure retorna tooa prompt dentro de alguns segundos de criação de implantação hello, mas hello instalação e configuração podem assumir um toocomplete de hora. Verificar o status de saudação da implantação de saudação com `azure group deployment show myResourceGroup`, ajustando o nome de saudação do seu grupo de recursos adequadamente. Aguarde até que a saudação **ProvisioningState** mostra *êxito* antes de conectar toohello VMs.


## <a name="next-steps"></a>Próximas etapas
Nestes exemplos, você se conectar toohello MongoDB instância local do hello VM. Se você desejar tooconnect toohello MongoDB instância da outra VM ou de rede, certifique-se de saudação apropriada [são criadas regras de grupo de segurança de rede](nsg-quickstart.md).

Para obter mais informações sobre como criar modelos de uso, consulte Olá [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).

modelos do Azure Resource Manager Olá usam toodownload de extensão de Script personalizado hello e executar scripts em suas VMs. Para obter mais informações, consulte [hello usando extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).

