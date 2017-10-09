#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Configurar o projeto de iOS Olá no Xamarin Studio
1. No Xamarin.Studio, abra **Info. plist**e atualização hello **identificador de pacote** com hello agrupar ID que você criou anteriormente com sua nova ID de aplicativo.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Role para baixo demais**modos de segundo plano**. Selecione Olá **habilitar modos de segundo plano** caixa e hello **remotas notificações** caixa.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Clique duas vezes em seu projeto no hello solução painel tooopen **opções de projeto**.
4. Em **criar**, escolha **iOS de assinatura de pacote**e selecione Olá identidade correspondente e o perfil de provisionamento você acabou de configurar para este projeto.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Isso garante que o projeto Olá usa o novo perfil de saudação para assinatura de código. Olá oficial Xamarin dispositivo provisionamento documentação, consulte [Xamarin aprovisionamento].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Configurar o projeto de iOS Olá no Visual Studio
1. No Visual Studio, clique com botão direito hello e, em seguida, clique em **propriedades**.
2. Nas páginas de propriedades de saudação, clique em Olá **iOS aplicativo** guia e atualização Olá **identificador** com a ID de saudação que você criou anteriormente.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. Em Olá **iOS de assinatura de pacote** guia identidade correspondente selecione hello e provisionamento de perfil você configurou backup para este projeto.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Isso garante que o projeto Olá usa o novo perfil de saudação para assinatura de código. Olá oficial Xamarin dispositivo provisionamento documentação, consulte [Xamarin aprovisionamento].
4. Clique duas vezes em tooopen Info. plist e, em seguida, habilitar **RemoteNotifications** em **modos de segundo plano**.

[Xamarin aprovisionamento]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
