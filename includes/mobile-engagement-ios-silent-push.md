> [!IMPORTANT]
> <span data-ttu-id="ddf6d-101">tooreceive notificações por Push do Mobile Engagement, você precisa tooenable `Silent Remote Notifications` em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ddf6d-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="ddf6d-102">Você precisa matriz de UIBackgroundModes tooadd Olá remoto notificação valor toohello no seu arquivo Info. plist.</span><span class="sxs-lookup"><span data-stu-id="ddf6d-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="ddf6d-103">Abra `info.plist` arquivo no projeto Olá</span><span class="sxs-lookup"><span data-stu-id="ddf6d-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="ddf6d-104">Clique com o botão direito no item de saudação superior na lista de saudação (`Information Property List`) e adicione uma nova linha</span><span class="sxs-lookup"><span data-stu-id="ddf6d-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="ddf6d-105">Em Olá Inserir nova linha`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="ddf6d-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="ddf6d-106">Clique em linha de saudação de tooexpand Olá seta para a esquerda</span><span class="sxs-lookup"><span data-stu-id="ddf6d-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="ddf6d-107">Adicionar Olá após valor toohello item 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="ddf6d-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="ddf6d-108">Depois que você alterar Olá, Olá Info. plist XML deve conter Olá a seguir de chave e valor:</span><span class="sxs-lookup"><span data-stu-id="ddf6d-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="ddf6d-109">Se você estiver usando **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="ddf6d-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="ddf6d-110">Habilite **Notificações por Push** em Destinos > Nome do seu destino > Recursos.</span><span class="sxs-lookup"><span data-stu-id="ddf6d-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

