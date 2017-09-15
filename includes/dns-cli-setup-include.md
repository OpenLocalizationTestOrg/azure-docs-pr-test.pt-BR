## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="1bc84-101">Configurar a CLI do Azure para DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="1bc84-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="1bc84-102">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1bc84-102">Before you begin</span></span>

<span data-ttu-id="1bc84-103">Antes de começar a configurar, verifique se você tem os itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="1bc84-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="1bc84-104">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc84-104">An Azure subscription.</span></span> <span data-ttu-id="1bc84-105">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bc84-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1bc84-106">Instale a versão mais recente da CLI do Azure, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="1bc84-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="1bc84-107">Mais informações estão disponíveis em [Instalar a CLI do Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1bc84-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="1bc84-108">Entre na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="1bc84-108">Sign in to your Azure account</span></span>

<span data-ttu-id="1bc84-109">Abra uma janela do console e autentique com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="1bc84-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="1bc84-110">Para obter mais informações, confira [Conectar-se ao Azure a partir da CLI do Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="1bc84-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="1bc84-111">Mudar para o modo CLI</span><span class="sxs-lookup"><span data-stu-id="1bc84-111">Switch CLI mode</span></span>

<span data-ttu-id="1bc84-112">O DNS do Azure usa o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bc84-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="1bc84-113">Mude para o modo CLI para usar os comandos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bc84-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="1bc84-114">Selecionar a assinatura</span><span class="sxs-lookup"><span data-stu-id="1bc84-114">Select the subscription</span></span>

<span data-ttu-id="1bc84-115">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="1bc84-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="1bc84-116">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="1bc84-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="1bc84-117">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="1bc84-117">Create a resource group</span></span>

<span data-ttu-id="1bc84-118">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="1bc84-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1bc84-119">Ele é usado como o local padrão para os recursos do grupo de recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="1bc84-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="1bc84-120">No entanto, como todos os recursos de DNS são globais, não regionais, a escolha do local do grupo de recursos não afeta o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc84-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="1bc84-121">Você pode ignorar esta etapa se está usando um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="1bc84-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="1bc84-122">Registrar provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="1bc84-122">Register resource provider</span></span>

<span data-ttu-id="1bc84-123">O serviço de DNS do Azure é gerenciado pelo provedor de recursos Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="1bc84-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="1bc84-124">Para que você possa usar o DNS do Azure, sua assinatura do Azure deve ser registrada para usar esse provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="1bc84-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="1bc84-125">Essa operação deve ser executa apenas uma vez para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="1bc84-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

