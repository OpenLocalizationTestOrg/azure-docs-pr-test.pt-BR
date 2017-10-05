---
title: "Criar a infraestrutura básica no Azure usando o Terraform | Microsoft Docs"
description: Saiba como criar recursos do Azure usando o Terraform
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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="462d9-103">Criar a infraestrutura básica no Azure usando o Terraform</span><span class="sxs-lookup"><span data-stu-id="462d9-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="462d9-104">Este artigo descreve as etapas necessárias para provisionar uma máquina virtual, junto com a infraestrutura subjacente, no Azure.</span><span class="sxs-lookup"><span data-stu-id="462d9-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="462d9-105">Você aprenderá a gravar scripts do Terraform e a visualizar as alterações antes de fazê-las na sua infraestrutura de nuvem.</span><span class="sxs-lookup"><span data-stu-id="462d9-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="462d9-106">Você também aprenderá a criar a infraestrutura no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="462d9-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="462d9-107">Para começar, crie um arquivo chamado \terraform_azure101.tf no editor de texto de sua preferência (Visual Studio Code/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="462d9-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="462d9-108">O nome exato do arquivo não é importante, pois o Terraform aceita o nome da pasta como parâmetro: todos os scripts na pasta são executados.</span><span class="sxs-lookup"><span data-stu-id="462d9-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="462d9-109">Cole o seguinte código no novo arquivo:</span><span class="sxs-lookup"><span data-stu-id="462d9-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="462d9-110">Na seção `provider` do script, você informa o Terraform para usar um provedor do Azure para provisionar recursos no script.</span><span class="sxs-lookup"><span data-stu-id="462d9-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="462d9-111">Para obter os valores de subscription_id, appId, senha e tenant_id, veja o guia [Instalar e configurar o Terraform](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="462d9-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="462d9-112">Se você tiver criado variáveis de ambiente para os valores nesse bloco, não precisará incluí-las.</span><span class="sxs-lookup"><span data-stu-id="462d9-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="462d9-113">O recurso `azurerm_resource_group` instrui o Terraform a criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="462d9-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="462d9-114">Você pode ver mais tipos de recursos que estão disponíveis no Terraform mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="462d9-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="462d9-115">Execute o script</span><span class="sxs-lookup"><span data-stu-id="462d9-115">Execute the script</span></span>
<span data-ttu-id="462d9-116">Depois de salvar o script, saia da linha de comando/console e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="462d9-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="462d9-117">para inicializar o provedor de Terraform do Azure.</span><span class="sxs-lookup"><span data-stu-id="462d9-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="462d9-118">Depois, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="462d9-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="462d9-119">Vamos supor que `terraformscripts` seja a pasta em que o script foi salvo.</span><span class="sxs-lookup"><span data-stu-id="462d9-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="462d9-120">Usamos o comando `plan` do Terraform, que examina os recursos definidos nos scripts.</span><span class="sxs-lookup"><span data-stu-id="462d9-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="462d9-121">Ele compara-os com as informações de estado salvas pelo Terraform e, em seguida, gera a execução planejada _sem_ de fato criar recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="462d9-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="462d9-122">Depois de executar o comando anterior, você deverá ver algo semelhante à seguinte tela:</span><span class="sxs-lookup"><span data-stu-id="462d9-122">After you execute the previous command, you should see something like the following screen:</span></span>

![Plano do Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="462d9-124">Se tudo parecer correto, provisione esse novo grupo de recursos no Azure executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="462d9-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="462d9-125">No portal do Azure, você deverá ver o novo grupo de recursos vazio chamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="462d9-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="462d9-126">Na seção abaixo, você adicionará uma máquina virtual e toda sua infraestrutura de suporte para essa máquina virtual a esse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="462d9-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="462d9-127">Provisionar uma VM Ubuntu com o Terraform</span><span class="sxs-lookup"><span data-stu-id="462d9-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="462d9-128">Vamos estender o script do Terraform criado com os detalhes necessários para provisionar uma máquina virtual executando Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="462d9-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="462d9-129">Os recursos que você provisionar nas seções a seguir são:</span><span class="sxs-lookup"><span data-stu-id="462d9-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="462d9-130">Uma rede com uma única sub-rede</span><span class="sxs-lookup"><span data-stu-id="462d9-130">A network with a single subnet</span></span>
* <span data-ttu-id="462d9-131">Uma placa de interface de rede</span><span class="sxs-lookup"><span data-stu-id="462d9-131">A network interface card</span></span> 
* <span data-ttu-id="462d9-132">Uma conta de armazenamento com um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="462d9-132">A storage account with a storage container</span></span>
* <span data-ttu-id="462d9-133">Um IP público</span><span class="sxs-lookup"><span data-stu-id="462d9-133">A public IP</span></span>
* <span data-ttu-id="462d9-134">Uma máquina virtual que utiliza todos os recursos anteriores</span><span class="sxs-lookup"><span data-stu-id="462d9-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="462d9-135">Para obter uma documentação completa de cada um dos recursos do Azure Terraform, consulte a [documentação do Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="462d9-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="462d9-136">A versão completa do [script de provisionamento](#complete-terraform-script) também é fornecida para conveniência.</span><span class="sxs-lookup"><span data-stu-id="462d9-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="462d9-137">Estender o script do Terraform</span><span class="sxs-lookup"><span data-stu-id="462d9-137">Extend the Terraform script</span></span>
<span data-ttu-id="462d9-138">Estenda o script criado com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="462d9-138">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="462d9-139">O script anterior cria uma rede virtual e uma sub-rede dentro daquela rede virtual.</span><span class="sxs-lookup"><span data-stu-id="462d9-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="462d9-140">Observe a referência ao grupo de recursos que você já criou por meio de “${azurerm_resource_group.helloterraform.name}” tanto na definição de rede virtual quanto na de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="462d9-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="462d9-141">Os trechos de script anteriores criam um IP público e um adaptador de rede que usa o IP público criado.</span><span class="sxs-lookup"><span data-stu-id="462d9-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="462d9-142">Observe as referências a subnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="462d9-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="462d9-143">O Terraform tem uma inteligência interna para entender que o adaptador de rede tem uma dependência dos recursos que precisam ser criados antes da criação do adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="462d9-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="462d9-144">Aqui, você criou uma conta de armazenamento e definiu um contêiner de armazenamento dentro dessa conta.</span><span class="sxs-lookup"><span data-stu-id="462d9-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="462d9-145">Essa conta de armazenamento é o local em que você armazena os VHDs (discos rígidos virtuais) para a máquina virtual prestes a ser criada.</span><span class="sxs-lookup"><span data-stu-id="462d9-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

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
<span data-ttu-id="462d9-146">Por fim, o trecho de código anterior cria uma máquina virtual que utiliza todos os recursos já provisionados.</span><span class="sxs-lookup"><span data-stu-id="462d9-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="462d9-147">Eles são uma conta de armazenamento e um contêiner para um VHD, um adaptador de rede com IP público e sub-rede especificados e o grupo de recursos já criado.</span><span class="sxs-lookup"><span data-stu-id="462d9-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="462d9-148">Observe a propriedade vm_size, na qual o script especifica um SKU A0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="462d9-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="462d9-149">Execute o script</span><span class="sxs-lookup"><span data-stu-id="462d9-149">Execute the script</span></span>
<span data-ttu-id="462d9-150">Com o script completo salvo, saia para o console/linha de comando e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="462d9-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="462d9-151">Depois de algum tempo, os recursos, incluindo uma máquina virtual, aparecem no grupo de recursos `terraformtest` no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="462d9-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="462d9-152">Script completo do Terraform</span><span class="sxs-lookup"><span data-stu-id="462d9-152">Complete Terraform script</span></span>

<span data-ttu-id="462d9-153">Para conveniência, abaixo está o script completo do Terraform que provisiona toda a infraestrutura discutida neste artigo.</span><span class="sxs-lookup"><span data-stu-id="462d9-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure the Microsoft Azure Provider
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

## <a name="next-steps"></a><span data-ttu-id="462d9-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="462d9-154">Next steps</span></span>
<span data-ttu-id="462d9-155">Você criou a infraestrutura básica no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="462d9-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="462d9-156">Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="462d9-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="462d9-157">Para obter uma lista atualizada de provedores do Azure com suporte, consulte a [Documentação do Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="462d9-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
