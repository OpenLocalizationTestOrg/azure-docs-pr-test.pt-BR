---
title: aaaHow toouse uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux | Microsoft Docs
description: Como toouse um Docker personalizado de imagem para o aplicativo Web do Azure no Linux.
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
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="05c00-104">Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="05c00-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="05c00-105">O Serviço de Aplicativo fornece pilhas de aplicativos predefinidas no Linux com suporte para versões específicas, como PHP 7.0 e Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="05c00-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="05c00-106">Serviço de aplicativo no Linux usa contêineres do Docker toohost esses pré-criadas pilhas de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="05c00-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="05c00-107">Você também pode usar um toodeploy de imagem personalizada do Docker sua pilha de aplicativos de tooan de aplicativo web que não ainda esteja definida no Azure.</span><span class="sxs-lookup"><span data-stu-id="05c00-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="05c00-108">As imagens personalizadas do Docker podem ser hospedadas em um repositório público ou privado do Docker.</span><span class="sxs-lookup"><span data-stu-id="05c00-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="05c00-109">Como definir uma imagem personalizada do Docker para um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="05c00-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="05c00-110">Você pode definir a imagem personalizada do Docker Olá para os novos e aplicativos de webs existentes.</span><span class="sxs-lookup"><span data-stu-id="05c00-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="05c00-111">Quando você cria um aplicativo web no Linux no hello [portal do Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), clique em **configurar contêiner** tooset uma imagem personalizada do Docker:</span><span class="sxs-lookup"><span data-stu-id="05c00-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Imagem personalizada do Docker para um novo aplicativo Web no Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="05c00-113">Como usar uma imagem personalizada do Docker no Hub do Docker</span><span class="sxs-lookup"><span data-stu-id="05c00-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="05c00-114">toouse uma imagem personalizada do Docker do Hub do Docker:</span><span class="sxs-lookup"><span data-stu-id="05c00-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="05c00-115">Em hello [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="05c00-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="05c00-116">Selecione **Hub do Docker** como Olá **origem da imagem**, em seguida, clique em **pública** ou **privada** e tipo hello **imagem e o nome da marca opcional**, como `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="05c00-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="05c00-117">Olá **comando de inicialização** é conjunto automaticamente com base no que é definido no arquivo de imagem do Docker hello, mas você pode definir seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="05c00-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Configurar a imagem do repositório público do Hub do Docker][2]

    <span data-ttu-id="05c00-119">Quando a imagem for de um repositório privado, você também precisa ter credenciais de Hub do Docker do tooenter hello como (**nome de usuário de logon** e **senha**) para repositório de Hub do Docker particular hello.</span><span class="sxs-lookup"><span data-stu-id="05c00-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Configurar a imagem do repositório privado do Hub do Docker][3]

3. <span data-ttu-id="05c00-121">Depois que você tiver configurado o contêiner de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="05c00-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="05c00-122">Como a imagem de um registro da imagem privada toouse um Docker</span><span class="sxs-lookup"><span data-stu-id="05c00-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="05c00-123">toouse uma imagem personalizada do Docker de um registro da imagem privada:</span><span class="sxs-lookup"><span data-stu-id="05c00-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="05c00-124">Em hello [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="05c00-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="05c00-125">Clique em **registro privado** como Olá **origem da imagem**.</span><span class="sxs-lookup"><span data-stu-id="05c00-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="05c00-126">Digite hello **imagem e o nome de marca opcional**, **URL do servidor** para registro privada hello, juntamente com as credenciais da saudação (**nome de usuário de logon** e **senha** ).</span><span class="sxs-lookup"><span data-stu-id="05c00-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="05c00-127">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="05c00-127">Click **Save**.</span></span>

    ![Configurar a imagem de Docker a partir do registro privado][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="05c00-129">Como: definir Olá porta usada pela sua imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="05c00-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="05c00-130">Quando você usar uma imagem personalizada do Docker para seu aplicativo web, você pode usar o hello `WEBSITES_PORT` variável de ambiente no Dockerfile, o que é adicionado contêiner toohello gerado.</span><span class="sxs-lookup"><span data-stu-id="05c00-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="05c00-131">Considere Olá exemplo de um arquivo de docker para um aplicativo Ruby a seguir:</span><span class="sxs-lookup"><span data-stu-id="05c00-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="05c00-132">Na última linha de comando hello, você pode ver que essa variável de ambiente WEBSITES_PORT Olá é passado em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="05c00-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="05c00-133">Lembre-se de que as diferenças entre maiúsculas e minúsculas importam nos comandos.</span><span class="sxs-lookup"><span data-stu-id="05c00-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="05c00-134">Plataforma Olá foi usando previamente `PORT` aplicativo configuração, podemos estiver planejando toodeprecate Olá use essa configuração de aplicativo e mover toousing `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="05c00-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="05c00-135">Quando você usar uma imagem do Docker existente criada por outra pessoa, talvez seja necessário toospecify uma porta diferente da porta 80 para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="05c00-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="05c00-136">tooconfigure Olá porta, adicione um configuração de aplicativo denominada `WEBSITES_PORT` com valor de saudação conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="05c00-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Definir a configuração de aplicativo PORT para a imagem personalizada do Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="05c00-138">Como: definir o tempo de inicialização de saudação para a imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="05c00-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="05c00-139">Por padrão, se o contêiner não for iniciado antes de 230 segundos, plataforma Olá reiniciará seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="05c00-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="05c00-140">Se sua imagem personalizada do Docker é iniciado em mais de 230 segundos, você pode usar o hello `WEBSITES_CONTAINER_START_TIME_LIMIT` aplicativo definindo, valor Olá para essa configuração é em segundos, isso permitirá Olá plataforma manter seu contêiner em execução antes de reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="05c00-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="05c00-141">valor padrão de saudação é 230 segundos e Olá máximo permitido para valor é de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="05c00-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="05c00-142">Como: desmontar o armazenamento de plataforma fornecido Olá</span><span class="sxs-lookup"><span data-stu-id="05c00-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="05c00-143">Por padrão, a plataforma de saudação montará toohello de compartilhamento de um armazenamento persistente `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="05c00-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="05c00-144">Se sua imagem de contêiner não precisa de um compartilhamento persistente, você pode desabilitar a montagem que o armazenamento por configuração Olá `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicativo configuração muito`false`.</span><span class="sxs-lookup"><span data-stu-id="05c00-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="05c00-145">Você ainda terá acesso toothat armazenamento do site de scm hello e todos os logs de Docker (se habilitado) serão gravados toohello arquivos de log gerados pela plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="05c00-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="05c00-146">Como: retorne toousing uma imagem interna</span><span class="sxs-lookup"><span data-stu-id="05c00-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="05c00-147">tooswitch de usar uma imagem personalizada de toousing uma imagem interna:</span><span class="sxs-lookup"><span data-stu-id="05c00-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="05c00-148">Em Olá [portal do Azure](https://portal.azure.com), localize o aplicativo web no Linux, em seguida, na **configurações** clique **do serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="05c00-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="05c00-149">Selecione seu **pilha de tempo de execução** toouse para imagem interna do hello, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="05c00-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Configurar a imagem interna do Docker][5]


## <a name="troubleshooting"></a><span data-ttu-id="05c00-151">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="05c00-151">Troubleshooting</span></span> ##

<span data-ttu-id="05c00-152">Quando o aplicativo falhar toostart com sua imagem personalizada do Docker, verifique Olá que docker registra no diretório de arquivos de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="05c00-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="05c00-153">Acesse esse diretório por meio de seu site SCM ou via FTP.</span><span class="sxs-lookup"><span data-stu-id="05c00-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="05c00-154">Olá toolog `stdout` e `stderr` de seu contêiner, você precisa tooenable **log do contêiner do Docker** em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="05c00-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitando o log][8]

![Usando logs de Docker tooview Kudu][7]

<span data-ttu-id="05c00-157">Você pode acessar o site SCM saudação do **ferramentas avançadas de** em Olá **ferramentas de desenvolvimento** menu.</span><span class="sxs-lookup"><span data-stu-id="05c00-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c00-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05c00-158">Next Steps</span></span> ##

<span data-ttu-id="05c00-159">Siga Olá tooget links de Introdução ao aplicativo Web no Linux a seguir.</span><span class="sxs-lookup"><span data-stu-id="05c00-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="05c00-160">Introdução tooAzure Web App no Linux</span><span class="sxs-lookup"><span data-stu-id="05c00-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="05c00-161">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="05c00-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="05c00-162">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="05c00-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="05c00-163">Poste perguntas e preocupações em [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="05c00-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
