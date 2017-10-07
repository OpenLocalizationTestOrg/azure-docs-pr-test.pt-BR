---
title: "aaaDeploy LÂMPADA em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial - pilha de LÂMPADA Olá instalar em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="e9fdf-103">Instalar um servidor Web LAMP em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="e9fdf-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="e9fdf-104">Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) em uma VM Ubuntu no Azure.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="e9fdf-105">Se preferir que o servidor de web NGINX hello, consulte Olá [pilha LEMP](tutorial-lemp-stack.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="e9fdf-106">servidor de LÂMPADA Olá toosee em ação, opcionalmente, você pode instalar e configurar um site de WordPress.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="e9fdf-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e9fdf-108">Criar uma VM Ubuntu (Olá 'L' na pilha de LÂMPADA Olá)</span><span class="sxs-lookup"><span data-stu-id="e9fdf-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="e9fdf-109">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="e9fdf-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e9fdf-110">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="e9fdf-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="e9fdf-111">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="e9fdf-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="e9fdf-112">Instalar o WordPress no servidor de LÂMPADA Olá</span><span class="sxs-lookup"><span data-stu-id="e9fdf-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="e9fdf-113">Para obter mais informações sobre a pilha de LÂMPADA hello, incluindo recomendações para um ambiente de produção, consulte Olá [Ubuntu documentação](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="e9fdf-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e9fdf-114">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e9fdf-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e9fdf-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e9fdf-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="e9fdf-117">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="e9fdf-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="e9fdf-118">Execute Olá comando tooupdate Ubuntu pacote origens a seguir e instalar o PHP, MySQL e Apache.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="e9fdf-119">Observe o circunflexo (^) do hello no final de saudação do comando hello.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="e9fdf-120">Você está tooinstall solicitadas Olá pacotes e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="e9fdf-121">Quando solicitado, defina uma senha de raiz para o MySQL e toocontinue [Enter].</span><span class="sxs-lookup"><span data-stu-id="e9fdf-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="e9fdf-122">Siga Olá restantes prompts.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="e9fdf-123">Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="e9fdf-125">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="e9fdf-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="e9fdf-126">Apache</span><span class="sxs-lookup"><span data-stu-id="e9fdf-126">Apache</span></span>

<span data-ttu-id="e9fdf-127">Verifique a versão de saudação do Apache com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="e9fdf-128">Com o Apache instalado e a porta 80 abra tooyour VM, servidor de web hello agora pode ser acessado de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="e9fdf-129">Olá tooview do Apache2 Ubuntu padrão página, abra um navegador da web e digite o endereço IP público de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="e9fdf-130">Use o endereço IP público Olá usado tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Página padrão do Apache][3]


### <a name="mysql"></a><span data-ttu-id="e9fdf-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="e9fdf-132">MySQL</span></span>

<span data-ttu-id="e9fdf-133">Verificar a versão de saudação do MySQL com o comando a seguir de saudação (Observe maiuscula Olá `V` parâmetro):</span><span class="sxs-lookup"><span data-stu-id="e9fdf-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="e9fdf-134">É recomendável executar Olá após a instalação do script toohelp Olá segura do MySQL:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="e9fdf-135">Digite sua senha de raiz de MySQL e definir configurações de segurança Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="e9fdf-136">Se você quiser toocreate um banco de dados MySQL, adicionar usuários ou alterar definições de configuração, tooMySQL de logon:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e9fdf-137">Quando terminar, saia Olá mysql prompt digitando `\q`.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="e9fdf-138">PHP</span><span class="sxs-lookup"><span data-stu-id="e9fdf-138">PHP</span></span>

<span data-ttu-id="e9fdf-139">Verifique a versão de saudação do PHP com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="e9fdf-140">Se você quiser mais tootest, crie um tooview de página de informações rápida do PHP em um navegador.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="e9fdf-141">Olá comando a seguir cria uma página de informações do PHP hello:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="e9fdf-142">Agora você pode verificar a página de informações do PHP Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="e9fdf-143">Abra um navegador e vá muito`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="e9fdf-144">Substitua o endereço IP público de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="e9fdf-145">Ela deve ser a imagem toothis semelhante.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-145">It should look similar toothis image.</span></span>

![Página de informações de PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="e9fdf-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9fdf-147">Next steps</span></span>

<span data-ttu-id="e9fdf-148">Neste tutorial, você implantou um servidor LAMP no Azure.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="e9fdf-149">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="e9fdf-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e9fdf-150">Criar uma VM do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e9fdf-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="e9fdf-151">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="e9fdf-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e9fdf-152">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="e9fdf-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="e9fdf-153">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="e9fdf-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="e9fdf-154">Instalar o WordPress no servidor de LÂMPADA Olá</span><span class="sxs-lookup"><span data-stu-id="e9fdf-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="e9fdf-155">Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="e9fdf-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9fdf-156">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="e9fdf-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png