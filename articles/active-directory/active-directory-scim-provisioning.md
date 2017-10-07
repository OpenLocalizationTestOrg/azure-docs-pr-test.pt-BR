---
title: "aaaUsing sistema para o gerenciamento de identidade de domínio cruzado provisionar automaticamente os usuários e grupos do Active Directory do Azure tooapplications | Microsoft Docs"
description: "Active Directory do Azure podem provisionar automaticamente os usuários e grupos tooany aplicativo ou a identidade do repositório que é apoiado por um serviço web com interface Olá definido na especificação do protocolo SCIM de saudação"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Usando o sistema de gerenciamento de identidade de domínio cruzado tooautomatically provisionar os usuários e grupos do Active Directory do Azure tooapplications

## <a name="overview"></a>Visão geral
Azure Active Directory (AD do Azure) podem provisionar automaticamente os usuários e grupos tooany aplicativo ou a identidade do repositório que é apoiado por um serviço web com interface Olá definido no hello [sistema de gerenciamento de identidade de domínio cruzado (SCIM) 2.0 especificação de protocolo](https://tools.ietf.org/html/draft-ietf-scim-api-19). Active Directory do Azure pode enviar solicitações toocreate, modificar ou excluir o serviço de web de toohello atribuído de usuários e grupos. serviço web de Hello, em seguida, pode traduzir essas solicitações em operações no repositório de identidades de destino hello. 

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. 



![][0]
*Figura 1: Provisionamento do repositório de identidades do Active Directory do Azure tooan por meio de um serviço web*

Esse recurso pode ser usado em conjunto com a funcionalidade de "traga seu próprio aplicativo" hello no AD do Azure tooenable-logon único e provisionamento para aplicativos que fornecem ou são apoiados por um serviço da web SCIM de usuário automático.

Há dois casos de uso para utilizar SCIM no Azure Active Directory:

* **Provisionamento de usuários e grupos tooapplications que oferecem suporte a SCIM** aplicativos que suportam SCIM 2.0 e usar os tokens de portador OAuth para autenticação funciona com o AD do Azure sem configuração.
* **Criar sua própria solução de provisionamento para aplicativos que oferecem suporte a outros provisionamento baseado em API** para aplicativos não-SCIM, você pode criar um tootranslate de ponto de extremidade SCIM entre o ponto de extremidade do hello SCIM do AD do Azure e oferece suporte a qualquer API Olá aplicativo para provisionamento do usuário. toohelp desenvolver um ponto de extremidade SCIM, fornecemos bibliotecas de infraestrutura de linguagem comum (CLI) junto com exemplos de código que mostram como toodo fornecem um ponto de extremidade SCIM e traduzir mensagens SCIM.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Provisionamento de usuários e grupos tooapplications que oferecem suporte a SCIM
O AD do Azure pode ser configurado tooautomatically atribuído de provisionar usuários e grupos tooapplications que implementam um [sistema para o gerenciamento de identidade de domínio cruzado 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) serviço web e aceitar os tokens de portador OAuth para autenticação . Aplicativos dentro da especificação de saudação SCIM 2.0 devem atender a esses requisitos:

* Oferece suporte à criação de usuários e/ou grupos, de acordo com a seção 3.3 da saudação protocolo SCIM.  
* Dá suporte à modificação de usuários e/ou grupos com solicitações de patch de acordo com a seção 3.5.2 Olá protocolo SCIM.  
* Dá suporte à recuperação de um recurso conhecido de acordo com a seção 3.4.1 Olá protocolo SCIM.  
* Oferece suporte ao consultar os usuários e/ou grupos, de acordo com a seção 3.4.2 Olá protocolo SCIM.  Por padrão, os usuários são consultados por externalId e os grupos são consultados por displayName.  
* Dá suporte à consulta de usuário por ID e pelo Gerenciador de acordo com a seção 3.4.2 Olá protocolo SCIM.  
* Oferece suporte ao consultar grupos por ID e por membro de acordo com a seção 3.4.2 Olá protocolo SCIM.  
* Aceita tokens de portador OAuth para autorização de acordo com a seção 2.1 de saudação protocolo SCIM.

Verifique com o seu provedor de aplicativo ou na documentação do seu provedor de aplicativo as declarações de compatibilidade com esses requisitos.

### <a name="getting-started"></a>Introdução
Aplicativos que dão suporte ao perfil SCIM Olá descrito neste artigo podem ser conectado tooAzure do Active Directory usando o recurso de "não Galeria aplicativo hello" na Galeria de aplicativos de saudação do AD do Azure. Depois de conectado, o Azure AD executa um processo de sincronização a cada 20 minutos em que ele consulta o ponto de extremidade do aplicativo hello SCIM para atribuídas a usuários e grupos e cria ou modifica-los de acordo com toohello detalhes da atribuição.

**tooconnect um aplicativo que oferece suporte a SCIM:**

1. Entrar muito[Olá portal do Azure](https://portal.azure.com). 
2. Procurar muito * * Active Directory do Azure > aplicativos da empresa e selecione **novo aplicativo > todos os > aplicativo Galeria não**.
3. Insira um nome para seu aplicativo e clique em **adicionar** ícone toocreate um objeto de aplicativo.
    
  ![][1]
  *Figura 2: Galeria de aplicativos do Azure AD*
    
4. Na tela de resultante hello, selecione Olá **provisionamento** guia na coluna esquerda hello.
5. Em Olá **modo de provisionamento** menu, selecione **automática**.
    
  ![][2]
  *Figura 3: Configurar o provisionamento em Olá portal do Azure*
    
6. Em Olá **URL do locatário** , digite a URL de saudação do ponto de extremidade do aplicativo hello SCIM. Exemplo: https://api.contoso.com/scim/v2/
7. Se o ponto de extremidade do hello SCIM requer um token de portador OAuth de um emissor que não sejam do AD do Azure, Olá cópia necessário token de portador OAuth em Olá opcional **segredo do Token** campo. Se esse campo estiver em branco, o Azure AD incluiu um token de portador OAuth emitido do Azure AD com cada solicitação. Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.
8. Clique em Olá **Conexão de teste** botão toohave Active Directory do Azure tentativa tooconnect toohello SCIM ponto de extremidade. Se Olá tentativas falharem, informações de erro são exibidas.  
9. Se tiver êxito Olá tentativas tooconnect toohello aplicativo, clique em **salvar** toosave credenciais de administrador de saudação.
10. Em Olá **mapeamentos** seção, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo. Selecione cada um atributos de saudação de tooreview que são sincronizados do Active Directory do Azure tooyour aplicativo. Olá atributos selecionados como **correspondência** propriedades são usadas toomatch Olá usuários e grupos em seu aplicativo para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

    >[!NOTE]
    >Opcionalmente, você pode desabilitar a sincronização de objetos de grupo desabilitando hello "grupos" mapeamento. 

11. Em **configurações**, Olá **escopo** campo define quais usuários e/ou grupos são sincronizados. Selecionar "Sincronização atribuído apenas usuários e grupos" (recomendado) sincronizará apenas os usuários e grupos atribuídos no hello **usuários e grupos** guia.
12. Depois que a configuração estiver concluída, alterar Olá **Status de provisionamento** muito**em**.
13. Clique em **salvar** toostart Olá serviço de provisionamento do AD do Azure. 
14. Se sincronizar apenas atribuídas a usuários e grupos (recomendados), ser se Olá de tooselect **usuários e grupos** guia e atribua usuários hello e/ou grupos que você deseja toosync.

Depois que a sincronização inicial Olá foi iniciado, você pode usar o hello **logs de auditoria** guia toomonitor progresso, que mostra todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo. Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Criando sua própria solução de provisionamento para qualquer aplicativo
Ao criar um serviço Web SCIM que interaja com o Active Directory do Azure, você poderá habilitar o logon único e o provisionamento de usuário automático para praticamente qualquer aplicativo que forneça uma API de provisionamento de usuário SOAP ou REST.

Veja como ele funciona:

1. O AD do Azure fornece uma biblioteca CLI denominada [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Os desenvolvedores e integradores de sistema podem usar essa toocreate de biblioteca e implantar uma empresa de serviço web baseado em SCIM capaz de se conectar o armazenamento de identidade do aplicativo do AD do Azure tooany.
2. Mapeamentos de são implementados no Olá web serviço toomap Olá usuário padronizado toohello usuário esquema e o protocolo exigido pelo aplicativo hello.
3. URL de ponto de extremidade Hello está registrado no AD do Azure como parte de um aplicativo personalizado na Galeria de aplicativo hello.
4. Usuários e grupos são atribuídos toothis aplicativo no AD do Azure. Após a atribuição, eles são colocados em um aplicativo de destino toohello fila toobe sincronizado. processo de sincronização de Olá tratamento fila Olá é executado a cada 20 minutos.

### <a name="code-samples"></a>Exemplos de código
toomake esse processo, um conjunto de [exemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) são fornecidas que criar um ponto de extremidade de serviço do SCIM web e demonstre o provisionamento automático. Um dos exemplos é de um provedor que mantém um arquivo com linhas de valores separados por vírgula representando usuários e grupos.  Olá outros é de um provedor que opera no serviço de gerenciamento de acesso e identidade do Amazon Web Services hello.  

**Pré-requisitos**

* Visual Studio 2013 ou posterior.
* [SDK do Azure para .NET](https://azure.microsoft.com/downloads/)
* Computador Windows que dá suporte a saudação ASP.NET framework 4.5 toobe usado como Olá ponto de extremidade SCIM. Esta máquina deve ser acessível da nuvem de saudação
* [Uma assinatura do Azure com uma versão de avaliação ou licenciada do Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* exemplo de AWS Amazon Hello requer bibliotecas do hello [AWS Kit de ferramentas do Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Para obter mais informações, consulte Olá Leiame arquivo incluído com o exemplo hello.

### <a name="getting-started"></a>Introdução
Olá tooimplement de maneira mais fácil solicitações de um ponto de extremidade SCIM pode aceitar a configuração do AD do Azure é toobuild e implantar o exemplo de código de saudação que gera o arquivo de valores separados por vírgulas (CSV) de tooa Olá usuários provisionados.

**toocreate um ponto de extremidade SCIM de exemplo:**

1. Baixar pacote de exemplo de código Olá em [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Descompacte o pacote hello e colocá-lo em seu computador Windows em um local como C:\AzureAD-BYOA-Provisioning-Samples\.
3. Nessa pasta, inicie a solução de FileProvisioningAgent Olá no Visual Studio.
4. Selecione **Ferramentas > Gerenciador de biblioteca de pacote > Package Manager Console**e executar Olá comandos Olá FileProvisioningAgent projeto tooresolve Olá solução referências a seguir:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Compile o projeto de FileProvisioningAgent de saudação.
6. Iniciar o aplicativo do Prompt de comando Olá no Windows (como administrador) e usar Olá **cd** comando toochange Olá diretório tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** pasta.
7. Execute Olá comando a seguir, substituindo < endereço ip > pelo nome de domínio ou endereço IP de saudação do computador do Windows hello:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. No Windows em **configurações do Windows > configurações de Internet e rede**, selecione Olá **Firewall do Windows > Configurações avançadas**e criar um **regra de entrada** que permite acesso de entrada tooport 9000.
9. Se o computador do Windows hello estiver atrás de um roteador, Olá roteador necessidades toobe configurado tooperform conversão de acesso de rede entre sua porta 9000 que é toohello exposto à internet e porta 9000 no computador do Windows hello. Isso é necessário para o AD do Azure toobe capaz de tooaccess esse ponto de extremidade na nuvem hello.

**tooregister Olá exemplo SCIM ponto de extremidade no AD do Azure:**

1. Entrar muito[Olá portal do Azure](https://portal.azure.com). 
2. Procurar muito * * Active Directory do Azure > aplicativos da empresa e selecione **novo aplicativo > todos os > aplicativo Galeria não**.
3. Insira um nome para seu aplicativo e clique em **adicionar** ícone toocreate um objeto de aplicativo. objeto de aplicativo Hello criado é aplicativo de destino de saudação toorepresent pretendido você seria provisionamento tooand implementação de ponto de extremidade SCIM Olá único de logon para o e não apenas.
4. Na tela de resultante hello, selecione Olá **provisionamento** guia na coluna esquerda hello.
5. Em Olá **modo de provisionamento** menu, selecione **automática**.
    
  ![][2]
  *Figura 4: Configurar o provisionamento em Olá portal do Azure*
    
6. Em Olá **URL do locatário** digite Olá expostos à internet URL e a porta de seu ponto de extremidade SCIM. Isso seria algo como http://testmachine.contoso.com:9000 ou http://<ip-address>:9000/, onde < endereço ip > é Olá internet expostos IP endereço.  
7. Se o ponto de extremidade do hello SCIM requer um token de portador OAuth de um emissor que não sejam do AD do Azure, Olá cópia necessário token de portador OAuth em Olá opcional **segredo do Token** campo. Se esse campo for deixado em branco, o Azure AD incluirá um token de portador OAuth emitido do Azure AD com cada solicitação. Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.
8. Clique em Olá **Conexão de teste** botão toohave Active Directory do Azure tentativa tooconnect toohello SCIM ponto de extremidade. Se Olá tentativas falharem, informações de erro são exibidas.  
9. Se tiver êxito Olá tentativas tooconnect toohello aplicativo, clique em **salvar** toosave credenciais de administrador de saudação.
10. Em Olá **mapeamentos** seção, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo. Selecione cada um atributos de saudação de tooreview que são sincronizados do Active Directory do Azure tooyour aplicativo. Olá atributos selecionados como **correspondência** propriedades são usadas toomatch Olá usuários e grupos em seu aplicativo para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.
11. Em **configurações**, Olá **escopo** campo define quais usuários e/ou grupos são sincronizados. Selecionar "Sincronização atribuído apenas usuários e grupos" (recomendado) sincronizará apenas os usuários e grupos atribuídos no hello **usuários e grupos** guia.
12. Depois que a configuração estiver concluída, alterar Olá **Status de provisionamento** muito**em**.
13. Clique em **salvar** toostart Olá serviço de provisionamento do AD do Azure. 
14. Se sincronizar apenas atribuídas a usuários e grupos (recomendados), ser se Olá de tooselect **usuários e grupos** guia e atribua usuários hello e/ou grupos que você deseja toosync.

Depois que a sincronização inicial Olá foi iniciado, você pode usar o hello **logs de auditoria** guia toomonitor progresso, que mostra todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo. Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

a etapa final Olá verificar exemplo hello é tooopen Olá arquivo TargetFile.csv na pasta de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug Olá no seu computador Windows. Após a saudação processo de provisionamento é executada, esse arquivo mostra detalhes de saudação de todos os atribuídos e provisionado usuários e grupos.

### <a name="development-libraries"></a>Bibliotecas de desenvolvimento
toodevelop seu próprio serviço da web que está em conformidade com a especificação de SCIM toohello, primeiro você se familiarizar com hello bibliotecas a seguir fornecido pela Microsoft toohelp acelerar o processo de desenvolvimento de saudação: 

1. As bibliotecas Common Language Infrastructure (CLI) são oferecidas para uso com linguagens que se baseiam na infraestrutura em questão, como C#. Uma dessas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara uma interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, mostrada na ilustração a seguir de saudação: um usando bibliotecas de saudação do desenvolvedor deve implementar essa interface com uma classe que pode ser chamada, genericamente, como um provedor. bibliotecas de saudação habilitar Olá desenvolvedor toodeploy um serviço web que está em conformidade com a especificação de SCIM toohello. serviço web de saudação ou pode ser hospedado em serviços de informações da Internet ou de qualquer assembly executável do Common Language Infrastructure. Solicitação é convertida em métodos do provedor de toohello chamadas, que poderiam ser programados Olá toooperate de desenvolvedor em algum armazenamento de identidade.
  
  ![][3]
  
2. [Express manipuladores de rotas](http://expressjs.com/guide/routing.html) estão disponíveis para analisar objetos de solicitação de Node. js que representam chamadas (conforme definido pela especificação de SCIM de saudação), feitas serviço de web tooa Node. js.   

### <a name="building-a-custom-scim-endpoint"></a>Criando um ponto de extremidade SCIM personalizado
Usando bibliotecas de CLI hello, os desenvolvedores que usam essas bibliotecas podem hospedar seus serviços de qualquer assembly do Common Language Infrastructure executável, ou em serviços de informações da Internet. Aqui está o código de exemplo para hospedar um serviço em um assembly executável, no endereço Olá http://localhost:9000: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Esse serviço deve ter um HTTP endereço e servidor de certificado de autenticação de quais hello autoridade de certificação raiz é um dos seguinte hello: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* Verisign
* WoSign

Um certificado de autenticação de servidor pode ser associado tooa porta em um host do Windows usando o utilitário de shell de rede Olá: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Aqui, o valor de Olá fornecido para o argumento de certhash Olá é impressão digital de saudação do certificado Olá, enquanto o valor de Olá fornecido para o argumento de appid Olá é um identificador global exclusivo arbitrário.  

serviço de saudação toohost em serviços de informações da Internet, um desenvolvedor criaria um assembly de biblioteca de código CLA com uma classe chamada inicialização no espaço para nome padrão de saudação do assembly hello.  Veja um exemplo dessa classe: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Manipulando a autenticação do ponto de extremidade
As solicitações do Active Directory do Azure incluem um token de portador do OAuth 2.0.   Qualquer solicitação de saudação serviço receptor deve autenticar emissor hello como sendo o Active Directory do Azure em nome do locatário do Active Directory do Azure Olá esperado, para acesso toohello serviço de web do Azure Active Directory Graph.  Token Olá, emissor de saudação é identificado por uma declaração de iss, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  Neste exemplo, o endereço de base de saudação do valor de declaração hello, https://sts.windows.net, identifica o Active Directory do Azure como Olá emissor, enquanto o segmento de endereço relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello é um identificador exclusivo do hello Azure Active Locatário de diretório em nome do qual Olá token foi emitido.  Se Olá token foi emitido para acessar o serviço web do Azure Active Directory Graph hello, em seguida, identificador Olá desse serviço, 00000002-0000-0000-c000-000000000000, deve ser no valor de saudação do aud do token de saudação de declaração.  

Os desenvolvedores que usam bibliotecas CLA Olá fornecidas pela Microsoft para a criação de um serviço SCIM podem autenticar solicitações do Azure Active Directory usando o pacote do ActiveDirectory Olá seguindo estas etapas: 

1. Em um provedor implementa a propriedade de Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de saudação fazendo com que ele retornar um toobe método chamado sempre que o serviço Olá é iniciado: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Adicione Olá após código toothat método toohave tooany qualquer solicitação de pontos de extremidade do serviço Olá autenticado como bearing um token emitido pelo Active Directory do Azure em nome de um locatário especificado, para acesso toohello serviço de web do Azure AD Graph: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Esquema de usuários e grupos
Active Directory do Azure pode provisionar os dois tipos de recursos tooSCIM serviços da web.  Esses tipos de recurso são usuários e grupos.  

Recursos do usuário são identificados pelo identificador do esquema hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, que está incluído nesta especificação de protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  mapeamento de padrão de saudação de atributos de saudação de usuários em atributos do Active Directory do Azure toohello de recursos de urn: ietf:params:scim:schemas:extension:enterprise:2.0:User é fornecido na tabela 1, abaixo.  

Recursos do grupo são identificados pelo identificador do esquema hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Tabela 2, abaixo, o mapeamento de padrão mostra Olá de atributos de saudação de grupos de atributos do Active Directory do Azure toohello de recursos de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  

### <a name="table-1-default-user-attribute-mapping"></a>Tabela 1: Mapeamento padrão de atributo do usuário
| Usuário do Active Directory do Azure | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |ativo |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |título |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| Serviço Móvel |phoneNumbers[type eq "mobile"].value |
| ID do objeto |ID |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| sobrenome |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>Tabela 2: Mapeamento padrão de atributo do grupo
| Grupo do Active Directory do Azure | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |displayName |
| membros |membros |
| ID do objeto |ID |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>Provisionamento e desprovisionamento de usuários
Olá mensagens de saudação do ilustração mostra que o Active Directory do Azure envia tooa SCIM serviço toomanage saudação do ciclo de vida de um usuário em outro repositório de identidade a seguir. diagrama de saudação também mostra como um serviço SCIM implementado usando bibliotecas CLI Olá fornecido pela Microsoft para criar que tais serviços essas solicitações se traduz em métodos de toohello chamadas de um provedor.  

![][4]
*Figura 5: Sequência de provisionamento e desprovisionamento de usuário*

1. Consultas do Active Directory do Azure Olá serviço para um usuário com um valor de atributo externalId correspondência do valor de atributo de mailNickname Olá de um usuário no AD do Azure. Olá consulta é expressa como uma solicitação do protocolo HTTP (Hypertext Transfer), como neste exemplo, no qual jyoung é um exemplo de um mailNickname de um usuário no Active Directory do Azure: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Se serviço Olá foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de consulta do provedor do serviço de saudação.  Aqui está a assinatura de saudação do método: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Esta é a definição de saudação da interface de Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  Em Olá seguindo o exemplo de uma consulta para um usuário com um valor especificado para o atributo de externalId hello, valores de argumentos Olá passados toohello método de consulta são: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Se Olá resposta tooa toohello web serviço de consulta para um usuário com um valor de atributo externalId que coincide com o valor do atributo mailNickname Olá de um usuário não retornar todos os usuários, Active Directory do Azure solicita que provisão de serviço Olá um usuário correspondente toohello um no Active Directory do Azure.  Veja um exemplo de tal solicitação: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM significa que a solicitação toohello uma chamada de método de criação de saudação do provedor de.  método Create da saudação tem essa assinatura: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  Em uma solicitação tooprovision um usuário, o valor de saudação do argumento de recurso Olá é uma instância de saudação Microsoft.SystemForCrossDomainIdentityManagement. Classe Core2EnterpriseUser, definida na biblioteca de Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.  Se o usuário de Olá Olá solicitação tooprovision for bem-sucedida, em seguida, hello implementação do método hello é tooreturn esperada uma instância do hello Microsoft.SystemForCrossDomainIdentityManagement. Classe Core2EnterpriseUser, com valor de saudação da propriedade do identificador de Olá definir toohello o identificador exclusivo do usuário recentemente provisionados hello.  

3. tooupdate um usuário conhecido tooexist em um repositório de identidade apoiado por um SCIM, Active Directory do Azure continua solicitando o estado atual de saudação do usuário do serviço de saudação com uma solicitação, como: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Em um serviço criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, a solicitação de saudação é convertida em toohello uma chamada de método de recuperação de saudação do provedor de.  Aqui está a assinatura de saudação do método de recuperação hello: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  No exemplo de saudação do estado atual de saudação do tooretrieve solicitação de um usuário, valores hello das propriedades de saudação do objeto de saudação fornecido como valor de saudação do argumento de parâmetros de saudação são: 
  
  * Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Se um atributo de referência for toobe atualizado, em seguida, Active Directory do Azure consultas Olá serviço toodetermine ou não hello atual valor do atributo de referência de saudação no repositório de identidades Olá apoiado por serviço Olá já corresponde o valor de saudação do atributo no Active Directory do Azure. Para usuários, Olá somente de quais hello valor atual é consultado dessa maneira é Olá manager atributo. Aqui está um exemplo de uma solicitação toodetermine se o atributo de gerente de saudação de um objeto específico do usuário atualmente tem um determinado valor: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Olá valor de parâmetro de consulta de atributos hello, id, significa que se existe um objeto de usuário que satisfaz a expressão Olá fornecido como valor de saudação do parâmetro de consulta de filtro de saudação, serviço Olá é esperado toorespond com um urn: ietf:params:scim:schemas: núcleo: 2.0:User ou urn: ietf:params:scim:schemas:extension:enterprise:2.0:User recursos, incluindo apenas o valor de saudação do atributo de id do recurso.  Olá valor Olá **id** atributo conhecido toohello solicitante. Ele está incluído no valor de saudação do parâmetro de consulta de filtro Olá; Olá finalidade pedindo a ela é realmente toorequest uma representação mínima de um recurso que satisfazem a expressão de filtro hello como uma indicação de se qualquer tal objeto existente.   

  Se serviço Olá foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de consulta do provedor do serviço de saudação. valor de saudação das propriedades de saudação do objeto de saudação fornecido como valor de saudação do argumento de parâmetros de saudação são da seguinte maneira: 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  Aqui, valor de saudação do índice Olá x pode ser 0 e valor Olá Olá índice y pode ser 1, ou Olá valor x pode ser 1 e valor Olá y pode ser 0, dependendo da ordem de saudação de expressões de saudação do parâmetro de consulta de filtro de saudação.   

5. Aqui está um exemplo de uma solicitação de tooupdate de serviço do Active Directory do Azure tooan SCIM um usuário: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  bibliotecas do Microsoft Common Language Infrastructure Olá para implementar serviços SCIM converterá solicitação Olá em toohello uma chamada de método de atualização do provedor do serviço hello. Aqui está a assinatura Olá Olá método de atualização: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    No exemplo hello de uma solicitação de tooupdate um usuário, o objeto de saudação fornecido como valor de saudação do argumento de patch Olá tem esses valores de propriedade: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. um usuário de um repositório de identidade de provisionar toode apoiado por um serviço SCIM, AD do Azure envia uma solicitação, como: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Se o serviço de saudação foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de exclusão de saudação do provedor de.   Esse método tem esta assinatura: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  objeto Olá fornecido como valor de saudação do argumento de resourceIdentifier Olá tem esses valores de propriedade no exemplo hello de uma solicitação toode-provisionar um usuário: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Provisionamento e desprovisionamento de grupo
Olá mensagens de saudação do ilustração mostra que AcD Azure envia tooa SCIM serviço toomanage saudação do ciclo de vida de um grupo em outro repositório de identidade a seguir.  Essas mensagens são diferentes de mensagens de saudação pertencente toousers de três maneiras: 

* esquema de saudação de um recurso de grupo é identificada como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Solicitações tooretrieve grupos estipulam atributo Olá membros é toobe excluído de qualquer recurso fornecido na solicitação de toohello de resposta.  
* Toodetermine solicitações se um atributo de referência tem um determinado valor são solicitações sobre o atributo de membros de saudação.  

![][5]
*Figura 6: sequência de provisionamento e desprovisionamento de grupo*

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md)
* [Personalizando os mapeamentos de atributos para provisionamento de usuários](active-directory-saas-customizing-attribute-mappings.md)
* [Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de escopo para provisionamento de usuários](active-directory-saas-scoping-filters.md)
* [Notificações de provisionamento de conta](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
