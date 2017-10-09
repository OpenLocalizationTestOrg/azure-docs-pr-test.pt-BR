---
title: "aaaDeploy tooLinux de aplicativo um Node. js máquinas virtuais no Azure"
description: "Saiba como toodeploy um Node. js máquinas de virtuais de tooLinux do aplicativo no Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Implantar um aplicativo de Node. js tooLinux máquinas virtuais no Azure
Este tutorial mostra como tootake um aplicativo Node. js e implantá-lo em máquinas virtuais de tooLinux em execução no Azure. instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional que é capaz de executar o Node. js.

Você aprenderá a:

* Bifurcar e clonar um repositório GitHub contendo um aplicativo TODO simples;
* Criar e configurar duas máquinas virtuais de Linux no aplicativo do Azure toorun hello;
* Itere o aplicativo hello enviando a máquina virtual do atualizações toohello web front-end.

> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do GitHub e uma conta do Microsoft Azure e Olá capacidade toouse Git de um computador de desenvolvimento.
> 
> Se você não tiver uma conta do GitHub, poderá se inscrever [aqui](https://github.com/join).
> 
> Se você não tiver uma conta do [Microsoft Azure](https://azure.microsoft.com/), poderá se inscrever para uma avaliação GRATUITA [aqui](https://azure.microsoft.com/pricing/free-trial/). Isso também levará você por meio do processo de inscrição Olá um [Account Microsoft](http://account.microsoft.com) se você ainda não tiver um. Como alternativa, se você for um assinante do Visual Studio, poderá [ativar os benefícios do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Se você não tiver o git na máquina de desenvolvimento e estiver usando um computador Windows ou Macintosh, instale o git [aqui](http://www.git-scm.com). Se você estiver usando o Linux, instale o git usando o mecanismo de hello mais apropriado para você, como `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Bifurcação e clonagem Olá TODO aplicativo
Olá aplicativo TODO usado por este tutorial implementa um front-end da web simples sobre uma instância do MongoDB que mantém o controle de uma lista de tarefas. Depois de entrar no tooGitHub, vá [aqui](https://github.com/stepro/node-todo) toofind Olá aplicativo e bifurcação usando o link de saudação na parte superior de saudação à direita. Isso deve criar um repositório em sua conta denominado *nomedaconta*/node-todo.

Agora, em sua máquina de desenvolvimento, clone este repositório:

    git clone https://github.com/accountname/node-todo.git

Usaremos esse clone local do repositório de saudação um pouco mais tarde ao fazer alterações de código-fonte toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Criando e configurando Olá máquinas virtuais do Linux
O Azure tem excelente suporte para computação bruta usando máquinas virtuais Linux. Esta parte do mostra de tutorial hello como você pode facilmente criar duas máquinas virtuais do Linux e implantar Olá TODO aplicativo toothem, executando Olá front-end da web em um e Olá instância MongoDB Olá outros.

### <a name="creating-virtual-machines"></a>Criando máquinas virtuais
toocreate de maneira mais fácil de saudação uma nova máquina virtual no Azure é toouse Olá Portal do Azure. Clique em [aqui](https://portal.azure.com) toosign no e inicie Olá Portal do Azure no seu navegador da web. Uma vez hello Azure Portal for carregada, conclua Olá etapas a seguir:

* Clique em Olá "+ novo" vincular;
* Selecione a categoria de "Computação" hello e escolha "Ubuntu Server 14.04 LTS";
* Selecione o modelo de implantação do hello "Gerenciador de recursos" e clique em "Criar";
* Preencha as Noções básicas de saudação estas diretrizes:
  * Especifique um nome que você pode identificar facilmente mais tarde;
  * Neste tutorial, escolha Autenticação de senha;
  * Crie um novo grupo de recursos com um nome identificável.
* Para Olá tamanho da máquina Virtual, o "Padrão" A1"é uma opção razoável para este tutorial.
* Para configurações adicionais, certifique-se de que o tipo de disco Olá é "Padrão" e aceite que todas Olá padrões restantes.
* Iniciar criação de saudação na página de resumo de saudação.

Executar Olá acima processar duas vezes toocreate duas máquinas virtuais do Linux, uma para Olá web front-end e uma instância do MongoDB hello. Criação de máquinas virtuais de saudação levará cerca de 5 a 10 minutos.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Atribuindo uma entrada DNS para máquinas virtuais
As máquinas virtuais criadas no Azure, por padrão, somente podem ser acessadas com endereço IP público, como 1.2.3.4. Vamos fazer máquinas hello mais facilmente identificáveis, atribuindo-lhes as entradas DNS.

Depois que o portal Olá indica que as máquinas virtuais de saudação tenham sido criadas, clique no link de "Máquinas virtuais" hello na barra de navegação esquerda hello e localize a suas máquinas. Para cada máquina:

* Localize o guia do Essentials hello e clique em Olá endereço IP público;
* Na configuração do endereço IP pública Olá, atribuir um rótulo de nome DNS e salvar.

portal de saudação garantirá que você especificar o nome hello está disponível. Depois de salvar a configuração de hello, as máquinas virtuais terão nomes de host semelhantes muito`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Conectando toohello máquinas virtuais
Quando as máquinas virtuais foram provisionadas, eles eram conexões remotas tooallow pré-configurado via SSH. Esse é o mecanismo de saudação usaremos tooconfigure Olá VMs. Se você estiver usando o Windows para o desenvolvimento, você precisará tooget um cliente SSH se você ainda não tiver um. Uma opção comum é o PuTTY, que pode ser baixado [aqui](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Os sistemas operacionais Macintosh e Linux vêm com uma versão do SSH pré-instalada.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configurando Olá máquina de Virtual de front-end da Web
Máquina de front-end do SSH toohello web que você criou usando PuTTY, ssh linha de comando ou outra ferramenta SSH favorita. Você deve ver uma mensagem de boas-vindas seguida de um prompt de comando.

Primeiro, vamos garantir que tanto o Git quanto o Node estão instalados:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Como o front-end da web do aplicativo hello depende de alguns módulos nativos do Node. js, também precisamos conjunto essencial de saudação de tooinstall de ferramentas de compilação:

    sudo apt-get install -y build-essential

Por fim, vamos instalar um aplicativo Node. js chamado *para sempre*, que ajuda a aplicativos de servidor toorun Node. js:

    sudo npm install -g forever

Estas são todas as dependências de saudação necessárias no front-end da web do aplicativo esta máquina virtual toobe toorun capaz de hello, então vamos que a execução. toodo isso, vamos primeiro criar um clone bare do repositório do GitHub Olá você bifurcada anteriormente para que você pode facilmente publicar atualizações toohello virtual machine (vamos abordar esse cenário de atualização mais tarde) e depois clonar Olá clone bare tooprovide uma versão de hello repositório que, na verdade, pode ser executado.

A partir do diretório do saudação inicial (~), execute o hello comandos a seguir (substituindo *accountname* com seu nome de conta de usuário do GitHub):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Agora insira Olá todo nó diretório e execute estes comandos:

    npm install
    forever start server.js

Olá front-end do aplicativo web está em execução, no entanto, há uma ou mais etapas antes de poder acessar o aplicativo hello em um navegador da web. Olá máquina virtual que você criou é protegida por um recurso do Azure chamado um *grupo de segurança de rede*, que foi criado para você quando você provisionou Olá máquina virtual. No momento, esse recurso permite que somente solicitações externas tooport toobe 22 roteadas toohello máquina virtual, que permite a comunicação SSH com hello máquina, mas nada mais. Portanto Olá tooview de ordem aplicativo TODO, que é toorun configurado na porta 8080, essa porta também precisa toobe aberta.

Retorno toohello Portal do Azure e Olá concluir as etapas a seguir:

* Clique em "Grupos de recursos" na barra de navegação esquerda Olá;
* Selecionar grupo de recursos de saudação que contém sua máquina virtual;
* Na lista resultante de saudação de recursos, selecione o grupo de segurança de rede de hello (Olá um com um ícone de escudo);
* Nas propriedades de saudação, escolha "regras de segurança de entrada";
* Na barra de ferramentas hello, clique em "Adicionar";
* Forneça um nome como "default-allow-todo";
* Definir o protocolo de saudação muito "TCP";
* Definir o intervalo de porta de destino Olá muito "8080;"
* Clique em Okey e aguarde Olá toobe de regra de segurança criado.

Depois de criar essa regra de segurança, Olá aplicativo TODO é visível publicamente em Olá internet e você pode procurar tooit, por exemplo, usando uma URL como:

    http://machinename.region.cloudapp.azure.com:8080

Você observará que mesmo que nós ainda não tiver configurado Olá MongoDB virtual machine, Olá aplicativo TODO aparece toobe totalmente funcional. Isso ocorre porque o repositório de origem de saudação é codificado toouse uma instância previamente implantada do MongoDB. Depois que configuramos Olá MongoDB virtual machine, podemos será voltar e alterar Olá tooutilize de código de origem nossa instância particular do MongoDB em vez disso.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Configurando Olá MongoDB Virtual Machine
SSH toohello segunda máquina que você criou usando PuTTY, ssh linha de comando ou outra ferramenta SSH favorita. Depois de ver a mensagem de boas-vindas hello e prompt de comando, instale o MongoDB (estas instruções foram tiradas da [aqui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Por padrão, o MongoDB é configurado para só poder ser acessado localmente. Para este tutorial, configuraremos MongoDB para que ele possa ser acessado da máquina de virtual do aplicativo hello. Em um contexto de sudo, abra o arquivo de /etc/mongod.conf hello e localize Olá `# network interfaces` seção. Saudação de alteração `net.bindIp` configuração valor muito`0.0.0.0`.

> [!NOTE]
> Essa configuração é para fins de saudação apenas deste tutorial. Ela **NÃO** é uma prática de segurança recomendada e não deve ser usada em ambientes de produção.
> 
> 

Certifique-se agora Olá MongoDB serviço foi iniciado:

    sudo service mongod restart

O MongoDB opera na porta 27017 por padrão. Portanto, em Olá a mesma forma que precisávamos tooopen porta 8080 na máquina virtual do Olá web front-end, precisamos de porta tooopen 27017 na máquina de virtual Olá MongoDB.

Retorno toohello Portal do Azure e Olá concluir as etapas a seguir:

* Clique em "Grupos de recursos" na barra de navegação esquerda Olá;
* Selecionar grupo de recursos de saudação que contém a máquina de virtual do MongoDB Olá;
* Na lista resultante de saudação de recursos, selecione grupo de segurança de rede hello (Olá um com um ícone de escudo) com hello que mesmo nome que você deu a máquina de virtual do MongoDB toohello;
* Nas propriedades de saudação, escolha "regras de segurança de entrada";
* Na barra de ferramentas hello, clique em "Adicionar";
* Forneça um nome como "default-allow-mongo";
* Definir o protocolo de saudação muito "TCP";
* Definir o intervalo de porta de destino Olá muito "27017";
* Clique em Okey e aguarde Olá toobe de regra de segurança criado.

## <a name="iterating-on-hello-todo-application"></a>Iterando em Olá aplicativo TODO
Até agora, podemos ter provisionado duas máquinas virtuais do Linux: um que está executando o aplicativo hello front-end da web e um que está executando uma instância do MongoDB. Mas há um problema - Olá web front-end não está realmente usando Olá provisionado MongoDB instância ainda. Vamos corrigir isso atualizando Olá web front-end código toouse uma variável de ambiente em vez de uma instância embutido.

### <a name="changing-hello-todo-application"></a>Alterar Olá TODO aplicativo
No computador de desenvolvimento em que você clonou primeiro repositório de todo nó hello, abra Olá `node-todo/config/database.js` arquivo em seu editor favorito e altere o valor de url de saudação do valor embutido em hello como `mongodb://...` muito`process.env.MONGODB`.

Confirmar as alterações e enviar por push toohello GitHub mestre:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Infelizmente, isso não publica máquina de virtual Olá alteração toohello web front-end. Vamos fazer algumas alterações toothat máquina virtual tooenable mais um mecanismo simple, porém efetivo para publicar atualizações para que você pode observar rapidamente efeito Olá alterações de saudação em ambiente dinâmico Olá.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configurando Olá máquina de Virtual de front-end da Web
Lembre-se de que é criado anteriormente um clone bare do repositório de todo nó Olá na máquina virtual do Olá web front-end. Na verdade, essa ação criada uma nova Git alterações toowhich remoto podem ser enviadas. No entanto, simplesmente pressionando toothis remoto não bastante dá modelo de iteração rápido Olá procurando por desenvolvedores ao trabalhar em seu código.

O que podemos gostariam de ter toodo capaz de toobe é garantir que, quando ocorre um repositório remoto do push toohello na máquina virtual de hello, aplicativo de tarefas em execução hello é atualizado automaticamente. Felizmente, isso é fácil tooachieve com o git.

Git expõe um número de conexões que são chamados em momentos específicos tooreact tooactions efetuados no repositório de saudação. Eles são especificados usando scripts do shell no repositório de saudação `hooks` pasta. gancho de saudação que é mais aplicável para o cenário de atualização automática de saudação é hello `post-update` eventos.

Em uma SSH sessão toohello web front-end máquina virtual, alterar toohello `~/node-todo.git/hooks` diretório e adicione Olá após o arquivo de conteúdo tooa chamado `post-update` (substituindo `machinename` e `region` com suas informações de máquina virtual do MongoDB):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Certifique-se de que esse arquivo é executável executando Olá comando a seguir:

    chmod 755 post-update

Esse script garante que Olá aplicativo de servidor atual está parado, Olá código repositório clonado Olá é toohello atualizada mais recente, todas as dependências atualizadas são atendidas e Olá servidor é reiniciado. Também garante que o ambiente de saudação foi configurado na preparação para receber nosso primeira instância aplicativo atualização tooget Olá MongoDB de uma variável de ambiente.

### <a name="configuring-your-development-machine"></a>Configurando seu computador de desenvolvimento
Agora vamos em sua máquina de desenvolvimento vinculada a máquina virtual do toohello web front-end. Isso é tão simple quanto adicionar repositório bare Olá na máquina virtual de saudação como um controle remoto. Execute Olá toodo de comando a seguir (substituindo *usuário* com seu nome de logon de máquina virtual de front-end da web e *machinename* e *região* conforme apropriado):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Isso é tudo o que é necessário tooenable enviar por push, ou publicar em vigor, alterações de máquina virtual do toohello web front-end.

### <a name="publishing-updates"></a>Publicação de atualizações
Vamos publicar Olá uma alteração foi feita até o momento para que o aplicativo hello usará sua própria instância do MongoDB:

    git push azure master

Você deve ver toothis semelhante de saída:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Depois que esse comando for concluído, tente atualizar o aplicativo hello em um navegador da web. Você deve ser capaz de toosee que lista de tarefas Olá apresentada aqui está vazia e não mais toohello empatado compartilhado implantados MongoDB instância.

tutorial de saudação toocomplete, vamos fazer a alteração mais visível e outra. No computador de desenvolvimento, abra o arquivo de node-todo/public/index.html de saudação usando seu editor favorito. Localize o cabeçalho de jumbotron Olá e altere o título de saudação do "Eu sou um aholic Todo" muito "eu sou um aholic de tarefas no Azure!".

Agora, vamos confirmar:

    git commit -am "Azurify hello title"

Esse tempo, vamos publicar Olá alteração tooAzure antes de enviar a ele tooback toohello do repositório GitHub:

    git push azure master

Depois que esse comando for concluído, página da web de atualização de saudação e você verá as alterações de saudação. Desde que eles tenham uma boas aparência, push Olá alteração toohello back origem remota: 

    git push origin master

## <a name="next-steps"></a>Próximas etapas
Este artigo mostrado como tootake um aplicativo Node. js e implantá-lo em máquinas virtuais de tooLinux em execução no Azure. toolearn mais sobre máquinas virtuais Linux no Azure, consulte [tooLinux de Introdução no Azure](/documentation/articles/virtual-machines-linux-introduction/).

Para obter mais informações sobre como toodevelop Node. js aplicativos no Azure, consulte Olá [Node. js Developer Center](/develop/nodejs/).

