## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="95dd4-101">Preparar para autenticar solicitações do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95dd4-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="95dd4-102">Autentique todas as operações que podem ser executadas nos recursos usando o [Azure Resource Manager][lnk-authenticate-arm] com o Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="95dd4-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="95dd4-103">A maneira mais fácil de configurar isso é usar o PowerShell ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="95dd4-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="95dd4-104">Instale os [cmdlets do Azure PowerShell][lnk-powershell-install] antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="95dd4-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="95dd4-105">As etapas a seguir mostram como configurar a autenticação de senha para um aplicativo do AD usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95dd4-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="95dd4-106">Você pode executar esses comandos em uma sessão do PowerShell padrão.</span><span class="sxs-lookup"><span data-stu-id="95dd4-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="95dd4-107">Faça logon em sua assinatura do Azure usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="95dd4-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="95dd4-108">Caso tenha várias assinaturas do Azure, entrar no Azure concede a você acesso a todas as assinaturas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="95dd4-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="95dd4-109">Use o comando a seguir para listar as assinaturas do Azure disponíveis para você:</span><span class="sxs-lookup"><span data-stu-id="95dd4-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="95dd4-110">Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="95dd4-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="95dd4-111">Você pode usar a ID ou nome da assinatura da saída do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="95dd4-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="95dd4-112">Anote seu **TenantId** e **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="95dd4-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="95dd4-113">Você precisará dessa informação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="95dd4-113">You need them later.</span></span>
3. <span data-ttu-id="95dd4-114">Crie um novo aplicativo do Active Directory do Azure usando o seguinte comando, substituindo os espaços reservados:</span><span class="sxs-lookup"><span data-stu-id="95dd4-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="95dd4-115">**{Display name}:** um nome de exibição para seu aplicativo, como **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="95dd4-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="95dd4-116">**{Home page URL}:** a URL da página inicial de seu aplicativo, como **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="95dd4-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="95dd4-117">Essa URL não precisa levar para um aplicativo real.</span><span class="sxs-lookup"><span data-stu-id="95dd4-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="95dd4-118">**{Application identifier}:** um identificador exclusivo, como **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="95dd4-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="95dd4-119">Essa URL não precisa levar para um aplicativo real.</span><span class="sxs-lookup"><span data-stu-id="95dd4-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="95dd4-120">**{Password}:** Uma senha que você usa para autenticar com o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95dd4-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="95dd4-121">Anote o **ApplicationId** do aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="95dd4-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="95dd4-122">Você precisa dessa informação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="95dd4-122">You need this later.</span></span>
5. <span data-ttu-id="95dd4-123">Criar uma nova entidade de serviço usando o comando a seguir, substituindo **{MyApplicationId}** pelo **ApplicationId** da etapa anterior:</span><span class="sxs-lookup"><span data-stu-id="95dd4-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="95dd4-124">Configure uma atribuição de função usando o comando a seguir, substituindo **{MyApplicationId}** por **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="95dd4-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="95dd4-125">Você terminou de criar o aplicativo do Azure AD que permitirá autenticar a partir do seu aplicativo C# personalizado.</span><span class="sxs-lookup"><span data-stu-id="95dd4-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="95dd4-126">Você precisa dos seguintes valores mais à frente neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="95dd4-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="95dd4-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="95dd4-127">TenantId</span></span>
* <span data-ttu-id="95dd4-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="95dd4-128">SubscriptionId</span></span>
* <span data-ttu-id="95dd4-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="95dd4-129">ApplicationId</span></span>
* <span data-ttu-id="95dd4-130">Senha</span><span class="sxs-lookup"><span data-stu-id="95dd4-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
