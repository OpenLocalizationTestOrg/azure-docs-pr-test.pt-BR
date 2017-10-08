---
title: aaaIntroduction tooAzure Web App no Linux | Microsoft Docs
description: Saiba mais sobre o Aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="dddd3-104">Introdução tooAzure Web App no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="dddd3-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dddd3-105">Overview</span></span>
<span data-ttu-id="dddd3-106">Os clientes podem usar o aplicativo Web em aplicativos de web do Linux toohost nativamente no Linux para as pilhas de aplicativos com suporte.</span><span class="sxs-lookup"><span data-stu-id="dddd3-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="dddd3-107">Olá, seção a seguir lista as pilhas de aplicativos de saudação que são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="dddd3-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="dddd3-108">Recursos</span><span class="sxs-lookup"><span data-stu-id="dddd3-108">Features</span></span>
<span data-ttu-id="dddd3-109">Web App no Linux atualmente suporta Olá pilhas de aplicativos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dddd3-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="dddd3-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="dddd3-110">Node.js</span></span>
    * <span data-ttu-id="dddd3-111">4.4</span><span class="sxs-lookup"><span data-stu-id="dddd3-111">4.4</span></span>
    * <span data-ttu-id="dddd3-112">4.5</span><span class="sxs-lookup"><span data-stu-id="dddd3-112">4.5</span></span>
    * <span data-ttu-id="dddd3-113">6.2</span><span class="sxs-lookup"><span data-stu-id="dddd3-113">6.2</span></span>
    * <span data-ttu-id="dddd3-114">6.6</span><span class="sxs-lookup"><span data-stu-id="dddd3-114">6.6</span></span>
    * <span data-ttu-id="dddd3-115">6.9</span><span class="sxs-lookup"><span data-stu-id="dddd3-115">6.9</span></span>
    * <span data-ttu-id="dddd3-116">6.10</span><span class="sxs-lookup"><span data-stu-id="dddd3-116">6.10</span></span>
    * <span data-ttu-id="dddd3-117">6.11</span><span class="sxs-lookup"><span data-stu-id="dddd3-117">6.11</span></span>
    * <span data-ttu-id="dddd3-118">8.0</span><span class="sxs-lookup"><span data-stu-id="dddd3-118">8.0</span></span>
    * <span data-ttu-id="dddd3-119">8.1</span><span class="sxs-lookup"><span data-stu-id="dddd3-119">8.1</span></span>
* <span data-ttu-id="dddd3-120">PHP</span><span class="sxs-lookup"><span data-stu-id="dddd3-120">PHP</span></span>
    * <span data-ttu-id="dddd3-121">5.6</span><span class="sxs-lookup"><span data-stu-id="dddd3-121">5.6</span></span>
    * <span data-ttu-id="dddd3-122">7.0</span><span class="sxs-lookup"><span data-stu-id="dddd3-122">7.0</span></span>
* <span data-ttu-id="dddd3-123">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dddd3-123">.Net Core</span></span>
    * <span data-ttu-id="dddd3-124">1.0</span><span class="sxs-lookup"><span data-stu-id="dddd3-124">1.0</span></span>
    * <span data-ttu-id="dddd3-125">1,1</span><span class="sxs-lookup"><span data-stu-id="dddd3-125">1.1</span></span>
* <span data-ttu-id="dddd3-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="dddd3-126">Ruby</span></span>
    * <span data-ttu-id="dddd3-127">2.3</span><span class="sxs-lookup"><span data-stu-id="dddd3-127">2.3</span></span>

<span data-ttu-id="dddd3-128">Os clientes podem implantar seus aplicativos usando:</span><span class="sxs-lookup"><span data-stu-id="dddd3-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="dddd3-129">FTP</span><span class="sxs-lookup"><span data-stu-id="dddd3-129">FTP</span></span>
* <span data-ttu-id="dddd3-130">Git local</span><span class="sxs-lookup"><span data-stu-id="dddd3-130">Local Git</span></span>
* <span data-ttu-id="dddd3-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="dddd3-131">GitHub</span></span>
* <span data-ttu-id="dddd3-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="dddd3-132">Bitbucket</span></span>

<span data-ttu-id="dddd3-133">Para o dimensionamento de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="dddd3-133">For application scaling:</span></span>

* <span data-ttu-id="dddd3-134">Os clientes podem dimensionar os aplicativos web para cima e para baixo, alterando o nível de saudação do seu plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="dddd3-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="dddd3-135">Os clientes podem dimensionar aplicativos e executar várias instâncias do aplicativo dentro dos limites de saudação do seu SKU</span><span class="sxs-lookup"><span data-stu-id="dddd3-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="dddd3-136">Para Kudu, algumas das funcionalidades básicas hello:</span><span class="sxs-lookup"><span data-stu-id="dddd3-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="dddd3-137">Ambientes</span><span class="sxs-lookup"><span data-stu-id="dddd3-137">Environments</span></span>
* <span data-ttu-id="dddd3-138">Implantações</span><span class="sxs-lookup"><span data-stu-id="dddd3-138">Deployments</span></span>
* <span data-ttu-id="dddd3-139">Console básico</span><span class="sxs-lookup"><span data-stu-id="dddd3-139">Basic console</span></span>
* <span data-ttu-id="dddd3-140">SSH</span><span class="sxs-lookup"><span data-stu-id="dddd3-140">SSH</span></span>

<span data-ttu-id="dddd3-141">Para DevOps:</span><span class="sxs-lookup"><span data-stu-id="dddd3-141">For devops:</span></span>

* <span data-ttu-id="dddd3-142">Ambientes de preparo</span><span class="sxs-lookup"><span data-stu-id="dddd3-142">Staging environments</span></span>
* <span data-ttu-id="dddd3-143">ACR e CI/CD do DockerHub</span><span class="sxs-lookup"><span data-stu-id="dddd3-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="dddd3-144">Limitações</span><span class="sxs-lookup"><span data-stu-id="dddd3-144">Limitations</span></span>
<span data-ttu-id="dddd3-145">Olá portal do Azure mostra apenas recursos que atualmente funcionam para o aplicativo Web no Linux e oculta Olá demais.</span><span class="sxs-lookup"><span data-stu-id="dddd3-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="dddd3-146">Como podemos habilitar mais recursos, ele ficará visível no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="dddd3-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="dddd3-147">Alguns recursos, como a integração de rede virtual, a autenticação do Azure Active Directory/de terceiros ou as extensões de site do Kudu, ainda não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="dddd3-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="dddd3-148">Depois que esses recursos estão disponíveis, atualizamos nossa documentação e o blog sobre alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="dddd3-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="dddd3-149">Essa visualização pública está disponível atualmente apenas em Olá regiões a seguir:</span><span class="sxs-lookup"><span data-stu-id="dddd3-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="dddd3-150">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="dddd3-150">West US</span></span>
* <span data-ttu-id="dddd3-151">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="dddd3-151">East US</span></span>
* <span data-ttu-id="dddd3-152">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="dddd3-152">West Europe</span></span>
* <span data-ttu-id="dddd3-153">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="dddd3-153">North Europe</span></span>
* <span data-ttu-id="dddd3-154">Centro-Sul dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="dddd3-154">South Central US</span></span>
* <span data-ttu-id="dddd3-155">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="dddd3-155">North Central US</span></span>
* <span data-ttu-id="dddd3-156">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="dddd3-156">Southeast Asia</span></span>
* <span data-ttu-id="dddd3-157">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="dddd3-157">East Asia</span></span>
* <span data-ttu-id="dddd3-158">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="dddd3-158">Australia East</span></span>
* <span data-ttu-id="dddd3-159">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="dddd3-159">Japan East</span></span>
* <span data-ttu-id="dddd3-160">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="dddd3-160">Brazil South</span></span>
* <span data-ttu-id="dddd3-161">Sul da Índia</span><span class="sxs-lookup"><span data-stu-id="dddd3-161">South India</span></span>

<span data-ttu-id="dddd3-162">No Linux, os aplicativos Web só é suportado em planos de serviço de aplicativo dedicado hello e não tem uma camada gratuito ou compartilhado.</span><span class="sxs-lookup"><span data-stu-id="dddd3-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="dddd3-163">Além disso, planos de Serviço de Aplicativo para aplicativos Web Linux e regulares são mutuamente exclusivos e, portanto, você não pode criar um aplicativo Linux em um plano do serviço de aplicativo não Linux.</span><span class="sxs-lookup"><span data-stu-id="dddd3-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="dddd3-164">No Linux, os aplicativos Web deve ser criado em um grupo de recursos que não contenha os aplicativos web não Linux em hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="dddd3-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dddd3-165">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dddd3-165">Troubleshooting</span></span> ##

<span data-ttu-id="dddd3-166">Quando o aplicativo falhar toostart ou se desejar toocheck log de saudação do seu aplicativo, verifique Olá que docker registra no diretório de arquivos de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="dddd3-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="dddd3-167">Acesse esse diretório por meio de seu site SCM ou via FTP.</span><span class="sxs-lookup"><span data-stu-id="dddd3-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="dddd3-168">Olá toolog `stdout` e `stderr` de seu contêiner, você precisa tooenable **log do contêiner do Docker** em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="dddd3-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitando o log][2]

![Usando logs de Docker tooview Kudu][1]

<span data-ttu-id="dddd3-171">Você pode acessar o site SCM saudação do **ferramentas avançadas de** em Olá **ferramentas de desenvolvimento** menu.</span><span class="sxs-lookup"><span data-stu-id="dddd3-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dddd3-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dddd3-172">Next steps</span></span>
<span data-ttu-id="dddd3-173">Consulte Olá tooget links de Introdução ao serviço de aplicativo no Linux a seguir.</span><span class="sxs-lookup"><span data-stu-id="dddd3-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="dddd3-174">Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="dddd3-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="dddd3-175">Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="dddd3-176">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="dddd3-177">Usando o .NET Core no Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="dddd3-178">Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="dddd3-179">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="dddd3-180">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="dddd3-181">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="dddd3-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="dddd3-182">Implantação contínua do Hub do Docker com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="dddd3-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png