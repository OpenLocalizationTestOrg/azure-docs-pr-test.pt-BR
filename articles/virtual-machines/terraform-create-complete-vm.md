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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Criar a infraestrutura básica no Azure usando o Terraform
Este artigo descreve etapas Olá tootake tooprovision uma máquina virtual, junto com a infraestrutura subjacente, você precisa no Azure. Você aprenderá como toowrite Terraform scripts e como Olá toovisualize alterações antes de torná-los o em sua infraestrutura de nuvem. Você também aprenderá como infraestrutura toocreate no Azure usando Terraform.

tooget iniciado, crie um arquivo chamado \terraform_azure101.tf em seu editor de texto da opção (Visual Studio código/Sublime Vim/etc.). nome exato de saudação do arquivo hello não é importante porque Terraform aceita o nome da pasta hello como um parâmetro: todos os scripts na pasta Olá seja executados. Cole Olá código no novo arquivo de saudação a seguir:

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
Em Olá `provider` seção de saudação do script, informar Terraform toouse recursos de tooprovision um provedor do Azure no script hello. valores de tooget subscription_id, appId, senha e tenant_id, consulte Olá [instalar e configurar Terraform](terraform-install-configure.md) guia. Se você criou variáveis de ambiente para os valores hello neste bloco, não será necessário tooinclude-lo. 

Olá `azurerm_resource_group` recurso instrui Terraform toocreate um novo grupo de recursos. Você pode ver mais tipos de recursos que estão disponíveis no Terraform mais adiante neste artigo.

## <a name="execute-hello-script"></a>Execute o script hello
Depois de salvar o script hello, sair da linha de comando do console de toohello e digite Olá a seguir:
```
terraform init
```
provedor de Terraform tooinitialize do Azure. Em seguida, digite o seguinte hello:
```
terraform plan terraformscripts
```
Vamos supor que `terraformscripts` é Olá pasta em que o script hello foi salvo. Usamos Olá `plan` Terraform comando, que examina os recursos de saudação definidos nos scripts de saudação. Ele compara toohello informações de estado salvas por Terraform e, em seguida, saídas Olá execução planejada _sem_ na verdade criando recursos no Azure. 

Depois de executar o comando anterior hello, você verá algo parecido com hello tela a seguir:

![Plano do Terraform](linux/media/terraform/tf_plan2.png)

Se tudo estiver correto, provisione esse novo grupo de recursos no Azure, executando Olá seguinte: 
```
terraform apply terraformscripts
```
Em Olá portal do Azure, você deve ver Olá novo vazio grupo de recursos chamado `terraformtest`. Olá seção a seguir, você adiciona que uma máquina virtual e todos os Olá infra-estrutura de suporte para esse grupo de recursos de toohello de máquina virtual.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Provisionar uma VM Ubuntu com o Terraform
Vamos estender uma máquina virtual executada Ubuntu script de Terraform Olá que criamos com detalhes de saudação tooprovision necessário. recursos de saudação provisionado no hello seções a seguir são:

* Uma rede com uma única sub-rede
* Uma placa de interface de rede 
* Uma conta de armazenamento com um contêiner de armazenamento
* Um IP público
* Uma máquina virtual que utiliza todos os recursos de saudação anterior 

Para obter a documentação completa para cada um dos recursos do Azure Terraform hello, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).

versão completa de saudação do hello [script de provisionamento](#complete-terraform-script) também é fornecido por questões de conveniência.

### <a name="extend-hello-terraform-script"></a>Estender o script de Terraform Olá
Estenda o script hello que foi criado com hello recursos a seguir: 
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
script de saudação anterior cria uma rede virtual e uma sub-rede dentro da rede virtual. Observe o grupo de recursos do hello referência toohello que você criou já via "${azurerm_resource_group.helloterraform.name}" na rede virtual hello e definição de subrede hello.

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
trechos de código de script de anterior Olá criar um IP público e uma interface de rede que usa o IP público de saudação criado. Observação Olá referências toosubnet_id e public_ip_address_id. Terraform tem toounderstand inteligência interna que Olá interface de rede tem uma dependência dos recursos de saudação que toobe necessidade criado antes da criação de Olá Olá da interface de rede.

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
Aqui, você criou uma conta de armazenamento e definiu um contêiner de armazenamento dentro dessa conta. Esta conta de armazenamento é onde você armazena os discos rígidos virtuais (VHDs) para a máquina virtual de saudação sobre toobe criado.

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
Finalmente, o trecho de código anterior Olá cria uma máquina virtual que utiliza todos os recursos de saudação provisionados já. Eles são uma conta de armazenamento e um contêiner para um VHD, uma interface de rede pública IP e sub-rede especificada, e o grupo de recursos Olá já criado. Observe a propriedade de vm_size hello, onde o script hello Especifica um SKU de A0 do Azure.

### <a name="execute-hello-script"></a>Execute o script hello
Com script completo Olá salvo, sair da linha de comando do console de toohello e digite Olá a seguir:
```
terraform apply terraformscripts
```
Depois de algum tempo, os recursos de hello, incluindo uma máquina virtual, são exibidos no hello `terraformtest` grupo de recursos em Olá portal do Azure.

## <a name="complete-terraform-script"></a>Script completo do Terraform

Para sua conveniência, abaixo é Olá completa Terraform script que provisiona toda a infra-estrutura de saudação discutidos neste artigo.

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

## <a name="next-steps"></a>Próximas etapas
Você criou a infraestrutura básica no Azure usando o Terraform. Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples). Para obter uma lista atualizada de provedores do Azure com suporte, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).
