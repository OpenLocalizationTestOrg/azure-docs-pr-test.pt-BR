---
title: "Olá aaaUsing extensão da VM Docker para Linux no Azure"
description: "Descreve o Docker e extensões de máquinas virtuais do Azure hello e mostra como tooprogrammatically criar máquinas virtuais no Azure são hosts de docker da linha de comando de saudação usando Olá CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="a34db-103">Usando a extensão da VM Docker de saudação do hello Azure Interface de linha de comando (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="a34db-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="a34db-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a34db-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a34db-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a34db-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a34db-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a34db-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a34db-107">Para obter informações sobre como usar a extensão de VM Docker Olá com o modelo do Gerenciador de recursos de hello, consulte [aqui](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a34db-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a34db-108">Este tópico descreve como toocreate uma VM com Olá extensão da VM Docker do hello serviço modo de gerenciamento (asm) em CLI do Azure em qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="a34db-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="a34db-109">[Docker](https://www.docker.com/) é uma saudação mais populares abordagens de virtualização que usa [contêineres Linux](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como um modo de isolamento de dados e computação em recursos compartilhados.</span><span class="sxs-lookup"><span data-stu-id="a34db-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="a34db-110">Você pode usar a extensão de VM Docker hello e hello [agente Linux do Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate uma VM Docker que hospeda qualquer número de contêineres para seus aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="a34db-111">toosee uma discussão detalhada sobre contêineres e suas vantagens, consulte Olá [Docker alto nível de quadro](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="a34db-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="a34db-112">Como toouse Olá extensão da VM Docker com o Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="a34db-113">extensão de VM Docker toouse Olá com o Azure, você deve instalar uma versão de hello [Interface de linha de comando do Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI do Azure) maior do que 0.8.6 (como de saudação esta gravação atual versão 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="a34db-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="a34db-114">Você pode instalar Olá CLI do Azure no Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="a34db-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="a34db-115">Olá processo completo toouse Docker no Azure é simple:</span><span class="sxs-lookup"><span data-stu-id="a34db-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="a34db-116">Instalar Olá CLI do Azure e suas dependências no computador de saudação do qual você deseja toocontrol do Azure (no Windows, isso será uma distribuição do Linux em execução como uma máquina virtual)</span><span class="sxs-lookup"><span data-stu-id="a34db-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="a34db-117">Usar o hello Azure CLI Docker comandos toocreate um host de VM Docker no Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="a34db-118">Use Olá local Docker comandos toomanage seus contêineres de Docker em sua VM Docker no Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="a34db-119">Instalar hello Azure Interface de linha de comando (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="a34db-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="a34db-120">tooinstall e configurar Olá CLI do Azure, consulte [como tooinstall Olá Interface de linha de comando do Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a34db-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="a34db-121">instalação de saudação tooconfirm, tipo `azure` no prompt de comando do hello e após um breve momento você deve ver Olá arte ASCII de CLI do Azure, que lista Olá basic comandos tooyou disponível.</span><span class="sxs-lookup"><span data-stu-id="a34db-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="a34db-122">Se instalação Olá funcionou corretamente, você deve ser capaz de tootype `azure help vm` e ver se um dos comandos de saudação listado é "docker".</span><span class="sxs-lookup"><span data-stu-id="a34db-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-123">Docker tem as ferramentas do Windows, [Docker máquina](https://docs.docker.com/installation/windows/), que você também pode usar a criação de um cliente do docker que você pode usar toowork com VMs do Azure como hosts de docker Olá tooautomate.</span><span class="sxs-lookup"><span data-stu-id="a34db-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="a34db-124">Conecte-se Olá CLI do Azure tootooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="a34db-125">Antes de usar o hello CLI do Azure, você deve associar suas credenciais de conta do Azure com hello CLI do Azure em sua plataforma.</span><span class="sxs-lookup"><span data-stu-id="a34db-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="a34db-126">Olá seção [como tooconnect tooyour assinatura do Azure](../../../xplat-cli-connect.md) explica como tooeither baixar e importar sua **. publishsettings** arquivo ou associar a CLI do Azure com uma id organizacional.</span><span class="sxs-lookup"><span data-stu-id="a34db-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-127">Há algumas diferenças no comportamento quando um ou hello outros métodos de autenticação, então ser se tooread Olá documento acima funcionalidade diferente do toounderstand hello.</span><span class="sxs-lookup"><span data-stu-id="a34db-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="a34db-128">Instalar o Docker e usar Olá extensão da VM Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="a34db-129">Siga Olá [instruções de instalação do Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a34db-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="a34db-130">toouse Docker com uma máquina Virtual do Azure, imagem do Linux Olá usada para Olá VM deve ter Olá [agente de VM do Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) instalado.</span><span class="sxs-lookup"><span data-stu-id="a34db-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="a34db-131">No momento, apenas dois tipos de imagens possibilitam isso:</span><span class="sxs-lookup"><span data-stu-id="a34db-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="a34db-132">Uma imagem do Ubuntu de saudação Galeria de imagens do Azure ou</span><span class="sxs-lookup"><span data-stu-id="a34db-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="a34db-133">Uma imagem personalizada do Linux que você criou com hello agente de VM do Linux do Azure instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="a34db-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="a34db-134">Consulte [agente de VM do Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como toobuild uma VM do Linux personalizado com hello Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="a34db-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="a34db-135">Usando a Galeria de imagens do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="a34db-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="a34db-136">A partir de uma sessão de Terminal ou Bash, usar Olá comando CLI do Azure toolocate Olá imagem Ubuntu mais recente no hello VM Galeria toouse digitando a seguir</span><span class="sxs-lookup"><span data-stu-id="a34db-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="a34db-137">e selecione um dos nomes de imagem hello, como `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, e o comando a seguir do uso Olá toocreate uma nova VM usando essa imagem.</span><span class="sxs-lookup"><span data-stu-id="a34db-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="a34db-138">onde:</span><span class="sxs-lookup"><span data-stu-id="a34db-138">where:</span></span>

* <span data-ttu-id="a34db-139">*&lt;nome de VM cloudservice&gt;*  é nome de saudação do hello VM que se tornará o computador de host de contêiner Olá Docker no Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="a34db-140">*&lt;nome de usuário&gt;*  é o nome de usuário de saudação do usuário de raiz de padrão de saudação do hello VM</span><span class="sxs-lookup"><span data-stu-id="a34db-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="a34db-141">*&lt;senha&gt;*  é a senha Olá Olá *username* conta que atende aos padrões de saudação de complexidade do Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-142">Atualmente, a senha deve ter pelo menos 8 caracteres, conter minúscula e maiuscula caracteres, um número e um caractere especial, como um dos seguintes caracteres de saudação: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="a34db-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="a34db-143">Não, o período Olá final Olá Olá anterior frase não é um caractere especial.</span><span class="sxs-lookup"><span data-stu-id="a34db-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="a34db-144">Se o comando Olá foi bem-sucedida, você verá algo parecido com hello seguinte, dependendo de argumentos preciso hello e opções que você usou:</span><span class="sxs-lookup"><span data-stu-id="a34db-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="a34db-145">Criando uma máquina virtual pode levar alguns minutos, mas depois foi provisionado (valor de estado de saudação é `ReadyRole`) Olá inicia do Docker daemon (Olá serviço do Docker) e você pode conectar o host do contêiner Docker toohello.</span><span class="sxs-lookup"><span data-stu-id="a34db-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="a34db-146">Olá tootest VM Docker que você criou no Azure, o tipo</span><span class="sxs-lookup"><span data-stu-id="a34db-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="a34db-147">onde  *&lt;vm-nome-você-usado&gt;*  é Olá nome da máquina virtual Olá usado na sua chamada muito`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="a34db-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="a34db-148">Você verá algo semelhante toohello seguinte, que indica que a VM do Host do Docker está ativo e em execução no Azure e aguardando seus comandos.</span><span class="sxs-lookup"><span data-stu-id="a34db-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="a34db-149">Agora você pode tentar tooconnect usando suas informações de tooobtain de cliente do docker (em algumas configurações de cliente do Docker, como no Mac, talvez seja necessário toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="a34db-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="a34db-150">Apenas toobe certeza de que ele é funcionar, você pode examinar hello VM para Olá extensão Docker:</span><span class="sxs-lookup"><span data-stu-id="a34db-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="a34db-151">Autenticação da máquina virtual host do Docker</span><span class="sxs-lookup"><span data-stu-id="a34db-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="a34db-152">Além disso toocreating Olá VM Docker, Olá `azure vm docker create` comando também cria automaticamente Olá certificados necessários tooallow seu host do contêiner do Azure Docker cliente computador tooconnect toohello usando HTTPS, e Olá certificados são armazenados nos dois Olá máquinas cliente e host, conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="a34db-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="a34db-153">Nas tentativas subsequentes, certificados existentes Olá são reutilizados e compartilhados com o novo host de saudação.</span><span class="sxs-lookup"><span data-stu-id="a34db-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="a34db-154">Por padrão, os certificados são colocados em `~/.docker`, e o Docker será toorun configurado na porta **2376**.</span><span class="sxs-lookup"><span data-stu-id="a34db-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="a34db-155">Se você gostaria que toouse uma porta diferente ou diretório, você pode usar um dos seguintes Olá `azure vm docker create` opções de linha de comando tooconfigure o Docker contêiner host VM toouse uma porta diferente ou certificados diferentes para conectar clientes:</span><span class="sxs-lookup"><span data-stu-id="a34db-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="a34db-156">Olá daemon do Docker no host de saudação é toolisten configurado para e autenticar o cliente conexões Olá especificado usando certificados de saudação de porta gerado pelo Olá `azure vm docker create` comando.</span><span class="sxs-lookup"><span data-stu-id="a34db-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="a34db-157">Olá cliente deve ter esses certificados toogain acessar toohello Docker host.</span><span class="sxs-lookup"><span data-stu-id="a34db-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-158">Um host de rede em execução sem esses certificados serão tooanyone vulnerável que pode tooconnect toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="a34db-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="a34db-159">Antes de modificar a configuração padrão de saudação, certifique-se de que entendeu Olá riscos tooyour computadores e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a34db-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a34db-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a34db-160">Next steps</span></span>
* <span data-ttu-id="a34db-161">Você está pronto toogo toohello [guia do usuário do Docker] e usar sua VM Docker.</span><span class="sxs-lookup"><span data-stu-id="a34db-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="a34db-162">toocreate uma VM Docker habilitado no novo portal de hello, consulte [como toouse Olá extensão da VM Docker com hello Portal].</span><span class="sxs-lookup"><span data-stu-id="a34db-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="a34db-163">Olá extensão VM Docker do Azure também oferece suporte a redação do Docker, que usa um tootake de arquivo YAML declarativa um aplicativo modelada desenvolvedor em qualquer ambiente e gerar uma implantação consistente.</span><span class="sxs-lookup"><span data-stu-id="a34db-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="a34db-164">Consulte [Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure].</span><span class="sxs-lookup"><span data-stu-id="a34db-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[como toouse Olá extensão da VM Docker com hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[guia do usuário do Docker]:https://docs.docker.com/userguide/

[Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure]:../docker-compose-quickstart.md
