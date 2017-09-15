<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="03849-101">Para fazer um backup</span><span class="sxs-lookup"><span data-stu-id="03849-101">To take a backup</span></span>

1. <span data-ttu-id="03849-102">Vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03849-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="03849-103">Da listagem de tabela de dispositivos, selecione e clique em seu dispositivo e, em seguida, clique em **Todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="03849-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="03849-104">Na folha **Configurações**, vá para **Configurações > Gerenciar > Política de backup**.</span><span class="sxs-lookup"><span data-stu-id="03849-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="03849-106">Na folha **Política de backup**, clique em **+ Adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="03849-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="03849-108">Na folha **Criar política de backup**, forneça um nome que contenha entre três e 150 caracteres para sua política de backup.</span><span class="sxs-lookup"><span data-stu-id="03849-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="03849-109">Selecione os volumes a serem incluídos no backup.</span><span class="sxs-lookup"><span data-stu-id="03849-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="03849-110">Se você selecionar mais de um volume, esses volumes serão agrupados para criar um backup com controle de falhas.</span><span class="sxs-lookup"><span data-stu-id="03849-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="03849-112">Na folha **Adicionar primeira agenda**:</span><span class="sxs-lookup"><span data-stu-id="03849-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="03849-113">Selecione o tipo de backup.</span><span class="sxs-lookup"><span data-stu-id="03849-113">Select the type of backup.</span></span> <span data-ttu-id="03849-114">Para obter restaurações mais rápidas, selecione instantâneo **Local**.</span><span class="sxs-lookup"><span data-stu-id="03849-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="03849-115">Para obter resiliência de dados, selecione instantâneo de **Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="03849-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="03849-116">Especifique a frequência de backup em minutos, em horas, em dias ou em semanas.</span><span class="sxs-lookup"><span data-stu-id="03849-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="03849-117">Selecione um tempo de retenção.</span><span class="sxs-lookup"><span data-stu-id="03849-117">Select a retention time.</span></span> <span data-ttu-id="03849-118">As opções de retenção dependem da frequência do backup.</span><span class="sxs-lookup"><span data-stu-id="03849-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="03849-119">Por exemplo, para uma política diária, a retenção pode ser especificada em semanas, enquanto a retenção para uma política mensal é especificada em meses.</span><span class="sxs-lookup"><span data-stu-id="03849-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="03849-120">Selecione a hora e a data de início para a política de backup.</span><span class="sxs-lookup"><span data-stu-id="03849-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="03849-121">Clique em **OK** para criar a política de backup.</span><span class="sxs-lookup"><span data-stu-id="03849-121">Click **OK** to create the backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="03849-123">Clique em **Criar** para iniciar a criação de política de backup.</span><span class="sxs-lookup"><span data-stu-id="03849-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="03849-124">Você será notificado quando a política de backup for criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="03849-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="03849-125">A lista de políticas de backup também é atualizada.</span><span class="sxs-lookup"><span data-stu-id="03849-125">The list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="03849-127">Agora você tem uma política de backup que cria backups agendados de seus dados de volume.</span><span class="sxs-lookup"><span data-stu-id="03849-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




