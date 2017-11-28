### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="530b6-101">Permitir acesso do Mobile Engagement à sua chave de API do GCM</span><span class="sxs-lookup"><span data-stu-id="530b6-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="530b6-102">Para permitir que o Mobile Engagement envie notificações por push em seu nome, é preciso conceder acesso à sua chave de API.</span><span class="sxs-lookup"><span data-stu-id="530b6-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="530b6-103">Isso é feito configurando e inserindo sua chave no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="530b6-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="530b6-104">No Portal Clássico do Azure, verifique se você está no aplicativo que estamos usando para este projeto e clique no botão **Acionar** na parte inferior:</span><span class="sxs-lookup"><span data-stu-id="530b6-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="530b6-105">Em seguida, clique na seção **Configurações** -> **Push Nativo** para inserir a chave do GCM:</span><span class="sxs-lookup"><span data-stu-id="530b6-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="530b6-106">Clique no ícone **Editar** na frente da **Chave de API**, na seção **Configurações do GCM**, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="530b6-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="530b6-107">No menu pop-up, cole a Chave do Servidor GCM obtida antes e clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="530b6-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="530b6-108"><a id="send"></a>Envie uma notificação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="530b6-108"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="530b6-109">Agora criaremos uma campanha simples de notificação por push que enviará uma notificação por push para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="530b6-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="530b6-110">Navegue até a guia **REACH** em seu portal do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="530b6-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="530b6-111">Clique em **Novo anúncio** para criar sua campanha de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="530b6-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="530b6-112">Configure o primeiro campo da campanha executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="530b6-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="530b6-113">a.</span><span class="sxs-lookup"><span data-stu-id="530b6-113">a.</span></span> <span data-ttu-id="530b6-114">Nome de sua campanha.</span><span class="sxs-lookup"><span data-stu-id="530b6-114">Name your campaign.</span></span>
   
    <span data-ttu-id="530b6-115">b.</span><span class="sxs-lookup"><span data-stu-id="530b6-115">b.</span></span> <span data-ttu-id="530b6-116">Selecione o **Tipo de entrega** como *Sistema de notificação -> Simples*: esse é o tipo de notificação por push do Android simples que apresenta um título e uma pequena linha de texto.</span><span class="sxs-lookup"><span data-stu-id="530b6-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="530b6-117">c.</span><span class="sxs-lookup"><span data-stu-id="530b6-117">c.</span></span> <span data-ttu-id="530b6-118">Selecione a **Hora de entrega** como *Sempre* para permitir que o aplicativo receba uma notificação quer ele tenha sido iniciado ou não.</span><span class="sxs-lookup"><span data-stu-id="530b6-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="530b6-119">d.</span><span class="sxs-lookup"><span data-stu-id="530b6-119">d.</span></span> <span data-ttu-id="530b6-120">No texto de notificação, digite o **Título** , que estará em negrito no envio por push.</span><span class="sxs-lookup"><span data-stu-id="530b6-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="530b6-121">e.</span><span class="sxs-lookup"><span data-stu-id="530b6-121">e.</span></span> <span data-ttu-id="530b6-122">Em seguida, digite sua **Mensagem**</span><span class="sxs-lookup"><span data-stu-id="530b6-122">Then type your **Message**</span></span>
4. <span data-ttu-id="530b6-123">Role para baixo e, na seção **Conteúdo**, selecione **Somente notificação**.</span><span class="sxs-lookup"><span data-stu-id="530b6-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="530b6-124">Você concluiu a configuração da campanha mais básica possível.</span><span class="sxs-lookup"><span data-stu-id="530b6-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="530b6-125">Agora, role para baixo novamente e clique no botão **Criar** para salvar sua campanha.</span><span class="sxs-lookup"><span data-stu-id="530b6-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="530b6-126">Última etapa: clique em **Ativar** para ativar sua campanha e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="530b6-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

