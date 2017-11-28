
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="0079f-101">Para criar um backup manual</span><span class="sxs-lookup"><span data-stu-id="0079f-101">To create a manual backup</span></span>

1. <span data-ttu-id="0079f-102">Acesse o serviço StorSimple Device Manager e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0079f-102">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="0079f-103">Na lista tabular de dispositivos, selecione seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0079f-103">From the tabular listing of devices, select your device.</span></span> <span data-ttu-id="0079f-104">Acesse **Configurações > Gerenciar > Políticas de backup**.</span><span class="sxs-lookup"><span data-stu-id="0079f-104">Go to **Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="0079f-105">A folha **Políticas de backup** lista todas as políticas de backup em um formato tabular, incluindo a política para o volume do qual você deseja fazer backup.</span><span class="sxs-lookup"><span data-stu-id="0079f-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span></span> <span data-ttu-id="0079f-106">Selecione a política associada ao volume do qual você deseja fazer backup e clique com o botão direito para invocar o menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="0079f-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span></span> <span data-ttu-id="0079f-107">Na lista suspensa, selecione **Fazer backup agora**.</span><span class="sxs-lookup"><span data-stu-id="0079f-107">From the dropdown list, select **Back up now**.</span></span>

    ![Criar o backup manual](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="0079f-109">Na folha **Fazer backup agora**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0079f-109">In the **Back up now** blade, do the following steps:</span></span>

    1. <span data-ttu-id="0079f-110">Escolha o **Tipo de instantâneo** apropriado na lista suspensa: instantâneo **Local** ou instantâneo de **Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="0079f-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="0079f-111">Selecione instantâneo local para backups ou restaurações rápidas, e instantâneo de nuvem para resiliência de dados.</span><span class="sxs-lookup"><span data-stu-id="0079f-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Criar o backup manual](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="0079f-113">Clique em **OK** para iniciar um trabalho a fim de criar um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="0079f-113">Click **OK** to start a job to create a snapshot.</span></span> <span data-ttu-id="0079f-114">Você verá uma notificação na parte superior da página após a criação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="0079f-114">You will see a notification at the top of the page after the job is successfully created.</span></span>

        ![Criar o backup manual](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="0079f-116">Para monitorar o trabalho, clique na notificação.</span><span class="sxs-lookup"><span data-stu-id="0079f-116">To monitor the job, click the notification.</span></span> <span data-ttu-id="0079f-117">Isso levará você até a folha **Trabalhos** onde poderá exibir o andamento do trabalho.</span><span class="sxs-lookup"><span data-stu-id="0079f-117">This takes you to the **Jobs** blade where you can view the job progress.</span></span>


5. <span data-ttu-id="0079f-118">Depois que o trabalho de backup for concluído, vá para a guia **Catálogo de backup** .</span><span class="sxs-lookup"><span data-stu-id="0079f-118">After the backup job is finished, go to the **Backup catalog** tab.</span></span>

6. <span data-ttu-id="0079f-119">Defina as seleções de filtro para o dispositivo apropriado, a política de backup e o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="0079f-119">Set the filter selections to the appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="0079f-120">O backup deve aparecer na lista de conjuntos de backup que é exibida no catálogo.</span><span class="sxs-lookup"><span data-stu-id="0079f-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

