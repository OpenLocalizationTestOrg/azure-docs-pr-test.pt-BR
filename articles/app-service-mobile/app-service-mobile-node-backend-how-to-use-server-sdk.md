---
title: "toowork aaaHow com o servidor de back-end Olá Node. js SDK para aplicativos móveis | Microsoft Docs"
description: "Saiba como toowork com hello o servidor de back-end node. js SDK para aplicativos de celular do serviço de aplicativo do Azure."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Como toouse Olá SDK de Node.js de aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Este artigo fornece informações detalhadas e exemplos que mostram como toowork com um back-end do Node. js em aplicativos de celular do serviço de aplicativo do Azure.

## <a name="Introduction"></a>Introdução
Aplicativos móveis de serviço de aplicativo do Azure fornece acesso a dados Olá recurso tooadd mobile-otimizado aplicativo de web tooa API da Web.  Olá SDK de aplicativos móveis do serviço de aplicativo do Azure é fornecido para aplicativos web ASP.NET e Node. js.  Olá SDK fornece Olá seguintes operações:

* Operações de tabela (Ler, Inserir, Atualizar Excluir) para acesso a dados
* Operações de API personalizadas

Ambas as operações permitem a autenticação em todos os provedores de identidade permitidos pelo Serviço de Aplicativo do Azure, incluindo provedores de identidade social como Facebook, Twitter, Google e Microsoft, além do Active Directory do Azure para a identidade corporativa.

Você pode encontrar exemplos para cada caso de uso no hello [diretório de exemplos no GitHub].

## <a name="supported-platforms"></a>Plataformas com suporte
Olá SDK de nó de aplicativos móveis do Azure oferece suporte a saudação que LTS atuais versão do nó e versões posteriores.  A partir de gravação, Olá LTS versão é v4.5.0 de nó.  Outras versões do Node podem funcionar, mas não são têm suporte.

Olá SDK de nó de aplicativos móveis do Azure oferece suporte a dois drivers de banco de dados - Olá nó mssql driver dá suporte ao SQL Azure e as instâncias locais do SQL Server.  driver de sqlite3 Olá dá suporte a bancos de dados SQLite em uma única instância.

### <a name="howto-cmdline-basicapp"></a>Como: criar um back-end node. js básica usando Olá linha de comando
Cada back-end de Node.js do Aplicativo Móvel do Serviço de Aplicativo do Azure inicia como um aplicativo ExpressJS.  ExpressJS é hello mais popular estrutura de serviço web disponível para Node. js.  Você pode criar um aplicativo [Express] básico da seguinte maneira:

1. Em um comando ou a janela do PowerShell, crie um diretório para seu projeto.

        mkdir basicapp
2. Execute a estrutura do pacote npm init tooinitialize hello.

        cd basicapp
        npm init

    comando de inicialização de npm Olá solicita um conjunto de projeto de saudação tooinitialize perguntas.  Consulte a saída de exemplo hello:

    ![saída de init npm Hello][0]
3. Instale bibliotecas de express e aplicativos do azure-mobile de saudação do repositório de npm hello.

        npm install --save express azure-mobile-apps
4. Crie um app.js tooimplement Olá básica móveis servidor de arquivos.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Esse aplicativo cria um WebAPI mobile otimizado com um ponto de extremidade (`/tables/TodoItem`) que fornece acesso não autenticado tooan subjacente usando um esquema dinâmico de armazenamento de dados SQL.  Ele é adequado para os seguintes inícios rápidos de biblioteca de cliente:

* [Início rápido do cliente Android]
* [Início rápido do cliente Apache Cordova]
* [Início rápido do cliente iOS]
* [Início rápido de cliente Windows Store]
* [Início rápido do cliente Xamarin.iOS]
* [Início rápido do cliente Xamarin.Android]
* [Início rápido do cliente Xamarin.Forms]

Você pode encontrar o código de saudação para este aplicativo básico em Olá [basicapp exemplo no GitHub].

### <a name="howto-vs2015-basicapp"></a>Como criar um back-end de nó com o Visual Studio 2015
Visual Studio 2015 exige uma extensão de toodevelop de Node. js aplicativos dentro de saudação IDE.  toostart, Olá install [Node. js Tools 1.1 para Visual Studio].  Depois que Olá Node. js Tools para Visual Studio estiverem instalados, crie um aplicativo de 4. x Express:

1. Olá abrir **novo projeto** caixa de diálogo (de **arquivo** > **novo** > **projeto...** ).
2. Expanda **Modelos** > **JavaScript** > **Node. js**.
3. Selecione Olá **Basic do Azure Node. js Express 4 Application**.
4. Preencha o nome do projeto hello.  Clique em *OK*.

    ![Novo projeto do Visual Studio 2015][1]
5. Saudação de atalho **npm** nó e selecione **instalar novos pacotes de npm...** .
6. Talvez seja necessário toorefresh Olá npm catálogo criando seu primeiro aplicativo Node. js.  Clique em **Atualizar** , se necessário.
7. Digite *aplicativos do azure-mobile* na caixa de pesquisa de saudação.  Clique em Olá **aplicativos do azure-mobile-2.0.0** do pacote e, em seguida, clique em **instalar pacote**.

    ![Instalar novos pacotes npm][2]
8. Clique em **fechar**
9. Olá abrir *app.js* arquivo tooadd suporte Olá SDK de aplicativos móveis do Azure.  Na parte inferior de saudação de 6 at linha da biblioteca de saudação requerem instruções, adicione Olá código a seguir:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    Em aproximadamente linha 27 após Olá outras instruções app.use, adicione Olá código a seguir:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Salve o arquivo hello.
10. Execute o aplicativo hello localmente (Olá API é divulgada http://localhost:3000) ou publicar tooAzure.

### <a name="create-node-backend-portal"></a>Como: criar um back-end node. js usando Olá portal do Azure
Você pode criar um direito de back-end do aplicativo móvel no hello [portal do Azure]. Você pode seguir Olá seguir as etapas ou cria um cliente e servidor juntos, Olá a seguir [criar um aplicativo móvel](app-service-mobile-ios-get-started.md) tutorial. tutorial de Olá contém uma versão simplificada dessas instruções e é melhor para a verificação de projetos de conceito.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Em Olá *começar* folha, em **criar uma tabela API**, escolha **Node. js** como seu **idioma de back-end**.
Marque a caixa Olá para "**confirmo que isto substituirá todos os conteúdos do site.**", em seguida, clique em **tabela TodoItem criar**.

### <a name="download-quickstart"></a>Como: Download Olá Node. js back-end quickstart projeto de código usando Git
Quando você cria um back-end do aplicativo móvel de Node. js usando o portal de saudação **início rápido** folha, um projeto de Node. js é criado para você e site tooyour implantado. Você pode adicionar tabelas e APIs e editar arquivos de código de back-end do hello Node. js no portal de saudação. Você também pode usar várias ferramentas toodownload Olá back-end projeto de implantação de modo que você pode adicionar ou modificar tabelas e APIs e republicar o projeto de saudação. Para saber mais, confira o [Guia de implantação do Serviço de Aplicativo do Azure]. Olá procedimento a seguir usa um código de projeto Git repositório toodownload Olá início rápido.

1. Instale o Git, caso ainda não tenha feito isso. Olá etapas necessárias tooinstall Git variar entre sistemas operacionais. Consulte [Instalando o Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para distribuições específicas de sistemas operacionais e orientações de instalação.
2. Siga as etapas de saudação em [habilitar Olá repositório de aplicativo de serviço de aplicativo](../app-service-web/app-service-deploy-local-git.md#Step3) repositório do Git tooenable Olá para seu site de back-end, fazendo uma anotação de saudação implantação username e password.
3. Na folha de saudação para seu back-end do aplicativo móvel, anote Olá **URL de clone de Git** configuração.
4. Executar Olá `git clone` comando usando a URL de clone de Git hello, inserir sua senha, quando necessário, como no exemplo a seguir:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Procurar o diretório toolocal, que Olá anterior exemplo é /todolist e observe que os arquivos de projeto foram baixados. Localizar Olá `todoitem.json` arquivo hello `/tables` directory.  Esse arquivo define as permissões na tabela.  Também encontrar hello `todoitem.js` arquivo hello mesmo diretório, que define que a operação CRUD scripts para a tabela de saudação.
6. Depois que você fez alterações tooproject arquivos, execute Olá comandos tooadd, confirmar, em seguida, carregar o site de toohello alterações a seguir:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Quando você adiciona um novo projeto de toohello de arquivos, é necessário primeiro Olá tooexecute `git add .` comando.

site de saudação for publicada novamente sempre que um novo conjunto de confirmação é enviada por push toohello site.

### <a name="howto-publish-to-azure"></a>Como: publicar sua tooAzure de back-end node. js
O Microsoft Azure fornece vários mecanismos para publicar seu back-end do Azure aplicativo serviços móveis aplicativos Node para Olá serviço do Azure.  Eles incluem a utilização das ferramentas de implantação integradas ao Visual Studio, das ferramentas de linha de comando e das opções de implantação contínua com base no controle de origem.  Para saber mais sobre esse tópico, confira o [Guia de implantação do Serviço de Aplicativo do Azure].

O Serviço de Aplicativo do Azure tem recomendações específicas para aplicativo Node.js que você deve examinar antes de implantar:

* Como muito[especificar Olá versão do nó]
* Como muito[usar módulos de nó]

### <a name="howto-enable-homepage"></a>Como habilitar uma home page para seu aplicativo
Muitos aplicativos são uma combinação de aplicativos web e móveis e Olá ExpressJS estrutura permite que você toocombine dois facetas.  Às vezes, no entanto, talvez você queira tooonly implementar uma interface móvel.  É útil tooprovide que um serviço de aplicativo da saudação inicial página tooensure está em execução.  Você pode fornecer sua própria home page ou habilitar uma home page temporária.  tooenable uma home page temporária, use Olá tooinstantiate Azure Mobile aplicativos a seguir:

    var mobile = azureMobileApps({ homePage: true });

Se você desejar somente essa opção disponível durante o desenvolvimento localmente, você pode adicionar essa configuração tooyour `azureMobile.js` arquivo.

## <a name="TableOperations"></a>Operações de tabela
Olá aplicativos do azure-mobile Node. js servidor SDK fornece mecanismos tooexpose dados tabelas armazenadas no banco de dados SQL Azure como um WebAPI.  Cinco operações são fornecidas.

| Operação | Descrição |
| --- | --- |
| GET /tables/*tablename* |Obter todos os registros na tabela de saudação |
| GET /tables/*tablename*/:id |Obter um registro específico na tabela de saudação |
| POST /tables/*tablename* |Criar um registro na tabela de saudação |
| PATCH /tables/*tablename*/:id |Atualizar um registro na tabela de saudação |
| DELETE /tables/*tablename*/:id |Excluir um registro na tabela de saudação |

Oferece suporte a essa WebAPI [OData] e estende o toosupport de esquema de tabela Olá [a sincronização de dados offline].

### <a name="howto-dynamicschema"></a>Como definir tabelas usando um esquema dinâmico
Antes de poder usar uma tabela, ela deve ser definida.  Tabelas podem ser definidas com um esquema estático (onde desenvolvedor Olá define colunas Olá no esquema de saudação) ou dinamicamente (onde Olá SDK controla o esquema de saudação com base nas solicitações de entrada). Além disso, o desenvolvedor de Olá pode controlar aspectos específicos de saudação WebAPI adicionando definição de toohello de código Javascript.

Como uma prática recomendada, você deve definir cada tabela em um arquivo Javascript no diretório de tabelas de saudação e usar as tabelas de saudação tables.import() método tooimport.  Estender o aplicativo hello basic, arquivo de app.js Olá seria ajustado:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Definir tabela hello. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

As tabelas usam o esquema dinâmico por padrão.  tooturn desativar dinâmicas de esquema definido globalmente, Olá configuração do aplicativo **MS_DynamicSchema** toofalse em Olá portal do Azure.

Você pode encontrar um exemplo completo em Olá [exemplo todo no GitHub].

### <a name="howto-staticschema"></a>Como definir tabelas usando um esquema estático
Você pode definir explicitamente Olá colunas tooexpose via Olá WebAPI.  Olá que aplicativos do azure-mobile Node. js SDK adiciona automaticamente a quaisquer colunas adicionais necessárias para a lista de toohello de sincronização de dados offline que você fornecer.  Por exemplo, os aplicativos de cliente QuickStart exigem uma tabela com duas colunas: texto (uma cadeia de caracteres) e completo (um valor booliano).  
tabela Olá pode ser definida no hello tabela JavaScript arquivo de definição (localizado no diretório de tabelas de saudação) da seguinte maneira:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Se você definir tabelas estaticamente, em seguida, você também deve chamar esquema de banco de dados de Olá Olá tables.initialize() método toocreate na inicialização.  Olá tables.initialize() método retorna um [promessa] para que o serviço web de saudação não atender a solicitações antes do banco de dados de hello está sendo inicializado.

### <a name="howto-sqlexpress-setup"></a>Como usar o SQL Express como um armazenamento de dados de desenvolvimento em sua máquina local
os aplicativos móveis do Azure Olá AzureMobile aplicativos nó SDK Hello fornece três opções para dados do servidor sem necessidade de saudação: SDK fornece três opções para dados fora da caixa de saudação do servidor:

* Saudação de uso **memória** repositório de exemplo do driver tooprovide um não persistente
* Saudação de uso **mssql** tooprovide de driver para o desenvolvimento de um repositório de dados SQL Express
* Saudação de uso **mssql** driver tooprovide um repositório de dados do banco de dados SQL para produção

Olá SDK de Node.js de aplicativos móveis do Azure usa Olá [mssql Node. js pacote] tooestablish e usar uma conexão tooboth SQL Express e o banco de dados SQL.  Este pacote requer que você habilite conexões TCP na instância do SQL Express.

> [!TIP]
> driver de saudação de memória não fornece um conjunto completo de recursos para teste.  Se você desejar tootest localmente seu back-end, recomendamos usar saudação de um repositório de dados do SQL Express e Olá mssql driver.
>
>

1. Baixe e instale o [Microsoft SQL Server 2014 Express].  Certifique-se de que você instalar Olá SQL Server 2014 Express com ferramentas edition.  A menos que você explicitamente precisar do suporte de 64 bits, versão de 32 bits Olá consome menos memória durante a execução.
2. Execute Olá Gerenciador de configuração do SQL Server 2014.

   1. Expanda Olá **configuração de rede do SQL Server** nó no menu de árvore à esquerda de saudação.
   2. Clique em **Protocolos para SQLEXPRESS**.
   3. Clique com o botão direito do mouse em **TCP/IP** e escolha **Habilitar**.  Clique em **Okey** na caixa de diálogo pop-up hello.
   4. Clique com o botão direito do mouse em **TCP/IP** e escolha **Propriedades**.
   5. Clique em Olá **endereços IP** guia.
   6. Localize Olá **IPAll** nó.  Em Olá **a porta TCP** , digite **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Clique em **OK**.  Clique em **Okey** na caixa de diálogo pop-up hello.
   8. Clique em **SQL Server Services** no menu de árvore à esquerda de saudação.
   9. Clique com o botão direito do mouse em **SQL Server (SQLEXPRESS)** e escolha **Reiniciar**
   10. Feche Olá Gerenciador de configuração do SQL Server 2014.
3. Executar Olá SQL Server 2014 Management Studio e conecte-se a instância do SQL Express local tooyour

   1. Clique em sua instância de saudação Pesquisador de objetos e selecione **propriedades**
   2. Selecione Olá **segurança** página.
   3. Certifique-se de saudação **modo de autenticação do Windows e SQL Server** está selecionada
   4. Clique em **OK**

          ![Configure SQL Express Authentication][4]
   5. Expanda **segurança** > **logons** em Olá Pesquisador de objetos
   6. Clique com o botão direito do mouse em **Logons** e escolha **Novo Logon...**
   7. Insira um nome de logon.  Selecione **Autenticação do SQL Server**.  Insira uma senha e digite Olá mesma senha em **Confirmar senha**.  senha Olá deve atender aos requisitos de complexidade do Windows.
   8. Clique em **OK**

          ![Add a new user tooSQL Express][5]
   9. Clique com o botão direito do mouse em seu novo logon e escolha **Propriedades**
   10. Selecione Olá **funções de servidor** página
   11. Verificar Olá caixa próxima toohello **dbcreator** função de servidor
   12. Clique em **OK**
   13. Fechar Olá SQL Server 2015 Management Studio

Verifique se você Olá registro de nome de usuário e senha que você selecionou.  Talvez seja necessário tooassign funções de servidor adicionais ou permissões, dependendo dos requisitos de banco de dados específico.

Olá Node. js aplicativo lê Olá **SQLCONNSTR_MS_TableConnectionString** variável de ambiente para a cadeia de caracteres de conexão de saudação do banco de dados.  Você pode definir essa variável em seu ambiente.  Por exemplo, você pode usar PowerShell tooset essa variável de ambiente:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Saudação de acesso de banco de dados por meio de uma conexão TCP/IP e fornecer um nome de usuário e senha para conexão hello.

### <a name="howto-config-localdev"></a>Como configurar seu projeto para desenvolvimento local
Aplicativos móveis do Azure lê um arquivo JavaScript chamado *azureMobile.js* do sistema de arquivos local hello.  Não use Olá de tooconfigure este arquivo SDK de aplicativos móveis do Azure em produção - usar configurações de aplicativo em hello [portal do Azure] em vez disso.  Olá *azureMobile.js* arquivo deverá exportar um objeto de configuração.  configurações de Hello mais comuns são:

* Configurações do banco de dados
* Configurações de registro em log de diagnóstico
* Configurações de CORS alternativas

Um exemplo *azureMobile.js* arquivo implementando Olá anterior a maneira de configurações de banco de dados:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Recomendamos que você adicione *azureMobile.js* tooyour *. gitignore* arquivo (ou outro controle do código fonte Ignorar arquivo) tooprevent senhas sejam armazenadas na nuvem hello.  Sempre configurar configurações de produção em configurações do aplicativo em Olá [portal do Azure].

### <a name="howto-appsettings"></a>Como definir configurações de aplicativo para seu aplicativo móvel
A maioria das configurações no hello *azureMobile.js* arquivo tem uma configuração de aplicativo equivalente no hello [portal do Azure].  Use o aplicativo de saudação tooconfigure lista a seguir nas configurações do aplicativo:

| Configurações de Aplicativo | *azureMobile.js*  | Descrição | Valores Válidos |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |nome de saudação do aplicativo hello |string |
| **MS_MobileLoggingLevel** |logging.level |Nível de log mínimo de toolog de mensagens |erro, aviso, informações, detalhado, depuração, simples |
| **MS_DebugMode** |depurar |Habilitar ou desabilitar o modo de depuração |verdadeiro, falso |
| **MS_TableSchema** |data.schema |Nome do esquema padrão para tabelas SQL |cadeia de caracteres (padrão: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Habilitar ou desabilitar o modo de depuração |verdadeiro, falso |
| **MS_DisableVersionHeader** |versão (tooundefined conjunto) |Desabilita o cabeçalho Olá X-ZUMO-Server-Version |verdadeiro, falso |
| **MS_SkipVersionCheck** |skipversioncheck |Desabilita a verificação de versão de API do cliente Olá |verdadeiro, falso |

tooset uma configuração de aplicativo:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu aplicativo móvel.
3. folha de configurações de saudação é aberto por padrão. Se ela não abrir, clique em **Configurações**.
4. Clique em **configurações de aplicativo** no menu geral hello.
5. Role toohello seção configurações do aplicativo.
6. Se seu aplicativo definindo já existir, clique em valor Olá Olá aplicativo definindo tooedit Olá valor.
7. Se sua configuração de aplicativo não existir, digite Olá configuração do aplicativo na caixa de chave de saudação e valor Olá na caixa de valor de saudação.
8. Quando você tiver concluído, clique em **Salvar**.

A alteração da maioria das Configurações do Aplicativo requer o reinício do serviço.

### <a name="howto-use-sqlazure"></a>Como usar o Banco de Dados SQL como o armazenamento de dados de produção
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

O uso do Banco de Dados SQL do Azure como armazenamento de dados é idêntico em todos os tipos de aplicativo do Serviço de Aplicativo do Azure. Se você não tiver feito isso ainda, siga essas etapas toocreate um back-end do aplicativo móvel.

1. Faça logon no toohello [portal do Azure].
2. Em hello superior esquerda da janela de saudação, clique em Olá **+ novo** botão > **Web + móvel** > **aplicativo móvel**, em seguida, forneça um nome para seu back-end do aplicativo móvel.
3. Em Olá **grupo de recursos** , digite Olá mesmo nome do seu aplicativo.
4. plano de serviço de aplicativo padrão de saudação é selecionado.  Se você quiser toochange seu plano de serviço de aplicativo, você pode fazer isso clicando Olá plano do serviço de aplicativo > **+ criar novos**.  Forneça um nome do novo plano do serviço de aplicativo hello e selecione um local apropriado.  Clique em preço hello e selecione um preço apropriado para o serviço de saudação. Selecione **exibir todos os** tooview preços mais opções, como **livre** e **compartilhado**.  Depois que você selecionou o tipo de preço, clique em Olá **selecione** botão.  Em Olá **plano de serviço de aplicativo** folha, clique em **Okey**.
5. Clique em **Criar**. O provisionamento de um back-end de aplicativo móvel pode levar alguns minutos.  Depois de back-end de aplicativo móvel Olá é configurado, o portal Olá abre Olá **configurações** folha de back-end de aplicativo móvel hello.

Depois de back-end de aplicativo móvel Olá é criado, você pode escolher tooeither se conectar a um SQL database tooyour aplicativo móvel back-end existente ou criar um novo banco de dados SQL.  Nesta seção, criamos um banco de dados SQL.

> [!NOTE]
> Se você já tiver um banco de dados em Olá mesmo local como back-end de aplicativo móvel hello, você pode optar por **usar um banco de dados** e, em seguida, selecione o banco de dados. uso de saudação do banco de dados em um local diferente não é recomendado devido a latências mais altas.
>
>

1. No hello novo aplicativo móvel back-end, clique em **configurações** > **aplicativo móvel** > **dados** > **+ adicionar**.
2. Em Olá **Adicionar conexão de dados** folha, clique em **banco de dados SQL - definir configurações obrigatórias** > **criar um novo banco de dados**.  Insira o nome de saudação do novo banco de dados de saudação em Olá **nome** campo.
3. Clique em **Servidor**.  Em Olá **novo servidor** folha, digite um nome de servidor exclusivo no hello **nome do servidor** campo e fornecer um adequado **logon de administrador do servidor** e **senha**.  Certifique-se de **permitir servidor de tooaccess de serviços do azure** é verificada.  Clique em **OK**.

    ![Criar um Banco de Dados SQL do Azure][6]
4. Em Olá **novo banco de dados** folha, clique em **Okey**.
5. Em Olá **Adicionar conexão de dados** folha, selecione **cadeia de caracteres de Conexão**, insira o logon de saudação e a senha que você forneceu ao criar o banco de dados de saudação.  Se você usar um banco de dados existente, fornece credenciais de logon de saudação do banco de dados.  Depois de inserir, clique em **OK**.
6. Em Olá **Adicionar conexão de dados** folha novamente, clique em **Okey** o banco de dados do toocreate hello.

<!--- END OF ALTERNATE INCLUDE -->

Criação de banco de dados de saudação pode levar alguns minutos.  Saudação de uso **notificações** progresso de saudação toomonitor área de implantação de saudação.  Não andamento até que o banco de dados de saudação foi implantado com êxito.  Uma vez implantado com êxito, uma cadeia de caracteres de Conexão é criada para a instância de banco de dados SQL Olá em suas configurações do aplicativo de back-end móvel.  Você pode ver essa configuração de aplicativo no hello **configurações** > **configurações do aplicativo** > **cadeias de caracteres de Conexão**.

### <a name="howto-tables-auth"></a>Como: exigir autenticação para acesso tootables
Se você quiser toouse autenticação do serviço de aplicativo com o ponto de extremidade do hello tabelas, você deve configurar autenticação do serviço de aplicativo no hello [portal do Azure] primeiro.  Para obter mais detalhes sobre como configurar a autenticação em um serviço de aplicativo do Azure, examine Olá guia de configuração para o provedor de identidade Olá pretende toouse:

* [Como tooconfigure autenticação do Active Directory do Azure]
* [Como tooconfigure autenticação do Facebook]
* [Como tooconfigure autenticação do Google]
* [Como tooconfigure Microsoft Authentication]
* [Como tooconfigure autenticação do Twitter]

Cada tabela tem uma propriedade de acesso que pode ser usado toocontrol acesso toohello tabela.  saudação de exemplo a seguir mostra uma tabela estaticamente definida com autenticação necessária.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

propriedade de acesso Olá pode assumir um dos três valores

* *anônimo* indica que o aplicativo de cliente hello é permitido tooread dados sem autenticação
* *autenticado* indica que o aplicativo de cliente hello deve enviar um token de autenticação válido com a solicitação de saudação
* *desabilitado* indica que essa tabela está desabilitada no momento

Se a propriedade de acesso de saudação não estiver definida, o acesso não autenticado é permitido.

### <a name="howto-tables-getidentity"></a>Como usar declarações de autenticação com as tabelas
Você pode configurar várias declarações que são solicitadas durante a configuração da autenticação.  Essas declarações normalmente não estão disponíveis por meio de saudação `context.user` objeto.  No entanto, eles podem ser recuperados usando Olá `context.user.getIdentity()` método.  Olá `getIdentity()` método retorna uma promessa resolvida tooan objeto.  objeto Olá é organizado pelo método de autenticação (facebook, google, twitter, conta da Microsoft ou aad).

Por exemplo, se você configurar a autenticação da Microsoft Account e declaração de endereços de email de saudação de solicitação, você pode adicionar o registro de toohello de endereço de email de saudação com hello controlador da tabela a seguir:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee quais declarações estão disponíveis, use uma saudação de tooview do navegador da web `/.auth/me` ponto de extremidade do seu site.

### <a name="howto-tables-disabled"></a>Como: operações de tabela desabilitar acesso toospecific
Em adição tooappearing na tabela Olá, propriedade de acesso de saudação pode ser usado toocontrol as operações individuais.  Há quatro operações:

* *ler* é a operação obter RESTful Olá na tabela de saudação
* *Inserir* é Olá POST RESTful operação na tabela de saudação
* *atualizar* é uma operação de PATCH RESTful Olá em tabela Olá
* *Excluir* é a operação Excluir RESTful Olá na tabela de saudação

Por exemplo, você poderá tooprovide uma tabela não autenticada somente leitura:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Como: ajustar a consulta de saudação que é usada com operações de tabela
Um requisito comum para operações de tabela é tooprovide uma exibição restrita do dados saudação.  Por exemplo, você pode fornecer uma tabela que é marcada com hello autenticado a ID de usuário, de modo que você pode apenas ler ou atualizar seus próprios registros.  Olá definição da tabela a seguir fornece essa funcionalidade:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

As operações que normalmente executam uma consulta têm uma propriedade de consulta que você pode ajustar com um cláusula where. Olá consulta propriedade é um [QueryJS] objeto tooconvert usado um toosomething de consulta OData que Olá dados back-end pode processar.  Para casos de igualdade simples (como Olá precedentes), um mapa pode ser usado. Você também pode adicionar cláusulas SQL específicas:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Como configurar a exclusão reversível em uma tabela
A Exclusão Reversível não exclui registros.  Em vez disso, ele marca como excluídos no banco de dados de saudação definindo Olá excluído tootrue de coluna.  Olá SDK de aplicativos móveis do Azure remove automaticamente registros excluídos por software de resultados, a menos que Olá SDK de cliente móveis usa IncludeDeleted().  tooconfigure excluir uma tabela para o software, definir Olá `softDelete` propriedade no arquivo de definição de tabela hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Você deve estabelecer um mecanismo para limpar registros, seja usando aplicativo cliente, trabalho Web, Azure Function ou API personalizada.

### <a name="howto-tables-seeding"></a>Como propagar seu banco de dados com dados
Ao criar um novo aplicativo, talvez você queira tooseed uma tabela com dados.  Isso pode ser feito no arquivo de JavaScript de definição de tabela de saudação da seguinte maneira:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

A propagação de dados é feita apenas quando Olá tabela é criada por Olá SDK de aplicativos móveis do Azure.  Se a tabela de saudação já existir no banco de dados Olá, nenhum dado é injetado em tabela hello.  Se o esquema dinâmico está ativada, o esquema é inferido do hello propagado dados.

É recomendável que você chamar explicitamente Olá `tables.initialize()` tabela de saudação do método toocreate quando Olá execução é iniciada.

### <a name="Swagger"></a>Como habilitar o suporte para o Swagger
Os Aplicativos Móveis do Serviço de Aplicativo do Azure vêm com suporte interno para o [Swagger] .  tooenable Swagger suporte, primeiro instale Olá swagger-interface do usuário como uma dependência:

    npm install --save swagger-ui

Uma vez instalado, você pode habilitar o suporte de Swagger no construtor de aplicativos do Azure Mobile hello:

    var mobile = azureMobileApps({ swagger: true });

Você provavelmente só deseja tooenable Swagger suporte nas edições de desenvolvimento.  Faça isso utilizando a configuração do aplicativo `NODE_ENV` :

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Olá ponto de extremidade de swagger está localizado em http://*yoursite*.azurewebsites.net/swagger.  Você pode acessar Olá Swagger da interface do usuário por meio de saudação `/swagger/ui` ponto de extremidade.  Se você escolher autenticação toorequire em todo o seu aplicativo, Swagger produz um erro.  Para obter melhores resultados, escolha solicitações tooallow não autenticado no hello autenticação do serviço de aplicativo do Azure / configurações de autorização, em seguida, controlar autenticação usando Olá `table.access` propriedade.

Você também pode adicionar Olá Swagger opção tooyour `azureMobile.js` arquivo se desejar Swagger suporte somente ao desenvolver localmente.

## <a name="a-namepushpush-notifications"></a><a name="push">Notificações por Push
Aplicativos móveis integra tooenable de Hubs de notificação do Azure você toosend direcionado toomillions de notificações por push de dispositivos em todas as plataformas principais. Usando Hubs de notificação, você pode enviar por push tooiOS notificações, dispositivos Android e Windows. toolearn mais sobre tudo o que você podem fazer com os Hubs de notificação, consulte [visão geral de Hubs de notificação](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Como enviar notificações por push
saudação de código a seguir mostra como toouse Olá push objeto toosend uma difusão por push a dispositivos de iOS tooregistered notificação:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Ao criar um registro de envio por push do modelo de cliente Olá, em vez disso, você pode enviar uma toodevices de mensagem de envio por push do modelo em todas as plataformas com suporte. Olá mostrado no código a seguir como toosend uma notificação de modelo:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Como: enviar por push notificações tooan autenticado usando marcas de usuário
Quando um usuário autenticado se registra para notificações de push, uma marca de identificação do usuário é adicionada automaticamente toohello registro. Usando essa marca, você pode enviar por push dispositivos de tooall notificações registrados por um usuário específico. Olá código a seguir obtém Olá SID do usuário que fez a solicitação de saudação e envia um registro de dispositivo tooevery de notificação do modelo por push para o usuário:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Ao se registrar para notificações por push de um cliente autenticado, verifique se a autenticação foi concluída antes de tentar o registro.

## <a name="CustomAPI"></a> APIs personalizadas
### <a name="howto-customapi-basic"></a>Como definir uma API personalizada
Além disso toohello de acesso a dados API pelo ponto de extremidade de /tables hello, aplicativos móveis do Azure pode fornecer a cobertura de API personalizada.  APIs personalizadas são definidas em um definições de tabela de toohello de maneira semelhante e pode acessar todos os Olá mesmo recursos, incluindo autenticação.

Se você quiser toouse autenticação do serviço de aplicativo com uma API personalizada, você deve configurar autenticação do serviço de aplicativo no hello [portal do Azure] primeiro.  Para obter mais detalhes sobre como configurar a autenticação em um serviço de aplicativo do Azure, examine Olá guia de configuração para o provedor de identidade Olá pretende toouse:

* [Como tooconfigure autenticação do Active Directory do Azure]
* [Como tooconfigure autenticação do Facebook]
* [Como tooconfigure autenticação do Google]
* [Como tooconfigure Microsoft Authentication]
* [Como tooconfigure autenticação do Twitter]

APIs personalizadas são definidas em grande parte Olá mesma maneira que Olá API de tabelas.

1. Crie um diretório **api**
2. Criar um arquivo de JavaScript da definição de API no hello **api** directory.
3. Use Olá importação método tooimport Olá **api** directory.

Aqui está a definição de api de protótipo Olá com base em amostra de aplicativo basic Olá que usamos anteriormente.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Vejamos um exemplo de API que retorna a data de servidor de saudação usando Olá *Date.now()* método.  Aqui está o arquivo de api/date.js hello:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Cada parâmetro é uma saudação RESTful verbos padrão - GET, POST, PATCH ou DELETE.  método Hello é um padrão [ExpressJS Middleware] função que envia saída de hello necessário.

### <a name="howto-customapi-auth"></a>Como: exigir autenticação de API personalizada do acesso tooa
SDK de aplicativos móveis do Azure implementa a autenticação em Olá mesma forma para o ponto de extremidade do hello tabelas e APIs personalizadas.  Para adicionar autenticação toohello API desenvolvido na seção anterior hello, adicione um **acesso** propriedade:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

Você também pode especificar a autenticação em operações específicas:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Olá mesmo token que é usado para o ponto de extremidade do hello tabelas deve ser usado para APIs personalizadas que requer autenticação.

### <a name="howto-customapi-auth"></a>Como manipular transferências de arquivos grandes
SDK de aplicativos móveis do Azure usa Olá [corpo analisador middleware](https://github.com/expressjs/body-parser) tooaccept e decodificar o conteúdo do corpo no seu envio.  Você pode pré-configurar carregamentos de arquivo maior do analisador de corpo tooaccept:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

arquivo Hello é codificada antes da transmissão de base 64.  Isso aumenta o tamanho de saudação do carregamento real hello (e hello, portanto, você deve considerar de tamanho).

### <a name="howto-customapi-sql"></a>Como executar instruções SQL personalizadas
Olá SDK de aplicativos móveis do Azure permite acesso toohello contexto inteiro por meio do objeto de solicitação hello, permitindo que você tooexecute parametrizadas provedor de dados definidas SQL instruções toohello facilmente:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Depuração, Tabelas Fáceis e APIs Fáceis
### <a name="howto-diagnostic-logs"></a>Como depurar, diagnosticar e solucionar problemas dos Aplicativos Móveis do Azure
saudação do serviço de aplicativo do Azure fornece vários depuração e solução de problemas técnicas para aplicativos Node. js.
Consulte toohello artigos tooget iniciado no seu back-end node. js móvel de solução de problemas a seguir:

* [Monitorando um Serviço de Aplicativo do Azure]
* [Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]
* [Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]

Aplicativos Node.js têm acesso tooa ampla variedade de ferramentas de log de diagnóstico.  Internamente, Olá usa o SDK do Azure Mobile aplicativos Node.js [Winston] para log de diagnóstico.  Registro em log é habilitado automaticamente, habilitando o modo de depuração ou por configuração Olá **MS_DebugMode** tootrue de configuração do aplicativo no hello [portal do Azure]. Os logs gerados aparecem no hello Logs de diagnóstico em Olá [portal do Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Como: trabalhar com tabelas fácil Olá portal do Azure
Tabelas fácil no portal de saudação lhe permitem criar e trabalhar com o direito de tabelas no portal de saudação. Você ainda pode editar operações de tabela usando Olá Editor de aplicativo de serviço.

Quando você clica em **Tabelas fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir uma tabela. Você também pode ver os dados na tabela de saudação.

![Trabalhar com Tabelas fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Olá a comandos a seguir estão disponíveis na barra de comandos Olá para uma tabela:

* **Alterar permissões** - modificar Olá permissão de leitura, inserção, atualização e excluir operações na tabela de saudação.
  As opções são tooallow o acesso anônimo, autenticação toorequire ou toodisable todos os acessos toohello operação.
* **Editar script** -arquivo de script hello para tabela Olá é aberto no hello Editor de aplicativo de serviço.
* **Gerenciar o esquema** - adicionar ou excluir colunas ou alterar o índice da tabela de saudação.
* **Limpar tabela** -trunca a uma tabela existente ser excluir todas as linhas de dados, mas deixar o esquema de saudação inalterado.
* **Excluir linhas** : exclua linhas individuais de dados.
* **Exibir logs de streaming** -conecta você toohello serviço de log para o site de streaming.

### <a name="work-easy-apis"></a>Como: trabalhar com APIs fácil Olá portal do Azure
APIs de fácil no portal de saudação permitem que você criar e trabalhar com o direito APIs personalizado no portal de saudação. Você pode editar scripts de API usando Olá Editor de aplicativo de serviço.

Quando você clica em **APIs fáceis** em suas configurações de site de back-end, você pode adicionar, modificar ou excluir um ponto de extremidade de API.

![Trabalhar com APIs fáceis](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

No portal de hello, alterar permissões de acesso de saudação para uma determinada ação HTTP, editar o arquivo de script hello API no Editor de serviço de aplicativo ou exibir logs de streaming hello.

### <a name="online-editor"></a>Como: editar o código no hello Editor de aplicativo de serviço
Olá portal do Azure permite que você edite seus arquivos de script de back-end node. js em Olá Editor de aplicativo de serviço sem a necessidade de baixar o computador local do hello projeto tooyour. arquivos de script tooedit no editor online hello:

1. Na folha do back-end de Aplicativo Móvel, clique em **Todas as configurações** > em **Tabelas fáceis** ou **APIs fáceis**, clique em uma tabela ou API e clique em **Editar script**. arquivo de script Hello é aberto em Olá Editor de aplicativo de serviço.

    ![Editor de Serviço de Aplicativo](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Verifique o arquivo de código toohello alterações no editor online hello. As alterações são salvas automaticamente enquanto você digita.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Início rápido do cliente Android]: app-service-mobile-android-get-started.md
[Início rápido do cliente Apache Cordova]: app-service-mobile-cordova-get-started.md
[Início rápido do cliente iOS]: app-service-mobile-ios-get-started.md
[Início rápido do cliente Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Início rápido do cliente Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Início rápido do cliente Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Início rápido de cliente Windows Store]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[a sincronização de dados offline]: app-service-mobile-offline-data-sync.md
[Como tooconfigure autenticação do Active Directory do Azure]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Como tooconfigure autenticação do Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Como tooconfigure autenticação do Google]: app-service-mobile-how-to-configure-google-authentication.md
[Como tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Como tooconfigure autenticação do Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guia de implantação do Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-deploy.md
[Monitorando um Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-monitor.md
[Habilitar o registro em log de diagnósticos no Serviço de Aplicativo do Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Solucionar problemas de um Serviço de Aplicativo do Azure no Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[especificar Olá versão do nó]: ../nodejs-specify-node-version-azure-apps.md
[usar módulos de nó]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portal do Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promessa]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp exemplo no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[exemplo todo no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[diretório de exemplos no GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node. js Tools 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node. js pacote]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
