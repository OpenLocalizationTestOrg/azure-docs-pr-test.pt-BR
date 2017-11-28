---
title: Aplicativo web de Django em uma VM do Azure do Windows Server | Microsoft Docs
description: "Este tutorial ensina como hospedar um site da web baseado em Django no Azure usando uma VM do Windows Server 2012 R2 Datacenter com o modelo clássico de implantação."
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="86e13-103">Aplicativo web Django Olá, Mundo em uma VM do Windows Server</span><span class="sxs-lookup"><span data-stu-id="86e13-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="86e13-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e o modelo de implantação clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="86e13-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="86e13-105">Este artigo descreve o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="86e13-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="86e13-106">Recomendamos que a maioria das novas implantações use o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86e13-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="86e13-107">Este tutorial mostra como hospedar um site baseado em Django no Windows Server em Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="86e13-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="86e13-108">No tutorial, supomos que não há nenhuma experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="86e13-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="86e13-109">Quando concluir o tutorial, você pode ter um aplicativo baseado em Django funcionando na nuvem.</span><span class="sxs-lookup"><span data-stu-id="86e13-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="86e13-110">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="86e13-110">Learn how to:</span></span>

* <span data-ttu-id="86e13-111">Configure uma máquina virtual Azure para hospedar o Django.</span><span class="sxs-lookup"><span data-stu-id="86e13-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="86e13-112">Embora este tutorial explique como fazer isso para **Windows Server**, você pode fazer o mesmo para uma VM do Linux hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="86e13-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="86e13-113">Criar um novo aplicativo Django no Windows.</span><span class="sxs-lookup"><span data-stu-id="86e13-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="86e13-114">O tutorial mostra como criar um aplicativo Web Olá, Mundo básico.</span><span class="sxs-lookup"><span data-stu-id="86e13-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="86e13-115">O aplicativo é hospedado em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="86e13-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="86e13-116">A captura de tela a seguir mostra o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="86e13-116">The following screenshot shows the completed application:</span></span>

![Uma janela do navegador exibe a página Olá, Mundo no Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="86e13-118">Criar e configurar uma máquina virtual do Azure para hospedar o Django</span><span class="sxs-lookup"><span data-stu-id="86e13-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="86e13-119">Para criar uma máquina virtual do Azure com a distribuição Windows Server 2012 R2, consulte [Criar uma máquina virtual que executa Windows no portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="86e13-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="86e13-120">Configure o Azure para direcionar o tráfego da porta 80 da web para a porta 80 na máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="86e13-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="86e13-121">No portal do Azure, vá para o painel e selecione sua máquina virtual recém-criada.</span><span class="sxs-lookup"><span data-stu-id="86e13-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="86e13-122">Clique em **Pontos de Extremidade** e depois em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86e13-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Adicionar um ponto de extremidade](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="86e13-124">Na página **Adicionar ponto de extremidade**, para **Nome**, digite **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="86e13-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="86e13-125">Defina as portas TCP pública e privada para **80**.</span><span class="sxs-lookup"><span data-stu-id="86e13-125">Set the public and private TCP ports to **80**.</span></span>

     ![Insira o nome e defina as portas pública e privada](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="86e13-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="86e13-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="86e13-128">No painel, selecione a sua VM.</span><span class="sxs-lookup"><span data-stu-id="86e13-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="86e13-129">Para usar o Protocolo da Área de Trabalho Remota (RDP) para fazer logon remotamente na máquina virtual recém-criada do Azure, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="86e13-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="86e13-130">As instruções a seguir pressupõem que você conectou-se à máquina virtual corretamente.</span><span class="sxs-lookup"><span data-stu-id="86e13-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="86e13-131">Elas também supõem que você esteja emitindo comandos na máquina virtual e não no computador local.</span><span class="sxs-lookup"><span data-stu-id="86e13-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="86e13-132"><a id="setup"> </a>Instalar Python, Django e WFastCGI</span><span class="sxs-lookup"><span data-stu-id="86e13-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="86e13-133">Para baixar usando o Internet Explorer, talvez você precise configurar as definições de **Configuração de Segurança Aprimorada** do Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="86e13-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="86e13-134">Para fazer isso, clique em **Iniciar** > **Ferramentas Administrativas** > **Gerenciador do Servidor** > **Servidor Local**.</span><span class="sxs-lookup"><span data-stu-id="86e13-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="86e13-135">Clique em **Configuração de Segurança Aprimorada do IE**e, em seguida, selecione **Desativada**.</span><span class="sxs-lookup"><span data-stu-id="86e13-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="86e13-136">Instalar as versões mais recentes do Python 2.7 ou Python 3.4 a partir do [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="86e13-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="86e13-137">Instale os pacotes wfastcgi e django usando pip.</span><span class="sxs-lookup"><span data-stu-id="86e13-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="86e13-138">No Python 2.7, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e13-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="86e13-139">No Python 3.4, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e13-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="86e13-140">Instale o IIS com o FastCGI</span><span class="sxs-lookup"><span data-stu-id="86e13-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="86e13-141">Instale os Serviços de Informações da Internet (IIS) com suporte do FastCGI.</span><span class="sxs-lookup"><span data-stu-id="86e13-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="86e13-142">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="86e13-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="86e13-143">Criar um novo aplicativo Django</span><span class="sxs-lookup"><span data-stu-id="86e13-143">Create a new Django application</span></span>
1. <span data-ttu-id="86e13-144">Em C:\inetpub\wwwroot, digite o seguinte comando para criar um novo projeto de Django:</span><span class="sxs-lookup"><span data-stu-id="86e13-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="86e13-145">No Python 2.7, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e13-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="86e13-146">No Python 3.4, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="86e13-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![O resultado do comando New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="86e13-148">O comando `django-admin` gera uma estrutura básica para sites da web baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="86e13-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="86e13-149">`helloworld\manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="86e13-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="86e13-150">`helloworld\helloworld\settings.py` tem configurações do Django para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86e13-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="86e13-151">`helloworld\helloworld\urls.py` tem o código de mapeamento entre cada URL e sua exibição.</span><span class="sxs-lookup"><span data-stu-id="86e13-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="86e13-152">No diretório C:\inetpub\wwwroot\helloworld\helloworld, crie um novo arquivo chamado views.py.</span><span class="sxs-lookup"><span data-stu-id="86e13-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="86e13-153">Esse arquivo contém a exibição que renderiza a página “Olá, Mundo”.</span><span class="sxs-lookup"><span data-stu-id="86e13-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="86e13-154">Em seu editor de código, digite os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="86e13-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="86e13-155">Substitua o conteúdo do arquivo urls.py pelos seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="86e13-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="86e13-156">Configurar IIS</span><span class="sxs-lookup"><span data-stu-id="86e13-156">Set up IIS</span></span>
1. <span data-ttu-id="86e13-157">Desbloqueie a seção de manipuladores no arquivo applicationhost.config global.</span><span class="sxs-lookup"><span data-stu-id="86e13-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="86e13-158">Isso permite que o arquivo web.config use o manipulador de Python.</span><span class="sxs-lookup"><span data-stu-id="86e13-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="86e13-159">Adicione este comando:</span><span class="sxs-lookup"><span data-stu-id="86e13-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="86e13-160">Ative o WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="86e13-160">Activate WFastCGI.</span></span> <span data-ttu-id="86e13-161">Isso adiciona um aplicativo ao applicationhost.config global que se refere ao seu interpretador de Python executável e ao script wfastcgi.py.</span><span class="sxs-lookup"><span data-stu-id="86e13-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="86e13-162">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="86e13-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="86e13-163">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="86e13-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="86e13-164">Crie um arquivo web.config em C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="86e13-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="86e13-165">O valor do atributo `scriptProcessor` deve corresponder à saída da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="86e13-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="86e13-166">Para obter mais informações sobre a configuração de wfastcgi, consulte [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="86e13-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="86e13-167">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="86e13-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="86e13-168">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="86e13-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="86e13-169">Atualize o local do site da Web padrão IIS para apontar para a pasta do projeto Django:</span><span class="sxs-lookup"><span data-stu-id="86e13-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="86e13-170">Carregue a página da Web no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="86e13-170">Load the webpage in your browser.</span></span>

![Uma janela do navegador exibe a página Olá, Mundo no Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="86e13-172">Desligar a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="86e13-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="86e13-173">Quando você concluir este tutorial, é recomendável desligar ou remover a VM do Azure que você criou para o tutorial.</span><span class="sxs-lookup"><span data-stu-id="86e13-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="86e13-174">Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.</span><span class="sxs-lookup"><span data-stu-id="86e13-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
