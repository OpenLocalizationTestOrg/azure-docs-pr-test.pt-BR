


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="e06b6-101">Marcando uma máquina virtual por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="e06b6-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="e06b6-102">Primeiramente, vamos observar uma marcação por meio de modelos.</span><span class="sxs-lookup"><span data-stu-id="e06b6-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="e06b6-103">[Este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) insere marcas no hello recursos a seguir: (Máquina Virtual) de computação, armazenamento (conta de armazenamento) e rede (endereço IP público, rede Virtual e Interface de rede).</span><span class="sxs-lookup"><span data-stu-id="e06b6-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="e06b6-104">Esse modelo destina-se a uma VM do Windows, mas pode ser adaptada para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="e06b6-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="e06b6-105">Clique em Olá **implantar tooAzure** botão da saudação [link modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="e06b6-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="e06b6-106">Isso vai navegar toohello [portal do Azure](https://portal.azure.com/) onde você pode implantar este modelo.</span><span class="sxs-lookup"><span data-stu-id="e06b6-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Implantação simples com marcas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="e06b6-108">Esse modelo inclui Olá marcas a seguir: *departamento*, *aplicativo*, e *criado por*.</span><span class="sxs-lookup"><span data-stu-id="e06b6-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="e06b6-109">Você pode adicionar/editar essas marcas diretamente no modelo de saudação se você gostaria que os nomes de marca diferente.</span><span class="sxs-lookup"><span data-stu-id="e06b6-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Marcas do Azure em um modelo](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="e06b6-111">Como você pode ver, marcas de saudação são definidas como pares chave/valor, separados por dois-pontos (:).</span><span class="sxs-lookup"><span data-stu-id="e06b6-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="e06b6-112">marcas de saudação devem ser definidas neste formato:</span><span class="sxs-lookup"><span data-stu-id="e06b6-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="e06b6-113">Salve o arquivo de modelo de saudação depois de terminar de editá-lo com marcas de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e06b6-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="e06b6-114">Em seguida, no hello **Editar parâmetros** seção, você pode preencher os valores hello suas marcas.</span><span class="sxs-lookup"><span data-stu-id="e06b6-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Editar marcas no Portal do Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="e06b6-116">Clique em **criar** toodeploy este modelo com seus valores de marca.</span><span class="sxs-lookup"><span data-stu-id="e06b6-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="e06b6-117">Marcação de saudação Portal</span><span class="sxs-lookup"><span data-stu-id="e06b6-117">Tagging through hello Portal</span></span>
<span data-ttu-id="e06b6-118">Depois de criar os recursos com marcas, você pode exibir, adicionar e excluir marcas no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e06b6-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="e06b6-119">Selecione Olá marcas ícone tooview suas marcas:</span><span class="sxs-lookup"><span data-stu-id="e06b6-119">Select hello tags icon tooview your tags:</span></span>

![Ícone de marcas no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="e06b6-121">Adicionar uma nova marca por meio do portal Olá definindo seu próprio par chave/valor e salve-o.</span><span class="sxs-lookup"><span data-stu-id="e06b6-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Adicionar nova marca no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="e06b6-123">A nova marca agora deve aparecer na lista de saudação de marcas de recurso.</span><span class="sxs-lookup"><span data-stu-id="e06b6-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nova marca salva no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

