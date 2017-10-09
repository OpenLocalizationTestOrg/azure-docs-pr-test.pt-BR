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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="b7d0e-103">Conectando tooMedia conta de serviços usando o SDK do Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="b7d0e-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7d0e-104">REST</span><span class="sxs-lookup"><span data-stu-id="b7d0e-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="b7d0e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b7d0e-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="b7d0e-106">Este tópico descreve como tooobtain tooMicrosoft uma conexão programática Azure Media Services quando você está programando com hello SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="b7d0e-107">Conectando a serviços tooMedia</span><span class="sxs-lookup"><span data-stu-id="b7d0e-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="b7d0e-108">tooconnect tooMedia serviços por meio de programação, você deve ter configurado uma conta do Azure anteriormente, configurado serviços de mídia nessa conta e, em seguida, configurar um projeto do Visual Studio para desenvolvimento com hello SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="b7d0e-109">Para obter mais informações, consulte configuração para o desenvolvimento com hello SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="b7d0e-110">No final de saudação do processo de configuração de conta de serviços de mídia hello, você obteve seguinte Olá necessário valores de conexão.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="b7d0e-111">Use essas conexões programáticas toomake tooMedia serviços.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="b7d0e-112">O nome da conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-112">Your Media Services account name.</span></span>
* <span data-ttu-id="b7d0e-113">A chave da conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-113">Your Media Services account key.</span></span>

<span data-ttu-id="b7d0e-114">toofind esses valores, vá toohello Portal de gerenciamento do Azure, selecione sua conta de serviço de mídia e clique em hello "**gerenciar chaves**" ícone na Olá inferior da janela portal hello.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="b7d0e-115">Clicando em Olá ícone próxima tooeach texto caixa cópias Olá valor toohello sistema da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="b7d0e-116">Criando uma instância CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="b7d0e-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="b7d0e-117">toostart programar Media Services é necessário toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="b7d0e-118">Olá **CloudMediaContext** inclui referências tooimportant coleções incluindo trabalhos, ativos, arquivos, políticas de acesso e localizadores.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d0e-119">Olá **CloudMediaContext** a classe não é thread-safe.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="b7d0e-120">Você deve criar um novo CloudMediaContext por thread ou por conjunto de operações.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="b7d0e-121">O CloudMediaContext possui cinco sobrecargas de construtor.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="b7d0e-122">É recomendado toouse construtores que usam **MediaServicesCredentials** como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="b7d0e-123">Para obter mais informações, consulte Olá **reutilizando Tokens de serviço de controle de acesso** que segue.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="b7d0e-124">Hello exemplo a seguir usa o construtor público de CloudMediaContext(MediaServicesCredentials credentials) hello:</span><span class="sxs-lookup"><span data-stu-id="b7d0e-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="b7d0e-125">Reutilizando Tokens de serviço de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="b7d0e-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="b7d0e-126">Esta seção mostra como os tokens de tooreuse serviço de controle de acesso usando construtores de CloudMediaContext que usam MediaServicesCredentials como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="b7d0e-127">[Azure controle de acesso do Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (também conhecido como Access Control Service ou ACS) é um serviço baseado em nuvem que fornece uma maneira fácil de autenticação e autorização aos usuários acesso de toogain tootheir aplicativos de web.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="b7d0e-128">Controles de serviços de mídia do Microsoft Azure acessar serviços tooits embora protocolo OAuth que requer um token do ACS.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="b7d0e-129">Serviços de mídia recebe tokens de ACS de saudação de um servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="b7d0e-130">Ao desenvolver com hello SDK do Media Services, você pode escolher para tratar toonot tokens Olá porque Olá gerenciadores de código do SDK-los para você.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="b7d0e-131">No entanto, permitindo Olá SDK totalmente gerenciar solicitações de token de toounnecessary Olá ACS tokens clientes potenciais.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="b7d0e-132">A solicitação de tokens demora e consome recursos de cliente e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="b7d0e-133">Além disso, o servidor de ACS de saudação limita solicitações Olá se Olá taxa seja muito alta.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="b7d0e-134">limite de saudação é de 30 solicitações por segundo, consulte [limitações do serviço ACS](https://msdn.microsoft.com/library/gg185909.aspx) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="b7d0e-135">Começando com hello SDK de serviços de mídia versão 3.0.0.0, você pode reutilizar tokens ACS de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="b7d0e-136">Olá **CloudMediaContext** construtores que usam **MediaServicesCredentials** como um parâmetro permitem o compartilhamento tokens Olá ACS entre vários contextos.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="b7d0e-137">Olá MediaServicesCredentials classe encapsula as credenciais de serviços de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="b7d0e-138">Se um token ACS estiver disponível e seu tempo de expiração é conhecido, você pode criar uma nova instância de MediaServicesCredentials com token de saudação e passá-lo construtor toohello de CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="b7d0e-139">Observe que Olá SDK do Media Services atualiza automaticamente tokens sempre que eles expiram.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="b7d0e-140">Há duas maneiras tooreuse ACS tokens, conforme mostrado nos exemplos de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="b7d0e-141">Você pode armazenar em cache Olá **MediaServicesCredentials** objeto na memória (por exemplo, em uma variável de classe estáticos).</span><span class="sxs-lookup"><span data-stu-id="b7d0e-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="b7d0e-142">Em seguida, passe o construtor de CloudMediaContext de toohello de objeto Olá armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="b7d0e-143">objeto MediaServicesCredentials de saudação contém um token do ACS que pode ser reutilizado se ele ainda é válido.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="b7d0e-144">Se Olá token não é válido, que ele será atualizado pelo Olá usando credenciais de saudação do SDK do Media Services dado toohello MediaServicesCredentials construtor.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="b7d0e-145">Observe que Olá **MediaServicesCredentials** objeto obtém um token válido após Olá RefreshToken é chamado.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="b7d0e-146">Olá **CloudMediaContext** Olá chamadas **RefreshToken** método no construtor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="b7d0e-147">Se você estiver planejando armazenamento externo de tooan toosave de valores do token Olá, tomar se toocheck Olá TokenExpiration valor é válido antes de salvar os dados do token hello.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="b7d0e-148">Se não for válido, chame RefreshToken antes de armazenar em cache.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="b7d0e-149">Você também pode armazenar a cadeia de caracteres hello AccessToken e valores de TokenExpiration hello.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="b7d0e-150">valores Hello mais tarde podem ser usado toocreate MediaServicesCredentials um novo objeto com dados do token Olá armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="b7d0e-151">Isso é especialmente útil para cenários onde Olá token pode ser compartilhado com segurança entre vários processos ou computadores.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="b7d0e-152">Olá trechos de código a seguir chamam hello métodos SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage e UpdateTokenDataInExternalStorageIfNeeded que não estão definidos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="b7d0e-153">Você pode definir esses métodos toostore, recuperar e atualizar dados de token em um armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="b7d0e-154">Use Olá salva valores do token toocreate MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="b7d0e-155">Atualize cópia do token Olá no caso de Olá token tenha sido atualizado por Olá SDK do Media Services.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="b7d0e-156">Se você tiver várias contas de serviços de mídia (por exemplo, para fins ou distribuição geográfica de compartilhamento de carga) você pode armazenar em cache objetos MediaServicesCredentials usando a coleção de System.Collections.Concurrent.ConcurrentDictionary hello (Olá Coleção de ConcurrentDictionary representa uma coleção thread-safe de pares chave/valor que podem ser acessados por vários threads ao mesmo tempo).</span><span class="sxs-lookup"><span data-stu-id="b7d0e-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="b7d0e-157">Você pode usar as credenciais do hello GetOrAdd método tooget Olá armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="b7d0e-158">Conectar-se a conta de serviços de mídia tooa localizada na região do Norte da China Olá</span><span class="sxs-lookup"><span data-stu-id="b7d0e-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="b7d0e-159">Se sua conta está localizada na região do Norte da China hello, use Olá construtor a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7d0e-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="b7d0e-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7d0e-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="b7d0e-161">Armazenando valores de conexão na configuração</span><span class="sxs-lookup"><span data-stu-id="b7d0e-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="b7d0e-162">É um valores de conexão de toostore altamente recomendável, especialmente valores confidenciais como seu nome de conta e senha na configuração.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="b7d0e-163">Além disso, é uma prática recomendada tooencrypt configuração confidenciais de dados.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="b7d0e-164">Você pode criptografar o arquivo de configuração inteiro hello usando Olá Windows Encrypting File System (EFS).</span><span class="sxs-lookup"><span data-stu-id="b7d0e-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="b7d0e-165">Selecione tooenable EFS em um arquivo, clique com botão direito hello, **propriedades**e habilitar a criptografia em hello **avançado** guia Configurações. Ou você pode criar uma solução personalizada para criptografar as partes selecionadas de um arquivo de configuração usando a configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="b7d0e-166">Consulte [Criptografando informações de configuração usando configuração protegida](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7d0e-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="b7d0e-167">Olá após o arquivo App. config contém valores de conexão de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="b7d0e-168">Olá valores hello <appSettings> elemento são valores hello necessários que você obteve no processo de configuração de conta de serviços de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="b7d0e-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="b7d0e-169">tooretrieve valores de conexão de configuração, você pode usar o hello **ConfigurationManager** classe e, em seguida, atribuir Olá toofields de valores no seu código:</span><span class="sxs-lookup"><span data-stu-id="b7d0e-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="b7d0e-170">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="b7d0e-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b7d0e-171">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="b7d0e-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

