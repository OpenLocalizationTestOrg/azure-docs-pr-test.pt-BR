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
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="48c09-103">Criar um servidor Jenkins em uma VM do Linux do Azure de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48c09-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="48c09-104">Este guia de início rápido mostra como tooinstall [Jenkins](https://jenkins.io) em uma VM do Linux Ubuntu com toowork configurados plug-ins e ferramentas de saudação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="48c09-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="48c09-105">Ao concluir, você terá um servidor Jenkins em execução no Azure criando um aplicativo Java de exemplo do [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="48c09-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48c09-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="48c09-106">Prerequisites</span></span>

* <span data-ttu-id="48c09-107">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="48c09-107">An Azure subscription</span></span>
* <span data-ttu-id="48c09-108">Acesso tooSSH na linha de comando do computador (como Olá Bash shell ou [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="48c09-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="48c09-109">Criar hello Jenkins VM de modelo de solução de saudação</span><span class="sxs-lookup"><span data-stu-id="48c09-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="48c09-110">Olá abrir [imagem do marketplace para Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) no seu navegador da web e selecione **obter TI agora** do lado esquerdo de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="48c09-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="48c09-111">Saudação de revisão, selecione e detalhes de preço **continuar**, em seguida, selecione **criar** Jenkins servidor Olá tooconfigure Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="48c09-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Diálogo do portal do Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="48c09-113">Em Olá **definir as configurações básicas** guia, preencha Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="48c09-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Definir as configurações básicas](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="48c09-115">Use **Jenkins** como **Nome**.</span><span class="sxs-lookup"><span data-stu-id="48c09-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="48c09-116">Insira um **nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="48c09-116">Enter a **User name**.</span></span> <span data-ttu-id="48c09-117">nome de usuário Olá deve atender aos [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="48c09-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="48c09-118">Selecione **senha** como Olá **tipo de autenticação** e digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="48c09-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="48c09-119">senha Olá deve ter um caractere maiusculo, um número e um caractere especial.</span><span class="sxs-lookup"><span data-stu-id="48c09-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="48c09-120">Use **myJenkinsResourceGroup** para Olá **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="48c09-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="48c09-121">Escolha Olá **Leste dos EUA** [região do Azure](https://azure.microsoft.com/regions/) de saudação **local** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="48c09-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="48c09-122">Selecione **Okey** tooproceed toohello **configurar opções adicionais** guia. Insira um único domínio nome tooidentify Olá Jenkins servidor e selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="48c09-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Configurar opções adicionais](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="48c09-124">Depois que a validação passa, selecione **Okey** novamente do hello **resumo** guia. Por fim, selecione **compra** toocreate Olá Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="48c09-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="48c09-125">Quando o servidor estiver pronto, você receberá uma notificação informando em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="48c09-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Notificação Jenkins está pronto](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="48c09-127">Conecte-se tooJenkins</span><span class="sxs-lookup"><span data-stu-id="48c09-127">Connect tooJenkins</span></span>

<span data-ttu-id="48c09-128">Navegue a máquina virtual de tooyour (por exemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) no navegador da web.</span><span class="sxs-lookup"><span data-stu-id="48c09-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="48c09-129">console de Jenkins Hello está inacessível por meio de HTTP não segura para que as instruções são fornecidas no console do hello página tooaccess Olá Jenkins com segurança do seu computador usando um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="48c09-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="48c09-131">Configurar o túnel de saudação usando Olá `ssh` comando na página Olá Olá linha de comando, substituindo `username` com o nome da saudação de usuário do administrador de máquina virtual Olá escolhido anteriormente ao configurar a máquina virtual de saudação do modelo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="48c09-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="48c09-132">Depois de iniciar o túnel de hello, navegar toohttp://localhost:8080 / em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="48c09-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="48c09-133">Obter senha inicial Olá executando Olá comando na linha de comando Olá enquanto estiver conectado por meio do SSH toohello Jenkins VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="48c09-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="48c09-134">Desbloquear painel Jenkins Olá Olá pela primeira vez usando essa senha inicial.</span><span class="sxs-lookup"><span data-stu-id="48c09-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="48c09-136">Selecione **instalar plug-ins sugerido** no hello próxima página e, em seguida, crie um painel Jenkins admin do usuário usadas tooaccess Olá Jenkins.</span><span class="sxs-lookup"><span data-stu-id="48c09-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![O Jenkins está pronto!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="48c09-138">Olá Jenkins server está pronto toobuild código.</span><span class="sxs-lookup"><span data-stu-id="48c09-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="48c09-139">Criar seu primeiro trabalho</span><span class="sxs-lookup"><span data-stu-id="48c09-139">Create your first job</span></span>

<span data-ttu-id="48c09-140">Selecione **criar novos trabalhos** Olá Jenkins no console do, em seguida, nomeie- **mySampleApp** e selecione **projeto Freestyle**, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="48c09-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Criar um novo trabalho](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="48c09-142">Selecione Olá **código-fonte gerenciamento** guia, habilite **Git**e digite Olá URL no seguinte **URL do repositório** campo:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="48c09-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definir o repositório do Git Olá](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="48c09-144">Selecione Olá **criar** guia e, em seguida, selecione **adicionar a etapa de compilação**, **Gradle invocar script**.</span><span class="sxs-lookup"><span data-stu-id="48c09-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="48c09-145">Selecione **Usar Wrapper Gradle**, digite `complete` na **localização do Wrapper** e `build` como **Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="48c09-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Use Olá Gradle wrapper toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="48c09-147">Selecione **Avançado**</span><span class="sxs-lookup"><span data-stu-id="48c09-147">Select **Advanced..**</span></span> <span data-ttu-id="48c09-148">e, em seguida, digite `complete` em Olá **raiz criar script** campo.</span><span class="sxs-lookup"><span data-stu-id="48c09-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="48c09-149">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48c09-149">Select **Save**.</span></span>

![Definir as configurações avançadas na etapa de compilação Olá Gradle wrapper](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="48c09-151">Criar código Olá</span><span class="sxs-lookup"><span data-stu-id="48c09-151">Build hello code</span></span>

<span data-ttu-id="48c09-152">Selecione **criar agora** toocompile Olá código e pacote hello aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="48c09-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="48c09-153">Quando a compilação for concluída, selecione Olá **espaço de trabalho** link para o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="48c09-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Procurar arquivo toohello espaço de trabalho tooget Olá JAR da compilação de saudação](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="48c09-155">Navegue muito`complete/build/libs` e certifique-se de saudação `gs-spring-boot-0.1.0.jar` há tooverify que a compilação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="48c09-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="48c09-156">Seu Jenkins servidor agora está pronto toobuild seus projetos no Azure.</span><span class="sxs-lookup"><span data-stu-id="48c09-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c09-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48c09-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48c09-158">Adicionar VMs do Azure como agentes do Jenkins</span><span class="sxs-lookup"><span data-stu-id="48c09-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
