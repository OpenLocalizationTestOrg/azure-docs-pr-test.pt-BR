---
title: "hospeda aaaUse Docker máquina toocreate Linux no Azure | Microsoft Docs"
description: "Descreve como toouse Docker máquina toocreate Docker hospeda no Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="bde71-103">Como toouse Docker máquina toocreate hospeda no Azure</span><span class="sxs-lookup"><span data-stu-id="bde71-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="bde71-104">Este artigo detalhes como toouse [Docker máquina](https://docs.docker.com/machine/) toocreate hosts no Azure.</span><span class="sxs-lookup"><span data-stu-id="bde71-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="bde71-105">Olá `docker-machine` comando cria uma máquina virtual do Linux (VM) no Azure, em seguida, instala o Docker.</span><span class="sxs-lookup"><span data-stu-id="bde71-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="bde71-106">Você pode gerenciar seus hosts de Docker no Azure usando Olá mesmas ferramentas locais e fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bde71-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="bde71-107">Criar VMs com o computador Docker</span><span class="sxs-lookup"><span data-stu-id="bde71-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="bde71-108">Primeiro, obtenha a ID da assinatura do Azure com [az account show](/cli/azure/account#show) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bde71-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="bde71-109">Criar VMs de host do Docker no Azure com `docker-machine create` especificando *azure* como driver hello.</span><span class="sxs-lookup"><span data-stu-id="bde71-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="bde71-110">Para obter mais informações, consulte Olá [documentação do Driver do Docker do Azure](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="bde71-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="bde71-111">Olá, exemplo a seguir cria uma VM denominada *myVM*, cria uma conta de usuário chamada *azureuser*e abre a porta *80* em Olá host de VM.</span><span class="sxs-lookup"><span data-stu-id="bde71-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="bde71-112">Execute qualquer toolog prompts no tooyour conta do Azure e conceder máquina Docker permissões toocreate e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="bde71-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="bde71-113">saída de Hello parece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bde71-113">hello output looks similar toohello following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="bde71-114">Configurar o shell do Docker</span><span class="sxs-lookup"><span data-stu-id="bde71-114">Configure your Docker shell</span></span>
<span data-ttu-id="bde71-115">host do Docker tooyour tooconnect no Azure, definir configurações de conexão apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="bde71-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="bde71-116">Como observado no fim de saudação da saída de hello, exiba informações de conexão Olá para o host do Docker, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bde71-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="bde71-117">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bde71-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="bde71-118">configurações de conexão de saudação toodefine pode qualquer execução Olá sugerido comando de configuração (`eval $(docker-machine env myvmdocker)`), ou você pode definir variáveis de ambiente Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="bde71-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="bde71-119">Executar um contêiner</span><span class="sxs-lookup"><span data-stu-id="bde71-119">Run a container</span></span>
<span data-ttu-id="bde71-120">toosee um contêiner em ação, permite executar um servidor de Web NGINX básica.</span><span class="sxs-lookup"><span data-stu-id="bde71-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="bde71-121">Crie um contêiner com `docker run` e exponha a porta 80 para o tráfego da Web da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bde71-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="bde71-122">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bde71-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="bde71-123">Exiba os contêineres em execução com `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="bde71-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="bde71-124">Olá, saída de exemplo a seguir mostra Olá contêiner NGINX em execução com a porta 80 expostos:</span><span class="sxs-lookup"><span data-stu-id="bde71-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="bde71-125">Contêiner de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="bde71-125">Test hello container</span></span>
<span data-ttu-id="bde71-126">Obtenha o endereço IP público de saudação do host do Docker da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bde71-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="bde71-127">contêiner de saudação toosee em ação, abra um navegador da web e digite o endereço IP público Olá observado na saída Olá Olá precede o comando:</span><span class="sxs-lookup"><span data-stu-id="bde71-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![Contêiner ngnix em execução](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="bde71-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bde71-129">Next steps</span></span>
<span data-ttu-id="bde71-130">Você também pode criar hosts com hello [extensão da VM Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="bde71-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="bde71-131">Para obter exemplos de como usar o Docker Compose, consulte [Introdução ao Docker e ao Compose no Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="bde71-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
