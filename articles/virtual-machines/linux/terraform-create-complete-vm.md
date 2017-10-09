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

# create a resource group if it doesn't exist
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
 provedor de Terraform tooinitialize Olá para o Azure. Alterar o diretório de saudação muito**terraformscripts**, e o comando a seguir saudação do problema:
```
terraform plan
```
Usamos Olá `plan` Terraform comando, que examina os recursos de saudação definidos nos scripts de saudação. Ele compara toohello informações de estado salvas por Terraform e, em seguida, saídas Olá execução planejada _sem_ na verdade criando recursos no Azure. 

Depois de executar o comando anterior hello, você verá algo parecido com hello tela a seguir:

![Plano do Terraform](./media/terraform/tf_plan2.png)

Se tudo estiver correto, provisione esse novo grupo de recursos no Azure, executando Olá seguinte: 
```
terraform apply
```
Em Olá portal do Azure, você deve ver Olá novo vazio grupo de recursos chamado `terraformtest`. Olá seção a seguir, você adiciona que uma máquina virtual e todos os Olá infra-estrutura de suporte para esse grupo de recursos de toohello de máquina virtual.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Provisionar uma VM Ubuntu com o Terraform
Vamos estender uma máquina virtual executada Ubuntu script de Terraform Olá que criamos com detalhes de saudação tooprovision necessário. recursos de saudação provisionado no hello seções a seguir são:

* Uma rede com uma única sub-rede
* Uma placa de interface de rede 
* Uma conta de armazenamento para diagnóstico de máquina virtual Olá
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
script de saudação anterior cria uma rede virtual e uma sub-rede dentro da rede virtual. Observe o grupo de recursos do hello referência toohello que você criou já via "${azurerm_resource_group.helloterraform.name}" na rede virtual hello e definição de subrede hello.

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
trechos de código de script de anterior Olá criar um IP público e uma interface de rede que usa o IP público de saudação criado. Observação Olá referências toosubnet_id e public_ip_address_id. Terraform tem toounderstand inteligência interna que Olá interface de rede tem uma dependência dos recursos de saudação que toobe necessidade criado antes da criação de Olá Olá da interface de rede.

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
Aqui, você criou uma conta de armazenamento. Essa conta de armazenamento é onde a máquina virtual de saudação armazenará seus detalhes de diagnóstico.

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
Finalmente, o trecho de código anterior Olá cria uma máquina virtual que utiliza todos os recursos de saudação provisionados já. Eles são uma conta de armazenamento para diagnóstico de máquina virtual hello, uma interface de rede pública IP e sub-rede especificada, e o grupo de recursos Olá já criado. Observe a propriedade de vm_size hello, onde o script hello Especifica um SKU DS1v2 padrão do Azure.

Você está toosupply necessária uma chave pública SSH. Coloque o valor da chave pública Olá na seção Olá **... INSIRA A CHAVE PÚBLICA OPENSSH AQUI...**  acima. Você pode usar um existente ssh par de chaves ou siga Olá [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) ou [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) par de chaves toogenerate Olá documentação.

### <a name="execute-hello-script"></a>Execute o script hello
Com script completo Olá salvo, sair da linha de comando do console de toohello e digite Olá a seguir:
```
terraform apply
```
Depois de algum tempo, os recursos de hello, incluindo uma máquina virtual, são exibidos no hello `terraformtest` grupo de recursos em Olá portal do Azure.

## <a name="complete-terraform-script"></a>Script completo do Terraform

Para sua conveniência, abaixo é Olá completa Terraform script que provisiona toda a infra-estrutura de saudação discutidos neste artigo.

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

## <a name="next-steps"></a>Próximas etapas
Você criou a infraestrutura básica no Azure usando o Terraform. Para obter cenários mais complexos, incluindo exemplos que usam balanceadores de carga e conjuntos de dimensionamento de máquinas virtuais, confira os vários [exemplos do Terraform para o Azure](https://github.com/hashicorp/terraform/tree/master/examples). Para obter uma lista atualizada de provedores do Azure com suporte, consulte Olá [Terraform documentação](https://www.terraform.io/docs/providers/azurerm/index.html).
