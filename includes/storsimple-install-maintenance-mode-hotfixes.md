<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="cae97-101">Para instalar os hotfixes do modo de manutenção por meio do Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="cae97-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cae97-102">Quando você estiver no modo de Manutenção, precisará aplicar a atualização primeiro em um controlador e, em seguida, no outro controlador.</span><span class="sxs-lookup"><span data-stu-id="cae97-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span></span>
> 
> 

1. <span data-ttu-id="cae97-103">Coloque o dispositivo no modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="cae97-103">Place the device into Maintenance mode.</span></span> <span data-ttu-id="cae97-104">Consulte [Etapa 2: Entrar no modo de manutenção](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções sobre como entrar no modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="cae97-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span></span>
2. <span data-ttu-id="cae97-105">Para aplicar o hotfix, digite:</span><span class="sxs-lookup"><span data-stu-id="cae97-105">To apply the hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="cae97-106">Quando solicitado, forneça o caminho para a pasta compartilhada que contém os arquivos de hotfix.</span><span class="sxs-lookup"><span data-stu-id="cae97-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
4. <span data-ttu-id="cae97-107">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="cae97-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="cae97-108">Digite **Y** para prosseguir com a instalação do hotfix.</span><span class="sxs-lookup"><span data-stu-id="cae97-108">Type **Y** to proceed with the hotfix installation.</span></span>
5. <span data-ttu-id="cae97-109">Após aplicar o hotfix em um controlador, faça logon no outro controlador.</span><span class="sxs-lookup"><span data-stu-id="cae97-109">After you have applied the hotfix on one controller, log on to the other controller.</span></span> <span data-ttu-id="cae97-110">Aplique o hotfix da mesma forma que você fez para o controlador anterior.</span><span class="sxs-lookup"><span data-stu-id="cae97-110">Apply the hotfix as you did for the previous controller.</span></span>
6. <span data-ttu-id="cae97-111">Após a aplicação dos hotfixes, saia do modo de Manutenção.</span><span class="sxs-lookup"><span data-stu-id="cae97-111">After the hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="cae97-112">Veja a [Etapa 4: Sair do modo de manutenção](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="cae97-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

