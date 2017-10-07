---
title: "Olá aaaUse extensão VM Docker do Azure com hello 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toouse Olá tooquickly de extensão de VM Docker e implantar com segurança um ambiente de Docker no Azure usando o Gerenciador de recursos de modelos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Criar um ambiente de Docker no Azure com extensão de VM Docker Olá Olá 1.0 da CLI do Azure
O docker é uma plataforma geração de imagens que permite que você tooquickly o trabalho com contêineres do Linux (e também do Windows) e o gerenciamento de contêiner populares. No Azure, há várias maneiras que você pode implantar o Docker de acordo com as necessidades de tooyour. Este artigo enfoca usando a extensão de VM Docker hello e modelos do Gerenciador de recursos do Azure. 

Para obter mais informações sobre métodos de implantação diferentes hello, incluindo o uso de máquina do Docker e serviços de contêiner do Azure, consulte Olá artigos a seguir:

* protótipo tooquickly um aplicativo, você pode criar um único host Docker usando [Docker máquina](docker-machine.md).
* Em ambientes maiores e mais estáveis, você pode usar a extensão de VM do Azure Docker hello, que também oferece suporte a [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate implantações de contêiner consistente. Este artigo detalha usando a extensão de VM do Azure Docker hello.
* toobuild ambientes de pronto para produção e escalonável que fornece ferramentas adicionais de planejamento e gerenciamento, você pode implantar um [Docker Swarm cluster nos serviços de contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#azure-docker-vm-extension-overview) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](dockerextension.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação 

## <a name="azure-docker-vm-extension-overview"></a>Visão geral da extensão de VM do Docker do Azure
Olá extensão VM Docker do Azure instala e configura o daemon do Docker hello, cliente do Docker e compor Docker em sua máquina virtual do Linux (VM). Usando a extensão de VM do Azure Docker hello, você tem mais controle e recursos do que simplesmente usando o Docker máquina ou criação de host do Docker Olá por conta própria. Adicionais esses recursos, tais como [Docker Compose](https://docs.docker.com/compose/overview/), tornar extensão de VM Docker do Azure Olá adequada para ambientes de produção ou desenvolvedor mais robustos.

Modelos do Gerenciador de recursos do Azure definem a estrutura inteira saudação do seu ambiente. Modelos permitem toocreate e configurar recursos como host do Docker Olá máquinas virtuais, armazenamento, controles de acesso baseado em função (RBAC) e diagnóstico. Você pode reutilizar essas implantações adicionais de toocreate modelos de maneira consistente. Para obter mais informações sobre o Azure Resource Manager e modelos, veja a [Visão geral do Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Implantar um modelo com hello extensão VM Docker do Azure
Vamos usar um existente toocreate de modelo de início rápido um Ubuntu VM que utilize Olá tooinstall de extensão de VM Docker do Azure e configurar o host do Docker hello. Você pode exibir o modelo de saudação aqui: [implantação simples de uma VM Ubuntu com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Você precisa Olá [CLI do Azure mais recentes](../../cli-install-nodejs.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:

```azurecli
azure config mode arm
```

Implante o modelo de saudação usando Olá CLI do Azure, especificando o modelo de saudação URI. Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local. Use seu próprio nome de grupo de recursos e local da seguinte maneira:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Responder Olá prompts tooname sua conta de armazenamento, forneça um nome de usuário e a senha e forneça um nome DNS. saudação de saída é similar toohello exemplo a seguir:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Olá CLI do Azure retorna toohello prompt após alguns segundos, mas o host do Docker ainda está sendo criado e configurado por Olá extensão VM Docker do Azure. Leva alguns minutos para Olá toofinish de implantação. Você pode exibir detalhes sobre o status de host do Docker hello usando Olá `azure vm show` comando.

Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*. Digite o nome de Olá Olá do grupo de recursos criado na saudação anterior etapa:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Olá saída de hello `azure vm show` comando é semelhante toohello exemplo a seguir:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Topo Olá da saída de hello, você verá Olá **ProvisioningState** de saudação VM. Quando exibe *êxito*, Olá implantação for concluída e você pode SSH toohello VM.

Final de saudação da saída de hello *FQDN* exibe o nome de domínio totalmente qualificado de saudação do seu host do Docker. O FQDN é o que você use host do Docker tooyour tooSSH em Olá restantes etapas.

## <a name="deploy-your-first-nginx-container"></a>Implantar seu primeiro contêiner nginx
Uma vez Olá implantação for concluída, SSH tooyour novo host do Docker do computador local. Insira seu próprio nome de usuário e o FQDN da seguinte maneira:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

Depois de conectado toohello host Docker, vamos executar um contêiner nginx:

```bash
sudo docker run -d -p 80:80 nginx
```

saída de Hello é semelhante toohello exemplo a seguir como Olá nginx imagem é baixada e um contêiner iniciado:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Verifique o status de saudação de contêineres de saudação em execução no host do Docker da seguinte maneira:

```bash
sudo docker ps
```

saída de Hello é semelhante toohello exemplo a seguir, mostrando o contêiner Olá nginx está em execução e as portas TCP 80 e 443 e encaminhadas:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee seu contêiner em ação, abra um navegador da web e digite o nome FQDN de saudação do seu host do Docker:

![Contêiner ngnix em execução](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Referência de modelo da extensão de VM do Docker do Azure
exemplo de Hello anterior usa um modelo existente do guia de início rápido. Você também pode implantar a extensão de VM do Azure Docker Olá com seus próprios modelos do Gerenciador de recursos. toodo, então, adicionar Olá tooyour modelos de Gerenciador de recursos a seguir, a definição de saudação *vmName* da VM adequadamente:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Você pode encontrar um passo a passo mais detalhado de como usar modelos do Gerenciador de Recursos lendo a [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Próximas etapas
Pode ser muito[configurar Olá Docker daemon TCP porta](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), entender [segurança de Docker](https://docs.docker.com/engine/security/security/), ou implantar contêineres usando [Docker Compose](https://docs.docker.com/compose/overview/). Para obter mais informações sobre Olá extensão da VM Docker do Azure em si, consulte Olá [GitHub projeto](https://github.com/Azure/azure-docker-extension/).

Ler mais informações sobre as opções implantação Docker de saudação adicionais no Azure:

* [Use Docker máquina com hello driver do Azure](docker-machine.md)  
* [Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure](docker-compose-quickstart.md).
* [Implantar um cluster do Serviço de Contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md)

