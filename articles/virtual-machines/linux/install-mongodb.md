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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="0dfc1-103">Como tooinstall e configurar o MongoDB em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="0dfc1-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="0dfc1-104">[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="0dfc1-105">Este artigo mostra como tooinstall e configurar o MongoDB em uma VM do Linux com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="0dfc1-106">Você também pode executar essas etapas com hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="0dfc1-107">São mostrados exemplos que explicam em detalhes como:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="0dfc1-108">Instalar e configurar uma instância básica do MongoDB manualmente</span><span class="sxs-lookup"><span data-stu-id="0dfc1-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="0dfc1-109">Criar uma instância básica do MongoDB usando um Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0dfc1-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="0dfc1-110">Criar um cluster fragmentado complexo MongoDB com conjuntos de réplicas usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0dfc1-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="0dfc1-111">Instalar e configurar manualmente o MongoDB em uma VM</span><span class="sxs-lookup"><span data-stu-id="0dfc1-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="0dfc1-112">O MongoDB [fornece instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuições de Linux incluindo Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="0dfc1-113">Olá exemplo a seguir cria um *CentOS* VM.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="0dfc1-114">toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0dfc1-115">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0dfc1-116">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0dfc1-117">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0dfc1-118">Olá, exemplo a seguir cria uma VM denominada *myVM* com um usuário chamado *azureuser* usando a autenticação de chave pública SSH</span><span class="sxs-lookup"><span data-stu-id="0dfc1-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="0dfc1-119">SSH toohello VM usando seu próprio nome de usuário e a saudação `publicIpAddress` listados na saída de saudação da etapa anterior hello:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="0dfc1-120">fontes de instalação tooadd Olá para o MongoDB, criar um **yum** arquivo de repositório da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="0dfc1-121">Abra o arquivo de repositório de MongoDB Olá para edição.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="0dfc1-122">Adicione Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="0dfc1-123">Instale o MongoDB usando o **yum** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="0dfc1-124">Por padrão, SELinux é imposto nas imagens do CentOS que impedem que você acesse o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="0dfc1-125">Instalar ferramentas de gerenciamento de política e configure SELinux tooallow MongoDB toooperate na porta TCP padrão 27017 da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="0dfc1-126">Inicie serviço de MongoDB de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="0dfc1-127">Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="0dfc1-128">Agora teste instância do MongoDB Olá por adicionar alguns dados e, em seguida, pesquisa:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="0dfc1-129">Se desejar, configure o MongoDB toostart automaticamente durante uma reinicialização do sistema:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="0dfc1-130">Criar uma instância básica do MongoDB em CentOS usando um modelo</span><span class="sxs-lookup"><span data-stu-id="0dfc1-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="0dfc1-131">Você pode criar uma instância do MongoDB básico em uma única VM CentOS usando Olá seguindo o modelo de início rápido do Azure do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="0dfc1-132">Este modelo usa a extensão de Script personalizado de saudação para Linux tooadd um **yum** repositório tooyour recém-criada em VM CentOS e, em seguida, instale o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="0dfc1-133">[Instância básica do MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="0dfc1-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="0dfc1-134">toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="0dfc1-135">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0dfc1-136">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0dfc1-137">Em seguida, implante o modelo do MongoDB Olá com [criar implantação de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="0dfc1-138">Defina seus próprios nomes e tamanhos de recurso quando necessário, como para *newStorageAccountName*, *virtualNetworkName* e *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="0dfc1-139">Faça logon no toohello VM usando o endereço DNS público Olá da VM.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="0dfc1-140">Você pode exibir o endereço DNS público Olá com [Mostrar de vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="0dfc1-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="0dfc1-141">SSH tooyour VM usando seu próprio nome de usuário e o endereço DNS público:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="0dfc1-142">Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="0dfc1-143">Agora teste instância Olá por adicionar alguns dados e a pesquisa da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="0dfc1-144">Criar um Cluster Fragmentado MongoDB complexo no CentOS usando um modelo</span><span class="sxs-lookup"><span data-stu-id="0dfc1-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="0dfc1-145">Você pode criar um cluster de fragmentados MongoDB complexas usando Olá seguindo o modelo de início rápido do Azure do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="0dfc1-146">Este modelo segue Olá [práticas recomendadas para clusters fragmentados MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide alta disponibilidade e redundância.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="0dfc1-147">modelo de saudação cria dois fragmentos, com três nós em cada conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="0dfc1-148">Uma réplica de servidor de configuração definido com três nós também é criada, e dois **mongos** roteador servidores tooprovide consistência tooapplications de entre fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="0dfc1-149">[Cluster Fragmentado MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="0dfc1-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="0dfc1-150">Implantar este cluster fragmentado do MongoDB complexo requer mais de 20 núcleos, que normalmente é saudação padrão contagem de núcleos por região para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="0dfc1-151">Abra um tooincrease de solicitação de suporte do Azure em sua contagem de núcleos.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="0dfc1-152">toocreate nesse ambiente, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="0dfc1-153">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0dfc1-154">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0dfc1-155">Em seguida, implante o modelo do MongoDB Olá com [criar implantação de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="0dfc1-156">Defina seus próprios nomes e tamanhos de recurso quando necessário, como para *mongoAdminUsername*, *sizeOfDataDiskInGB* e *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="0dfc1-157">Esta implantação pode assumir um toodeploy de hora e configurar todas as instâncias VM hello.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="0dfc1-158">Olá `--no-wait` sinalizador é usado no final de saudação do hello precede o prompt de comando do comando tooreturn controle toohello depois que a implantação de modelo Olá foi aceita pelo Olá plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="0dfc1-159">Você pode exibir o status de implantação de saudação com [Mostrar de implantação de grupo az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="0dfc1-160">exibições de exemplo a seguir Olá Olá status Olá *myMongoDBCluster* implantação em Olá *myResourceGroup* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="0dfc1-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="0dfc1-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dfc1-161">Next steps</span></span>
<span data-ttu-id="0dfc1-162">Nestes exemplos, você se conectar toohello MongoDB instância local do hello VM.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="0dfc1-163">Se você desejar tooconnect toohello MongoDB instância da outra VM ou de rede, certifique-se de saudação apropriada [são criadas regras de grupo de segurança de rede](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="0dfc1-164">Esses exemplos implantar ambiente de MongoDB core Olá para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="0dfc1-165">Aplica opções de configuração de segurança Olá necessários para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="0dfc1-166">Para obter mais informações, consulte Olá [documentos de segurança do MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="0dfc1-167">Para obter mais informações sobre como criar modelos de uso, consulte Olá [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="0dfc1-168">modelos do Azure Resource Manager Olá usam toodownload de extensão de Script personalizado hello e executar scripts em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="0dfc1-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="0dfc1-169">Para obter mais informações, consulte [hello usando extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="0dfc1-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

