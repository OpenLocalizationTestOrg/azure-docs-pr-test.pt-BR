<span data-ttu-id="94d7b-101">emulador de armazenamento Olá dá suporte a uma única conta fixa e uma chave de autenticação conhecida para autenticação de chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="94d7b-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="94d7b-102">A conta e a chave são credenciais de chave compartilhada somente Olá permitidas para uso com o emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="94d7b-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="94d7b-103">Eles são:</span><span class="sxs-lookup"><span data-stu-id="94d7b-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="94d7b-104">chave de autenticação Olá suportada pelo emulador de armazenamento Olá destina-se somente para teste funcionalidade de saudação do seu código de autenticação de cliente.</span><span class="sxs-lookup"><span data-stu-id="94d7b-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="94d7b-105">Ela não serve para fins de segurança.</span><span class="sxs-lookup"><span data-stu-id="94d7b-105">It does not serve any security purpose.</span></span> <span data-ttu-id="94d7b-106">Você não pode usar a conta de armazenamento de produção e a chave com o emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="94d7b-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="94d7b-107">Você não deve usar a conta de saudação de desenvolvimento com dados de produção.</span><span class="sxs-lookup"><span data-stu-id="94d7b-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="94d7b-108">emulador de armazenamento Olá dá suporte à conexão via HTTP.</span><span class="sxs-lookup"><span data-stu-id="94d7b-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="94d7b-109">No entanto, o HTTPS é recomendado de protocolo para acessar recursos em uma conta de armazenamento do Azure de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="94d7b-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="94d7b-110">Conecte-se a conta do emulador toohello usando um atalho</span><span class="sxs-lookup"><span data-stu-id="94d7b-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="94d7b-111">Olá mais fácil maneira tooconnect toohello emulador de armazenamento de seu aplicativo é tooconfigure uma cadeia de caracteres de conexão no arquivo de configuração do aplicativo que referencia o atalho Olá `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="94d7b-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="94d7b-112">Aqui está um exemplo de um emulador de armazenamento de toohello da cadeia de caracteres de conexão em um *App. config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="94d7b-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="94d7b-113">Conecte-se toohello conta do emulador usando a chave e nome de conta bem conhecida Olá</span><span class="sxs-lookup"><span data-stu-id="94d7b-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="94d7b-114">toocreate uma cadeia de caracteres de conexão que referências Olá nome de conta do emulador e chave, você deve especificar pontos de extremidade Olá para cada Olá serviços que você deseja toouse do emulador Olá na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="94d7b-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="94d7b-115">Isso é necessário para que a cadeia de caracteres de conexão Olá fará referência Olá emulador pontos de extremidade, que são diferentes para uma conta de armazenamento de produção.</span><span class="sxs-lookup"><span data-stu-id="94d7b-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="94d7b-116">Por exemplo, valor de saudação de sua cadeia de caracteres de conexão será assim:</span><span class="sxs-lookup"><span data-stu-id="94d7b-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="94d7b-117">Esse valor é idêntico toohello atalho mostrado acima, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="94d7b-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="94d7b-118">Especificar um proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="94d7b-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="94d7b-119">Quando você estiver testando o seu serviço no emulador de armazenamento hello, você também pode especificar um toouse de proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="94d7b-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="94d7b-120">Isso pode ser útil para observar solicitações e respostas HTTP enquanto você estiver depurando operações em serviços de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="94d7b-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="94d7b-121">toospecify um proxy, adicionar Olá `DevelopmentStorageProxyUri` opção de cadeia de caracteres de conexão toohello e defina o URI de proxy toohello seu valor.</span><span class="sxs-lookup"><span data-stu-id="94d7b-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="94d7b-122">Por exemplo, aqui está uma cadeia de caracteres de conexão que aponta o emulador de armazenamento toohello e configura um proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="94d7b-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

