---
title: Criar um servidor Jenkins no Azure
description: "Instale o Jenkins em uma máquina virtual Linux do Azure no modelo de solução Jenkins e crie um aplicativo Java de exemplo."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="3e0e6-103">Criar um servidor Jenkins em uma VM Linux do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3e0e6-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="3e0e6-104">Este guia de início rápido mostra como instalar o [Jenkins](https://jenkins.io) em uma VM Linux Ubuntu com as ferramentas e os plug-ins configurados para funcionar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="3e0e6-105">Ao concluir, você terá um servidor Jenkins em execução no Azure criando um aplicativo Java de exemplo do [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="3e0e6-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e0e6-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3e0e6-106">Prerequisites</span></span>

* <span data-ttu-id="3e0e6-107">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="3e0e6-107">An Azure subscription</span></span>
* <span data-ttu-id="3e0e6-108">Acesso a SSH na linha de comando do computador (como o shell Bash ou o [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="3e0e6-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="3e0e6-109">Criar a VM Jenkins do modelo de solução</span><span class="sxs-lookup"><span data-stu-id="3e0e6-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="3e0e6-110">Abra a [imagem do marketplace para o Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) no seu navegador da Web e selecione **OBTER AGORA** no lado esquerdo da página.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="3e0e6-111">Examine os detalhes de preços e selecione **Continuar**. Em seguida, selecione **Criar** para configurar o servidor Jenkins no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Diálogo do portal do Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="3e0e6-113">Na guia **Definir as configurações básicas**, preencha os campos abaixo:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Definir as configurações básicas](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="3e0e6-115">Use **Jenkins** como **Nome**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="3e0e6-116">Insira um **nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-116">Enter a **User name**.</span></span> <span data-ttu-id="3e0e6-117">O nome de usuário deve atender aos [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="3e0e6-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="3e0e6-118">Selecione **Senha** como **Tipo de autenticação** e digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="3e0e6-119">A senha deve conter um caractere em maiúscula, um número e um caractere especial.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="3e0e6-120">Use **myJenkinsResourceGroup** como **Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="3e0e6-121">Escolha o **Leste dos EUA** como [região do Azure](https://azure.microsoft.com/regions/) na lista suspensa **Localização**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="3e0e6-122">Selecione **OK** para prosseguir para a guia **Configurar opções adicionais**. Insira um nome de domínio exclusivo para identificar o servidor Jenkins e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![Configurar opções adicionais](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="3e0e6-124">Depois de validado, selecione **OK** novamente na guia **Resumo**. Por fim, selecione **Comprar** para criar a VM Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="3e0e6-125">Quando o servidor estiver pronto, você receberá uma notificação no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="3e0e6-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Notificação Jenkins está pronto](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="3e0e6-127">Conectar-se ao Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e0e6-127">Connect to Jenkins</span></span>

<span data-ttu-id="3e0e6-128">Navegue até sua máquina virtual (por exemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="3e0e6-129">O console do Jenkins não pode ser acessado por meio de HTTP não segura e, portanto, instruções são fornecidas na página para acessar o console do Jenkins com segurança do seu computador usando um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="3e0e6-131">Configure o túnel usando o comando `ssh` na página a partir da linha de comando, substituindo `username` pelo nome do usuário administrador da máquina virtual escolhido anteriormente durante a configuração da máquina virtual no modelo de solução.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="3e0e6-132">Depois de iniciar o túnel, navegue para http://localhost:8080/ em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="3e0e6-133">Obtenha a senha inicial executando o comando abaixo na linha de comando, enquanto estiver conectado à VM Jenkins por meio do SSH.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="3e0e6-134">Desbloqueie o painel Jenkins pela primeira vez usando essa senha inicial.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Desbloquear Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="3e0e6-136">Selecione **Instalar plug-ins sugeridos** na próxima página e crie um usuário administrador do Jenkins usado para acessar o painel do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![O Jenkins está pronto!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="3e0e6-138">O servidor Jenkins agora está pronto para compilar código.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="3e0e6-139">Criar seu primeiro trabalho</span><span class="sxs-lookup"><span data-stu-id="3e0e6-139">Create your first job</span></span>

<span data-ttu-id="3e0e6-140">Selecione **Criar novos trabalhos** no console do Jenkins, nomeie-o **mySampleApp** e selecione **projeto Freestyle**. Em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Criar um novo trabalho](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="3e0e6-142">Selecione a guia **Gerenciamento de código-fonte**, habilite o **Git**e digite a seguinte URL no campo **URL do Repositório**:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="3e0e6-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definir o repositório Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="3e0e6-144">Selecione a guia **Build** e selecione **Adicionar etapa de compilação**, **Invocar script Gradle**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="3e0e6-145">Selecione **Usar Wrapper Gradle**, digite `complete` na **localização do Wrapper** e `build` como **Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Use o wrapper Gradle para compilar](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="3e0e6-147">Selecione **Avançado**</span><span class="sxs-lookup"><span data-stu-id="3e0e6-147">Select **Advanced..**</span></span> <span data-ttu-id="3e0e6-148">e digite `complete` no campo **Script da Compilação da Raiz**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="3e0e6-149">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-149">Select **Save**.</span></span>

![Definir as configurações avançadas na etapa de compilação do wrapper Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="3e0e6-151">Compilar o código</span><span class="sxs-lookup"><span data-stu-id="3e0e6-151">Build the code</span></span>

<span data-ttu-id="3e0e6-152">Selecione **Criar agora** para compilar o código e empacotar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="3e0e6-153">Quando a compilação for concluída, selecione o link **Espaço de Trabalho** para o projeto.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Navegue até o espaço de trabalho para obter o arquivo JAR da compilação](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="3e0e6-155">Navegue até `complete/build/libs` e verifique se o `gs-spring-boot-0.1.0.jar` está disponível a fim de verificar se a compilação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="3e0e6-156">O servidor Jenkins agora está pronto para criar seus próprios projetos no Azure.</span><span class="sxs-lookup"><span data-stu-id="3e0e6-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e0e6-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e0e6-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e0e6-158">Adicionar VMs do Azure como agentes do Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e0e6-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
