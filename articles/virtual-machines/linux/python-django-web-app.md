---
title: Aplicativo Web Python com Django em uma VM Linux do Azure | Microsoft Docs
description: Saiba como hospedar um aplicativo Web baseado em Django no Azure usando uma VM Linux.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="5f0a1-103">Aplicativo Web Django Olá, Mundo em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="5f0a1-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f0a1-104">Windows</span><span class="sxs-lookup"><span data-stu-id="5f0a1-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="5f0a1-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5f0a1-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="5f0a1-106">Este tutorial mostra como hospedar um site baseado em Django no Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="5f0a1-107">No tutorial, supomos que não há nenhuma experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="5f0a1-108">Quando concluir o tutorial, você pode ter um aplicativo baseado em Django funcionando na nuvem.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="5f0a1-109">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-109">Learn how to:</span></span>

* <span data-ttu-id="5f0a1-110">Configure uma máquina virtual Azure para hospedar o Django.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="5f0a1-111">Embora este tutorial explique como fazer isso para **Linux**, você pode fazer o mesmo para uma VM do Windows Server hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="5f0a1-112">Crie um novo aplicativo Django do Linux.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="5f0a1-113">O tutorial mostra como criar um aplicativo Web Olá, Mundo básico.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="5f0a1-114">O aplicativo é hospedado em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="5f0a1-115">A captura de tela a seguir mostra o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-115">The following screenshot shows the completed application:</span></span>

![Uma janela do navegador exibe a página Olá, Mundo no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="5f0a1-117">Criar e configurar uma máquina virtual do Azure para hospedar o Django</span><span class="sxs-lookup"><span data-stu-id="5f0a1-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="5f0a1-118">Para criar uma máquina virtual do Azure com a distribuição Ubuntu Server 14.04 LTS, consulte [Criar uma máquina virtual Linux no Portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5f0a1-119">Você também pode escolher a autenticação de senha em vez de usar uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="5f0a1-120">Para editar o grupo de segurança de rede para permitir o tráfego HTTP de entrada para a porta 80, consulte [Criar grupos de segurança de rede no Portal do Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="5f0a1-121">(Opcional) Por padrão, a nova máquina virtual não tem um FQDN (nome de domínio totalmente qualificado).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="5f0a1-122">Para criar uma VM com um FQDN, consulte [Criar um FQDN no Portal do Azure para uma VM Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5f0a1-123">Esta etapa não é necessária para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="5f0a1-124"><a id="setup"> </a>Configurar o ambiente de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="5f0a1-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="5f0a1-125">Se precisar instalar o Python ou se quiser usar as bibliotecas do cliente, confira o [Guia de instalação do Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="5f0a1-126">A VM Ubuntu Linux tem o Python 2.7 pré-instalado, mas ele não vem com o Apache ou o Django.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="5f0a1-127">Conclua as etapas a seguir para se conectar à sua VM e instalar o Apache e o Django:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="5f0a1-128">Abra uma nova janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="5f0a1-129">Para se conectar à VM do Azure, insira o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="5f0a1-130">Se não tiver criado um FQDN, poderá se conectar usando o endereço IP público exibido no resumo da máquina virtual no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="5f0a1-131">Para instalar o Django, digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="5f0a1-132">Para instalar o Apache com mod-wsgi, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="5f0a1-133">Criar um novo aplicativo Django</span><span class="sxs-lookup"><span data-stu-id="5f0a1-133">Create a new Django app</span></span>
1. <span data-ttu-id="5f0a1-134">Para usar o SSH para acessar sua VM, abra a janela do terminal usada na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="5f0a1-135">Para criar um novo projeto de Django, insira os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="5f0a1-136">O script `django-admin.py` gera uma estrutura básica para sites da web baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="5f0a1-137">`helloworld/manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="5f0a1-138">`helloworld/helloworld/settings.py` tem configurações do Django para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="5f0a1-139">`helloworld/helloworld/urls.py` tem o código de mapeamento entre cada URL e sua exibição.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="5f0a1-140">No diretório /var/www/helloworld/helloworld, crie um novo arquivo chamado views.py.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="5f0a1-141">Esse arquivo contém a exibição que renderiza a página “Olá, Mundo”.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="5f0a1-142">Em seu editor de código, digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="5f0a1-143">Substitua o conteúdo do arquivo urls.py com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="5f0a1-144">Configurar o Apache</span><span class="sxs-lookup"><span data-stu-id="5f0a1-144">Set up Apache</span></span>
1. <span data-ttu-id="5f0a1-145">Na pasta /etc/apache2/sites-available/helloworld.conf, crie um arquivo de configuração do host virtual Apache.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="5f0a1-146">Defina o conteúdo para os seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-146">Set the contents to the following values.</span></span> <span data-ttu-id="5f0a1-147">Substitua *yourVmName* pelo nome real do computador que você está usando (por exemplo *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="5f0a1-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="5f0a1-148">Para ativar o site, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="5f0a1-149">Para reiniciar o Apache, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="5f0a1-150">Carregue a página da Web no seu navegador:</span><span class="sxs-lookup"><span data-stu-id="5f0a1-150">Load the webpage in your browser:</span></span>
   
   ![Uma janela do navegador exibe a página Olá, Mundo no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="5f0a1-152">Desligar a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5f0a1-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="5f0a1-153">Quando você concluir este tutorial, é recomendável desligar ou remover a VM do Azure que você criou para o tutorial.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="5f0a1-154">Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f0a1-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

