<span data-ttu-id="39dc7-101">O suporte a dois recursos de depuração agora está disponível no Azure: Saída do Console e a Captura de Tela para o modelo de implantação do Resource Manager de Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="39dc7-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="39dc7-102">Ao colocar tooAzure sua própria imagem ou até mesmo inicialização uma das imagens da plataforma Olá, pode haver várias razões por que uma máquina Virtual entra em um estado não inicializável.</span><span class="sxs-lookup"><span data-stu-id="39dc7-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="39dc7-103">Habilitar esses recursos você tooeasily diagnosticar e recuperar suas máquinas virtuais de falhas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="39dc7-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="39dc7-104">Para máquinas de virtuais de Linux, você pode facilmente exibir saída de hello de seu log de console da saudação Portal:</span><span class="sxs-lookup"><span data-stu-id="39dc7-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portal do Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="39dc7-106">No entanto, para o Windows e máquinas virtuais do Linux Azure também permite que toosee uma captura de tela de Olá VM do hipervisor hello:</span><span class="sxs-lookup"><span data-stu-id="39dc7-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Erro](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="39dc7-108">Esses dois recursos têm suporte em máquinas virtuais do Azure em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="39dc7-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="39dc7-109">Observe, capturas de tela e saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="39dc7-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="39dc7-110">Erros comuns de inicialização</span><span class="sxs-lookup"><span data-stu-id="39dc7-110">Common boot errors</span></span>

- [<span data-ttu-id="39dc7-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="39dc7-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="39dc7-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="39dc7-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="39dc7-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="39dc7-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="39dc7-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="39dc7-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="39dc7-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="39dc7-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="39dc7-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="39dc7-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="39dc7-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="39dc7-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="39dc7-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="39dc7-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="39dc7-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="39dc7-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="39dc7-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="39dc7-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="39dc7-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="39dc7-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="39dc7-122">Não foi possível encontrar um sistema operacional</span><span class="sxs-lookup"><span data-stu-id="39dc7-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="39dc7-123">Falha de inicialização ou INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="39dc7-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="39dc7-124">Habilitar o diagnóstico em uma nova máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39dc7-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="39dc7-125">Ao criar uma nova máquina Virtual do Portal de visualização de saudação, selecione Olá **do Azure Resource Manager** na lista suspensa de modelo de implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="39dc7-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gerenciador de Recursos](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="39dc7-127">Configure Olá conta de armazenamento de saudação do monitoramento opção tooselect em que você deseja tooplace esses arquivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="39dc7-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Criar VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="39dc7-129">Se você estiver implantando um modelo do Azure Resource Manager, navegue tooyour recurso de máquina Virtual e acrescentar a seção de perfil de diagnóstico hello.</span><span class="sxs-lookup"><span data-stu-id="39dc7-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="39dc7-130">Lembre-se o cabeçalho de versão de API do toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="39dc7-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="39dc7-131">perfil de diagnóstico Olá permite tooselect conta de armazenamento de saudação onde você deseja tooput esses logs.</span><span class="sxs-lookup"><span data-stu-id="39dc7-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="39dc7-132">toodeploy um exemplo de máquina Virtual com o diagnóstico de inicialização habilitado, Confira nosso repositório aqui.</span><span class="sxs-lookup"><span data-stu-id="39dc7-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="39dc7-133">Atualizar uma máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="39dc7-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="39dc7-134">Diagnóstico de inicialização tooenable por meio de saudação Portal, você também pode atualizar uma máquina Virtual existente por meio do Portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="39dc7-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="39dc7-135">Selecione Olá opção de diagnóstico de inicialização e salvar.</span><span class="sxs-lookup"><span data-stu-id="39dc7-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="39dc7-136">Reinicie o efeito de tootake VM hello.</span><span class="sxs-lookup"><span data-stu-id="39dc7-136">Restart hello VM tootake effect.</span></span>

![Atualizar VM existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

