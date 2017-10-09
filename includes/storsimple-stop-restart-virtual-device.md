#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="37f9e-101">toostop e iniciar um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="37f9e-101">toostop and start a virtual device</span></span>
<span data-ttu-id="37f9e-102">toostop um dispositivo virtual, clique em seu nome e, em seguida, clique em **desligamento**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="37f9e-103">Quando o dispositivo virtual hello está desligando, seu status é **parando**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="37f9e-104">Depois que o dispositivo virtual Olá for interrompido, seu status é **parado**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="37f9e-105">Use Olá toostop cmdlets a seguir e inicie um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="37f9e-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="37f9e-106">toorestart um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="37f9e-106">toorestart a virtual device</span></span>
<span data-ttu-id="37f9e-107">Quando um dispositivo virtual está em execução e você deseja toorestart-la, clique em seu nome e, em seguida, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="37f9e-108">Quando o dispositivo virtual hello está reiniciando, seu status é **reiniciando**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="37f9e-109">Quando o dispositivo virtual hello está pronto para você toouse, seu status é **executando**.</span><span class="sxs-lookup"><span data-stu-id="37f9e-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="37f9e-110">Use Olá cmdlet toorestart um dispositivo virtual a seguir.</span><span class="sxs-lookup"><span data-stu-id="37f9e-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

