---
title: aplicativo web de aaaPython com Django em uma VM do Linux do Azure | Microsoft Docs
description: Saiba como toohost um baseado em Django web aplicativo no Azure usando uma VM do Linux.
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
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="b04c4-103">Aplicativo Web Django Olá, Mundo em uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="b04c4-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b04c4-104">Windows</span><span class="sxs-lookup"><span data-stu-id="b04c4-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="b04c4-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="b04c4-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="b04c4-106">Este tutorial mostra como toohost um site baseado em Django no Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="b04c4-107">Tutorial de Olá, vamos supor sem experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="b04c4-108">Quando você concluir o tutorial Olá, você pode ter um aplicativo baseado em Django para cima e em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="b04c4-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="b04c4-109">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="b04c4-109">Learn how to:</span></span>

* <span data-ttu-id="b04c4-110">Configure uma máquina virtual do Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="b04c4-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="b04c4-111">Embora este tutorial explica como toodo para **Linux**, você pode fazer hello mesmo para uma VM do Windows Server hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="b04c4-112">Crie um novo aplicativo Django do Linux.</span><span class="sxs-lookup"><span data-stu-id="b04c4-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="b04c4-113">tutorial de saudação mostra como toobuild um Hello World básicas de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b04c4-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="b04c4-114">aplicativo Hello é hospedado em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="b04c4-115">Olá captura de tela a seguir mostra um aplicativo hello concluída:</span><span class="sxs-lookup"><span data-stu-id="b04c4-115">hello following screenshot shows hello completed application:</span></span>

![Uma janela do navegador exibe a página do Olá Olá, mundo no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="b04c4-117">Criar e configurar uma máquina virtual do Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="b04c4-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="b04c4-118">toocreate uma máquina virtual do Azure com hello distribuição Ubuntu Server 14.04 LTS, consulte [criar uma máquina virtual Linux no portal do Azure de saudação](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b04c4-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b04c4-119">Você também pode escolher a autenticação de senha em vez de usar uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="b04c4-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="b04c4-120">tooedit Olá rede segurança grupo tooallow entrada HTTP tráfego tooport 80, consulte [criar grupos de segurança de rede no portal do Azure de saudação](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="b04c4-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="b04c4-121">(Opcional) Por padrão, a nova máquina virtual não tem um FQDN (nome de domínio totalmente qualificado).</span><span class="sxs-lookup"><span data-stu-id="b04c4-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="b04c4-122">toocreate uma VM com um FQDN, consulte [criar um FQDN no hello portal do Azure para uma VM do Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b04c4-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b04c4-123">Esta etapa não é necessária para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b04c4-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="b04c4-124"><a id="setup"></a>Configurar o ambiente de desenvolvimento Olá</span><span class="sxs-lookup"><span data-stu-id="b04c4-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="b04c4-125">Se você precisa tooinstall Python ou bibliotecas de cliente toouse Olá, consulte Olá [guia de instalação do Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="b04c4-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="b04c4-126">Olá Ubuntu Linux VM tem Python 2.7 pré-instalado, mas ela não vem com o Apache ou Django.</span><span class="sxs-lookup"><span data-stu-id="b04c4-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="b04c4-127">Completar Olá seguindo as etapas tooconnect tooyour VM e instalar o Apache e Django:</span><span class="sxs-lookup"><span data-stu-id="b04c4-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="b04c4-128">Abra uma nova janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="b04c4-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="b04c4-129">tooconnect toohello VM do Azure, digite Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b04c4-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="b04c4-130">Se você não criar um FQDN, você pode se conectar usando o endereço IP público Olá que é exibido na máquina virtual de saudação resumida Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="b04c4-131">tooinstall Django, digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="b04c4-132">tooinstall Apache com mod-wsgi, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="b04c4-133">Criar um novo aplicativo Django</span><span class="sxs-lookup"><span data-stu-id="b04c4-133">Create a new Django app</span></span>
1. <span data-ttu-id="b04c4-134">toouse tooaccess SSH sua VM, a janela do Terminal Olá abrir usado na saudação anterior de seção.</span><span class="sxs-lookup"><span data-stu-id="b04c4-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="b04c4-135">toocreate um novo projeto de Django, digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="b04c4-136">Olá `django-admin.py` script gera uma estrutura básica para sites baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="b04c4-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="b04c4-137">`helloworld/manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="b04c4-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="b04c4-138">`helloworld/helloworld/settings.py` tem configurações do Django para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b04c4-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="b04c4-139">`helloworld/helloworld/urls.py`tiver um código de mapeamento de saudação entre cada URL e sua exibição.</span><span class="sxs-lookup"><span data-stu-id="b04c4-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="b04c4-140">No diretório de /var/www/helloworld/helloworld hello, crie um novo arquivo denominado views.py.</span><span class="sxs-lookup"><span data-stu-id="b04c4-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="b04c4-141">Este arquivo tem o modo de exibição de saudação que renderiza a página de "hello world" hello.</span><span class="sxs-lookup"><span data-stu-id="b04c4-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="b04c4-142">Em seu editor de código, digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="b04c4-143">Substitua o conteúdo de saudação do arquivo de urls.py de saudação com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="b04c4-144">Configurar o Apache</span><span class="sxs-lookup"><span data-stu-id="b04c4-144">Set up Apache</span></span>
1. <span data-ttu-id="b04c4-145">Na pasta de /etc/apache2/sites-available/helloworld.conf hello, crie um arquivo de configuração de host virtual Apache.</span><span class="sxs-lookup"><span data-stu-id="b04c4-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="b04c4-146">Definir Olá conteúdo toohello valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="b04c4-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="b04c4-147">Substituir *Nomedasuavm* com nome real de saudação do máquina Olá que você está usando (por exemplo, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="b04c4-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="b04c4-148">site de saudação tooactivate, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="b04c4-149">toorestart Apache, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04c4-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="b04c4-150">Carregar Olá página da Web no navegador:</span><span class="sxs-lookup"><span data-stu-id="b04c4-150">Load hello webpage in your browser:</span></span>
   
   ![Uma janela do navegador exibirá a página do hello hello world no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="b04c4-152">Desligar a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b04c4-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="b04c4-153">Quando você concluir este tutorial, é recomendável desligar ou remover Olá VM do Azure que você criou para o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="b04c4-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="b04c4-154">Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04c4-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

