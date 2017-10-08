---
title: "aaaCreate um aplicativo de linha de negócios do Azure com autenticação do AD FS | Microsoft Docs"
description: "Saiba como toocreate um aplicativo de linha de negócios no serviço de aplicativo do Azure que se autentica com local STS. Este tutorial destina-se como Olá STS locais do AD FS."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Criar um aplicativo de linha de negócios do Azure com autenticação do AD FS
Este artigo mostra como aplicativo toocreate uma ASP.NET MVC linha de negócios em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) usando um local [os serviços de Federação do Active Directory](http://technet.microsoft.com/library/hh831502.aspx) como provedor de identidade hello. Este cenário poderá funcionar quando você deseja que os aplicativos de linha de negócios toocreate no serviço de aplicativo do Azure, mas sua organização exigir toobe de dados do diretório armazenada no local.

> [!NOTE]
> Para obter uma visão geral das opções de autenticação e autorização de empresa diferente de saudação do serviço de aplicativo do Azure, consulte [autenticar com o Active Directory local em seu aplicativo do Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>O que você compilará
Você criará um aplicativo básico ASP.NET em aplicativos de Web do serviço de aplicativo do Azure com hello recursos a seguir:

* Autentica usuários no AD FS
* Usa `[Authorize]` tooauthorize usuários para ações diferentes
* Configuração estática para depuração no Visual Studio e publicar aplicativos Web do serviço de tooApp (configura uma vez, depurar e publicar a qualquer momento)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>O que você precisa
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Você precisa Olá toocomplete a seguir este tutorial:

* Um local em implantação do AD FS (para uma explicação de ponta a ponta do laboratório de teste Olá usado neste tutorial, consulte [laboratório de teste: STS autônomo com o AD FS na VM do Azure (para teste)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Relações de confiança de terceira parte confiável toocreate permissões no gerenciamento do AD FS
* Visual Studio 2013 Atualização 4 ou posterior
* [SDK do Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou posterior

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Usar o aplicativo de exemplo para modelo de linha de negócios
Olá o aplicativo de exemplo neste tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), é criado pela equipe do Active Directory do Azure hello. Como o AD FS oferece suporte para WS-Federation, você pode usar isso como um aplicativo de linha de negócios do modelo toocreate com facilidade. Ele tem Olá recursos a seguir:

* Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate com um local em implantação do AD FS
* Funcionalidade de entrada e saída
* Usa [pt](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (em vez do Windows Identity Foundation), que é Olá futuras do ASP.NET e muito mais simples tooset para autenticação e autorização que o WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Configurar o aplicativo de exemplo hello
1. Clonar ou baixar a solução de exemplo hello em [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour diretório de local.
   
   > [!NOTE]
   > Olá instruções em [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) mostram como tooset o aplicativo hello com o Active Directory do Azure. Mas, neste tutorial, você configurá-lo com o AD FS, portanto, siga etapas Olá aqui em vez disso.
   > 
   > 
2. Abrir solução hello e abra Controllers\AccountController.cs em Olá **Gerenciador de soluções**.
   
   Você verá que o código de saudação simplesmente emite um usuário de saudação autenticação desafio tooauthenticate usando o WS-Federation. Todas as autenticações são configuradas em App_Start\Startup.Auth.cs.
3. Abra App_Start\Startup.Auth.cs. Em Olá `ConfigureAuth` método, a linha de saudação de Observação:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Em Olá, mundo OWIN, este trecho de código é realmente Olá bare que mínimo necessário para autenticação de WS-Federation tooconfigure. É muito mais simples e mais elegante de WIF, em que o Web. config é injetado com XML em todos os lugares hello. Olá apenas informações que você precisa são Olá da terceira parte confiável (RP) identificador e hello URL do arquivo de metadados do serviço do AD FS. Aqui está um exemplo:
   
   * Identificador RP: `https://contoso.com/MyLOBApp`
   * Endereço de metadados: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. No App_Start\Startup.Auth.cs, altere Olá definições de cadeia de caracteres estática a seguir:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Agora, fazer as alterações correspondentes de saudação em Web. config. Abra Olá Web. config e modifique Olá configurações do aplicativo a seguir:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Preencha os valores de chave Olá com base em seu respectivo ambiente.
6. Olá aplicativo toomake-se de que não existem erros de compilação.

É isso. Agora o aplicativo de exemplo hello está pronto toowork com o AD FS. Você ainda precisa tooconfigure uma relação de confiança com este aplicativo no AD FS RP.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Implantar tooAzure de aplicativo de exemplo hello aplicativos de Web do serviço de aplicativo
Aqui, você publica Olá aplicativo tooa web app no aplicativo de serviço Web aplicativos enquanto preserva o ambiente de depuração de saudação. Observe que você vai aplicativo hello de toopublish antes que ele tem uma relação de confiança com o AD FS, RP para que autenticação ainda não funciona ainda. No entanto, se você fazê-lo agora você pode ter Olá URL do aplicativo web que você pode usar mais tarde tooconfigure Olá RP relação de confiança.

1. Clique duas vezes com o botão direito em seu projeto e selecione **Publicar**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Clique em **Serviço de Aplicativo do Microsoft Azure**.
3. Se você ainda não tiver entrado no tooAzure, clique em **entrar** e usar a conta da Microsoft hello para toosign sua assinatura do Azure no.
4. Depois de conectado, clique em **novo** toocreate um aplicativo web.
5. Preencha todos os campos obrigatórios. Posteriormente, que serão os dados de local tooon tooconnect para não criar um banco de dados para este aplicativo web.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Clique em **Criar**. Depois de criar aplicativo de web hello, de diálogo Publicar Web hello é aberto.
7. Em **URL de destino**, alterar **http** muito**https**. Copie Olá todo URL tooa editor de texto para uso posterior. Em seguida, clique em **Publicar**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. No Visual Studio, abra **Web.Release.config** em seu projeto. Inserir saudação XML a seguir em Olá `<configuration>` marca e substitua o valor da chave Olá com URL de publicação do seu aplicativo web.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Quando terminar, você tem dois identificadores RP configurados no seu projeto, um para o seu ambiente de depuração no Visual Studio, e um para Olá publicado o aplicativo web no Azure. Você configurará uma relação de confiança RP para cada um dos dois ambientes de saudação do AD FS. Durante a depuração, configurações do aplicativo hello em Web. config são usada toomake seu **depurar** do trabalho de configuração com o AD FS. Quando ele é publicado (por padrão, Olá **versão** configuração é publicada), um Web. config transformados é carregado que incorpora as alterações de configuração de aplicativo hello em Web.Release.config.

Se você quiser tooattach Olá web publicados aplicativo no depurador de toohello do Azure (ou seja, você deve carregar símbolos de depuração do seu código no aplicativo de web publicados Olá), você pode criar um clone de saudação depurar a configuração de depuração do Azure, mas com seu próprio Web. config personalizado transformar ( Por exemplo, Web.AzureDebug.config) que usa configurações de aplicativo de saudação do Web.Release.config. Isso permite que você toomaintain estático entre ambientes diferentes hello.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Configurar a terceira parte confiável no gerenciamento do AD FS
Agora, é necessário tooconfigure uma relação de confiança RP no gerenciamento do AD FS antes de usar o aplicativo de exemplo e, na verdade, autenticar com o AD FS. Você precisará tooset backup duas relações de confiança RP separadas, uma para o seu ambiente de depuração e outra para seu aplicativo web publicado.

> [!NOTE]
> Certifique-se de que você repita Olá seguindo as etapas para ambos os ambientes.
> 
> 

1. No servidor do AD FS, faça logon com credenciais que tenham direitos de gerenciamento tooAD FS.
2. Abra o gerenciamento do AD FS. Clique com o botão direito do mouse em **AD FS\Relacionamentos confiáveis\Objetos de confiança de terceira parte confiável** e selecione **Adicionar objeto de confiança de terceira parte confiável**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. Em Olá **Selecionar fonte de dados** , selecione **inserir manualmente dados sobre a terceira parte confiável Olá**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. Em Olá **especificar nome de exibição** página, digite um nome para exibição para o aplicativo hello e clique em **próximo**.
5. Em Olá **escolha protocolo** , clique em **próximo**.
6. Em Olá **configurar certificado** , clique em **próximo**.
   
   > [!NOTE]
   > Como você já deve usar HTTPS, os tokens criptografados são opcionais. Se você realmente deseja tooencrypt tokens do AD FS nesta página, você também deve adicionar lógica de descriptografia de token em seu código. Para obter mais informações, consulte [Configuração manual de middleware OWIN WS-Federation e aceitação de tokens criptografados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Antes de passar para a próxima etapa do hello, é necessário um pedaço de informações do seu projeto do Visual Studio. Nas propriedades do projeto hello, observe Olá **SSL URL** do aplicativo hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. Em gerenciamento do AD FS, em Olá **configurar URL** página de saudação **terceira parte confiável Assistente para adicionar confiança**, selecione **habilitar o suporte para o protocolo WS-Federation Passive do hello** e digite hello URL de SSL de seu projeto do Visual Studio que você anotou na etapa anterior hello. Em seguida, clique em **Avançar**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL especifica onde o cliente de saudação toosend após a autenticação for bem-sucedida. Para o ambiente de depuração hello, ele deve ser <code>https://localhost:&lt;port&gt;/</code>. Para o aplicativo de web publicados hello, deve ser URL do aplicativo web hello.
   > 
   > 
9. Em Olá **configurar identificadores** página, verifique se que seu projeto SSL URL já está listado e clique em **próximo**. Clique em **próximo** todos Olá final de toohello de maneira do Assistente de saudação com as seleções padrão.
   
   > [!NOTE]
   > No App_Start\Startup.Auth.cs do projeto do Visual Studio, esse identificador é comparado com o valor de saudação do <code>WsFederationAuthenticationOptions.Wtrealm</code> durante a autenticação federada. Por padrão, a URL do aplicativo hello da etapa anterior Olá é adicionado como um identificador RP.
   > 
   > 
10. Agora terminar de configurar Olá aplicativo RP para seu projeto no AD FS. Em seguida, configure toosend esse aplicativo hello declarações necessitadas para seu aplicativo. Olá **editar regras de declaração** caixa de diálogo é aberta por padrão para você no final de saudação do Assistente de saudação para que você possa começar imediatamente. Vamos configurar pelo menos Olá seguintes declarações (com esquemas entre parênteses):
    
    * Nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - usado por ASP.NET toohydrate `User.Identity.Name`.
    * Usuário nome principal (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - usado toouniquely identificar os usuários na organização hello.
    * Associações de grupo, como funções (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - pode ser usado com `[Authorize(Roles="role1, role2,...")]` decoração tooauthorize controladores/ações. Na verdade, essa abordagem pode não ser Olá para autorização de função de melhor desempenho. Se os usuários do AD pertencem toohundreds dos grupos de segurança, eles se tornam centenas de declarações de função no token SAML hello. Uma abordagem alternativa é toosend uma única função de declaração condicionalmente dependendo da associação do usuário Olá em um grupo específico. No entanto, vamos manter isso simples para este tutorial.
    * ID do nome (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) – pode ser usado para validação antifalsificação. Para obter mais informações sobre como toomake que ele funciona com a validação de antifalsificação, consulte Olá **adiciona a funcionalidade de linha de negócios** seção [criar um aplicativo de linha de negócios do Azure com a autenticação do Active Directory do Azure ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Olá declaração tipos você precisará tooconfigure para seu aplicativo depende das necessidades do seu aplicativo. Para obter lista de saudação de declarações suportado por aplicativos do Active Directory do Azure (ou seja, relações de confiança RP), por exemplo, consulte [tipos de declaração e Token com suporte](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Na caixa de diálogo Olá editar regras de declaração, clique em **Adicionar regra**.
12. Configurar as declarações de nome UPN e função hello conforme mostrado na captura de tela de saudação e clique em **concluir**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Em seguida, crie um nome transitório de declaração de ID usando etapas Olá demonstrado no [identificadores de nome em declarações SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Clique em **Adicionar regra** novamente.
14. Selecione **Enviar Declarações Usando uma Regra Personalizada** e clique em **Avançar**.
15. Idioma de regra a seguir Olá colar em Olá **regra personalizada** caixa, uma regra de saudação do nome **por identificador de sessão** e clique em **concluir**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    A regra personalizada deve parecer com esta captura de tela:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Clique em **Adicionar regra** novamente.
17. Selecione **Transformar uma declaração de entrada** e clique em **Avançar**.
18. Configurar regra de hello, conforme mostrado na captura de tela de saudação (usando o tipo de declaração Olá criado na regra personalizada de saudação) e clique em **concluir**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Para obter informações detalhadas sobre as etapas de saudação para declaração de ID de nome temporária hello, consulte [identificadores de nome em declarações SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Clique em **aplicar** em Olá **editar regras de declaração** caixa de diálogo. Agora, ele deve ser como Olá captura de tela a seguir:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Novamente, certifique-se de repetir essas etapas para seu ambiente de depuração e o aplicativo Web publicado.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Teste a autenticação federada em seu aplicativo
Você está pronto tootest lógica de autenticação do aplicativo no AD FS. Em meu ambiente de laboratório do AD FS, tenho um usuário de teste que pertence o grupo de teste tooa no Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

autenticação tootest no depurador Olá, tudo o que você precisa toodo agora é o tipo `F5`. Se você deseja que a autenticação de tootest no aplicativo de web publicados Olá, navegue toohello URL.

Depois que o aplicativo da web hello carrega, clique em **entrar**. Agora, você deve obter ou uma caixa de diálogo ou Olá logon página de logon servida pelo AD FS, dependendo do método de autenticação de saudação escolhido pelo AD FS. Aqui está o que acontece no Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Depois de fazer logon com um usuário no domínio de AD de saudação da implantação do hello AD FS, você verá agora homepage Olá novamente com **Hello, <User Name>!** no canto hello. Aqui está o que acontece.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Até agora, você já teve êxito ao Olá maneiras a seguir:

* Seu aplicativo atingiu com êxito do AD FS e um identificador RP correspondente foi encontrado no hello banco de dados do AD FS
* O AD FS foi autenticado com êxito um usuário do AD e fazer home page do aplicativo toohello de redirecionamento
* O AD FS como nome de saudação enviada com êxito de declaração (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour aplicativo, conforme indicado pelo fato de saudação usuário Olá nome é exibido no canto hello. 

Se a declaração de nome hello estiver ausente, você teria visto **Hello,!**. Se você observar exibições \ compartilhadas\_LoginPartial.cshtml, você achar que ele usa `User.Identity.Name` toodisplay nome de usuário de saudação. Conforme mencionado anteriormente, se nome hello de declaração de saudação autenticada usuário está disponível no token SAML hello, ASP.NET hydrates essa propriedade com ele. toosee que Olá por todas as declarações que são enviadas pelo AD FS, colocar um ponto de interrupção em Controllers\HomeController.cs, Olá método de ação do índice. Depois Olá usuário é autenticado, inspecionar Olá `System.Security.Claims.Current.Claims` coleção.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autorizar usuários para controladores específicos ou ações
Desde que você incluiu associações de grupo como declarações de função em sua configuração de confiança RP, agora você pode usá-los diretamente no hello `[Authorize(Roles="...")]` decoração de controladores e ações. Em um aplicativo de linha de negócios com padrão de criar-leitura-atualização-exclusão (CRUD) hello, você pode autorizar funções específicas tooaccess cada ação. Por enquanto, você será apenas experimentar esse recurso no controlador Home existente de saudação.

1. Abra Controllers\HomeController.cs.
2. Decore Olá `About` e `Contact` ação métodos semelhantes toohello código a seguir, o uso de associações de grupo de segurança do usuário autenticado.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Como eu adicionei **usuário de teste** muito**grupo de teste** em meu ambiente de laboratório do AD FS, vou usar autorização do grupo de teste tootest em `About`. Para `Contact`, vai testar caso negativo de saudação do **Admins. do domínio**, toowhich **testar usuário** não pertence.
3. Iniciar o depurador Olá digitando `F5` entrar e clique em **sobre**. Você deve agora estar visualizando Olá `~/About/Index` página com êxito, se o usuário autenticado é autorizado para aquela ação.
4. Agora clique **entre em contato com**, que, em meu caso não deve autorizar **usuário de teste** para ação hello. No entanto, o navegador de saudação é redirecionado tooAD FS, que eventualmente mostra esta mensagem:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Se você examinar este erro no Visualizador de eventos em saudação do servidor AD FS, você vir essa mensagem de exceção:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    motivo Olá para esse erro é que por padrão, MVC retorna um 401 não autorizado quando uma função do usuário não está autorizada. Isso dispara um provedor de identidade reautenticação solicitação tooyour (AD FS). Como o usuário Olá já está autenticado, o AD FS retorna toohello mesma página, que, em seguida, emite outro 401, criando um loop de redirecionamento. Ignorará do AuthorizeAttribute `HandleUnauthorizedRequest` método com lógica simples tooshow algo que faça sentido em vez de loop de redirecionamento Olá continuando.
5. Crie um arquivo no projeto Olá chamado AuthorizeAttribute.cs e colar Olá código a seguir para ele.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Olá substituir envia código um HTTP 403 (proibido) em vez de HTTP 401 (não autorizado) nos casos autenticados, mas não autorizados.
6. Executar o depurador Olá novamente com `F5`. Clicar em **Contato** agora mostra uma mensagem de erro mais informativa (embora não atraente):
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Publicar novamente o hello aplicativo tooAzure aplicativos de Web do serviço de aplicativo e testar o comportamento de saudação do aplicativo ao vivo hello.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Conecte-se a dados locais tooon
Um motivo que você esperaria tooimplement seu aplicativo de linha de negócios com o AD FS, em vez de Active Directory do Azure é problemas de conformidade com a manter a organização dados fora do local. Isso também pode significar que o seu aplicativo web no Azure deve acessar bancos de dados local, desde que você não tem permissão toouse [banco de dados SQL](/services/sql-database/) como camada de dados Olá para seus aplicativos web.

Os Aplicativos Web do Serviço de Aplicativo do Azure dão suporte ao acesso a bancos de dados locais com duas abordagens: [Conexões Híbridas](../biztalk-services/integration-hybrid-connection-overview.md) e [Redes Virtuais](web-sites-integrate-with-vnet.md). Para obter mais informações, consulte [Usando integração de VNET e conexões híbridas com Aplicativos Web do Serviço de Aplicativo do Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Outros recursos
* [Autenticar com o Active Directory local em seu aplicativo do Azure](web-sites-authentication-authorization.md)
* [Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Use Olá opção de autenticação organizacional local (ADFS) com ASP.NET no Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Migrar um tooKatana VS2013 projeto da Web do WIF](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Visão geral dos Serviços de Federação do Active Directory](http://technet.microsoft.com/library/hh831502.aspx)
* [Especificação do WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

