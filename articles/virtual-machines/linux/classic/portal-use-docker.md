---
title: "aaaUsing extensão da VM Docker para Linux | Microsoft Docs"
description: "Descreve como toocreate máquinas virtuais do Azure que são hosts de docker usando Olá CLI do Azure no modelo de implantação clássico e extensões de máquinas virtuais do Azure hello e Docker."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="f25df-103">Usando Olá extensão da VM Docker com hello portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f25df-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f25df-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f25df-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f25df-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="f25df-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f25df-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f25df-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f25df-107">[Docker](https://www.docker.com/) é uma saudação mais populares abordagens de virtualização que usa [contêineres Linux](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como um modo de isolamento de dados e computação em recursos compartilhados.</span><span class="sxs-lookup"><span data-stu-id="f25df-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="f25df-108">Você pode usar a extensão de VM Docker Olá gerenciado pelo [agente Linux do Azure] toocreate uma VM Docker que hospeda qualquer número de contêineres para seus aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="f25df-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f25df-109">Este tópico descreve como toocreate uma VM Docker do hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f25df-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="f25df-110">toosee como toocreate uma VM Docker na linha de comando hello, consulte [como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)].</span><span class="sxs-lookup"><span data-stu-id="f25df-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="f25df-111">toosee uma discussão detalhada sobre contêineres e suas vantagens, consulte Olá [Docker alto nível de quadro](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="f25df-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="f25df-112">Criar uma nova VM da Galeria de imagens de saudação</span><span class="sxs-lookup"><span data-stu-id="f25df-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="f25df-113">Olá primeira etapa exige uma VM do Azure de uma imagem do Linux que oferece suporte a saudação extensão da VM Docker, usando uma imagem do Ubuntu 14.04 LTS de saudação Galeria de imagens como uma imagem de servidor de exemplo e área de trabalho do Ubuntu 14.04 como um cliente.</span><span class="sxs-lookup"><span data-stu-id="f25df-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="f25df-114">No portal de saudação, clique em **+ novo** no hello inferior esquerda canto toocreate uma nova instância de máquina virtual e selecione uma imagem Ubuntu 14.04 LTS de seleções de saudação disponíveis ou de saudação concluir a Galeria de imagens, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f25df-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="f25df-115">Atualmente, apenas imagens de Ubuntu 14.04 LTS mais recentes do que de julho de 2014 aceita Olá extensão da VM Docker.</span><span class="sxs-lookup"><span data-stu-id="f25df-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Criar uma nova imagem Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="f25df-117">Criar certificados Docker</span><span class="sxs-lookup"><span data-stu-id="f25df-117">Create Docker Certificates</span></span>
<span data-ttu-id="f25df-118">Após Olá que VM foi criada, certifique-se de que o Docker é instalado no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="f25df-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="f25df-119">Para obter detalhes, confira [Instruções de instalação do Docker](https://docs.docker.com/installation/#installation).</span><span class="sxs-lookup"><span data-stu-id="f25df-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="f25df-120">Criar hello arquivos de certificado e a chave para comunicação do Docker de acordo com muito[Docker em execução com https] e colocá-los em Olá  **`~/.docker`**  diretório no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="f25df-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="f25df-121">Olá extensão da VM Docker no portal de saudação atualmente requer credenciais que são codificados na base64.</span><span class="sxs-lookup"><span data-stu-id="f25df-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="f25df-122">Na linha de comando hello, use  **`base64`**  ou favorito outra codificação tópicos sobre a ferramenta toocreate codificado na base64.</span><span class="sxs-lookup"><span data-stu-id="f25df-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="f25df-123">Fazer isso com um conjunto simple de arquivos de certificado e chave pode parecer semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="f25df-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="f25df-124">Adicionar Olá extensão da VM Docker</span><span class="sxs-lookup"><span data-stu-id="f25df-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="f25df-125">tooadd Olá extensão da VM Docker, localize a instância VM Olá criada e role para baixo demais**extensões** e clique toobring a extensões de VM, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="f25df-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="f25df-126">Essa funcionalidade é suportada no portal de visualização de saudação apenas: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="f25df-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="f25df-127">Adicionar uma extensão</span><span class="sxs-lookup"><span data-stu-id="f25df-127">Add an Extension</span></span>
<span data-ttu-id="f25df-128">Clique em Olá **+ adicionar** toodisplay Olá possíveis extensões de VM, você pode adicionar toothis VM.</span><span class="sxs-lookup"><span data-stu-id="f25df-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="f25df-129">Selecione Olá extensão da VM Docker</span><span class="sxs-lookup"><span data-stu-id="f25df-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="f25df-130">Escolha Olá extensão da VM Docker, que traz links importantes e descrição de Docker Olá, e, em seguida, clique em **criar** no procedimento de instalação do hello inferior toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="f25df-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="f25df-131">Adicionar seus arquivos de certificado e de chaves:</span><span class="sxs-lookup"><span data-stu-id="f25df-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="f25df-132">Olá campos de formulário, insira versões codificada em base64 de saudação do seu certificado de autoridade de certificação, o certificado de servidor e a chave do servidor, conforme mostrado no gráfico a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f25df-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="f25df-133">Observe que (como saudação anterior imagem) Olá 2376 é preenchido por padrão.</span><span class="sxs-lookup"><span data-stu-id="f25df-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="f25df-134">Você pode inserir qualquer ponto de extremidade aqui, mas Olá próximo passo será tooopen backup Olá correspondência de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f25df-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="f25df-135">Se você alterar o padrão de hello, verifique se tooopen backup Olá correspondência na próxima etapa de saudação do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f25df-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="f25df-136">Adicionar Olá ponto de extremidade de comunicação de Docker</span><span class="sxs-lookup"><span data-stu-id="f25df-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="f25df-137">Ao exibir o grupo de recursos de saudação que você criou, selecione Olá grupo de segurança de rede associado a sua VM e clique em **regras de segurança de entrada** tooview Olá regras conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="f25df-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="f25df-138">Clique em **+ adicionar** tooadd outra regra e no caso de padrão de saudação, insira um nome para o ponto de extremidade de saudação (neste exemplo, **Docker**) e 2376 'intervalo de porta de destino'.</span><span class="sxs-lookup"><span data-stu-id="f25df-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="f25df-139">Definir mostrando de valor de protocolo hello **TCP**e clique em **Okey** toocreate regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="f25df-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="f25df-140">Testar o cliente Docker e o host Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="f25df-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="f25df-141">Localize e copie Olá nome de domínio da VM e na linha de comando de saudação do computador cliente, o tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (onde *dockerextension* é substituído pelo Olá subdomínio para sua VM).</span><span class="sxs-lookup"><span data-stu-id="f25df-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="f25df-142">resultado de saudação deve aparecer toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="f25df-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="f25df-143">Depois de concluir Olá acima etapas, agora você tem um host Docker totalmente funcional em execução em uma VM do Azure, configurado toobe conectado tooremotely de outros clientes.</span><span class="sxs-lookup"><span data-stu-id="f25df-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="f25df-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f25df-144">Next steps</span></span>
<span data-ttu-id="f25df-145">Você está pronto toogo toohello [guia do usuário do Docker] e usar sua VM Docker.</span><span class="sxs-lookup"><span data-stu-id="f25df-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="f25df-146">Se você quiser tooautomate criando hosts de Docker em VMs do Azure por meio da interface de linha de comando, consulte [como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)]</span><span class="sxs-lookup"><span data-stu-id="f25df-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux do Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[Docker em execução com https]:http://docs.docker.com/articles/https/
[guia do usuário do Docker]:https://docs.docker.com/userguide/
