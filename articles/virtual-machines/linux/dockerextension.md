---
title: "Olá aaaUse extensão VM Docker do Azure | Microsoft Docs"
description: "Saiba como toouse Olá tooquickly de extensão de VM Docker e com segurança implantar um ambiente de Docker no Azure usando o Gerenciador de recursos de modelos e Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Criar um ambiente de Docker no Azure usando a extensão de VM Docker Olá
O docker é uma plataforma de geração de imagens que permite que você tooquickly o trabalho com contêineres no Linux e o gerenciamento de contêiner populares. No Azure, há várias maneiras que você pode implantar o Docker de acordo com as necessidades de tooyour. Este artigo enfoca usando a extensão de VM Docker hello e modelos do Gerenciador de recursos do Azure com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Visão geral da extensão de VM do Docker do Azure
Olá extensão VM Docker do Azure instala e configura o daemon do Docker hello, cliente do Docker e compor Docker em sua máquina virtual do Linux (VM). Usando a extensão de VM do Azure Docker hello, você tem mais controle e recursos do que simplesmente usando o Docker máquina ou criação de host do Docker Olá por conta própria. Adicionais esses recursos, tais como [Docker Compose](https://docs.docker.com/compose/overview/), tornar extensão de VM Docker do Azure Olá adequada para ambientes de produção ou desenvolvedor mais robustos.

Para obter mais informações sobre métodos de implantação diferentes hello, incluindo o uso de máquina do Docker e serviços de contêiner do Azure, consulte Olá artigos a seguir:

* protótipo tooquickly um aplicativo, você pode criar um único host Docker usando [Docker máquina](docker-machine.md).
* toobuild ambientes de pronto para produção e escalonável que fornece ferramentas adicionais de planejamento e gerenciamento, você pode implantar um [Docker Swarm cluster nos serviços de contêiner do Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Implantar um modelo com hello extensão VM Docker do Azure
Vamos usar um existente toocreate de modelo de início rápido um Ubuntu VM que utilize Olá tooinstall de extensão de VM Docker do Azure e configurar o host do Docker hello. Você pode exibir o modelo de saudação aqui: [implantação simples de uma VM Ubuntu com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local:

```azurecli
az group create --name myResourceGroup --location westus
```

Em seguida, implantar uma VM com [criar implantação de grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker de saudação do [este modelo do Gerenciador de recursos do Azure no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* da seguinte maneira:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Leva alguns minutos para Olá toofinish de implantação. Quando terminar de implantação Olá, [mover etapa toonext](#deploy-your-first-nginx-container) tooSSH tooyour VM. 

Opcionalmente, a solicitação de toohello de controle de retorno de tooinstead e implantação Olá permitem continuar no plano de fundo Olá, adicione Olá `--no-wait` sinalizador toohello antes do comando. Esse processo permite que você tooperform outro trabalho no hello CLI interromper a implantação de saudação por alguns minutos. 

Você pode exibir detalhes sobre o status do host Docker Olá com [Mostrar de vm az](/cli/azure/vm#show). Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Quando esse comando retorna *êxito*, Olá implantação for concluída e você poderá SSH toohello VM em Olá etapa a seguir.

## <a name="deploy-your-first-nginx-container"></a>Implantar seu primeiro contêiner nginx
tooview detalhes da VM, incluindo nome DNS hello, usam `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour Docker novo host do computador local da seguinte maneira:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
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

toosee seu contêiner em ação, abra um navegador da web e digite o nome DNS de saudação do seu host do Docker:

![Contêiner ngnix em execução](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Referência de modelo da extensão de VM do Docker do Azure
exemplo de Hello anterior usa um modelo existente do guia de início rápido. Você também pode implantar a extensão de VM do Azure Docker Olá com seus próprios modelos do Gerenciador de recursos. toodo, então, adicionar Olá tooyour modelos de Gerenciador de recursos a seguir, a definição de saudação `vmName` da VM adequadamente:

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
    "typeHandlerVersion": "1.*",
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

