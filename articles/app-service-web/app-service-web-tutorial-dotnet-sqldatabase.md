---
title: um aplicativo ASP.NET no Azure com o banco de dados SQL do aaaBuild | Microsoft Docs
description: "Saiba como tooget um ASP.NET aplicativo trabalhando no Azure, com conexão tooa banco de dados SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Compilar um aplicativo ASP.NET no Azure com Banco de Dados SQL

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches. Este tutorial mostra como toodeploy um ASP.NET controladas por dados aplicativo no Azure da web e conectá-lo muito[banco de dados do SQL Azure](../sql-database/sql-database-technical-overview.md). Quando você terminar, você tem um aplicativo ASP.NET em execução no [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) e conectado tooSQL banco de dados.

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um Banco de Dados SQL no Azure
> * Conecte-se um aplicativo ASP.NET tooSQL banco de dados
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Logs de fluxo do Azure tooyour terminal
> * Gerenciar o aplicativo hello em Olá portal do Azure

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

* Instalar [2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello cargas de trabalho a seguir:
  - **Desenvolvimento Web e do ASP.NET**
  - **Desenvolvimento do Azure**

  ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Baixe o exemplo hello

[Baixe o projeto de exemplo hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Extrair (Descompactar) Olá *dotnet-sqldb tutorial master.zip* arquivo.

projeto de exemplo Hello contém básico [ASP.NET MVC](https://www.asp.net/mvc) CRUD (criar-leitura-atualização-exclusão) usando o aplicativo [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Executar o aplicativo hello

Olá abrir *dotnet-sqldb-tutorial-mestre/DotNetAppSqlDb.sln* arquivo no Visual Studio. 

Tipo `Ctrl+F5` toorun Olá aplicativo sem depuração. Olá aplicativo é exibido no navegador padrão. Selecione Olá **criar novo** vincular e criar algumas *tarefas* itens. 

![Caixa de diálogo Novo Projeto ASP .NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Saudação de teste **editar**, **detalhes**, e **excluir** links.

aplicativo Hello usa um tooconnect de contexto do banco de dados com o banco de dados de saudação. Neste exemplo, o contexto de banco de dados de saudação usa uma cadeia de caracteres de conexão chamada `MyDbConnection`. cadeia de caracteres de conexão de saudação é definida no hello *Web. config* arquivo e hello referenciado no *Models/MyDatabaseContext.cs* arquivo. nome de cadeia de caracteres de conexão de saudação é usado posteriormente Olá tooconnect tutorial Olá web do Azure aplicativo tooan banco de dados do SQL Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Publicar tooAzure com o banco de dados SQL

Em Olá **Solution Explorer**, clique com botão direito seu **DotNetAppSqlDb** do projeto e selecione **publicar**.

![Publicar no Gerenciador de Soluções](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.

![Publicar na página de visão geral do projeto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publicação abre Olá **criar serviço de aplicativo** caixa de diálogo, que ajuda a criar todos os Olá recursos do Azure, você precisa toorun seu aplicativo da web ASP.NET no Azure.

### <a name="sign-in-tooazure"></a>Entrar tooAzure

Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **adicionar uma conta**e entre tooyour assinatura do Azure. Se você já entrou em uma conta da Microsoft, verifique se a conta tem sua assinatura do Azure. Se conectado no hello conta da Microsoft não tem a sua assinatura do Azure, clique em tooadd Olá corretas da conta.
   
![Entrar tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Depois de conectado, você está pronto toocreate que Olá a todos os recursos que necessários para seu aplicativo web do Azure nesta caixa de diálogo.

### <a name="configure-hello-web-app-name"></a>Configurar o nome do aplicativo web Olá

Você pode manter o nome do aplicativo web hello gerado ou altere-o nome exclusivo do tooanother (caracteres válidos são `a-z`, `0-9`, e `-`). nome do aplicativo web Hello é usado como parte da URL do saudação padrão para seu aplicativo (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo web). nome do aplicativo web Hello precisa toobe exclusivo entre todos os aplicativos no Azure. 

![Criar caixa de diálogo do serviço de aplicativo](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Avançar muito**grupo de recursos**, clique em **novo**.

![TooResource próximo grupo, clique em novo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Grupo de recursos do nome hello **myResourceGroup**.

> [!NOTE]
> Não clique em **Criar**. É necessário primeiro tooset um banco de dados SQL em uma etapa posterior.

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Avançar muito**plano do serviço de aplicativo**, clique em **novo**. 

Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, configure o novo plano de serviço de aplicativo hello com hello configurações a seguir:

![Criar plano de Serviço de Aplicativo](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Configuração  | Valor sugerido | Para obter mais informações |
| ----------------- | ------------ | ----|
|**Plano do Serviço de Aplicativo**| myAppServicePlan | [Planos do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Localidade**| Europa Ocidental | [Regiões do Azure](https://azure.microsoft.com/regions/) |
|**Tamanho**| Grátis | [Tipos de preço](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Criar uma instância do SQL Server

Antes de criar um banco de dados, é necessário um [servidor lógico do Banco de dados SQL do Azure](../sql-database/sql-database-features.md). Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente.

Selecione **Explorar serviços adicionais do Azure**.

![Configurar o nome do aplicativo Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

Em Olá **serviços** , clique em Olá  **+**  ícone Avançar muito**banco de dados SQL**. 

![Na Olá serviços guia, clique no ícone + Olá tooSQL próximo banco de dados.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

Em Olá **configurar banco de dados SQL** caixa de diálogo, clique em **novo** Avançar muito**do SQL Server**. 

Um nome do servidor único é gerado. Esse nome é usado como parte da URL de padrão de saudação do seu servidor lógico, `<server_name>.database.windows.net`. Ele deve ser exclusivo em todas as instâncias do servidor lógico no Azure. Você pode alterar o nome do servidor de saudação, mas para este tutorial, mantenha o valor de saudação gerada.

Adicione um nome de usuário administrador e a senha e, em seguida, selecione **OK**. Para requisitos de complexidade de senha, consulte [Política de Senha](/sql/relational-databases/security/password-policy).

Lembre desse nome de usuário e senha. Você precisa servidor lógico de saudação toomanage instância mais tarde.

![Criar instância do SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Criar um banco de dados SQL

Em Olá **configurar banco de dados SQL** caixa de diálogo: 

* Mantenha saudação padrão gerado **nome do banco de dados**.
* Em **Nome da Cadeia de Conexão**, digite *MyDbConnection*. Esse nome deve corresponder a cadeia de caracteres de conexão de saudação que é referenciada em *Models/MyDatabaseContext.cs*.
* Selecione **OK**.

![Configurar banco de dados SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Olá **criar serviço de aplicativo** caixa de diálogo mostra os recursos de saudação que você criou. Clique em **Criar**. 

![recursos de saudação que você criou](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Depois que o Assistente de saudação terminar de criar hello recursos do Azure, ela publica seu tooAzure de aplicativo do ASP.NET. Navegador padrão é iniciado com hello URL toohello implantado aplicativo. 

Adicione alguns itens de tarefas.

![Aplicativo ASP.NET publicado no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Parabéns! Seu aplicativo ASP.NET controlado por dados está em execução em tempo real no Serviço de Aplicativo do Azure.

## <a name="access-hello-sql-database-locally"></a>Acessar Olá localmente no banco de dados SQL

O Visual Studio permite explorar e gerenciar seu novo banco de dados SQL facilmente no hello **Pesquisador de objetos do SQL Server**.

### <a name="create-a-database-connection"></a>Criar uma conexão de banco de dados

De saudação **exibição** menu, selecione **Pesquisador de objetos do SQL Server**.

Na parte superior de saudação do **Pesquisador de objetos do SQL Server**, clique em Olá **adicionar SQL Server** botão.

### <a name="configure-hello-database-connection"></a>Configurar conexão do banco de dados de saudação

Em Olá **conectar** caixa de diálogo, expanda Olá **Azure** nó. Todas as suas instâncias de Banco de Dados SQL no Azure são listadas aqui.

Selecione Olá `DotNetAppSqlDb` banco de dados SQL. conexão Olá criado anteriormente é preenchido automaticamente na parte inferior da saudação.

Digite a senha de administrador de banco de dados Olá criado anteriormente e clique em **conectar**.

![Configurar a conexão de Banco de Dados do Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Permitir conexão do cliente a partir de seu computador

Olá **criar uma nova regra de firewall** caixa de diálogo é aberta. Por padrão, sua instância do Banco de dados SQL somente permite conexões dos serviços do Azure, como o aplicativo Web do Azure. tooconnect tooyour de banco de dados, crie uma regra de firewall na instância de banco de dados SQL hello. regra de firewall Olá permite que o endereço IP público de saudação do computador local.

caixa de diálogo Olá já é preenchida com o endereço IP público do seu computador.

Certifique-se de que **Adicionar meu IP do cliente** está selecionado e clique em **OK**. 

![Define o firewall para as instância do Banco de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Depois que o Visual Studio termina de criar a configuração de firewall de saudação para sua instância de banco de dados SQL, sua conexão aparece na **Pesquisador de objetos do SQL Server**.

Aqui, você pode executar operações de banco de dados mais comuns hello, como consultas de execução, criam exibições e procedimentos armazenados e muito mais. 

Clique duas vezes em Olá `Todoes` de tabela e selecione **exibir dados**. 

![Explorar objetos do Banco de Dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Atualizar aplicativo com Migrações do Code First

Você pode usar as ferramentas familiares do hello no Visual Studio tooupdate seu banco de dados e o aplicativo web no Azure. Nesta etapa, você use migrações do Code First no Entity Framework toomake um esquema de banco de dados de tooyour de alteração e publicá-lo tooAzure.

Para obter mais informações sobre como usar as Migrações do Entity Framework Code First, consulte [Introdução ao Entity Framework 6 Code First usando MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Atualizar seu modelo de dados

Abra _Models\Todo.cs_ no editor de códigos de saudação. Adicionar Olá toohello de propriedade a seguir `ToDo` classe:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Executar Migrações do Code First localmente

Execute alguns comandos toomake atualizações tooyour banco de dados local. 

De saudação **ferramentas** menu, clique em **NuGet Package Manager** > **Package Manager Console**.

Em Olá janela do Console do Gerenciador de pacotes, habilite migrações do Code First:

```PowerShell
Enable-Migrations
```

Adicione uma migração:

```PowerShell
Add-Migration AddProperty
```

Atualize o banco de dados local hello:

```PowerShell
Update-Database
```

Tipo `Ctrl+F5` toorun Olá aplicativo. Saudação de teste editar detalhes e criar links.

Se o aplicativo hello carregado sem erros, migrações do Code First foi bem-sucedida. No entanto, a aparência de página ainda Olá mesmo porque a lógica do aplicativo ainda não usando essa nova propriedade. 

### <a name="use-hello-new-property"></a>Usar a nova propriedade de saudação

Fazer algumas alterações no seu Olá toouse de código `Done` propriedade. Para simplificar este tutorial, você terá apenas Olá toochange `Index` e `Create` exibe a propriedade de saudação toosee em ação.

Abra _Controllers\TodosController.cs_.

Localize Olá `Create()` método e adicionar `Done` toohello lista de propriedades em Olá `Bind` atributo. Quando terminar, sua `Create()` assinatura do método aparência Olá código a seguir:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Abra _Views\Todos\Create.cshtml_.

Olá código Razor, você verá um `<div class="form-group">` elemento usa `model.Description`e, em seguida, outro `<div class="form-group">` elemento usa `model.CreatedDate`. Imediatamente após esses dois elementos, adicione outro elemento `<div class="form-group">` que usa `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Abra _Views\Todos\Index.cshtml_.

Pesquise Olá vazio `<th></th>` elemento. Acima desse elemento, adicione Olá código Razor a seguir:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Localize Olá `<td>` elemento que contém a saudação `Html.ActionLink()` métodos auxiliares. Acima desse elemento, adicione Olá código Razor a seguir:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Isso é tudo o que você precisa toosee alterações Olá Olá `Index` e `Create` modos de exibição. 

Tipo `Ctrl+F5` toorun Olá aplicativo.

Agora você pode adicionar um item de tarefas e marcar **Concluído**. Em seguida, ele deverá aparecer na sua página inicial como um item concluído. Lembre-se de que Olá `Edit` exibição não mostra Olá `Done` campo, porque você não alterar Olá `Edit` exibição.

### <a name="enable-code-first-migrations-in-azure"></a>Habilitar Migrações do Code First no Azure

Agora que seu código alterar funciona, incluindo a migração do banco de dados, você publicá-lo tooyour aplicativo de web do Azure e atualizar o banco de dados SQL com migrações do Code First muito.

Exatamente como antes, clique com o botão direito do mouse no projeto e selecione **Publicar**.

Clique em **configurações** tooopen Olá Assistente de publicação.

![Abrir as configurações de publicação](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

No Assistente de saudação, clique em **próximo**.

Verifique se essa cadeia de caracteres de conexão de saudação para seu banco de dados SQL é populado em **MyDatabaseContext (MyDbConnection)**. Talvez seja necessário Olá tooselect **myToDoAppDb** banco de dados na lista suspensa de saudação. 

Selecione **Executar o Migrations do Code First (executado na inicialização do aplicativo)** e, em seguida, clique em **Salvar**.

![Habilitar Migrações do Code First no aplicativo Web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Publicar suas alterações

Agora que as Migrações do Code First estão habilitadas no seu aplicativo Web do Azure, publique suas alterações de código.

No hello publicar página, clique em **publicar**.

Tente adicionar os itens pendentes outra vez, selecione **Concluído** e os itens deverão aparecer na sua página inicial como um item concluído.

![Aplicativo Web do Azure após Migração do Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Observe que todos os itens de tarefas existentes ainda são exibidos. Quando você republicar seu aplicativo ASP.NET, os dados existentes no Banco de Dados SQL não serão perdidos. Além disso, migrações do Code First altera somente o esquema de dados hello e deixa os dados existentes intactas.


## <a name="stream-application-logs"></a>Transmitir logs de aplicativos

Você pode transmitir mensagens de rastreamento diretamente do seu aplicativo de web do Azure tooVisual Studio.

Abra _Controllers\TodosController.cs_.

Cada ação inicia com um método `Trace.WriteLine()`. Esse código é adicionado tooshow você como as mensagens de rastreamento tooadd tooyour aplicativo de web do Azure.

### <a name="open-server-explorer"></a>Abra o Gerenciador de Servidores

De saudação **exibição** menu, selecione **Server Explorer**. É possível configurar o log para o aplicativo Web do Azure no **Gerenciador de Servidores**. 

### <a name="enable-log-streaming"></a>Habilitar streaming de log

No **Gerenciador de Servidores**, expanda **Azure** > **Serviço de Aplicativo**.

Expanda Olá **myResourceGroup** grupo de recursos que você criou ao criar aplicativo web do Azure de saudação.

Clique com o botão direito do mouse no aplicativo Web do Azure e selecione **Exibir Logs de Streaming**.

![Habilitar streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Olá logs são agora transmitidos em Olá **saída** janela. 

![Streaming de log na janela Saída](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

No entanto, você não vir quaisquer mensagens de saudação do rastreamento ainda. Isso porque, quando você seleciona pela primeira vez **Exibir Logs de Streaming**, seu aplicativo web do Azure define o nível de rastreamento de saudação muito`Error`, que registra somente eventos de erro (com hello `Trace.TraceError()` método).

### <a name="change-trace-levels"></a>Alterar níveis de rastreamento

rastreamento de saudação toochange níveis toooutput outras mensagens de rastreamento, vá volta muito**Server Explorer**.

Clique com o botão direito do mouse no aplicativo Web do Azure novamente e selecione **Configurações**.

Em Olá **(sistema de arquivos) de log de aplicativo** lista suspensa, selecione **detalhado**. Clique em **Salvar**.

![Alterar tooVerbose de nível de rastreamento](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Você pode fazer experiências com toosee de níveis diferentes de rastreamento que tipos de mensagens são exibidos para cada nível. Por exemplo, Olá **informações** nível inclui todos os logs criados por `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, mas não os logs criados por `Trace.WriteLine()`.
>
>

No navegador, tente clicar em torno do aplicativo de lista de tarefas pendentes de hello no Azure. mensagens de rastreamento de saudação agora são transmitidas toohello **saída** janela no Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Parar o streaming de log

toostop Olá serviço log de streaming, clique em Olá **parar de monitorar** botão Olá **saída** janela.

![Parar o streaming de log](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Gerenciar seu aplicativo Web do Azure

Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou. 



No menu à esquerda do hello, clique em **do serviço de aplicativo**, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Você aterrissou na página do seu aplicativo Web. 

Por padrão, o portal de saudação mostra Olá **visão geral** página. Esta página fornece uma visão de como está seu aplicativo. Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir. 

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Criar um Banco de Dados SQL no Azure
> * Conecte-se um aplicativo ASP.NET tooSQL banco de dados
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Logs de fluxo do Azure tooyour terminal
> * Gerenciar o aplicativo hello em Olá portal do Azure

Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome toohello web app.

> [!div class="nextstepaction"]
> [Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md)
