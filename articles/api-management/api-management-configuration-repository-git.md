---
title: "Configurar o serviço de Gerenciamento de API usando o Git - Azure | Microsoft Docs"
description: "Saiba como salvar e definir a configuração de seu serviço de Gerenciamento de API usando o Git"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="2fddc-103">Como salvar e definir a configuração de seu serviço de Gerenciamento de API usando o Git</span><span class="sxs-lookup"><span data-stu-id="2fddc-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="2fddc-104">Cada instância do serviço de Gerenciamento de API mantém um banco de dados de configuração que contém informações sobre a configuração e sobre os metadados da instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="2fddc-105">É possível fazer alterações na instância do serviço alterando uma configuração no portal do editor, usando um cmdlet do PowerShell ou fazendo uma chamada à API REST.</span><span class="sxs-lookup"><span data-stu-id="2fddc-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="2fddc-106">Além desses métodos, você também pode gerenciar a configuração da instância do serviço usando o Git, permitindo cenários de gerenciamento de serviço, como:</span><span class="sxs-lookup"><span data-stu-id="2fddc-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="2fddc-107">Controle de versão da configuração - baixe e armazene versões diferentes da configuração do seu serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="2fddc-108">Alterações de configuração em massa - faça alterações em várias partes da configuração de seu serviço no repositório local e integre essas alterações no servidor com uma única operação</span><span class="sxs-lookup"><span data-stu-id="2fddc-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="2fddc-109">Cadeia de ferramentas e fluxo de trabalho conhecido do Git - use as ferramentas e fluxo de trabalho do Git com os quais você já está familiarizado</span><span class="sxs-lookup"><span data-stu-id="2fddc-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="2fddc-110">O diagrama a seguir mostra uma visão geral das diferentes maneiras de configurar sua instância de serviço do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2fddc-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Configuração do Git][api-management-git-configure]

<span data-ttu-id="2fddc-112">Quando você faz alterações em seu serviço usando o portal do editor, cmdlets do PowerShell ou a API REST, você está gerenciando o banco de dados de configuração de seu serviço usando o ponto de extremidade `https://{name}.management.azure-api.net` , como exibido no lado direito do diagrama.</span><span class="sxs-lookup"><span data-stu-id="2fddc-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="2fddc-113">O lado esquerdo do diagrama ilustra como você pode gerenciar a configuração de seu serviço usando o Git e o repositório Git de seu serviço localizado em `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="2fddc-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="2fddc-114">As etapas a seguir fornecem uma visão geral do gerenciamento de sua instância de serviço de Gerenciamento de API usando o Git.</span><span class="sxs-lookup"><span data-stu-id="2fddc-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="2fddc-115">Acessar a configuração GIT em seu serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="2fddc-116">Salvar o banco de dados de configuração de seu serviço em seu repositório Git</span><span class="sxs-lookup"><span data-stu-id="2fddc-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="2fddc-117">Clonar o repositório Git em seu computador local</span><span class="sxs-lookup"><span data-stu-id="2fddc-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="2fddc-118">Obter o repositório mais recente em seu computador local, confirmar e enviar as alterações de volta ao seu repositório</span><span class="sxs-lookup"><span data-stu-id="2fddc-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="2fddc-119">Implantar as alterações de seu repositório para o banco de dados de configuração de seu serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="2fddc-120">Este artigo descreve como habilitar e usar o Git para gerenciar a configuração de seu serviço e fornece uma referência para os arquivos e pastas no repositório Git.</span><span class="sxs-lookup"><span data-stu-id="2fddc-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="2fddc-121">Acessar a configuração GIT em seu serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-121">Access Git configuration in your service</span></span>
<span data-ttu-id="2fddc-122">Você pode exibir rapidamente o status da configuração do Git exibindo o ícone do Git no canto superior direito do portal do editor.</span><span class="sxs-lookup"><span data-stu-id="2fddc-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="2fddc-123">Neste exemplo, a mensagem de status indica que há alterações não salvas no repositório.</span><span class="sxs-lookup"><span data-stu-id="2fddc-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="2fddc-124">Isso ocorre porque o banco de dados de configuração do serviço de Gerenciamento de API ainda não foi salvo no repositório.</span><span class="sxs-lookup"><span data-stu-id="2fddc-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Status do Git][api-management-git-icon-enable]

<span data-ttu-id="2fddc-126">Para exibir e definir as configurações do Git, clique no ícone do Git ou clique no menu **Segurança** e navegue até a guia **Repositório de configuração**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Habilitar o GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="2fddc-128">Quaisquer segredos que não sejam definidos como propriedades serão armazenados no repositório e permanecerão em seu histórico até que você desabilite e habilite novamente o acesso ao Git.</span><span class="sxs-lookup"><span data-stu-id="2fddc-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="2fddc-129">As propriedades fornecem um local seguro para o gerenciamento de valores constantes de cadeia de caracteres, incluindo segredos, em todas as configurações e políticas de API. Portanto, não é necessário armazená-los diretamente nas instruções de sua política.</span><span class="sxs-lookup"><span data-stu-id="2fddc-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="2fddc-130">Para saber mais, confira [Como usar as propriedades nas políticas de Gerenciamento de API do Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="2fddc-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="2fddc-131">Para saber mais sobre como habilitar ou desabilitar o acesso ao Git usando a API REST, confira [Habilitar ou desabilitar o acesso ao Git usando a API REST](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="2fddc-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="2fddc-132">Para salvar a configuração do serviço no repositório Git</span><span class="sxs-lookup"><span data-stu-id="2fddc-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="2fddc-133">A primeira etapa antes de clonar o repositório é salvar o estado atual da configuração do serviço no repositório.</span><span class="sxs-lookup"><span data-stu-id="2fddc-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="2fddc-134">Clique em **Salvar configuração no repositório**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-134">Click **Save configuration to repository**.</span></span>

![Salvar configuração][api-management-save-configuration]

<span data-ttu-id="2fddc-136">Faça as alterações desejadas na tela de confirmação e clique em **Ok** para salvar.</span><span class="sxs-lookup"><span data-stu-id="2fddc-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Salvar configuração][api-management-save-configuration-confirm]

<span data-ttu-id="2fddc-138">Após alguns instantes, a configuração será salva e o status da configuração do repositório será exibido, incluindo a data e a hora da última alteração de configuração e a última sincronização entre a configuração do serviço e o repositório.</span><span class="sxs-lookup"><span data-stu-id="2fddc-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Status da configuração][api-management-configuration-status]

<span data-ttu-id="2fddc-140">Quando a configuração for salva no repositório, ele poderá ser clonado.</span><span class="sxs-lookup"><span data-stu-id="2fddc-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="2fddc-141">Para saber mais sobre como executar essa operação usando a API REST, confira [Confirmar a configuração do instantâneo usando a API REST](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="2fddc-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="2fddc-142">Para clonar o repositório em seu computador local</span><span class="sxs-lookup"><span data-stu-id="2fddc-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="2fddc-143">Para clonar um repositório, você precisa da URL de seu repositório, um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="2fddc-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="2fddc-144">O nome de usuário e a URL são exibidos próximos à parte superior da guia **Repositório de configuração** .</span><span class="sxs-lookup"><span data-stu-id="2fddc-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Clone do Git][api-management-configuration-git-clone]

<span data-ttu-id="2fddc-146">A senha é gerada na parte inferior da guia **Repositório de configuração** .</span><span class="sxs-lookup"><span data-stu-id="2fddc-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Gerar senha][api-management-generate-password]

<span data-ttu-id="2fddc-148">Para gerar uma senha, primeiro verifique se **Vencimento** está definido como a data e a hora de vencimento desejadas e clique em **Gerar Token**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Senha][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="2fddc-150">Anote essa senha.</span><span class="sxs-lookup"><span data-stu-id="2fddc-150">Make a note of this password.</span></span> <span data-ttu-id="2fddc-151">Depois que você sair desta página a senha não será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="2fddc-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="2fddc-152">Os exemplos a seguir usam a ferramenta Git Bash do [Git para Windows](http://www.git-scm.com/downloads) , mas você pode usar qualquer ferramenta Git com a qual esteja familiarizado.</span><span class="sxs-lookup"><span data-stu-id="2fddc-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="2fddc-153">Abra sua ferramenta Git na pasta desejada e execute o comando a seguir para clonar o repositório git em seu computador local usando o comando fornecido pelo portal do editor.</span><span class="sxs-lookup"><span data-stu-id="2fddc-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="2fddc-154">Quando solicitado, forneça o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="2fddc-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="2fddc-155">Se ocorrer algum erro, tente modificar seu comando `git clone` para incluir o nome de usuário e a senha, conforme exibido no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fddc-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="2fddc-156">Se isso resultar em erro, tente codificar na URL a parte da senha do comando.</span><span class="sxs-lookup"><span data-stu-id="2fddc-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="2fddc-157">Uma maneira rápida de fazer isso é abrir o Visual Studio e emitir o seguinte comando na **Janela Imediata**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="2fddc-158">Para abrir a **Janela Imediata**, abra qualquer solução ou projeto no Visual Studio (ou crie um novo aplicativo de console vazio) e escolha **Janelas**, **Imediata** no menu **Depuração**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="2fddc-159">Use a senha codificada juntamente com seu nome de usuário e o local do repositório para construir o comando do git.</span><span class="sxs-lookup"><span data-stu-id="2fddc-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="2fddc-160">Assim que o repositório for clonado, você poderá exibi-lo e trabalhar com ele no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="2fddc-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="2fddc-161">Para obter mais informações, veja [Referência da estrutura de pastas e arquivos do repositório Git local](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="2fddc-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="2fddc-162">Para atualizar seu repositório local com a configuração mais recente da instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="2fddc-163">Se você fizer alterações na instância de seu serviço de Gerenciamento de API no portal do editor, ou usando a API REST, será necessário salvar essas alterações no repositório antes de poder atualizar seu repositório local com as alterações mais recentes.</span><span class="sxs-lookup"><span data-stu-id="2fddc-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="2fddc-164">Para fazer isso, clique em **Salvar configuração no repositório** na guia **Repositório de configuração** no portal do editor e emita o seguinte comando em seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="2fddc-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="2fddc-165">Antes de executar o `git pull` , certifique-se de que você esteja na pasta de seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="2fddc-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="2fddc-166">Se você acabou de concluir o comando `git clone` , será necessário alterar o diretório de seu repositório executando um comando parecido com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="2fddc-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="2fddc-167">Para enviar por push as alterações de seu repositório local para o repositório do servidor</span><span class="sxs-lookup"><span data-stu-id="2fddc-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="2fddc-168">Para enviar por push as alterações de seu repositório local para o repositório do servidor, você deve confirmar as alterações e, em seguida, enviá-las ao repositório do servidor.</span><span class="sxs-lookup"><span data-stu-id="2fddc-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="2fddc-169">Para confirmar as alterações, abra sua ferramenta de comando do Git, alterne para o diretório de seu repositório local e execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fddc-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="2fddc-170">Para enviar por push todas as confirmações para o servidor, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fddc-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="2fddc-171">Para implantar quaisquer alterações da configuração do serviço na instância do serviço de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="2fddc-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="2fddc-172">Após a confirmação de suas alterações locais e o envio para o repositório do servidor, você pode implantá-las na instância de seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2fddc-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Implantar][api-management-configuration-deploy]

<span data-ttu-id="2fddc-174">Para saber mais sobre como executar essa operação usando a API REST, confira [Implantar as alterações do Git no banco de dados de configuração usando a API REST](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="2fddc-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="2fddc-175">Referência da estrutura de pastas e arquivos do repositório Git local</span><span class="sxs-lookup"><span data-stu-id="2fddc-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="2fddc-176">Os arquivos e pastas no repositório git local contêm as informações de configuração sobre a instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="2fddc-177">Item</span><span class="sxs-lookup"><span data-stu-id="2fddc-177">Item</span></span> | <span data-ttu-id="2fddc-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="2fddc-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2fddc-179">pasta api-management raiz</span><span class="sxs-lookup"><span data-stu-id="2fddc-179">root api-management folder</span></span> |<span data-ttu-id="2fddc-180">Contém a configuração de nível superior da instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="2fddc-181">pasta apis</span><span class="sxs-lookup"><span data-stu-id="2fddc-181">apis folder</span></span> |<span data-ttu-id="2fddc-182">Contém a configuração das APIs na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="2fddc-183">pasta groups</span><span class="sxs-lookup"><span data-stu-id="2fddc-183">groups folder</span></span> |<span data-ttu-id="2fddc-184">Contém a configuração dos grupos na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="2fddc-185">pasta policies</span><span class="sxs-lookup"><span data-stu-id="2fddc-185">policies folder</span></span> |<span data-ttu-id="2fddc-186">Contém as políticas na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="2fddc-187">pasta portalStyles</span><span class="sxs-lookup"><span data-stu-id="2fddc-187">portalStyles folder</span></span> |<span data-ttu-id="2fddc-188">Contém a configuração das personalizações do portal do desenvolvedor na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="2fddc-189">pasta products</span><span class="sxs-lookup"><span data-stu-id="2fddc-189">products folder</span></span> |<span data-ttu-id="2fddc-190">Contém a configuração dos produtos na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="2fddc-191">pasta templates</span><span class="sxs-lookup"><span data-stu-id="2fddc-191">templates folder</span></span> |<span data-ttu-id="2fddc-192">Contém a configuração dos modelos de email na instância do serviço</span><span class="sxs-lookup"><span data-stu-id="2fddc-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="2fddc-193">Cada pasta pode conter um ou mais arquivos e, em alguns casos, uma ou mais pastas, por exemplo, uma pasta para cada API, produto ou grupo.</span><span class="sxs-lookup"><span data-stu-id="2fddc-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="2fddc-194">Os arquivos em cada pasta são específicos ao tipo de entidade descrito pelo nome da pasta.</span><span class="sxs-lookup"><span data-stu-id="2fddc-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="2fddc-195">Tipo de arquivo</span><span class="sxs-lookup"><span data-stu-id="2fddc-195">File type</span></span> | <span data-ttu-id="2fddc-196">Finalidade</span><span class="sxs-lookup"><span data-stu-id="2fddc-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="2fddc-197">json</span><span class="sxs-lookup"><span data-stu-id="2fddc-197">json</span></span> |<span data-ttu-id="2fddc-198">Informações de configuração sobre a respectiva entidade</span><span class="sxs-lookup"><span data-stu-id="2fddc-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="2fddc-199">html</span><span class="sxs-lookup"><span data-stu-id="2fddc-199">html</span></span> |<span data-ttu-id="2fddc-200">Descrições sobre a entidade, geralmente exibidas no portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2fddc-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="2fddc-201">xml</span><span class="sxs-lookup"><span data-stu-id="2fddc-201">xml</span></span> |<span data-ttu-id="2fddc-202">Declarações de políticas</span><span class="sxs-lookup"><span data-stu-id="2fddc-202">Policy statements</span></span> |
| <span data-ttu-id="2fddc-203">css</span><span class="sxs-lookup"><span data-stu-id="2fddc-203">css</span></span> |<span data-ttu-id="2fddc-204">Folhas de estilo para personalização do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2fddc-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="2fddc-205">Esses arquivos podem ser criados, excluídos, editados e gerenciados em seu sistema de arquivos local, e as alterações podem ser implantadas de volta na instância de seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2fddc-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="2fddc-206">As entidades a seguir não estão no repositório Git e não podem ser configuradas usando o Git.</span><span class="sxs-lookup"><span data-stu-id="2fddc-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="2fddc-207">Usuários</span><span class="sxs-lookup"><span data-stu-id="2fddc-207">Users</span></span>
> * <span data-ttu-id="2fddc-208">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="2fddc-208">Subscriptions</span></span>
> * <span data-ttu-id="2fddc-209">Propriedades</span><span class="sxs-lookup"><span data-stu-id="2fddc-209">Properties</span></span>
> * <span data-ttu-id="2fddc-210">Outras entidades do portal do desenvolvedor além dos estilos</span><span class="sxs-lookup"><span data-stu-id="2fddc-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="2fddc-211">Pasta api-management raiz</span><span class="sxs-lookup"><span data-stu-id="2fddc-211">Root api-management folder</span></span>
<span data-ttu-id="2fddc-212">A pasta `api-management` raiz contém um arquivo `configuration.json` com informações de alto nível sobre a instância do serviço no seguinte formato.</span><span class="sxs-lookup"><span data-stu-id="2fddc-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="2fddc-213">As primeiras quatro configurações (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` e `UserRegistrationTermsConsentRequired`) são mapeadas para as seguintes configurações na guia **Identidades** da seção **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="2fddc-214">Configuração de identidade</span><span class="sxs-lookup"><span data-stu-id="2fddc-214">Identity setting</span></span> | <span data-ttu-id="2fddc-215">É mapeada para</span><span class="sxs-lookup"><span data-stu-id="2fddc-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="2fddc-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="2fddc-216">RegistrationEnabled</span></span> |<span data-ttu-id="2fddc-217">**Redirecionar usuários anônimos para a página de entrada** </span><span class="sxs-lookup"><span data-stu-id="2fddc-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="2fddc-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="2fddc-218">UserRegistrationTerms</span></span> |<span data-ttu-id="2fddc-219">**Termos de uso na inscrição do usuário** </span><span class="sxs-lookup"><span data-stu-id="2fddc-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="2fddc-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="2fddc-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="2fddc-221">**Mostrar os termos de uso na página de entrada** </span><span class="sxs-lookup"><span data-stu-id="2fddc-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="2fddc-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="2fddc-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="2fddc-223">**Exigir consentimento** </span><span class="sxs-lookup"><span data-stu-id="2fddc-223">**Require consent** checkbox</span></span> |

![Configurações de identidade][api-management-identity-settings]

<span data-ttu-id="2fddc-225">As quatro configurações seguintes (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` e `DelegationValidationKey`) são mapeadas para as seguintes configurações na guia **Delegação** da seção **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="2fddc-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="2fddc-226">Configuração de delegação</span><span class="sxs-lookup"><span data-stu-id="2fddc-226">Delegation setting</span></span> | <span data-ttu-id="2fddc-227">É mapeada para</span><span class="sxs-lookup"><span data-stu-id="2fddc-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="2fddc-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="2fddc-228">DelegationEnabled</span></span> |<span data-ttu-id="2fddc-229">Caixa de seleção **Delegar entrada e inscrição**</span><span class="sxs-lookup"><span data-stu-id="2fddc-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="2fddc-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="2fddc-230">DelegationUrl</span></span> |<span data-ttu-id="2fddc-231">**URL do ponto de extremidade da delegação** </span><span class="sxs-lookup"><span data-stu-id="2fddc-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="2fddc-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="2fddc-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="2fddc-233">**Delegar assinatura do produto** </span><span class="sxs-lookup"><span data-stu-id="2fddc-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="2fddc-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="2fddc-234">DelegationValidationKey</span></span> |<span data-ttu-id="2fddc-235">**Delegar Chave de Validação** </span><span class="sxs-lookup"><span data-stu-id="2fddc-235">**Delegate Validation Key** textbox</span></span> |

![Configurações de delegação][api-management-delegation-settings]

<span data-ttu-id="2fddc-237">A configuração final, `$ref-policy`, é mapeada para o arquivo de instruções de política global da instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="2fddc-238">pasta apis</span><span class="sxs-lookup"><span data-stu-id="2fddc-238">apis folder</span></span>
<span data-ttu-id="2fddc-239">A pasta `apis` contém uma pasta para cada API na instância do serviço que contém os itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fddc-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="2fddc-240">`apis\<api name>\configuration.json` - é a configuração da API e contém informações sobre a URL do serviço de back-end e as operações.</span><span class="sxs-lookup"><span data-stu-id="2fddc-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="2fddc-241">Essas são as mesmas informações que retornariam se você chamasse [Obter uma API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) com `export=true` no formato `application/json`.</span><span class="sxs-lookup"><span data-stu-id="2fddc-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="2fddc-242">`apis\<api name>\api.description.html` - é a descrição da API e corresponde à propriedade `description` da [entidade da API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="2fddc-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="2fddc-243">`apis\<api name>\operations\` - esta pasta contém os arquivos `<operation name>.description.html` que são mapeados para as operações na API.</span><span class="sxs-lookup"><span data-stu-id="2fddc-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="2fddc-244">Cada arquivo contém a descrição de uma única operação na API que mapeia para a propriedade `description` da [entidade de operação](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) na API REST.</span><span class="sxs-lookup"><span data-stu-id="2fddc-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="2fddc-245">pasta groups</span><span class="sxs-lookup"><span data-stu-id="2fddc-245">groups folder</span></span>
<span data-ttu-id="2fddc-246">A pasta `groups` contém uma pasta para cada grupo definido na instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="2fddc-247">`groups\<group name>\configuration.json` - é a configuração do grupo.</span><span class="sxs-lookup"><span data-stu-id="2fddc-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="2fddc-248">Essas são as mesmas informações que retornariam se você chamasse a operação [Obter um grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .</span><span class="sxs-lookup"><span data-stu-id="2fddc-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="2fddc-249">`groups\<group name>\description.html` - é a descrição do grupo e corresponde à propriedade `description` da [entidade de grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="2fddc-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="2fddc-250">pasta policies</span><span class="sxs-lookup"><span data-stu-id="2fddc-250">policies folder</span></span>
<span data-ttu-id="2fddc-251">A pasta `policies` contém as instruções da política para a instância de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="2fddc-252">`policies\global.xml` - contém políticas definidas no escopo global da instância de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="2fddc-253">`policies\apis\<api name>\` - se houver alguma política definida no escopo da API, ela estará nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="2fddc-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="2fddc-254">Pasta `policies\apis\<api name>\<operation name>\` - se houver alguma política definida no escopo da operação, ela estará nessa pasta, nos arquivos `<operation name>.xml`, que são mapeados para as instruções da política de cada operação.</span><span class="sxs-lookup"><span data-stu-id="2fddc-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="2fddc-255">`policies\products\` - se houver alguma política definida no escopo do produto, ela estará nessa pasta, que contém os arquivos `<product name>.xml`, que são mapeados para as instruções da política de cada produto.</span><span class="sxs-lookup"><span data-stu-id="2fddc-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="2fddc-256">pasta portalStyles</span><span class="sxs-lookup"><span data-stu-id="2fddc-256">portalStyles folder</span></span>
<span data-ttu-id="2fddc-257">A pasta `portalStyles` contém folhas de estilo e configuração para personalizações do portal do desenvolvedor da instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="2fddc-258">`portalStyles\configuration.json` - contém os nomes das folhas de estilo usadas pelo portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="2fddc-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="2fddc-259">`portalStyles\<style name>.css` - cada arquivo `<style name>.css` contém estilos para o portal do desenvolvedor (`Preview.css` e `Production.css` por padrão).</span><span class="sxs-lookup"><span data-stu-id="2fddc-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="2fddc-260">pasta products</span><span class="sxs-lookup"><span data-stu-id="2fddc-260">products folder</span></span>
<span data-ttu-id="2fddc-261">A pasta `products` contém uma pasta para cada produto definida na instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="2fddc-262">`products\<product name>\configuration.json` - é a configuração do produto.</span><span class="sxs-lookup"><span data-stu-id="2fddc-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="2fddc-263">Essas são as mesmas informações que retornariam se você chamasse a operação [Obter um produto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .</span><span class="sxs-lookup"><span data-stu-id="2fddc-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="2fddc-264">`products\<product name>\product.description.html` - é a descrição do produto e corresponde à propriedade `description` da [entidade do produto](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) na API REST.</span><span class="sxs-lookup"><span data-stu-id="2fddc-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="2fddc-265">modelos</span><span class="sxs-lookup"><span data-stu-id="2fddc-265">templates</span></span>
<span data-ttu-id="2fddc-266">A pasta `templates` contém a configuração dos [modelos de email](api-management-howto-configure-notifications.md) na instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="2fddc-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="2fddc-267">`<template name>\configuration.json` - é a configuração do modelo de email.</span><span class="sxs-lookup"><span data-stu-id="2fddc-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="2fddc-268">`<template name>\body.html` - é o corpo do modelo de email.</span><span class="sxs-lookup"><span data-stu-id="2fddc-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fddc-269">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fddc-269">Next steps</span></span>
<span data-ttu-id="2fddc-270">Para saber mais sobre outras maneiras de gerenciar sua instância de serviço, confira:</span><span class="sxs-lookup"><span data-stu-id="2fddc-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="2fddc-271">Gerenciar a instância de seu serviço usando os seguintes cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fddc-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="2fddc-272">Referência de cmdlets do PowerShell para implantação de serviços</span><span class="sxs-lookup"><span data-stu-id="2fddc-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="2fddc-273">Referência de cmdlet do PowerShell para gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="2fddc-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="2fddc-274">Gerenciar a instância de seu serviço no portal do editor.</span><span class="sxs-lookup"><span data-stu-id="2fddc-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="2fddc-275">Gerenciar sua primeira API</span><span class="sxs-lookup"><span data-stu-id="2fddc-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="2fddc-276">Gerenciar a instância de seu serviço usando a API REST</span><span class="sxs-lookup"><span data-stu-id="2fddc-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="2fddc-277">Referência de API REST do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="2fddc-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="2fddc-278">Assista a uma visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="2fddc-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




