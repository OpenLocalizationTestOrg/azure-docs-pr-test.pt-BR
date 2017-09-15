

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="2baea-101">Gerar o arquivo de Solicitação de Assinatura de Certificado</span><span class="sxs-lookup"><span data-stu-id="2baea-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="2baea-102">O APNS (Serviço de Notificação por Push da Apple) usa certificados para autenticar suas notificações por push.</span><span class="sxs-lookup"><span data-stu-id="2baea-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="2baea-103">Siga estas instruções para criar o certificado de push necessário para enviar e receber notificações.</span><span class="sxs-lookup"><span data-stu-id="2baea-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="2baea-104">Para obter mais informações sobre esses conceitos, consulte a documentação oficial do [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) .</span><span class="sxs-lookup"><span data-stu-id="2baea-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="2baea-105">Gere o arquivo CSR (Solicitação de Assinatura de Certificado), usado pela Apple para gerar um certificado de push assinado.</span><span class="sxs-lookup"><span data-stu-id="2baea-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="2baea-106">Em seu Mac, execute a ferramenta Acesso do Conjunto de Chaves.</span><span class="sxs-lookup"><span data-stu-id="2baea-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="2baea-107">Ela pode ser aberta da pasta **Utilitários** ou da pasta **Outros** no launch pad.</span><span class="sxs-lookup"><span data-stu-id="2baea-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="2baea-108">Clique em **Acesso do Conjunto de Chaves**, expanda **Assistente de Certificado** e clique em **Solicitar um Certificado de uma Autoridade de Certificação...**.</span><span class="sxs-lookup"><span data-stu-id="2baea-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="2baea-109">Selecione seu **Endereço de Email de Usuário** e seu **Nome Comum**, verifique se **Salvo em disco** está selecionado e, em seguida, clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="2baea-110">Deixe o campo **Endereço de Email de CA** em branco, pois ele não é necessário.</span><span class="sxs-lookup"><span data-stu-id="2baea-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="2baea-111">Digite um nome para o arquivo CSR (Solicitação de Assinatura de Certificado) em **Salvar como**, selecione o local em **Onde** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="2baea-112">Isso salvará o arquivo CSR no local selecionado; o local padrão está situado na Área de Trabalho.</span><span class="sxs-lookup"><span data-stu-id="2baea-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="2baea-113">Lembre-se do local escolhido para esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="2baea-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="2baea-114">Em seguida, você registrará seu aplicativo na Apple, habilitará as notificações por push e carregará esse CSR exportado para criar um certificado de push.</span><span class="sxs-lookup"><span data-stu-id="2baea-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="2baea-115">Registrar seu aplicativo para notificações por push</span><span class="sxs-lookup"><span data-stu-id="2baea-115">Register your app for push notifications</span></span>
<span data-ttu-id="2baea-116">Para poder enviar notificações por push para um aplicativo iOS, você deverá registrar seu aplicativo na Apple e também registrar-se em notificações por push.</span><span class="sxs-lookup"><span data-stu-id="2baea-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="2baea-117">Se você ainda não registrou seu aplicativo, navegue até o <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de Provisionamento do iOS</a> no Apple Developer Center, faça logon com a sua Apple ID, clique em **Identificadores**, em seguida, clique em **IDs de Aplicativo** e, finalmente, clique no sinal de **+** para registrar um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2baea-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="2baea-118">Atualize os três campos a seguir para o novo aplicativo e clique em **Continuar**:</span><span class="sxs-lookup"><span data-stu-id="2baea-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="2baea-119">**Nome**: digite um nome descritivo para o aplicativo no campo **Nome**, na seção **Descrição de ID do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="2baea-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="2baea-120">**Identificador de Pacote**: na seção **ID do Aplicativo Explícita**, digite um **Identificador de Pacote** no formato `<Organization Identifier>.<Product Name>`, como mencionado no [Guia de Distribuição de Aplicativo](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="2baea-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="2baea-121">O *Identificador de Organização* e *Nome do Produto* usados deverão corresponder ao identificador da organização e o nome do produto usados quando você criar seu projeto XCode.</span><span class="sxs-lookup"><span data-stu-id="2baea-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="2baea-122">Na captura de tela abaixo, *NotificationHubs* é usado como um identificador de organização e *GetStarted* é usado como o nome do produto.</span><span class="sxs-lookup"><span data-stu-id="2baea-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="2baea-123">Garantir que isso corresponda aos valores que você usará em seu projeto XCode permitirá que você use o perfil de publicação correto com XCode.</span><span class="sxs-lookup"><span data-stu-id="2baea-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="2baea-124">**Notificações por Push**: marque a opção **Notificações por Push** na seção **Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2baea-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="2baea-125">Isso gerará sua ID do Aplicativo e solicitará que você confirme as informações.</span><span class="sxs-lookup"><span data-stu-id="2baea-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="2baea-126">Clique em **Registrar** para confirmar a nova ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2baea-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="2baea-127">Depois de clicar em **Registrar**, você verá a tela **Registro concluído**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2baea-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="2baea-128">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="2baea-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="2baea-129">Na Central de Desenvolvedores, em IDs de Aplicativo, localize a ID do aplicativo que você acabou de criar e clique na respectiva linha.</span><span class="sxs-lookup"><span data-stu-id="2baea-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="2baea-130">Clicar na ID do aplicativo exibirá os detalhes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2baea-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="2baea-131">Clique no botão **Editar** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2baea-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="2baea-132">Role até a parte inferior da tela e clique no botão **Criar Certificado...** na seção **Certificado SSL por Push para Desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="2baea-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="2baea-133">Isso exibirá o assistente "Adicionar Certificado de iOS".</span><span class="sxs-lookup"><span data-stu-id="2baea-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2baea-134">Este tutorial usa um certificado de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2baea-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="2baea-135">O mesmo processo é usado para registrar um certificado de produção.</span><span class="sxs-lookup"><span data-stu-id="2baea-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="2baea-136">Use o mesmo tipo de certificado ao enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="2baea-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="2baea-137">Clique em **Escolher Arquivo**, navegue até o local em que salvou o arquivo CSR criado na primeira tarefa e clique em **Gerar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="2baea-138">Depois que o certificado for criado pelo portal, clique no botão **Baixar** e, em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="2baea-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="2baea-139">Isso baixará e salvará esse certificado no seu computador na pasta Downloads.</span><span class="sxs-lookup"><span data-stu-id="2baea-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="2baea-140">Por padrão, o arquivo baixado, um certificado de desenvolvimento, é denominado **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="2baea-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="2baea-141">Clique duas vezes no certificado de push baixado, **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="2baea-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="2baea-142">Isso instalará o novo certificado no Conjunto de Chaves, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2baea-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="2baea-143">O nome em seu certificado pode ser diferente, mas ele será prefixado com **Serviços de Notificação por Push do iOS para Desenvolvimento da Apple:**.</span><span class="sxs-lookup"><span data-stu-id="2baea-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="2baea-144">No Acesso ao Conjunto de Chaves, clique com o botão direito do mouse no novo certificado push criado na categoria **Certificados** .</span><span class="sxs-lookup"><span data-stu-id="2baea-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="2baea-145">Clique em **Exportar**, nomeie o arquivo, selecione o formato **.p12** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="2baea-146">Anote o nome do arquivo e o local do certificado .p12 exportado.</span><span class="sxs-lookup"><span data-stu-id="2baea-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="2baea-147">Ele será usado para habilitar a autenticação com APNS.</span><span class="sxs-lookup"><span data-stu-id="2baea-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2baea-148">Este tutorial cria um arquivo QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="2baea-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="2baea-149">O nome do arquivo e o local podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="2baea-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="2baea-150">Criar um perfil de provisionamento para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="2baea-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="2baea-151">De volta ao <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de Provisionamento do iOS</a>, selecione **Perfis de Provisionamento**, escolha **Tudo** e clique no botão **+** para criar um novo perfil.</span><span class="sxs-lookup"><span data-stu-id="2baea-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="2baea-152">Isso iniciará o Assistente **Adicionar Perfil de Provisionamento do iOS**</span><span class="sxs-lookup"><span data-stu-id="2baea-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="2baea-153">Selecione **Desenvolvimento de Aplicativos do iOS** em **Desenvolvimento** como o tipo de perfil de provisionamento e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="2baea-154">Em seguida, selecione a ID do aplicativo que você acabou de criar da lista suspensa **ID do Aplicativo** e clique em **Continuar**</span><span class="sxs-lookup"><span data-stu-id="2baea-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="2baea-155">Na tela **Selecionar certificados**, selecione seu certificado de desenvolvimento normal usado por assinatura de código e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="2baea-156">Esse não é o certificado de push que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="2baea-156">This is not the push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="2baea-157">Em seguida, selecione os **Dispositivos** a serem usados no teste e clique em **Continuar**</span><span class="sxs-lookup"><span data-stu-id="2baea-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="2baea-158">Por fim, escolha um nome para o perfil em **Nome do Perfil** e clique em **Gerar**.</span><span class="sxs-lookup"><span data-stu-id="2baea-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="2baea-159">Quando o novo perfil de provisionamento for criado, clique para baixá-lo e instalá-lo em seu computador de desenvolvimento do Xcode.</span><span class="sxs-lookup"><span data-stu-id="2baea-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="2baea-160">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="2baea-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
