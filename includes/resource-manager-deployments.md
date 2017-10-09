## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="1c339-101">Implantações incrementais e completas</span><span class="sxs-lookup"><span data-stu-id="1c339-101">Incremental and complete deployments</span></span>
<span data-ttu-id="1c339-102">Ao implantar seus recursos, você especificar que a implantação de saudação é uma atualização incremental ou uma atualização completa.</span><span class="sxs-lookup"><span data-stu-id="1c339-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="1c339-103">Olá principal diferença entre esses dois modos é como o Gerenciador de recursos lida com recursos existentes no grupo de recursos de saudação que não estão no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c339-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="1c339-104">No modo completo, o Gerenciador de recursos **exclui** recursos que existem no grupo de recursos hello, mas não estão especificados no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c339-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="1c339-105">No modo incremental, o Gerenciador de recursos de **deixa inalteradas** recursos que existem no grupo de recursos hello, mas não estão especificados no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c339-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="1c339-106">Para ambos os modos, o Gerenciador de recursos de tentativas tooprovision todos os recursos especificados no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c339-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="1c339-107">Se o recurso Olá já existe no grupo de recursos de saudação e suas configurações foram modificadas, a operação de saudação resulta em nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="1c339-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="1c339-108">Se você alterar as configurações de saudação para um recurso, o recurso de saudação é provisionado com as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="1c339-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="1c339-109">Se você tentar local de saudação tooupdate ou o tipo de um recurso existente, a implantação de saudação falhará com um erro.</span><span class="sxs-lookup"><span data-stu-id="1c339-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="1c339-110">Em vez disso, implante um novo recurso com o local de saudação ou digite o que você precisa.</span><span class="sxs-lookup"><span data-stu-id="1c339-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="1c339-111">Por padrão, o Gerenciador de recursos usa modo incremental hello.</span><span class="sxs-lookup"><span data-stu-id="1c339-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="1c339-112">diferença de saudação tooillustrate entre os modos de incrementais e completos, considere Olá cenário a seguir.</span><span class="sxs-lookup"><span data-stu-id="1c339-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="1c339-113">O **Grupo de recursos existente** contém:</span><span class="sxs-lookup"><span data-stu-id="1c339-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="1c339-114">Recurso A</span><span class="sxs-lookup"><span data-stu-id="1c339-114">Resource A</span></span>
* <span data-ttu-id="1c339-115">Recurso B</span><span class="sxs-lookup"><span data-stu-id="1c339-115">Resource B</span></span>
* <span data-ttu-id="1c339-116">Recurso C</span><span class="sxs-lookup"><span data-stu-id="1c339-116">Resource C</span></span>

<span data-ttu-id="1c339-117">O **Modelo** define:</span><span class="sxs-lookup"><span data-stu-id="1c339-117">**Template** defines:</span></span>

* <span data-ttu-id="1c339-118">Recurso A</span><span class="sxs-lookup"><span data-stu-id="1c339-118">Resource A</span></span>
* <span data-ttu-id="1c339-119">Recurso B</span><span class="sxs-lookup"><span data-stu-id="1c339-119">Resource B</span></span>
* <span data-ttu-id="1c339-120">Recurso D</span><span class="sxs-lookup"><span data-stu-id="1c339-120">Resource D</span></span>

<span data-ttu-id="1c339-121">Quando implantado em **incremental** modo, o grupo de recursos Olá contém:</span><span class="sxs-lookup"><span data-stu-id="1c339-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="1c339-122">Recurso A</span><span class="sxs-lookup"><span data-stu-id="1c339-122">Resource A</span></span>
* <span data-ttu-id="1c339-123">Recurso B</span><span class="sxs-lookup"><span data-stu-id="1c339-123">Resource B</span></span>
* <span data-ttu-id="1c339-124">Recurso C</span><span class="sxs-lookup"><span data-stu-id="1c339-124">Resource C</span></span>
* <span data-ttu-id="1c339-125">Recurso D</span><span class="sxs-lookup"><span data-stu-id="1c339-125">Resource D</span></span>

<span data-ttu-id="1c339-126">Quando implantado no modo **completo**, o Recurso C é excluído.</span><span class="sxs-lookup"><span data-stu-id="1c339-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="1c339-127">grupo de recursos de saudação contém:</span><span class="sxs-lookup"><span data-stu-id="1c339-127">hello resource group contains:</span></span>

* <span data-ttu-id="1c339-128">Recurso A</span><span class="sxs-lookup"><span data-stu-id="1c339-128">Resource A</span></span>
* <span data-ttu-id="1c339-129">Recurso B</span><span class="sxs-lookup"><span data-stu-id="1c339-129">Resource B</span></span>
* <span data-ttu-id="1c339-130">Recurso D</span><span class="sxs-lookup"><span data-stu-id="1c339-130">Resource D</span></span>
