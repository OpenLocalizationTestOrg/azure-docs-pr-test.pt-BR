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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="1c192-103">Como tooinstall e configurar o MongoDB em uma VM do Linux usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1c192-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1c192-104">[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="1c192-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="1c192-105">Este artigo mostra como tooinstall e configurar o MongoDB em uma VM do Linux no Azure usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c192-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="1c192-106">São mostrados exemplos que explicam em detalhes como:</span><span class="sxs-lookup"><span data-stu-id="1c192-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="1c192-107">Instalar e configurar uma instância básica do MongoDB manualmente</span><span class="sxs-lookup"><span data-stu-id="1c192-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="1c192-108">Criar uma instância básica do MongoDB usando um Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c192-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="1c192-109">Criar um cluster fragmentado complexo MongoDB com conjuntos de réplicas usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c192-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1c192-110">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="1c192-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1c192-111">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c192-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1c192-112">CLI do Azure 1.0 – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="1c192-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1c192-113">[2.0 do CLI do Azure](create-cli-complete-nodejs.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="1c192-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="1c192-114">Instalar e configurar manualmente o MongoDB em uma VM</span><span class="sxs-lookup"><span data-stu-id="1c192-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="1c192-115">O MongoDB [fornece instruções de instalação](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuições de Linux incluindo Red Hat/CentOS, SUSE, Ubuntu e Debian.</span><span class="sxs-lookup"><span data-stu-id="1c192-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="1c192-116">Olá exemplo a seguir cria um *CentOS* VM usando uma chave SSH armazenada em *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="1c192-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="1c192-117">Saudação de resposta solicita nome da conta de armazenamento, o nome DNS e credenciais de administrador:</span><span class="sxs-lookup"><span data-stu-id="1c192-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="1c192-118">Faça logon no toohello VM usando o endereço IP público Olá exibido final Olá Olá anterior da etapa de criação da VM:</span><span class="sxs-lookup"><span data-stu-id="1c192-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="1c192-119">fontes de instalação tooadd Olá para o MongoDB, criar um **yum** arquivo de repositório da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="1c192-120">Abra o arquivo de repositório de MongoDB Olá para edição.</span><span class="sxs-lookup"><span data-stu-id="1c192-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="1c192-121">Adicione Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="1c192-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="1c192-122">Instale o MongoDB usando o **yum** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="1c192-123">Por padrão, SELinux é imposto nas imagens do CentOS que impedem que você acesse o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c192-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="1c192-124">Instalar ferramentas de gerenciamento de política e configure SELinux tooallow MongoDB toooperate na porta TCP padrão 27017 da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="1c192-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="1c192-125">Inicie serviço de MongoDB de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="1c192-126">Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente:</span><span class="sxs-lookup"><span data-stu-id="1c192-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="1c192-127">Agora teste instância do MongoDB Olá por adicionar alguns dados e, em seguida, pesquisa:</span><span class="sxs-lookup"><span data-stu-id="1c192-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="1c192-128">Se desejar, configure o MongoDB toostart automaticamente durante uma reinicialização do sistema:</span><span class="sxs-lookup"><span data-stu-id="1c192-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="1c192-129">Criar uma instância básica do MongoDB em CentOS usando um modelo</span><span class="sxs-lookup"><span data-stu-id="1c192-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="1c192-130">Você pode criar uma instância do MongoDB básico em uma única VM CentOS usando Olá seguindo o modelo de início rápido do Azure do GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c192-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="1c192-131">Este modelo usa a extensão de Script personalizado de saudação para Linux tooadd um `yum` tooyour repositório recém-criada em VM CentOS e, em seguida, instale o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c192-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="1c192-132">[Instância básica do MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1c192-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="1c192-133">Olá exemplo a seguir cria um grupo de recursos com o nome da saudação `myResourceGroup` em Olá `eastus` região.</span><span class="sxs-lookup"><span data-stu-id="1c192-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="1c192-134">Insira seus próprios valores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="1c192-135">Olá CLI do Azure retorna tooa prompt dentro de alguns segundos de criação de implantação hello, mas a instalação hello e configuração pega toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1c192-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="1c192-136">Verificar o status de saudação da implantação de saudação com `azure group deployment show myResourceGroup`, inserir o nome de saudação do seu grupo de recursos adequadamente.</span><span class="sxs-lookup"><span data-stu-id="1c192-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="1c192-137">Aguarde até que a saudação **ProvisioningState** mostra *êxito* antes de tentar tooSSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1c192-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="1c192-138">Depois que a implantação Olá é concluída, SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="1c192-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="1c192-139">Obter endereço IP de saudação da VM usando Olá `azure vm show` comando como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c192-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="1c192-140">Final Olá da saída de hello, endereço IP público de saudação é exibido.</span><span class="sxs-lookup"><span data-stu-id="1c192-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="1c192-141">SSH tooyour VM com o endereço IP de saudação da VM:</span><span class="sxs-lookup"><span data-stu-id="1c192-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="1c192-142">Verificar a instalação do MongoDB de saudação ao se conectar usando Olá local `mongo` cliente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="1c192-143">Agora teste instância Olá por adicionar alguns dados e a pesquisa da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="1c192-144">Criar um Cluster Fragmentado MongoDB complexo no CentOS usando um modelo</span><span class="sxs-lookup"><span data-stu-id="1c192-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="1c192-145">Você pode criar um cluster de fragmentados MongoDB complexas usando Olá seguindo o modelo de início rápido do Azure do GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c192-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="1c192-146">Este modelo segue Olá [práticas recomendadas para clusters fragmentados MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide alta disponibilidade e redundância.</span><span class="sxs-lookup"><span data-stu-id="1c192-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="1c192-147">modelo de saudação cria dois fragmentos, com três nós em cada conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="1c192-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="1c192-148">Uma réplica de servidor de configuração definido com três nós também é criada, e dois **mongos** roteador servidores tooprovide consistência tooapplications de entre fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="1c192-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="1c192-149">[Cluster Fragmentado MongoDB no CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) –https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1c192-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="1c192-150">Implantar este cluster fragmentado do MongoDB complexo requer mais de 20 núcleos, que normalmente é saudação padrão contagem de núcleos por região para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="1c192-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="1c192-151">Abra um tooincrease de solicitação de suporte do Azure em sua contagem de núcleos.</span><span class="sxs-lookup"><span data-stu-id="1c192-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="1c192-152">Olá exemplo a seguir cria um grupo de recursos com o nome da saudação *myResourceGroup* em Olá *eastus* região.</span><span class="sxs-lookup"><span data-stu-id="1c192-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="1c192-153">Insira seus próprios valores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1c192-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="1c192-154">Olá CLI do Azure retorna tooa prompt dentro de alguns segundos de criação de implantação hello, mas hello instalação e configuração podem assumir um toocomplete de hora.</span><span class="sxs-lookup"><span data-stu-id="1c192-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="1c192-155">Verificar o status de saudação da implantação de saudação com `azure group deployment show myResourceGroup`, ajustando o nome de saudação do seu grupo de recursos adequadamente.</span><span class="sxs-lookup"><span data-stu-id="1c192-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="1c192-156">Aguarde até que a saudação **ProvisioningState** mostra *êxito* antes de conectar toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="1c192-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c192-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c192-157">Next steps</span></span>
<span data-ttu-id="1c192-158">Nestes exemplos, você se conectar toohello MongoDB instância local do hello VM.</span><span class="sxs-lookup"><span data-stu-id="1c192-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="1c192-159">Se você desejar tooconnect toohello MongoDB instância da outra VM ou de rede, certifique-se de saudação apropriada [são criadas regras de grupo de segurança de rede](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="1c192-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="1c192-160">Para obter mais informações sobre como criar modelos de uso, consulte Olá [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c192-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="1c192-161">modelos do Azure Resource Manager Olá usam toodownload de extensão de Script personalizado hello e executar scripts em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="1c192-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="1c192-162">Para obter mais informações, consulte [hello usando extensão de Script personalizado do Azure com as máquinas virtuais Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="1c192-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

