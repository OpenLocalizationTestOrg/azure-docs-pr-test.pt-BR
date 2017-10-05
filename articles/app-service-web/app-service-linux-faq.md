---
title: "Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux | Microsoft Docs"
description: "Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo web, perguntas frequentes, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="4e258-104">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4e258-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="4e258-105">Com a liberação do Aplicativo Web no Linux, estamos trabalhando para adicionar recursos e fazer melhorias em nossa plataforma.</span><span class="sxs-lookup"><span data-stu-id="4e258-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="4e258-106">Estas são algumas perguntas frequentes que nossos clientes têm feito nos últimos meses.</span><span class="sxs-lookup"><span data-stu-id="4e258-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="4e258-107">Caso tenha uma pergunta, comente o artigo e responderemos assim que possível.</span><span class="sxs-lookup"><span data-stu-id="4e258-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="4e258-108">Imagens internas</span><span class="sxs-lookup"><span data-stu-id="4e258-108">Built-in images</span></span>

<span data-ttu-id="4e258-109">**P:** desejo divida os contêineres de Docker internos que a plataforma oferece.</span><span class="sxs-lookup"><span data-stu-id="4e258-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="4e258-110">Onde posso encontrar esses arquivos?</span><span class="sxs-lookup"><span data-stu-id="4e258-110">Where can I find those files?</span></span>

<span data-ttu-id="4e258-111">**R:** É possível encontrar todos os arquivos do Docker no [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="4e258-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="4e258-112">É possível encontrar todos os contêineres do Docker no [Hub do Docker](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="4e258-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="4e258-113">**P:** Quais são os valores esperados para a seção Arquivo de Inicialização quando configuro a pilha de tempo de execução?</span><span class="sxs-lookup"><span data-stu-id="4e258-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="4e258-114">**R:** Para o Node.js, é possível especificar o arquivo de configuração PM2 ou o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="4e258-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="4e258-115">Para o .NET Core, especifique o nome da DLL compilada.</span><span class="sxs-lookup"><span data-stu-id="4e258-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="4e258-116">Para o Ruby, é possível especificar o script Ruby com o qual você deseja inicializar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e258-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="4e258-117">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4e258-117">Management</span></span>

<span data-ttu-id="4e258-118">**P:** O que acontece quando eu pressiono o botão de reinicialização no Portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="4e258-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="4e258-119">**R:** Isso equivale à reinicialização do Docker.</span><span class="sxs-lookup"><span data-stu-id="4e258-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="4e258-120">**P:** Posso usar o SSH (Secure Shell) para me conectar à VM (máquina virtual) do contêiner de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="4e258-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="4e258-121">**R:** Sim, você pode fazer isso por meio do site do SCM; verifique o artigo a seguir para obter mais informações [Suporte de SSH para o Aplicativo Web no Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="4e258-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="4e258-122">**P:** Quero criar um plano do Serviço de Aplicativo do Linux por meio do SDK ou de um modelo do ARM, como posso fazer isso?</span><span class="sxs-lookup"><span data-stu-id="4e258-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="4e258-123">**R:** Você precisa definir o campo `reserved` do serviço de aplicativo como `true`.</span><span class="sxs-lookup"><span data-stu-id="4e258-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="4e258-124">Integração/implantação contínua</span><span class="sxs-lookup"><span data-stu-id="4e258-124">Continuous integration/deployment</span></span>

<span data-ttu-id="4e258-125">**P:** Meu aplicativo Web ainda usa uma imagem de contêiner antiga do Docker depois que atualizei a imagem no Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="4e258-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="4e258-126">Há suporte para implantação/integração contínua de contêineres personalizados?</span><span class="sxs-lookup"><span data-stu-id="4e258-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="4e258-127">**R:** Para configurar a integração/implantação contínua para o Registro de Contêiner do Azure ou imagens do DockerHub, verifique o artigo [Implantação contínua com o Aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="4e258-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="4e258-128">Para registros privados, é possível atualizar o contêiner parando e, em seguida, iniciando o Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4e258-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="4e258-129">Se preferir, é possível alterar ou adicionar uma configuração de aplicativo fictício para forçar uma atualização do contêiner.</span><span class="sxs-lookup"><span data-stu-id="4e258-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="4e258-130">**P:** Há suporte para ambientes de preparo?</span><span class="sxs-lookup"><span data-stu-id="4e258-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="4e258-131">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="4e258-131">**A:** Yes.</span></span>

<span data-ttu-id="4e258-132">**P:** Posso usar **implantação da web** implantar meu aplicativo web?</span><span class="sxs-lookup"><span data-stu-id="4e258-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="4e258-133">**R:** Sim, você precisa definir um aplicativo de configuração chamado `WEBSITE_WEBDEPLOY_USE_SCM` para `false`.</span><span class="sxs-lookup"><span data-stu-id="4e258-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="4e258-134">Suporte ao idioma</span><span class="sxs-lookup"><span data-stu-id="4e258-134">Language support</span></span>

<span data-ttu-id="4e258-135">**P:** Há suporte para aplicativos .NET Core não compilados?</span><span class="sxs-lookup"><span data-stu-id="4e258-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="4e258-136">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="4e258-136">**A:** Yes.</span></span>

<span data-ttu-id="4e258-137">**P:** Há suporte para o Criador como um gerenciador de dependências para aplicativos PHP?</span><span class="sxs-lookup"><span data-stu-id="4e258-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="4e258-138">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="4e258-138">**A:** Yes.</span></span> <span data-ttu-id="4e258-139">Durante a implantação de Git, Kudu deve detectar que você está implantando um aplicativo PHP (graças à presença de um arquivo de composer.json) e disparará uma instalação de criador para você.</span><span class="sxs-lookup"><span data-stu-id="4e258-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="4e258-140">Contêineres personalizados</span><span class="sxs-lookup"><span data-stu-id="4e258-140">Custom containers</span></span>

<span data-ttu-id="4e258-141">**P:** Estou usando meu próprio contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="4e258-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="4e258-142">Meu aplicativo reside no diretório `\home\`, mas não consigo encontrar meus arquivos ao navegar pelo conteúdo usando o [site do SCM](https://github.com/projectkudu/kudu) ou um cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="4e258-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="4e258-143">Onde estão meus arquivos?</span><span class="sxs-lookup"><span data-stu-id="4e258-143">Where are my files?</span></span>

<span data-ttu-id="4e258-144">**R:** Montamos um compartilhamento SMB no diretório `\home\`.</span><span class="sxs-lookup"><span data-stu-id="4e258-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="4e258-145">Isso substituirá todo o conteúdo existente nele.</span><span class="sxs-lookup"><span data-stu-id="4e258-145">This will override any content that's there.</span></span>

<span data-ttu-id="4e258-146">**P:** Estou usando meu próprio contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="4e258-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="4e258-147">Não quero que a plataforma monte um compartilhamento SMB para o `\home\`.</span><span class="sxs-lookup"><span data-stu-id="4e258-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="4e258-148">**R:** Você pode fazer isso definindo a configuração de aplicativo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` como `false`.</span><span class="sxs-lookup"><span data-stu-id="4e258-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="4e258-149">**P:** Meu contêiner personalizado demora para iniciar e a plataforma o reinicia antes que ele termine a inicialização.</span><span class="sxs-lookup"><span data-stu-id="4e258-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="4e258-150">**R:** Você pode configurar o tempo que a plataforma aguardará antes de reiniciar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="4e258-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="4e258-151">Isso pode ser feito definindo a configuração de aplicativo `WEBSITES_CONTAINER_START_TIME_LIMIT` para o valor desejado em segundos.</span><span class="sxs-lookup"><span data-stu-id="4e258-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="4e258-152">O padrão é 230 segundos e o máximo é de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="4e258-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="4e258-153">**P:** Qual é o formato da URL do servidor do Registro privado?</span><span class="sxs-lookup"><span data-stu-id="4e258-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="4e258-154">**R:** Você precisa fornecer a URL completa do registro, incluindo `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="4e258-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="4e258-155">**P:** Qual é o formato do nome da imagem na opção de Registro privado?</span><span class="sxs-lookup"><span data-stu-id="4e258-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="4e258-156">**R:** Você precisa adicionar o nome de imagem completo, incluindo a URL do Registro privado (por exemplo,</span><span class="sxs-lookup"><span data-stu-id="4e258-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="4e258-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="4e258-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="4e258-158">**P:** que quero expor mais de uma porta em minha imagem de contêiner personalizados.</span><span class="sxs-lookup"><span data-stu-id="4e258-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="4e258-159">Isso é possível?</span><span class="sxs-lookup"><span data-stu-id="4e258-159">Is that possible?</span></span>

<span data-ttu-id="4e258-160">**R:** No momento, não há suporte para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4e258-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="4e258-161">**P:** posso colocar meu próprio armazenamento?</span><span class="sxs-lookup"><span data-stu-id="4e258-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="4e258-162">**R:** No momento, não há suporte para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4e258-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="4e258-163">**P:** não é possível navegar os processos do meu contêiner personalizado em execução ou de sistema de arquivos do site do SCM.</span><span class="sxs-lookup"><span data-stu-id="4e258-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="4e258-164">Por que isso acontece?</span><span class="sxs-lookup"><span data-stu-id="4e258-164">Why is that?</span></span>

<span data-ttu-id="4e258-165">**R:** O site do SCM é executado em um contêiner separado.</span><span class="sxs-lookup"><span data-stu-id="4e258-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="4e258-166">Não é possível verificar o sistema de arquivos ou os processos em execução do contêiner de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e258-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="4e258-167">**P:** Meu contêiner personalizado escuta uma porta diferente da porta 80.</span><span class="sxs-lookup"><span data-stu-id="4e258-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="4e258-168">Como configurar meu aplicativo para rotear as solicitações para essa porta?</span><span class="sxs-lookup"><span data-stu-id="4e258-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="4e258-169">**R:** Nós temos detecção automática da porta; além disso, é possível especificar uma configuração de aplicativo chamada **WEBSITES_PORT** e fornecer a ela o valor do número da porta esperada.</span><span class="sxs-lookup"><span data-stu-id="4e258-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="4e258-170">A plataforma estava usando a configuração de aplicativo `PORT` anteriormente, estamos planejando substituir o uso dessa configuração de aplicativo e passar a usar exclusivamente `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="4e258-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="4e258-171">**P:** É necessário implementar o HTTPS no meu contêiner personalizado?</span><span class="sxs-lookup"><span data-stu-id="4e258-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="4e258-172">**R:** Não, a plataforma manipula a terminação HTTPS nos front-ends compartilhados.</span><span class="sxs-lookup"><span data-stu-id="4e258-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="4e258-173">Preço e SLA</span><span class="sxs-lookup"><span data-stu-id="4e258-173">Pricing and SLA</span></span>

<span data-ttu-id="4e258-174">**P:** Qual é o preço durante o uso da visualização pública?</span><span class="sxs-lookup"><span data-stu-id="4e258-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="4e258-175">**R:** Você pagará metade do número de horas em que o aplicativo é executado, com o preço normal do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e258-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="4e258-176">Isso significa que você obtém um desconto de 50% sobre o preço normal do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e258-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="4e258-177">Outros</span><span class="sxs-lookup"><span data-stu-id="4e258-177">Other</span></span>

<span data-ttu-id="4e258-178">**P:** quais são os caracteres com suporte em nomes de configurações do aplicativo?</span><span class="sxs-lookup"><span data-stu-id="4e258-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="4e258-179">**R:** Só é possível usar A-Z, a-z, 0-9 e sublinhado para as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e258-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="4e258-180">**P:** onde solicitar novos recursos?</span><span class="sxs-lookup"><span data-stu-id="4e258-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="4e258-181">**R:** É possível enviar sua ideia para o [fórum de comentários dos Aplicativos Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="4e258-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="4e258-182">Adicione “[Linux]” ao título de sua ideia.</span><span class="sxs-lookup"><span data-stu-id="4e258-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e258-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e258-183">Next steps</span></span>
* [<span data-ttu-id="4e258-184">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="4e258-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="4e258-185">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4e258-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="4e258-186">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="4e258-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="4e258-187">Implantação contínua com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4e258-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
