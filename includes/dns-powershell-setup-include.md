## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="f2b5b-101">Configurar o Azure PowerShell para DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="f2b5b-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="f2b5b-102">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f2b5b-102">Before you begin</span></span>

<span data-ttu-id="f2b5b-103">Verifique se você tem Olá itens a seguir antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="f2b5b-104">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-104">An Azure subscription.</span></span> <span data-ttu-id="f2b5b-105">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2b5b-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f2b5b-106">Você precisa tooinstall hello mais recente versão do hello cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f2b5b-107">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f2b5b-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="f2b5b-108">Entrar tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="f2b5b-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="f2b5b-109">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="f2b5b-110">Para obter mais informações, confira [Usar o PowerShell com o Gerenciador de Recursos](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f2b5b-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="f2b5b-111">Selecione a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="f2b5b-111">Select hello subscription</span></span>
 
<span data-ttu-id="f2b5b-112">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f2b5b-113">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f2b5b-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f2b5b-114">Create a resource group</span></span>

<span data-ttu-id="f2b5b-115">O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f2b5b-116">Esse local é usado como o local padrão de saudação para recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="f2b5b-117">No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="f2b5b-118">Você pode ignorar esta etapa se está usando um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="f2b5b-119">Registrar provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="f2b5b-119">Register resource provider</span></span>

<span data-ttu-id="f2b5b-120">Olá serviço DNS do Azure é gerenciado pelo provedor de recursos Microsoft. Network hello.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="f2b5b-121">Sua assinatura do Azure deve ser registrado toouse este provedor de recursos antes de usar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="f2b5b-122">Essa operação deve ser executa apenas uma vez para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="f2b5b-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```