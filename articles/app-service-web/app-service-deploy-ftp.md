---
title: "aaaDeploy tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S | Microsoft Docs"
description: "Saiba como toodeploy tooAzure seu aplicativo do serviço de aplicativo usando FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="63cb4-103">Implantar seu tooAzure de aplicativo do serviço de aplicativo usando o FTP/S</span><span class="sxs-lookup"><span data-stu-id="63cb4-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="63cb4-104">Este artigo mostra como toouse FTP ou FTPS toodeploy seu aplicativo web, o back-end do aplicativo móvel ou o aplicativo de API muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="63cb4-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="63cb4-105">ponto de extremidade FTP/S de saudação para seu aplicativo já está ativo.</span><span class="sxs-lookup"><span data-stu-id="63cb4-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="63cb4-106">Nenhuma configuração é necessária tooenable implantação de FTP/S.</span><span class="sxs-lookup"><span data-stu-id="63cb4-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63cb4-107">Estamos continuamente realizando as etapas tooimprove segurança da plataforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="63cb4-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="63cb4-108">Como parte desse esforço contínuo, um upgrade dos Aplicativos Web está planejado para as regiões Central e Nordeste da Alemanha.</span><span class="sxs-lookup"><span data-stu-id="63cb4-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="63cb4-109">Durante esse aplicativos Web serão desativar uso de saudação do protocolo de texto sem formatação FTP para implantações.</span><span class="sxs-lookup"><span data-stu-id="63cb4-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="63cb4-110">Clientes de tooour nossa recomendação é tooFTPS tooswitch para implantações.</span><span class="sxs-lookup"><span data-stu-id="63cb4-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="63cb4-111">Não esperamos que qualquer serviço de tooyour de interrupção durante esta atualização que está planejada para 9/5.</span><span class="sxs-lookup"><span data-stu-id="63cb4-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="63cb4-112">Agradecemos sua compreensão.</span><span class="sxs-lookup"><span data-stu-id="63cb4-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="63cb4-113">Etapa 1: Definir credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="63cb4-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="63cb4-114">servidor de saudação FTP tooaccess para seu aplicativo, primeiro é necessário credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="63cb4-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="63cb4-115">tooset ou redefinir suas credenciais de implantação, consulte [credenciais de implantação de serviço de aplicativo do Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="63cb4-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="63cb4-116">Este tutorial demonstra o uso de saudação de credenciais de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="63cb4-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="63cb4-117">Etapa 2: Obter informações de conexão de FTP</span><span class="sxs-lookup"><span data-stu-id="63cb4-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="63cb4-118">Em Olá [portal do Azure](https://portal.azure.com), abra o aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="63cb4-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="63cb4-119">Selecione **visão geral** no menu da esquerda hello, observe os valores hello para **usuário de FTP/implantação**, **nome de Host do FTP**, e **FTPS nome de Host**.</span><span class="sxs-lookup"><span data-stu-id="63cb4-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informações de conexão de FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="63cb4-121">Olá **usuário de FTP/implantação** valor usuário conforme exibido pelo Portal do Azure incluindo o nome do aplicativo hello em contexto apropriado do tooprovide de ordem para o servidor FTP de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="63cb4-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="63cb4-122">Você pode encontrar hello as mesmas informações quando você seleciona **propriedades** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="63cb4-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="63cb4-123">Além disso, a senha de implantação Olá nunca é mostrada.</span><span class="sxs-lookup"><span data-stu-id="63cb4-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="63cb4-124">Se você esquecer sua senha de implantação, volte muito[etapa 1](#step1) e redefinir a senha de implantação.</span><span class="sxs-lookup"><span data-stu-id="63cb4-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="63cb4-125">Etapa 3: Implantar arquivos tooAzure</span><span class="sxs-lookup"><span data-stu-id="63cb4-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="63cb4-126">Seu cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use informações de conexão Olá coletadas tooconnect tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63cb4-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="63cb4-127">Copie os arquivos e sua toohello de estrutura de diretório do respectivos [ **/site/wwwroot** diretório](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou hello **/site/wwwroot/App_Data/trabalhos/** diretório para WebJobs).</span><span class="sxs-lookup"><span data-stu-id="63cb4-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="63cb4-128">Aplicativo de saudação do aplicativo do procurar tooyour URL tooverify está sendo executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="63cb4-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="63cb4-129">Ao contrário de [implantações com base no Git](app-service-deploy-local-git.md), implantação de FTP não dá suporte a saudação automações de implantação a seguir:</span><span class="sxs-lookup"><span data-stu-id="63cb4-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="63cb4-130">restauração de dependência (como automações NuGet, NPM, PIP e criador)</span><span class="sxs-lookup"><span data-stu-id="63cb4-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="63cb4-131">compilação de binários do .NET</span><span class="sxs-lookup"><span data-stu-id="63cb4-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="63cb4-132">geração de Web. config (eis uma [Node. js exemplo](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="63cb4-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="63cb4-133">Você deve restaurar, criar e gerar esses arquivos necessários manualmente no computador local e implantá-los junto com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63cb4-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="63cb4-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63cb4-134">Next steps</span></span>

<span data-ttu-id="63cb4-135">Para cenários de implantação mais avançados, tente [Implantando tooAzure com Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="63cb4-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="63cb4-136">Implantação baseada em Git tooAzure habilita o controle de versão, a restauração do pacote, MSBuild e muito mais.</span><span class="sxs-lookup"><span data-stu-id="63cb4-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="63cb4-137">Mais Recursos</span><span class="sxs-lookup"><span data-stu-id="63cb4-137">More Resources</span></span>

* <span data-ttu-id="63cb4-138">[Criar um aplicativo Web do PHP-MySQL e implantá-lo usando o FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="63cb4-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="63cb4-139">Credenciais de implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="63cb4-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
