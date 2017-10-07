---
title: aplicativos web aaaPython com garrafa no Azure
description: "Um tutorial que apresenta a você toorunning um aplicativo da web Python em aplicativos de Web do serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a>Criando aplicativos Web com Bottle no Azure
Este tutorial descreve como tooget iniciado Python em aplicativos de Web do serviço de aplicativo do Azure. Os Aplicativos Web fornecem hospedagem gratuita limitada e implantação rápida, além permitirem a você usar o Python! Como seu aplicativo cresce, você pode alternar a hospedagem de toopaid e você também pode integrar com todos os Olá outros serviços do Azure.

Você criará um aplicativo web usando a estrutura de web garrafa hello (consulte versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [bulbo](web-sites-python-create-deploy-flask-app.md)). Você criar o aplicativo da web de saudação do hello Azure Marketplace, configurar a implantação do Git e clonar Olá repositório localmente. Em seguida, irá executar o aplicativo da web de saudação localmente, fazer alterações, confirmar e enviá-las muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Olá tutorial mostra como toodo isso do Windows ou Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* Windows, Mac ou Linux
* Python 2.7 ou 3.4
* setuptools, pip, virtualenv (somente Python 2.7)
* Git
* [Ferramentas Python 2.2 para Visual Studio][Ferramentas Python 2.2 para Visual Studio] (PTVS) — Observação: isso é opcional

**Observação**: atualmente não há suporte à a publicação do TFS em projetos de Python.

### <a name="windows"></a>Windows
Caso você ainda não tenha o Python 2.7 ou 3.4 instalado (32 bits), recomendamos instalar o [SDK do Azure para Python 2.7] ou [SDK do Azure para Python 3.4] usando o Web Platform Installer. Isso instala a versão de 32 bits de saudação do Python setuptools, pip, virtualenv, etc (Python de 32 bits é o que é instalado em computadores de host do Azure Olá). Como alternativa, você pode obter o Python por meio de [python.org].

Para Git, recomendamos [Git para Windows] ou [GitHub para Windows]. Se você usar o Visual Studio, você pode usar o suporte de Git Olá integrado.

Também recomendamos a instalação das [Ferramentas Python 2.2 para Visual Studio]. Isso é opcional, mas se você tiver [Visual Studio], incluindo Olá liberar o Visual Studio Community 2013 ou o Visual Studio Express 2013 para Web, e isso lhe dará um grande IDE de Python.

### <a name="maclinux"></a>Mac/Linux
Você deve ter o Python e Git já instalados, mas certifique-se de ter uma das versões 2.7 ou 3.4 do Python.

## <a name="web-app-creation-on-hello-azure-portal"></a>Criação de aplicativo Web em Olá Portal do Azure
primeira etapa na criação de seu aplicativo Hello é toocreate Olá web aplicativo via Olá [Portal do Azure](https://portal.azure.com).  

1. Faça logon no hello Portal do Azure e clique em Olá **novo** botão no canto do hello inferior esquerdo. 
2. Na caixa de pesquisa hello, digite "python".
3. Nos resultados da pesquisa hello, selecione **garrafa**, em seguida, clique em **criar**.
4. Configure o novo aplicativo de garrafa hello, como criar um novo plano de serviço de aplicativo e um novo grupo de recursos para ele. Em seguida, clique em **Criar**.
5. Configurar a publicação de Git para seu aplicativo web criado recentemente, seguindo as instruções de saudação em [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Visão geral do aplicativo
### <a name="git-repository-contents"></a>Conteúdos do repositório Git
Aqui está uma visão geral dos arquivos Olá que no repositório Git inicial Olá que podemos será clonar na próxima seção, Olá.

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

Principais fontes para o aplicativo hello. Consiste em 3 páginas (índice, sobre, contato) com um layout mestre.  Scripts e conteúdo estático incluem bootstrap, jquery, modernizr e respond.

    \app.py

Suporte ao servidor de desenvolvimento local. Use este aplicativo de saudação do toorun localmente.

    \BottleWebProject.pyproj
    \BottleWebProject.sln

Arquivos de projeto para uso com [Python Tools para Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy de IIS para ambientes virtuais e suporte à depuração remota de PTVS.

    \requirements.txt

Pacotes externos requeridos por este aplicativo. script de implantação Hello serão pip instalar pacotes de saudação listados neste arquivo.

    \web.2.7.config
    \web.3.4.config

Arquivos de configuração do IIS. script de implantação de saudação será usar web.x.y.config apropriado hello e copie-o como Web. config.

### <a name="optional-files---customizing-deployment"></a>Arquivos opcionais - personalizando a implantação
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Arquivos opcionais - tempo de execução do Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Arquivos adicionais no servidor
Alguns arquivos existem no servidor de saudação, mas não são adicionados o repositório do git toohello. Eles são criados pelo script de implantação de saudação.

    \web.config

Arquivo de configuração do IIS. Criado por meio de web.x.y.config em toda implantação.

    \env\

Ambiente virtual do Python. Criado durante a implantação se um ambiente virtual compatível já não existe no aplicativo web de saudação.  Os pacotes listados no requirements.txt são pip instalado, mas pip vai ignorar a instalação se Olá pacotes já estão instalados.

Olá próximos 3 seções descrevem como tooproceed com Olá web desenvolvimento de aplicativo em 3 ambientes diferentes:

* Windows, com Python Tools para Visual Studio
* Windows, com linha de comando
* Mac/Linux, com linha de comando

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Desenvolvimento de aplicativo Web - Windows - Python Tools para Visual Studio
### <a name="clone-hello-repository"></a>Repositório de saudação do clone
Primeiro, clone o repositório de saudação usando Olá url fornecida no hello Portal do Azure. Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).

Abra o arquivo de solução da saudação (. sln) que está incluído na raiz de saudação do repositório de saudação.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a>Criar um ambiente virtual
Agora vamos criar um ambiente virtual para desenvolvimento local. Clique com o botão direito do mouse em **Ambientes Python** e selecione **Adicionar ambiente virtual...**.

* Certifique-se de nome de saudação do ambiente Olá é `env`.
* Selecione o interpretador base hello. Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (em runtime.txt ou Olá **configurações de aplicativo** folha do seu aplicativo web no hello Portal do Azure).
* Certifique-se de saudação opção toodownload e instalar pacotes é verificada.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

Clique em **Criar**. Isso será criar ambiente virtual hello e instalar dependências listadas em requirements.txt.

### <a name="run-using-development-server"></a>Executar usando o servidor de desenvolvimento
Pressione F5 toostart depuração e o navegador da web serão aberto automaticamente toohello página em execução localmente.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

Você pode definir pontos de interrupção em fontes de hello, use Olá inspecionar windows, etc. Consulte Olá [ferramentas Python para documentação do Visual Studio] para obter mais informações sobre Olá vários recursos.

### <a name="make-changes"></a>Fazer alterações
Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.

Depois de testar suas alterações, confirme repositório do Git toohello:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a>Instalar mais pacotes
Seu aplicativo pode ter dependências além de Python e Bottle.

Você pode instalar pacotes adicionais usando pip. tooinstall um pacote, clique com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.

Por exemplo, tooinstall hello Azure SDK para Python, que oferece acesso tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite `azure`:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

Clique com botão direito no ambiente virtual hello e selecione **gerar requirements.txt** tooupdate requirements.txt.

Em seguida, Olá confirmação altera o repositório do Git toohello toorequirements.txt.

### <a name="deploy-tooazure"></a>Implantar tooAzure
tootrigger uma implantação, clique em **sincronização** ou **Push**. A opção Sincronização faz um envio por push e a extração.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

implantação Olá levará algum tempo, pois ele cria um ambiente virtual, pacotes de instalação, etc.

O Visual Studio não mostra o progresso de saudação de implantação de saudação. Se desejar que a saída de hello tooreview, consulte a seção de saudação em [solução de problemas - implantação](#troubleshooting-deployment).

Procure toohello URL do Azure tooview suas alterações.

## <a name="web-app-development---windows---command-line"></a>Desenvolvimento de aplicativos Web - Windows - linha de comando
### <a name="clone-hello-repository"></a>Repositório de saudação do clone
Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto. Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Criar um ambiente virtual
Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório). Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.

Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (runtime.txt ou hello folha de configurações do aplicativo para seu aplicativo web no hello Portal do Azure)

Para o Python 2.7:

    c:\python27\python.exe -m virtualenv env

Para o Python 3.4:

    c:\python34\python.exe -m venv env

Instale quaisquer pacotes externos exigidos pelo seu aplicativo. Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Executar usando o servidor de desenvolvimento
Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:

    env\scripts\python app.py

console Olá exibirá a URL de saudação e servidor de saudação porta escuta:

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

Em seguida, abra a URL de toothat do navegador da web.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a>Fazer alterações
Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.

Depois de testar suas alterações, confirme repositório do Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalar mais pacotes
Seu aplicativo pode ter dependências além de Python e Bottle.

Você pode instalar pacotes adicionais usando pip. Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:

    env\scripts\pip install azure

Certifique-se de que requirements.txt de tooupdate:

    env\scripts\pip freeze > requirements.txt

Confirme as alterações de saudação:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implantar tooAzure
tootrigger uma implantação, Olá push altera tooAzure:

    git push azure master

Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.

Procure toohello URL do Azure tooview suas alterações.

## <a name="web-app-development---maclinux---command-line"></a>Desenvolvimento de aplicativos Web - Mac/Linux - linha de comando
### <a name="clone-hello-repository"></a>Repositório de saudação do clone
Primeiro, clonar repositório hello usando Olá URL fornecida no hello Portal do Azure e adicionar Olá repositório do Azure como um controle remoto. Para obter mais informações, consulte [tooAzure de implantação Local do Git do serviço de aplicativo](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Criar um ambiente virtual
Vamos criar um novo ambiente virtual para fins de desenvolvimento (não adicioná-lo toohello repositório). Ambientes virtuais no Python não são relocáveis, portanto, todos os desenvolvedores trabalhando em um aplicativo hello vai criar seus próprios localmente.

Certifique-se de toouse Olá a mesma versão do Python é selecionado para seu aplicativo web (runtime.txt ou hello folha de configurações de aplicativo do seu aplicativo web no hello Portal do Azure).

Para o Python 2.7:

    python -m virtualenv env

Para o Python 3.4:

    python -m venv env
ou pyvenv env

Instale quaisquer pacotes externos exigidos pelo seu aplicativo. Você pode usar o arquivo de requirements.txt de saudação na raiz de saudação de pacotes de saudação do hello repositório tooinstall em seu ambiente virtual:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Executar usando o servidor de desenvolvimento
Você pode iniciar o aplicativo hello em um servidor de desenvolvimento com hello comando a seguir:

    env/bin/python app.py

console Olá exibirá a URL de saudação e servidor de saudação porta escuta:

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

Em seguida, abra a URL de toothat do navegador da web.

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a>Fazer alterações
Agora você pode testar fazendo alterações toohello aplicativo fontes e/ou modelos.

Depois de testar suas alterações, confirme repositório do Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalar mais pacotes
Seu aplicativo pode ter dependências além de Python e Bottle.

Você pode instalar pacotes adicionais usando pip. Por exemplo, tooinstall hello Azure SDK para Python, que dá a você acessar tooAzure armazenamento, barramento de serviço e outros serviços do Azure, digite:

    env/bin/pip install azure

Certifique-se de que requirements.txt de tooupdate:

    env/bin/pip freeze > requirements.txt

Confirme as alterações de saudação:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implantar tooAzure
tootrigger uma implantação, Olá push altera tooAzure:

    git push azure master

Você verá uma saída Olá Olá do script de implantação, incluindo a criação do ambiente virtual, a instalação de pacotes, criação de Web. config.

Procure toohello URL do Azure tooview suas alterações.

## <a name="troubleshooting---package-installation"></a>Solução de problemas - Instalação de pacotes
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Solução de problemas - Ambiente virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais sobre garrafa e as ferramentas Python para Visual Studio: 

* [Documentação do Bottle]
* [ferramentas Python para documentação do Visual Studio]

Para obter informações sobre como usar o Armazenamento de Tabela do Azure e o MongoDB:

* [Bottle e MongoDB no Azure com Ferramentas Python 2.1 para Visual Studio]
* [Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.1 para Visual Studio]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Bottle e MongoDB no Azure com Ferramentas Python 2.1 para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle e Armazenamento de Tabela do Azure com Ferramentas Python 2.1 para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[SDK do Azure para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[SDK do Azure para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs 
[Documentação do Bottle]: http://bottlepy.org/docs/dev/index.html

