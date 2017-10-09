#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="36d5b-101">Configurar o projeto de iOS Olá no Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="36d5b-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="36d5b-102">No Xamarin.Studio, abra **Info. plist**e atualização hello **identificador de pacote** com hello agrupar ID que você criou anteriormente com sua nova ID de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36d5b-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="36d5b-103">Role para baixo demais**modos de segundo plano**.</span><span class="sxs-lookup"><span data-stu-id="36d5b-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="36d5b-104">Selecione Olá **habilitar modos de segundo plano** caixa e hello **remotas notificações** caixa.</span><span class="sxs-lookup"><span data-stu-id="36d5b-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="36d5b-105">Clique duas vezes em seu projeto no hello solução painel tooopen **opções de projeto**.</span><span class="sxs-lookup"><span data-stu-id="36d5b-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="36d5b-106">Em **criar**, escolha **iOS de assinatura de pacote**e selecione Olá identidade correspondente e o perfil de provisionamento você acabou de configurar para este projeto.</span><span class="sxs-lookup"><span data-stu-id="36d5b-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="36d5b-107">Isso garante que o projeto Olá usa o novo perfil de saudação para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="36d5b-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="36d5b-108">Olá oficial Xamarin dispositivo provisionamento documentação, consulte [Xamarin aprovisionamento].</span><span class="sxs-lookup"><span data-stu-id="36d5b-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="36d5b-109">Configurar o projeto de iOS Olá no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="36d5b-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="36d5b-110">No Visual Studio, clique com botão direito hello e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="36d5b-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="36d5b-111">Nas páginas de propriedades de saudação, clique em Olá **iOS aplicativo** guia e atualização Olá **identificador** com a ID de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="36d5b-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="36d5b-112">Em Olá **iOS de assinatura de pacote** guia identidade correspondente selecione hello e provisionamento de perfil você configurou backup para este projeto.</span><span class="sxs-lookup"><span data-stu-id="36d5b-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="36d5b-113">Isso garante que o projeto Olá usa o novo perfil de saudação para assinatura de código.</span><span class="sxs-lookup"><span data-stu-id="36d5b-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="36d5b-114">Olá oficial Xamarin dispositivo provisionamento documentação, consulte [Xamarin aprovisionamento].</span><span class="sxs-lookup"><span data-stu-id="36d5b-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="36d5b-115">Clique duas vezes em tooopen Info. plist e, em seguida, habilitar **RemoteNotifications** em **modos de segundo plano**.</span><span class="sxs-lookup"><span data-stu-id="36d5b-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin aprovisionamento]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
