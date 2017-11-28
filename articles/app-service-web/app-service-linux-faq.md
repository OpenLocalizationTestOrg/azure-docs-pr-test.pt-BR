---
title: "aaaAzure aplicativo de serviço Web aplicativo nas perguntas frequentes sobre o Linux | Microsoft Docs"
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
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="ecd17-104">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ecd17-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="ecd17-105">Com a versão de saudação do aplicativo Web no Linux, estamos trabalhando para adicionar recursos e fazer melhorias tooour plataforma.</span><span class="sxs-lookup"><span data-stu-id="ecd17-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="ecd17-106">Aqui estão algumas perguntas frequentes (FAQ) que nossos clientes têm solicitado conosco sobre Olá última meses.</span><span class="sxs-lookup"><span data-stu-id="ecd17-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="ecd17-107">Se você tiver uma pergunta, o comentário sobre o artigo hello e responderemos-lo assim que possível.</span><span class="sxs-lookup"><span data-stu-id="ecd17-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="ecd17-108">Imagens internas</span><span class="sxs-lookup"><span data-stu-id="ecd17-108">Built-in images</span></span>

<span data-ttu-id="ecd17-109">**P:** desejo toofork Olá internos contêineres do Docker que Olá plataforma fornece.</span><span class="sxs-lookup"><span data-stu-id="ecd17-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="ecd17-110">Onde posso encontrar esses arquivos?</span><span class="sxs-lookup"><span data-stu-id="ecd17-110">Where can I find those files?</span></span>

<span data-ttu-id="ecd17-111">**R:** É possível encontrar todos os arquivos do Docker no [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="ecd17-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="ecd17-112">É possível encontrar todos os contêineres do Docker no [Hub do Docker](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="ecd17-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="ecd17-113">**P:** quais são os valores esperados de saudação para Olá seção do arquivo de inicialização quando configura o pilha de tempo de execução de saudação?</span><span class="sxs-lookup"><span data-stu-id="ecd17-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="ecd17-114">**R:** para Node.Js, especifique o arquivo de configuração Olá PM2 ou o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="ecd17-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="ecd17-115">Para o .NET Core, especifique o nome da DLL compilada.</span><span class="sxs-lookup"><span data-stu-id="ecd17-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="ecd17-116">Para Ruby, você pode especificar Olá Ruby script que você deseja tooinitialize seu aplicativo com.</span><span class="sxs-lookup"><span data-stu-id="ecd17-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="ecd17-117">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ecd17-117">Management</span></span>

<span data-ttu-id="ecd17-118">**P:** o que acontece quando eu pressionar o botão de reinicialização de saudação em Olá portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="ecd17-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="ecd17-119">**R:** isso é Olá equivalente de reinicialização do Docker.</span><span class="sxs-lookup"><span data-stu-id="ecd17-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="ecd17-120">**P:** posso usar o Secure Shell (SSH) tooconnect toohello aplicativo contêiner VM (máquina virtual)?</span><span class="sxs-lookup"><span data-stu-id="ecd17-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="ecd17-121">**R:** Sim, você pode fazer que através do site SCM hello, seleção seguinte de saudação do artigo para obter mais informações [suporte SSH para o aplicativo Web no Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="ecd17-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="ecd17-122">**P:** desejo toocreate um plano de Linux App Service através do SDK ou um modelo do ARM, como fazer isso?</span><span class="sxs-lookup"><span data-stu-id="ecd17-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="ecd17-123">**R:** necessário Olá tooset `reserved` campo do aplicativo hello serviço muito`true`.</span><span class="sxs-lookup"><span data-stu-id="ecd17-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="ecd17-124">Integração/implantação contínua</span><span class="sxs-lookup"><span data-stu-id="ecd17-124">Continuous integration/deployment</span></span>

<span data-ttu-id="ecd17-125">**P:** meu aplicativo web ainda usa uma imagem de contêiner do Docker antiga depois de atualizar a imagem Olá no Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="ecd17-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="ecd17-126">Há suporte para implantação/integração contínua de contêineres personalizados?</span><span class="sxs-lookup"><span data-stu-id="ecd17-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="ecd17-127">**R:** tooset integração/implantação contínua para imagens de registro de contêiner do Azure ou DockerHub por seleção Olá artigo a seguir [implantação contínua com o aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="ecd17-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="ecd17-128">Para registros privados, você pode atualizar o contêiner de saudação ao parar e iniciar o seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="ecd17-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="ecd17-129">Ou você pode alterar ou adicionar um aplicativo fictício configuração tooforce uma atualização do seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecd17-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="ecd17-130">**P:** Há suporte para ambientes de preparo?</span><span class="sxs-lookup"><span data-stu-id="ecd17-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="ecd17-131">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="ecd17-131">**A:** Yes.</span></span>

<span data-ttu-id="ecd17-132">**P:** posso usar **implantação da web** toodeploy meu aplicativo web?</span><span class="sxs-lookup"><span data-stu-id="ecd17-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="ecd17-133">**R:** Sim, você precisa tooset um aplicativo chamada `WEBSITE_WEBDEPLOY_USE_SCM` muito`false`.</span><span class="sxs-lookup"><span data-stu-id="ecd17-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="ecd17-134">Suporte ao idioma</span><span class="sxs-lookup"><span data-stu-id="ecd17-134">Language support</span></span>

<span data-ttu-id="ecd17-135">**P:** Há suporte para aplicativos .NET Core não compilados?</span><span class="sxs-lookup"><span data-stu-id="ecd17-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="ecd17-136">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="ecd17-136">**A:** Yes.</span></span>

<span data-ttu-id="ecd17-137">**P:** Há suporte para o Criador como um gerenciador de dependências para aplicativos PHP?</span><span class="sxs-lookup"><span data-stu-id="ecd17-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="ecd17-138">**R:** Sim.</span><span class="sxs-lookup"><span data-stu-id="ecd17-138">**A:** Yes.</span></span> <span data-ttu-id="ecd17-139">Durante a implantação de Git, Kudu deve detectar que você está implantando um aplicativo PHP (obrigado a presença de toohello de um arquivo de composer.json) e disparará uma instalação de criador para você.</span><span class="sxs-lookup"><span data-stu-id="ecd17-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="ecd17-140">Contêineres personalizados</span><span class="sxs-lookup"><span data-stu-id="ecd17-140">Custom containers</span></span>

<span data-ttu-id="ecd17-141">**P:** Estou usando meu próprio contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="ecd17-142">Meu aplicativo reside no hello `\home\` diretório, mas não é possível localizar Meus arquivos quando navegar conteúdo hello usando Olá [site SCM](https://github.com/projectkudu/kudu) ou um cliente de FTP.</span><span class="sxs-lookup"><span data-stu-id="ecd17-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="ecd17-143">Onde estão meus arquivos?</span><span class="sxs-lookup"><span data-stu-id="ecd17-143">Where are my files?</span></span>

<span data-ttu-id="ecd17-144">**R:** montamos uma toohello de compartilhamento SMB `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="ecd17-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="ecd17-145">Isso substituirá todo o conteúdo existente nele.</span><span class="sxs-lookup"><span data-stu-id="ecd17-145">This will override any content that's there.</span></span>

<span data-ttu-id="ecd17-146">**P:** Estou usando meu próprio contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="ecd17-147">Não quero Olá plataforma toomount um toohello de compartilhamento SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="ecd17-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="ecd17-148">**R:** você pode fazer isso por configuração Olá `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicativo configuração muito`false`.</span><span class="sxs-lookup"><span data-stu-id="ecd17-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="ecd17-149">**P:** meu contêiner personalizado leva um tempo longo toostart e conclusão contêiner de saudação do hello plataforma reinicialização antes que ele for iniciado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="ecd17-150">**R:** você pode configurar o tempo de saudação plataforma Olá aguardará antes de reiniciar seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecd17-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="ecd17-151">Isso pode ser feito por configuração Olá `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de configuração de aplicativo o valor desejado em segundos.</span><span class="sxs-lookup"><span data-stu-id="ecd17-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="ecd17-152">padrão de saudação é 230 segundos e Olá máximo é de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="ecd17-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="ecd17-153">**P:** o que é o formato de saudação para url do servidor de registro privada?</span><span class="sxs-lookup"><span data-stu-id="ecd17-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="ecd17-154">**R:** necessárias tooprovide Olá registro completo url incluindo `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="ecd17-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="ecd17-155">**P:** o que é o formato de saudação para nome da imagem Olá na opção do registro privada?</span><span class="sxs-lookup"><span data-stu-id="ecd17-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="ecd17-156">**R:** você precisa de nome de imagem completa Olá tooadd incluindo Olá url de registro particular (por exemplo.</span><span class="sxs-lookup"><span data-stu-id="ecd17-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="ecd17-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="ecd17-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="ecd17-158">**P:** desejada tooexpose mais de uma porta na minha imagem de contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="ecd17-159">Isso é possível?</span><span class="sxs-lookup"><span data-stu-id="ecd17-159">Is that possible?</span></span>

<span data-ttu-id="ecd17-160">**R:** No momento, não há suporte para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ecd17-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="ecd17-161">**P:** posso colocar meu próprio armazenamento?</span><span class="sxs-lookup"><span data-stu-id="ecd17-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="ecd17-162">**R:** No momento, não há suporte para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ecd17-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="ecd17-163">**P:** não é possível navegar os processos do meu contêiner personalizado execução ou sistema de arquivos do site SCM Olá.</span><span class="sxs-lookup"><span data-stu-id="ecd17-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="ecd17-164">Por que isso acontece?</span><span class="sxs-lookup"><span data-stu-id="ecd17-164">Why is that?</span></span>

<span data-ttu-id="ecd17-165">**R:** site SCM Olá é executado em um contêiner separado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="ecd17-166">Não é possível verificar o sistema de arquivos de saudação ou executando processos do contêiner do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ecd17-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="ecd17-167">**P:** meu contêiner personalizado escuta tooa porta diferente da porta 80.</span><span class="sxs-lookup"><span data-stu-id="ecd17-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="ecd17-168">Como posso configurar meu aplicativo tooroute Olá solicitações toothat porta?</span><span class="sxs-lookup"><span data-stu-id="ecd17-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="ecd17-169">**R:** temos a detecção automática porta, também é possível especificar um aplicativo de chamada **WEBSITES_PORT**e dê a ele valor de saudação do número de porta Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="ecd17-170">Plataforma Olá foi usando previamente `PORT` aplicativo configuração, podemos estiver planejando toodeprecate Olá use essa configuração de aplicativo e mover toousing `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="ecd17-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="ecd17-171">**P:** necessário tooimplement HTTPS no meu contêiner personalizado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="ecd17-172">**R:** não, plataforma Olá manipula a terminação HTTPS no front-ends Olá compartilhado.</span><span class="sxs-lookup"><span data-stu-id="ecd17-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="ecd17-173">Preço e SLA</span><span class="sxs-lookup"><span data-stu-id="ecd17-173">Pricing and SLA</span></span>

<span data-ttu-id="ecd17-174">**P:** o que é Olá preços enquanto você estiver usando a visualização pública Olá?</span><span class="sxs-lookup"><span data-stu-id="ecd17-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="ecd17-175">**R:** você é cobrado pelo número de saudação metade de horas que seu aplicativo é executado, com preços do saudação normal do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd17-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="ecd17-176">Isso significa que você obtém um desconto de 50% sobre o preço normal do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd17-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="ecd17-177">outro</span><span class="sxs-lookup"><span data-stu-id="ecd17-177">Other</span></span>

<span data-ttu-id="ecd17-178">**P:** o que são caracteres hello suportado em nomes de configurações do aplicativo?</span><span class="sxs-lookup"><span data-stu-id="ecd17-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="ecd17-179">**R:** você só pode usar A-Z, a-z, 0-9 e Olá sublinhado para configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ecd17-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="ecd17-180">**P:** onde solicitar novos recursos?</span><span class="sxs-lookup"><span data-stu-id="ecd17-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="ecd17-181">**R:** poderá enviar sua ideia no hello [Fórum de comentários de aplicativos Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="ecd17-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="ecd17-182">Adicione "[Linux]" toohello título de sua ideia.</span><span class="sxs-lookup"><span data-stu-id="ecd17-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecd17-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecd17-183">Next steps</span></span>
* [<span data-ttu-id="ecd17-184">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="ecd17-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="ecd17-185">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ecd17-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="ecd17-186">Configurar ambientes de preparo no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ecd17-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="ecd17-187">Implantação contínua com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="ecd17-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
