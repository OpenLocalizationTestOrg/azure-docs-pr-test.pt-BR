<span data-ttu-id="63c31-101">Quando você não precisa mais um disco de dados é anexado tooa VM, você pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="63c31-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="63c31-102">Desanexar um disco remove o disco de saudação da máquina virtual de hello, mas não exclui o disco de saudação da saudação conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="63c31-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="63c31-103">Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma máquina virtual ou outro.</span><span class="sxs-lookup"><span data-stu-id="63c31-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="63c31-104">toodetach um disco do sistema operacional, é necessário primeiro toodelete Olá VM.</span><span class="sxs-lookup"><span data-stu-id="63c31-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="63c31-105">Localizar o disco Olá</span><span class="sxs-lookup"><span data-stu-id="63c31-105">Find hello disk</span></span>
<span data-ttu-id="63c31-106">Se você não souber o nome de saudação do hello disco ou deseja tooverify-lo antes de desconectá-lo, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="63c31-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="63c31-107">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63c31-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="63c31-108">Clique em **máquinas virtuais**, e, em seguida, selecione Olá VM apropriado.</span><span class="sxs-lookup"><span data-stu-id="63c31-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="63c31-109">Clique em **discos** ao longo de saudação extremidade esquerda do painel de máquina virtual hello, em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="63c31-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="63c31-110">Painel de máquina virtual Olá lista Nome hello e tipo de todos os discos conectados.</span><span class="sxs-lookup"><span data-stu-id="63c31-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="63c31-111">Por exemplo, esta tela mostra uma máquina virtual com um disco do sistema operacional (SO) e um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="63c31-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Encontrar disco de dados](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="63c31-113">Desanexar o disco Olá</span><span class="sxs-lookup"><span data-stu-id="63c31-113">Detach hello disk</span></span>
1. <span data-ttu-id="63c31-114">De Olá portal do Azure, clique em **máquinas virtuais**e então clique Olá nome da máquina virtual Olá que possui o disco de dados Olá deseja toodetach.</span><span class="sxs-lookup"><span data-stu-id="63c31-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="63c31-115">Clique em **discos** ao longo de saudação extremidade esquerda do painel de máquina virtual hello, em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="63c31-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="63c31-116">Clique em disco Olá toodetach desejado.</span><span class="sxs-lookup"><span data-stu-id="63c31-116">Click hello disk you want toodetach.</span></span>

  ![Identificar Olá disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="63c31-118">Na barra de comandos de saudação, clique em **desanexar**.</span><span class="sxs-lookup"><span data-stu-id="63c31-118">From hello command bar, click **Detach**.</span></span>

  ![Localizar Olá comando detach](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="63c31-120">Na janela de confirmação de saudação, clique em **Sim** toodetach disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="63c31-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Confirmar desanexando disco Olá](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="63c31-122">disco Olá permanece no armazenamento, mas não está mais anexado tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="63c31-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
