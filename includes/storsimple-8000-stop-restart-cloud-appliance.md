#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="2d92e-101">toostop e iniciar um dispositivo de nuvem</span><span class="sxs-lookup"><span data-stu-id="2d92e-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="2d92e-102">toostop um dispositivo de nuvem, vá toohello VM para sua solução de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2d92e-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="2d92e-103">![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="2d92e-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="2d92e-104">Na barra de comandos de saudação, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-104">From hello command bar, click **Stop**.</span></span>

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="2d92e-106">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="2d92e-108">Quando você para uma VM, ela é desalocada.</span><span class="sxs-lookup"><span data-stu-id="2d92e-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="2d92e-109">Quando o dispositivo de nuvem hello está parando, seu status é **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="2d92e-110">Depois que o dispositivo de nuvem Olá é interrompido, seu status é **parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="2d92e-112">Depois que uma VM for interrompida, clique em **iniciar** (botão fica disponível) toostart Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d92e-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="2d92e-113">Depois que o dispositivo de nuvem Olá tenha sido iniciado, seu status é **iniciado**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="2d92e-115">Use Olá toostop cmdlets a seguir e iniciar um dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2d92e-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="2d92e-116">toorestart um dispositivo de nuvem</span><span class="sxs-lookup"><span data-stu-id="2d92e-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="2d92e-117">toorestart um dispositivo de nuvem, vá toohello VM para sua solução de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2d92e-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="2d92e-118">Na barra de comandos de saudação, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="2d92e-119">Quando solicitado, confirme Olá reinicialização.</span><span class="sxs-lookup"><span data-stu-id="2d92e-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="2d92e-120">Quando o dispositivo de nuvem hello está pronto para você toouse, seu status é **executando**.</span><span class="sxs-lookup"><span data-stu-id="2d92e-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="2d92e-122">Use Olá cmdlet toorestart um dispositivo de nuvem a seguir.</span><span class="sxs-lookup"><span data-stu-id="2d92e-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

