---
title: "CI/CD Jenkins com Kubernetes no Serviço de Contêiner do Azure | Microsoft Docs"
description: "Como automatizar um processo de CI/CD com Jenkins para implantar e atualizar um aplicativo em recipientes no Kubernetes no Serviço de Contêiner do Azure"
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
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="e2f2b-104">Integração do Jenkins com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e2f2b-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="e2f2b-105">Neste tutorial, percorreremos o processo para configurar a integração contínua de um aplicativo de vários contêineres no Kubernetes do Serviço de Contêiner do Azure usando a plataforma Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="e2f2b-106">O fluxo de trabalho atualiza a imagem de contêiner no Hub do Docker e atualiza os pods do Kubernetes usando uma distribuição de implantação.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="e2f2b-107">Processo de alto nível</span><span class="sxs-lookup"><span data-stu-id="e2f2b-107">High level process</span></span>
<span data-ttu-id="e2f2b-108">As etapas básicas descritas neste artigo são:</span><span class="sxs-lookup"><span data-stu-id="e2f2b-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="e2f2b-109">Instalar um cluster Kubernetes no Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="e2f2b-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="e2f2b-110">Configurar o Jenkins e configurar o acesso ao Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="e2f2b-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="e2f2b-111">Criar um fluxo de trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="e2f2b-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="e2f2b-112">Testar o processo de CI/CD de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="e2f2b-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="e2f2b-113">Instalar um cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e2f2b-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="e2f2b-114">Implante o cluster Kubernetes no Serviço de Contêiner do Azure usando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="e2f2b-115">A documentação completa está [aqui](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="e2f2b-116">Etapa 1: criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e2f2b-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="e2f2b-117">Etapa 2: implantar o cluster</span><span class="sxs-lookup"><span data-stu-id="e2f2b-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="e2f2b-118">As etapas a seguir exigem uma chave pública SSH local armazenada na pasta ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="e2f2b-119">Configurar o Jenkins e configurar o acesso ao Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="e2f2b-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="e2f2b-120">Etapa 1: instalar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="e2f2b-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="e2f2b-121">Crie uma VM do Azure com o Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="e2f2b-122">Já que posteriormente nas etapas você precisará se conectar a essa VM usando bash no seu computador local, defina o 'Tipo de autenticação' para 'Chave pública SSH' e cole a chave pública SSH que está armazenada localmente em sua pasta ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="e2f2b-123">Além disso, anote o 'Nome de usuário' que você especificar, pois esse nome de usuário será necessário para exibir o painel do Jenkins e para conectar-se à VM Jenkins em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="e2f2b-124">Instale o Jenkins seguindo estas [instruções](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="e2f2b-125">Um tutorial mais detalhado está disponível em [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="e2f2b-126">Para exibir o painel do Jenkins em seu computador local, atualize o grupo de segurança de rede do Azure para permitir a porta 8080 adicionando uma regra de entrada para permitir o acesso à porta 8080.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="e2f2b-127">Como alternativa, você pode configurar o encaminhamento de porta executando este comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="e2f2b-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="e2f2b-128">Conecte-se ao seu servidor Jenkins usando o navegador para navegar até o IP público (http://<seu_IP_público_do_jenkins>:8080) e desbloqueie o painel do Jenkins pela primeira vez com a senha de administrador inicial.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="e2f2b-129">A senha de administrador é armazenada em /var/lib/jenkins/secrets/initialAdminPassword na VM Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="e2f2b-130">É uma maneira fácil de obter essa senha é conectar-se por SSH à VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="e2f2b-131">Em seguida, execute: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="e2f2b-132">Instale o Docker no computador do Jenkins seguindo estas [instruções](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="e2f2b-133">Isso permite que os comandos do Docker sejam executados em trabalhos do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="e2f2b-134">Configure as permissões do Docker para permitir que o Jenkins acesse o ponto de extremidade do Docker.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="e2f2b-135">Instale a CLI `kubectl` no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="e2f2b-136">Mais detalhes podem ser encontrados em [Instalando e Configurando kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="e2f2b-137">Os trabalhos do Jenkins usarão 'kubectl' para gerenciar e implantar o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="e2f2b-138">Etapa 2: configurar o acesso ao cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e2f2b-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="e2f2b-139">Há várias abordagens para realizar as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="e2f2b-140">Use a abordagem que for mais fácil para você.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="e2f2b-141">Copie o arquivo de configuração `kubectl` para o computador Jenkins para que trabalhos do Jenkins tenham acesso ao cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="e2f2b-142">Essas instruções pressupõem que você está usando bash de um computador diferente que a VM Jenkins e que uma chave pública SSH local está armazenada na pasta ~/.ssh do computador.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="e2f2b-143">Do Jenkins, valide que o cluster Kubernetes está acessível.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="e2f2b-144">Para fazer isso, conecte-se por SSH à VM Jenkins: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="e2f2b-145">Em seguida, verifique se o Jenkins pode se conectar com êxito ao cluster: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="e2f2b-146">Criar um fluxo de trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="e2f2b-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e2f2b-147">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e2f2b-147">Prerequisites</span></span>

- <span data-ttu-id="e2f2b-148">Conta do GitHub para o repositório de código.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="e2f2b-149">Conta de Hub do Docker para armazenar e atualizar imagens.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="e2f2b-150">Aplicativo em contêineres que pode ser recompilado e atualizado.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="e2f2b-151">Você pode usar este aplicativo de contêiner de exemplo escrito em Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="e2f2b-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="e2f2b-152">As etapas a seguir devem ser executadas em sua própria conta do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="e2f2b-153">Fique à vontade para clonar o repositório acima, mas você deve usar sua própria conta para configurar os webhooks e o acesso ao Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="e2f2b-154">Etapa 1: implantar o v1 inicial do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e2f2b-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="e2f2b-155">Compilar o aplicativo no computador do desenvolvedor usando os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="e2f2b-156">Substitua `myrepo` com o seu próprio.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="e2f2b-157">Envie a imagem por push ao Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="e2f2b-158">Implante no cluster do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e2f2b-159">Edite o arquivo `go-web.yaml` para atualizar o repositório e a imagem do contêiner.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="e2f2b-160">Etapa 2: configurar o sistema Jenkins</span><span class="sxs-lookup"><span data-stu-id="e2f2b-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="e2f2b-161">Clique em **Gerenciar Jenkins** > **Configurar Sistema**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="e2f2b-162">Em **GitHub**, selecione **Adicionar Servidor GitHub**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="e2f2b-163">Deixe **URL da API** como padrão.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="e2f2b-164">Em **Credenciais**, adicione uma credencial do Jenkins usando **Texto secreto**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="e2f2b-165">É recomendável usar os tokens de acesso pessoal do GitHub, que são definidos nas configurações de conta de usuário do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="e2f2b-166">Mais detalhes sobre isso podem ser encontrados [aqui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="e2f2b-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="e2f2b-167">Clique em **Testar conexão** para assegurar que isso esteja configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="e2f2b-168">Em **Propriedades Globais**, adicione uma variável de ambiente `DOCKER_HUB` e forneça sua senha do Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="e2f2b-169">(Isso é útil para esta demonstração, mas um cenário de produção exige uma abordagem mais segura.)</span><span class="sxs-lookup"><span data-stu-id="e2f2b-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="e2f2b-170">Salve.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-170">Save.</span></span>

![Acesso ao GitHub do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="e2f2b-172">Etapa 3: criar o fluxo de trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="e2f2b-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="e2f2b-173">Crie um item do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="e2f2b-174">Forneça um nome (por exemplo, "go-web") e selecione **Projeto Estilo Livre**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="e2f2b-175">Marque a opção **Projeto GitHub** e forneça a URL para seu repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="e2f2b-176">Em **Gerenciamento de Código-Fonte**, forneça a URL do repositório GitHub e as credenciais.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="e2f2b-177">Adicione uma **Etapa de Build** do tipo **Executar shell** e use o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="e2f2b-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="e2f2b-178">Adicione outra **Etapa de Build** do tipo **Executar shell** e use o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="e2f2b-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Etapas de build do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="e2f2b-180">Salve o item do Jenkins e teste com **Compilar Agora**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="e2f2b-181">Etapa 4: conectar o webhook do GitHub</span><span class="sxs-lookup"><span data-stu-id="e2f2b-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="e2f2b-182">No item do Jenkins criado, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="e2f2b-183">Em **Gatilhos de Build**, selecione **Gatilho de webhook do GitHub para sondagem de GITScm** e **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="e2f2b-184">Isso configura automaticamente o webhook do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="e2f2b-185">No seu repositório GitHub para go-web, clique em **Configurações > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="e2f2b-186">Verifique se a URL do webhook Jenkins foi adicionada com êxito.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="e2f2b-187">A URL deve terminar em "github-webhook".</span><span class="sxs-lookup"><span data-stu-id="e2f2b-187">The URL should end in "github-webhook".</span></span>

![Configuração de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="e2f2b-189">Testar o processo de CI/CD de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="e2f2b-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="e2f2b-190">Atualize o código para o repositório e envie por push/sincronize com o repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="e2f2b-191">No console do Jenkins, verifique o **Histórico de Build** e valide que o trabalho foi executado.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="e2f2b-192">Exiba a saída do console para ver detalhes.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-192">View console output to see details.</span></span>
3. <span data-ttu-id="e2f2b-193">Do Kubernetes, exiba detalhes da implantação atualizada:</span><span class="sxs-lookup"><span data-stu-id="e2f2b-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="e2f2b-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2f2b-194">Next steps</span></span>

- <span data-ttu-id="e2f2b-195">Implante o Registro de Contêiner do Azure e armazene as imagens em um repositório seguro.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="e2f2b-196">Confira [Documentos do Registro de Contêiner do Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="e2f2b-197">Crie um fluxo de trabalho mais complexo que inclua implantação lado a lado e testes automatizados no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e2f2b-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="e2f2b-198">Para obter mais informações sobre CI/CD com Jenkins e Kubernetes, consulte o [blog do Jenkins](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="e2f2b-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
