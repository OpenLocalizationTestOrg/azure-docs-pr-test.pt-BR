---
title: "aaaAzure AD .NET web API Introdução | Microsoft Docs"
description: "Como toobuild uma API da web .NET MVC que se integra com o Azure AD para autenticação e autorização."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Proteger uma API Web usando os tokens de portador do Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Se você estiver criando um aplicativo que fornece acesso a recursos tooprotected, será necessário tooknow como tooprevent injustificada acessar os recursos de toothose.
Azure Active Directory (AD do Azure) torna simples e direto toohelp proteger uma API da web usando os tokens de acesso de portador OAuth 2.0 com apenas algumas linhas de código.

Em aplicativos da web ASP.NET, você pode realizar essa proteção usando a implementação da Microsoft de saudação do hello dirigida pela comunidade middleware OWIN incluído no .NET Framework 4.5. Aqui, usaremos OWIN toobuild uma API da web "tooDo lista" que:

* Designa quais APIs estão protegidas.
* Valida que Olá chamadas de API da web contém um token de acesso válido.

saudação de toobuild tooDo API da lista, primeiro você precisa:

1. Registrar um aplicativo com o Azure AD.
2. Configure o pipeline de autenticação Olá aplicativo toouse Olá OWIN.
3. Configure um cliente aplicativo toocall Olá API da web.

tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Cada um é uma solução do Visual Studio 2013. Também é necessário um locatário Azure AD no qual tooregister seu aplicativo. Se você não tiver uma, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Etapa 1: registrar um aplicativo com o Azure AD
toohelp proteger seu aplicativo, você primeiro precisa toocreate um aplicativo no seu locatário e fornece algumas informações importantes de AD do Azure.

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.

3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.

4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.

5. Siga os prompts de saudação e criar um novo **aplicativo Web e/ou API da Web**.
  * **Nome** descreve toousers seu aplicativo. Digite **tooDo lista serviço**.
  * **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que usa o AD do Azure tooreturn qualquer tokens que seu aplicativo tenha solicitado. Digite `https://localhost:44321/` para esse valor.

6. De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização. Insira um identificador específico ao locatário. Por exemplo, insira: `https://contoso.onmicrosoft.com/TodoListService`.

7. Salve a configuração de saudação. Deixe o portal Olá aberto, porque você também precisará tooregister seu aplicativo cliente em breve.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Etapa 2: Configurar o pipeline de autenticação Olá aplicativo toouse Olá OWIN
solicitações de entrada toovalidate e tokens, é necessário tooset backup toocommunicate seu aplicativo com o Azure AD.

1. toobegin, abra a solução de saudação e adicionar projeto de TodoListService toohello de pacotes NuGet de middleware OWIN de saudação usando Olá Package Manager Console.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Adicionar um projeto TodoListService do toohello da classe de inicialização OWIN chamado `Startup.cs`.  Projeto de saudação com o botão direito, selecione **adicionar** > **Novo Item**e, em seguida, procure **OWIN**. Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.

3. Altere a declaração de classe Olá muito`public partial class Startup`. Já implementamos parte dessa classe para você em outro arquivo. Em Olá `Configuration(…)` método, fazer uma chamada muito`ConfgureAuth(…)` tooset a autenticação para seu aplicativo web.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método. Olá parâmetros que você fornece em `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Agora você pode usar `[Authorize]` atributos toohelp proteger seus controladores e ações com autenticação do portador do JSON Web Token (JWT). Decore Olá `Controllers\TodoListController.cs` classe com uma marca de autorização. Isso forçará Olá usuário toosign em antes de acessar essa página.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Quando um chamador autorizado com êxito invoca uma saudação `TodoListController` APIs, ação Olá pode precisar acessar tooinformation sobre chamador hello. OWIN fornece acesso toohello declarações no token de portador Olá via Olá `ClaimsPrincpal` objeto.  

6. Um requisito comum para APIs da web é toovalidate hello "escopos" presentes no token de saudação. Isso garante que o usuário Olá consentiu toohello permissões tooaccess necessário Olá tooDo serviço da lista.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Olá abrir `web.config` na raiz de saudação do projeto TodoListService de saudação do arquivo e insira os valores de configuração no hello `<appSettings>` seção.
  * `ida:Tenant`é o nome de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.
  * `ida:Audience`é Olá URI de ID de aplicativo do aplicativo hello que você inseriu na Olá portal do Azure.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Etapa 3: Configurar um aplicativo cliente e executar o serviço de saudação
Antes de poder ver Olá tooDo serviço da lista em ação, você precisa cliente da lista tooconfigure Olá tooDo para que possa obter tokens do AD do Azure e fazer chamadas toohello serviço.

1. Voltar toohello [portal do Azure](https://portal.azure.com).

2. Criar um novo aplicativo no seu locatário do AD do Azure e selecione **aplicativo cliente nativo** no prompt de saudação resultante.
  * **Nome** descreve toousers seu aplicativo.
  * Digite `http://TodoListClient/` para Olá **Uri de redirecionamento** valor.

3. Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único. Você precisará desse valor nas etapas da próximas hello, portanto copie-o da página de aplicativo hello.

4. De saudação **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**. Localize e selecione Olá tooDo serviço da lista, adicione Olá **acesso TodoListService** permissão em **permissões delegadas**e, em seguida, clique em **feito**.

5. No Visual Studio, abra `App.config` Olá TodoListClient projeto e, em seguida, insira os valores de configuração no hello `<appSettings>` seção.

  * `ida:Tenant`é o nome de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.
  * `ida:ClientId`é a ID do aplicativo hello que você copiou da saudação portal do Azure.
  * `todo:TodoListResourceId`é hello URI de ID do aplicativo de saudação tooDo aplicativo de serviço de lista que você inseriu na Olá portal do Azure.

## <a name="next-steps"></a>Próximas etapas
Por fim, limpe, compile e execute cada projeto. Se você ainda não fez isso, agora é Olá tempo toocreate um novo usuário em seu locatário com um *. c o m domínio. Entrar no cliente da lista tooDo toohello com esse usuário e adicionar a lista de tarefas do usuário toohello algumas tarefas.

Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Agora você pode mover toomore cenários de identidade.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
