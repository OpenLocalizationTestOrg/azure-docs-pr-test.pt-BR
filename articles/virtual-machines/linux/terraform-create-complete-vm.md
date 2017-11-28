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
ms.openlocfilehash: aa0926de32dd85f4460bbfa84b7a6007e2199d51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="c6e11-103">Criar a infraestrutura básica no Azure usando o Terraform</span><span class="sxs-lookup"><span data-stu-id="c6e11-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="c6e11-104">Este artigo descreve as etapas necessárias para provisionar uma máquina virtual, junto com a infraestrutura subjacente, no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e11-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="c6e11-105">Você aprenderá a gravar scripts do Terraform e a visualizar as alterações antes de fazê-las na sua infraestrutura de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6e11-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="c6e11-106">Você também aprenderá a criar a infraestrutura no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="c6e11-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="c6e11-107">Para começar, crie um arquivo chamado \terraform_azure101.tf no editor de texto de sua preferência (Visual Studio Code/Sublime/Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="c6e11-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="c6e11-108">O nome exato do arquivo não é importante, pois o Terraform aceita o nome da pasta como parâmetro: todos os scripts na pasta são executados.</span><span class="sxs-lookup"><span data-stu-id="c6e11-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="c6e11-109">Cole o seguinte código no novo arquivo:</span><span class="sxs-lookup"><span data-stu-id="c6e11-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="c6e11-110">Na seção `provider` do script, você informa o Terraform para usar um provedor do Azure para provisionar recursos no script.</span><span class="sxs-lookup"><span data-stu-id="c6e11-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="c6e11-111">Para obter os valores de subscription_id, appId, senha e tenant_id, veja o guia [Instalar e configurar o Terraform](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c6e11-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="c6e11-112">Se você tiver criado variáveis de ambiente para os valores nesse bloco, não precisará incluí-las.</span><span class="sxs-lookup"><span data-stu-id="c6e11-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="c6e11-113">O recurso `azurerm_resource_group` instrui o Terraform a criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6e11-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="c6e11-114">Você pode ver mais tipos de recursos que estão disponíveis no Terraform mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c6e11-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="c6e11-115">Execute o script</span><span class="sxs-lookup"><span data-stu-id="c6e11-115">Execute the script</span></span>
<span data-ttu-id="c6e11-116">Depois de salvar o script, saia da linha de comando/console e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6e11-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
 <span data-ttu-id="c6e11-117">para inicializar o provedor de Terraform do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e11-117">to initialize the Terraform provider for Azure.</span></span> <span data-ttu-id="c6e11-118">Em seguida, altere o diretório para **terraformscripts** e emita o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6e11-118">Then change the directory to **terraformscripts**, and issue the following command:</span></span>
```
terraform plan
```
<span data-ttu-id="c6e11-119">Usamos o comando `plan` do Terraform, que examina os recursos definidos nos scripts.</span><span class="sxs-lookup"><span data-stu-id="c6e11-119">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="c6e11-120">Ele compara-os com as informações de estado salvas pelo Terraform e, em seguida, gera a execução planejada _sem_ de fato criar recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e11-120">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="c6e11-121">Depois de executar o comando anterior, você deverá ver algo semelhante à seguinte tela:</span><span class="sxs-lookup"><span data-stu-id="c6e11-121">After you execute the previous command, you should see something like the following screen:</span></span>

![Plano do Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="c6e11-123">Se tudo parecer correto, provisione esse novo grupo de recursos no Azure executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6e11-123">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply
```
<span data-ttu-id="c6e11-124">No portal do Azure, você deverá ver o novo grupo de recursos vazio chamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="c6e11-124">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="c6e11-125">Na seção abaixo, você adicionará uma máquina virtual e toda sua infraestrutura de suporte para essa máquina virtual a esse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6e11-125">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="c6e11-126">Provisionar uma VM Ubuntu com o Terraform</span><span class="sxs-lookup"><span data-stu-id="c6e11-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="c6e11-127">Vamos estender o script do Terraform criado com os detalhes necessários para provisionar uma máquina virtual executando Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c6e11-127">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="c6e11-128">Os recursos que você provisionar nas seções a seguir são:</span><span class="sxs-lookup"><span data-stu-id="c6e11-128">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="c6e11-129">Uma rede com uma única sub-rede</span><span class="sxs-lookup"><span data-stu-id="c6e11-129">A network with a single subnet</span></span>
* <span data-ttu-id="c6e11-130">Uma placa de interface de rede</span><span class="sxs-lookup"><span data-stu-id="c6e11-130">A network interface card</span></span> 
* <span data-ttu-id="c6e11-131">Uma conta de armazenamento para o diagnóstico da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c6e11-131">A storage account for the virtual machine diagnostics</span></span>
* <span data-ttu-id="c6e11-132">Um IP público</span><span class="sxs-lookup"><span data-stu-id="c6e11-132">A public IP</span></span>
* <span data-ttu-id="c6e11-133">Uma máquina virtual que utiliza todos os recursos anteriores</span><span class="sxs-lookup"><span data-stu-id="c6e11-133">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="c6e11-134">Para obter uma documentação completa de cada um dos recursos do Azure Terraform, consulte a [documentação do Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c6e11-134">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="c6e11-135">A versão completa do [script de provisionamento](#complete-terraform-script) também é fornecida para conveniência.</span><span class="sxs-lookup"><span data-stu-id="c6e11-135">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="c6e11-136">Estender o script do Terraform</span><span class="sxs-lookup"><span data-stu-id="c6e11-136">Extend the Terraform script</span></span>
<span data-ttu-id="c6e11-137">Estenda o script criado com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c6e11-137">Extend the script that was created with the following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="c6e11-138">O script anterior cria uma rede virtual e uma sub-rede dentro daquela rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c6e11-138">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="c6e11-139">Observe a referência ao grupo de recursos que você já criou por meio de “${azurerm_resource_group.helloterraform.name}” tanto na definição de rede virtual quanto na de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c6e11-139">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c6e11-140">Os trechos de script anteriores criam um IP público e um adaptador de rede que usa o IP público criado.</span><span class="sxs-lookup"><span data-stu-id="c6e11-140">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="c6e11-141">Observe as referências a subnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="c6e11-141">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="c6e11-142">O Terraform tem uma inteligência interna para entender que o adaptador de rede tem uma dependência dos recursos que precisam ser criados antes da criação do adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="c6e11-142">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c6e11-143">Aqui, você criou uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6e11-143">Here, you created a storage account.</span></span> <span data-ttu-id="c6e11-144">Essa conta de armazenamento é onde a máquina virtual armazena seus detalhes de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c6e11-144">This storage account is where the virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="c6e11-145">Por fim, o trecho de código anterior cria uma máquina virtual que utiliza todos os recursos já provisionados.</span><span class="sxs-lookup"><span data-stu-id="c6e11-145">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="c6e11-146">Eles são uma conta de armazenamento para os diagnósticos de máquina virtual, um adaptador de rede com IP público e sub-rede especificados e o grupo de recursos já criado.</span><span class="sxs-lookup"><span data-stu-id="c6e11-146">They are a storage account for the virtual machine diagnostics, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="c6e11-147">Observe a propriedade vm_size, na qual o script especifica um SKU DS1v2 do Azure Standard.</span><span class="sxs-lookup"><span data-stu-id="c6e11-147">Note the vm_size property, where the script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="c6e11-148">Você deve fornecer uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="c6e11-148">You are required to supply an SSH public key.</span></span> <span data-ttu-id="c6e11-149">Coloque o valor da chave pública na seção **... INSIRA A CHAVE PÚBLICA OPENSSH AQUI...**  acima.</span><span class="sxs-lookup"><span data-stu-id="c6e11-149">Place the public key value into the section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="c6e11-150">Você pode usar um par de chave ssh existente ou seguir a documentação do [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) para gerar o par de chaves.</span><span class="sxs-lookup"><span data-stu-id="c6e11-150">You can use an existing ssh key pair or follow the [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation to generate the key pair.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="c6e11-151">Execute o script</span><span class="sxs-lookup"><span data-stu-id="c6e11-151">Execute the script</span></span>
<span data-ttu-id="c6e11-152">Com o script completo salvo, saia para o console/linha de comando e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6e11-152">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply
```
<span data-ttu-id="c6e11-153">Depois de algum tempo, os recursos, incluindo uma máquina virtual, aparecem no grupo de recursos `terraformtest` no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e11-153">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="c6e11-154">Script completo do Terraform</span><span class="sxs-lookup"><span data-stu-id="c6e11-154">Complete Terraform script</span></span>

<span data-ttu-id="c6e11-155">Para conveniência, abaixo está o script completo do Terraform que provisiona toda a infraestrutura discutida neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c6e11-155">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c6e11-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6e11-156">Next steps</span></span>
<span data-ttu-id="c6e11-157">Você criou a infraestrutura básica no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="c6e11-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="c6e11-158">Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c6e11-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="c6e11-159">Para obter uma lista atualizada de provedores do Azure com suporte, consulte a [Documentação do Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c6e11-159">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
