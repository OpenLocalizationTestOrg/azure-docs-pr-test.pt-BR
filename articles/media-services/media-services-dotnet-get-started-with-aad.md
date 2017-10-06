---
title: "aaaUse tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com o .NET | Microsoft Docs"
description: "Este tópico mostra como toouse tooaccess de autenticação do Azure Active Directory (AD do Azure) do Azure Media Services (AMS) API com .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Usar tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com .NET

A partir do windowsazure.mediaservices 4.0.0.4, os Serviços de Mídia do Azure dão suporte à autenticação baseada no Azure AD (Azure Active Directory). Este tópico mostra como toouse tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com o Microsoft .NET.

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta do Azure. Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Uma conta dos Serviços de Mídia. Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).
- Olá mais recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacote.
- Familiaridade com o tópico Olá [acessar API do Azure Media Services visão geral de autenticação do AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Ao usar a autenticação do Azure AD com os Serviços de Mídia do Azure, você pode fazer a autenticação usando uma destas duas maneiras:

- **Autenticação de usuário** autentica um usuário que está usando Olá aplicativo toointeract com recursos de serviços de mídia do Azure. aplicativo interativo do Hello primeiro deve solicitar credenciais ao usuário Olá. Um exemplo é um aplicativo de console de gerenciamento que é usado por usuários autorizados toomonitor trabalhos de codificação ou transmissão ao vivo. 
- A **autenticação de entidade de serviço** autentica um serviço. Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços daemon, serviços de camada intermediária ou trabalhos agendados, como aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs ou microsserviços.

>[!IMPORTANT]
>Atualmente, os Serviços de Mídia do Azure dão suporte a um modelo de autenticação do Serviço de Controle de Acesso do Azure. No entanto, a autorização de controle de acesso será toobe preterido no dia 1 de junho de 2018. É recomendável que você migre o modelo de autenticação do Active Directory do Azure tooan assim que possível.

## <a name="get-an-azure-ad-access-token"></a>Obter um token de acesso do Azure AD

tooconnect toohello API de serviços de mídia do Azure com a autenticação do AD do Azure, o aplicativo de cliente de Olá precisa toorequest um token de acesso do AD do Azure. Quando você usa o cliente .NET de serviços de mídia de saudação SDK, muitos dos detalhes de saudação sobre como tooacquire um token de acesso do AD do Azure são encapsuladas e simplificada para você no hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) e [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes. 

Por exemplo, você não precisa tooprovide autoridade de saudação do AD do Azure, o URI de recurso de serviços de mídia ou o nativo detalhes do aplicativo do Azure AD. Estes são os valores conhecidos que já são configurados por Olá classe de provedor de token de acesso do AD do Azure. 

Se você não estiver usando o SDK do .NET do Azure Media Service, recomendamos que você use Olá [biblioteca de autenticação do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md). tooget valores para parâmetros de saudação que você precisa toouse com biblioteca de autenticação do AD do Azure, consulte [usar configurações de autenticação tooaccess portal do Azure AD do Azure Olá](media-services-portal-get-started-with-aad.md).

Você também tem a opção de saudação de substituir a implementação padrão Olá Olá **AzureAdTokenProvider** com sua própria implementação.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Instalar e configurar o SDK do .NET dos Serviços de Mídia do Azure

>[!NOTE] 
>autenticação toouse AD do Azure com hello SDK do Media Services .NET, você precisa toohave hello mais recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacote. Além disso, adicione uma referência toohello **ActiveDirectory** assembly. Se você estiver usando um aplicativo existente, incluem hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly. 

1. No Visual Studio, crie um novo aplicativo de console C#.
2. Saudação de uso [windowsazure. mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de pacote do NuGet **SDK do Azure Media Services .NET**. 

    referências de tooadd usando o NuGet, levar Olá etapas a seguir: em **Solution Explorer**, nome do projeto hello e, em seguida, selecione **gerenciar pacotes do NuGet**. Em seguida, pesquise **windowsazure.mediaservices** e selecione **Instalar**.
    
    -ou-

    Execução hello seguinte comando no **Package Manager Console** no Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Adicionar **usando** tooyour código-fonte.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Usar a autenticação de usuário

tooconnect toohello API de serviços de mídia do Azure com a opção de autenticação de usuário hello, aplicativo de cliente Olá precisa toorequest um token do AD do Azure usando Olá parâmetros a seguir:  

- Ponto de extremidade do locatário do Azure AD. informações de locatário Olá podem ser recuperadas da saudação portal do Azure. Passe o mouse sobre Olá assinado usuário no canto superior direito de saudação.
- URI de recurso dos Serviços de Mídia.
- ID do cliente do aplicativo (nativo) dos Serviços de Mídia. 
- URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia. 

valores de saudação para esses parâmetros podem ser encontrados em **AzureEnvironments.AzureCloudEnvironment**. Olá **AzureEnvironments.AzureCloudEnvironment** constante é um auxiliar na Olá .NET SDK tooget definições de variável de ambiente certo Olá para um Data Center pública do Azure. 

Ele contém configurações de ambiente predefinida para acessar os serviços de mídia em centros de dados públicos Olá somente. Para regiões de nuvem soberana ou governamental, use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment**, respectivamente.

saudação de exemplo de código a seguir cria um token:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart programação no Media Services, você precisa toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor. Olá **CloudMediaContext** inclui referências tooimportant coleções incluindo trabalhos, ativos, arquivos, políticas de acesso e localizadores. 

Você também precisa toopass Olá **URI do Media Services de REST do recurso** toohello **CloudMediaContext** construtor. URI de recurso Olá tooget serviços REST de mídia de entrada toohello portal do Azure, selecione sua conta de serviços de mídia do Azure, selecione **acesso à API**e, em seguida, selecione **conectar os serviços de mídia tooAzure com usuário autenticação**. 

Olá exemplo de código a seguir cria um **CloudMediaContext** instância:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

saudação de exemplo a seguir mostra como toocreate Olá contexto de token e saudação do AD do Azure:

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Se você obtiver uma exceção que diz "servidor remoto Olá retornou um erro: não autorizado (401)," consulte Olá [controle de acesso](media-services-use-aad-auth-to-access-ams-api.md#access-control) seção acesso a API de serviços de mídia do Azure com visão geral de autenticação do AD do Azure.

## <a name="use-service-principal-authentication"></a>Usar a autenticação de entidade de serviço
    
tooconnect toohello API de serviços de mídia do Azure com a opção de entidade de serviço hello, seu aplicativo de camada intermediária (API da web ou aplicativo web) precisa toorequests um token do AD do Azure com hello parâmetros a seguir:  

- Ponto de extremidade do locatário do Azure AD. informações de locatário Olá podem ser recuperadas da saudação portal do Azure. Passe o mouse sobre Olá assinado usuário no canto superior direito de saudação.
- URI de recurso dos Serviços de Mídia.
- Valores de aplicativo do Azure AD: Olá **ID do cliente** e **segredo do cliente**.

Olá valores hello **ID do cliente** e **segredo do cliente** parâmetros podem ser encontrados no hello portal do Azure. Para obter mais informações, consulte [guia de Introdução com o uso de autenticação do AD do Azure Olá portal do Azure](media-services-portal-get-started-with-aad.md).

Olá exemplo de código a seguir cria um token usando Olá **AzureAdTokenCredentials** construtor **AzureAdClientSymmetricKey** como um parâmetro: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Você também pode especificar Olá **AzureAdTokenCredentials** construtor **AzureAdClientCertificate** como um parâmetro. 

Para obter instruções sobre como toocreate e configurar um certificado em um formulário que pode ser usado pelo AD do Azure, consulte [tooAzure AD em aplicativos de daemon com certificados - etapas de configuração manual de autenticação](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart programação no Media Services, você precisa toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor. Você também precisa toopass Olá **URI do Media Services de REST do recurso** toohello **CloudMediaContext** construtor. Você pode obter Olá **URI do Media Services de REST do recurso** valor da saudação também portal do Azure.

Olá exemplo de código a seguir cria um **CloudMediaContext** instância:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
saudação de exemplo a seguir mostra como toocreate Olá contexto de token e saudação do AD do Azure:

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Próximas etapas

Introdução ao [carregando arquivos tooyour conta](media-services-dotnet-upload-files.md).
