<span data-ttu-id="3f4f3-101">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-101">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="3f4f3-102">O modelo inclui uma seção chamada Parâmetros, que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-102">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="3f4f3-103">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-103">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="3f4f3-104">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-104">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="3f4f3-105">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-105">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

<span data-ttu-id="3f4f3-106">Ao definir parâmetros, use o campo **allowedValues** para especificar quais valores um usuário pode fornecer durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-106">When defining parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span></span> <span data-ttu-id="3f4f3-107">Use o campo **defaultValue** para atribuir um valor para o parâmetro, se nenhum valor for fornecido durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-107">Use the **defaultValue** field to assign a value to the parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="3f4f3-108">Descreveremos cada parâmetro no modelo.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-108">We will describe each parameter in the template.</span></span>

### <a name="sitename"></a><span data-ttu-id="3f4f3-109">siteName</span><span class="sxs-lookup"><span data-stu-id="3f4f3-109">siteName</span></span>
<span data-ttu-id="3f4f3-110">O nome do aplicativo Web que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-110">The name of the web app that you wish to create.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="3f4f3-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="3f4f3-111">hostingPlanName</span></span>
<span data-ttu-id="3f4f3-112">O nome do plano do Serviço de Aplicativo a usar para hospedar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-112">The name of the App Service plan to use for hosting the web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="3f4f3-113">sku</span><span class="sxs-lookup"><span data-stu-id="3f4f3-113">sku</span></span>
<span data-ttu-id="3f4f3-114">A camada de preços do plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-114">The pricing tier for the hosting plan.</span></span>

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
        "description": "The pricing tier for the hosting plan."
      }
    }

<span data-ttu-id="3f4f3-115">O modelo define os valores permitidos para esse parâmetro e atribui um valor padrão (S1) se nenhum valor é especificado.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-115">The template defines the values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="3f4f3-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="3f4f3-116">workerSize</span></span>
<span data-ttu-id="3f4f3-117">O tamanho da instância do plano de hospedagem (pequeno, médio ou grande).</span><span class="sxs-lookup"><span data-stu-id="3f4f3-117">The instance size of the hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="3f4f3-118">O modelo define os valores que são permitidos para esse parâmetro (0, 1 ou 2) e atribui um valor padrão (0) se nenhum valor é especificado.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-118">The template defines the values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="3f4f3-119">Os valores correspondem a pequeno, médio e grande.</span><span class="sxs-lookup"><span data-stu-id="3f4f3-119">The values correspond to small, medium and large.</span></span>

