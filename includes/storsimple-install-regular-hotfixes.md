<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="74b30-101">Para instalar hotfixes normais por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="74b30-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="74b30-102">Conecte-se ao console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="74b30-102">Connect to the device serial console.</span></span> <span data-ttu-id="74b30-103">Para saber mais, consulte [Etapa 1: Conectar-se ao console serial](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="74b30-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="74b30-104">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="74b30-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="74b30-105">Digite a senha.</span><span class="sxs-lookup"><span data-stu-id="74b30-105">Type the password.</span></span> <span data-ttu-id="74b30-106">A senha padrão é **Senha1**.</span><span class="sxs-lookup"><span data-stu-id="74b30-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="74b30-107">No prompt de comando, digite:</span><span class="sxs-lookup"><span data-stu-id="74b30-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="74b30-108">>>-Este comando se aplica somente a hotfixes normais.</span><span class="sxs-lookup"><span data-stu-id="74b30-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="74b30-109">Executar esse comando em apenas um controlador, mas ambos os controladores serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="74b30-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="74b30-110">Você pode perceber um failover de controlador durante o processo de atualização; no entanto, o failover não afetará a disponibilidade ou operação do sistema.</span><span class="sxs-lookup"><span data-stu-id="74b30-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="74b30-111">Quando solicitado, forneça o caminho para a pasta compartilhada que contém os arquivos de hotfix.</span><span class="sxs-lookup"><span data-stu-id="74b30-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="74b30-112">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="74b30-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="74b30-113">Digite **Y** para prosseguir com a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="74b30-113">Type **Y** to proceed with the hotfix installation.</span></span>

