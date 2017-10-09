<span data-ttu-id="68a61-101">Aplicativos .NET podem usar Olá **Stackexchange** cliente de cache, que pode ser configurado no Visual Studio usando um pacote NuGet que simplifica a configuração de saudação do aplicativos clientes de cache.</span><span class="sxs-lookup"><span data-stu-id="68a61-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="68a61-102">Para obter mais informações, consulte Olá [Stackexchange](http://github.com/StackExchange/StackExchange.Redis) github página e hello [documentação do cliente de cache Stackexchange](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="68a61-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="68a61-103">tooconfigure um aplicativo cliente no Visual Studio usando Olá pacote NuGet stackexchange. Redis, clique com botão direito Olá em **Solution Explorer** e escolha **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="68a61-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Gerenciar pacotes NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="68a61-105">Tipo **Stackexchange** ou **Stackexchange** na caixa de texto de pesquisa hello, selecione a versão desejada de saudação nos resultados de saudação e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="68a61-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="68a61-106">Se você preferir toouse uma versão de nome forte do hello **Stackexchange** biblioteca de cliente, escolha **Stackexchange**; caso contrário, escolha **Stackexchange**.</span><span class="sxs-lookup"><span data-stu-id="68a61-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![Pacote NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="68a61-108">Olá NuGet pacote baixa e adiciona Olá necessárias referências de assembly para tooaccess seu aplicativo de cliente Cache Redis do Azure com o cliente de cache Stackexchange hello.</span><span class="sxs-lookup"><span data-stu-id="68a61-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="68a61-109">Se você já tiver configurado seu toouse Stackexchange do projeto, você pode verificar para o pacote de toohello atualizações de saudação **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="68a61-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="68a61-110">toocheck para e versões de instalação atualizada do hello pacote NuGet stackexchange. Redis, clique em **atualizações** em Olá Olá **NuGet Package Manager** janela.</span><span class="sxs-lookup"><span data-stu-id="68a61-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="68a61-111">Se um toohello de atualização de pacote NuGet Stackexchange estiver disponível, você pode atualizar sua versão do projeto toouse Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="68a61-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="68a61-112">Você também pode instalar Olá pacote NuGet Stackexchange clicando **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu e Olá em execução Após o comando Olá **Package Manager Console** janela.</span><span class="sxs-lookup"><span data-stu-id="68a61-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
