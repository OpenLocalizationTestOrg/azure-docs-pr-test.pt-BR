<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b73f4-101">atualizações regulares de tooinstall por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b73f4-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b73f4-102">Abra o console serial do dispositivo hello e selecione a opção 1, **entrar com acesso completo**.</span><span class="sxs-lookup"><span data-stu-id="b73f4-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b73f4-103">Digite a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="b73f4-103">Type hello password.</span></span> <span data-ttu-id="b73f4-104">a senha padrão Olá é *Password1*.</span><span class="sxs-lookup"><span data-stu-id="b73f4-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="b73f4-105">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="b73f4-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="b73f4-106">Você será notificado se houver atualizações disponíveis e se as atualizações de saudação são interrompidas ou interrupções.</span><span class="sxs-lookup"><span data-stu-id="b73f4-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="b73f4-107">No prompt de comando hello, digite:</span><span class="sxs-lookup"><span data-stu-id="b73f4-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="b73f4-108">processo de atualização de saudação será iniciado.</span><span class="sxs-lookup"><span data-stu-id="b73f4-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b73f4-109">Esse comando se aplica apenas atualizações de tooregular.</span><span class="sxs-lookup"><span data-stu-id="b73f4-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="b73f4-110">Executar esse comando em apenas um controlador, mas ambos os controladores serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="b73f4-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="b73f4-111">Você pode perceber um failover de controlador durante o processo de atualização de saudação; No entanto, Olá failover não afetará a disponibilidade do sistema ou a operação.</span><span class="sxs-lookup"><span data-stu-id="b73f4-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

