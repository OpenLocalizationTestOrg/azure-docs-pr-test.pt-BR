---
title: aaaDjango e banco de dados do SQL Azure com as ferramentas Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas Python para Visual Studio toocreate um aplicativo web Django que armazena dados em uma instância do banco de dados SQL e implantá-lo tooAzure aplicativos de Web do serviço de aplicativo."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django e Banco de Dados SQL no Azure com Ferramentas Python 2.2 para Visual Studio
Neste tutorial, vamos usar [ferramentas Python para Visual Studio] toocreate um simples aplicativo da web usando um dos modelos de exemplo hello PTVS de pesquisa. Este tutorial também está disponível como um [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Aprenderemos como toouse um banco de dados SQL hospedado no Azure, como tooconfigure Olá toouse de aplicativo da web a um banco de dados do SQL e como toopublish Olá aplicativo web muito[aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Consulte Olá [Central de desenvolvedores de Python] para obter mais artigos que abordam o desenvolvimento de aplicativos Web de serviço de aplicativo do Azure ao PTVS usando garrafa de, Bulbo e Django web frameworks, com serviços de armazenamento de tabela do Azure, MySQL e banco de dados SQL. Enquanto este artigo concentra-se no serviço de aplicativo, etapas de saudação são semelhantes ao desenvolver [serviços de nuvem do Azure].

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2015
* [Python 2.7 de 32 bits]
* [Ferramentas Python 2.2 para Visual Studio]
* [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]
* [Ferramentas do SDK do Azure para VS 2015]
* Django 1.9 ou posterior

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
>
>

## <a name="create-hello-project"></a>Criar hello projeto
Nesta seção, criaremos um projeto Visual Studio usando um modelo de amostra. Criaremos um ambiente virtual e instalaremos pacotes necessários. Criaremos um banco de dados local usando sqlite. Em seguida, vamos executar Olá web aplicativo localmente.

1. No Visual Studio, selecione **Arquivo**, **Novo Projeto**.
2. Olá modelos de projeto de saudação [as ferramentas Python 2.2 para VSIX de amostras do Visual Studio] estão disponíveis em **Python**, **exemplos**. Selecione **sondagens Django Web projeto** e clique em projeto de saudação toocreate Okey.

     ![Caixa de diálogo Novo Projeto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Você será pacotes externos tooinstall solicitada. Selecione **Instalar em um ambiente virtual**.

     ![Caixa de diálogo Pacotes Externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Selecione **Python 2.7** como interpretador base hello.

     ![Caixa de diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.  Em seguida, selecione **Criar Superusuário do Django**.
6. Isso abra um Console de gerenciamento Django e criará um banco de dados sqlite na pasta de projeto hello. Siga Olá prompts toocreate um usuário.
7. Confirme se o aplicativo hello funciona pressionando <kbd>F5</kbd>.
8. Clique em **login** Olá na barra de navegação na parte superior da saudação.

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Insira as credenciais de saudação para usuário Olá criado quando você sincroniza o banco de dados de saudação.

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Clique em **Criar Votações de Exemplo**.

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Clique em uma pesquisa e vote.

      ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Criar um banco de dados SQL
Banco de dados Olá, vamos criar um banco de dados do SQL Azure.

Você pode criar um banco de dados seguindo estas etapas.

1. Faça logon no hello [Portal do Azure].
2. Na parte inferior do Olá Olá do painel de navegação, clique em **novo**. Clique em **Dados + Armazenamento** > **Banco de Dados SQL**.
3. Configurar Olá novo banco de dados SQL, criando um novo grupo de recursos e selecione Olá local apropriado para ele.
4. Depois de criar hello banco de dados SQL, clique em **aberto no Visual Studio** na folha do banco de dados de saudação.
5. Clique em **Configurar seu firewall**.
6. Em Olá **as configurações do Firewall** folha, adicionar uma regra de firewall com **IP inicial** e **IP final** definir toohello de endereço IP público de sua máquina de desenvolvimento. Clique em **Salvar**.

   Isso permitirá que o servidor de banco de dados de toohello de conexões do computador de desenvolvimento.
7. Na folha do banco de dados de saudação, clique em **propriedades**, em seguida, clique em **Mostrar cadeias de conexão de banco de dados**.
8. Use Olá cópia botão tooput Olá valor **ADO.NET** na área de transferência hello.

## <a name="configure-hello-project"></a>Configurar Olá projeto
Nesta seção, configuraremos nosso web aplicativo toouse Olá banco de dados SQL que acabamos de criar. Também instalaremos adicionais Python pacotes necessários toouse bancos de dados SQL com Django. Em seguida, vamos executar Olá web aplicativo localmente.

1. No Visual Studio, abra **settings.py**, da saudação *ProjectName* pasta. Temporariamente cole a cadeia de caracteres de conexão de saudação no editor de saudação. cadeia de caracteres de conexão de saudação é neste formato:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Editar definição de saudação do `DATABASES` valores de saudação toouse acima.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. No Gerenciador de soluções, em **Python ambientes**, com o botão direito no ambiente virtual hello e selecione **instalar pacote da Python**.
2. Instalar o pacote de saudação `pyodbc` usando **pip**.

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Instalar o pacote de saudação `django-pyodbc-azure` usando **pip**.

     ![Caixa de diálogo Instalar Pacote Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **Python**e, em seguida, selecione **Django migrar**.  Em seguida, selecione **Criar Superusuário do Django**.

   Isso cria tabelas de saudação do banco de dados do SQL Olá criada na seção anterior hello. Siga Olá prompts toocreate um usuário, que não tem um usuário de saudação toomatch no banco de dados sqlite Olá criado na primeira seção do hello.
5. Executar o aplicativo hello com `F5`. Pesquisas que são criadas com **criar pesquisas de exemplo** e dados de saudação enviados ao votar serão serializados no banco de dados SQL Olá.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar tooAzure de aplicativo web de saudação do serviço de aplicativo
Olá SDK .NET do Azure fornece um toodeploy de maneira fácil seu tooAzure de aplicativo de web serviço de aplicativo Web de aplicativos web.

1. Em **Solution Explorer**, com o botão direito no nó do projeto hello e selecione **publicar**.

     ![Caixa de diálogo Web Publicar](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Clique em **Aplicativos Web do Microsoft Azure**.
3. Clique em **novo** toocreate um novo aplicativo web.
4. Preencha Olá campos a seguir e clique em **criar**.

   * **Nome do aplicativo Web**
   * **Plano do Serviço de Aplicativo**
   * **Grupo de recursos**
   * **Região**
   * Deixe **o servidor de banco de dados** definido muito**nenhum banco de dados**
5. Aceite todos os outros padrões e clique em **Publicar**.
6. Seu navegador da web será aberto automaticamente toohello aplicativo de web publicados. Você deve ver o trabalho de aplicativo web hello conforme o esperado, usando Olá **SQL** banco de dados hospedado no Azure.

   Parabéns!

     ![Navegador da Web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais sobre as ferramentas Python para Visual Studio, Django e banco de dados SQL.

* [Ferramentas Python para documentação do Visual Studio]
  * [Projetos da Web]
  * [Projetos do serviço de nuvem]
  * [Depuração remota no Microsoft Azure]
* [Documentação do Django]
* [Banco de Dados SQL]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Central de desenvolvedores de Python]: /develop/python/
[serviços de nuvem do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[ferramentas Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[as ferramentas Python 2.2 para VSIX de amostras do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do SDK do Azure para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Ferramentas Python para documentação do Visual Studio]: http://aka.ms/ptvsdocs
[Depuração remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos da Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do serviço de nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[Banco de Dados SQL]: /documentation/services/sql-database/
