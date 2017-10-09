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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Aplicativo web Django Olá, Mundo em uma VM do Windows Server

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [modelo de implantação clássico do Azure Resource Manager e hello](../../../resource-manager-deployment-model.md). Este artigo descreve o modelo de implantação clássico hello. É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Este tutorial mostra como toohost um site baseado em Django no Windows Server em máquinas virtuais do Azure. Tutorial de Olá, vamos supor sem experiência anterior com o Azure. Quando você concluir o tutorial Olá, você pode ter um aplicativo baseado em Django para cima e em execução na nuvem hello.

Saiba como:

* Configure uma máquina virtual do Azure de toohost Django. Embora este tutorial explica como toodo para **Windows Server**, você pode fazer Olá mesmo para uma VM do Linux hospedado no Azure.
* Criar um novo aplicativo Django no Windows.

tutorial de saudação mostra como toobuild um Hello World básicas de aplicativo web. aplicativo Hello é hospedado em uma máquina virtual do Azure.

Olá captura de tela a seguir mostra um aplicativo hello concluída:

![Uma janela do navegador exibirá a página do hello hello world no Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Criar e configurar uma máquina virtual do Azure de toohost Django

1. toocreate uma máquina virtual do Azure com hello distribuição do Windows Server 2012 R2 Datacenter, consulte [criar uma máquina virtual executando o Windows hello portal do Azure](tutorial.md).
2. Defina o tráfego da porta 80 do Azure toodirect de Olá web tooport 80 na máquina virtual de saudação:
   
   1. No hello portal do Azure, vá toohello painel e selecione sua máquina virtual recém-criada.
   2. Clique em **Pontos de Extremidade** e depois em **Adicionar**.

     ![Adicionar um ponto de extremidade](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Em Olá **Adicionar ponto de extremidade** página, para **nome**, digite **HTTP**. Definir as portas TCP públicas e privadas Olá muito**80**.

     ![Insira o nome e defina as portas pública e privada](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Clique em **OK**.
     
3. No painel de Olá, selecione sua VM. toouse protocolo de área de trabalho remota (RDP) tooremotely entrar toohello criado recentemente a máquina virtual do Azure, clique em **conectar**.  

> [!IMPORTANT] 
> Olá instruções a seguir pressupõem que você conectado na máquina virtual de toohello corretamente. Eles também supõem que você esteja emitindo comandos na máquina virtual de saudação e não no computador local.

## <a id="setup"> </a>Instalar Python, Django e WFastCGI
> [!NOTE]
> toodownload usando o Internet Explorer, você pode ter tooconfigure Internet Explorer **configuração de segurança reforçada** configurações. toodo, clique **iniciar** > **ferramentas administrativas** > **Gerenciador do servidor** > **doservidorLocal**. Clique em **Configuração de Segurança Aprimorada do IE**e, em seguida, selecione **Desativada**.

1. Instalar versões mais recentes de saudação do Python 2.7 ou Python 3.4 do [python.org][python.org].
2. Instale pacotes wfastcgi e django hello usando pip.
   
    Para Python 2.7, use Olá comando a seguir:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Para Python 3.4, use Olá comando a seguir:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Instale o IIS com o FastCGI
* Instale os Serviços de Informações da Internet (IIS) com suporte do FastCGI. Isso pode levar vários tooexecute de minutos.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Criar um novo aplicativo Django
1. Em C:\inetpub\wwwroot, toocreate um novo projeto de Django, digite Olá comando a seguir:
   
   Para Python 2.7, use Olá comando a seguir:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Para Python 3.4, use Olá comando a seguir:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de saudação do comando de saudação New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Olá `django-admin` comando gera uma estrutura básica para sites baseados em Django:
   
   * `helloworld\manage.py` ajuda a iniciar a hospedagem e parar a hospedagem do seu site da web baseado em Django.
   * `helloworld\helloworld\settings.py` tem configurações do Django para seu aplicativo.
   * `helloworld\helloworld\urls.py`tiver um código de mapeamento de saudação entre cada URL e sua exibição.
3. No diretório de C:\inetpub\wwwroot\helloworld\helloworld hello, crie um novo arquivo denominado views.py. Este arquivo tem o modo de exibição de saudação que renderiza a página de "hello world" hello. Em seu editor de código, digite Olá comandos a seguir:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Substitua o conteúdo de saudação do arquivo de urls.py de saudação com hello comandos a seguir:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Configurar IIS
1. No arquivo de applicationHost. config global hello, desbloqueie a seção de manipuladores de saudação.  Isso permite que o manipulador de Python de saudação do Web. config arquivo toouse. Adicione este comando:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Ative o WFastCGI. Isso adiciona um aplicativo toohello global arquivo applicationHost config, que se refere a tooyour interpretador executável e hello wfastcgi.py script Python.
   
    No Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    No Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. Crie um arquivo web.config em C:\inetpub\wwwroot\helloworld. Olá valor Olá `scriptProcessor` atributo deve corresponder a saída de saudação do hello anterior da etapa. Para obter mais informações sobre a configuração de wfastcgi hello, consulte [pypi wfastcgi][wfastcgi].
   
   No Python 2.7:
   
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
   
   No Python 3.4:
   
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
4. Atualize o local de Olá Olá IIS padrão site toopoint toohello Django da pasta de projeto:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Carregar Olá página da Web no navegador.

![Uma janela do navegador exibirá a página do hello hello world no Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Desligar a máquina virtual do Azure
Quando você concluir este tutorial, é recomendável desligar ou remover Olá VM do Azure que você criou para o tutorial hello. Isso libera os recursos para outros tutoriais e você pode evitar incorrer em encargos de uso do Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
