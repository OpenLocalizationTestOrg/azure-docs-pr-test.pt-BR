

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="821d7-101">Gerar arquivo de solicitação de assinatura de certificado Olá</span><span class="sxs-lookup"><span data-stu-id="821d7-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="821d7-102">Olá serviço de notificação de envio por Push da Apple (APNS) usa certificados tooauthenticate as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="821d7-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="821d7-103">Siga estas instruções toocreate Olá necessário push certificado toosend e receber notificações.</span><span class="sxs-lookup"><span data-stu-id="821d7-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="821d7-104">Para obter mais informações sobre esses conceitos, consulte oficial Olá [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentação.</span><span class="sxs-lookup"><span data-stu-id="821d7-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="821d7-105">Gerar arquivo de solicitação de assinatura de certificado (CSR) hello, que é usado pelo Apple toogenerate um certificado assinado de envio.</span><span class="sxs-lookup"><span data-stu-id="821d7-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="821d7-106">No seu Mac, execute Olá, ferramenta de acesso do conjunto de chaves.</span><span class="sxs-lookup"><span data-stu-id="821d7-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="821d7-107">Ele pode ser aberto do hello **utilitários** pasta ou hello **outros** pasta no ponto de partida hello.</span><span class="sxs-lookup"><span data-stu-id="821d7-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="821d7-108">Clique em **Acesso do Conjunto de Chaves**, expanda **Assistente de Certificado** e clique em **Solicitar um Certificado de uma Autoridade de Certificação...**.</span><span class="sxs-lookup"><span data-stu-id="821d7-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="821d7-109">Selecione seu **endereço de Email do usuário** e **nome comum** , certifique-se de que **salvo toodisk** está selecionado e, em seguida, clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="821d7-110">Deixe Olá **endereço de Email da autoridade de certificação** campo em branco, como não é necessária.</span><span class="sxs-lookup"><span data-stu-id="821d7-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="821d7-111">Digite um nome para o arquivo de solicitação de assinatura de certificado (CSR) de saudação em **Salvar como**, selecione Olá local **onde**, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="821d7-112">Esse arquivo CSR Olá salva no local de saudação selecionado; saudação padrão local é Olá área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="821d7-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="821d7-113">Lembre-se de local de saudação escolhida para este arquivo.</span><span class="sxs-lookup"><span data-stu-id="821d7-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="821d7-114">Em seguida, você será registrar seu aplicativo com a Apple, habilitar notificações por push e carregar este toocreate exportado do CSR um certificado de push.</span><span class="sxs-lookup"><span data-stu-id="821d7-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="821d7-115">Registrar seu aplicativo para notificações por push</span><span class="sxs-lookup"><span data-stu-id="821d7-115">Register your app for push notifications</span></span>
<span data-ttu-id="821d7-116">toobe toosend capaz de envio notificações tooan aplicativo do iOS, você deve registrar seu aplicativo com o Apple e também se registram para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="821d7-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="821d7-117">Se você já não registrou seu aplicativo, toohello, navegue <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de provisionamento do iOS</a> na Olá Apple Developer Center, faça logon com sua ID da Apple, clique em **identificadores**, em seguida, clique em **IDs de aplicativo** e, finalmente, clique em Olá  **+**  entrar tooregister um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="821d7-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="821d7-118">Atualizar Olá três campos para seu novo aplicativo a seguir e, em seguida, clique em **continuar**:</span><span class="sxs-lookup"><span data-stu-id="821d7-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="821d7-119">**Nome**: digite um nome descritivo para o aplicativo hello **nome** campo Olá **descrição de ID de aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="821d7-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="821d7-120">**Identificador de pacote**: sob Olá **explícita ID do aplicativo** seção, insira um **identificador de pacote** na forma de saudação `<Organization Identifier>.<Product Name>` conforme mencionado em Olá [distribuição de aplicativos Guia](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="821d7-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="821d7-121">Olá *identificador de organização* e *nome do produto* usado deve coincidir com o identificador de organização hello e nome de produto que será usado quando você criar seu projeto XCode.</span><span class="sxs-lookup"><span data-stu-id="821d7-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="821d7-122">Em Olá screeshot abaixo *hubs de notificação* é usado como um identificador de organização e *GetStarted* é usado como nome de produto hello.</span><span class="sxs-lookup"><span data-stu-id="821d7-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="821d7-123">Assegurar-se de que isso coincide com os valores hello que você usará em seu projeto XCode permitirá que você toouse Olá correto perfil de publicação com o XCode.</span><span class="sxs-lookup"><span data-stu-id="821d7-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="821d7-124">**Notificações por push**: seleção Olá **notificações por Push** opção Olá **serviços de aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="821d7-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="821d7-125">Isso gera o ID do aplicativo e solicita a você informações de saudação do tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="821d7-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="821d7-126">Clique em **registrar** tooconfirm Olá nova ID de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="821d7-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="821d7-127">Depois de clicar em **registrar**, você verá Olá **concluir registro** tela, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="821d7-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="821d7-128">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="821d7-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="821d7-129">No hello Developer Center, em IDs de aplicativo, localize o ID do aplicativo hello que recém-criado e clique em uma linha.</span><span class="sxs-lookup"><span data-stu-id="821d7-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="821d7-130">Clique na ID de aplicativo hello exibir detalhes do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="821d7-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="821d7-131">Clique em Olá **editar** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="821d7-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="821d7-132">Role toohello inferior da tela hello e, em seguida, clique em Olá **Create Certificate...**  botão na seção Olá **desenvolvimento Push certificado de SSL**.</span><span class="sxs-lookup"><span data-stu-id="821d7-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="821d7-133">Isso exibe o Assistente de "Adicionar o certificado do iOS" hello.</span><span class="sxs-lookup"><span data-stu-id="821d7-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="821d7-134">Este tutorial usa um certificado de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="821d7-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="821d7-135">Olá mesmo processo é usado ao registrar um certificado de produção.</span><span class="sxs-lookup"><span data-stu-id="821d7-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="821d7-136">Apenas certifique-se de que você use Olá mesmo tipo de certificado ao enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="821d7-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="821d7-137">Clique em **Escolher arquivo**, procurar toohello no local onde você salvou o arquivo CSR Olá que você criou na primeira tarefa de saudação e clique em **gerar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="821d7-138">Depois de saudação certificado é criado pelo portal hello, clique em Olá **baixar** botão e, em seguida, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="821d7-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="821d7-139">Isso faz o download de certificado hello e salva tooyour computador na sua pasta de Downloads.</span><span class="sxs-lookup"><span data-stu-id="821d7-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="821d7-140">Por padrão, o arquivo chamado de um certificado de desenvolvimento baixado Olá **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="821d7-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="821d7-141">Clique duas vezes no certificado de push baixado Olá **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="821d7-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="821d7-142">Isso instala o novo certificado de saudação em Olá conjunto de chaves, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="821d7-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="821d7-143">Olá nome no certificado pode ser diferente, mas ele será prefixado com **desenvolvimento Apple iOS serviços por Push:**.</span><span class="sxs-lookup"><span data-stu-id="821d7-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="821d7-144">No conjunto de chaves de acesso, clique com botão direito Olá novo certificado de push que você criou no hello **certificados** categoria.</span><span class="sxs-lookup"><span data-stu-id="821d7-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="821d7-145">Clique em **exportar**, nome de arquivo hello, selecione Olá **. p12** Formatar e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="821d7-146">Faça uma nota do nome de arquivo hello e o local do certificado do hello. p12 exportado.</span><span class="sxs-lookup"><span data-stu-id="821d7-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="821d7-147">Ele será uma autenticação tooenable usado com APNS.</span><span class="sxs-lookup"><span data-stu-id="821d7-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="821d7-148">Este tutorial cria um arquivo QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="821d7-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="821d7-149">O nome do arquivo e o local podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="821d7-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="821d7-150">Criar um perfil de provisionamento para o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="821d7-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="821d7-151">Em Olá <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de provisionamento do iOS</a>, selecione **perfis de provisionamento**, selecione **todos os**e, em seguida, clique em Olá  **+**  botão toocreate um novo perfil.</span><span class="sxs-lookup"><span data-stu-id="821d7-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="821d7-152">Isso inicia o hello **adicionar perfil Provisiong iOS** Assistente</span><span class="sxs-lookup"><span data-stu-id="821d7-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="821d7-153">Selecione **o desenvolvimento de aplicativos do iOS** em **desenvolvimento** como tipo de perfil provisiong hello e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="821d7-154">Em seguida, selecione a ID do aplicativo hello você acabou de criar na Olá **ID do aplicativo** lista suspensa e clique em **continuar**</span><span class="sxs-lookup"><span data-stu-id="821d7-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="821d7-155">Em Olá **selecionar certificados** tela, selecione o certificado de desenvolvimento comum usado para assinatura de código e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="821d7-156">Isso não é um certificado de push Olá que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="821d7-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="821d7-157">Em seguida, selecione Olá **dispositivos** toouse para teste e clique em **continuar**</span><span class="sxs-lookup"><span data-stu-id="821d7-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="821d7-158">Por fim, escolha um nome para o perfil de saudação em **nome do perfil**, clique em **gerar**.</span><span class="sxs-lookup"><span data-stu-id="821d7-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="821d7-159">Quando Olá novo perfil de provisionamento é criado clique toodownload-lo e instale-o em sua máquina de desenvolvimento do Xcode.</span><span class="sxs-lookup"><span data-stu-id="821d7-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="821d7-160">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="821d7-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
