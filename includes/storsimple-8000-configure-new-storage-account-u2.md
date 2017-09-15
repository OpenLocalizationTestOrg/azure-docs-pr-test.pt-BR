<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="611d1-101">Para adicionar uma credencial de conta de armazenamento na mesma assinatura do Azure que o serviço StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="611d1-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="611d1-102">Vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="611d1-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="611d1-103">Na seção **Configuração**, clique em **Credenciais da conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="611d1-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![Credenciais da conta de armazenamento](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="611d1-105">Na folha **Credenciais da conta de armazenamento**, clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="611d1-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![Adicionar uma credencial de conta de armazenamento](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="611d1-107">Na folha **Adicionar credencial de uma conta de armazenamento**, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="611d1-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="611d1-108">Como você está adicionando uma credencial de conta de armazenamento à mesma assinatura do Azure de seu serviço, certifique-se de que **Atual** esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="611d1-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="611d1-109">Na lista suspensa **conta de armazenamento**, selecione uma conta de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="611d1-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="611d1-110">Com base na conta de armazenamento selecionada, o **local** será exibido (esmaecido, e não poderá ser alterado aqui).</span><span class="sxs-lookup"><span data-stu-id="611d1-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="611d1-111">Selecione **Habilitar modo SSL** para criar um canal seguro para comunicação de rede entre o dispositivo e a nuvem.</span><span class="sxs-lookup"><span data-stu-id="611d1-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="611d1-112">Desabilite **Habilitar SSL** somente se você estiver operando em uma nuvem privada.</span><span class="sxs-lookup"><span data-stu-id="611d1-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![Folha Adicionar credenciais da conta de armazenamento](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="611d1-114">Clique em **Adicionar** para iniciar a criação do trabalho para a credencial de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="611d1-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="611d1-115">Você receberá uma notificação após a criação da credencial de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="611d1-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![Notificação de êxito para as credenciais de conta de armazenamento](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="611d1-117">A credencial da conta de armazenamento recém-criada será exibida na lista de **Credenciais de conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="611d1-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![Lista de credenciais de conta de armazenamento](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

