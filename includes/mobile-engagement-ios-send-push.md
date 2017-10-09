### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="b1bbc-101">Conceder acesso tooyour Push certificado tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="b1bbc-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="b1bbc-102">tooallow Mobile Engagement toosend notificações por Push em seu nome, será necessário toogrant-lo acessar o certificado de tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="b1bbc-103">Isso é feito configurando e inserindo seu certificado no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="b1bbc-104">Certifique-se de ter o certificado .p12, conforme explicado na [documentação da Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="b1bbc-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="b1bbc-105">Navegue tooyour portal do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="b1bbc-106">Verifique se você está no hello correto e, em seguida, clique em Olá **Engage** botão na parte inferior da saudação:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="b1bbc-107">Clique em Olá **configurações** página no Portal do compromisso.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="b1bbc-108">De lá, clique em Olá **Push nativo** seção tooupload seu certificado p12:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="b1bbc-109">Selecione seu p12, carregue-o e digite sua senha:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="b1bbc-110"><a id="send"></a>Enviar um aplicativo de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="b1bbc-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="b1bbc-111">Agora, vamos criar uma campanha de notificação por Push simple que enviará um aplicativo de tooour por push:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="b1bbc-112">Navegue toohello **alcançar** no seu portal do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="b1bbc-113">Clique em **novo comunicado** toocreate sua campanha de push</span><span class="sxs-lookup"><span data-stu-id="b1bbc-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="b1bbc-114">Campos de primeira Olá da sua campanha de configuração:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="b1bbc-115">Forneça um **Nome** para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="b1bbc-116">Selecione Olá **tempo de entrega** como **somente fora do aplicativo**: isso é Olá Apple push notificação tipo simples que apresenta um texto.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="b1bbc-117">Texto de notificação hello, digite hello primeiro **título** que será a primeira linha hello push hello.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="b1bbc-118">Em seguida, digite sua **mensagem** qual será a segunda linha de saudação</span><span class="sxs-lookup"><span data-stu-id="b1bbc-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="b1bbc-119">Role para baixo e em Olá seção conteúda selecione **somente notificação**</span><span class="sxs-lookup"><span data-stu-id="b1bbc-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="b1bbc-120">Você concluiu a campanha mais básica de saudação de configuração.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="b1bbc-121">Agora, role para baixo e clique em **criar** botão toosave sua campanha de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="b1bbc-122">Por fim - clique em **ativar** toosend notificação de envio.</span><span class="sxs-lookup"><span data-stu-id="b1bbc-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="b1bbc-123">Você poderá receber a notificação de saudação em seu dispositivo iOS no Centro de notificação hello como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="b1bbc-124">Se você tiver um Apple Watch emparelhado com este dispositivo iOS, em seguida, você verá Olá notificação em seu Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="b1bbc-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

