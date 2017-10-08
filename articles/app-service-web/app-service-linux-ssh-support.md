---
title: "suporte a aaaSSH Azure serviço de aplicativo Web App no Linux | Microsoft Docs"
description: Saiba como usar SSH com o Aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="cd799-104">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="cd799-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cd799-105">Overview</span></span>

<span data-ttu-id="cd799-106">O [SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell) é um protocolo de rede criptográfico para usar serviços de rede de forma segura.</span><span class="sxs-lookup"><span data-stu-id="cd799-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="cd799-107">É toolog mais comumente usado em um sistema remotamente com segurança de uma linha de comando e executar comandos administrativos remotamente.</span><span class="sxs-lookup"><span data-stu-id="cd799-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="cd799-108">Web App no Linux fornece suporte SSH no contêiner do aplicativo hello com cada uma das imagens do Docker internas Olá usadas para Olá pilha de tempo de execução de novos aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="cd799-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Pilhas de tempo de execução](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="cd799-110">Você também pode usar SSH com as imagens do Docker personalizadas, incluindo o servidor SSH hello como parte da imagem hello e configurá-lo, conforme descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="cd799-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="cd799-111">Estabelecendo uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="cd799-111">Making a client connection</span></span>

<span data-ttu-id="cd799-112">toomake uma conexão de cliente SSH, o site principal Olá deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="cd799-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="cd799-113">Cole o ponto de extremidade de gerenciamento de controle de origem (SCM) de saudação para seu aplicativo web no seu navegador usando Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd799-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="cd799-114">Se você não estiver autenticado, será necessário tooauthenticate com sua assinatura do Azure tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cd799-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Conexão SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="cd799-116">Suporte de SSH com imagens personalizadas do Docker</span><span class="sxs-lookup"><span data-stu-id="cd799-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="cd799-117">Em ordem para uma personalizado Docker imagem toosupport SSH comunicação entre o contêiner de saudação e cliente Olá Olá portal do Azure, execute Olá seguindo as etapas para a imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="cd799-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="cd799-118">Essas etapas são mostrados na Olá repositório do serviço de aplicativo do Azure como um exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="cd799-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="cd799-119">Incluir Olá `openssh-server` instalação [ `RUN` instrução](https://docs.docker.com/engine/reference/builder/#run) em hello Dockerfile para sua imagem e definir a senha de saudação para conta de raiz de saudação muito`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="cd799-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cd799-120">Essa configuração não permite que o contêiner de toohello conexões externas.</span><span class="sxs-lookup"><span data-stu-id="cd799-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="cd799-121">SSH só pode ser acessado por meio de saudação Kudu / Site de SCM, que é autenticado usando Olá credenciais de publicação.</span><span class="sxs-lookup"><span data-stu-id="cd799-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="cd799-122">Adicionar um [ `COPY` instrução](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy um [sshd_config](http://man.openbsd.org/sshd_config) arquivo toohello */etc/ssh/* directory.</span><span class="sxs-lookup"><span data-stu-id="cd799-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="cd799-123">O arquivo de configuração deve ser baseado em nosso arquivo sshd_config no repositório do GitHub do serviço de aplicativo do Azure Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="cd799-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd799-124">Olá *sshd_config* arquivo deve incluir o seguinte hello ou falha de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="cd799-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="cd799-125">`Ciphers`deve incluir pelo menos um dos seguintes Olá: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="cd799-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="cd799-126">`MACs`deve incluir pelo menos um dos seguintes Olá: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="cd799-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="cd799-127">Incluir porta 2222 na Olá [ `EXPOSE` instrução](https://docs.docker.com/engine/reference/builder/#expose) para Olá Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="cd799-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="cd799-128">Embora a senha de raiz de saudação for conhecida, porta 2222 não pode ser acessada de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="cd799-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="cd799-129">É uma única porta interna acessível somente por contêineres dentro da rede de ponte de saudação de uma rede virtual privada.</span><span class="sxs-lookup"><span data-stu-id="cd799-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="cd799-130">Certifique-se de toostart Olá ssh de serviço.</span><span class="sxs-lookup"><span data-stu-id="cd799-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="cd799-131">exemplo Hello [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) usa um script de shell em */bin* directory.</span><span class="sxs-lookup"><span data-stu-id="cd799-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="cd799-132">Olá Dockerfile usa Olá [ `CMD` instrução](https://docs.docker.com/engine/reference/builder/#cmd) toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd799-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="cd799-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd799-133">Next steps</span></span>
<span data-ttu-id="cd799-134">Consulte Olá seguindo os links para obter mais informações sobre o aplicativo Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="cd799-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="cd799-135">Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="cd799-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="cd799-136">Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="cd799-137">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="cd799-138">Usando o .NET Core no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="cd799-139">Usando Ruby no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="cd799-140">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cd799-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

