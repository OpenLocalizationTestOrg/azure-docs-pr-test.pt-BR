---
title: aaaDjango e MySQL no Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo web Django que armazena dados em uma instância de banco de dados MySQL e implantá-lo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Django e MySQL no Azure com Ferramentas Python 2.2 para Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Neste tutorial, você usará [ferramentas Python para Visual Studio](https://www.visualstudio.com/vs/python) toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa. Você aprenderá como toouse um serviço do MySQL hospedados no Azure, como tooconfigure Olá web aplicativo toouse MySQL e como toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> informações de saudação contidas neste tutorial também estão disponíveis no hello vídeo a seguir:
> 
> [PTVS 2.1: aplicativo do Django com o MySQL][video]
> 
> 

Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com serviços de armazenamento de tabela do Azure, MySQL e banco de dados SQL. Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2015
* [Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]
* [Ferramentas Python 2.2 para Visual Studio]
* [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]
* [Ferramentas do SDK do Azure para VS 2015]
* Django 1.9 ou posterior

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido e não há compromissos.
> 
> 

## <a name="create-hello-project"></a>Criar hello projeto
Nesta seção, criaremos um projeto do Visual Studio usando um modelo de amostra. Você irá criar um ambiente virtual e instalará os pacotes necessários. Você irá criar um banco de dados local usando sqlite. Em seguida, você executará o aplicativo hello localmente.

1. No Visual Studio, selecione **Arquivo**, **Novo Projeto**.
2. Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**. Selecione **sondagens Django Web projeto** e clique em projeto de saudação toocreate Okey.
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Você será pacotes externos tooinstall solicitada. Selecione **Instalar em um ambiente virtual**.
   
    ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Selecione **Python 2.7** ou **Python 3.4** como interpretador base hello.
   
    ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.  Em seguida, selecione **Criar Superusuário do Django**.
6. Isso abra um Console de gerenciamento Django e criará um banco de dados sqlite na pasta de projeto hello. Siga Olá prompts toocreate um usuário.
7. Confirme se o aplicativo hello funciona pressionando `F5`.
8. Clique em **login** Olá na barra de navegação na parte superior da saudação.
   
    ![Barra de navegação do Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Insira as credenciais de saudação para usuário Olá criado quando você sincroniza o banco de dados de saudação.
   
    ![Formulário de logon](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Clique em **Criar Votações de Exemplo**.
    
     ![Criar Votações de Exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Clique em uma pesquisa e vote.
    
     ![Votação em votações de exemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Criar um banco de dados MySQL
Banco de dados hello, você criará um banco de dados ClearDB MySQL hospedado no Azure.

Como alternativa, você pode criar sua própria máquina virtual em execução no Azure, em seguida, instalar e administrar o MySQL por conta própria.

Você pode criar um banco de dados com um plano grátis seguindo estas etapas.

1. Faça logon no toohello [Portal do Azure].
2. Na Olá superior do painel de navegação de saudação, clique em **novo**, em seguida, clique em **dados + armazenamento**e, em seguida, clique em **banco de dados MySQL**.
3. Configurar Olá novo MySQL banco de dados, criando um novo grupo de recursos e selecione o local apropriado do Olá para ele.
4. Depois que o banco de dados do hello MySQL é criado, clique em **propriedades** na folha do banco de dados de saudação.
5. Use Olá cópia botão tooput Olá valor **cadeia de conexão** na área de transferência hello.

## <a name="configure-hello-project"></a>Configurar Olá projeto
Nesta seção, você vai configurar o nosso aplicativo toouse Olá MySQL banco de dados web que você acabou de criar. Você também instalará o Python pacotes necessários toouse MySQL bancos de dados adicionais com Django. Em seguida, você executará Olá web aplicativo localmente.

1. No Visual Studio, abra **settings.py**, da saudação *ProjectName* pasta. Temporariamente cole a cadeia de caracteres de conexão de saudação no editor de saudação. cadeia de caracteres de conexão de saudação é neste formato:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Alterar banco de dados de padrão de saudação **mecanismo** toouse MySQL e defina Olá valores para **nome**, **usuário**, **senha** e  **HOST** de saudação **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. No Gerenciador de soluções, em **Python ambientes**, com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.
3. Instalar o pacote de saudação `mysqlclient` usando **pip**.
   
    ![Caixa de diálogo Instalar Pacote](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.  Em seguida, selecione **Criar Superusuário do Django**.
   
    Isso cria tabelas de saudação do banco de dados MySQL Olá que você criou na seção anterior hello. Siga Olá prompts toocreate um usuário, que não tem um usuário de saudação toomatch no banco de dados sqlite Olá criado na primeira seção Olá deste artigo.
5. Executar o aplicativo hello com `F5`. Pesquisas que são criadas com **criar pesquisas de exemplo** e dados saudação enviados ao votar serão serializados no banco de dados do hello MySQL.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo
Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo web do serviço de aplicativo.

1. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.
   
    ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Clique em **Serviço de Aplicativo do Microsoft Azure**.
3. Clique em **novo** toocreate um novo aplicativo web.
4. Preencha Olá campos a seguir e clique em **criar**:
   
   * **Nome do aplicativo Web**
   * **Plano do Serviço de Aplicativo**
   * **Grupo de recursos**
   * **Região**
   * Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**
5. Aceite todos os outros padrões e clique em **Publicar**.
6. Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados. Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **MySQL** banco de dados hospedado no Azure.
   
    ![Navegador da Web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Parabéns! Você publicou com êxito sua tooAzure de aplicativo web com base em MySQL.

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, Django e MySQL.

* [Ferramentas Python para documentação do Visual Studio]
  * [Projetos da Web]
  * [Projetos do serviço de nuvem]
  * [Depuração remota no Microsoft Azure]
* [Documentação do Django]
* [MySQL]

Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).

<!--Link references-->

[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal do Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
