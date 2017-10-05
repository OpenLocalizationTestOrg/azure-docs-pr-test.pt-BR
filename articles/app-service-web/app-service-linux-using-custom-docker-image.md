---
title: Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux | Microsoft Docs
description: Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, linux, docker, contêiner"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="4dcac-104">Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4dcac-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="4dcac-105">O Serviço de Aplicativo fornece pilhas de aplicativos predefinidas no Linux com suporte para versões específicas, como PHP 7.0 e Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="4dcac-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="4dcac-106">O Serviço de Aplicativo no Linux usa contêineres do Docker para hospedar estas pilhas de aplicativos predefinidas.</span><span class="sxs-lookup"><span data-stu-id="4dcac-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="4dcac-107">Também é possível usar uma imagem personalizada do Docker para implantar seu aplicativo Web em uma pilha de aplicativos que ainda não foi definida no Azure.</span><span class="sxs-lookup"><span data-stu-id="4dcac-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="4dcac-108">As imagens personalizadas do Docker podem ser hospedadas em um repositório público ou privado do Docker.</span><span class="sxs-lookup"><span data-stu-id="4dcac-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="4dcac-109">Como definir uma imagem personalizada do Docker para um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="4dcac-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="4dcac-110">Você pode definir a imagem personalizada do Docker para aplicativos Web novos e existentes.</span><span class="sxs-lookup"><span data-stu-id="4dcac-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="4dcac-111">Quando você cria um aplicativo Web no Linux no [Portal do Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), clique em **Configurar contêiner** para definir uma imagem personalizada do Docker:</span><span class="sxs-lookup"><span data-stu-id="4dcac-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Imagem personalizada do Docker para um novo aplicativo Web no Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="4dcac-113">Como usar uma imagem personalizada do Docker no Hub do Docker</span><span class="sxs-lookup"><span data-stu-id="4dcac-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="4dcac-114">Para usar uma imagem personalizada do Docker no Hub do Docker:</span><span class="sxs-lookup"><span data-stu-id="4dcac-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="4dcac-115">No [portal do Azure](https://portal.azure.com), localize seu aplicativo Web no Linux e, em **Configurações**, clique em **Contêiner do Docker**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="4dcac-116">Selecione **Hub do Docker** como a **Origem da imagem** e, depois, clique em **Pública** ou **Privada** e digite o **Nome da imagem e o nome opcional da marca**, por exemplo `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="4dcac-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="4dcac-117">O **Comando de inicialização** é definido automaticamente com base no que está definido no arquivo de imagem do Docker, mas você pode definir seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="4dcac-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Configurar a imagem do repositório público do Hub do Docker][2]

    <span data-ttu-id="4dcac-119">Quando a imagem é de um repositório privado, também é precisa inserir as credenciais de Hub do Docker como (**Nome de usuário de logon** e **Senha**) para o repositório privado do Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="4dcac-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Configurar a imagem do repositório privado do Hub do Docker][3]

3. <span data-ttu-id="4dcac-121">Depois de configurar o contêiner, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="4dcac-122">Como usar uma imagem do Docker a partir de um registro da imagem privada</span><span class="sxs-lookup"><span data-stu-id="4dcac-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="4dcac-123">Para usar uma imagem personalizada do Docker a partir de um registro da imagem privada:</span><span class="sxs-lookup"><span data-stu-id="4dcac-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="4dcac-124">No [portal do Azure](https://portal.azure.com), localize seu aplicativo Web no Linux e, em **Configurações**, clique em **Contêiner do Docker**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="4dcac-125">Clique em **Registro privado** como a **Origem da imagem**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="4dcac-126">Insira o **Nome da imagem e da marca opcional**, **URL do Servidor** para o registro privado, juntamente com as credenciais (**nome de usuário de logon** e **senha**).</span><span class="sxs-lookup"><span data-stu-id="4dcac-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="4dcac-127">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-127">Click **Save**.</span></span>

    ![Configurar a imagem de Docker a partir do registro privado][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="4dcac-129">Como configurar a porta usada pela sua imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="4dcac-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="4dcac-130">Quando você usa uma imagem personalizada do Docker para seu aplicativo Web, você pode usar a variável de ambiente `WEBSITES_PORT` em seu Dockerfile, que é adicionado ao contêiner gerado.</span><span class="sxs-lookup"><span data-stu-id="4dcac-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="4dcac-131">Considere o exemplo a seguir de um arquivo do docker para um aplicativo Ruby:</span><span class="sxs-lookup"><span data-stu-id="4dcac-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="4dcac-132">Na última linha do comando, você pode ver que a variável de ambiente WEBSITES_PORT é transmitida em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="4dcac-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="4dcac-133">Lembre-se de que as diferenças entre maiúsculas e minúsculas importam nos comandos.</span><span class="sxs-lookup"><span data-stu-id="4dcac-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="4dcac-134">A plataforma estava usando a configuração de aplicativo `PORT` anteriormente, estamos planejando substituir o uso dessa configuração de aplicativo e passar a usar exclusivamente `WEBSITES_PORT`.</span><span class="sxs-lookup"><span data-stu-id="4dcac-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="4dcac-135">Ao usar uma imagem existente do Docker criada por outra pessoa, talvez seja necessário especificar uma porta diferente da porta 80 para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4dcac-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="4dcac-136">Para configurar a porta, adicione um configuração de aplicativo chamada `WEBSITES_PORT` com o valor mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4dcac-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![Definir a configuração de aplicativo PORT para a imagem personalizada do Docker][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="4dcac-138">Como definir a hora de inicialização para sua imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="4dcac-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="4dcac-139">Por padrão, se o contêiner não for iniciado antes de 230 segundos, a plataforma o reiniciará.</span><span class="sxs-lookup"><span data-stu-id="4dcac-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="4dcac-140">Se a imagem personalizada do Docker demorar mais 230 segundos para iniciar, você poderá usar a configuração de aplicativo `WEBSITES_CONTAINER_START_TIME_LIMIT`; o valor para essa configuração estará em segundos, o que permitirá que a plataforma mantenha o contêiner em execução antes de reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="4dcac-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="4dcac-141">O valor padrão é 230 segundos e o valor máximo permitido é 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="4dcac-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="4dcac-142">Como desmontar o armazenamento fornecido pela plataforma</span><span class="sxs-lookup"><span data-stu-id="4dcac-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="4dcac-143">Por padrão, a plataforma montará um compartilhamento de armazenamento persistente para o diretório `\home\`.</span><span class="sxs-lookup"><span data-stu-id="4dcac-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="4dcac-144">Se a imagem do contêiner não precisar de um compartilhamento persistente, você poderá desabilitar a montagem do armazenamento definindo a configuração de aplicativo `WEBSITES_ENABLE_APP_SERVICE_STORAGE` como `false`.</span><span class="sxs-lookup"><span data-stu-id="4dcac-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="4dcac-145">Você continuará tendo acesso a esse armazenamento pelo site scm e todos os logs do Docker (se habilitados) serão gravados nos arquivos de log gerados pela plataforma.</span><span class="sxs-lookup"><span data-stu-id="4dcac-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="4dcac-146">Como voltar a usar uma imagem interna</span><span class="sxs-lookup"><span data-stu-id="4dcac-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="4dcac-147">Para trocar uma imagem personalizada para uma imagem interna:</span><span class="sxs-lookup"><span data-stu-id="4dcac-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="4dcac-148">No [portal do Azure](https://portal.azure.com), localize seu aplicativo Web no Linux e, em **Configurações**, clique em **Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="4dcac-149">Selecione sua **Pilha em Tempo de Execução** para usar para a imagem interna, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Configurar a imagem interna do Docker][5]


## <a name="troubleshooting"></a><span data-ttu-id="4dcac-151">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="4dcac-151">Troubleshooting</span></span> ##

<span data-ttu-id="4dcac-152">Quando o aplicativo falha ao iniciar com sua imagem personalizada do Docker, verifique os log do Docker no diretório LogFiles.</span><span class="sxs-lookup"><span data-stu-id="4dcac-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="4dcac-153">Acesse esse diretório por meio de seu site SCM ou via FTP.</span><span class="sxs-lookup"><span data-stu-id="4dcac-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="4dcac-154">Para registrar `stdout` e `stderr` por meio do contêiner, você precisa habilitar o **Registro em log do Contêiner do Docker** em **Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitando o log][8]

![Como usar o Kudu para exibir os logs do Docker][7]

<span data-ttu-id="4dcac-157">Acesse o site SCM nas **Ferramentas Avançadas** no menu **Ferramentas de Desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="4dcac-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dcac-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4dcac-158">Next Steps</span></span> ##

<span data-ttu-id="4dcac-159">Siga estes links para começar a usar o Aplicativo Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="4dcac-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="4dcac-160">Introdução ao Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4dcac-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="4dcac-161">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4dcac-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="4dcac-162">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="4dcac-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="4dcac-163">Poste perguntas e preocupações em [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="4dcac-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
