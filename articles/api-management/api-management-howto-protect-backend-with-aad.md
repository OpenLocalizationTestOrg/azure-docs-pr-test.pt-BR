---
title: aaaProtect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API | Microsoft Docs
description: Saiba como tooprotect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Como tooprotect um back-end de API da Web com o Active Directory do Azure e o gerenciamento de API
Olá seguindo o vídeo mostra como toobuild um back-end de API da Web e protegê-los usando o protocolo OAuth 2.0 com o Active Directory do Azure e o gerenciamento de API.  Este artigo fornece uma visão geral e informações adicionais para Olá etapas vídeo hello. Este vídeo de 24 minutos mostra como:

* Criar um back-end de API da Web e protegê-lo com o AAD - iniciando em 1:30
* Importar Olá API para gerenciamento de API - começando em 7:10
* Configurar Olá Developer portal toocall Olá API - começando em 9:09
* Configurar uma saudação do aplicativo de desktop toocall API - começando em 18:08
* Configurar um toopre de política de validação de JWT-autorizar solicitações - começando em 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Criar um diretório do AD do Azure
toosecure API da Web do seu backup usando o Azure Active Directory, primeiro você deve ter um um locatário do AAD. Neste vídeo, um locatário chamado **APIMDemo** é usado. toocreate um locatário do AAD, entrar toohello [Portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços de aplicativos**->**ativa Diretório**->**diretório**->**criação personalizada**. 

![Azure Active Directory][api-management-create-aad-menu]

Neste exemplo, um diretório chamado **APIMDemo** é criado com um domínio padrão chamado **DemoAPIM.onmicrosoft.com**. Esse diretório é usado em todo o vídeo de saudação.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Criar um serviço de API da Web protegido pelo Active Directory do Azure
Nesta etapa, um back-end de API da Web é criado usando o Visual Studio 2013. Esta etapa do hello vídeo começa em 1:30. projeto de back-end de API da Web toocreate no, clique em Visual Studio **arquivo**->**novo**->**projeto**e escolha **da Web do ASP.NET Aplicativo** de saudação **Web** lista de modelos. Este vídeo Olá projeto é denominado **APIMAADDemo**. Clique em **Okey** toocreate projeto de saudação. 

![Visual Studio][api-management-new-web-app]

Clique em **API da Web** de saudação **selecionar uma lista de modelos** toocreate um projeto de API da Web. Clique em tooconfigure autenticação de diretório do Azure **alterar autenticação**.

![Novo Projeto][api-management-new-project]

Clique em **contas organizacionais**e especifique Olá **domínio** do seu locatário do AAD. Olá Este exemplo domínio é **DemoAPIM.onmicrosoft.com**. domínio saudação do seu diretório pode ser obtido Olá **domínios** guia de seu diretório.

![Domínios][api-management-aad-domains]

Definir configurações de saudação desejada no hello **alterar autenticação** caixa de diálogo e clique em **Okey**.

![Alterar Autenticação][api-management-change-authentication]

Quando você clica em **Okey** Visual Studio tentará tooregister seu aplicativo com o diretório do AD do Azure e pode ser solicitado toosign no Visual Studio. Entre usando uma conta administrativa para seu diretório.

![Entrar tooVisual Studio][api-management-sign-in-vidual-studio]

tooconfigure este projeto como uma saudação de seleção de API da Web do Azure caixa **Host na nuvem Olá** e, em seguida, clique em **Okey**.

![Novo Projeto][api-management-new-project-cloud]

Pode ser solicitado toosign em tooAzure e, em seguida, você pode configurar Olá aplicativo Web.

![Configurar][api-management-configure-web-app]

Neste exemplo, um novo **Plano do Serviço de Aplicativo** chamado **APIMAADDemo** é especificado.

Clique em **Okey** tooconfigure Olá Web App e crie o projeto de saudação.

## <a name="add-hello-code-toohello-web-api-project"></a>Adicionar projeto de API da Web do hello código toohello
a próxima etapa Olá vídeo Olá adiciona o projeto de API da Web do hello código toohello. Esta etapa começa em 4:35.

Olá API da Web neste exemplo implementa um serviço de calculadora básica usando um modelo e um controlador. modelo de saudação tooadd para serviço hello, clique **modelos** na **Solution Explorer** e escolha **adicionar**, **classe**. Nome de classe Olá `CalcInput` e clique em **adicionar**.

Adicione o seguinte Olá `using` superior de toohello de instrução de saudação `CalcInput.cs` arquivo.

```c#
using Newtonsoft.Json;
```

Substitua classe Olá gerado pelo Olá código a seguir.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Clique com o botão direito em **Controladores** no **Gerenciador de Soluções** e escolha **Adicionar**->**Controlador**. Clique em **Controlador de API da Web 2 - Vazio**, depois clique em **Adicionar**. Tipo **CalcController** para Olá controlador nome e clique em **adicionar**.

![Adicionar controlador][api-management-add-controller]

Adicione o seguinte Olá `using` superior de toohello de instrução de saudação `CalcController.cs` arquivo.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Saudação de substituição gerado classe do controlador com hello código a seguir. Esse código implementa Olá `Add`, `Subtract`, `Multiply`, e `Divide` operações de saudação básica API de calculadora.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Pressione **F6** toobuild e verifique se a solução de saudação.

## <a name="publish-hello-project-tooazure"></a>Publicar Olá projeto tooAzure
Olá essa etapa Visual Studio project é tooAzure publicado. Esta etapa do hello vídeo começa em 5:45.

toopublish Olá tooAzure do projeto, clique com botão direito Olá **APIMAADDemo** do projeto no Visual Studio e escolha **publicar**. Manter as configurações padrão de saudação em Olá **Publicar Web** caixa de diálogo e clique em **publicar**.

![Publicar na Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Conceder permissões de aplicativo de serviço de back-end toohello AD do Azure
Um novo aplicativo de serviço de back-end de saudação é criado no diretório do AD do Azure como parte da configuração de saudação e o processo de publicação do seu projeto de API da Web. Nesta etapa do hello vídeo, começando em 6:13, permissões são concedidas back-end do toohello API da Web.

![Aplicativo][api-management-aad-backend-app]

Clique em nome Olá Olá tooconfigure Olá necessário de permissões de aplicativos. Navegue toohello **configurar** guia e role para baixo toohello **permissões tooother aplicativos** seção. Clique Olá **permissões de aplicativo** lista suspensa ao lado de **Windows** **Active Directory do Azure**, marque caixa Olá **ler dados do diretório**e clique em **salvar**.

![Adicionar permissões][api-management-aad-add-permissions]

> [!NOTE]
> Se **Windows** **Active Directory do Azure** não é listado em aplicativos de tooother de permissões, clique em **Adicionar aplicativo** e adicioná-lo da lista de saudação.
> 
> 

Anote Olá **URI da Id do aplicativo** para uso em uma etapa posterior, quando um aplicativo do AD do Azure está configurado para o portal do desenvolvedor de gerenciamento de API de saudação.

![URI da Id do aplicativo][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Importar Olá API da Web para gerenciamento de API
APIs são configurados da saudação API portal do publicador, que pode é acessada por meio de saudação Portal do Azure. tooreach-la, clique em **portal do publicador** na barra de ferramentas de saudação do seu serviço de gerenciamento de API. Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [gerenciar sua primeira API] [ Manage your first API] tutorial.

![Portal do editor][api-management-management-console]

Operações podem ser [adicionado tooAPIs manualmente](api-management-howto-add-operations.md), ou eles podem ser importados. Neste vídeo, as operações são importadas no formato Swagger começando em 6:40.

Crie um arquivo chamado `calcapi.json` com conteúdo a seguir e salve-o computador tooyour. Certifique-se de que Olá `host` atributo aponta back-end do tooyour API da Web. Neste exemplo, `"host": "apimaaddemo.azurewebsites.net"` é usado.

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

Calculadora de saudação tooimport API, clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importação API**.

![Botão Importar API][api-management-import-api]

Execute Olá etapas tooconfigure Olá Calculadora API a seguir.

1. Clique em **do arquivo**, procurar toohello `calculator.json` arquivo que você salvou e clique em Olá **Swagger** botão de opção.
2. Tipo **calc** em Olá **sufixo de URL da API da Web** caixa de texto.
3. Clique em Olá **produtos (opcionais)** caixa e escolha **Starter**.
4. Clique em **salvar** tooimport Olá API.

![Adicionar nova API][api-management-import-new-api]

Depois que Olá API é importado, hello página Resumo para a API de saudação é exibida no portal do publicador hello.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Chamar API Olá com êxito do portal do desenvolvedor Olá
Neste ponto, Olá API foi importado para o gerenciamento de API, mas não pode ainda ser chamado com êxito do portal do desenvolvedor Olá porque o serviço de back-end de saudação é protegido com a autenticação do AD do Azure. Isso é demonstrado no vídeo Olá começando com 7:40 usando Olá etapas a seguir.

Clique em **portal do desenvolvedor** Olá superior-direita do portal do publicador hello.

![Portal do desenvolvedor][api-management-developer-portal-menu]

Clique em **APIs** e clique em Olá **Calculadora** API.

![Portal do desenvolvedor][api-management-dev-portal-apis]

Clique em **Experimentar**.

![Experimente][api-management-dev-portal-try-it]

Clique em **enviar** e observe o status de resposta de saudação do **401 não autorizado**.

![Enviar][api-management-dev-portal-send-401]

solicitação de saudação não está autorizada porque Olá API back-end está protegido pelo Active Directory do Azure. Antes de chamar com êxito a API de saudação portal do desenvolvedor Olá deve ser configurado tooauthorize desenvolvedores usando OAuth 2.0. Esse processo é descrito nas seções a seguir de saudação.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Registrar o portal do desenvolvedor hello como um aplicativo AAD
Olá primeira etapa na configuração de desenvolvedores de tooauthorize portal do desenvolvedor hello usando OAuth 2.0 é o portal do desenvolvedor Olá tooregister como um aplicativo AAD. Isso é demonstrado começando em 8:27 vídeo hello.

Navegue toohello AD do Azure locatário da primeira etapa Olá neste vídeo, neste exemplo **APIMDemo** e navegue toohello **aplicativos** guia.

![Novo aplicativo][api-management-aad-new-application-devportal]

Clique em Olá **adicionar** botão toocreate um novo aplicativo do Active Directory do Azure e escolha **adicionar um aplicativo que minha organização esteja desenvolvendo**.

![Novo aplicativo][api-management-new-aad-application-menu]

Escolha **Web aplicativo e/ou API da Web**, insira um nome e clique em seta Avançar hello. Neste exemplo, **APIMDeveloperPortal** é usado.

![Novo aplicativo][api-management-aad-new-application-devportal-1]

Para **URL de logon** digite Olá URL de seu serviço de gerenciamento de API e acrescente `/signin`. Neste exemplo, `https://contoso5.portal.azure-api.net/signin` é usado.

Para **URL de Id do aplicativo** digite Olá URL de seu serviço de gerenciamento de API e acrescenta alguns caracteres exclusivos. Eles podem ser qualquer caractere desejado e, neste exemplo, `https://contoso5.portal.azure-api.net/dp` é usado. Quando a saudação desejado **propriedades do aplicativo** são configuradas, clique em aplicativo de saudação de toocreate hello marca de seleção.

![Novo aplicativo][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Configurar um servidor de autorização do OAuth 2.0 no Gerenciamento de API
Olá próxima etapa é tooconfigure um servidor de autorização OAuth 2.0 no gerenciamento de API. Esta etapa é demonstrada no hello vídeo começando em 9:43.

Clique em **segurança** no menu de gerenciamento de API Olá Olá esquerda, clique em **OAuth 2.0**e, em seguida, clique em **adicionar autorização** server.

![Adicionar servidor de autorização][api-management-add-authorization-server]

Insira um nome e uma descrição opcional na Olá **nome** e **descrição** campos. Esses campos são do servidor de autorização de saudação OAuth 2.0 tooidentify usado na instância do serviço de gerenciamento de API de saudação. Neste exemplo, **Demonstração de servidor de autorização** é usado. Mais tarde quando você especificar um toobe de servidor OAuth 2.0 usado para autenticação de uma API, você selecionará esse nome.

Para Olá **URL de página de registro de cliente** Insira um valor de espaço reservado como `http://localhost`.  Olá **URL de página de registro de cliente** pontos toohello página que os usuários podem usar toocreate e configurar suas próprias contas para provedores OAuth 2.0 que dão suporte ao gerenciamento de contas de usuário. Neste exemplo os usuários não criam e configuram suas próprias contas, é usado um espaço reservado.

![Adicionar servidor de autorização][api-management-add-authorization-server-1]

Em seguida, especifique a **URL de ponto de extremidade de autorização** e a **URL de ponto de extremidade de Token**.

![Servidor de autorização][api-management-add-authorization-server-1a]

Esses valores podem ser recuperados de saudação **pontos de extremidade do aplicativo** página do aplicativo AAD que você criou para o portal do desenvolvedor de saudação do hello. Navegue de pontos de extremidade de saudação tooaccess toohello **configurar** guia para o aplicativo do AAD hello e clique em **exibir pontos de extremidade**.

![Aplicativo][api-management-aad-devportal-application]

![Exibir pontos de extremidade][api-management-aad-view-endpoints]

Saudação de cópia **ponto de extremidade de autorização OAuth 2.0** e cole-a saudação **URL de ponto de extremidade de autorização** caixa de texto.

![Adicionar servidor de autorização][api-management-add-authorization-server-2]

Saudação de cópia **ponto de extremidade de token OAuth 2.0** e cole-a saudação **URL de ponto de extremidade de Token** caixa de texto.

![Adicionar servidor de autorização][api-management-add-authorization-server-2a]

Além disso toopasting no ponto de extremidade token hello, adicionar um parâmetro de corpo adicional denominado **recurso** e valor Olá use Olá **URI da Id do aplicativo** de saudação aplicativo AAD para o serviço de back-end de saudação foi criado quando o projeto do Visual Studio Olá foi publicado.

![URI da Id do aplicativo][api-management-aad-sso-uri]

Em seguida, especifique as credenciais do cliente hello. Essas são as credenciais de saudação para o recurso de saudação desejado tooaccess, nesse caso Olá portal do desenvolvedor.

![Credenciais do cliente][api-management-client-credentials]

Olá tooget **Id do cliente**, navegar toohello **configurar** guia do aplicativo AAD para Olá Olá de portal e a cópia do desenvolvedor de saudação **Id do cliente**.

Olá tooget **segredo do cliente** clique Olá **selecionar duração** suspensa no hello **chaves** seção e especificar um intervalo. Neste exemplo, 1 ano é usado.

![ID do cliente][api-management-aad-client-id]

Clique em **salvar** toosave Olá configuração e exibição Olá a chave. 

> [!IMPORTANT]
> Anote esta chave. Quando você fechar a janela de configuração do Active Directory do Azure hello, chave de saudação não pode ser exibida novamente.
> 
> 

Copiar Olá chave toohello área de transferência, switch back toohello portal do publicador, cole a chave de saudação na Olá **segredo do cliente** caixa de texto e clique em **salvar**.

![Adicionar servidor de autorização][api-management-add-authorization-server-3]

Imediatamente após as credenciais do cliente Olá é uma concessão de código de autorização. Copie esse código de autorização e switch back tooyour aplicativo de portal de desenvolvedor do AD do Azure para Configurar página e cole a concessão de autorização Olá Olá **URL de resposta** campo e, em seguida, clique em **salvar** novamente.

![URL de resposta][api-management-aad-reply-url]

Olá próxima etapa é tooconfigure permissões de saudação para o portal do desenvolvedor Olá aplicativo AAD. Clique em **permissões de aplicativo** e marque caixa Olá **ler dados do diretório**. Clique em **salvar** toosave isso alterar e, em seguida, clique em **Adicionar aplicativo**.

![Adicionar permissões][api-management-add-devportal-permissions]

Clique ícone de pesquisa hello, tipo **APIM** em hello a partir da caixa, selecione **APIMAADDemo**e clique em Olá toosave de marca de seleção.

![Adicionar permissões][api-management-aad-add-app-permissions]

Clique em **permissões delegadas** para **APIMAADDemo** e marque caixa Olá **acesso APIMAADDemo**e clique em **salvar**. Isso permite que o desenvolvedor de saudação serviço de back-end do aplicativo de portal tooaccess hello.

![Adicionar permissões][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Ativar a autorização de usuário OAuth 2.0 para Olá API de Calculadora
Olá servidor OAuth 2.0 já está configurado, você pode especificá-lo nas configurações de segurança de saudação para sua API. Esta etapa é demonstrada no hello vídeo começando na 14:30.

Clique em **APIs** no hello menus à esquerda e clique em **Calculadora** tooview e definir suas configurações.

![API de Calculadora][api-management-calc-api]

Navegue toohello **segurança** guia, verifique Olá **OAuth 2.0** caixa de seleção servidor de autorização desejado Olá select de saudação **servidor de autorização** lista suspensa e clique em **Salvar**.

![API de Calculadora][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Chame com sucesso Olá API de Calculadora do portal do desenvolvedor Olá
Autorização Olá OAuth 2.0 já está configurado no hello API, suas operações podem ser chamadas com êxito do Centro de desenvolvedores de saudação. Esta etapa é demonstrada no hello vídeo iniciando às 15:00.

Navegue back toohello **adicionar dois inteiros** operação do serviço de calculadora Olá no portal do desenvolvedor hello e clique em **Experimente**. Observação Olá novo item no hello **autorização** seção servidor de autorização toohello correspondente que acabou de adicionar.

![API de Calculadora][api-management-calc-authorization-server]

Selecione **código de autorização** da autorização Olá suspensa lista e digite as credenciais de saudação do hello conta toouse. Se você já tiver entrado com conta Olá que não pode ser solicitado.

![API de Calculadora][api-management-devportal-authorization-code]

Clique em **enviar** e observe hello **status da resposta** de **200 Okey** e resultados de saudação da operação de saudação no conteúdo de resposta de saudação.

![API de Calculadora][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Configurar uma saudação do aplicativo de desktop toocall API
próximo procedimento Olá Olá vídeo inicia às 16:30 e configura uma saudação do aplicativo de área de trabalho simples toocall API. Olá primeira etapa é um aplicativo de área de trabalho tooregister hello no AD do Azure e dê a ele serviço de back-end acesso toohello diretório e toohello. 18:25 há uma demonstração do aplicativo de área de trabalho hello chamar uma operação em Calculadora Olá API.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Configurar um toopre de política de validação de JWT-autorizar solicitações
Olá procedimento final vídeo Olá inicia às 20:48 e mostra como Olá toouse [validar JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) política toopre-autorizar solicitações, validando tokens de acesso de saudação de cada solicitação de entrada. Se a solicitação de saudação não for validada pelo Olá política validar JWT, solicitação de Olá está bloqueada pela API de gerenciamento e não é passada toohello back-end.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Para outra demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: recursos de gerenciamento de API mais](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too13:50. Avanço too15:00 toosee políticas de saudação configuradas no editor de diretiva de saudação e, em seguida, too18:50 para ver uma demonstração de como chamar uma operação do portal do desenvolvedor do hello com e sem Olá necessário token de autorização.

## <a name="next-steps"></a>Próximas etapas
* Confira mais [vídeos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sobre o Gerenciamento de API.
* Para outra maneiras toosecure seu serviço de back-end, consulte [autenticação mútua de certificado](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
