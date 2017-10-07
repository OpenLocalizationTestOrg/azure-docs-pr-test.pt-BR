---
title: aaaCreate um pipeline de desenvolvimento no Azure com Jenkins | Microsoft Docs
description: "Saiba como máquina toocreate um Jenkins virtual no Azure que recebe do GitHub em cada código de confirmação e cria um novo Docker contêiner toorun seu aplicativo"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="11398-103">Como toocreate uma infra-estrutura de desenvolvimento em uma VM do Linux no Azure com Jenkins, GitHub e o Docker</span><span class="sxs-lookup"><span data-stu-id="11398-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="11398-104">tooautomate Olá compilação e teste a fase de desenvolvimento de aplicativos, você pode usar uma integração contínua e pipeline de implantação (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="11398-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="11398-105">Neste tutorial, você cria um pipeline de CI/CD em uma VM do Azure, incluindo como:</span><span class="sxs-lookup"><span data-stu-id="11398-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11398-106">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="11398-107">Instalar e configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="11398-108">Criar integração de webhooks entre o GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="11398-109">Criar e disparar trabalhos de build do Jenkins por meio de confirmações do GitHub</span><span class="sxs-lookup"><span data-stu-id="11398-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="11398-110">Criar uma imagem de Docker para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="11398-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="11398-111">Verificar se as confirmações do GitHub compilam a nova imagem do Docker e atualizam o aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="11398-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="11398-112">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="11398-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="11398-113">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="11398-114">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="11398-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="11398-115">Criar instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-115">Create Jenkins instance</span></span>
<span data-ttu-id="11398-116">Um tutorial anterior em [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com a nuvem init.</span><span class="sxs-lookup"><span data-stu-id="11398-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="11398-117">Este tutorial usa um arquivo de inicialização de nuvem tooinstall Jenkins e Docker em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="11398-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="11398-118">No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração.</span><span class="sxs-lookup"><span data-stu-id="11398-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="11398-119">Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="11398-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="11398-120">Digite `sensible-editor cloud-init-jenkins.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="11398-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="11398-121">Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="11398-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="11398-122">Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="11398-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="11398-123">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupJenkins* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="11398-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="11398-124">Agora, crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="11398-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="11398-125">Saudação de uso `--custom-data` toopass de parâmetro no arquivo de configuração de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="11398-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="11398-126">Forneça o caminho completo do hello muito*jenkins.txt de inicialização de nuvem* se você salvou o arquivo hello fora de seu diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="11398-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="11398-127">Leva alguns minutos para Olá VM toobe criado e configurado.</span><span class="sxs-lookup"><span data-stu-id="11398-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="11398-128">tooallow web tooreach tráfego sua VM, use [az vm abrir portas](/cli/azure/vm#open-port) tooopen porta *8080* para tráfego Jenkins e a porta *1337* Olá Node. js aplicativo que é usado toorun um aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="11398-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="11398-129">Configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-129">Configure Jenkins</span></span>
<span data-ttu-id="11398-130">tooaccess seu Jenkins instância, obtenha o endereço IP público de saudação da VM:</span><span class="sxs-lookup"><span data-stu-id="11398-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="11398-131">Para fins de segurança, você precisa tooenter saudação inicial administrador a senha que é armazenada em um arquivo de texto no seu Olá toostart VM que Jenkins instalar.</span><span class="sxs-lookup"><span data-stu-id="11398-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="11398-132">Use o endereço IP público Olá obtido na saudação anterior etapa tooSSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="11398-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="11398-133">Saudação de exibição `initialAdminPassword` para seu Jenkins instalar e copiá-lo:</span><span class="sxs-lookup"><span data-stu-id="11398-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="11398-134">Se o arquivo hello ainda não está disponível, aguarde alguns minutos para nuvem init toocomplete Olá Jenkins e instale o Docker.</span><span class="sxs-lookup"><span data-stu-id="11398-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="11398-135">Abra um navegador da web e vá muito`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="11398-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="11398-136">Conclua a configuração inicial Jenkins Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="11398-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="11398-137">Digite hello *initialAdminPassword* obtido Olá VM na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="11398-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="11398-138">Clique em **selecionar tooinstall de plug-ins**</span><span class="sxs-lookup"><span data-stu-id="11398-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="11398-139">Procurar *GitHub* na caixa de texto de saudação na superior hello, selecione Olá *plug-in do GitHub*, em seguida, clique em **instalar**</span><span class="sxs-lookup"><span data-stu-id="11398-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="11398-140">toocreate uma conta de usuário Jenkins preenchê-Olá conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="11398-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="11398-141">De uma perspectiva de segurança, você deve criar este primeiro usuário Jenkins em vez de continuar como conta de administrador padrão hello.</span><span class="sxs-lookup"><span data-stu-id="11398-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="11398-142">Quando terminar, clique em **Começar a usar o Jenkins**</span><span class="sxs-lookup"><span data-stu-id="11398-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="11398-143">Criar um webhook do GitHub</span><span class="sxs-lookup"><span data-stu-id="11398-143">Create GitHub webhook</span></span>
<span data-ttu-id="11398-144">integração de saudação tooconfigure com GitHub, abra Olá [aplicativo de exemplo do Node. js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) do repositório de exemplos do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="11398-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="11398-145">toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="11398-146">Crie um webhook dentro de bifurcação Olá criado:</span><span class="sxs-lookup"><span data-stu-id="11398-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="11398-147">Clique em **configurações**, em seguida, selecione **serviços e integrações** no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="11398-148">Clique em **Adicionar serviço** e, em seguida, digite *Jenkins* na caixa de filtro.</span><span class="sxs-lookup"><span data-stu-id="11398-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="11398-149">Selecione *Jenkins (plug-in do GitHub)*</span><span class="sxs-lookup"><span data-stu-id="11398-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="11398-150">Para Olá **Jenkins gancho URL**, digite `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="11398-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="11398-151">Certifique-se de incluir a saudação à direita /</span><span class="sxs-lookup"><span data-stu-id="11398-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="11398-152">Clique em **Adicionar serviço**</span><span class="sxs-lookup"><span data-stu-id="11398-152">Click **Add service**</span></span>

![Adicionar repositório do GitHub webhook tooyour bifurcada](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="11398-154">Criar trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-154">Create Jenkins job</span></span>
<span data-ttu-id="11398-155">toohave Jenkins responder tooan evento no GitHub como confirmar o código, crie um trabalho de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="11398-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="11398-156">No seu site Jenkins, clique em **criar novos trabalhos** Olá home page:</span><span class="sxs-lookup"><span data-stu-id="11398-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="11398-157">Insira *HelloWorld* como nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="11398-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="11398-158">Escolha **Projeto Freestyle** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="11398-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="11398-159">Em Olá **geral** seção, selecione **GitHub** do projeto e insira a URL do repositório bifurcado, como *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="11398-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="11398-160">Em Olá **gerenciamento de código de origem** seção, selecione **Git**, insira seu repositório bifurcado *.git* URL, como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="11398-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="11398-161">Em Olá **criar gatilhos** seção, selecione **GitHub gancho de gatilho para sondagem GITscm**.</span><span class="sxs-lookup"><span data-stu-id="11398-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="11398-162">Em Olá **criar** , escolha **adicionar a etapa de compilação**.</span><span class="sxs-lookup"><span data-stu-id="11398-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="11398-163">Selecione **executar shell**, em seguida, digite `echo "Testing"` na janela toocommand.</span><span class="sxs-lookup"><span data-stu-id="11398-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="11398-164">Clique em **salvar** na parte inferior da saudação da janela de trabalhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="11398-165">Testar a integração do GitHub</span><span class="sxs-lookup"><span data-stu-id="11398-165">Test GitHub integration</span></span>
<span data-ttu-id="11398-166">Olá tootest integração do GitHub com Jenkins, confirmar uma alteração em sua bifurcação.</span><span class="sxs-lookup"><span data-stu-id="11398-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="11398-167">No GitHub web da interface do usuário, selecione seu repositório bifurcado e, em seguida, clique em Olá **js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="11398-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="11398-168">Clique em tooedit de ícone de lápis Olá esse arquivo para leituras de linha 6:</span><span class="sxs-lookup"><span data-stu-id="11398-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="11398-169">toocommit as alterações, clique em Olá **confirmar alterações** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="11398-170">Em Jenkins, uma nova compilação iniciada em Olá **criar histórico** seção do canto superior esquerdo do hello parte inferior da página do trabalho.</span><span class="sxs-lookup"><span data-stu-id="11398-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="11398-171">Clique o link de número de compilação hello e selecione **saída de Console** no tamanho de saudação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="11398-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="11398-172">Você pode exibir as etapas de saudação Jenkins assume que seu código retirado do GitHub e hello ação de compilação saídas de mensagem de saudação `Testing` toohello console.</span><span class="sxs-lookup"><span data-stu-id="11398-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="11398-173">Cada vez que uma confirmação é feita no GitHub, Olá webhook atinge tooJenkins e disparam uma nova compilação dessa maneira.</span><span class="sxs-lookup"><span data-stu-id="11398-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="11398-174">Definir a imagem de build do Docker</span><span class="sxs-lookup"><span data-stu-id="11398-174">Define Docker build image</span></span>
<span data-ttu-id="11398-175">toosee Olá Node. js aplicativo em execução com base em suas confirmações GitHub, permite criar um Docker imagem toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="11398-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="11398-176">imagem de saudação é criada a partir de um Dockerfile que define como tooconfigure Olá contêiner que executa o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="11398-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="11398-177">De saudação SSH conexão tooyour VM, altere o diretório de espaço de trabalho de Jenkins de toohello nomeado trabalho Olá que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="11398-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="11398-178">Em nosso exemplo, isso foi nomeado como *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="11398-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="11398-179">Criar um arquivo com nesse diretório de espaço de trabalho com `sudo sensible-editor Dockerfile` e colar Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="11398-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="11398-180">Certifique-se de que Olá que dockerfile inteira é copiado corretamente, especialmente Olá primeira linha:</span><span class="sxs-lookup"><span data-stu-id="11398-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="11398-181">Este Dockerfile usa Olá imagem base do Node. js usando Alpine Linux, porta expõe 1337 Olá aplicativo Hello World é executado, em seguida, copia os arquivos de aplicativo hello e a inicializa.</span><span class="sxs-lookup"><span data-stu-id="11398-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="11398-182">Criar regras de build do Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-182">Create Jenkins build rules</span></span>
<span data-ttu-id="11398-183">Em uma etapa anterior, você criou uma regra de compilação Jenkins básica que um console de toohello de mensagem de saída.</span><span class="sxs-lookup"><span data-stu-id="11398-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="11398-184">Permite criar toouse de etapa de compilação Olá nosso Dockerfile e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="11398-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="11398-185">Em sua instância Jenkins, selecione o trabalho de saudação criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="11398-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="11398-186">Clique em **configurar** no lado esquerdo do hello e role para baixo toohello **criar** seção:</span><span class="sxs-lookup"><span data-stu-id="11398-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="11398-187">Remova sua etapa de build `echo "Test"` existente.</span><span class="sxs-lookup"><span data-stu-id="11398-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="11398-188">Clique em Olá vermelho cruzada no canto superior direito de saudação de caixa de etapa de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="11398-189">Clique em **Adicionar etapa de build** e, em seguida, selecione **Executar shell**</span><span class="sxs-lookup"><span data-stu-id="11398-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="11398-190">Em Olá **comando** caixa, digite Olá os comandos a seguir e selecione **salvar**:</span><span class="sxs-lookup"><span data-stu-id="11398-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="11398-191">etapas de build do Docker Olá criam uma imagem e marca-o com hello Jenkins número da compilação para que possa manter um histórico de imagens.</span><span class="sxs-lookup"><span data-stu-id="11398-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="11398-192">Qualquer contêiner existente executando o aplicativo hello é interrompido e, em seguida, removida.</span><span class="sxs-lookup"><span data-stu-id="11398-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="11398-193">Um novo contêiner é iniciado usando a imagem de saudação e executa o aplicativo Node. js com base em confirmações de hello mais recentes no GitHub.</span><span class="sxs-lookup"><span data-stu-id="11398-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="11398-194">Testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="11398-194">Test your pipeline</span></span>
<span data-ttu-id="11398-195">pipeline de inteiro de saudação toosee em ação, editar Olá *js* em seu repositório GitHub bifurcado novamente e clique em **Confirmar alteração**.</span><span class="sxs-lookup"><span data-stu-id="11398-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="11398-196">Um novo trabalho inicia em Jenkins com base em webhook Olá para o GitHub.</span><span class="sxs-lookup"><span data-stu-id="11398-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="11398-197">Ele leva alguns segundos a imagem de Docker Olá toocreate e iniciar o aplicativo em um novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="11398-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="11398-198">Se necessário, obtenha o endereço IP público de saudação da VM novamente:</span><span class="sxs-lookup"><span data-stu-id="11398-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="11398-199">Abra um navegador da Web e insira `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="11398-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="11398-200">Seu aplicativo Node. js é exibido e reflete confirmações mais recentes de saudação na sua bifurcação GitHub da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="11398-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Executar o aplicativo Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="11398-202">Agora, faça outra toohello de edição *js* arquivo no GitHub e Confirmar alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="11398-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="11398-203">Aguarde alguns segundos para Olá trabalho toocomplete em Jenkins e atualize sua versão de hello atualizado web navegador toosee do seu aplicativo em execução em um novo contêiner da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="11398-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Executar o aplicativo Node.js após outra confirmação do GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="11398-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11398-205">Next steps</span></span>
<span data-ttu-id="11398-206">Neste tutorial, você configurado GitHub toorun um trabalho de compilação Jenkins em cada confirmação de código e, em seguida, implante um tootest de contêiner do Docker seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="11398-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="11398-207">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="11398-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="11398-208">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="11398-209">Instalar e configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="11398-210">Criar integração de webhooks entre o GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="11398-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="11398-211">Criar e disparar trabalhos de build do Jenkins por meio de confirmações do GitHub</span><span class="sxs-lookup"><span data-stu-id="11398-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="11398-212">Criar uma imagem de Docker para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="11398-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="11398-213">Verificar se as confirmações do GitHub compilam a nova imagem do Docker e atualizam o aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="11398-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="11398-214">Avançar toolearn tutorial do próximo toohello mais informações sobre como toointegrate Jenkins com o Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="11398-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11398-215">Implantar aplicativos com Jenkins e Team Services</span><span class="sxs-lookup"><span data-stu-id="11398-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)