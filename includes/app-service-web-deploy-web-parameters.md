<span data-ttu-id="d9970-101">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="d9970-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="d9970-102">modelo de saudação inclui uma seção chamada parâmetros que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="d9970-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="d9970-103">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="d9970-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="d9970-104">Não defina parâmetros para valores sempre ficará Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="d9970-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="d9970-105">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="d9970-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="d9970-106">Ao definir parâmetros, use Olá **allowedValues** toospecify campo quais valores um usuário pode fornecer durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="d9970-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="d9970-107">Saudação de uso **defaultValue** tooassign campo um parâmetro de toohello valor, se nenhum valor for fornecido durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="d9970-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="d9970-108">Descreveremos cada parâmetro no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9970-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="d9970-109">siteName</span><span class="sxs-lookup"><span data-stu-id="d9970-109">siteName</span></span>
<span data-ttu-id="d9970-110">nome de saudação do aplicativo web de saudação que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="d9970-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="d9970-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="d9970-111">hostingPlanName</span></span>
<span data-ttu-id="d9970-112">nome de saudação de saudação do serviço de aplicativo planejar toouse para hospedar o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9970-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="d9970-113">sku</span><span class="sxs-lookup"><span data-stu-id="d9970-113">sku</span></span>
<span data-ttu-id="d9970-114">Olá preço Olá plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="d9970-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="d9970-115">Olá modelo define os valores de saudação que são permitidos para esse parâmetro e atribui um valor padrão (S1) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="d9970-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="d9970-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="d9970-116">workerSize</span></span>
<span data-ttu-id="d9970-117">tamanho da instância de saudação da saudação (pequeno, médio ou grande) de plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="d9970-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="d9970-118">Olá modelo define os valores de saudação que são permitidos para este parâmetro (0, 1 ou 2) e atribui um valor padrão (0) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="d9970-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="d9970-119">os valores Hello correspondem toosmall, médio e grande.</span><span class="sxs-lookup"><span data-stu-id="d9970-119">hello values correspond toosmall, medium and large.</span></span>

