---
title: "infraestrutura básica aaaCreate no Azure usando Terraform | Microsoft Docs"
description: Saiba como toocreate Azure recursos usando Terraform
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="69629-103">Criar a infraestrutura básica no Azure usando o Terraform</span><span class="sxs-lookup"><span data-stu-id="69629-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="69629-104">Este artigo descreve etapas Olá tootake tooprovision uma máquina virtual, junto com a infraestrutura subjacente, você precisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="69629-105">Você aprenderá como toowrite Terraform scripts e como Olá toovisualize alterações antes de torná-los o em sua infraestrutura de nuvem.</span><span class="sxs-lookup"><span data-stu-id="69629-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="69629-106">Você também aprenderá como infraestrutura toocreate no Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="69629-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="69629-107">tooget iniciado, crie um arquivo chamado \terraform_azure101.tf em seu editor de texto da opção (Visual Studio código/Sublime Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="69629-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="69629-108">nome exato de saudação do arquivo hello não é importante porque Terraform aceita o nome da pasta hello como um parâmetro: todos os scripts na pasta Olá seja executados.</span><span class="sxs-lookup"><span data-stu-id="69629-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="69629-109">Cole Olá código no novo arquivo de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="69629-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="69629-110">Em Olá `provider` seção de saudação do script, informar Terraform toouse recursos de tooprovision um provedor do Azure no script hello.</span><span class="sxs-lookup"><span data-stu-id="69629-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="69629-111">valores de tooget subscription_id, appId, senha e tenant_id, consulte Olá [instalar e configurar Terraform](terraform-install-configure.md) guia.</span><span class="sxs-lookup"><span data-stu-id="69629-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="69629-112">Se você criou variáveis de ambiente para os valores hello neste bloco, não será necessário tooinclude-lo.</span><span class="sxs-lookup"><span data-stu-id="69629-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="69629-113">Olá `azurerm_resource_group` recurso instrui Terraform toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="69629-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="69629-114">Você pode ver mais tipos de recursos que estão disponíveis no Terraform mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="69629-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="69629-115">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="69629-115">Execute hello script</span></span>
<span data-ttu-id="69629-116">Depois de salvar o script hello, sair da linha de comando do console de toohello e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="69629-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="69629-117">provedor de Terraform tooinitialize do Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="69629-118">Em seguida, digite o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="69629-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="69629-119">Vamos supor que `terraformscripts` é Olá pasta em que o script hello foi salvo.</span><span class="sxs-lookup"><span data-stu-id="69629-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="69629-120">Usamos Olá `plan` Terraform comando, que examina os recursos de saudação definidos nos scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="69629-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="69629-121">Ele compara toohello informações de estado salvas por Terraform e, em seguida, saídas Olá execução planejada _sem_ na verdade criando recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="69629-122">Depois de executar o comando anterior hello, você verá algo parecido com hello tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="69629-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Plano do Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="69629-124">Se tudo estiver correto, provisione esse novo grupo de recursos no Azure, executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="69629-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="69629-125">Em Olá portal do Azure, você deve ver Olá novo vazio grupo de recursos chamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="69629-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="69629-126">Olá seção a seguir, você adiciona que uma máquina virtual e todos os Olá infra-estrutura de suporte para esse grupo de recursos de toohello de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="69629-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="69629-127">Provisionar uma VM Ubuntu com o Terraform</span><span class="sxs-lookup"><span data-stu-id="69629-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="69629-128">Vamos estender uma máquina virtual executada Ubuntu script de Terraform Olá que criamos com detalhes de saudação tooprovision necessário.</span><span class="sxs-lookup"><span data-stu-id="69629-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="69629-129">recursos de saudação provisionado no hello seções a seguir são:</span><span class="sxs-lookup"><span data-stu-id="69629-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="69629-130">Uma rede com uma única sub-rede</span><span class="sxs-lookup"><span data-stu-id="69629-130">A network with a single subnet</span></span>
* <span data-ttu-id="69629-131">Uma placa de interface de rede</span><span class="sxs-lookup"><span data-stu-id="69629-131">A network interface card</span></span> 
* <span data-ttu-id="69629-132">Uma conta de armazenamento com um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="69629-132">A storage account with a storage container</span></span>
* <span data-ttu-id="69629-133">Um IP público</span><span class="sxs-lookup"><span data-stu-id="69629-133">A public IP</span></span>
* <span data-ttu-id="69629-134">Uma máquina virtual que utiliza todos os recursos de saudação anterior</span><span class="sxs-lookup"><span data-stu-id="69629-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="69629-135">Para obter a documentação completa para cada um dos recursos do Azure Terraform hello, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="69629-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="69629-136">versão completa de saudação do hello [script de provisionamento](#complete-terraform-script) também é fornecido por questões de conveniência.</span><span class="sxs-lookup"><span data-stu-id="69629-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="69629-137">Estender o script de Terraform Olá</span><span class="sxs-lookup"><span data-stu-id="69629-137">Extend hello Terraform script</span></span>
<span data-ttu-id="69629-138">Estenda o script hello que foi criado com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="69629-138">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="69629-139">script de saudação anterior cria uma rede virtual e uma sub-rede dentro da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="69629-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="69629-140">Observe o grupo de recursos do hello referência toohello que você criou já via "${azurerm_resource_group.helloterraform.name}" na rede virtual hello e definição de subrede hello.</span><span class="sxs-lookup"><span data-stu-id="69629-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
<span data-ttu-id="69629-141">trechos de código de script de anterior Olá criar um IP público e uma interface de rede que usa o IP público de saudação criado.</span><span class="sxs-lookup"><span data-stu-id="69629-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="69629-142">Observação Olá referências toosubnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="69629-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="69629-143">Terraform tem toounderstand inteligência interna que Olá interface de rede tem uma dependência dos recursos de saudação que toobe necessidade criado antes da criação de Olá Olá da interface de rede.</span><span class="sxs-lookup"><span data-stu-id="69629-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="69629-144">Aqui, você criou uma conta de armazenamento e definiu um contêiner de armazenamento dentro dessa conta.</span><span class="sxs-lookup"><span data-stu-id="69629-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="69629-145">Esta conta de armazenamento é onde você armazena os discos rígidos virtuais (VHDs) para a máquina virtual de saudação sobre toobe criado.</span><span class="sxs-lookup"><span data-stu-id="69629-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="69629-146">Finalmente, o trecho de código anterior Olá cria uma máquina virtual que utiliza todos os recursos de saudação provisionados já.</span><span class="sxs-lookup"><span data-stu-id="69629-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="69629-147">Eles são uma conta de armazenamento e um contêiner para um VHD, uma interface de rede pública IP e sub-rede especificada, e o grupo de recursos Olá já criado.</span><span class="sxs-lookup"><span data-stu-id="69629-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="69629-148">Observe a propriedade de vm_size hello, onde o script hello Especifica um SKU de A0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="69629-149">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="69629-149">Execute hello script</span></span>
<span data-ttu-id="69629-150">Com script completo Olá salvo, sair da linha de comando do console de toohello e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="69629-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="69629-151">Depois de algum tempo, os recursos de hello, incluindo uma máquina virtual, são exibidos no hello `terraformtest` grupo de recursos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="69629-152">Script completo do Terraform</span><span class="sxs-lookup"><span data-stu-id="69629-152">Complete Terraform script</span></span>

<span data-ttu-id="69629-153">Para sua conveniência, abaixo é Olá completa Terraform script que provisiona toda a infra-estrutura de saudação discutidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="69629-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="69629-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69629-154">Next steps</span></span>
<span data-ttu-id="69629-155">Você criou a infraestrutura básica no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="69629-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="69629-156">Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="69629-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="69629-157">Para obter uma lista atualizada de provedores do Azure com suporte, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="69629-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
