---
title: "Suporte de SSH para o Aplicativo Web do Serviço de Aplicativo do Azure no Linux | Microsoft Docs"
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
ms.openlocfilehash: feee7a5c91d213a6b0bfdaf264a4da4d9e79cbe7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="b44d5-104">Suporte de SSH para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="b44d5-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b44d5-105">Overview</span></span>

<span data-ttu-id="b44d5-106">O [SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell) é um protocolo de rede criptográfico para usar serviços de rede de forma segura.</span><span class="sxs-lookup"><span data-stu-id="b44d5-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="b44d5-107">Ele é usado com maior frequência para fazer logon em um sistema remotamente com segurança em uma linha de comando, bem como para executar comandos administrativos remotamente.</span><span class="sxs-lookup"><span data-stu-id="b44d5-107">It is most commonly used to log into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="b44d5-108">O Aplicativo Web no Linux fornece suporte de SSH no contêiner de aplicativo com cada uma das imagens internas do Docker usadas para a Pilha em Tempo de Execução de novos aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="b44d5-108">Web App on Linux provides SSH support into the app container with each of the built-in Docker images used for the Runtime Stack of new web apps.</span></span> 

![Pilhas de tempo de execução](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="b44d5-110">Você também pode usar SSH com suas imagens personalizadas do Docker incluindo o servidor SSH como parte da imagem e configurando-o conforme descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b44d5-110">You can also use SSH with your custom Docker images by including the SSH server as part of the image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="b44d5-111">Estabelecendo uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="b44d5-111">Making a client connection</span></span>

<span data-ttu-id="b44d5-112">Para estabelecer uma conexão de cliente SSH, o site principal deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="b44d5-112">To make an SSH client connection, the main site must be started.</span></span> 

<span data-ttu-id="b44d5-113">Cole o ponto de extremidade de SCM (gerenciamento de controle do código-fonte) de seu aplicativo Web no navegador usando o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b44d5-113">Paste the Source Control Management (SCM) endpoint for your web app into your browser using the following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="b44d5-114">Se ainda não estiver autenticado, você precisará se autenticar usando sua assinatura do Azure para se conectar.</span><span class="sxs-lookup"><span data-stu-id="b44d5-114">If you are not already authenticated, you are required to authenticate with your Azure subscription to connect.</span></span>

![Conexão SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="b44d5-116">Suporte de SSH com imagens personalizadas do Docker</span><span class="sxs-lookup"><span data-stu-id="b44d5-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="b44d5-117">Para que uma imagem personalizada do Docker dê suporte à comunicação SSH entre o contêiner e o cliente no portal do Azure, execute as seguintes etapas para a imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="b44d5-117">In order for a custom Docker image to support SSH communication between the container and the client in the Azure portal, perform the following steps for your Docker image.</span></span> 

<span data-ttu-id="b44d5-118">Essas etapas são mostradas no repositório do Serviço de Aplicativo do Azure como exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="b44d5-118">These steps are are shown in the Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="b44d5-119">Inclua a instalação `openssh-server` na [instrução `RUN`](https://docs.docker.com/engine/reference/builder/#run) no Dockerfile para sua imagem e defina a senha da conta raiz como `"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="b44d5-119">Include the `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in the Dockerfile for your image and set the password for the root account to `"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="b44d5-120">Essa configuração não permite conexões externas com o contêiner.</span><span class="sxs-lookup"><span data-stu-id="b44d5-120">This configuration does not allow external connections to the container.</span></span> <span data-ttu-id="b44d5-121">O SSH só pode ser acessado por meio do site do Kudu/SCM, que é autenticado usando as credenciais de publicação.</span><span class="sxs-lookup"><span data-stu-id="b44d5-121">SSH can only be accessed via the Kudu / SCM Site, which is authenticated using the publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="b44d5-122">Adicione uma [instrução `COPY`](https://docs.docker.com/engine/reference/builder/#copy) ao Dockerfile para copiar um arquivo [sshd_config](http://man.openbsd.org/sshd_config) para o diretório */etc/ssh/*.</span><span class="sxs-lookup"><span data-stu-id="b44d5-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) to the Dockerfile to copy a [sshd_config](http://man.openbsd.org/sshd_config) file to the */etc/ssh/* directory.</span></span> <span data-ttu-id="b44d5-123">Seu arquivo de configuração deve ser baseado em nosso arquivo sshd_config no repositório Azure-App-Service do GitHub [aqui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="b44d5-123">Your configuration file should be based on our sshd_config file in the Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b44d5-124">O arquivo *sshd_config* deve incluir o seguinte ou a conexão falhará:</span><span class="sxs-lookup"><span data-stu-id="b44d5-124">The *sshd_config* file must include the following or the connection fails:</span></span> 
    > * <span data-ttu-id="b44d5-125">`Ciphers` deve incluir pelo menos um dos itens a seguir: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="b44d5-125">`Ciphers` must include at least one of the following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="b44d5-126">`MACs` deve incluir pelo menos um dos itens a seguir: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="b44d5-126">`MACs` must include at least one of the following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="b44d5-127">Inclua a porta 2222 na [instrução `EXPOSE`](https://docs.docker.com/engine/reference/builder/#expose) para o Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="b44d5-127">Include port 2222 in the [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for the Dockerfile.</span></span> <span data-ttu-id="b44d5-128">Embora a senha raiz seja conhecida, a porta 2222 não pode ser acessada da Internet.</span><span class="sxs-lookup"><span data-stu-id="b44d5-128">Although the root password is known, port 2222 cannot be accessed from the internet.</span></span> <span data-ttu-id="b44d5-129">Ela é uma porta interna que pode ser acessada somente por contêineres dentro da rede ponte de uma rede virtual privada.</span><span class="sxs-lookup"><span data-stu-id="b44d5-129">It is an internal only port accessible only by containers within the bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="b44d5-130">Certifique-se de iniciar o serviço SSH.</span><span class="sxs-lookup"><span data-stu-id="b44d5-130">Make sure to start the ssh service.</span></span> <span data-ttu-id="b44d5-131">Este exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) usa um script shell no diretório */bin*.</span><span class="sxs-lookup"><span data-stu-id="b44d5-131">The example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="b44d5-132">O Dockerfile usa a [instrução `CMD`](https://docs.docker.com/engine/reference/builder/#cmd) para executar o script.</span><span class="sxs-lookup"><span data-stu-id="b44d5-132">The Dockerfile uses the [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) to run the script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="b44d5-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b44d5-133">Next steps</span></span>
<span data-ttu-id="b44d5-134">Consulte os links a seguir para obter mais informações sobre o Aplicativo Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="b44d5-134">See the following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="b44d5-135">Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="b44d5-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="b44d5-136">Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-136">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="b44d5-137">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="b44d5-138">Usando o .NET Core no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="b44d5-139">Usando Ruby no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="b44d5-140">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="b44d5-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

