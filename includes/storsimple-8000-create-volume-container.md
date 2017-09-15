<!--author=alkohli last changed: 06/22/17-->

#### <a name="to-create-a-volume-container"></a><span data-ttu-id="7f3dd-101">Para criar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="7f3dd-101">To create a volume container</span></span>
1. <span data-ttu-id="7f3dd-102">Acesse o serviço Gerenciador de Dispositivo StorSimple e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-102">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="7f3dd-103">Na listagem tabular dos dispositivos, selecione e clique em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-103">From the tabular listing of the devices, select and click a device.</span></span> 

    ![Folha Contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="7f3dd-105">No painel do dispositivo, clique em **+ Adicionar contêiner de volume**</span><span class="sxs-lookup"><span data-stu-id="7f3dd-105">In the device dashboard, click **+ Add volume container**</span></span>

    ![Folha Contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="7f3dd-107">Na folha **Adicionar contêiner de volume**:</span><span class="sxs-lookup"><span data-stu-id="7f3dd-107">In the **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="7f3dd-108">O dispositivo é selecionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-108">The device is automatically selected.</span></span>
   2. <span data-ttu-id="7f3dd-109">Fornecer um **Nome** para o seu contêiner do volume.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="7f3dd-110">O nome deve ter entre 3 a 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-110">The name must be 3 to 32 characters long.</span></span> <span data-ttu-id="7f3dd-111">Você não pode renomear um contêiner de volume quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="7f3dd-112">Selecione **Habilitar Criptografia de Armazenamento em Nuvem** para habilitar a criptografia dos dados enviados do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-112">Select **Enable Cloud Storage Encryption** to enable encryption of the data sent from the device to the cloud.</span></span>
   4. <span data-ttu-id="7f3dd-113">Forneça e confirme uma **Chave de Criptografia de Armazenamento em Nuvem** que possui entre 8 a 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 to 32 characters long.</span></span> <span data-ttu-id="7f3dd-114">Essa chave é usada pelo dispositivo para acessar dados criptografados.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-114">This key is used by the device to access encrypted data.</span></span>
   5. <span data-ttu-id="7f3dd-115">Selecione uma **Conta de Armazenamento** para associar a esse contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-115">Select a **Storage Account** to associate with this volume container.</span></span> <span data-ttu-id="7f3dd-116">Você pode escolher uma conta de armazenamento existente ou a conta padrão gerada no momento da criação do serviço.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-116">You can choose an existing storage account or the default account that is generated at the time of service creation.</span></span> <span data-ttu-id="7f3dd-117">Você também pode usar a opção **Adicionar novo** para especificar uma conta de armazenamento que não está vinculada a essa assinatura de serviço.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-117">You can also use the **Add new** option to specify a storage account that is not linked to this service subscription.</span></span>
   6. <span data-ttu-id="7f3dd-118">Selecione **Ilimitada** na lista suspensa **Especificar largura de banda** se desejar consumir toda a largura de banda disponível.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-118">Select **Unlimited** in the **Specify bandwidth** drop-down list if you wish to consume all the available bandwidth.</span></span> <span data-ttu-id="7f3dd-119">Você também pode definir essa opção para **Personalizada** para empregar os controles de largura de banda, e especifique um valor entre 1 Mbps e 1.000 Mbps.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-119">You can also set this option to **Custom** to employ bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="7f3dd-120">Se você tiver informações de uso da largura de banda disponíveis, você poderá alocar a largura de banda com base em uma agenda especificando **Selecionar um modelo de largura de banda**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-120">If you have your bandwidth usage information available, you may be able to allocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="7f3dd-121">Para obter um procedimento passo a passo, vá para [Adicionar um modelo de largura de banda](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span><span class="sxs-lookup"><span data-stu-id="7f3dd-121">For a step-by-step procedure, go to [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![Folha Contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="7f3dd-123">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-123">Click **Create**.</span></span>

        ![Folha Contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="7f3dd-125">Você será notificado quando o contêiner de volume for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-125">You are notified when the volume container is successfully created.</span></span>

       ![Notificação de criação do contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="7f3dd-127">O contêiner de volume criado recentemente é listado na lista de contêineres de volume para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-127">The newly created volume container is listed in the list of volume containers for your device.</span></span>

   ![Folha Adicionar contêiner de volume](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


