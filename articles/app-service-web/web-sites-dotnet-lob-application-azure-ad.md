---
title: "aaaCreate um aplicativo de linha de negócios do Azure com a autenticação do Active Directory do Azure | Microsoft Docs"
description: "Saiba como o aplicativo toocreate uma ASP.NET MVC linha de negócios no serviço de aplicativo do Azure que autentica com o Active Directory do Azure"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory
Este artigo mostra como aplicativo toocreate uma .NET linha de negócios em [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando Olá [autenticação / autorização](../app-service/app-service-authentication-overview.md) recurso. Ele também mostra como Olá toouse [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dados do diretório de aplicativo hello.

locatário do Active Directory do Azure Olá que você usar pode ser um diretório somente no Azure. Ou, pode ser [sincronizado com o Active Directory no local](../active-directory/active-directory-aadconnect.md) toocreate uma experiência de logon único para os funcionários que estão em locais e remotos. Este artigo usa o diretório padrão de saudação para sua conta do Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>O que você compilará
Você criará um aplicativo simples de criar-leitura-atualização-exclusão (CRUD) de linha de negócios em aplicativos de Web do serviço de aplicativo que rastreia itens de trabalho com hello recursos a seguir:

* Autentica usuários no Active Directory do Azure
* Consulta usuários de diretório e grupos usando a [API do Graph do Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Use Olá ASP.NET MVC *sem autenticação* modelo

Se você precisar de controle de acesso baseado em função (RBAC) para seu aplicativo de linha de negócios no Azure, confira a [Próxima etapa](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>O que você precisa
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Você precisa Olá toocomplete a seguir este tutorial:

* Um locatário do Active Directory do Azure com usuários em vários grupos
* Permissões toocreate aplicativos no locatário do Active Directory do Azure Olá
* Visual Studio 2013 Atualização 4 ou posterior
* [SDK 2.8.1 do Azure ou posterior](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Criar e implantar um tooAzure de aplicativo web
1. No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.
2. Selecione **Aplicativo Web ASP.NET**, nomeie seu projeto e clique em **OK**.
3. Selecione Olá **MVC** modelo, altere a autenticação de saudação muito**sem autenticação**. Certifique-se de **Host na nuvem de saudação** está selecionado e clique em **Okey**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **adicionar uma conta** (e, em seguida, **adicionar uma conta** na lista suspensa de saudação) toolog em tooyour conta do Azure.
5. Depois de conectado, configure seu aplicativo Web. Criar um grupo de recursos e um novo plano de serviço de aplicativo clicando Olá respectivo **novo** botão. Clique em **explorar serviços adicionais do Azure** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. Em Olá **serviços** , clique em  **+**  tooadd um banco de dados SQL para seu aplicativo. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. Em **configurar banco de dados SQL**, clique em **novo** toocreate uma instância do SQL Server.
8. Em **Configurar SQL Server**, configure sua instância do SQL Server. Em seguida, clique em **Okey**, **Okey**, e **criar** tookick desativar a criação de saudação de aplicativo no Azure.
9. Em **atividade de serviço de aplicativo do Azure**, você pode ver quando da criação do aplicativo hello for concluída. Clique em  **publicar &lt;* appname*> toothis aplicativo Web agora * *, em seguida, clique em **publicar**. 
   
    Depois que o Visual Studio for concluído, ele abre Olá publicar o aplicativo no navegador de saudação. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Configurar a autenticação e acesso ao diretório
1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. No menu à esquerda do hello, clique em **serviços de aplicativos** > **&lt;*appname*> * * > **autenticação / autorização**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Ative a autenticação do Azure Active Directory clicando em **Ativar** > **Azure Active Directory** > **Expresso** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Clique em **salvar** na barra de comandos de saudação.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Depois que as configurações de autenticação Olá foram salvas com êxito, tente navegar tooyour aplicativo novamente no navegador de saudação. As configurações padrão impõem a autenticação no aplicativo inteiro hello. Se você já não estiver conectado, você é redirecionado tooa a tela de login. Depois de conectado, você verá seu aplicativo protegido por HTTPS. Em seguida, você precisa toodirectory tooenable acessar os dados. 
5. Navegue toohello [portal clássico](https://manage.windowsazure.com).
6. No menu à esquerda do hello, clique em **do Active Directory** > **diretório padrão** > **aplicativos**  >   **&lt;* appname*> * *.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Este é o aplicativo do Active Directory do Azure hello que o serviço de aplicativo criado para você tooenable Olá autorização / recurso de autenticação.
7. Clique em **usuários** e **grupos** toomake-se de que há alguns usuários e grupos no diretório de saudação. Caso contrário, crie alguns usuários e grupos de teste.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Clique em **configurar** tooconfigure este aplicativo.
9. Role para baixo toohello **chaves** seção e adicione uma chave, selecionando uma duração. Em seguida, clique em **Permissões Delegadas** e selecione **Ler dados do diretório**. 
   Clique em **Salvar**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Depois que as configurações são salvas, role para cima toohello **chaves** seção e clique em Olá **cópia** chave botão toocopy de saudação do cliente. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Se você sair desta página agora, não será capaz de tooaccess esse cliente nunca novamente da chave.
    > 
    > 
11. Em seguida, você precisa tooconfigure seu aplicativo web com essa chave. Faça logon no toohello [Gerenciador de recursos do Azure](https://resources.azure.com) com sua conta do Azure.
12. Na parte superior de saudação da página de saudação, clique em **leitura/gravação** toomake alterações Olá Gerenciador de recursos do Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Localizar as configurações de autenticação para seu aplicativo, localizado em assinaturas de hello >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **provedores** > **Microsoft**  >  **sites** > **&lt;*appname*> * * > **config**  >  **authsettings**.
14. Clique em **Editar**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Olá painel de edição, definido Olá `clientSecret` e `additionalLoginParams` propriedades da seguinte maneira.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Clique em **colocar** em Olá toosubmit superior suas alterações.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Tootest agora, se você tiver autorização Olá token Olá tooaccess API do Graph do Azure Active Directory, basta navegar até  **https://&lt;*appname*>.azurewebsites.net/.auth/me** no seu Navegador. Se você configurou tudo corretamente, você deverá ver Olá `access_token` propriedade Olá resposta JSON.
    
    Olá `~/.auth/me` caminho da URL é gerenciado pelo aplicativo serviço de autenticação / autorização toogive você todas as informações de saudação relacionados sessão tooyour autenticado. Para saber mais, confira [Autenticação e autorização no Serviço de Aplicativo do Azure](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Olá `access_token` tem um período de expiração. No entanto, a Autenticação/Autorização do Serviço de Aplicativo fornece a funcionalidade de atualização do token com `~/.auth/refresh`. Para obter mais informações sobre como toouse, consulte [armazenamento de Token do serviço de aplicativo](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Em seguida, você fará algo útil com os dados do diretório.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Adicionar a funcionalidade de linha de negócios tooyour aplicativo
Agora, crie um rastreador de itens de trabalho CRUD simples.  

1. Na pasta de ~\Models hello, crie um arquivo de classe chamado WorkItem.cs e substitua `public class WorkItem {...}` com hello código a seguir:
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Crie hello projeto toomake sua nova lógica de scaffolding toohello acessível do modelo no Visual Studio.
3. Adicionar um novo item de scaffolding `WorkItemsController` toohello ~\Controllers pasta (clique **controladores**, ponto muito**adicionar**e selecione **novo item de scaffolding**). 
4. Selecione **Controlador MVC 5 com modos de exibição usando o Entity Framework** e clique em **Adicionar**.
5. Modelo de saudação selecione que você criou, clique  **+**  e, em seguida, **adicionar** tooadd um contexto de dados e, em seguida, clique em **adicionar**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. No ~\Views\WorkItems\Create.cshtml (um item de scaffolding automaticamente), localize Olá `Html.BeginForm` método auxiliar e fazer Olá realçadas alterações a seguir:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Observe que `token` e `tenant` são usados por Olá `AadPicker` toomake objeto chamadas de API do Graph do Azure Active Directory. Você adicionará `AadPicker` mais tarde.     
   
   > [!NOTE]
   > Você também pode obter `token` e `tenant` do lado do cliente Olá com `~/.auth/me`, mas que deve ser uma chamada de servidor adicional. Por exemplo:
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. Alterar Olá mesmo com ~ \Views\WorkItems\Edit.cshtml.
8. Olá `AadPicker` objeto é definido em um script que você precisa tooadd tooyour projeto. Clique Olá ~\Scripts pasta, aponte muito**adicionar**e clique em **arquivo JavaScript**. Tipo `AadPickerLibrary` para o nome de arquivo hello e clique em **Okey**.
9. Copiar o conteúdo de saudação do [aqui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) em ~ \Scripts\AadPickerLibrary.js.
   
   No script hello, Olá `AadPicker` objeto chamadas [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para usuários e grupos que corresponder à entrada hello.  
10. ~\Scripts\AadPickerLibrary.js também usa Olá [jQuery UI AutoCompletar widget](https://jqueryui.com/autocomplete/). Assim, é necessário o projeto de tooyour tooadd jQuery UI. Clique com o botão direito do mouse em seu projeto e clique em **Gerenciar Pacotes NuGet**.
11. Em Olá NuGet Package Manager, clique em Procurar, tipo **jquery ui** Olá barra de pesquisa e clique em **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. No painel direito da saudação, clique em **instalar**, em seguida, clique em **Okey** tooproceed.
13. Abra ~\App_Start\BundleConfig.cs e verifique Olá realçadas alterações a seguir:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Há toomanage de maneiras mais eficazes JavaScript e arquivos CSS em seu aplicativo. No entanto, para manter a simplicidade você apenas vai toopiggyback em pacotes de saudação que serão carregados com cada exibição.
14. Por fim, em ~ \Global.asax, adicionar Olá a seguinte linha de código no hello `Application_Start()` método. `Ctrl`+`.`em cada erro de resolução de nomes muito corrigi-lo.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Esta linha de código é necessário porque o modelo saudação padrão MVC usa <code>[ValidateAntiForgeryToken]</code> decoração em algumas das ações de saudação. Devido a toohello comportamento descrito por [Brock Allen](https://twitter.com/BrockLAllen) em [MVC 4, AntiForgeryToken e declarações](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) sua POSTAGEM HTTP pode falhar a validação de token antifalsificação porque:
    > 
    > * Active Directory do Azure não envia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, que é requerido por padrão pelo token antifalsificação de saudação.
    > * Se o Active Directory do Azure é sincronizado com o AD FS de diretório, relação de confiança de saudação do AD FS por padrão não enviar Olá http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider declaração, embora você possa configurar manualmente o AD FS toosend Esta declaração.
    > 
    > `ClaimTypes.NameIdentifies`Especifica a declaração de saudação `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que forneça Active Directory do Azure.  
    > 
    > 
15. Agora, publique suas alterações. Clique com o botão direito do mouse em seu projeto e clique em **Publicar**.
16. Clique em **configurações**, verifique se há uma cadeia de caracteres de conexão tooyour banco de dados SQL, selecione **Atualizar banco de dados** toomake Olá alterações de esquema para o seu modelo e clique em **publicar** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. No navegador de hello, navegue toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e clique em **criar novo**.
18. Clique em Olá **AssignedToName** caixa. Agora você verá os usuários e grupos do seu locatário do Azure Active Directory em uma lista suspensa. Você pode digitar toofilter, ou usar Olá `Up` ou `Down` de chave ou clique tooselect Olá usuário ou grupo. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Clique em **criar** toosave alterações de saudação. Em seguida, clique em **editar** trabalho Olá criado item tooobserve Olá mesmo comportamento.

Parabéns, você está executando um aplicativo de linha de negócios no Azure com acesso ao diretório! Há muito mais que você pode fazer com hello API do Graph. Consulte a [referência da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Próxima etapa
Se você precisar de controle de acesso baseado em função (RBAC) para seu aplicativo de linha de negócios no azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obter um exemplo da equipe do Active Directory do Azure hello. Ele mostra como funções de tooenable para seu aplicativo do Active Directory do Azure e, em seguida, autorizar usuários com hello `[Authorize]` decoração.

Se seu aplicativo de linha de negócios precisa acessar dados tooon locais, consulte [acessar recursos usando conexões híbridas no serviço de aplicativo do Azure locais](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Outros recursos
* [Autenticação e autorização no Serviço de Aplicativo do Azure](../app-service/app-service-authentication-overview.md)
* [Autenticar com o Active Directory local em seu aplicativo do Azure](web-sites-authentication-authorization.md)
* [Criar um aplicativo de linha de negócios no Azure com autenticação do AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Autenticação do serviço de aplicativo e hello Azure AD Graph API](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Exemplos e documentação do Microsoft Azure Active Directory](https://github.com/AzureADSamples)
* [Tipos de declaração e token com suporte no Active Directory do Azure](http://msdn.microsoft.com/library/azure/dn195587.aspx)
