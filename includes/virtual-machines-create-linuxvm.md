
1. <span data-ttu-id="5a694-101">Entrar tooyour assinatura do Azure usando Olá etapas listadas na [conectar tooAzure do hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5a694-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="5a694-102">Verifique se que você está no modo de implantação clássico Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a694-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="5a694-103">Descubra imagem do Linux Olá que você deseja tooload de imagens disponíveis Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a694-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="5a694-104">Em uma janela de prompt de comando do Windows, use **find** em vez de grep.</span><span class="sxs-lookup"><span data-stu-id="5a694-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="5a694-105">Use `azure vm create` toocreate uma VM com a imagem do Linux Olá na lista anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a694-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="5a694-106">Esta etapa cria uma conta de armazenamento e um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5a694-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="5a694-107">Você também pode se conectar a esse serviço de nuvem existente do VM tooan com um `-c` opção.</span><span class="sxs-lookup"><span data-stu-id="5a694-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="5a694-108">Criar um toolog de ponto de extremidade SSH na máquina de virtual do Linux toohello com hello `-e` opção.</span><span class="sxs-lookup"><span data-stu-id="5a694-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="5a694-109">Olá, exemplo a seguir cria uma VM denominada `myVM` usando Olá `Ubuntu-14_04_4-LTS` imagem no hello `West US` local e adiciona um nome de usuário `ops`:</span><span class="sxs-lookup"><span data-stu-id="5a694-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="5a694-110">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a694-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="5a694-111">Para uma máquina virtual Linux, você deve fornecer Olá `-e` opção `vm create`.</span><span class="sxs-lookup"><span data-stu-id="5a694-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="5a694-112">Não é possível tooenable SSH depois de máquina virtual de saudação foi criada.</span><span class="sxs-lookup"><span data-stu-id="5a694-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="5a694-113">Para obter mais detalhes sobre SSH, leia [como tooUse SSH com Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a694-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="5a694-114">Você pode verificar os atributos de saudação do hello VM usando Olá `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="5a694-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="5a694-115">Olá exemplo a seguir lista as informações para Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5a694-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="5a694-116">Iniciar a VM com hello `azure vm start` comando da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a694-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="5a694-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a694-117">Next steps</span></span>
<span data-ttu-id="5a694-118">Para obter detalhes sobre todos esses comandos de máquina virtual do Azure CLI 1.0, leia Olá [usando Olá 1.0 da CLI do Azure com a API de implantação clássico Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5a694-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

