#### <a name="to-stop-and-start-a-virtual-device"></a><span data-ttu-id="cf1e4-101">Parar e iniciar um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="cf1e4-101">To stop and start a virtual device</span></span>
<span data-ttu-id="cf1e4-102">Para parar um dispositivo virtual, clique em seu nome e, em seguida, clique em **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-102">To stop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="cf1e4-103">Enquanto o dispositivo virtual estiver desligando, seu status será **Parando**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-103">While the virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="cf1e4-104">Depois que o dispositivo virtual parar, seu status será **Parado**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-104">After the virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="cf1e4-105">Use os seguintes cmdlets para parar e iniciar um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-105">Use the following cmdlets to stop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-virtual-device"></a><span data-ttu-id="cf1e4-106">Parar e reiniciar um dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="cf1e4-106">To restart a virtual device</span></span>
<span data-ttu-id="cf1e4-107">Quando um dispositivo virtual estiver em execução e você quiser reiniciá-lo, clique em seu nome e, em seguida, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-107">When a virtual device is running and you want to restart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="cf1e4-108">Enquanto o dispositivo virtual estiver reiniciando, seu status será **Reiniciando**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-108">While the virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="cf1e4-109">Quando o dispositivo virtual estiver pronto para uso, seu status será **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-109">When the virtual device is ready for you to use, its status is **Running**.</span></span>

<span data-ttu-id="cf1e4-110">Use o seguinte cmdlet para parar e reiniciar um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="cf1e4-110">Use the following cmdlet to restart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

