---
title: aaaCreate uma API REST no Azure com o ASP.NET e o banco de dados SQL | Microsoft Docs
description: "Um tutorial que ensina como toodeploy um aplicativo que usa Olá ASP.NET Web API tooan aplicativo web do Azure usando o Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Criar um serviço REST usando a API Web ASP.NET e o Banco de Dados SQL no Serviço de Aplicativo do Azure
Este tutorial mostra como toodeploy uma ASP.NET web aplicativo tooan [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando o Assistente de publicar Web Olá no Visual Studio 2013 ou o Visual Studio 2013 Community Edition. 

Você pode abrir uma conta do Azure gratuitamente e se você ainda não tiver o Visual Studio 2013, Olá SDK instalará automaticamente o Visual Studio 2013 para Web Express. Portanto, você pode começar a desenvolver para o Azure de maneira totalmente gratuita.

Este tutorial pressupõe que você não tem nenhuma experiência anterior com o Azure. Ao concluir este tutorial, você terá um aplicativo da web simples para cima e em execução na nuvem hello.

Você aprenderá a:

* Como tooenable sua máquina de desenvolvimento do Azure instalando Olá SDK do Azure.
* Como toocreate um Visual Studio ASP.NET MVC 5 do projeto e publicá-lo tooan aplicativo do Azure.
* Como toouse Olá ASP.NET Web API tooenable chamadas de API Restful.
* Como toouse um SQL banco de dados toostore dados no Azure.
* Como o aplicativo toopublish atualiza tooAzure.

Será possível compilar um aplicativo da web de lista de contatos simples que se baseia no ASP.NET MVC 5 e usa hello ADO.NET Entity Framework para acesso de banco de dados. Olá seguinte ilustração mostra Olá concluída aplicativo:

![captura de tela do site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Criar projeto Olá
1. Inicie o Visual Studio 2013.
2. De saudação **arquivo** menu clique **novo projeto**.
3. Em Olá **novo projeto** caixa de diálogo caixa, expanda **Visual C#** e selecione **Web** e, em seguida, selecione **aplicativo Web ASP.NET**. Nome do aplicativo hello **ContactManager** e clique em **Okey**.
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. Em Olá **novo projeto ASP.NET** caixa de diálogo, selecione Olá **MVC** modelo, verifique **API da Web** e, em seguida, clique em **alterar autenticação**.
5. Em Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **Okey**.
   
    ![Sem Autenticação](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    aplicativo de exemplo Hello que você está criando não tenha recursos que exigem toolog usuários em. Para obter informações sobre como tooimplement recursos de autenticação e autorização, consulte Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial. 
6. Em Olá **novo projeto ASP.NET** caixa de diálogo, Olá se tornar **Host na nuvem de saudação** está marcada e clique em **Okey**.

Se você não tiver entrado anteriormente no tooAzure, será solicitada toosign no.

1. Assistente de configuração de saudação sugerirá um nome exclusivo baseado no *ContactManager* (consulte a imagem de saudação abaixo). Selecione uma região perto de você. Você pode usar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Olá menor latência Datacenter. 
2. Se você não criou um servidor de banco de dados antes, selecione **Criar novo servidor**, digite um nome de usuário de banco de dados e uma senha.
   
    ![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Se você tiver um servidor de banco de dados, use esse toocreate um novo banco de dados. Servidores de banco de dados são um recurso precioso e geralmente você deseja toocreate vários bancos de dados Olá mesmo servidor de teste e desenvolvimento em vez de criar um servidor de banco de dados por banco de dados. Verifique se o seu site da web e o banco de dados estão em hello mesma região.

![Configurar o site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Definir Olá cabeçalho e rodapé
1. Em **Solution Explorer**, expanda Olá *exibições \ compartilhadas* pasta e abra Olá *cshtml* arquivo.
   
    ![_Layout.cshtml no Gerenciador de Soluções][newapp004]
2. Substitua o conteúdo de saudação do hello *Views\Shared_Layout.cshtml* arquivo com hello código a seguir:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

marcação de saudação acima do nome do aplicativo hello alterações de "My App ASP.NET" muito "gerente do contato" e remove links Olá muito**início**, **sobre** e **entre em contato com**.

### <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
1. Pressione CTRL + F5 aplicativo de hello de toorun.
   home page do aplicativo Hello aparece no navegador padrão de saudação.
    ![página de início da lista de tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Isso é tudo o que você precisa toodo para aplicativo de hello toocreate agora que você implantará tooAzure. Posteriormente, você adicionará a funcionalidade do banco de dados.

## <a name="deploy-hello-application-tooazure"></a>Implantar Olá aplicativo tooAzure
1. No Visual Studio, clique com botão direito Olá em **Solution Explorer** e selecione **publicar** Olá no menu de contexto.
   
    ![Publicar no menu de contexto do projeto][PublishVSSolution]
   
    Olá **Publicar Web** assistente é aberto.
2. Clique em **Publicar**.

![Guia Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

O Visual Studio inicia o processo de saudação de copiar Olá arquivos toohello servidor do Azure. Olá **saída** janela mostra quais ações de implantação foram realizadas e relata a conclusão bem-sucedida da implantação de saudação.

1. navegador padrão de saudação é aberto automaticamente toohello URL do site Olá implantado.
   
   aplicativo Hello que você criou agora está em execução na nuvem hello.
   
   ![página de início da lista de tooDo em execução no Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Adicionar um aplicativo de toohello do banco de dados
Em seguida, você vai atualizar Olá MVC aplicativo tooadd Olá capacidade toodisplay e atualizar contatos e armazenar dados de saudação em um banco de dados. aplicativo Hello usar tooread e o banco de dados do Entity Framework toocreate Olá Olá e atualizar dados no banco de dados de saudação.

### <a name="add-data-model-classes-for-hello-contacts"></a>Adicionar classes de modelo de dados para os contatos Olá
Você começa criando um modelo de dados simples no código.

1. Em **Solution Explorer**, pasta de modelos de saudação, clique **adicionar**e, em seguida, **classe**.
   
    ![Adicionar Classe no menu de contexto da pasta Modelos][adddb001]
2. Em Olá **Adicionar Novo Item** caixa de diálogo, o nome hello novo arquivo de classe *Contact.cs*e, em seguida, clique em **adicionar**.
   
    ![Caixa de diálogo Adicionar Novo Item][adddb002]
3. Substitua o conteúdo de saudação do arquivo de Contacts.cs de saudação com hello código a seguir.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

Olá **entre em contato com** classe define dados hello serão armazenados para cada contato, além de uma chave primária, a ID de contato, que é necessária para o banco de dados de saudação. Você pode obter mais informações sobre modelos de dados em Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Criar páginas da web que permitem toowork de usuários do aplicativo com contatos Olá
Olá recurso do ASP.NET MVC Olá scaffolding pode gerar automaticamente código que executa a criar, ler, atualizar e excluir ações (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Adicionar um controlador e uma exibição para dados de saudação
1. Em **Solution Explorer**, expanda a pasta de controladores de saudação.
2. Criar projeto Olá **(Ctrl + Shift + B)**. (Você deve criar o projeto de saudação antes de usar o mecanismo de scaffolding.) 
3. Pasta de controladores de saudação de mouse e clique em **adicionar**e, em seguida, clique em **controlador**.
   
    ![Adicionar Controlador no menu de contexto da pasta Controladores][addcode001]
4. Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC com modos de exibição usando o Entity Framework** e clique em **adicionar**.
   
   ![Adicionar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Defina o nome do controlador Olá muito**HomeController**. Selecione **Contato** como a classe de modelo. Clique em Olá **novo contexto de dados** botão e aceite o padrão de hello "ContactManager.Models.ContactManagerContext" hello **novo tipo de contexto de dados**. Clique em **Adicionar**.

    Uma caixa de diálogo solicitará que você: "um arquivo com nome hello HomeController já existente. Você deseja tooreplace-lo? ". Clique em **Sim**. Nós são substituindo Olá início controlador que foi criado com o novo projeto de saudação. Usaremos Olá novo início controlador para nossa lista de contatos.

    O Visual Studio cria métodos do controlador e modos de exibição para as operações de banco de dados CRUD para objetos **Contact** .

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Permitir as migrações, criar hello banco de dados, adicionar dados de exemplo e um inicializador de dados
Olá próxima tarefa é Olá tooenable [migrações do Code First](http://curah.microsoft.com/55220) recurso no banco de dados do pedido toocreate Olá baseada no modelo de dados de saudação criado por você.

1. Em Olá **ferramentas** menu, selecione **Gerenciador de biblioteca de pacote** e **Package Manager Console**.
   
    ![Console do Gerenciador de Pacotes no menu Ferramentas][addcode008]
2. Em Olá **Package Manager Console** janela, digite Olá comando a seguir:
   
        enable-migrations 
   
    Olá **enable-migrations** comando cria um *migrações* pasta e o coloca na pasta um *Configuration.cs* arquivo que você pode editar tooconfigure migrações. 
3. Em Olá **Package Manager Console** janela, digite Olá comando a seguir:
   
        add-migration Initial
   
    Olá **inicial de migração adicionar** comando gera uma classe denominada  **&lt;date_stamp&gt;inicial** que cria o banco de dados de saudação. Olá primeiro parâmetro ( *inicial* ) é arbitrário e usada toocreate Olá nome do arquivo hello. Você pode ver os novos arquivos de classe Olá no **Gerenciador de soluções**.
   
    Em Olá **inicial** classe hello **backup** método cria a tabela de contatos hello e hello **para baixo** descarta método (usado quando você deseja que o estado anterior do tooreturn toohello).
4. Olá abrir *Migrations\Configuration.cs* arquivo. 
5. Adicione Olá namespaces a seguir. 
   
         using ContactManager.Models;
6. Substituir saudação *semente* método com hello código a seguir:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    Esse código acima será inicializar banco de dados de saudação com informações de contato de saudação. Para obter mais informações sobre a propagação do banco de dados hello, consulte [bancos de dados de depuração Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. Em Olá **Package Manager Console** digite Olá comando:
   
        update-database
   
    ![Comandos do Console do Gerenciador de Pacotes][addcode009]
   
    Olá **Atualizar banco de dados** executa Olá primeiro migração que cria o banco de dados de saudação. Por padrão, o banco de dados de saudação é criado como um banco de dados do SQL Server Express LocalDB.
8. Pressione CTRL + F5 aplicativo de hello de toorun. 

aplicativo Hello mostra dados de propagação de saudação e fornece edição, detalhes e links de exclusão.

![Exibição do MVC de dados][rxz3]

## <a name="edit-hello-view"></a>Editar saudação exibição
1. Olá abrir *Views\Home\Index.cshtml* arquivo. Na próxima etapa de hello, substituiremos marcação Olá gerado pelo código que usa [jQuery](http://jquery.com/) e [Knockout. js](http://knockoutjs.com/). Esse novo código recupera a lista de contatos de saudação do usando a API da web e JSON e, em seguida, associa Olá entre em contato com dados toohello da interface do usuário usando Knockout. js. Para obter mais informações, consulte Olá [próximas etapas](#nextsteps) seção Olá final deste tutorial. 
2. Substitua o conteúdo de saudação do arquivo hello com hello código a seguir.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Pasta de conteúdo de saudação de mouse e clique em **adicionar**e, em seguida, clique em **Novo Item...** .
   
    ![Adicionar folha de estilos no menu de contexto da pasta Content][addcode005]
4. Em Olá **Adicionar Novo Item** caixa de diálogo, digite **estilo** Olá caixa de pesquisa à direita superior e, em seguida, selecione **folha de estilo**.
    ![Caixa de diálogo Adicionar Novo Item][rxStyle]
5. Arquivo de saudação do nome *Contacts.css* e clique em **adicionar**. Substitua o conteúdo de saudação do arquivo hello com hello código a seguir.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    Usaremos esta folha de estilos para layout hello, cores e estilos usados no aplicativo de contato do Gerenciador de saudação.
6. Olá abrir *App_Start\BundleConfig.cs* arquivo.
7. Adicionar Olá Olá de tooregister de código a seguir [Knockout](http://knockoutjs.com/index.html "KO") plug-in.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Este exemplo usando knockout toosimplify dinâmico código JavaScript que trata os modelos de tela hello.
8. Modificar Olá Olá de tooregister de entrada de conteúdo/css *contacts.css* folha de estilos. Alterar Olá seguinte linha:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Para:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Olá Package Manager Console, a execução Olá comando tooinstall Knockout a seguir.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Adicionar um controlador de interface da Web API Restful Olá
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em Controllers, clique em **Adicionar** e, em seguida, em **Controlador...** 
2. Em Olá **adicionar Scaffold** caixa de diálogo, digite **Web 2 controlador API com ações, usando o Entity Framework** e, em seguida, clique em **adicionar**.
   
    ![Adicionar a API do controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. Em Olá **Adicionar controlador** caixa de diálogo, digite "ContactsController" como o nome do controlador. Selecione "Contato (ContactManager.Models)" para Olá **classe modelo**.  Manter o valor padrão Olá Olá **classe de contexto de dados**. 
4. Clique em **Adicionar**.

### <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
1. Pressione CTRL + F5 aplicativo de hello de toorun.
   
    ![Página de índice][intro001]
2. Digite um contato e clique em **Adicionar**. aplicativo Hello retorna home page do toohello e exibe o contato Olá inserido.
   
    ![Página de índice com itens da lista de tarefas pendentes][addwebapi004]
3. No navegador de hello, acrescente **/api/contatos** toohello URL.
   
    URL de saudação resultante será parecida com a api/http://localhost:1234/contatos. Olá web RESTful API que você adicionou retorna contatos Olá armazenado. Firefox e no Chrome, exibirá dados de saudação em formato XML.
   
    ![Página de índice com itens da lista de tarefas pendentes][rxFFchrome]

    IE será solicitará que você tooopen ou salvar contatos hello.

    ![Caixa de diálogo Salvar API Web][addwebapi006]


    Você pode abrir hello retornada contatos no bloco de notas ou em um navegador.

    Essa saída pode ser consumida por outro aplicativo, como um aplicativo ou uma página da web móvel.

    ![Caixa de diálogo Salvar API Web][addwebapi007]

    **Aviso de segurança**: neste ponto, seu aplicativo é inseguro e vulnerável tooCSRF ataque. Posteriormente no tutorial Olá removeremos essa vulnerabilidade. Para obter mais informações, confira [Evitando ataques de solicitação intersite forjada (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Adicionar proteção XSRF
Falsificação de solicitação entre sites (também conhecido como XSRF ou CSRF) é um ataque contra aplicativos web hospedados no qual um site mal-intencionado pode influenciar a interação de saudação entre um navegador de cliente e um site confiada pelo navegador. Esses ataques são possibilitados como navegadores da web enviará os tokens de autenticação automaticamente com o site de tooa cada solicitação. exemplo canônico Hello é um cookie de autenticação, como ASP. Tíquete de autenticação de formulários do NET. No entanto, os sites que usam qualquer mecanismo de autenticação persistente (como a autenticação do Windows, Basic e assim por diante) podem ser alvos desses ataques.

Um ataque XSRF é diferente de um ataque de phishing. Ataques de phishing requerem interação da vítima hello. Em um ataque de phishing, um site mal-intencionado imitar o site de destino hello e vítima Olá enganar fornecendo invasor de toohello informações confidenciais. Em um ataque de XSRF, geralmente há nenhuma interação necessárias da vítima hello. Em vez disso, invasor Olá depende navegador Olá enviar automaticamente todos os site de destino de toohello cookies relevantes.

Para obter mais informações, consulte Olá [Abrir projeto de segurança do aplicativo Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **ContactManager**, clique em **Adicionar** e em **Classe**.
2. Arquivo de saudação do nome *ValidateHttpAntiForgeryTokenAttribute.cs* e adicione Olá código a seguir:
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Adicione o seguinte Olá *usando* toohello de instrução de contratos de controlador para que você tenha acesso toohello **[ValidateHttpAntiForgeryToken]** atributo.
   
        using ContactManager.Filters;
4. Adicionar Olá **[ValidateHttpAntiForgeryToken]** toohello métodos de postagem de saudação do atributo **ContactsController** tooprotect-lo contra ameaças XSRF. Você irá adicionar toohello "PutContact", "PostContact" e **DeleteContact** métodos de ação.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Saudação de atualização *Scripts* seção Olá *Views\Home\Index.cshtml* tokens de XSRF tooinclude código tooget saudação do arquivo.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Publicar Olá tooAzure de atualização de aplicativo e banco de dados SQL
aplicativo de hello toopublish, você repetir procedimento Olá que você seguiu anteriormente.

1. Em **Solution Explorer**, projeto Olá clique com botão direito e selecione **publicar**.
   
    ![Publicar][rxP]
2. Clique em Olá **configurações** guia.
3. Em **ContactsManagerContext(ContactsManagerContext)**, clique em Olá **v** ícone toochange *cadeia de caracteres de conexão remota* toohello cadeia de caracteres de conexão para contato Olá banco de dados. Clique em **ContactDB**.
   
    ![Configurações](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Marque a caixa Olá para **executar migrações do Code First (executado na inicialização do aplicativo)**.
5. Clique em **Avançar** e, em seguida, em **Visualizar**. O Visual Studio exibe uma lista de arquivos de saudação que serão adicionados ou atualizados.
6. Clique em **Publicar**.
   Após a conclusão da implantação hello, o navegador de saudação abre toohello home page do aplicativo hello.
   
    ![Página de índice sem contatos][intro001]
   
    Olá Visual Studio publicar cadeia de caracteres de conexão do processo configurado automaticamente Olá no hello implantado *Web. config* banco de dados do arquivo toopoint toohello SQL. Ele também configurado migrações do Code First tooautomatically Olá Atualizar banco de dados toohello versão mais recente primeiro aplicativo de saudação tempo hello acessa o banco de dados de saudação após a implantação.
   
    Como resultado, essa configuração Code First criou Olá banco de dados, executando código Olá em Olá **inicial** classe que você criou anteriormente. Que este Olá primeiro tempo Olá aplicativo tentado tooaccess Olá banco de dados após a implantação.
7. Insira um contato como você fez quando você executou Olá aplicativo localmente, tooverify implantação de banco de dados foi bem-sucedida.

Quando você vir esse item Olá que inserir é salva e aparece na página de contato do Gerenciador de saudação, você saberá que foram armazenado no banco de dados de saudação.

![Página de índice com contatos][addwebapi004]

aplicativo Hello está em execução na nuvem hello, usando o banco de dados SQL toostore seus dados. Depois de concluir o teste o aplicativo hello no Azure, exclua-o. aplicativo Hello é público e não tem acesso de toolimit um mecanismo.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Outra maneira como toostore os dados em um aplicativo do Azure serão toouse armazenamento do Azure, que fornecem armazenamento de dados não relacionais no formato de saudação de blobs e tabelas. Olá links a seguir fornece mais informações sobre a API da Web, o ASP.NET MVC e o Windows Azure.

* [Introdução ao Entity Framework usando MVC][EFCodeFirstMVCTutorial]
* [Introdução tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Sua primeira API Web ASP.NET](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Depurando WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Este aplicativo de exemplo do tutorial e hello foi escrito por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) com a Ajuda de Tom Dykstra e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Deixe comentários sobre o que você gostou ou o que você gostaria que toosee aprimorado, não apenas sobre tutorial Olá em si, mas também sobre produtos Olá demonstra. Seus comentários nos ajudarão a priorizar melhorias. Estamos especialmente interessados em saber quantos interesse lá está em mais automação para o processo de saudação de configuração e implantação de banco de dados de associação de saudação. 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

