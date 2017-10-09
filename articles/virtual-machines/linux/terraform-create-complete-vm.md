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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="c41be-103">Criar a infraestrutura básica no Azure usando o Terraform</span><span class="sxs-lookup"><span data-stu-id="c41be-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="c41be-104">Este artigo descreve etapas Olá tootake tooprovision uma máquina virtual, junto com a infraestrutura subjacente, você precisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="c41be-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="c41be-105">Você aprenderá como toowrite Terraform scripts e como Olá toovisualize alterações antes de torná-los o em sua infraestrutura de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c41be-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="c41be-106">Você também aprenderá como infraestrutura toocreate no Azure usando Terraform.</span><span class="sxs-lookup"><span data-stu-id="c41be-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="c41be-107">tooget iniciado, crie um arquivo chamado \terraform_azure101.tf em seu editor de texto da opção (Visual Studio código/Sublime Vim/etc.).</span><span class="sxs-lookup"><span data-stu-id="c41be-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="c41be-108">nome exato de saudação do arquivo hello não é importante porque Terraform aceita o nome da pasta hello como um parâmetro: todos os scripts na pasta Olá seja executados.</span><span class="sxs-lookup"><span data-stu-id="c41be-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="c41be-109">Cole Olá código no novo arquivo de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="c41be-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
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
<span data-ttu-id="c41be-110">Em Olá `provider` seção de saudação do script, informar Terraform toouse recursos de tooprovision um provedor do Azure no script hello.</span><span class="sxs-lookup"><span data-stu-id="c41be-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="c41be-111">valores de tooget subscription_id, appId, senha e tenant_id, consulte Olá [instalar e configurar Terraform](terraform-install-configure.md) guia.</span><span class="sxs-lookup"><span data-stu-id="c41be-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="c41be-112">Se você criou variáveis de ambiente para os valores hello neste bloco, não será necessário tooinclude-lo.</span><span class="sxs-lookup"><span data-stu-id="c41be-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="c41be-113">Olá `azurerm_resource_group` recurso instrui Terraform toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c41be-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="c41be-114">Você pode ver mais tipos de recursos que estão disponíveis no Terraform mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c41be-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="c41be-115">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="c41be-115">Execute hello script</span></span>
<span data-ttu-id="c41be-116">Depois de salvar o script hello, sair da linha de comando do console de toohello e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c41be-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="c41be-117">provedor de Terraform tooinitialize Olá para o Azure.</span><span class="sxs-lookup"><span data-stu-id="c41be-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="c41be-118">Alterar o diretório de saudação muito**terraformscripts**, e o comando a seguir saudação do problema:</span><span class="sxs-lookup"><span data-stu-id="c41be-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="c41be-119">Usamos Olá `plan` Terraform comando, que examina os recursos de saudação definidos nos scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="c41be-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="c41be-120">Ele compara toohello informações de estado salvas por Terraform e, em seguida, saídas Olá execução planejada _sem_ na verdade criando recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c41be-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="c41be-121">Depois de executar o comando anterior hello, você verá algo parecido com hello tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="c41be-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Plano do Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="c41be-123">Se tudo estiver correto, provisione esse novo grupo de recursos no Azure, executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c41be-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="c41be-124">Em Olá portal do Azure, você deve ver Olá novo vazio grupo de recursos chamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="c41be-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="c41be-125">Olá seção a seguir, você adiciona que uma máquina virtual e todos os Olá infra-estrutura de suporte para esse grupo de recursos de toohello de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c41be-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="c41be-126">Provisionar uma VM Ubuntu com o Terraform</span><span class="sxs-lookup"><span data-stu-id="c41be-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="c41be-127">Vamos estender uma máquina virtual executada Ubuntu script de Terraform Olá que criamos com detalhes de saudação tooprovision necessário.</span><span class="sxs-lookup"><span data-stu-id="c41be-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="c41be-128">recursos de saudação provisionado no hello seções a seguir são:</span><span class="sxs-lookup"><span data-stu-id="c41be-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="c41be-129">Uma rede com uma única sub-rede</span><span class="sxs-lookup"><span data-stu-id="c41be-129">A network with a single subnet</span></span>
* <span data-ttu-id="c41be-130">Uma placa de interface de rede</span><span class="sxs-lookup"><span data-stu-id="c41be-130">A network interface card</span></span> 
* <span data-ttu-id="c41be-131">Uma conta de armazenamento para diagnóstico de máquina virtual Olá</span><span class="sxs-lookup"><span data-stu-id="c41be-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="c41be-132">Um IP público</span><span class="sxs-lookup"><span data-stu-id="c41be-132">A public IP</span></span>
* <span data-ttu-id="c41be-133">Uma máquina virtual que utiliza todos os recursos de saudação anterior</span><span class="sxs-lookup"><span data-stu-id="c41be-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="c41be-134">Para obter a documentação completa para cada um dos recursos do Azure Terraform hello, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c41be-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="c41be-135">versão completa de saudação do hello [script de provisionamento](#complete-terraform-script) também é fornecido por questões de conveniência.</span><span class="sxs-lookup"><span data-stu-id="c41be-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="c41be-136">Estender o script de Terraform Olá</span><span class="sxs-lookup"><span data-stu-id="c41be-136">Extend hello Terraform script</span></span>
<span data-ttu-id="c41be-137">Estenda o script hello que foi criado com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c41be-137">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="c41be-138">script de saudação anterior cria uma rede virtual e uma sub-rede dentro da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c41be-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="c41be-139">Observe o grupo de recursos do hello referência toohello que você criou já via "${azurerm_resource_group.helloterraform.name}" na rede virtual hello e definição de subrede hello.</span><span class="sxs-lookup"><span data-stu-id="c41be-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="c41be-140">trechos de código de script de anterior Olá criar um IP público e uma interface de rede que usa o IP público de saudação criado.</span><span class="sxs-lookup"><span data-stu-id="c41be-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="c41be-141">Observação Olá referências toosubnet_id e public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="c41be-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="c41be-142">Terraform tem toounderstand inteligência interna que Olá interface de rede tem uma dependência dos recursos de saudação que toobe necessidade criado antes da criação de Olá Olá da interface de rede.</span><span class="sxs-lookup"><span data-stu-id="c41be-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="c41be-143">Aqui, você criou uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c41be-143">Here, you created a storage account.</span></span> <span data-ttu-id="c41be-144">Essa conta de armazenamento é onde a máquina virtual de saudação armazenará seus detalhes de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c41be-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="c41be-145">Finalmente, o trecho de código anterior Olá cria uma máquina virtual que utiliza todos os recursos de saudação provisionados já.</span><span class="sxs-lookup"><span data-stu-id="c41be-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="c41be-146">Eles são uma conta de armazenamento para diagnóstico de máquina virtual hello, uma interface de rede pública IP e sub-rede especificada, e o grupo de recursos Olá já criado.</span><span class="sxs-lookup"><span data-stu-id="c41be-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="c41be-147">Observe a propriedade de vm_size hello, onde o script hello Especifica um SKU DS1v2 padrão do Azure.</span><span class="sxs-lookup"><span data-stu-id="c41be-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="c41be-148">Você está toosupply necessária uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="c41be-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="c41be-149">Coloque o valor da chave pública Olá na seção Olá **... INSIRA A CHAVE PÚBLICA OPENSSH AQUI...**  acima.</span><span class="sxs-lookup"><span data-stu-id="c41be-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="c41be-150">Você pode usar um existente ssh par de chaves ou siga Olá [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) par de chaves toogenerate Olá documentação.</span><span class="sxs-lookup"><span data-stu-id="c41be-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="c41be-151">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="c41be-151">Execute hello script</span></span>
<span data-ttu-id="c41be-152">Com script completo Olá salvo, sair da linha de comando do console de toohello e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c41be-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="c41be-153">Depois de algum tempo, os recursos de hello, incluindo uma máquina virtual, são exibidos no hello `terraformtest` grupo de recursos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c41be-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="c41be-154">Script completo do Terraform</span><span class="sxs-lookup"><span data-stu-id="c41be-154">Complete Terraform script</span></span>

<span data-ttu-id="c41be-155">Para sua conveniência, abaixo é Olá completa Terraform script que provisiona toda a infra-estrutura de saudação discutidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c41be-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
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

## <a name="next-steps"></a><span data-ttu-id="c41be-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c41be-156">Next steps</span></span>
<span data-ttu-id="c41be-157">Você criou a infraestrutura básica no Azure usando o Terraform.</span><span class="sxs-lookup"><span data-stu-id="c41be-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="c41be-158">Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c41be-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="c41be-159">Para obter uma lista atualizada de provedores do Azure com suporte, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="c41be-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
