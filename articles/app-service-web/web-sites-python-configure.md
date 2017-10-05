---
title: "Configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure"
description: "Este tutorial descreve opções para criar e configurar um servidor Web básico compatível com aplicativos de Python Gateway Interface (WSGI) nos Aplicativos Web do Serviço de Aplicativo do Azure."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 9683a1af13eeff364d3c4714f0b791324fd82659
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="70f76-103">Configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="70f76-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="70f76-104">Este tutorial descreve as opções para criação e configuração de uma Web Server Gateway Interface (WSGI) básica compatível com aplicativos Python nos [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="70f76-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="70f76-105">Ele descreve os recursos adicionais de implantação do Git, como o ambiente virtual e a instalação do pacote usando requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="70f76-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="70f76-106">Bottle, Django ou Flask?</span><span class="sxs-lookup"><span data-stu-id="70f76-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="70f76-107">O Azure Marketplace contém modelos para as estruturas Bottle, Django e Flask.</span><span class="sxs-lookup"><span data-stu-id="70f76-107">The Azure Marketplace contains templates for the Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="70f76-108">Se você estiver desenvolvendo seu primeiro aplicativo Web no Serviço de Aplicativo do Azure ou se não estiver familiarizado com o Git, recomendamos que você siga um destes tutoriais, que incluem instruções passo a passo para criar um aplicativo funcional da galeria usando a implantação do Git do Windows ou Mac:</span><span class="sxs-lookup"><span data-stu-id="70f76-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from the gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="70f76-109">Criando aplicativos Web com Bottle</span><span class="sxs-lookup"><span data-stu-id="70f76-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="70f76-110">Criando aplicativos Web com Django</span><span class="sxs-lookup"><span data-stu-id="70f76-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="70f76-111">Criando aplicativos Web com Flask</span><span class="sxs-lookup"><span data-stu-id="70f76-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="70f76-112">Criação de aplicativos Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="70f76-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="70f76-113">Este tutorial assume uma assinatura existente do Azure e acesso ao Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f76-113">This tutorial assumes an existing Azure subscription and access to the Azure Portal.</span></span>

<span data-ttu-id="70f76-114">Se não tiver um aplicativo Web já existente, você poderá criar um no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70f76-114">If you do not have an existing web app, you can create one from the [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="70f76-115">Clique no botão NOVO no canto superior esquerdo e clique em **Web + Celular** > **aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="70f76-115">Click the NEW button in the top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="70f76-116">Publicação Git</span><span class="sxs-lookup"><span data-stu-id="70f76-116">Git Publishing</span></span>
<span data-ttu-id="70f76-117">Configure a publicação de Git para seu aplicativo Web recém-criado seguindo as instruções em [Implantação de GIT local no Serviço de Aplicativo do Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="70f76-117">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="70f76-118">Este tutorial usa Git para criar, gerenciar e publicar nosso aplicativo Web Python para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f76-118">This tutorial uses Git to create, manage, and publish our Python web app to Azure App Service.</span></span>

<span data-ttu-id="70f76-119">Depois que a publicação Git estiver configurada, um repositório Git será criado e associado ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="70f76-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="70f76-120">A URL do repositório será exibida e poderá ser usada para enviar por push dados do ambiente de desenvolvimento local para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="70f76-120">The repository's URL will be displayed and can henceforth be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="70f76-121">Para publicar aplicativos via Git, certifique-se de que um cliente Git também esteja instalado e use as instruções fornecidas para enviar o conteúdo do seu aplicativo Web para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="70f76-121">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="70f76-122">Visão geral do aplicativo</span><span class="sxs-lookup"><span data-stu-id="70f76-122">Application Overview</span></span>
<span data-ttu-id="70f76-123">Nas próximas seções, os arquivos a seguir são criados.</span><span class="sxs-lookup"><span data-stu-id="70f76-123">In the next sections, the following files are created.</span></span> <span data-ttu-id="70f76-124">Eles devem ser colocados na raiz do repositório Git.</span><span class="sxs-lookup"><span data-stu-id="70f76-124">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="70f76-125">Manipulador WSGI</span><span class="sxs-lookup"><span data-stu-id="70f76-125">WSGI Handler</span></span>
<span data-ttu-id="70f76-126">WSGI é um padrão de Python descrito por [PEP 3333](http://www.python.org/dev/peps/pep-3333/) definindo uma interface entre o servidor web e o Python.</span><span class="sxs-lookup"><span data-stu-id="70f76-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="70f76-127">Ele fornece uma interface padronizada para escrever vários aplicativos da web e estruturas usando o Python.</span><span class="sxs-lookup"><span data-stu-id="70f76-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="70f76-128">As estruturas web populares Python de hoje usam a WSGI.</span><span class="sxs-lookup"><span data-stu-id="70f76-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="70f76-129">Os Aplicativos Web do Serviço de Aplicativo do Azure oferecem suporte para essas estruturas; além disso, os usuários avançados podem até mesmo criar seus próprios, desde que o manipulador personalizado siga as diretrizes de especificação WSGI.</span><span class="sxs-lookup"><span data-stu-id="70f76-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="70f76-130">Aqui está um exemplo de um `app.py` que define um manipulador personalizado:</span><span class="sxs-lookup"><span data-stu-id="70f76-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="70f76-131">Você pode executar esse aplicativo localmente com `python app.py` e, em seguida, navegar até `http://localhost:5555` no seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="70f76-131">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="70f76-132">Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="70f76-132">Virtual Environment</span></span>
<span data-ttu-id="70f76-133">Embora o aplicativo de exemplo acima não exija pacotes externos, é provável que seu aplicativo exija alguns.</span><span class="sxs-lookup"><span data-stu-id="70f76-133">Although the example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="70f76-134">Para ajudar a gerenciar as dependências do pacote externo, a implantação do Git do Azure dá suporte à criação de ambientes virtuais.</span><span class="sxs-lookup"><span data-stu-id="70f76-134">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="70f76-135">Quando o Azure detecta um arquivo requirements.txt na raiz do repositório, ele cria automaticamente um ambiente virtual chamado `env`.</span><span class="sxs-lookup"><span data-stu-id="70f76-135">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="70f76-136">Isso ocorre apenas na primeira implantação ou durante qualquer implantação depois que o tempo de execução do Python selecionado é alterado.</span><span class="sxs-lookup"><span data-stu-id="70f76-136">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="70f76-137">Você provavelmente desejará criar um ambiente virtual localmente para desenvolvimento, mas não o inclua em seu repositório Git.</span><span class="sxs-lookup"><span data-stu-id="70f76-137">You will probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="70f76-138">Gerenciamento de pacote</span><span class="sxs-lookup"><span data-stu-id="70f76-138">Package Management</span></span>
<span data-ttu-id="70f76-139">Os pacotes listados no arquivo requirements.txt serão instalados automaticamente no ambiente virtual usando pip.</span><span class="sxs-lookup"><span data-stu-id="70f76-139">Packages listed in requirements.txt will be installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="70f76-140">Isso ocorre em todas as implantações, mas pip ignorará a instalação se um pacote já estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="70f76-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="70f76-141">Exemplo `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="70f76-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="70f76-142">Versão do Python</span><span class="sxs-lookup"><span data-stu-id="70f76-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="70f76-143">Exemplo `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="70f76-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="70f76-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="70f76-144">Web.config</span></span>
<span data-ttu-id="70f76-145">Você precisará criar um arquivo web.config para especificar como o servidor deve manipular solicitações.</span><span class="sxs-lookup"><span data-stu-id="70f76-145">You'll need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="70f76-146">Observe que, se você tiver um arquivo web.x.y.config no repositório, em que x.y corresponde ao tempo de execução do Python selecionado, o Azure copiará automaticamente o arquivo apropriado como web.config.</span><span class="sxs-lookup"><span data-stu-id="70f76-146">Note that if you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure will automatically copy the appropriate file as web.config.</span></span>

<span data-ttu-id="70f76-147">Os exemplos de web.config a seguir contam com um script de proxy do ambiente virtual, que é descrito na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="70f76-147">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="70f76-148">Eles funcionam com o manipulador WSGI usado no exemplo `app.py` acima.</span><span class="sxs-lookup"><span data-stu-id="70f76-148">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="70f76-149">Exemplo `web.config` para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="70f76-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="70f76-150">Exemplo `web.config` para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="70f76-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="70f76-151">Arquivos estáticos são manipulados pelo servidor Web diretamente, sem passar pelo código do Python, para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="70f76-151">Static files will be handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="70f76-152">Nos exemplos acima, o local dos arquivos estáticos no disco deve corresponder ao local na URL.</span><span class="sxs-lookup"><span data-stu-id="70f76-152">In the above examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="70f76-153">Isso significa que uma solicitação para `http://pythonapp.azurewebsites.net/static/site.css` fornecerá o arquivo no disco em `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="70f76-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="70f76-154">`WSGI_ALT_VIRTUALENV_HANDLER` é onde você especifica o manipulador WSGI.</span><span class="sxs-lookup"><span data-stu-id="70f76-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="70f76-155">Nos exemplos acima, é `app.wsgi_app` porque o manipulador é uma função chamada `wsgi_app` em `app.py` na pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="70f76-155">In the above examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="70f76-156">`PYTHONPATH` pode ser personalizado, mas se você instalar todas as suas dependências no ambiente virtual especificando-as em requirements.txt, não deverá precisar alterá-lo.</span><span class="sxs-lookup"><span data-stu-id="70f76-156">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="70f76-157">Proxy de ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="70f76-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="70f76-158">O script a seguir é usado para recuperar o manipulador WSGI, ativar o ambiente virtual e registrar os erros em log.</span><span class="sxs-lookup"><span data-stu-id="70f76-158">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="70f76-159">Foi projetado para ser genérico e ser usado sem modificações.</span><span class="sxs-lookup"><span data-stu-id="70f76-159">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="70f76-160">Conteúdo de `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="70f76-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="70f76-161">Personalizar a implantação do Git</span><span class="sxs-lookup"><span data-stu-id="70f76-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="70f76-162">Solução de problemas - Instalação de pacotes</span><span class="sxs-lookup"><span data-stu-id="70f76-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="70f76-163">Solução de problemas - Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="70f76-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="70f76-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70f76-164">Next steps</span></span>
<span data-ttu-id="70f76-165">Para saber mais, confira o [Centro de Desenvolvedores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="70f76-165">For more information, see the [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="70f76-166">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70f76-166">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="70f76-167">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="70f76-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="70f76-168">O que mudou</span><span class="sxs-lookup"><span data-stu-id="70f76-168">What's changed</span></span>
* <span data-ttu-id="70f76-169">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="70f76-169">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

