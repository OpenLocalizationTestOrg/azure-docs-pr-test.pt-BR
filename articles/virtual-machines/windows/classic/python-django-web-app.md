---
title: aplicativo web de aaaDjango em uma VM do Azure do Windows Server | Microsoft Docs
description: "Saiba como toohost um site baseado em Django no Azure usando uma VM do Windows Server 2012 R2 Datacenter com o modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="481ea-103">Aplicativo web Django Olá, Mundo em uma VM do Windows Server</span><span class="sxs-lookup"><span data-stu-id="481ea-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="481ea-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [modelo de implantação clássico do Azure Resource Manager e hello](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="481ea-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="481ea-105">Este artigo descreve o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="481ea-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="481ea-106">É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="481ea-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="481ea-107">Este tutorial mostra como toohost um site baseado em Django no Windows Server em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="481ea-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="481ea-108">Tutorial de Olá, vamos supor sem experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="481ea-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="481ea-109">Quando você concluir o tutorial Olá, você pode ter um aplicativo baseado em Django para cima e em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="481ea-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="481ea-110">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="481ea-110">Learn how to:</span></span>

* <span data-ttu-id="481ea-111">Configure uma máquina virtual do Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="481ea-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="481ea-112">Embora este tutorial explica como toodo para **Windows Server**, você pode fazer Olá mesmo para uma VM do Linux hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="481ea-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="481ea-113">Criar um novo aplicativo Django no Windows.</span><span class="sxs-lookup"><span data-stu-id="481ea-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="481ea-114">tutorial de saudação mostra como toobuild um Hello World básicas de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="481ea-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="481ea-115">aplicativo Hello é hospedado em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="481ea-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="481ea-116">Olá captura de tela a seguir mostra um aplicativo hello concluída:</span><span class="sxs-lookup"><span data-stu-id="481ea-116">hello following screenshot shows hello completed application:</span></span>

![Uma janela do navegador exibirá a página do hello hello world no Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="481ea-118">Criar e configurar uma máquina virtual do Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="481ea-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="481ea-119">toocreate uma máquina virtual do Azure com hello distribuição do Windows Server 2012 R2 Datacenter, consulte [criar uma máquina virtual executando o Windows hello portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="481ea-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="481ea-120">Defina o tráfego da porta 80 do Azure toodirect de Olá web tooport 80 na máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="481ea-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="481ea-121">No hello portal do Azure, vá toohello painel e selecione sua máquina virtual recém-criada.</span><span class="sxs-lookup"><span data-stu-id="481ea-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="481ea-122">Clique em **Pontos de Extremidade** e depois em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="481ea-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Adicionar um ponto de extremidade](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="481ea-124">Em Olá **Adicionar ponto de extremidade** página, para **nome**, digite **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="481ea-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="481ea-125">Definir as portas TCP públicas e privadas Olá muito**80**.</span><span class="sxs-lookup"><span data-stu-id="481ea-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Insira o nome e defina as portas pública e privada](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="481ea-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="481ea-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="481ea-128">No painel de Olá, selecione sua VM.</span><span class="sxs-lookup"><span data-stu-id="481ea-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="481ea-129">toouse protocolo de área de trabalho remota (RDP) tooremotely entrar toohello criado recentemente a máquina virtual do Azure, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="481ea-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="481ea-130">Olá instruções a seguir pressupõem que você conectado na máquina virtual de toohello corretamente.</span><span class="sxs-lookup"><span data-stu-id="481ea-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="481ea-131">Eles também supõem que você esteja emitindo comandos na máquina virtual de saudação e não no computador local.</span><span class="sxs-lookup"><span data-stu-id="481ea-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="481ea-132"><a id="setup"> </a>Instalar Python, Django e WFastCGI</span><span class="sxs-lookup"><span data-stu-id="481ea-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="481ea-133">toodownload usando o Internet Explorer, você pode ter tooconfigure Internet Explorer **configuração de segurança reforçada** configurações.</span><span class="sxs-lookup"><span data-stu-id="481ea-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="481ea-134">toodo, clique **iniciar** > **ferramentas administrativas** > **Gerenciador do servidor** > **doservidorLocal**.</span><span class="sxs-lookup"><span data-stu-id="481ea-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="481ea-135">Clique em **Configuração de Segurança Aprimorada do IE**e, em seguida, selecione **Desativada**.</span><span class="sxs-lookup"><span data-stu-id="481ea-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="481ea-136">Instalar versões mais recentes de saudação do Python 2.7 ou Python 3.4 do [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="481ea-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="481ea-137">Instale pacotes wfastcgi e django hello usando pip.</span><span class="sxs-lookup"><span data-stu-id="481ea-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="481ea-138">Para Python 2.7, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="481ea-139">Para Python 3.4, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="481ea-140">Instale o IIS com o FastCGI</span><span class="sxs-lookup"><span data-stu-id="481ea-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="481ea-141">Instale os Serviços de Informações da Internet (IIS) com suporte do FastCGI.</span><span class="sxs-lookup"><span data-stu-id="481ea-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="481ea-142">Isso pode levar vários tooexecute de minutos.</span><span class="sxs-lookup"><span data-stu-id="481ea-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="481ea-143">Criar um novo aplicativo Django</span><span class="sxs-lookup"><span data-stu-id="481ea-143">Create a new Django application</span></span>
1. <span data-ttu-id="481ea-144">Em C:\inetpub\wwwroot, toocreate um novo projeto de Django, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="481ea-145">Para Python 2.7, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="481ea-146">Para Python 3.4, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de saudação do comando de saudação New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="481ea-148">Olá `django-admin` comando gera uma estrutura básica para sites baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="481ea-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="481ea-149">`helloworld\manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="481ea-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="481ea-150">`helloworld\helloworld\settings.py` tem configurações do Django para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="481ea-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="481ea-151">`helloworld\helloworld\urls.py`tiver um código de mapeamento de saudação entre cada URL e sua exibição.</span><span class="sxs-lookup"><span data-stu-id="481ea-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="481ea-152">No diretório de C:\inetpub\wwwroot\helloworld\helloworld hello, crie um novo arquivo denominado views.py.</span><span class="sxs-lookup"><span data-stu-id="481ea-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="481ea-153">Este arquivo tem o modo de exibição de saudação que renderiza a página de "hello world" hello.</span><span class="sxs-lookup"><span data-stu-id="481ea-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="481ea-154">Em seu editor de código, digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="481ea-155">Substitua o conteúdo de saudação do arquivo de urls.py de saudação com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="481ea-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="481ea-156">Configurar IIS</span><span class="sxs-lookup"><span data-stu-id="481ea-156">Set up IIS</span></span>
1. <span data-ttu-id="481ea-157">No arquivo de applicationHost. config global hello, desbloqueie a seção de manipuladores de saudação.</span><span class="sxs-lookup"><span data-stu-id="481ea-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="481ea-158">Isso permite que o manipulador de Python de saudação do Web. config arquivo toouse.</span><span class="sxs-lookup"><span data-stu-id="481ea-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="481ea-159">Adicione este comando:</span><span class="sxs-lookup"><span data-stu-id="481ea-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="481ea-160">Ative o WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="481ea-160">Activate WFastCGI.</span></span> <span data-ttu-id="481ea-161">Isso adiciona um aplicativo toohello global arquivo applicationHost config, que se refere a tooyour interpretador executável e hello wfastcgi.py script Python.</span><span class="sxs-lookup"><span data-stu-id="481ea-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="481ea-162">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="481ea-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="481ea-163">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="481ea-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="481ea-164">Crie um arquivo web.config em C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="481ea-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="481ea-165">Olá valor Olá `scriptProcessor` atributo deve corresponder a saída de saudação do hello anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="481ea-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="481ea-166">Para obter mais informações sobre a configuração de wfastcgi hello, consulte [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="481ea-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="481ea-167">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="481ea-167">In  Python 2.7:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   <span data-ttu-id="481ea-168">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="481ea-168">In  Python 3.4:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. <span data-ttu-id="481ea-169">Atualize o local de Olá Olá IIS padrão site toopoint toohello Django da pasta de projeto:</span><span class="sxs-lookup"><span data-stu-id="481ea-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="481ea-170">Carregar Olá página da Web no navegador.</span><span class="sxs-lookup"><span data-stu-id="481ea-170">Load hello webpage in your browser.</span></span>

![Uma janela do navegador exibirá a página do hello hello world no Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="481ea-172">Desligar a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="481ea-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="481ea-173">Quando você concluir este tutorial, é recomendável desligar ou remover Olá VM do Azure que você criou para o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="481ea-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="481ea-174">Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.</span><span class="sxs-lookup"><span data-stu-id="481ea-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
