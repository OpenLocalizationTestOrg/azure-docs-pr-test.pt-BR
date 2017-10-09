---
title: "aaaJenkins CI/CD com Kubernetes no serviço de contêiner do Azure | Microsoft Docs"
description: "Como tooautomate um CI/CD processar com toodeploy Jenkins e atualizar um aplicativo em contêineres em Kubernetes no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, Contêineres, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="9a9e4-104">Integração do Jenkins com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9a9e4-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="9a9e4-105">Neste tutorial, vemos Olá processo tooset a integração contínua de um aplicativo de contêiner vários em Kubernetes de serviço de contêiner do Azure usando Olá Jenkins plataforma.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="9a9e4-106">fluxo de trabalho de saudação imagem de contêiner Olá no Hub do Docker de compartimentos de Kubernetes hello usando uma implantação de atualizações.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="9a9e4-107">Processo de alto nível</span><span class="sxs-lookup"><span data-stu-id="9a9e4-107">High level process</span></span>
<span data-ttu-id="9a9e4-108">etapas básicas de saudação detalhadas neste artigo são:</span><span class="sxs-lookup"><span data-stu-id="9a9e4-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="9a9e4-109">Instalar um cluster Kubernetes no Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="9a9e4-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="9a9e4-110">Configurar Jenkins e configurar acesso tooContainer serviço</span><span class="sxs-lookup"><span data-stu-id="9a9e4-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="9a9e4-111">Criar um fluxo de trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a9e4-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="9a9e4-112">Testar Olá CI/CD processo final tooend</span><span class="sxs-lookup"><span data-stu-id="9a9e4-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="9a9e4-113">Instalar um cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9a9e4-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="9a9e4-114">Implante Olá Kubernetes cluster no serviço de contêiner do Azure usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="9a9e4-115">A documentação completa está [aqui](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="9a9e4-116">Etapa 1: criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9a9e4-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="9a9e4-117">Etapa 2: Implantar o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="9a9e4-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="9a9e4-118">Olá etapas a seguir exigem uma chave pública local do SSH armazenada na pasta de ~/.ssh hello.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="9a9e4-119">Configurar Jenkins e configurar acesso tooContainer serviço</span><span class="sxs-lookup"><span data-stu-id="9a9e4-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="9a9e4-120">Etapa 1: instalar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a9e4-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="9a9e4-121">Crie uma VM do Azure com o Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="9a9e4-122">Como etapas Olá posteriormente, você será necessário tooconnect toothis VM usando bash no seu computador local, a chave pública do conjunto Olá 'Tipo de autenticação' too'SSH' e colar Olá SSH chave pública que é armazenado localmente em sua pasta ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="9a9e4-123">Além disso, observe que você especificar como esse nome de usuário serão painel de Jenkins Olá tooview necessários e para conectar-se toohello Jenkins VM em etapas posteriores da saudação 'Nome de usuário'.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="9a9e4-124">Instale o Jenkins seguindo estas [instruções](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="9a9e4-125">Um tutorial mais detalhado está disponível em [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="9a9e4-126">tooview Olá Jenkins painel em seu computador local, atualize a porta de tooallow de grupo para segurança de rede do Azure Olá 8080 adicionando uma regra de entrada que permite acesso tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="9a9e4-127">Como alternativa, você pode configurar o encaminhamento de porta executando este comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="9a9e4-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="9a9e4-128">Conectar tooyour Jenkins servidor usando o navegador de saudação navegando IP público toohello (http:// < your_jenkins_public_ip >: 8080) e desbloquear painel Jenkins Olá Olá primeira vez com a senha de administrador inicial hello.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="9a9e4-129">senha do administrador do Hello está armazenada em /var/lib/jenkins/secrets/initialAdminPassword em Olá Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="9a9e4-130">Um tooget de maneira fácil essa senha é tooSSH em Olá Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="9a9e4-131">Em seguida, execute: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="9a9e4-132">Instalar o Docker na máquina de Jenkins Olá via esses [instruções](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="9a9e4-133">Isso permite que toobe de comandos do Docker executado em trabalhos Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="9a9e4-134">Configure o Docker permissões tooallow Jenkins tooaccess Olá Docker ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="9a9e4-135">Instale a CLI `kubectl` no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="9a9e4-136">Mais detalhes podem ser encontrados em [Instalando e Configurando kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="9a9e4-137">Trabalhos Jenkins usará toomanage 'kubectl' e implantar toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="9a9e4-138">Etapa 2: Configurar o cluster de Kubernetes toohello acesso</span><span class="sxs-lookup"><span data-stu-id="9a9e4-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="9a9e4-139">Há vários Olá tooaccomplishing de abordagens etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="9a9e4-140">Use a abordagem de saudação que é mais fácil para você.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="9a9e4-141">Saudação de cópia `kubectl` toohello do arquivo de configuração Jenkins máquina para que os trabalhos de Jenkins têm o cluster de Kubernetes toohello acesso.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="9a9e4-142">Essas instruções pressupõem que você está usando bash de um computador diferente que Olá Jenkins VM e que uma chave pública de SSH local é armazenada na pasta de ~/.ssh da máquina hello.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="9a9e4-143">Validar que Olá Kubernetes Jenkins cluster está acessível.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="9a9e4-144">toodo, SSH em Olá Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="9a9e4-145">Em seguida, verifique se Jenkins pode se conectar com êxito cluster tooyour: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="9a9e4-146">Criar um fluxo de trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a9e4-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9a9e4-147">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a9e4-147">Prerequisites</span></span>

- <span data-ttu-id="9a9e4-148">Conta do GitHub para o repositório de código.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="9a9e4-149">Docker Hub conta toostore e atualizar imagens.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="9a9e4-150">Aplicativo em contêineres que pode ser recompilado e atualizado.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="9a9e4-151">Você pode usar este aplicativo de contêiner de exemplo escrito em Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="9a9e4-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="9a9e4-152">Olá etapas a seguir devem ser executadas em sua própria conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="9a9e4-153">Sinta-se livre tooclone Olá acima repositório, mas você deve usar webhooks de saudação de tooconfigure sua própria conta e acessar Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="9a9e4-154">Etapa 1: implantar o v1 inicial do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9a9e4-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="9a9e4-155">Crie aplicativo de saudação do computador de um desenvolvedor de saudação com hello comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="9a9e4-156">Substitua `myrepo` com o seu próprio.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="9a9e4-157">Imagem de push tooDocker Hub.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="9a9e4-158">Implante toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="9a9e4-159">Editar saudação `go-web.yaml` arquivo tooupdate sua imagem de contêiner e o repositório.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="9a9e4-160">Etapa 2: configurar o sistema Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a9e4-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="9a9e4-161">Clique em **Gerenciar Jenkins** > **Configurar Sistema**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="9a9e4-162">Em **GitHub**, selecione **Adicionar Servidor GitHub**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="9a9e4-163">Deixe **URL da API** como padrão.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="9a9e4-164">Em **Credenciais**, adicione uma credencial do Jenkins usando **Texto secreto**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="9a9e4-165">É recomendável usar os tokens de acesso pessoal do GitHub, que são definidos nas configurações de conta de usuário do GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="9a9e4-166">Mais detalhes sobre isso podem ser encontrados [aqui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="9a9e4-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="9a9e4-167">Clique em **Testar conexão** tooensure isso está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="9a9e4-168">Em **Propriedades Globais**, adicione uma variável de ambiente `DOCKER_HUB` e forneça sua senha do Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="9a9e4-169">(Isso é útil para esta demonstração, mas um cenário de produção exige uma abordagem mais segura.)</span><span class="sxs-lookup"><span data-stu-id="9a9e4-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="9a9e4-170">Salve.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-170">Save.</span></span>

![Acesso ao GitHub do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="9a9e4-172">Etapa 3: Criar o fluxo de trabalho do hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="9a9e4-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="9a9e4-173">Crie um item do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="9a9e4-174">Forneça um nome (por exemplo, "go-web") e selecione **Projeto Estilo Livre**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="9a9e4-175">Verificar **GitHub projeto** e fornecer um repositório GitHub do hello URL tooyour.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="9a9e4-176">Em **código-fonte gerenciamento**, forneça a URL de repositório do GitHub hello e credenciais.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="9a9e4-177">Adicionar um **passo de compilação** do tipo **executar shell** e use Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a9e4-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="9a9e4-178">Adicione outro **passo de compilação** do tipo **executar shell** e use Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a9e4-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Etapas de build do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="9a9e4-180">Salvar item de Jenkins hello e testar com **criar agora**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="9a9e4-181">Etapa 4: conectar o webhook do GitHub</span><span class="sxs-lookup"><span data-stu-id="9a9e4-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="9a9e4-182">No item de Jenkins Olá criado, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="9a9e4-183">Em **Gatilhos de Build**, selecione **Gatilho de webhook do GitHub para sondagem de GITScm** e **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="9a9e4-184">Isso configura automaticamente o hello GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="9a9e4-185">No seu repositório GitHub para go-web, clique em **Configurações > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="9a9e4-186">Verifique se esse Olá webhook Jenkins URL foi adicionada com êxito.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="9a9e4-187">Olá URL deve terminar em "github-webhook".</span><span class="sxs-lookup"><span data-stu-id="9a9e4-187">hello URL should end in "github-webhook".</span></span>

![Configuração de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="9a9e4-189">Testar Olá CI/CD processo final tooend</span><span class="sxs-lookup"><span data-stu-id="9a9e4-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="9a9e4-190">Atualize o código para hello e o envio de sincronia com o repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="9a9e4-191">Olá Jenkins no console do, verifique Olá **histórico de compilação** e validar esse Olá trabalho foi executado.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="9a9e4-192">Exibir console saída toosee detalhes.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-192">View console output toosee details.</span></span>
3. <span data-ttu-id="9a9e4-193">De Kubernetes, exibir detalhes da saudação atualizados implantação:</span><span class="sxs-lookup"><span data-stu-id="9a9e4-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="9a9e4-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a9e4-194">Next steps</span></span>

- <span data-ttu-id="9a9e4-195">Implante o Registro de Contêiner do Azure e armazene as imagens em um repositório seguro.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="9a9e4-196">Confira [Documentos do Registro de Contêiner do Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="9a9e4-197">Crie um fluxo de trabalho mais complexo que inclua implantação lado a lado e testes automatizados no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9a9e4-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="9a9e4-198">Para obter mais informações sobre CI/CD com Jenkins e Kubernetes, consulte Olá [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="9a9e4-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
