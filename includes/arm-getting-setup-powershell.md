## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="05a24-101">Configurando o PowerShell para modelos do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="05a24-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="05a24-102">Antes de você pode usar o PowerShell do Azure com o Gerenciador de recursos, você precisará toohave saudação do Windows PowerShell e o Azure PowerShell versões corretas.</span><span class="sxs-lookup"><span data-stu-id="05a24-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="05a24-103">Verificar as versões do PowerShell</span><span class="sxs-lookup"><span data-stu-id="05a24-103">Verify PowerShell versions</span></span>
<span data-ttu-id="05a24-104">Verifique se você tem o Windows PowerShell versão 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="05a24-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="05a24-105">versão de hello toofind do Windows PowerShell, digite este comando no prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05a24-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="05a24-106">Olá, tipo de informações a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="05a24-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="05a24-107">Verifique se o valor de saudação **PSVersion** é 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="05a24-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="05a24-108">Caso não seja, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="05a24-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="05a24-109">Definir sua conta e assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="05a24-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="05a24-110">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05a24-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="05a24-111">Abra um prompt de comando do PowerShell do Azure e faça logon tooAzure com este comando.</span><span class="sxs-lookup"><span data-stu-id="05a24-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="05a24-112">Se você tiver várias assinaturas do Azure, você pode listar suas assinaturas do Azure com este comando.</span><span class="sxs-lookup"><span data-stu-id="05a24-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="05a24-113">Olá, tipo de informações a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="05a24-113">You will receive hello following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="05a24-114">Você pode definir a assinatura do Azure Olá executando esses comandos no prompt de comando do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="05a24-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="05a24-115">Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com o nome correto da saudação.</span><span class="sxs-lookup"><span data-stu-id="05a24-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="05a24-116">Para obter mais informações sobre contas e assinaturas do Azure, consulte [como: conectar-se a assinatura de tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="05a24-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

