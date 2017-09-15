


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="8cc8b-101">Marcando uma máquina virtual por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="8cc8b-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="8cc8b-102">Primeiramente, vamos observar uma marcação por meio de modelos.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="8cc8b-103">[Este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) coloca marcas nos seguintes recursos: Computação (Máquina Virtual), Armazenamento (Conta de Armazenamento) e Rede (Endereço IP Público, Rede Virtual e Interface de Rede).</span><span class="sxs-lookup"><span data-stu-id="8cc8b-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="8cc8b-104">Esse modelo destina-se a uma VM do Windows, mas pode ser adaptada para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="8cc8b-105">Clique no botão **Implantar no Azure** no [link do modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="8cc8b-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="8cc8b-106">Você será direcionado para o [Portal do Azure](https://portal.azure.com/) , onde poderá implantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Implantação simples com marcas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="8cc8b-108">Esse modelo inclui as seguintes marcas: *Departamento*, *Aplicativo* e *Criado por*.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="8cc8b-109">Você pode adicionar/editar essas marcas diretamente no modelo se desejar diferentes nomes de marca.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Marcas do Azure em um modelo](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="8cc8b-111">Como pode ser visto, as marcas são pares de chave/valor definidos, separados por dois-pontos (:).</span><span class="sxs-lookup"><span data-stu-id="8cc8b-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="8cc8b-112">As marcas devem ser definidas neste formato:</span><span class="sxs-lookup"><span data-stu-id="8cc8b-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="8cc8b-113">Salve o arquivo de modelo quando terminar de editá-lo com as marcas de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="8cc8b-114">Em seguida, na seção **Editar Parâmetros** , você pode preencher os valores de suas marcas.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Editar marcas no Portal do Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="8cc8b-116">Clique em **Criar** para implantar esse modelo com seus valores de marca.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="8cc8b-117">Marcando por meio do portal</span><span class="sxs-lookup"><span data-stu-id="8cc8b-117">Tagging through the Portal</span></span>
<span data-ttu-id="8cc8b-118">Depois de criar seus recursos com marcas, você pode exibir, adicionar e excluir as marcas no portal.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="8cc8b-119">Selecione o ícone de marcas para exibir suas marcas:</span><span class="sxs-lookup"><span data-stu-id="8cc8b-119">Select the tags icon to view your tags:</span></span>

![Ícone de marcas no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="8cc8b-121">Adicione uma nova marca por meio do portal definindo seu próprio par de chave/valor e salve-a.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Adicionar nova marca no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="8cc8b-123">Agora, a nova marca deve aparecer na lista de marcas do seu recurso.</span><span class="sxs-lookup"><span data-stu-id="8cc8b-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Nova marca salva no Portal do Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

