---
title: aaaUse Docker Compose em uma VM do Linux no Azure | Microsoft Docs
description: "Como toouse Docker e compor em máquinas virtuais Linux Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Obter Introdução ao Docker e compor toodefine e executar um aplicativo de contêiner vários no Azure
Com [redigir](http://github.com/docker/compose), você usar um toodefine do arquivo de texto simples, um aplicativo que consiste em vários contêineres de Docker. Em seguida, você criar seu aplicativo em um único comando que faz toodeploy seu ambiente definido. Por exemplo, este artigo mostra como tooquickly configurado um blog do WordPress com um back-end banco de dados SQL MariaDB em uma VM do Ubuntu. Você também pode usar tooset compor aplicativos mais complexos.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configurar uma VM Linux como um host do Docker
Você pode usar vários procedimentos do Azure e as imagens disponíveis ou modelos do Gerenciador de recursos no Azure Marketplace de saudação toocreate uma VM do Linux e configurá-lo como um host Docker. Por exemplo, consulte [usando Olá extensão da VM Docker toodeploy seu ambiente](dockerextension.md) tooquickly criar uma VM Ubuntu com hello extensão VM Docker do Azure usando um [quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Quando você usa a extensão de VM Docker hello, sua VM é automaticamente configurada como um host Docker e compor já está instalado.


### <a name="create-docker-host-with-azure-cli-20"></a>Criar host do Docker com a CLI do Azure 2.0
Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).

Primeiro, crie um grupo de recursos para seu ambiente do Docker com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local:

```azurecli
az group create --name myResourceGroup --location westus
```

Em seguida, implantar uma VM com [criar implantação de grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker de saudação do [este modelo do Gerenciador de recursos do Azure no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Forneça seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Leva alguns minutos para Olá toofinish de implantação. Quando terminar de implantação Olá, [mover etapa toonext](#verify-that-compose-is-installed) tooSSH tooyour VM. 

Opcionalmente, a solicitação de toohello de controle de retorno de tooinstead e implantação Olá permitem continuar no plano de fundo Olá, adicione Olá `--no-wait` sinalizador toohello antes do comando. Esse processo permite que você tooperform outro trabalho no hello CLI interromper a implantação de saudação por alguns minutos. Você pode exibir detalhes sobre o status do host Docker Olá com [Mostrar de vm az](/cli/azure/vm#show). Olá, exemplo a seguir verifica o status de saudação do hello VM denominada *myDockerVM* (Olá nome padrão do modelo hello, não altere esse nome) no grupo de recursos de saudação denominado *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Quando esse comando retorna *êxito*, Olá implantação for concluída e você poderá SSH toohello VM em Olá etapa a seguir.


## <a name="verify-that-compose-is-installed"></a>Verificar se o Compose está instalado
Quando terminar de implantação Olá, SSH tooyour novo host do Docker usando o nome DNS de saudação que você forneceu durante a implantação. Você pode usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalhes de sua VM, incluindo o nome DNS hello.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck compor estiver instalado em Olá VM, execute Olá comando a seguir:

```bash
docker-compose --version
```

Você verá uma saída semelhante muito*docker-compor 1.6.2, crie 4d 72027*.

> [!TIP]
> Se você tiver usado outro método toocreate um host Docker e precisa tooinstall redigir por conta própria, consulte Olá [compor documentação](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Criar um arquivo de configuração docker-compose.yml
Agora você criará um `docker-compose.yml` arquivo, que é apenas um arquivo de configuração de texto, toodefine Olá Docker contêineres toorun em Olá VM. arquivo Hello Especifica Olá imagem toorun em cada contêiner (ou pode ser uma compilação de um Dockerfile), variáveis de ambiente necessários e dependências, portas e links de saudação entre contêineres. Para obter detalhes sobre a sintaxe do arquivo yml, veja a [referência de arquivo do Redigir](https://docs.docker.com/compose/compose-file/).

Criar hello *docker compose.yml* arquivos da seguinte maneira:

```bash
touch docker-compose.yml
```

Use o tooadd do editor de texto favorito algum arquivo toohello de dados. Olá, exemplo a seguir usa Olá *vi* editor:

```bash
vi docker-compose.yml
```

Cole o exemplo a seguir em seu arquivo de texto de saudação. Essa configuração usa imagens de saudação [DockerHub registro](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Olá código-fonte aberto blogs e conteúdo do sistema de gerenciamento) e um back-end vinculado MariaDB SQL de banco de dados. Insira seu próprio *MYSQL_ROOT_PASSWORD* da seguinte maneira:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Contêineres de saudação inicial com redigir
Em Olá mesmo diretório como o *docker compose.yml* arquivo, execute o comando a seguir de saudação (dependendo do seu ambiente, talvez seja necessário toorun `docker-compose` usando `sudo`):

```bash
docker-compose up -d
```

Esse comando inicia a contêineres do Docker Olá especificados em *docker compose.yml*. Ele usa um ou dois minutos para toocomplete esta etapa. Você verá a saída toohello semelhante exemplo a seguir:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Ser Olá-se de toouse **-d** opção na inicialização para que os contêineres de saudação executado continuamente no plano de fundo de saudação.


tooverify que são contêineres hello, tipo `docker-compose ps`. Você deve ver algo como:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Agora você pode conectar tooWordPress diretamente no hello VM na porta 80. Abra um navegador da web e digite o nome DNS de saudação da VM (como `http://mypublicdns.westus.cloudapp.azure.com`). Agora você deve ver Olá que WordPress iniciar tela, onde você pode concluir a instalação de saudação e introdução ao aplicativo hello.

![Tela inicial do WordPress][wordpress_start]

## <a name="next-steps"></a>Próximas etapas
* Vá toohello [guia do usuário de extensão de VM Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obter mais opções tooconfigure Docker e compor em sua VM Docker. Por exemplo, uma opção é tooput Olá redigir yml arquivo (tooJSON convertido) diretamente na configuração Olá Olá extensão da VM Docker.
* Check-out Olá [compõem a referência de linha de comando](http://docs.docker.com/compose/reference/) e [guia do usuário](http://docs.docker.com/compose/) para obter mais exemplos de criação e implantação de aplicativos de contêiner vários.
* Usar um modelo do Gerenciador de recursos do Azure, sua própria ou uma contribuição de saudação [community](https://azure.microsoft.com/documentation/templates/), toodeploy uma VM do Azure com o Docker e um aplicativo configurado com redação. Por exemplo, Olá [implantar um blog do WordPress com o Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) Docker usa o modelo e compor tooquickly implantar WordPress com um back-end do MySQL em uma VM do Ubuntu.
* Tente integrar o Docker Compose com um cluster do Docker Swarm. Veja [Using Compose with Swarm (Uso do Redigir com o Swarm)](https://docs.docker.com/compose/swarm/) para obter os cenários.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
