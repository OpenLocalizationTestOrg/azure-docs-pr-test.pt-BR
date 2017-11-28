## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="61d13-101">Implantações incrementais e completas</span><span class="sxs-lookup"><span data-stu-id="61d13-101">Incremental and complete deployments</span></span>
<span data-ttu-id="61d13-102">Ao implantar os recursos, especifique que a implantação é uma atualização incremental ou uma atualização completa.</span><span class="sxs-lookup"><span data-stu-id="61d13-102">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="61d13-103">A principal diferença entre esses dois modos é como o Resource Manager lida com os recursos existentes no grupo de recursos que não estão no modelo:</span><span class="sxs-lookup"><span data-stu-id="61d13-103">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that are not in the template:</span></span>

* <span data-ttu-id="61d13-104">No modo completo, o Resource Manager **exclui** os recursos existentes no grupo de recursos, mas que não foram especificados no modelo.</span><span class="sxs-lookup"><span data-stu-id="61d13-104">In complete mode, Resource Manager **deletes** resources that exist in the resource group but are not specified in the template.</span></span> 
* <span data-ttu-id="61d13-105">No modo incremental, o Resource Manager **deixa inalterados** os recursos existentes no grupo de recursos, mas que não foram especificados no modelo.</span><span class="sxs-lookup"><span data-stu-id="61d13-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but are not specified in the template.</span></span>

<span data-ttu-id="61d13-106">Para ambos os modos, o Resource Manager tenta provisionar todos os recursos especificados no modelo.</span><span class="sxs-lookup"><span data-stu-id="61d13-106">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="61d13-107">Se o recurso já existe no grupo de recursos e suas configurações são as mesmas, a operação resulta em nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="61d13-107">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="61d13-108">Se você alterar as configurações de um recurso, o recurso será provisionado com as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="61d13-108">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="61d13-109">Se você tentar atualizar o local ou o tipo de um recurso existente, a implantação falhará com um erro.</span><span class="sxs-lookup"><span data-stu-id="61d13-109">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="61d13-110">Em vez disso, implante um novo recurso com o local ou o tipo de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="61d13-110">Instead, deploy a new resource with the location or type that you need.</span></span>

<span data-ttu-id="61d13-111">Por padrão, o Resource Manager usa o modo incremental.</span><span class="sxs-lookup"><span data-stu-id="61d13-111">By default, Resource Manager uses the incremental mode.</span></span>

<span data-ttu-id="61d13-112">Para ilustrar a diferença entre os modos incrementais e completos, considere o cenário a seguir.</span><span class="sxs-lookup"><span data-stu-id="61d13-112">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="61d13-113">O **Grupo de recursos existente** contém:</span><span class="sxs-lookup"><span data-stu-id="61d13-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="61d13-114">Recurso A</span><span class="sxs-lookup"><span data-stu-id="61d13-114">Resource A</span></span>
* <span data-ttu-id="61d13-115">Recurso B</span><span class="sxs-lookup"><span data-stu-id="61d13-115">Resource B</span></span>
* <span data-ttu-id="61d13-116">Recurso C</span><span class="sxs-lookup"><span data-stu-id="61d13-116">Resource C</span></span>

<span data-ttu-id="61d13-117">O **Modelo** define:</span><span class="sxs-lookup"><span data-stu-id="61d13-117">**Template** defines:</span></span>

* <span data-ttu-id="61d13-118">Recurso A</span><span class="sxs-lookup"><span data-stu-id="61d13-118">Resource A</span></span>
* <span data-ttu-id="61d13-119">Recurso B</span><span class="sxs-lookup"><span data-stu-id="61d13-119">Resource B</span></span>
* <span data-ttu-id="61d13-120">Recurso D</span><span class="sxs-lookup"><span data-stu-id="61d13-120">Resource D</span></span>

<span data-ttu-id="61d13-121">Quando implantado no modo **incremental**, o grupo de recursos contém:</span><span class="sxs-lookup"><span data-stu-id="61d13-121">When deployed in **incremental** mode, the resource group contains:</span></span>

* <span data-ttu-id="61d13-122">Recurso A</span><span class="sxs-lookup"><span data-stu-id="61d13-122">Resource A</span></span>
* <span data-ttu-id="61d13-123">Recurso B</span><span class="sxs-lookup"><span data-stu-id="61d13-123">Resource B</span></span>
* <span data-ttu-id="61d13-124">Recurso C</span><span class="sxs-lookup"><span data-stu-id="61d13-124">Resource C</span></span>
* <span data-ttu-id="61d13-125">Recurso D</span><span class="sxs-lookup"><span data-stu-id="61d13-125">Resource D</span></span>

<span data-ttu-id="61d13-126">Quando implantado no modo **completo**, o Recurso C é excluído.</span><span class="sxs-lookup"><span data-stu-id="61d13-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="61d13-127">O grupo de recursos contém:</span><span class="sxs-lookup"><span data-stu-id="61d13-127">The resource group contains:</span></span>

* <span data-ttu-id="61d13-128">Recurso A</span><span class="sxs-lookup"><span data-stu-id="61d13-128">Resource A</span></span>
* <span data-ttu-id="61d13-129">Recurso B</span><span class="sxs-lookup"><span data-stu-id="61d13-129">Resource B</span></span>
* <span data-ttu-id="61d13-130">Recurso D</span><span class="sxs-lookup"><span data-stu-id="61d13-130">Resource D</span></span>
