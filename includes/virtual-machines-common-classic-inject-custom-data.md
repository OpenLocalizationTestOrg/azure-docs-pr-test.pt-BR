


<span data-ttu-id="0e4e4-101">Este tópico descreve como:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-101">This topic describes how to:</span></span>

* <span data-ttu-id="0e4e4-102">Injetar dados em uma VM (máquina virtual) do Azure quando está sendo provisionada.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="0e4e4-103">Recuperá-los para Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="0e4e4-104">Use ferramentas especiais disponíveis em alguns sistemas toodetect e manipular dados personalizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="0e4e4-105">Este artigo descreve os dados como personalizada pode ser inserida por meio de uma máquina virtual criada com hello API de gerenciamento de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="0e4e4-106">toosee como toouse Olá API de gerenciamento de recursos do Azure, consulte [modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="0e4e4-107">Injetando dados personalizados na máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0e4e4-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="0e4e4-108">Esse recurso é suportado apenas em Olá [Interface de linha de comando do Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="0e4e4-109">Aqui criamos uma `custom-data.txt` arquivo que contém os dados, e então insira que em toohello VM durante o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="0e4e4-110">Embora você possa usar qualquer uma das opções de saudação para Olá `azure vm create` comando seguinte Olá demonstra uma abordagem muito básica:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="0e4e4-111">Usando dados personalizados na máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="0e4e4-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="0e4e4-112">Se sua VM do Azure é uma VM com base em Windows, o arquivo de dados personalizados de saudação é salvo muito`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="0e4e4-113">Embora fosse tootransfer codificada em base64 de saudação computador local toohello nova VM, ela será automaticamente decodificado e pode ser aberta ou usada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0e4e4-114">Se o arquivo hello existir, ele será substituído.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="0e4e4-115">segurança de saudação no diretório de saudação está definida muito**System: Full Control** e **Administrators: Full Control**.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="0e4e4-116">Se sua VM do Azure é uma VM com base em Linux, em seguida, o arquivo de dados personalizados Olá estará localizado em um dos seguintes Olá coloca dependendo de sua distribuição.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="0e4e4-117">dados saudação podem ser codificada em base64, portanto, dados de saudação toodecode talvez seja necessário primeiro:</span><span class="sxs-lookup"><span data-stu-id="0e4e4-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="0e4e4-118">Cloud-init no Azure</span><span class="sxs-lookup"><span data-stu-id="0e4e4-118">Cloud-init on Azure</span></span>
<span data-ttu-id="0e4e4-119">Se sua VM do Azure for de uma imagem Ubuntu ou CoreOS, você pode usar CustomData toosend toocloud-init uma configuração de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="0e4e4-120">Ou, se o arquivo de dados personalizado for um script, cloud-init poderá simplesmente executá-lo.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="0e4e4-121">Imagens de nuvem do Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0e4e4-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="0e4e4-122">Na maioria das imagens do Linux do Azure, você edita "/ etc/waagent.conf" arquivo de disco e a troca de recursos temporário de saudação do tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="0e4e4-123">Consulte o [Guia de usuário agente do Linux do Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="0e4e4-124">No entanto, nas imagens de nuvem do Ubuntu hello, você deve usar init nuvem tooconfigure Olá recursos disco (ou seja, Olá "efêmera") e troca de partição.</span><span class="sxs-lookup"><span data-stu-id="0e4e4-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="0e4e4-125">Consulte Olá página a seguir no wiki do Ubuntu Olá para obter mais detalhes: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="0e4e4-126">Próximas etapas: usando cloud-init</span><span class="sxs-lookup"><span data-stu-id="0e4e4-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="0e4e4-127">Para obter mais informações, consulte Olá [documentação nuvem init para Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="0e4e4-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="0e4e4-128">Referência da API REST de gerenciamento para adicionar serviço de função</span><span class="sxs-lookup"><span data-stu-id="0e4e4-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="0e4e4-129">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="0e4e4-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

