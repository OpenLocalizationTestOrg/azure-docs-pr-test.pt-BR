<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="068eb-101">tooinstall uma atualização do hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="068eb-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="068eb-102">Na página de serviço do StorSimple hello, selecione seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="068eb-102">On hello StorSimple service page, select your device.</span></span>

    ![Selecionar dispositivo](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="068eb-104">Navegue muito**configurações do dispositivo** > **atualizações de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="068eb-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="068eb-106">Uma notificação será exibida se houver novas atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="068eb-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="068eb-107">Como alternativa, no hello **atualizações de dispositivo** folha, clique em **verificar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="068eb-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="068eb-108">Um trabalho é criado tooscan atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="068eb-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="068eb-109">Você será notificado quando Olá for concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="068eb-109">You are notified when hello job completes successfully.</span></span>

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="068eb-111">É recomendável que você revise as notas de versão de saudação antes de aplicar uma atualização em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="068eb-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="068eb-112">tooapply atualizações, clique em **instalar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="068eb-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="068eb-113">Em Olá **confirmar atualizações regulares** folha, examine Olá pré-requisitos toocomplete antes de aplicar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="068eb-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="068eb-114">Selecione Olá tooindicate de caixa de seleção que você tooupdate pronto do hello dispositivo e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="068eb-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Clique em Atualizações de dispositivo](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="068eb-116">Um conjunto de verificações de pré-requisito é iniciado.</span><span class="sxs-lookup"><span data-stu-id="068eb-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="068eb-117">Essas verificações incluem:</span><span class="sxs-lookup"><span data-stu-id="068eb-117">These checks include:</span></span>
   
   * <span data-ttu-id="068eb-118">**Verificações de integridade do controlador** tooverify que ambos Olá controladores de dispositivo estiverem íntegros e online.</span><span class="sxs-lookup"><span data-stu-id="068eb-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="068eb-119">**Verificações de integridade do componente de hardware** tooverify que todos os Olá componentes de hardware no seu dispositivo StorSimple estão íntegros.</span><span class="sxs-lookup"><span data-stu-id="068eb-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="068eb-120">**DATA 0 verifica** tooverify que DATA 0 está habilitado no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="068eb-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="068eb-121">Se essa interface não estiver habilitada, você deverá habilitá-la e repetir a ação.</span><span class="sxs-lookup"><span data-stu-id="068eb-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="068eb-122">atualização de saudação é baixada e instalada somente se todas as verificações de saudação são concluídas com êxito.</span><span class="sxs-lookup"><span data-stu-id="068eb-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="068eb-123">Você será notificado quando Olá verificações estão em andamento.</span><span class="sxs-lookup"><span data-stu-id="068eb-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="068eb-124">Se Olá prechecks falharem, você será fornecido com motivos Olá da falha.</span><span class="sxs-lookup"><span data-stu-id="068eb-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="068eb-125">Resolver esses problemas e, em seguida, repita a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="068eb-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="068eb-126">Se você não pode resolver esses problemas sozinho, talvez seja necessário toocontact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="068eb-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="068eb-127">Depois de saudação prechecks são concluídos com êxito, um trabalho de atualização é criado.</span><span class="sxs-lookup"><span data-stu-id="068eb-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="068eb-128">Você será notificado quando o trabalho de atualização de saudação é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="068eb-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Criação do trabalho de atualização](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="068eb-130">atualização de saudação é então aplicada em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="068eb-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="068eb-131">atualização de saudação leva alguns toocomplete de horas.</span><span class="sxs-lookup"><span data-stu-id="068eb-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="068eb-132">Selecione o trabalho de atualização de saudação e clique em **detalhes** tooview detalhes de saudação do trabalho Olá a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="068eb-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Criação do trabalho de atualização](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="068eb-134">Você também pode monitorar o progresso de saudação do trabalho de atualização de saudação do **configurações do dispositivo > trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="068eb-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="068eb-135">Em Olá **trabalhos** folha, você pode ver Olá progresso da atualização.</span><span class="sxs-lookup"><span data-stu-id="068eb-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Criação do trabalho de atualização](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="068eb-137">Após a conclusão do trabalho hello, navegar toohello **configurações do dispositivo > atualizações de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="068eb-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="068eb-138">versão do software Olá agora deve ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="068eb-138">hello software version should now be updated.</span></span>

    ![Criação do trabalho de atualização](./media/storsimple-8000-install-update4-via-portal/update9.png)

