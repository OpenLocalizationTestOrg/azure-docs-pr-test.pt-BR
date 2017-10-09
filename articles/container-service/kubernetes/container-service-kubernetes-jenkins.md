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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Integração do Jenkins com o Serviço de Contêiner do Azure e o Kubernetes 
Neste tutorial, vemos Olá processo tooset a integração contínua de um aplicativo de contêiner vários em Kubernetes de serviço de contêiner do Azure usando Olá Jenkins plataforma. fluxo de trabalho de saudação imagem de contêiner Olá no Hub do Docker de compartimentos de Kubernetes hello usando uma implantação de atualizações. 

## <a name="high-level-process"></a>Processo de alto nível
etapas básicas de saudação detalhadas neste artigo são: 
- Instalar um cluster Kubernetes no Serviço de Contêiner
- Configurar Jenkins e configurar acesso tooContainer serviço
- Criar um fluxo de trabalho do Jenkins
- Testar Olá CI/CD processo final tooend

## <a name="install-a-kubernetes-cluster"></a>Instalar um cluster Kubernetes
    
Implante Olá Kubernetes cluster no serviço de contêiner do Azure usando Olá etapas a seguir. A documentação completa está [aqui](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Etapa 1: criar um grupo de recursos
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Etapa 2: Implantar o cluster Olá
> [!NOTE]
> Olá etapas a seguir exigem uma chave pública local do SSH armazenada na pasta de ~/.ssh hello.
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Configurar Jenkins e configurar acesso tooContainer serviço

### <a name="step-1-install-jenkins"></a>Etapa 1: instalar o Jenkins
1. Crie uma VM do Azure com o Ubuntu 16.04 LTS.  Como etapas Olá posteriormente, você será necessário tooconnect toothis VM usando bash no seu computador local, a chave pública do conjunto Olá 'Tipo de autenticação' too'SSH' e colar Olá SSH chave pública que é armazenado localmente em sua pasta ~/.ssh.  Além disso, observe que você especificar como esse nome de usuário serão painel de Jenkins Olá tooview necessários e para conectar-se toohello Jenkins VM em etapas posteriores da saudação 'Nome de usuário'.
2. Instale o Jenkins seguindo estas [instruções](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Um tutorial mais detalhado está disponível em [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview Olá Jenkins painel em seu computador local, atualize a porta de tooallow de grupo para segurança de rede do Azure Olá 8080 adicionando uma regra de entrada que permite acesso tooport 8080.  Como alternativa, você pode configurar o encaminhamento de porta executando este comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Conectar tooyour Jenkins servidor usando o navegador de saudação navegando IP público toohello (http:// < your_jenkins_public_ip >: 8080) e desbloquear painel Jenkins Olá Olá primeira vez com a senha de administrador inicial hello.  senha do administrador do Hello está armazenada em /var/lib/jenkins/secrets/initialAdminPassword em Olá Jenkins VM.  Um tooget de maneira fácil essa senha é tooSSH em Olá Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Em seguida, execute: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Instalar o Docker na máquina de Jenkins Olá via esses [instruções](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Isso permite que toobe de comandos do Docker executado em trabalhos Jenkins.
6. Configure o Docker permissões tooallow Jenkins tooaccess Olá Docker ponto de extremidade.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Instale a CLI `kubectl` no Jenkins. Mais detalhes podem ser encontrados em [Instalando e Configurando kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).  Trabalhos Jenkins usará toomanage 'kubectl' e implantar toohello Kubernetes cluster.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Etapa 2: Configurar o cluster de Kubernetes toohello acesso

> [!NOTE]
> Há vários Olá tooaccomplishing de abordagens etapas a seguir. Use a abordagem de saudação que é mais fácil para você.
>

1. Saudação de cópia `kubectl` toohello do arquivo de configuração Jenkins máquina para que os trabalhos de Jenkins têm o cluster de Kubernetes toohello acesso. Essas instruções pressupõem que você está usando bash de um computador diferente que Olá Jenkins VM e que uma chave pública de SSH local é armazenada na pasta de ~/.ssh da máquina hello.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Validar que Olá Kubernetes Jenkins cluster está acessível.  toodo, SSH em Olá Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Em seguida, verifique se Jenkins pode se conectar com êxito cluster tooyour: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Criar um fluxo de trabalho do Jenkins

### <a name="prerequisites"></a>Pré-requisitos

- Conta do GitHub para o repositório de código.
- Docker Hub conta toostore e atualizar imagens.
- Aplicativo em contêineres que pode ser recompilado e atualizado. Você pode usar este aplicativo de contêiner de exemplo escrito em Golang: https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Olá etapas a seguir devem ser executadas em sua própria conta do GitHub. Sinta-se livre tooclone Olá acima repositório, mas você deve usar webhooks de saudação de tooconfigure sua própria conta e acessar Jenkins.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Etapa 1: implantar o v1 inicial do aplicativo
1. Crie aplicativo de saudação do computador de um desenvolvedor de saudação com hello comandos a seguir. Substitua `myrepo` com o seu próprio.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Imagem de push tooDocker Hub.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Implante toohello Kubernetes cluster.
    
    > [!NOTE] 
    > Editar saudação `go-web.yaml` arquivo tooupdate sua imagem de contêiner e o repositório.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Etapa 2: configurar o sistema Jenkins
1. Clique em **Gerenciar Jenkins** > **Configurar Sistema**.
2. Em **GitHub**, selecione **Adicionar Servidor GitHub**.
3. Deixe **URL da API** como padrão.
4. Em **Credenciais**, adicione uma credencial do Jenkins usando **Texto secreto**. É recomendável usar os tokens de acesso pessoal do GitHub, que são definidos nas configurações de conta de usuário do GitHub. Mais detalhes sobre isso podem ser encontrados [aqui.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Clique em **Testar conexão** tooensure isso está configurado corretamente.
6. Em **Propriedades Globais**, adicione uma variável de ambiente `DOCKER_HUB` e forneça sua senha do Hub do Docker. (Isso é útil para esta demonstração, mas um cenário de produção exige uma abordagem mais segura.)
7. Salve.

![Acesso ao GitHub do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Etapa 3: Criar o fluxo de trabalho do hello Jenkins
1. Crie um item do Jenkins.
2. Forneça um nome (por exemplo, "go-web") e selecione **Projeto Estilo Livre**. 
3. Verificar **GitHub projeto** e fornecer um repositório GitHub do hello URL tooyour.
4. Em **código-fonte gerenciamento**, forneça a URL de repositório do GitHub hello e credenciais. 
5. Adicionar um **passo de compilação** do tipo **executar shell** e use Olá texto a seguir:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Adicione outro **passo de compilação** do tipo **executar shell** e use Olá texto a seguir:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Etapas de build do Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Salvar item de Jenkins hello e testar com **criar agora**.

### <a name="step-4-connect-github-webhook"></a>Etapa 4: conectar o webhook do GitHub
1. No item de Jenkins Olá criado, clique em **configurar**.
2. Em **Gatilhos de Build**, selecione **Gatilho de webhook do GitHub para sondagem de GITScm** e **Salvar**. Isso configura automaticamente o hello GitHub webhook.
3. No seu repositório GitHub para go-web, clique em **Configurações > Webhooks**.
4. Verifique se esse Olá webhook Jenkins URL foi adicionada com êxito. Olá URL deve terminar em "github-webhook".

![Configuração de webhook Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Testar Olá CI/CD processo final tooend

1. Atualize o código para hello e o envio de sincronia com o repositório do GitHub hello.
2. Olá Jenkins no console do, verifique Olá **histórico de compilação** e validar esse Olá trabalho foi executado. Exibir console saída toosee detalhes.
3. De Kubernetes, exibir detalhes da saudação atualizados implantação:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Próximas etapas

- Implante o Registro de Contêiner do Azure e armazene as imagens em um repositório seguro. Confira [Documentos do Registro de Contêiner do Azure](https://docs.microsoft.com/azure/container-registry).
- Crie um fluxo de trabalho mais complexo que inclua implantação lado a lado e testes automatizados no Jenkins.
- Para obter mais informações sobre CI/CD com Jenkins e Kubernetes, consulte Olá [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
