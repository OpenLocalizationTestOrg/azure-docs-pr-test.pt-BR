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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Como toocreate uma infra-estrutura de desenvolvimento em uma VM do Linux no Azure com Jenkins, GitHub e o Docker
tooautomate Olá compilação e teste a fase de desenvolvimento de aplicativos, você pode usar uma integração contínua e pipeline de implantação (CI/CD). Neste tutorial, você cria um pipeline de CI/CD em uma VM do Azure, incluindo como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Instalar e configurar o Jenkins
> * Criar integração de webhooks entre o GitHub e Jenkins
> * Criar e disparar trabalhos de build do Jenkins por meio de confirmações do GitHub
> * Criar uma imagem de Docker para o aplicativo
> * Verificar se as confirmações do GitHub compilam a nova imagem do Docker e atualizam o aplicativo em execução


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Criar instância do Jenkins
Um tutorial anterior em [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com a nuvem init. Este tutorial usa um arquivo de inicialização de nuvem tooinstall Jenkins e Docker em uma máquina virtual. 

No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração. Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local. Digite `sensible-editor cloud-init-jenkins.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis. Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:

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

Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupJenkins* em Olá *eastus* local:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Agora, crie uma VM com [az vm create](/cli/azure/vm#create). Saudação de uso `--custom-data` toopass de parâmetro no arquivo de configuração de inicialização de nuvem. Forneça o caminho completo do hello muito*jenkins.txt de inicialização de nuvem* se você salvou o arquivo hello fora de seu diretório de trabalho atual.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Leva alguns minutos para Olá VM toobe criado e configurado.

tooallow web tooreach tráfego sua VM, use [az vm abrir portas](/cli/azure/vm#open-port) tooopen porta *8080* para tráfego Jenkins e a porta *1337* Olá Node. js aplicativo que é usado toorun um aplicativo de exemplo:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Configurar o Jenkins
tooaccess seu Jenkins instância, obtenha o endereço IP público de saudação da VM:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Para fins de segurança, você precisa tooenter saudação inicial administrador a senha que é armazenada em um arquivo de texto no seu Olá toostart VM que Jenkins instalar. Use o endereço IP público Olá obtido na saudação anterior etapa tooSSH tooyour VM:

```bash
ssh azureuser@<publicIps>
```

Saudação de exibição `initialAdminPassword` para seu Jenkins instalar e copiá-lo:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Se o arquivo hello ainda não está disponível, aguarde alguns minutos para nuvem init toocomplete Olá Jenkins e instale o Docker.

Abra um navegador da web e vá muito`http://<publicIps>:8080`. Conclua a configuração inicial Jenkins Olá da seguinte maneira:

- Digite hello *initialAdminPassword* obtido Olá VM na etapa anterior hello.
- Clique em **selecionar tooinstall de plug-ins**
- Procurar *GitHub* na caixa de texto de saudação na superior hello, selecione Olá *plug-in do GitHub*, em seguida, clique em **instalar**
- toocreate uma conta de usuário Jenkins preenchê-Olá conforme desejado. De uma perspectiva de segurança, você deve criar este primeiro usuário Jenkins em vez de continuar como conta de administrador padrão hello.
- Quando terminar, clique em **Começar a usar o Jenkins**


## <a name="create-github-webhook"></a>Criar um webhook do GitHub
integração de saudação tooconfigure com GitHub, abra Olá [aplicativo de exemplo do Node. js Hello World](https://github.com/Azure-Samples/nodejs-docs-hello-world) do repositório de exemplos do Azure hello. toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.

Crie um webhook dentro de bifurcação Olá criado:

- Clique em **configurações**, em seguida, selecione **serviços e integrações** no lado esquerdo da saudação.
- Clique em **Adicionar serviço** e, em seguida, digite *Jenkins* na caixa de filtro.
- Selecione *Jenkins (plug-in do GitHub)*
- Para Olá **Jenkins gancho URL**, digite `http://<publicIps>:8080/github-webhook/`. Certifique-se de incluir a saudação à direita /
- Clique em **Adicionar serviço**

![Adicionar repositório do GitHub webhook tooyour bifurcada](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Criar trabalho do Jenkins
toohave Jenkins responder tooan evento no GitHub como confirmar o código, crie um trabalho de Jenkins. 

No seu site Jenkins, clique em **criar novos trabalhos** Olá home page:

- Insira *HelloWorld* como nome do trabalho. Escolha **Projeto Freestyle** e selecione **OK**.
- Em Olá **geral** seção, selecione **GitHub** do projeto e insira a URL do repositório bifurcado, como *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Em Olá **gerenciamento de código de origem** seção, selecione **Git**, insira seu repositório bifurcado *.git* URL, como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Em Olá **criar gatilhos** seção, selecione **GitHub gancho de gatilho para sondagem GITscm**.
- Em Olá **criar** , escolha **adicionar a etapa de compilação**. Selecione **executar shell**, em seguida, digite `echo "Testing"` na janela toocommand.
- Clique em **salvar** na parte inferior da saudação da janela de trabalhos de saudação.


## <a name="test-github-integration"></a>Testar a integração do GitHub
Olá tootest integração do GitHub com Jenkins, confirmar uma alteração em sua bifurcação. 

No GitHub web da interface do usuário, selecione seu repositório bifurcado e, em seguida, clique em Olá **js** arquivo. Clique em tooedit de ícone de lápis Olá esse arquivo para leituras de linha 6:

```nodejs
response.end("Hello World!");
```

toocommit as alterações, clique em Olá **confirmar alterações** botão na parte inferior da saudação.

Em Jenkins, uma nova compilação iniciada em Olá **criar histórico** seção do canto superior esquerdo do hello parte inferior da página do trabalho. Clique o link de número de compilação hello e selecione **saída de Console** no tamanho de saudação à esquerda. Você pode exibir as etapas de saudação Jenkins assume que seu código retirado do GitHub e hello ação de compilação saídas de mensagem de saudação `Testing` toohello console. Cada vez que uma confirmação é feita no GitHub, Olá webhook atinge tooJenkins e disparam uma nova compilação dessa maneira.


## <a name="define-docker-build-image"></a>Definir a imagem de build do Docker
toosee Olá Node. js aplicativo em execução com base em suas confirmações GitHub, permite criar um Docker imagem toorun Olá aplicativo. imagem de saudação é criada a partir de um Dockerfile que define como tooconfigure Olá contêiner que executa o aplicativo hello. 

De saudação SSH conexão tooyour VM, altere o diretório de espaço de trabalho de Jenkins de toohello nomeado trabalho Olá que você criou na etapa anterior. Em nosso exemplo, isso foi nomeado como *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Criar um arquivo com nesse diretório de espaço de trabalho com `sudo sensible-editor Dockerfile` e colar Olá conteúdo a seguir. Certifique-se de que Olá que dockerfile inteira é copiado corretamente, especialmente Olá primeira linha:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Este Dockerfile usa Olá imagem base do Node. js usando Alpine Linux, porta expõe 1337 Olá aplicativo Hello World é executado, em seguida, copia os arquivos de aplicativo hello e a inicializa.


## <a name="create-jenkins-build-rules"></a>Criar regras de build do Jenkins
Em uma etapa anterior, você criou uma regra de compilação Jenkins básica que um console de toohello de mensagem de saída. Permite criar toouse de etapa de compilação Olá nosso Dockerfile e executar o aplicativo hello.

Em sua instância Jenkins, selecione o trabalho de saudação criado na etapa anterior. Clique em **configurar** no lado esquerdo do hello e role para baixo toohello **criar** seção:

- Remova sua etapa de build `echo "Test"` existente. Clique em Olá vermelho cruzada no canto superior direito de saudação de caixa de etapa de compilação de saudação.
- Clique em **Adicionar etapa de build** e, em seguida, selecione **Executar shell**
- Em Olá **comando** caixa, digite Olá os comandos a seguir e selecione **salvar**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

etapas de build do Docker Olá criam uma imagem e marca-o com hello Jenkins número da compilação para que possa manter um histórico de imagens. Qualquer contêiner existente executando o aplicativo hello é interrompido e, em seguida, removida. Um novo contêiner é iniciado usando a imagem de saudação e executa o aplicativo Node. js com base em confirmações de hello mais recentes no GitHub.


## <a name="test-your-pipeline"></a>Testar o pipeline
pipeline de inteiro de saudação toosee em ação, editar Olá *js* em seu repositório GitHub bifurcado novamente e clique em **Confirmar alteração**. Um novo trabalho inicia em Jenkins com base em webhook Olá para o GitHub. Ele leva alguns segundos a imagem de Docker Olá toocreate e iniciar o aplicativo em um novo contêiner.

Se necessário, obtenha o endereço IP público de saudação da VM novamente:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Abra um navegador da Web e insira `http://<publicIps>:1337`. Seu aplicativo Node. js é exibido e reflete confirmações mais recentes de saudação na sua bifurcação GitHub da seguinte maneira:

![Executar o aplicativo Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Agora, faça outra toohello de edição *js* arquivo no GitHub e Confirmar alteração de saudação. Aguarde alguns segundos para Olá trabalho toocomplete em Jenkins e atualize sua versão de hello atualizado web navegador toosee do seu aplicativo em execução em um novo contêiner da seguinte maneira:

![Executar o aplicativo Node.js após outra confirmação do GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você configurado GitHub toorun um trabalho de compilação Jenkins em cada confirmação de código e, em seguida, implante um tootest de contêiner do Docker seu aplicativo. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Instalar e configurar o Jenkins
> * Criar integração de webhooks entre o GitHub e Jenkins
> * Criar e disparar trabalhos de build do Jenkins por meio de confirmações do GitHub
> * Criar uma imagem de Docker para o aplicativo
> * Verificar se as confirmações do GitHub compilam a nova imagem do Docker e atualizam o aplicativo em execução

Avançar toolearn tutorial do próximo toohello mais informações sobre como toointegrate Jenkins com o Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Implantar aplicativos com Jenkins e Team Services](tutorial-build-deploy-jenkins.md)