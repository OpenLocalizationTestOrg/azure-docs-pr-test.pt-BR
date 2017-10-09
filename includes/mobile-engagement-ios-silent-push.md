> [!IMPORTANT]
> tooreceive notificações por Push do Mobile Engagement, você precisa tooenable `Silent Remote Notifications` em seu aplicativo. Você precisa matriz de UIBackgroundModes tooadd Olá remoto notificação valor toohello no seu arquivo Info. plist.
> 
> 

1. Abra `info.plist` arquivo no projeto Olá
2. Clique com o botão direito no item de saudação superior na lista de saudação (`Information Property List`) e adicione uma nova linha
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Em Olá Inserir nova linha`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Clique em linha de saudação de tooexpand Olá seta para a esquerda
5. Adicionar Olá após valor toohello item 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Depois que você alterar Olá, Olá Info. plist XML deve conter Olá a seguir de chave e valor:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Se você estiver usando **Xcode 7+** e **iOS 9+**:
   
   * Habilite **Notificações por Push** em Destinos > Nome do seu destino > Recursos.

