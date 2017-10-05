---
title: "Implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP/S | Microsoft Docs"
description: "Saiba como implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP ou FTPS."
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="8d2e0-103">Implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP/S</span><span class="sxs-lookup"><span data-stu-id="8d2e0-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="8d2e0-104">Este artigo mostra como usar o FTP ou FTPS para implantar seu aplicativo web, back-end do aplicativo móvel ou aplicativo de API [o serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8d2e0-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="8d2e0-105">O ponto de extremidade FTP/S para seu aplicativo já está ativo.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="8d2e0-106">Nenhuma configuração é necessária para habilitar a implantação de FTP/S.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d2e0-107">Estamos sempre tomando medidas para melhorar a segurança da Plataforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="8d2e0-108">Como parte desse esforço contínuo, um upgrade dos Aplicativos Web está planejado para as regiões Central e Nordeste da Alemanha.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="8d2e0-109">Nesse período, o uso do protocolo FTP de texto sem formatação para implantação será desabilitado.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="8d2e0-110">Nossa recomendação para os clientes é alternar para FTPS nas implantações.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="8d2e0-111">Não esperamos qualquer interrupção no serviço durante esse upgrade, que está planejado para 5/9.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="8d2e0-112">Agradecemos sua compreensão.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="8d2e0-113">Etapa 1: Definir credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="8d2e0-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="8d2e0-114">Para acessar o servidor FTP para o seu aplicativo, você primeiro precisa de credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="8d2e0-115">Para definir ou redefinir suas credenciais de implantação, consulte [credenciais de implantação do serviço de aplicativo do Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="8d2e0-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="8d2e0-116">Este tutorial demonstra o uso de credenciais de nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="8d2e0-117">Etapa 2: Obter informações de conexão de FTP</span><span class="sxs-lookup"><span data-stu-id="8d2e0-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="8d2e0-118">No [portal do Azure](https://portal.azure.com), abra a [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="8d2e0-119">Selecione **visão geral** no menu à esquerda, em seguida, observe os valores de **usuário FTP/implantação**, **nome do Host FTP**, e **nome de Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informações de conexão de FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="8d2e0-121">O valor de usuário **FTP/Usuário de Implantação** como exibido pelo Portal do Azure, incluindo o nome do aplicativo a fim de fornecer contexto adequado ao servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="8d2e0-122">Você pode encontrar as mesmas informações quando você seleciona **propriedades** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="8d2e0-123">Além disso, a senha de implantação nunca é mostrada.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="8d2e0-124">Se você esquecer sua senha de implantação, vá até [etapa 1](#step1) e redefinir a senha de implantação.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="8d2e0-125">Etapa 3: Implantar arquivos para o Azure</span><span class="sxs-lookup"><span data-stu-id="8d2e0-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="8d2e0-126">De seu cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client) etc), use as informações de conexão coletadas para conectar-se ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="8d2e0-127">Copie seus arquivos e a respectiva estrutura de diretórios para o diretório [**/site/wwwroot** ](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou o diretório **/site/wwwroot/App_Data/Jobs/** para Trabalhos Web).</span><span class="sxs-lookup"><span data-stu-id="8d2e0-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="8d2e0-128">Navegue até a URL do aplicativo para verificar se ele está sendo executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8d2e0-129">Ao contrário de [implantações com base em Git](app-service-deploy-local-git.md), implantação de FTP não oferece suporte as automações de implantação a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d2e0-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="8d2e0-130">restauração de dependência (como automações NuGet, NPM, PIP e criador)</span><span class="sxs-lookup"><span data-stu-id="8d2e0-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="8d2e0-131">compilação de binários do .NET</span><span class="sxs-lookup"><span data-stu-id="8d2e0-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="8d2e0-132">geração de Web. config (eis uma [Node. js exemplo](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="8d2e0-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="8d2e0-133">Você deve restaurar, criar e gerar esses arquivos necessários manualmente no computador local e implantá-los junto com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8d2e0-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d2e0-134">Next steps</span></span>

<span data-ttu-id="8d2e0-135">Para cenários mais avançados de implantação, tente [implantação no Azure com Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="8d2e0-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="8d2e0-136">Implantação baseada em Git no Azure permite o controle de versão, restauração do pacote, MSBuild e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8d2e0-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="8d2e0-137">Mais Recursos</span><span class="sxs-lookup"><span data-stu-id="8d2e0-137">More Resources</span></span>

* <span data-ttu-id="8d2e0-138">[Criar um aplicativo Web do PHP-MySQL e implantá-lo usando o FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="8d2e0-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="8d2e0-139">Credenciais de implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8d2e0-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
