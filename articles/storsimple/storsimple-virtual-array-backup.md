---
title: tutorial backup do Azure StorSimple Virtual Array aaaMicrosoft | Microsoft Docs
description: Descreve como tooback matriz Virtual StorSimple compartilhamentos e volumes.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="98936-103">Fazer backup de volumes ou compartilhamentos no StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="98936-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="98936-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="98936-104">Overview</span></span>

<span data-ttu-id="98936-105">Olá matriz Virtual StorSimple é um híbrido nuvem armazenamento no dispositivo virtual local que pode ser configurado como um servidor de arquivos ou um servidor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98936-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="98936-106">matriz virtual Olá permite Olá usuário toocreate backups agendados e manuais de todos os volumes ou compartilhamentos Olá Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98936-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="98936-107">Quando configurado como um servidor de arquivos, ele também permite a recuperação em nível de item.</span><span class="sxs-lookup"><span data-stu-id="98936-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="98936-108">Este tutorial descreve como toocreate agendados e backups manuais e executar a recuperação em nível de item toorestore a exclusão de um arquivo em sua matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="98936-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="98936-109">Este tutorial aplica toohello StorSimple Virtual matrizes somente.</span><span class="sxs-lookup"><span data-stu-id="98936-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="98936-110">Para obter informações sobre a 8000 série, vá muito[criar um backup para o dispositivo da 8000 série](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="98936-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="98936-111">Fazer backup de compartilhamentos e volumes</span><span class="sxs-lookup"><span data-stu-id="98936-111">Back up shares and volumes</span></span>

<span data-ttu-id="98936-112">Backups oferecem proteção pontual, melhoram a capacidade de recuperação e minimizam os tempos de compartilhamentos e volumes.</span><span class="sxs-lookup"><span data-stu-id="98936-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="98936-113">É possível fazer backup de um compartilhamento ou volume em seu dispositivo StorSimple de duas maneiras: **Agendada** ou **Manual**.</span><span class="sxs-lookup"><span data-stu-id="98936-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="98936-114">Cada um dos métodos de saudação é abordada em Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="98936-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="98936-115">Altere a hora de início de backup Olá</span><span class="sxs-lookup"><span data-stu-id="98936-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="98936-116">Nesta versão, os backups agendados são criados por uma política padrão que é executada diariamente em um período especificado e faz backup de todos os volumes ou compartilhamentos Olá no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98936-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="98936-117">Não é possível toocreate políticas personalizadas para backups agendados no momento.</span><span class="sxs-lookup"><span data-stu-id="98936-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="98936-118">A matriz de Virtual do StorSimple tem uma política de backup padrão que inicia em um determinado horário do dia (22:30) e faz o backup de todos os volumes ou compartilhamentos Olá no dispositivo Olá uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="98936-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="98936-119">Você pode alterar o tempo de saudação em que início do backup hello, mas frequência hello e Olá retenção (que especifica o número de saudação de backups tooretain) não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="98936-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="98936-120">Durante esses backups, o dispositivo virtual inteira de saudação é feito backup.</span><span class="sxs-lookup"><span data-stu-id="98936-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="98936-121">Potencialmente, isso pode afetar o desempenho de saudação do dispositivo hello e afetam as cargas de trabalho Olá implantadas no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98936-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="98936-122">Portanto, recomendamos agendar esses backups fora do horário de pico.</span><span class="sxs-lookup"><span data-stu-id="98936-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="98936-123">backup de padrão de saudação toochange hora de início, execute Olá etapas Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="98936-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="98936-124">Olá toochange hora de início para política de backup saudação padrão</span><span class="sxs-lookup"><span data-stu-id="98936-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="98936-125">Vá muito**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="98936-125">Go too**Devices**.</span></span> <span data-ttu-id="98936-126">Olá lista de dispositivos registrados com o serviço do Gerenciador de dispositivos de StorSimple será exibida.</span><span class="sxs-lookup"><span data-stu-id="98936-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="98936-128">Selecione e clique em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98936-128">Select and click your device.</span></span> <span data-ttu-id="98936-129">Olá **configurações** folha será exibida.</span><span class="sxs-lookup"><span data-stu-id="98936-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="98936-130">Vá muito**Gerenciar > políticas de Backup**.</span><span class="sxs-lookup"><span data-stu-id="98936-130">Go too**Manage > Backup policies**.</span></span>
   
    ![selecionar o dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="98936-132">Em Olá **as políticas de Backup** folha, hora de início do saudação padrão é 22:30.</span><span class="sxs-lookup"><span data-stu-id="98936-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="98936-133">Você pode especificar a nova hora de início Olá para agendamento diário Olá no fuso horário do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98936-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Navegue toobackup políticas](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="98936-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="98936-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="98936-136">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="98936-136">Take a manual backup</span></span>

<span data-ttu-id="98936-137">Além disso tooscheduled backups, você pode fazer um backup manual do (sob demanda) dos dados de dispositivo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="98936-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="98936-138">toocreate um backup manual</span><span class="sxs-lookup"><span data-stu-id="98936-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="98936-139">Vá muito**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="98936-139">Go too**Devices**.</span></span> <span data-ttu-id="98936-140">Selecione o dispositivo e clique **...**  em hello mais à direita na linha selecionada da saudação.</span><span class="sxs-lookup"><span data-stu-id="98936-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="98936-141">No menu de contexto hello, selecione **fazer backup**.</span><span class="sxs-lookup"><span data-stu-id="98936-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Navegue tootake backup](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="98936-143">Em Olá **fazer backup** folha, clique em **fazer backup**.</span><span class="sxs-lookup"><span data-stu-id="98936-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="98936-144">Isto fará backup de todos os compartilhamentos de saudação no servidor de arquivos de saudação ou todos os volumes de saudação em seu servidor do iSCSI.</span><span class="sxs-lookup"><span data-stu-id="98936-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![backup iniciando](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="98936-146">Um backup sob demanda é iniciado e você verá que um trabalho de backup foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="98936-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![backup iniciando](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="98936-148">Depois que o trabalho de saudação for concluída com êxito, você será notificado novamente.</span><span class="sxs-lookup"><span data-stu-id="98936-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="98936-149">em seguida, inicia o processo de backup Hello.</span><span class="sxs-lookup"><span data-stu-id="98936-149">hello backup process then starts.</span></span>
   
    ![trabalho de backup criado](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="98936-151">progresso de saudação tootrack de backups de saudação e examinar os detalhes do trabalho hello, clique em notificação hello.</span><span class="sxs-lookup"><span data-stu-id="98936-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="98936-152">Isso leva muito **detalhes do trabalho**.</span><span class="sxs-lookup"><span data-stu-id="98936-152">This takes you too **Job details**.</span></span>
   
     ![detalhes do trabalho de backup](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="98936-154">Após a conclusão do backup hello, ir muito**gerenciamento > Catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="98936-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="98936-155">Você verá um instantâneo de nuvem de todos os compartilhamentos hello (ou volumes) em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98936-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Backup concluído](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="98936-157">Exibir os backups existentes</span><span class="sxs-lookup"><span data-stu-id="98936-157">View existing backups</span></span>
<span data-ttu-id="98936-158">backups existentes do tooview hello, executar Olá etapas Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="98936-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="98936-159">backups existentes tooview</span><span class="sxs-lookup"><span data-stu-id="98936-159">tooview existing backups</span></span>

1. <span data-ttu-id="98936-160">Vá muito**dispositivos** folha.</span><span class="sxs-lookup"><span data-stu-id="98936-160">Go too**Devices** blade.</span></span> <span data-ttu-id="98936-161">Selecione e clique em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="98936-161">Select and click your device.</span></span> <span data-ttu-id="98936-162">Em Olá **configurações** folha, ir muito**gerenciamento > Catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="98936-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Navegue toobackup catálogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="98936-164">Especifique Olá toobe critérios usado para filtrar a seguir:</span><span class="sxs-lookup"><span data-stu-id="98936-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="98936-165">**Intervalo de tempo** – pode ser **Última hora**, **Últimas 24 horas**, **Últimos 7 dias**, **Últimos 30 dias**, **Ano passado** e **Data personalizada**.</span><span class="sxs-lookup"><span data-stu-id="98936-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="98936-166">**Dispositivos** – selecione na lista de saudação de servidores de arquivos ou iSCSI servidores registrados com o serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="98936-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="98936-167">**Iniciado** – pode ser **Agendado** automaticamente (por uma política de backup) ou iniciado **Manualmente** (por você).</span><span class="sxs-lookup"><span data-stu-id="98936-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Backups de filtro](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="98936-169">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="98936-169">Click **Apply**.</span></span> <span data-ttu-id="98936-170">Olá lista filtrada de backups é exibida no hello **catálogo de Backup** folha.</span><span class="sxs-lookup"><span data-stu-id="98936-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="98936-171">Observe que apenas 100 elementos de backup podem ser exibidos de cada vez.</span><span class="sxs-lookup"><span data-stu-id="98936-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catálogo de backup atualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="98936-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98936-173">Next steps</span></span>

<span data-ttu-id="98936-174">Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="98936-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

