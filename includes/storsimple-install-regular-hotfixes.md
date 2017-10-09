<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="eb72f-101">hotfixes regulares de tooinstall por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="eb72f-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="eb72f-102">Conecte-se toohello console serial do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eb72f-102">Connect toohello device serial console.</span></span> <span data-ttu-id="eb72f-103">Para obter mais informações, consulte [etapa 1: conectar-se o console serial toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="eb72f-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="eb72f-104">No menu do console serial hello, selecione a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="eb72f-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="eb72f-105">Digite a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb72f-105">Type hello password.</span></span> <span data-ttu-id="eb72f-106">a senha padrão Olá é **Password1**.</span><span class="sxs-lookup"><span data-stu-id="eb72f-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="eb72f-107">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="eb72f-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="eb72f-108">Esse comando se aplica somente tooregular hotfixes.</span><span class="sxs-lookup"><span data-stu-id="eb72f-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="eb72f-109">Executar esse comando em apenas um controlador, mas ambos os controladores serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="eb72f-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="eb72f-110">Você pode perceber um failover de controlador durante o processo de atualização de saudação; No entanto, Olá failover não afetará a disponibilidade do sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="eb72f-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="eb72f-111">Quando solicitado, forneça Olá caminho toohello pasta de rede compartilhada que contém os arquivos de hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="eb72f-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="eb72f-112">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="eb72f-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="eb72f-113">Tipo **Y** tooproceed com a instalação do hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="eb72f-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

