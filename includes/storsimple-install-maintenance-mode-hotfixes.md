<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="86f18-101">tooinstall hotfixes do modo de manutenção por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="86f18-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="86f18-102">No modo de manutenção, precisa tooapply Olá hotfix primeiro em um controlador e, em seguida, em Olá outro controlador.</span><span class="sxs-lookup"><span data-stu-id="86f18-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="86f18-103">Coloque o dispositivo de saudação em modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="86f18-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="86f18-104">Consulte [etapa 2: modo de manutenção insira](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções sobre como o modo de manutenção tooenter.</span><span class="sxs-lookup"><span data-stu-id="86f18-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="86f18-105">tooapply Olá hotfix, tipo:</span><span class="sxs-lookup"><span data-stu-id="86f18-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="86f18-106">Quando solicitado, forneça Olá caminho toohello pasta de rede compartilhada que contém os arquivos de hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="86f18-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="86f18-107">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="86f18-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="86f18-108">Tipo **Y** tooproceed com a instalação do hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="86f18-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="86f18-109">Após ter aplicado Olá hotfix em um controlador, logon toohello outro controlador.</span><span class="sxs-lookup"><span data-stu-id="86f18-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="86f18-110">Aplique o hotfix de saudação de controlador de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="86f18-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="86f18-111">Após Olá hotfixes forem aplicados, saia do modo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="86f18-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="86f18-112">Veja a [Etapa 4: Sair do modo de manutenção](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="86f18-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

