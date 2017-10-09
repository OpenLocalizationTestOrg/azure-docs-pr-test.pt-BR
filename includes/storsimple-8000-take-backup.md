<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="a08ef-101">tootake um backup</span><span class="sxs-lookup"><span data-stu-id="a08ef-101">tootake a backup</span></span>

1. <span data-ttu-id="a08ef-102">Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="a08ef-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a08ef-103">Na listagem tabular de saudação de dispositivos, selecione e clique em seu dispositivo e, em seguida, clique em **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="a08ef-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="a08ef-104">Em Olá **configurações** folha, ir muito**Configurações > Gerenciar > política de Backup**.</span><span class="sxs-lookup"><span data-stu-id="a08ef-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="a08ef-106">Em Olá **política de Backup** folha, clique em **+ adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="a08ef-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="a08ef-108">Em Olá **Criar política de backup** folha, forneça um nome que contenha entre 3 e 150 caracteres para sua política de backup.</span><span class="sxs-lookup"><span data-stu-id="a08ef-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="a08ef-109">Selecione Olá volumes toobe backup.</span><span class="sxs-lookup"><span data-stu-id="a08ef-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="a08ef-110">Se você selecionar mais de um volume, esses volumes são toocreate agrupado junto um backup consistente.</span><span class="sxs-lookup"><span data-stu-id="a08ef-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="a08ef-112">Na folha **Adicionar primeira agenda**:</span><span class="sxs-lookup"><span data-stu-id="a08ef-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="a08ef-113">Selecione o tipo de saudação do backup.</span><span class="sxs-lookup"><span data-stu-id="a08ef-113">Select hello type of backup.</span></span> <span data-ttu-id="a08ef-114">Para obter restaurações mais rápidas, selecione instantâneo **Local**.</span><span class="sxs-lookup"><span data-stu-id="a08ef-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="a08ef-115">Para obter resiliência de dados, selecione instantâneo de **Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="a08ef-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="a08ef-116">Especifique a frequência de backup Olá em minutos, horas, dias ou semanas.</span><span class="sxs-lookup"><span data-stu-id="a08ef-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="a08ef-117">Selecione um tempo de retenção.</span><span class="sxs-lookup"><span data-stu-id="a08ef-117">Select a retention time.</span></span> <span data-ttu-id="a08ef-118">as escolhas de retenção de saudação dependem da frequência de backup hello.</span><span class="sxs-lookup"><span data-stu-id="a08ef-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="a08ef-119">Por exemplo, para uma política diária, Olá retenção pode ser especificada em semanas, enquanto a retenção para uma política mensal será indicada em meses.</span><span class="sxs-lookup"><span data-stu-id="a08ef-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="a08ef-120">Selecione Olá hora e data Olá política de backup.</span><span class="sxs-lookup"><span data-stu-id="a08ef-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="a08ef-121">Clique em **Okey** toocreate política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="a08ef-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="a08ef-123">Clique em **criar** toostart criação de política de backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="a08ef-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="a08ef-124">Você será notificado quando a política de backup Olá é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="a08ef-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="a08ef-125">lista de saudação de políticas de backup também é atualizada.</span><span class="sxs-lookup"><span data-stu-id="a08ef-125">hello list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="a08ef-127">Agora você tem uma política de backup que cria backups agendados de seus dados de volume.</span><span class="sxs-lookup"><span data-stu-id="a08ef-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




