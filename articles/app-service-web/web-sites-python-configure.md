---
title: "aaaConfiguring Python com aplicativos de Web do serviço de aplicativo do Azure"
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
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure
Este tutorial descreve as opções para criação e configuração de uma Web Server Gateway Interface (WSGI) básica compatível com aplicativos Python nos [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).

Ele descreve os recursos adicionais de implantação do Git, como o ambiente virtual e a instalação do pacote usando requirements.txt.

## <a name="bottle-django-or-flask"></a>Bottle, Django ou Flask?
Hello Azure Marketplace contém modelos para estruturas de vidro, Django e bulbo hello. Se você estiver desenvolvendo seu primeiro aplicativo web no serviço de aplicativo do Azure, ou você não estiver familiarizado com o Git, recomendamos que você siga um destes tutoriais, que incluem instruções passo a passo para criar um aplicativo de trabalho na Galeria de saudação usando a implantação do Git do Windows ou Mac:

* [Criando aplicativos Web com Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Criando aplicativos Web com Django](web-sites-python-create-deploy-django-app.md)
* [Criando aplicativos Web com Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Criação de aplicativos Web no Portal do Azure
Este tutorial assume um existente do Azure assinatura e acesso toohello Portal do Azure.

Se você não tiver um aplicativo web existente, você pode criar um de saudação [Portal do Azure](https://portal.azure.com).  NOVO botão Olá no canto superior esquerdo da saudação clique **Web + móvel** > **aplicativo Web**.

## <a name="git-publishing"></a>Publicação Git
Configurar a publicação de Git para seu aplicativo web criado recentemente, seguindo as instruções de saudação em [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md). Este tutorial usa toocreate Git, gerenciar e publicar nosso tooAzure de aplicativo web do Python do serviço de aplicativo.

Depois que a publicação Git estiver configurada, um repositório Git será criado e associado ao seu aplicativo Web. URL do repositório Hello será exibido e daqui em diante pode ser usado toopush dados da nuvem de toohello de ambiente de desenvolvimento local hello. toopublish aplicativos por meio de Git, certifique-se de um cliente de Git também é instalado e instruções Olá fornecido toopush seu tooAzure de conteúdo de aplicativo do serviço de aplicativo web.

## <a name="application-overview"></a>Visão geral do aplicativo
Nas seções de Avançar hello, Olá seguintes arquivos é criado. Eles devem ser colocados na raiz de saudação do repositório do Git de saudação.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Manipulador WSGI
WSGI é um padrão de Python descrito por [PEP 3333](http://www.python.org/dev/peps/pep-3333/) define uma interface entre o servidor de web hello e Python. Ele fornece uma interface padronizada para escrever vários aplicativos da web e estruturas usando o Python. As estruturas web populares Python de hoje usam a WSGI. Azure fornece serviço de aplicativo Web de aplicativos que você oferece suporte para essas estruturas; Além disso, os usuários avançados podem até mesmo criar seus próprios como manipulador personalizado Olá segue diretrizes de especificação de WSGI hello.

Aqui está um exemplo de um `app.py` que define um manipulador personalizado:

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

Você pode executar este aplicativo localmente com `python app.py`, procure muito`http://localhost:5555` no navegador da web.

## <a name="virtual-environment"></a>Ambiente virtual
Embora o aplicativo de exemplo hello acima não exige qualquer pacotes externos, é provável que seu aplicativo exigir alguns.

toohelp gerenciar as dependências do pacote externo, implantação do Git do Azure dá suporte à criação de saudação de ambientes virtuais.

Quando o Azure detecta um requirements.txt na raiz de saudação do repositório de hello, ele cria automaticamente um ambiente virtual denominado `env`. Isso ocorre apenas na primeira implantação de hello, ou durante qualquer implantação após Olá tempo de execução do Python selecionado foi alterado.

Você provavelmente desejará toocreate um ambiente virtual localmente para o desenvolvimento, mas não incluí-lo em seu repositório Git.

## <a name="package-management"></a>Gerenciamento de pacote
Os pacotes listados no requirements.txt serão instalados automaticamente no ambiente virtual do hello usando pip. Isso ocorre em todas as implantações, mas pip ignorará a instalação se um pacote já estiver instalado.

Exemplo `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Versão do Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Exemplo `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Você precisará toocreate um toospecify do arquivo Web. config como servidor de saudação deve tratar solicitações.

Observe que se você tiver um arquivo web.x.y.config em seu repositório, onde x. y corresponde Olá selecionado em tempo de execução do Python, Azure copiará automaticamente o arquivo apropriado de saudação como Web. config.

Olá exemplos de Web. config a seguir dependem de um script de proxy do ambiente virtual, que é descrito na próxima seção, Olá.  Elas funcionam com o manipulador WSGI Olá usado no exemplo hello `app.py` acima.

Exemplo `web.config` para Python 2.7:

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


Exemplo `web.config` para Python 3.4:

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


Arquivos estáticos são manipulados pelo servidor de web hello diretamente, sem passar pelo código Python, para melhorar o desempenho.

Em Olá acima exemplos, local de saudação de arquivos estáticos de saudação em disco deve corresponder local Olá Olá URL. Isso significa que uma solicitação para `http://pythonapp.azurewebsites.net/static/site.css` servirá arquivo hello no disco `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`é onde você especifica o manipulador WSGI hello. Em Olá acima exemplos, ele tem `app.wsgi_app` porque o manipulador de saudação é uma função chamada `wsgi_app` em `app.py` na pasta raiz de saudação.

`PYTHONPATH`pode ser personalizado, mas se você instalar todas as suas dependências no ambiente virtual Olá especificando-os na requirements.txt, não será necessário toochange-lo.

## <a name="virtual-environment-proxy"></a>Proxy de ambiente virtual
Olá script a seguir é manipulador de WSGI tooretrieve usado hello, ativar Olá virtuais ambiente e log de erros. Ele é projetado toobe genérico e usado sem modificações.

Conteúdo de `ptvs_virtualenv_proxy.py`:

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
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
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
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


## <a name="customize-git-deployment"></a>Personalizar a implantação do Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Solução de problemas - Instalação de pacotes
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Solução de problemas - Ambiente virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

