---
title: "Implantar LAMP em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial – instalar a pilha LAMP em uma VM do Linux no Azure"
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
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="cf139-103">Instalar um servidor Web LAMP em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="cf139-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="cf139-104">Este artigo explica como implantar um servidor Web Apache, MySQL e PHP (a pilha LAMP) em uma VM do Ubuntu no Azure.</span><span class="sxs-lookup"><span data-stu-id="cf139-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="cf139-105">Se você prefere o servidor Web NGINX, consulte o tutorial da [Pilha LEMP](tutorial-lemp-stack.md).</span><span class="sxs-lookup"><span data-stu-id="cf139-105">If you prefer the NGINX web server, see the [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="cf139-106">Para ver o servidor LAMP em ação, opcionalmente, você pode instalar e configurar um site de WordPress.</span><span class="sxs-lookup"><span data-stu-id="cf139-106">To see the LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="cf139-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cf139-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf139-108">Criar uma VM Ubuntu (o "L" na pilha de LAMP)</span><span class="sxs-lookup"><span data-stu-id="cf139-108">Create an Ubuntu VM (the 'L' in the LAMP stack)</span></span>
> * <span data-ttu-id="cf139-109">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="cf139-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="cf139-110">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="cf139-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="cf139-111">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="cf139-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="cf139-112">Instalar o WordPress no servidor LAMP</span><span class="sxs-lookup"><span data-stu-id="cf139-112">Install WordPress on the LAMP server</span></span>


<span data-ttu-id="cf139-113">Para saber mais sobre a pilha LAMP, incluindo recomendações para um ambiente de produção, consulte a [Documentação do Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="cf139-113">For more on the LAMP stack, including recommendations for a production environment, see the [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cf139-114">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="cf139-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cf139-115">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="cf139-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="cf139-116">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cf139-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="cf139-117">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="cf139-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="cf139-118">Execute o seguinte comando para atualizar as fontes de pacote do Ubuntu e instalar o Apache, o MySQL e o PHP.</span><span class="sxs-lookup"><span data-stu-id="cf139-118">Run the following command to update Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="cf139-119">Observe o acento circunflexo (^) no final do comando.</span><span class="sxs-lookup"><span data-stu-id="cf139-119">Note the caret (^) at the end of the command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="cf139-120">Você será solicitado a instalar os pacotes e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="cf139-120">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="cf139-121">Quando solicitado, defina uma senha raiz para o MySQL e, em seguida, pressione [Enter] para continuar.</span><span class="sxs-lookup"><span data-stu-id="cf139-121">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="cf139-122">Avance pelas solicitações restantes.</span><span class="sxs-lookup"><span data-stu-id="cf139-122">Follow the remaining prompts.</span></span> <span data-ttu-id="cf139-123">Esse processo instala as extensões PHP mínimas obrigatórias e necessárias para usar o PHP com o MySQL.</span><span class="sxs-lookup"><span data-stu-id="cf139-123">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="cf139-125">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="cf139-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="cf139-126">Apache</span><span class="sxs-lookup"><span data-stu-id="cf139-126">Apache</span></span>

<span data-ttu-id="cf139-127">Verifique a versão do Apache com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cf139-127">Check the version of Apache with the following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="cf139-128">Com o Apache instalado e a porta 80 aberta para a sua VM, o servidor Web agora pode ser acessado por meio da Internet.</span><span class="sxs-lookup"><span data-stu-id="cf139-128">With Apache installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="cf139-129">Para exibir a página padrão do Apache2 Ubuntu, abra um navegador da Web e digite o endereço IP público da VM.</span><span class="sxs-lookup"><span data-stu-id="cf139-129">To view the Apache2 Ubuntu Default Page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="cf139-130">Insira o endereço IP público que você usou para o SSH para a VM:</span><span class="sxs-lookup"><span data-stu-id="cf139-130">Use the public IP address you used to SSH to the VM:</span></span>

![Página padrão do Apache][3]


### <a name="mysql"></a><span data-ttu-id="cf139-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="cf139-132">MySQL</span></span>

<span data-ttu-id="cf139-133">Verifique a versão do MySQL com o seguinte comando (observe o parâmetro `V` em letra maiúscula):</span><span class="sxs-lookup"><span data-stu-id="cf139-133">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="cf139-134">É recomendável executar o seguinte script para ajudar a proteger a instalação do MySQL:</span><span class="sxs-lookup"><span data-stu-id="cf139-134">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="cf139-135">Digite a senha raiz do MySQL e defina as configurações de segurança do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cf139-135">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="cf139-136">Se você deseja criar um banco de dados MySQL, adicionar usuários ou alterar definições de configuração, faça logon no MySQL:</span><span class="sxs-lookup"><span data-stu-id="cf139-136">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="cf139-137">Quando terminar, saia do prompt do MySQL digitando `\q`.</span><span class="sxs-lookup"><span data-stu-id="cf139-137">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="cf139-138">PHP</span><span class="sxs-lookup"><span data-stu-id="cf139-138">PHP</span></span>

<span data-ttu-id="cf139-139">Verifique a versão do PHP com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cf139-139">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="cf139-140">Se você deseja realizar mais testes, crie uma página de informações rápida de PHP para exibição em um navegador.</span><span class="sxs-lookup"><span data-stu-id="cf139-140">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="cf139-141">O comando a seguir cria a página de informações de PHP:</span><span class="sxs-lookup"><span data-stu-id="cf139-141">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="cf139-142">Agora você pode verificar a página de informações de PHP que você criou.</span><span class="sxs-lookup"><span data-stu-id="cf139-142">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="cf139-143">Abra um navegador e acesse `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="cf139-143">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="cf139-144">Substitua o endereço IP público de sua VM.</span><span class="sxs-lookup"><span data-stu-id="cf139-144">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="cf139-145">A página deve ser semelhante a esta imagem.</span><span class="sxs-lookup"><span data-stu-id="cf139-145">It should look similar to this image.</span></span>

![Página de informações de PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="cf139-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf139-147">Next steps</span></span>

<span data-ttu-id="cf139-148">Neste tutorial, você implantou um servidor LAMP no Azure.</span><span class="sxs-lookup"><span data-stu-id="cf139-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="cf139-149">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="cf139-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf139-150">Criar uma VM do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cf139-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="cf139-151">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="cf139-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="cf139-152">Instalar Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="cf139-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="cf139-153">Verificar a instalação e a configuração</span><span class="sxs-lookup"><span data-stu-id="cf139-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="cf139-154">Instalar o WordPress no servidor LAMP</span><span class="sxs-lookup"><span data-stu-id="cf139-154">Install WordPress on the LAMP server</span></span>

<span data-ttu-id="cf139-155">Vá para o próximo tutorial para saber como proteger servidores Web com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="cf139-155">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf139-156">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="cf139-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png