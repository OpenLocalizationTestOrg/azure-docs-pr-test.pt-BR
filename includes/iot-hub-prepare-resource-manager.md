## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="347bc-101">Preparar tooauthenticate solicitações do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="347bc-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="347bc-102">Você deve autenticar todas as operações de saudação que podem ser executadas em recursos usando Olá [do Azure Resource Manager] [ lnk-authenticate-arm] com o Azure AD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="347bc-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="347bc-103">Olá tooconfigure de maneira mais fácil é toouse PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="347bc-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="347bc-104">Instalar Olá [cmdlets do PowerShell do Azure] [ lnk-powershell-install] antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="347bc-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="347bc-105">Olá mostram as etapas a seguir como tooset a autenticação de senha para um aplicativo do AD usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="347bc-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="347bc-106">Você pode executar esses comandos em uma sessão do PowerShell padrão.</span><span class="sxs-lookup"><span data-stu-id="347bc-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="347bc-107">Faça logon no tooyour assinatura do Azure usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="347bc-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="347bc-108">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="347bc-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="347bc-109">Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="347bc-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="347bc-110">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toomanage seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="347bc-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="347bc-111">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="347bc-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="347bc-112">Anote seu **TenantId** e **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="347bc-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="347bc-113">Você precisará dessa informação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="347bc-113">You need them later.</span></span>
3. <span data-ttu-id="347bc-114">Crie um novo aplicativo do Active Directory do Azure usando Olá comando a seguir, substituindo espaços reservados de saudação:</span><span class="sxs-lookup"><span data-stu-id="347bc-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="347bc-115">**{Display name}:** um nome de exibição para seu aplicativo, como **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="347bc-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="347bc-116">**{URL da Home page}:** Olá URL da página inicial de saudação do seu aplicativo, como **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="347bc-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="347bc-117">Essa URL não precisa de aplicativo real do toopoint tooa.</span><span class="sxs-lookup"><span data-stu-id="347bc-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="347bc-118">**{Application identifier}:** um identificador exclusivo, como **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="347bc-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="347bc-119">Essa URL não precisa de aplicativo real do toopoint tooa.</span><span class="sxs-lookup"><span data-stu-id="347bc-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="347bc-120">**{Password}:** uma senha que você use tooauthenticate com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="347bc-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="347bc-121">Anote Olá **ApplicationId** do aplicativo hello criado por você.</span><span class="sxs-lookup"><span data-stu-id="347bc-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="347bc-122">Você precisa dessa informação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="347bc-122">You need this later.</span></span>
5. <span data-ttu-id="347bc-123">Criar uma nova entidade de serviço usando Olá comando a seguir, substituindo **{MyApplicationId}** com hello **ApplicationId** da etapa anterior hello:</span><span class="sxs-lookup"><span data-stu-id="347bc-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="347bc-124">Configurar uma atribuição de função usando Olá comando a seguir, substituindo **{MyApplicationId}** com seus **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="347bc-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="347bc-125">Agora terminar de criar o aplicativo do AD do Azure hello que permite que você tooauthenticate do seu aplicativo c# personalizado.</span><span class="sxs-lookup"><span data-stu-id="347bc-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="347bc-126">Você precisa Olá seguinte valores posteriormente neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="347bc-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="347bc-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="347bc-127">TenantId</span></span>
* <span data-ttu-id="347bc-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="347bc-128">SubscriptionId</span></span>
* <span data-ttu-id="347bc-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="347bc-129">ApplicationId</span></span>
* <span data-ttu-id="347bc-130">Senha</span><span class="sxs-lookup"><span data-stu-id="347bc-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
