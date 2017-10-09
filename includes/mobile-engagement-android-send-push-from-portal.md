### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="5ad87-101">Compromisso de mobilidade de conceder acesso tooyour chave API do GCM</span><span class="sxs-lookup"><span data-stu-id="5ad87-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="5ad87-102">notificações de push tooallow Mobile Engagement toosend em seu nome, é necessário toogrant ele acessar tooyour chave de API.</span><span class="sxs-lookup"><span data-stu-id="5ad87-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="5ad87-103">Isso é feito configurando e digitar a chave no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="5ad87-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="5ad87-104">Do seu Portal clássico do Azure, certifique-se você estiver no aplicativo hello que está usando para este projeto e clique em hello **Engage** botão na parte inferior da saudação:</span><span class="sxs-lookup"><span data-stu-id="5ad87-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="5ad87-105">Em seguida, clique em Olá **configurações** -> **Push nativo** seção tooenter sua chave GCM:</span><span class="sxs-lookup"><span data-stu-id="5ad87-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="5ad87-106">Clique em hello **editar** ícone na frente do **chave API** em hello **configurações do GCM** seção conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ad87-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="5ad87-107">No pop-up hello, cole Olá GCM chave de servidor obtido antes e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5ad87-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="5ad87-108"><a id="send"></a>Enviar um aplicativo de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="5ad87-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="5ad87-109">Agora, vamos criar uma campanha de notificação por push simples que envia um aplicativo de tooour de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="5ad87-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="5ad87-110">Navegue toohello **alcançar** no seu portal do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="5ad87-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="5ad87-111">Clique em **novo comunicado** toocreate sua campanha de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="5ad87-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="5ad87-112">Configure o primeiro campo de saudação da campanha por meio de saudação etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ad87-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="5ad87-113">a.</span><span class="sxs-lookup"><span data-stu-id="5ad87-113">a.</span></span> <span data-ttu-id="5ad87-114">Nome de sua campanha.</span><span class="sxs-lookup"><span data-stu-id="5ad87-114">Name your campaign.</span></span>
   
    <span data-ttu-id="5ad87-115">b.</span><span class="sxs-lookup"><span data-stu-id="5ad87-115">b.</span></span> <span data-ttu-id="5ad87-116">Selecione Olá **tipo de entrega** como *notificação do sistema -> simples*: Este é o tipo de notificação de push Android simples Olá que apresenta um título e uma linha pequena de texto.</span><span class="sxs-lookup"><span data-stu-id="5ad87-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="5ad87-117">c.</span><span class="sxs-lookup"><span data-stu-id="5ad87-117">c.</span></span> <span data-ttu-id="5ad87-118">Selecione **tempo de entrega** como *sempre* tooallow Olá aplicativo tooreceive uma notificação se o aplicativo hello é iniciado ou não.</span><span class="sxs-lookup"><span data-stu-id="5ad87-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="5ad87-119">d.</span><span class="sxs-lookup"><span data-stu-id="5ad87-119">d.</span></span> <span data-ttu-id="5ad87-120">Em Olá Olá de tipo de texto de notificação **título** que será em negrito no envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ad87-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="5ad87-121">e.</span><span class="sxs-lookup"><span data-stu-id="5ad87-121">e.</span></span> <span data-ttu-id="5ad87-122">Em seguida, digite sua **Mensagem**</span><span class="sxs-lookup"><span data-stu-id="5ad87-122">Then type your **Message**</span></span>
4. <span data-ttu-id="5ad87-123">Role para baixo e em Olá **conteúdo** seção, selecione **somente notificação**.</span><span class="sxs-lookup"><span data-stu-id="5ad87-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="5ad87-124">Você concluiu possíveis de campanha configuração hello mais básica.</span><span class="sxs-lookup"><span data-stu-id="5ad87-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="5ad87-125">Agora, role para baixo novamente e clique em Olá **criar** botão toosave sua campanha.</span><span class="sxs-lookup"><span data-stu-id="5ad87-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="5ad87-126">Última etapa: clique em **ativar** tooactivate suas notificações de push de toosend da campanha.</span><span class="sxs-lookup"><span data-stu-id="5ad87-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

