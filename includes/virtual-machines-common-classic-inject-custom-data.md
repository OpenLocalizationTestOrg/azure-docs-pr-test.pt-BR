


<span data-ttu-id="eb884-101">Este tópico descreve como:</span><span class="sxs-lookup"><span data-stu-id="eb884-101">This topic describes how to:</span></span>

* <span data-ttu-id="eb884-102">Injetar dados em uma VM (máquina virtual) do Azure quando está sendo provisionada.</span><span class="sxs-lookup"><span data-stu-id="eb884-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="eb884-103">Recuperá-los para Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="eb884-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="eb884-104">Usar ferramentas especiais em alguns sistemas para detectar e identificar dados personalizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="eb884-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="eb884-105">Este artigo descreve como injetar dados personalizados usando uma VM criada com a API do Gerenciamento de Serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb884-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="eb884-106">Para aprender a usar a API do Gerenciamento de Recursos do Azure, consulte [o modelo de exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="eb884-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="eb884-107">Injetando dados personalizados na máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="eb884-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="eb884-108">No momento, esse recurso tem suporte apenas na [Interface de Linha de Comando do Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="eb884-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="eb884-109">Vamos criar um arquivo `custom-data.txt` que contém os dados para então inseri-los na VM durante o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="eb884-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="eb884-110">Embora você possa usar qualquer uma das opções para o comando `azure vm create` , a abordagem demonstrada é muito básica:</span><span class="sxs-lookup"><span data-stu-id="eb884-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="eb884-111">Usando dados personalizados na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="eb884-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="eb884-112">Se sua VM do Azure for do Windows, o arquivo de dados personalizado estará salvo em `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="eb884-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="eb884-113">Embora tenha sido codificado com base64 para transferência do computador local para a nova VM, ele é decodificado automaticamente e pode ser aberto imediatamente.</span><span class="sxs-lookup"><span data-stu-id="eb884-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="eb884-114">Se já existir, o arquivo será substituído.</span><span class="sxs-lookup"><span data-stu-id="eb884-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="eb884-115">A segurança no diretório é definida como **Sistema:Controle Total** e **Administratores:Controle Total**.</span><span class="sxs-lookup"><span data-stu-id="eb884-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="eb884-116">Se sua VM do Azure for uma VM do Linux, o arquivo de dados personalizado se encontrará em um dos dois locais a seguir dependendo da sua distribuição.</span><span class="sxs-lookup"><span data-stu-id="eb884-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="eb884-117">Os dados serão codificados com base64, portanto, você precisará decodificar os dados primeiro:</span><span class="sxs-lookup"><span data-stu-id="eb884-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="eb884-118">Cloud-init no Azure</span><span class="sxs-lookup"><span data-stu-id="eb884-118">Cloud-init on Azure</span></span>
<span data-ttu-id="eb884-119">Se a sua VM do Azure for de uma imagem do Ubuntu ou CoreOS, você poderá usar o CustomData para enviar um cloud-config para cloud-init.</span><span class="sxs-lookup"><span data-stu-id="eb884-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="eb884-120">Ou, se o arquivo de dados personalizado for um script, cloud-init poderá simplesmente executá-lo.</span><span class="sxs-lookup"><span data-stu-id="eb884-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="eb884-121">Imagens de nuvem do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="eb884-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="eb884-122">Na maioria das imagens do Linux do Azure você editaria "/etc/waagent.conf" para configurar o disco de recurso temporário e o arquivo de troca.</span><span class="sxs-lookup"><span data-stu-id="eb884-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="eb884-123">Consulte o [Guia de usuário agente do Linux do Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="eb884-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="eb884-124">No entanto, nas Imagens de Nuvem do Ubuntu, devemos usar cloud-init para configurar o disco de recurso (ou seja, o disco "efêmero") e a partição de troca.</span><span class="sxs-lookup"><span data-stu-id="eb884-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="eb884-125">Consulte a seguinte página no wiki do Ubuntu para obter mais detalhes: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="eb884-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="eb884-126">Próximas etapas: usando cloud-init</span><span class="sxs-lookup"><span data-stu-id="eb884-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="eb884-127">Para obter mais informações, consulte [Documentação de cloud-init para Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="eb884-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="eb884-128">Referência da API REST de gerenciamento para adicionar serviço de função</span><span class="sxs-lookup"><span data-stu-id="eb884-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="eb884-129">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="eb884-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

