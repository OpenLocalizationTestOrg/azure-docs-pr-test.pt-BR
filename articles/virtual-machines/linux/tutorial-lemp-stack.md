---
title: "aaaDeploy LEMP em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial - pilha LEMP Olá instalar em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="214f2-103">Instalar um servidor Web LEMP em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="214f2-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="214f2-104">Este artigo o orienta como toodeploy uma NGINX web server, MySQL e PHP (pilha LEMP Olá) em uma VM Ubuntu no Azure.</span><span class="sxs-lookup"><span data-stu-id="214f2-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="214f2-105">pilha LEMP Olá é uma alternativa toohello popular [pilha LAMP](tutorial-lamp-stack.md), que você também pode instalar no Azure.</span><span class="sxs-lookup"><span data-stu-id="214f2-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="214f2-106">servidor LEMP Olá toosee em ação, opcionalmente, você pode instalar e configurar um site de WordPress.</span><span class="sxs-lookup"><span data-stu-id="214f2-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="214f2-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="214f2-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="214f2-108">Criar uma VM Ubuntu (Olá 'L' na pilha LEMP Olá)</span><span class="sxs-lookup"><span data-stu-id="214f2-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="214f2-109">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="214f2-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="214f2-110">Instalar NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="214f2-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="214f2-111">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="214f2-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="214f2-112">Instalar o WordPress no servidor LEMP Olá</span><span class="sxs-lookup"><span data-stu-id="214f2-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="214f2-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="214f2-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="214f2-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="214f2-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="214f2-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="214f2-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="214f2-116">Instalar NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="214f2-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="214f2-117">Execute Olá comando tooupdate Ubuntu pacote origens a seguir e instalar o PHP, MySQL e NGINX.</span><span class="sxs-lookup"><span data-stu-id="214f2-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="214f2-118">Você está tooinstall solicitadas Olá pacotes e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="214f2-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="214f2-119">Quando solicitado, defina uma senha de raiz para o MySQL e toocontinue [Enter].</span><span class="sxs-lookup"><span data-stu-id="214f2-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="214f2-120">Siga Olá restantes prompts.</span><span class="sxs-lookup"><span data-stu-id="214f2-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="214f2-121">Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="214f2-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="214f2-123">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="214f2-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="214f2-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="214f2-124">NGINX</span></span>

<span data-ttu-id="214f2-125">Verifique a versão de saudação do NGINX com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="214f2-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="214f2-126">Com NGINX instalado e a porta 80 abra tooyour VM, servidor de web hello agora pode ser acessado de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="214f2-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="214f2-127">página inicial do tooview Olá NGINX, abra um navegador da web e digite o endereço IP público de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="214f2-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="214f2-128">Use o endereço IP público Olá usado tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="214f2-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Página padrão do NGINX][3]


### <a name="mysql"></a><span data-ttu-id="214f2-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="214f2-130">MySQL</span></span>

<span data-ttu-id="214f2-131">Verificar a versão de saudação do MySQL com o comando a seguir de saudação (Observe maiuscula Olá `V` parâmetro):</span><span class="sxs-lookup"><span data-stu-id="214f2-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="214f2-132">É recomendável executar Olá após a instalação do script toohelp Olá segura do MySQL:</span><span class="sxs-lookup"><span data-stu-id="214f2-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="214f2-133">Digite sua senha de raiz de MySQL e definir configurações de segurança Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="214f2-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="214f2-134">Se você quiser toocreate um banco de dados MySQL, adicionar usuários ou alterar definições de configuração, tooMySQL de logon:</span><span class="sxs-lookup"><span data-stu-id="214f2-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="214f2-135">Quando terminar, saia Olá mysql prompt digitando `\q`.</span><span class="sxs-lookup"><span data-stu-id="214f2-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="214f2-136">PHP</span><span class="sxs-lookup"><span data-stu-id="214f2-136">PHP</span></span>

<span data-ttu-id="214f2-137">Verifique a versão de saudação do PHP com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="214f2-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="214f2-138">Configure a saudação de toouse NGINX o Gerenciador de processo de FastCGI do PHP (PHP FPM).</span><span class="sxs-lookup"><span data-stu-id="214f2-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="214f2-139">Execute Olá tooback servidor NGINX original de saudação bloquear o arquivo de configuração e edite o arquivo original de saudação em um editor de sua escolha de comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="214f2-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="214f2-140">No editor de hello, substitua o conteúdo de saudação do `/etc/nginx/sites-available/default` com os seguintes hello.</span><span class="sxs-lookup"><span data-stu-id="214f2-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="214f2-141">Consulte Olá comentários para obter explicação das configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="214f2-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="214f2-142">Substitua o endereço IP público de saudação da VM para *yourPublicIPAddress*e deixe Olá restantes configurações.</span><span class="sxs-lookup"><span data-stu-id="214f2-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="214f2-143">Salve arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="214f2-143">Then save hello file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="214f2-144">Verifique a configuração de NGINX Olá erros de sintaxe:</span><span class="sxs-lookup"><span data-stu-id="214f2-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="214f2-145">Se a sintaxe de saudação estiver correto, reinicie o NGINX com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="214f2-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="214f2-146">Se você quiser mais tootest, crie um tooview de página de informações rápida do PHP em um navegador.</span><span class="sxs-lookup"><span data-stu-id="214f2-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="214f2-147">Olá comando a seguir cria uma página de informações do PHP hello:</span><span class="sxs-lookup"><span data-stu-id="214f2-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="214f2-148">Agora você pode verificar a página de informações do PHP Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="214f2-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="214f2-149">Abra um navegador e vá muito`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="214f2-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="214f2-150">Substitua o endereço IP público de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="214f2-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="214f2-151">Ela deve ser a imagem toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="214f2-151">It should look similar toothis image.</span></span>

![Página de informações de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="214f2-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="214f2-153">Next steps</span></span>

<span data-ttu-id="214f2-154">Neste tutorial, você implantou um servidor LEMP no Azure.</span><span class="sxs-lookup"><span data-stu-id="214f2-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="214f2-155">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="214f2-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="214f2-156">Criar uma VM do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="214f2-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="214f2-157">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="214f2-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="214f2-158">Instalar NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="214f2-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="214f2-159">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="214f2-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="214f2-160">Instalar o WordPress na pilha LEMP Olá</span><span class="sxs-lookup"><span data-stu-id="214f2-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="214f2-161">Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="214f2-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="214f2-162">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="214f2-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
