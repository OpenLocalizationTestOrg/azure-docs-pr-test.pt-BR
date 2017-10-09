---
title: aaaCreate um servidor Jenkins no Azure
description: "Instalar Jenkins em uma máquina virtual de Linux do Azure do modelo de solução Olá Jenkins e criar um aplicativo de Java de exemplo."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Criar um servidor Jenkins em uma VM do Linux do Azure de saudação portal do Azure

Este guia de início rápido mostra como tooinstall [Jenkins](https://jenkins.io) em uma VM do Linux Ubuntu com toowork configurados plug-ins e ferramentas de saudação com o Azure. Ao concluir, você terá um servidor Jenkins em execução no Azure criando um aplicativo Java de exemplo do [GitHub](https://github.com).

## <a name="prerequisites"></a>Pré-requisitos

* Uma assinatura do Azure
* Acesso tooSSH na linha de comando do computador (como Olá Bash shell ou [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Criar hello Jenkins VM de modelo de solução de saudação

Olá abrir [imagem do marketplace para Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) no seu navegador da web e selecione **obter TI agora** do lado esquerdo de saudação da página de saudação. Saudação de revisão, selecione e detalhes de preço **continuar**, em seguida, selecione **criar** Jenkins servidor Olá tooconfigure Olá portal do Azure. 
   
![Diálogo do portal do Azure](./media/install-jenkins-solution-template/ap-create.png)

Em Olá **definir as configurações básicas** guia, preencha Olá campos a seguir:

![Definir as configurações básicas](./media/install-jenkins-solution-template/ap-basic.png)

* Use **Jenkins** como **Nome**.
* Insira um **nome de usuário**. nome de usuário Olá deve atender aos [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Selecione **senha** como Olá **tipo de autenticação** e digite uma senha. senha Olá deve ter um caractere maiusculo, um número e um caractere especial.
* Use **myJenkinsResourceGroup** para Olá **grupo de recursos**.
* Escolha Olá **Leste dos EUA** [região do Azure](https://azure.microsoft.com/regions/) de saudação **local** lista suspensa.

Selecione **Okey** tooproceed toohello **configurar opções adicionais** guia. Insira um único domínio nome tooidentify Olá Jenkins servidor e selecione **Okey**.

![Configurar opções adicionais](./media/install-jenkins-solution-template/ap-addtional.png)  

 Depois que a validação passa, selecione **Okey** novamente do hello **resumo** guia. Por fim, selecione **compra** toocreate Olá Jenkins VM. Quando o servidor estiver pronto, você receberá uma notificação informando em Olá portal do Azure:   

![Notificação Jenkins está pronto](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Conecte-se tooJenkins

Navegue a máquina virtual de tooyour (por exemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) no navegador da web. console de Jenkins Hello está inacessível por meio de HTTP não segura para que as instruções são fornecidas no console do hello página tooaccess Olá Jenkins com segurança do seu computador usando um túnel SSH.

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Configurar o túnel de saudação usando Olá `ssh` comando na página Olá Olá linha de comando, substituindo `username` com o nome da saudação de usuário do administrador de máquina virtual Olá escolhido anteriormente ao configurar a máquina virtual de saudação do modelo de solução de saudação.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Depois de iniciar o túnel de hello, navegar toohttp://localhost:8080 / em seu computador local. 

Obter senha inicial Olá executando Olá comando na linha de comando Olá enquanto estiver conectado por meio do SSH toohello Jenkins VM a seguir.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Desbloquear painel Jenkins Olá Olá pela primeira vez usando essa senha inicial.

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Selecione **instalar plug-ins sugerido** no hello próxima página e, em seguida, crie um painel Jenkins admin do usuário usadas tooaccess Olá Jenkins.

![O Jenkins está pronto!](./media/install-jenkins-solution-template/jenkins-welcome.png)

Olá Jenkins server está pronto toobuild código.

## <a name="create-your-first-job"></a>Criar seu primeiro trabalho

Selecione **criar novos trabalhos** Olá Jenkins no console do, em seguida, nomeie- **mySampleApp** e selecione **projeto Freestyle**, em seguida, selecione **Okey**.

![Criar um novo trabalho](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Selecione Olá **código-fonte gerenciamento** guia, habilite **Git**e digite Olá URL no seguinte **URL do repositório** campo:`https://github.com/spring-guides/gs-spring-boot.git`

![Definir o repositório do Git Olá](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Selecione Olá **criar** guia e, em seguida, selecione **adicionar a etapa de compilação**, **Gradle invocar script**. Selecione **Usar Wrapper Gradle**, digite `complete` na **localização do Wrapper** e `build` como **Tarefas**.

![Use Olá Gradle wrapper toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Selecione **Avançado** e, em seguida, digite `complete` em Olá **raiz criar script** campo. Selecione **Salvar**.

![Definir as configurações avançadas na etapa de compilação Olá Gradle wrapper](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Criar código Olá

Selecione **criar agora** toocompile Olá código e pacote hello aplicativo de exemplo. Quando a compilação for concluída, selecione Olá **espaço de trabalho** link para o projeto de saudação.

![Procurar arquivo toohello espaço de trabalho tooget Olá JAR da compilação de saudação](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Navegue muito`complete/build/libs` e certifique-se de saudação `gs-spring-boot-0.1.0.jar` há tooverify que a compilação foi bem-sucedida. Seu Jenkins servidor agora está pronto toobuild seus projetos no Azure.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Adicionar VMs do Azure como agentes do Jenkins](jenkins-azure-vm-agents.md)
