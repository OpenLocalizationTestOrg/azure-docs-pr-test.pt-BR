## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="6052a-101">Configurar a CLI do Azure para DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="6052a-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="6052a-102">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6052a-102">Before you begin</span></span>

<span data-ttu-id="6052a-103">Verifique se você tem Olá itens a seguir antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="6052a-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="6052a-104">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6052a-104">An Azure subscription.</span></span> <span data-ttu-id="6052a-105">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6052a-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6052a-106">Instale a versão mais recente Olá de saudação CLI do Azure, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="6052a-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="6052a-107">Mais informações estão disponíveis em [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6052a-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="6052a-108">Entrar tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="6052a-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="6052a-109">Abra uma janela do console e autentique com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="6052a-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="6052a-110">Para obter mais informações, consulte [login tooAzure de saudação CLI do Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="6052a-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="6052a-111">Mudar para o modo CLI</span><span class="sxs-lookup"><span data-stu-id="6052a-111">Switch CLI mode</span></span>

<span data-ttu-id="6052a-112">O DNS do Azure usa o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6052a-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="6052a-113">Verifique se que você alternar comandos modo toouse Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6052a-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="6052a-114">Selecione a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="6052a-114">Select hello subscription</span></span>

<span data-ttu-id="6052a-115">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="6052a-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="6052a-116">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6052a-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6052a-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6052a-117">Create a resource group</span></span>

<span data-ttu-id="6052a-118">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="6052a-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6052a-119">Isso é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6052a-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="6052a-120">No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="6052a-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="6052a-121">Você pode ignorar esta etapa se está usando um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="6052a-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="6052a-122">Registrar provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="6052a-122">Register resource provider</span></span>

<span data-ttu-id="6052a-123">Olá serviço DNS do Azure é gerenciado pelo provedor de recursos Microsoft. Network hello.</span><span class="sxs-lookup"><span data-stu-id="6052a-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="6052a-124">Sua assinatura do Azure deve ser registrado toouse este provedor de recursos antes de usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="6052a-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="6052a-125">Essa operação deve ser executa apenas uma vez para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="6052a-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

