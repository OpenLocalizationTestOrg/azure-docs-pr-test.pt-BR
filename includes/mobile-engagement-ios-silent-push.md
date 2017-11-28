> [!IMPORTANT]
> <span data-ttu-id="e0ae4-101">Para receber notificações por push do Mobile Engagement, você precisa habilitar `Silent Remote Notifications` em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0ae4-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="e0ae4-102">Você precisa adicionar o valor remote-notification à matriz UIBackgroundModes no arquivo Info.plist.</span><span class="sxs-lookup"><span data-stu-id="e0ae4-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="e0ae4-103">Abra o arquivo `info.plist` no projeto</span><span class="sxs-lookup"><span data-stu-id="e0ae4-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="e0ae4-104">Clique com o botão direito no item superior na lista (`Information Property List`) e adicione uma nova linha</span><span class="sxs-lookup"><span data-stu-id="e0ae4-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="e0ae4-105">Na nova linha, digite `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="e0ae4-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="e0ae4-106">Clique na seta à esquerda para expandir a linha</span><span class="sxs-lookup"><span data-stu-id="e0ae4-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="e0ae4-107">Adicione o seguinte valor para o item 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="e0ae4-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="e0ae4-108">Após a alteração, o XML info.plist deve conter a chave e o valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0ae4-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="e0ae4-109">Se você estiver usando **Xcode 7+** e **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="e0ae4-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="e0ae4-110">Habilite **Notificações por Push** em Destinos > Nome do seu destino > Recursos.</span><span class="sxs-lookup"><span data-stu-id="e0ae4-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

