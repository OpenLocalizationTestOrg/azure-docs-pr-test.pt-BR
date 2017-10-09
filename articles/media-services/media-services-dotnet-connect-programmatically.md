---
title: "Conta de serviços de tooMedia aaaConnecting usando .NET"
description: "Este tópico demonstra como usar os serviços de tooMedia tooconnect .NET."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Conectando tooMedia conta de serviços usando o SDK do Media Services para .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Este tópico descreve como tooobtain tooMicrosoft uma conexão programática Azure Media Services quando você está programando com hello SDK do Media Services para .NET.

## <a name="connecting-toomedia-services"></a>Conectando a serviços tooMedia
tooconnect tooMedia serviços por meio de programação, você deve ter configurado uma conta do Azure anteriormente, configurado serviços de mídia nessa conta e, em seguida, configurar um projeto do Visual Studio para desenvolvimento com hello SDK do Media Services para .NET. Para obter mais informações, consulte configuração para o desenvolvimento com hello SDK do Media Services para .NET.

No final de saudação do processo de configuração de conta de serviços de mídia hello, você obteve seguinte Olá necessário valores de conexão. Use essas conexões programáticas toomake tooMedia serviços.

* O nome da conta de serviços de mídia.
* A chave da conta de serviços de mídia.

toofind esses valores, vá toohello Portal de gerenciamento do Azure, selecione sua conta de serviço de mídia e clique em hello "**gerenciar chaves**" ícone na Olá inferior da janela portal hello. Clicando em Olá ícone próxima tooeach texto caixa cópias Olá valor toohello sistema da área de transferência.

## <a name="creating-a-cloudmediacontext-instance"></a>Criando uma instância CloudMediaContext
toostart programar Media Services é necessário toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor. Olá **CloudMediaContext** inclui referências tooimportant coleções incluindo trabalhos, ativos, arquivos, políticas de acesso e localizadores.

> [!NOTE]
> Olá **CloudMediaContext** a classe não é thread-safe. Você deve criar um novo CloudMediaContext por thread ou por conjunto de operações.
> 
> 

O CloudMediaContext possui cinco sobrecargas de construtor. É recomendado toouse construtores que usam **MediaServicesCredentials** como um parâmetro. Para obter mais informações, consulte Olá **reutilizando Tokens de serviço de controle de acesso** que segue. 

Hello exemplo a seguir usa o construtor público de CloudMediaContext(MediaServicesCredentials credentials) hello:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Reutilizando Tokens de serviço de controle de acesso
Esta seção mostra como os tokens de tooreuse serviço de controle de acesso usando construtores de CloudMediaContext que usam MediaServicesCredentials como um parâmetro.

[Azure controle de acesso do Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (também conhecido como Access Control Service ou ACS) é um serviço baseado em nuvem que fornece uma maneira fácil de autenticação e autorização aos usuários acesso de toogain tootheir aplicativos de web. Controles de serviços de mídia do Microsoft Azure acessar serviços tooits embora protocolo OAuth que requer um token do ACS. Serviços de mídia recebe tokens de ACS de saudação de um servidor de autorização.

Ao desenvolver com hello SDK do Media Services, você pode escolher para tratar toonot tokens Olá porque Olá gerenciadores de código do SDK-los para você. No entanto, permitindo Olá SDK totalmente gerenciar solicitações de token de toounnecessary Olá ACS tokens clientes potenciais. A solicitação de tokens demora e consome recursos de cliente e servidor de saudação. Além disso, o servidor de ACS de saudação limita solicitações Olá se Olá taxa seja muito alta. limite de saudação é de 30 solicitações por segundo, consulte [limitações do serviço ACS](https://msdn.microsoft.com/library/gg185909.aspx) para obter mais detalhes.

Começando com hello SDK de serviços de mídia versão 3.0.0.0, você pode reutilizar tokens ACS de saudação. Olá **CloudMediaContext** construtores que usam **MediaServicesCredentials** como um parâmetro permitem o compartilhamento tokens Olá ACS entre vários contextos. Olá MediaServicesCredentials classe encapsula as credenciais de serviços de mídia hello. Se um token ACS estiver disponível e seu tempo de expiração é conhecido, você pode criar uma nova instância de MediaServicesCredentials com token de saudação e passá-lo construtor toohello de CloudMediaContext. Observe que Olá SDK do Media Services atualiza automaticamente tokens sempre que eles expiram. Há duas maneiras tooreuse ACS tokens, conforme mostrado nos exemplos de saudação abaixo.

* Você pode armazenar em cache Olá **MediaServicesCredentials** objeto na memória (por exemplo, em uma variável de classe estáticos). Em seguida, passe o construtor de CloudMediaContext de toohello de objeto Olá armazenado em cache. objeto MediaServicesCredentials de saudação contém um token do ACS que pode ser reutilizado se ele ainda é válido. Se Olá token não é válido, que ele será atualizado pelo Olá usando credenciais de saudação do SDK do Media Services dado toohello MediaServicesCredentials construtor.
  
    Observe que Olá **MediaServicesCredentials** objeto obtém um token válido após Olá RefreshToken é chamado. Olá **CloudMediaContext** Olá chamadas **RefreshToken** método no construtor de saudação. Se você estiver planejando armazenamento externo de tooan toosave de valores do token Olá, tomar se toocheck Olá TokenExpiration valor é válido antes de salvar os dados do token hello. Se não for válido, chame RefreshToken antes de armazenar em cache.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Você também pode armazenar a cadeia de caracteres hello AccessToken e valores de TokenExpiration hello. valores Hello mais tarde podem ser usado toocreate MediaServicesCredentials um novo objeto com dados do token Olá armazenado em cache.  Isso é especialmente útil para cenários onde Olá token pode ser compartilhado com segurança entre vários processos ou computadores.
  
    Olá trechos de código a seguir chamam hello métodos SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage e UpdateTokenDataInExternalStorageIfNeeded que não estão definidos neste exemplo. Você pode definir esses métodos toostore, recuperar e atualizar dados de token em um armazenamento externo. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Use Olá salva valores do token toocreate MediaServicesCredentials.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Atualize cópia do token Olá no caso de Olá token tenha sido atualizado por Olá SDK do Media Services. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Se você tiver várias contas de serviços de mídia (por exemplo, para fins ou distribuição geográfica de compartilhamento de carga) você pode armazenar em cache objetos MediaServicesCredentials usando a coleção de System.Collections.Concurrent.ConcurrentDictionary hello (Olá Coleção de ConcurrentDictionary representa uma coleção thread-safe de pares chave/valor que podem ser acessados por vários threads ao mesmo tempo). Você pode usar as credenciais do hello GetOrAdd método tooget Olá armazenado em cache. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Conectar-se a conta de serviços de mídia tooa localizada na região do Norte da China Olá
Se sua conta está localizada na região do Norte da China hello, use Olá construtor a seguir:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Por exemplo:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Armazenando valores de conexão na configuração
É um valores de conexão de toostore altamente recomendável, especialmente valores confidenciais como seu nome de conta e senha na configuração. Além disso, é uma prática recomendada tooencrypt configuração confidenciais de dados. Você pode criptografar o arquivo de configuração inteiro hello usando Olá Windows Encrypting File System (EFS). Selecione tooenable EFS em um arquivo, clique com botão direito hello, **propriedades**e habilitar a criptografia em hello **avançado** guia Configurações. Ou você pode criar uma solução personalizada para criptografar as partes selecionadas de um arquivo de configuração usando a configuração protegida. Consulte [Criptografando informações de configuração usando configuração protegida](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Olá após o arquivo App. config contém valores de conexão de Olá necessário. Olá valores hello <appSettings> elemento são valores hello necessários que você obteve no processo de configuração de conta de serviços de mídia hello.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve valores de conexão de configuração, você pode usar o hello **ConfigurationManager** classe e, em seguida, atribuir Olá toofields de valores no seu código:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

