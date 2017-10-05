---
title: "Introdução ao Aplicativo Web do Azure no Linux | Microsoft Docs"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="639e5-104">Introdução ao Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="639e5-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="639e5-105">Overview</span></span>
<span data-ttu-id="639e5-106">Os clientes podem usar o Aplicativo Web no Linux para hospedar aplicativos Web nativos no Linux para as pilhas de aplicativos com suporte.</span><span class="sxs-lookup"><span data-stu-id="639e5-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="639e5-107">A seção a seguir lista as pilhas de aplicativos que têm suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="639e5-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="639e5-108">Recursos</span><span class="sxs-lookup"><span data-stu-id="639e5-108">Features</span></span>
<span data-ttu-id="639e5-109">Atualmente, o Aplicativo Web no Linux dá suporte a estas pilhas de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="639e5-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="639e5-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="639e5-110">Node.js</span></span>
    * <span data-ttu-id="639e5-111">4.4</span><span class="sxs-lookup"><span data-stu-id="639e5-111">4.4</span></span>
    * <span data-ttu-id="639e5-112">4.5</span><span class="sxs-lookup"><span data-stu-id="639e5-112">4.5</span></span>
    * <span data-ttu-id="639e5-113">6.2</span><span class="sxs-lookup"><span data-stu-id="639e5-113">6.2</span></span>
    * <span data-ttu-id="639e5-114">6.6</span><span class="sxs-lookup"><span data-stu-id="639e5-114">6.6</span></span>
    * <span data-ttu-id="639e5-115">6.9</span><span class="sxs-lookup"><span data-stu-id="639e5-115">6.9</span></span>
    * <span data-ttu-id="639e5-116">6.10</span><span class="sxs-lookup"><span data-stu-id="639e5-116">6.10</span></span>
    * <span data-ttu-id="639e5-117">6.11</span><span class="sxs-lookup"><span data-stu-id="639e5-117">6.11</span></span>
    * <span data-ttu-id="639e5-118">8.0</span><span class="sxs-lookup"><span data-stu-id="639e5-118">8.0</span></span>
    * <span data-ttu-id="639e5-119">8.1</span><span class="sxs-lookup"><span data-stu-id="639e5-119">8.1</span></span>
* <span data-ttu-id="639e5-120">PHP</span><span class="sxs-lookup"><span data-stu-id="639e5-120">PHP</span></span>
    * <span data-ttu-id="639e5-121">5.6</span><span class="sxs-lookup"><span data-stu-id="639e5-121">5.6</span></span>
    * <span data-ttu-id="639e5-122">7.0</span><span class="sxs-lookup"><span data-stu-id="639e5-122">7.0</span></span>
* <span data-ttu-id="639e5-123">.NET Core</span><span class="sxs-lookup"><span data-stu-id="639e5-123">.Net Core</span></span>
    * <span data-ttu-id="639e5-124">1.0</span><span class="sxs-lookup"><span data-stu-id="639e5-124">1.0</span></span>
    * <span data-ttu-id="639e5-125">1,1</span><span class="sxs-lookup"><span data-stu-id="639e5-125">1.1</span></span>
* <span data-ttu-id="639e5-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="639e5-126">Ruby</span></span>
    * <span data-ttu-id="639e5-127">2.3</span><span class="sxs-lookup"><span data-stu-id="639e5-127">2.3</span></span>

<span data-ttu-id="639e5-128">Os clientes podem implantar seus aplicativos usando:</span><span class="sxs-lookup"><span data-stu-id="639e5-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="639e5-129">FTP</span><span class="sxs-lookup"><span data-stu-id="639e5-129">FTP</span></span>
* <span data-ttu-id="639e5-130">Git local</span><span class="sxs-lookup"><span data-stu-id="639e5-130">Local Git</span></span>
* <span data-ttu-id="639e5-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="639e5-131">GitHub</span></span>
* <span data-ttu-id="639e5-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="639e5-132">Bitbucket</span></span>

<span data-ttu-id="639e5-133">Para o dimensionamento de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="639e5-133">For application scaling:</span></span>

* <span data-ttu-id="639e5-134">Os clientes podem escalar ou reduzir verticalmente aplicativos Web, alterando a camada dos respectivos planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="639e5-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="639e5-135">Os clientes podem escalar horizontalmente seus aplicativos e executar várias instâncias do aplicativo dentro dos limites de seu SKU</span><span class="sxs-lookup"><span data-stu-id="639e5-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="639e5-136">Para o Kudu, algumas das funcionalidades básicas:</span><span class="sxs-lookup"><span data-stu-id="639e5-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="639e5-137">Ambientes</span><span class="sxs-lookup"><span data-stu-id="639e5-137">Environments</span></span>
* <span data-ttu-id="639e5-138">Implantações</span><span class="sxs-lookup"><span data-stu-id="639e5-138">Deployments</span></span>
* <span data-ttu-id="639e5-139">Console básico</span><span class="sxs-lookup"><span data-stu-id="639e5-139">Basic console</span></span>
* <span data-ttu-id="639e5-140">SSH</span><span class="sxs-lookup"><span data-stu-id="639e5-140">SSH</span></span>

<span data-ttu-id="639e5-141">Para DevOps:</span><span class="sxs-lookup"><span data-stu-id="639e5-141">For devops:</span></span>

* <span data-ttu-id="639e5-142">Ambientes de preparo</span><span class="sxs-lookup"><span data-stu-id="639e5-142">Staging environments</span></span>
* <span data-ttu-id="639e5-143">ACR e CI/CD do DockerHub</span><span class="sxs-lookup"><span data-stu-id="639e5-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="639e5-144">Limitações</span><span class="sxs-lookup"><span data-stu-id="639e5-144">Limitations</span></span>
<span data-ttu-id="639e5-145">O portal do Azure mostra somente os recursos que funcionam atualmente para o Aplicativo Web no Linux e oculta os demais.</span><span class="sxs-lookup"><span data-stu-id="639e5-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="639e5-146">Conforme habilitarmos mais recursos, eles ficarão visíveis no portal.</span><span class="sxs-lookup"><span data-stu-id="639e5-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="639e5-147">Alguns recursos, como a integração de rede virtual, a autenticação do Azure Active Directory/de terceiros ou as extensões de site do Kudu, ainda não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="639e5-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="639e5-148">Quando esses recursos estiverem disponíveis, atualizaremos nossa documentação e nosso blog sobre as alterações.</span><span class="sxs-lookup"><span data-stu-id="639e5-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="639e5-149">Esta visualização pública está disponível atualmente nas seguintes regiões:</span><span class="sxs-lookup"><span data-stu-id="639e5-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="639e5-150">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="639e5-150">West US</span></span>
* <span data-ttu-id="639e5-151">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="639e5-151">East US</span></span>
* <span data-ttu-id="639e5-152">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="639e5-152">West Europe</span></span>
* <span data-ttu-id="639e5-153">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="639e5-153">North Europe</span></span>
* <span data-ttu-id="639e5-154">Centro-Sul dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="639e5-154">South Central US</span></span>
* <span data-ttu-id="639e5-155">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="639e5-155">North Central US</span></span>
* <span data-ttu-id="639e5-156">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="639e5-156">Southeast Asia</span></span>
* <span data-ttu-id="639e5-157">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="639e5-157">East Asia</span></span>
* <span data-ttu-id="639e5-158">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="639e5-158">Australia East</span></span>
* <span data-ttu-id="639e5-159">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="639e5-159">Japan East</span></span>
* <span data-ttu-id="639e5-160">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="639e5-160">Brazil South</span></span>
* <span data-ttu-id="639e5-161">Sul da Índia</span><span class="sxs-lookup"><span data-stu-id="639e5-161">South India</span></span>

<span data-ttu-id="639e5-162">No Linux, os aplicativos Web só têm suporte nos planos de serviço de aplicativo Dedicados e não têm uma camada Gratuita ou Compartilhada.</span><span class="sxs-lookup"><span data-stu-id="639e5-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="639e5-163">Além disso, planos de Serviço de Aplicativo para aplicativos Web Linux e regulares são mutuamente exclusivos e, portanto, você não pode criar um aplicativo Linux em um plano do serviço de aplicativo não Linux.</span><span class="sxs-lookup"><span data-stu-id="639e5-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="639e5-164">Os Aplicativos Web no Linux devem ser criados em um grupo de recursos que não contenha aplicativos Web não Linux na mesma região.</span><span class="sxs-lookup"><span data-stu-id="639e5-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="639e5-165">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="639e5-165">Troubleshooting</span></span> ##

<span data-ttu-id="639e5-166">Quando seu aplicativo falhar ao iniciar ou você quiser verificar o log do aplicativo, verifique os logs do Docker no diretório LogFiles.</span><span class="sxs-lookup"><span data-stu-id="639e5-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="639e5-167">Acesse esse diretório por meio de seu site SCM ou via FTP.</span><span class="sxs-lookup"><span data-stu-id="639e5-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="639e5-168">Para registrar `stdout` e `stderr` por meio do contêiner, você precisa habilitar o **Registro em log do Contêiner do Docker** em **Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="639e5-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitando o log][2]

![Como usar o Kudu para exibir os logs do Docker][1]

<span data-ttu-id="639e5-171">Acesse o site SCM nas **Ferramentas Avançadas** no menu **Ferramentas de Desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="639e5-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="639e5-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="639e5-172">Next steps</span></span>
<span data-ttu-id="639e5-173">Veja os links a seguir para começar a usar o Serviço de Aplicativo no Linux.</span><span class="sxs-lookup"><span data-stu-id="639e5-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="639e5-174">Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="639e5-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="639e5-175">Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="639e5-176">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="639e5-177">Usando o .NET Core no Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="639e5-178">Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="639e5-179">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="639e5-180">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="639e5-181">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="639e5-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="639e5-182">Implantação contínua do Hub do Docker com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="639e5-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png