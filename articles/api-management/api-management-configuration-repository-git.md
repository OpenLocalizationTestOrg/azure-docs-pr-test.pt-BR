---
title: "aaaConfigure seu serviço de gerenciamento de API usando o Git - Azure | Microsoft Docs"
description: "Saiba como toosave e configurar a configuração do serviço de gerenciamento de API usando o Git."
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
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="733b2-103">Como toosave e configurar a configuração do serviço de gerenciamento de API usando o Git</span><span class="sxs-lookup"><span data-stu-id="733b2-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="733b2-104">Cada instância de serviço de gerenciamento de API mantém um banco de dados de configuração que contém informações sobre a configuração de saudação e metadados para a instância do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="733b2-105">Alterações a instância do serviço toohello alterar uma configuração no portal do publicador hello, usando um cmdlet do PowerShell ou fazer uma chamada à API REST.</span><span class="sxs-lookup"><span data-stu-id="733b2-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="733b2-106">Além de métodos de toothese, você também pode gerenciar a configuração de instância do serviço usando o Git, permitindo cenários de gerenciamento de serviço, como:</span><span class="sxs-lookup"><span data-stu-id="733b2-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="733b2-107">Controle de versão da configuração - baixe e armazene versões diferentes da configuração do seu serviço</span><span class="sxs-lookup"><span data-stu-id="733b2-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="733b2-108">Em massa as alterações de configuração - faça alterações toomultiple partes da sua configuração de serviço no seu repositório local e integrar o servidor de back toohello de alterações de saudação com uma única operação</span><span class="sxs-lookup"><span data-stu-id="733b2-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="733b2-109">Cadeia de ferramentas do Git e fluxo de trabalho - familiar usar ferramentas de Git hello e fluxos de trabalho que você já estiver familiarizado com</span><span class="sxs-lookup"><span data-stu-id="733b2-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="733b2-110">Olá diagrama a seguir mostra uma visão geral de tooconfigure de maneiras diferentes de saudação sua instância de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="733b2-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Configuração do Git][api-management-git-configure]

<span data-ttu-id="733b2-112">Quando você fizer alterações tooyour serviço usando o portal do publicador hello, cmdlets do PowerShell ou Olá API REST, você está gerenciando o banco de dados de configuração de serviço usando Olá `https://{name}.management.azure-api.net` ponto de extremidade, conforme mostrado no lado direito de saudação do diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="733b2-113">lado esquerdo de saudação do diagrama Olá ilustra como você pode gerenciar a configuração de serviço usando o Git e repositório Git para seu serviço localizado em `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="733b2-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="733b2-114">Olá, as etapas a seguir fornece uma visão geral do gerenciamento de sua instância de serviço de gerenciamento de API usando o Git.</span><span class="sxs-lookup"><span data-stu-id="733b2-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="733b2-115">Acessar a configuração GIT em seu serviço</span><span class="sxs-lookup"><span data-stu-id="733b2-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="733b2-116">Salvar o repositório do Git de tooyour do banco de dados de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="733b2-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="733b2-117">Clonar a máquina local de tooyour Olá de repositório Git</span><span class="sxs-lookup"><span data-stu-id="733b2-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="733b2-118">Pull hello mais recente máquina local tooyour e o repositório de backup tooyour alterações confirmação e enviar por push</span><span class="sxs-lookup"><span data-stu-id="733b2-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="733b2-119">Implantar alterações de saudação do seu repositório em seu banco de dados de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="733b2-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="733b2-120">Este artigo descreve como tooenable usar Git toomanage sua configuração de serviço e fornece uma referência para os arquivos de saudação e pastas no repositório do Git hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="733b2-121">Acessar a configuração GIT em seu serviço</span><span class="sxs-lookup"><span data-stu-id="733b2-121">Access Git configuration in your service</span></span>
<span data-ttu-id="733b2-122">Você pode exibir rapidamente status de saudação da configuração do Git exibindo o ícone de Git Olá no canto superior direito de saudação do portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="733b2-123">Neste exemplo, a mensagem de saudação do status indica que há um repositório de toohello alterações não salvas.</span><span class="sxs-lookup"><span data-stu-id="733b2-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="733b2-124">Isso ocorre porque o banco de dados do gerenciamento de API serviço configuração Olá ainda não foi salvo toohello repositório.</span><span class="sxs-lookup"><span data-stu-id="733b2-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Status do Git][api-management-git-icon-enable]

<span data-ttu-id="733b2-126">tooview e configurar as definições de configuração de Git, você pode clique ícone de Git hello, ou Olá **segurança** menu e navegue toohello **repositório de configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="733b2-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Habilitar o GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="733b2-128">Nenhum segredo que não está definido como propriedades serão armazenadas no repositório de saudação e permanecerão no histórico de até que você desabilita e reabilitar o acesso de Git.</span><span class="sxs-lookup"><span data-stu-id="733b2-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="733b2-129">Propriedades fornecem um local seguro toomanage valores de constante de cadeia de caracteres, inclusive segredos, em todas as políticas e configurações de API para não ter toostore-los diretamente em suas instruções de política.</span><span class="sxs-lookup"><span data-stu-id="733b2-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="733b2-130">Para obter mais informações, consulte [como toouse propriedades nas políticas de gerenciamento do Azure API](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="733b2-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="733b2-131">Para obter informações sobre como habilitar ou desabilitar o acesso de Git usando Olá API REST, consulte [habilitar ou desabilitar o acesso de Git usando a API REST de saudação](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="733b2-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="733b2-132">repositório do Git toosave Olá serviço configuração toohello</span><span class="sxs-lookup"><span data-stu-id="733b2-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="733b2-133">a primeira etapa Olá antes da clonagem do repositório de saudação é estado atual do toosave saudação do repositório de toohello de configuração de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="733b2-134">Clique em **Salvar configuração toorepository**.</span><span class="sxs-lookup"><span data-stu-id="733b2-134">Click **Save configuration toorepository**.</span></span>

![Salvar configuração][api-management-save-configuration]

<span data-ttu-id="733b2-136">Faça as alterações desejadas na tela de confirmação de saudação e clique em **Okey** toosave.</span><span class="sxs-lookup"><span data-stu-id="733b2-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Salvar configuração][api-management-save-configuration-confirm]

<span data-ttu-id="733b2-138">Após alguns instantes configuração Olá é salvo e status de configuração de saudação do repositório de saudação é exibida, incluindo date de hello e a hora da última alteração de configuração hello e a última sincronização Olá entre a configuração do serviço hello e hello repositório.</span><span class="sxs-lookup"><span data-stu-id="733b2-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Status da configuração][api-management-configuration-status]

<span data-ttu-id="733b2-140">Depois de salvo toohello repositório configuração hello, ele pode ser clonado.</span><span class="sxs-lookup"><span data-stu-id="733b2-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="733b2-141">Para obter informações sobre como executar essa operação usando Olá API REST, consulte [configuração de confirmação de instantâneo usando a API REST de saudação](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="733b2-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="733b2-142">máquina local do tooyour tooclone Olá repositório</span><span class="sxs-lookup"><span data-stu-id="733b2-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="733b2-143">tooclone um repositório, que é necessário que o repositório de tooyour URL hello, um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="733b2-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="733b2-144">Olá nome de usuário e URL são exibidos superior de saudação do hello **repositório de configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="733b2-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Clone do Git][api-management-configuration-git-clone]

<span data-ttu-id="733b2-146">senha Olá é gerada na parte inferior de saudação do hello **repositório de configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="733b2-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Gerar senha][api-management-generate-password]

<span data-ttu-id="733b2-148">toogenerate uma senha, primeiro certifique-se que Olá **expiração** está definida toohello desejado de data e hora e, em seguida, clique em **gerar Token**.</span><span class="sxs-lookup"><span data-stu-id="733b2-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Senha][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="733b2-150">Anote essa senha.</span><span class="sxs-lookup"><span data-stu-id="733b2-150">Make a note of this password.</span></span> <span data-ttu-id="733b2-151">Depois que você deixar essa senha de saudação de página não será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="733b2-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="733b2-152">Olá seguindo exemplos de uso Olá Git Bash ferramenta de [Git para Windows](http://www.git-scm.com/downloads) , mas você pode usar qualquer ferramenta de Git que você esteja familiarizado com.</span><span class="sxs-lookup"><span data-stu-id="733b2-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="733b2-153">Abra sua ferramenta de Git na pasta desejada hello e execute Olá comando tooclone Olá git repositório tooyour máquina local a seguir, usando o comando Olá fornecido pelo portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="733b2-154">Fornece nome de usuário de saudação e a senha quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="733b2-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="733b2-155">Se você receber erros, tente modificar sua `git clone` comando tooinclude Olá nome e uma senha, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="733b2-156">Se isso fornece um erro, tente parte de senha de saudação do comando de saudação de codificação de URL.</span><span class="sxs-lookup"><span data-stu-id="733b2-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="733b2-157">Um toodo de maneira rápida isso é tooopen Visual Studio, e o comando a seguir de saudação problema em Olá **janela imediata**.</span><span class="sxs-lookup"><span data-stu-id="733b2-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="733b2-158">Olá tooopen **janela imediata**, abra qualquer solução ou projeto no Visual Studio (ou crie um novo aplicativo de console vazio) e escolha **Windows**, **imediato** de Olá **depurar** menu.</span><span class="sxs-lookup"><span data-stu-id="733b2-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="733b2-159">Use senha Olá codificado junto com seu nome e o repositório local tooconstruct Olá git comando de usuário.</span><span class="sxs-lookup"><span data-stu-id="733b2-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="733b2-160">Depois que o repositório de saudação é clonado, você pode exibir e trabalhar com ele no sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="733b2-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="733b2-161">Para obter mais informações, veja [Referência da estrutura de pastas e arquivos do repositório Git local](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="733b2-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="733b2-162">tooupdate seu repositório local com a configuração mais atual da instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="733b2-163">Se você fizer a instância de serviço de gerenciamento de API de tooyour alterações no portal do publicador hello ou Olá API REST, você deve salvar o repositório de toohello essas alterações antes de atualizar o seu repositório local com as alterações mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="733b2-164">toodo, clique **Salvar configuração toorepository** em Olá **repositório de configuração** guia no portal do publicador hello e, em seguida, emitir Olá comando no seu repositório local a seguir.</span><span class="sxs-lookup"><span data-stu-id="733b2-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="733b2-165">Antes de executar `git pull` Certifique-se de que você está na pasta Olá para seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="733b2-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="733b2-166">Se você concluiu a saudação `git clone` de comando, em seguida, você deve alterar o repositório de tooyour directory Olá executando um comando como Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="733b2-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="733b2-167">alterações de toopush do seu repositório de servidor toohello repositório local</span><span class="sxs-lookup"><span data-stu-id="733b2-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="733b2-168">toopush alterações do seu repositório de servidor toohello repositório local, você deve confirmar suas alterações e, em seguida, enviá-las toohello repositório de servidor.</span><span class="sxs-lookup"><span data-stu-id="733b2-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="733b2-169">toocommit suas alterações, abra a ferramenta de comando Git, comutador toohello diretório de repositório local e Olá problema comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="733b2-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="733b2-170">toopush todos Olá confirma que o servidor toohello, execute Olá seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="733b2-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="733b2-171">toodeploy qualquer instância de serviço do serviço configuração alterações toohello gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="733b2-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="733b2-172">Depois que as alterações locais são confirmadas e enviadas por push toohello repositório de servidor, você pode implantá-las tooyour instância de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="733b2-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Implantar][api-management-configuration-deploy]

<span data-ttu-id="733b2-174">Para obter informações sobre como executar essa operação usando Olá API REST, consulte [Git implantar alterações tooconfiguration banco de dados usando a API REST de saudação](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="733b2-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="733b2-175">Referência da estrutura de pastas e arquivos do repositório Git local</span><span class="sxs-lookup"><span data-stu-id="733b2-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="733b2-176">Olá arquivos e pastas no repositório do git local Olá contêm Olá informações de configuração sobre a instância de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="733b2-177">Item</span><span class="sxs-lookup"><span data-stu-id="733b2-177">Item</span></span> | <span data-ttu-id="733b2-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="733b2-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="733b2-179">pasta api-management raiz</span><span class="sxs-lookup"><span data-stu-id="733b2-179">root api-management folder</span></span> |<span data-ttu-id="733b2-180">Contém a configuração de nível superior para a instância do serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="733b2-181">pasta apis</span><span class="sxs-lookup"><span data-stu-id="733b2-181">apis folder</span></span> |<span data-ttu-id="733b2-182">Contém a configuração de Olá Olá APIs na instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="733b2-183">pasta groups</span><span class="sxs-lookup"><span data-stu-id="733b2-183">groups folder</span></span> |<span data-ttu-id="733b2-184">Contém a configuração de saudação de grupos de saudação na instância do serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="733b2-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="733b2-185">pasta policies</span><span class="sxs-lookup"><span data-stu-id="733b2-185">policies folder</span></span> |<span data-ttu-id="733b2-186">Contém políticas de saudação na instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="733b2-187">pasta portalStyles</span><span class="sxs-lookup"><span data-stu-id="733b2-187">portalStyles folder</span></span> |<span data-ttu-id="733b2-188">Contém a configuração de saudação de personalizações portal do desenvolvedor Olá na instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="733b2-189">pasta products</span><span class="sxs-lookup"><span data-stu-id="733b2-189">products folder</span></span> |<span data-ttu-id="733b2-190">Contém a configuração de saudação de produtos Olá na instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="733b2-191">pasta templates</span><span class="sxs-lookup"><span data-stu-id="733b2-191">templates folder</span></span> |<span data-ttu-id="733b2-192">Contém a configuração de saudação para modelos de email de saudação na instância de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="733b2-193">Cada pasta pode conter um ou mais arquivos e, em alguns casos, uma ou mais pastas, por exemplo, uma pasta para cada API, produto ou grupo.</span><span class="sxs-lookup"><span data-stu-id="733b2-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="733b2-194">arquivos Hello dentro de cada pasta são específicos para o tipo de entidade Olá descrito pelo nome da pasta hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="733b2-195">Tipo de arquivo</span><span class="sxs-lookup"><span data-stu-id="733b2-195">File type</span></span> | <span data-ttu-id="733b2-196">Finalidade</span><span class="sxs-lookup"><span data-stu-id="733b2-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="733b2-197">json</span><span class="sxs-lookup"><span data-stu-id="733b2-197">json</span></span> |<span data-ttu-id="733b2-198">Informações de configuração sobre a entidade respectivos Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="733b2-199">html</span><span class="sxs-lookup"><span data-stu-id="733b2-199">html</span></span> |<span data-ttu-id="733b2-200">Descrições sobre entidade hello, geralmente é exibido no portal do desenvolvedor Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="733b2-201">xml</span><span class="sxs-lookup"><span data-stu-id="733b2-201">xml</span></span> |<span data-ttu-id="733b2-202">Declarações de políticas</span><span class="sxs-lookup"><span data-stu-id="733b2-202">Policy statements</span></span> |
| <span data-ttu-id="733b2-203">css</span><span class="sxs-lookup"><span data-stu-id="733b2-203">css</span></span> |<span data-ttu-id="733b2-204">Folhas de estilo para personalização do portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="733b2-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="733b2-205">Esses arquivos podem ser criados, excluídos, editados e gerenciados no sistema de arquivos local, e alterações de saudação implantadas toohello back sua instância de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="733b2-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="733b2-206">Olá entidades a seguir não estão contidas no repositório do Git hello e não podem ser configuradas usando o Git.</span><span class="sxs-lookup"><span data-stu-id="733b2-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="733b2-207">Usuários</span><span class="sxs-lookup"><span data-stu-id="733b2-207">Users</span></span>
> * <span data-ttu-id="733b2-208">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="733b2-208">Subscriptions</span></span>
> * <span data-ttu-id="733b2-209">Propriedades</span><span class="sxs-lookup"><span data-stu-id="733b2-209">Properties</span></span>
> * <span data-ttu-id="733b2-210">Outras entidades do portal do desenvolvedor além dos estilos</span><span class="sxs-lookup"><span data-stu-id="733b2-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="733b2-211">Pasta api-management raiz</span><span class="sxs-lookup"><span data-stu-id="733b2-211">Root api-management folder</span></span>
<span data-ttu-id="733b2-212">raiz de saudação `api-management` pasta contém um `configuration.json` arquivo que contém informações de nível superior sobre a instância de serviço de saudação no hello formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="733b2-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

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

<span data-ttu-id="733b2-213">Olá primeiro quatro configurações (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, e `UserRegistrationTermsConsentRequired`) mapear toohello configurações a seguir no hello **identidades** guia Olá **segurança** seção.</span><span class="sxs-lookup"><span data-stu-id="733b2-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="733b2-214">Configuração de identidade</span><span class="sxs-lookup"><span data-stu-id="733b2-214">Identity setting</span></span> | <span data-ttu-id="733b2-215">Mapeia muito</span><span class="sxs-lookup"><span data-stu-id="733b2-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="733b2-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="733b2-216">RegistrationEnabled</span></span> |<span data-ttu-id="733b2-217">**Redirecionar usuários anônimos toosign na página** caixa de seleção</span><span class="sxs-lookup"><span data-stu-id="733b2-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="733b2-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="733b2-218">UserRegistrationTerms</span></span> |<span data-ttu-id="733b2-219">**Termos de uso na inscrição do usuário** </span><span class="sxs-lookup"><span data-stu-id="733b2-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="733b2-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="733b2-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="733b2-221">**Mostrar os termos de uso na página de entrada** </span><span class="sxs-lookup"><span data-stu-id="733b2-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="733b2-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="733b2-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="733b2-223">**Exigir consentimento** </span><span class="sxs-lookup"><span data-stu-id="733b2-223">**Require consent** checkbox</span></span> |

![Configurações de identidade][api-management-identity-settings]

<span data-ttu-id="733b2-225">Olá quatro configurações (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, e `DelegationValidationKey`) mapear toohello configurações a seguir no hello **delegação** guia Olá **segurança** seção.</span><span class="sxs-lookup"><span data-stu-id="733b2-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="733b2-226">Configuração de delegação</span><span class="sxs-lookup"><span data-stu-id="733b2-226">Delegation setting</span></span> | <span data-ttu-id="733b2-227">Mapeia muito</span><span class="sxs-lookup"><span data-stu-id="733b2-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="733b2-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="733b2-228">DelegationEnabled</span></span> |<span data-ttu-id="733b2-229">Caixa de seleção **Delegar entrada e inscrição**</span><span class="sxs-lookup"><span data-stu-id="733b2-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="733b2-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="733b2-230">DelegationUrl</span></span> |<span data-ttu-id="733b2-231">**URL do ponto de extremidade da delegação** </span><span class="sxs-lookup"><span data-stu-id="733b2-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="733b2-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="733b2-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="733b2-233">**Delegar assinatura do produto** </span><span class="sxs-lookup"><span data-stu-id="733b2-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="733b2-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="733b2-234">DelegationValidationKey</span></span> |<span data-ttu-id="733b2-235">**Delegar Chave de Validação** </span><span class="sxs-lookup"><span data-stu-id="733b2-235">**Delegate Validation Key** textbox</span></span> |

![Configurações de delegação][api-management-delegation-settings]

<span data-ttu-id="733b2-237">Olá configuração final, `$ref-policy`, mapeia toohello política global instruções arquivo hello instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="733b2-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="733b2-238">pasta apis</span><span class="sxs-lookup"><span data-stu-id="733b2-238">apis folder</span></span>
<span data-ttu-id="733b2-239">Olá `apis` pasta contém uma pasta para cada API na instância de serviço Olá que contém Olá itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="733b2-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="733b2-240">`apis\<api name>\configuration.json`-Esta é a configuração Olá Olá API e contém informações sobre a URL de serviço de back-end hello e operações de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="733b2-241">Isso é hello mesmas informações que seriam retornadas se você toocall [obter uma API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) com `export=true` na `application/json` formato.</span><span class="sxs-lookup"><span data-stu-id="733b2-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="733b2-242">`apis\<api name>\api.description.html`-Esta é a descrição de saudação do hello API e corresponde toohello `description` propriedade Olá [entidade API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="733b2-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="733b2-243">`apis\<api name>\operations\`-Esta pasta contém `<operation name>.description.html` arquivos que operações de mapa toohello no hello API.</span><span class="sxs-lookup"><span data-stu-id="733b2-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="733b2-244">Cada arquivo contém a descrição de saudação de uma única operação no hello API que mapeia toohello `description` propriedade Olá [entidade de operação](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) em Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="733b2-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="733b2-245">pasta groups</span><span class="sxs-lookup"><span data-stu-id="733b2-245">groups folder</span></span>
<span data-ttu-id="733b2-246">Olá `groups` pasta contém uma pasta para cada grupo definido na instância de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="733b2-247">`groups\<group name>\configuration.json`-Esta é a configuração Olá para o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="733b2-248">Isso é hello mesmas informações que seriam retornadas se você Olá toocall [obter um grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operação.</span><span class="sxs-lookup"><span data-stu-id="733b2-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="733b2-249">`groups\<group name>\description.html`-Esta é a descrição de saudação do grupo de saudação e corresponde toohello `description` propriedade Olá [grupo entidade](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="733b2-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="733b2-250">pasta policies</span><span class="sxs-lookup"><span data-stu-id="733b2-250">policies folder</span></span>
<span data-ttu-id="733b2-251">Olá `policies` pasta contém declarações de política de saudação para sua instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="733b2-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="733b2-252">`policies\global.xml` - contém políticas definidas no escopo global da instância de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="733b2-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="733b2-253">`policies\apis\<api name>\` - se houver alguma política definida no escopo da API, ela estará nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="733b2-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="733b2-254">`policies\apis\<api name>\<operation name>\`pasta - se você tiver qualquer políticas definidas no escopo da operação, elas são contidas nessa pasta na `<operation name>.xml` arquivos mapeados toohello declarações de política para cada operação.</span><span class="sxs-lookup"><span data-stu-id="733b2-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="733b2-255">`policies\products\`-Se você tiver qualquer políticas definidas no escopo do produto, elas são contidas nessa pasta, que contém `<product name>.xml` arquivos mapeados toohello declarações de política para cada produto.</span><span class="sxs-lookup"><span data-stu-id="733b2-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="733b2-256">pasta portalStyles</span><span class="sxs-lookup"><span data-stu-id="733b2-256">portalStyles folder</span></span>
<span data-ttu-id="733b2-257">Olá `portalStyles` pasta contém a configuração e folhas de estilo para personalizações portal do desenvolvedor Olá instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="733b2-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="733b2-258">`portalStyles\configuration.json`-contém os nomes de Olá Olá de folhas de estilo usadas pelo portal do desenvolvedor Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="733b2-259">`portalStyles\<style name>.css`-cada `<style name>.css` arquivo contém estilos para o portal do desenvolvedor hello (`Preview.css` e `Production.css` por padrão).</span><span class="sxs-lookup"><span data-stu-id="733b2-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="733b2-260">pasta products</span><span class="sxs-lookup"><span data-stu-id="733b2-260">products folder</span></span>
<span data-ttu-id="733b2-261">Olá `products` pasta contém uma pasta para cada produto definido na instância de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="733b2-262">`products\<product name>\configuration.json`-Esta é a configuração Olá para o produto de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="733b2-263">Isso é hello mesmas informações que seriam retornadas se você Olá toocall [obter um produto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operação.</span><span class="sxs-lookup"><span data-stu-id="733b2-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="733b2-264">`products\<product name>\product.description.html`-Esta é a descrição de saudação do produto de saudação e corresponde toohello `description` propriedade Olá [entidade product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) em Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="733b2-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="733b2-265">modelos</span><span class="sxs-lookup"><span data-stu-id="733b2-265">templates</span></span>
<span data-ttu-id="733b2-266">Olá `templates` pasta contém a configuração de saudação [modelos de email](api-management-howto-configure-notifications.md) da instância de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="733b2-267">`<template name>\configuration.json`-Esta é a configuração Olá para o modelo de email hello.</span><span class="sxs-lookup"><span data-stu-id="733b2-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="733b2-268">`<template name>\body.html`-Este é o corpo de saudação do modelo de email de saudação.</span><span class="sxs-lookup"><span data-stu-id="733b2-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="733b2-269">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="733b2-269">Next steps</span></span>
<span data-ttu-id="733b2-270">Para obter informações sobre outra maneiras toomanage sua instância de serviço, consulte:</span><span class="sxs-lookup"><span data-stu-id="733b2-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="733b2-271">Gerenciar a instância de serviço usando Olá seguintes cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="733b2-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="733b2-272">Referência de cmdlets do PowerShell para implantação de serviços</span><span class="sxs-lookup"><span data-stu-id="733b2-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="733b2-273">Referência de cmdlet do PowerShell para gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="733b2-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="733b2-274">Gerenciar a instância de serviço no portal do publicador Olá</span><span class="sxs-lookup"><span data-stu-id="733b2-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="733b2-275">Gerenciar sua primeira API</span><span class="sxs-lookup"><span data-stu-id="733b2-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="733b2-276">Gerenciar a instância de serviço usando a API REST de saudação</span><span class="sxs-lookup"><span data-stu-id="733b2-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="733b2-277">Referência de API REST do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="733b2-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="733b2-278">Assista a uma visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="733b2-278">Watch a video overview</span></span>
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




