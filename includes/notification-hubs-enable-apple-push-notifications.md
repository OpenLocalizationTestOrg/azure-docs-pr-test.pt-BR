

## <a name="generate-hello-certificate-signing-request-file"></a>Gerar arquivo de solicitação de assinatura de certificado Olá
Olá serviço de notificação de envio por Push da Apple (APNS) usa certificados tooauthenticate as notificações por push. Siga estas instruções toocreate Olá necessário push certificado toosend e receber notificações. Para obter mais informações sobre esses conceitos, consulte oficial Olá [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentação.

Gerar arquivo de solicitação de assinatura de certificado (CSR) hello, que é usado pelo Apple toogenerate um certificado assinado de envio.

1. No seu Mac, execute Olá, ferramenta de acesso do conjunto de chaves. Ele pode ser aberto do hello **utilitários** pasta ou hello **outros** pasta no ponto de partida hello.
2. Clique em **Acesso do Conjunto de Chaves**, expanda **Assistente de Certificado** e clique em **Solicitar um Certificado de uma Autoridade de Certificação...**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Selecione seu **endereço de Email do usuário** e **nome comum** , certifique-se de que **salvo toodisk** está selecionado e, em seguida, clique em **continuar**. Deixe Olá **endereço de Email da autoridade de certificação** campo em branco, como não é necessária.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Digite um nome para o arquivo de solicitação de assinatura de certificado (CSR) de saudação em **Salvar como**, selecione Olá local **onde**, em seguida, clique em **salvar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Esse arquivo CSR Olá salva no local de saudação selecionado; saudação padrão local é Olá área de trabalho. Lembre-se de local de saudação escolhida para este arquivo.

Em seguida, você será registrar seu aplicativo com a Apple, habilitar notificações por push e carregar este toocreate exportado do CSR um certificado de push.

## <a name="register-your-app-for-push-notifications"></a>Registrar seu aplicativo para notificações por push
toobe toosend capaz de envio notificações tooan aplicativo do iOS, você deve registrar seu aplicativo com o Apple e também se registram para notificações por push.  

1. Se você já não registrou seu aplicativo, toohello, navegue <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de provisionamento do iOS</a> na Olá Apple Developer Center, faça logon com sua ID da Apple, clique em **identificadores**, em seguida, clique em **IDs de aplicativo** e, finalmente, clique em Olá  **+**  entrar tooregister um novo aplicativo.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Atualizar Olá três campos para seu novo aplicativo a seguir e, em seguida, clique em **continuar**:
   
   * **Nome**: digite um nome descritivo para o aplicativo hello **nome** campo Olá **descrição de ID de aplicativo** seção.
   * **Identificador de pacote**: sob Olá **explícita ID do aplicativo** seção, insira um **identificador de pacote** na forma de saudação `<Organization Identifier>.<Product Name>` conforme mencionado em Olá [distribuição de aplicativos Guia](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Olá *identificador de organização* e *nome do produto* usado deve coincidir com o identificador de organização hello e nome de produto que será usado quando você criar seu projeto XCode. Em Olá screeshot abaixo *hubs de notificação* é usado como um identificador de organização e *GetStarted* é usado como nome de produto hello. Assegurar-se de que isso coincide com os valores hello que você usará em seu projeto XCode permitirá que você toouse Olá correto perfil de publicação com o XCode. 
   * **Notificações por push**: seleção Olá **notificações por Push** opção Olá **serviços de aplicativos** seção.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Isso gera o ID do aplicativo e solicita a você informações de saudação do tooconfirm. Clique em **registrar** tooconfirm Olá nova ID de aplicativo.
     
      Depois de clicar em **registrar**, você verá Olá **concluir registro** tela, conforme mostrado abaixo. Clique em **Concluído**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. No hello Developer Center, em IDs de aplicativo, localize o ID do aplicativo hello que recém-criado e clique em uma linha.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Clique na ID de aplicativo hello exibir detalhes do aplicativo hello. Clique em Olá **editar** botão na parte inferior da saudação.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Role toohello inferior da tela hello e, em seguida, clique em Olá **Create Certificate...**  botão na seção Olá **desenvolvimento Push certificado de SSL**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Isso exibe o Assistente de "Adicionar o certificado do iOS" hello.
   
   > [!NOTE]
   > Este tutorial usa um certificado de desenvolvimento. Olá mesmo processo é usado ao registrar um certificado de produção. Apenas certifique-se de que você use Olá mesmo tipo de certificado ao enviar notificações.
   > 
   > 
3. Clique em **Escolher arquivo**, procurar toohello no local onde você salvou o arquivo CSR Olá que você criou na primeira tarefa de saudação e clique em **gerar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Depois de saudação certificado é criado pelo portal hello, clique em Olá **baixar** botão e, em seguida, clique em **feito**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Isso faz o download de certificado hello e salva tooyour computador na sua pasta de Downloads.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Por padrão, o arquivo chamado de um certificado de desenvolvimento baixado Olá **aps_development.cer**.
   > 
   > 
5. Clique duas vezes no certificado de push baixado Olá **aps_development.cer**.
   
      Isso instala o novo certificado de saudação em Olá conjunto de chaves, conforme mostrado abaixo:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > Olá nome no certificado pode ser diferente, mas ele será prefixado com **desenvolvimento Apple iOS serviços por Push:**.
   > 
   > 
6. No conjunto de chaves de acesso, clique com botão direito Olá novo certificado de push que você criou no hello **certificados** categoria. Clique em **exportar**, nome de arquivo hello, selecione Olá **. p12** Formatar e, em seguida, clique em **salvar**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Faça uma nota do nome de arquivo hello e o local do certificado do hello. p12 exportado. Ele será uma autenticação tooenable usado com APNS.
   
   > [!NOTE]
   > Este tutorial cria um arquivo QuickStart.p12. O nome do arquivo e o local podem ser diferentes.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Criar um perfil de provisionamento para o aplicativo hello
1. Em Olá <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">Portal de provisionamento do iOS</a>, selecione **perfis de provisionamento**, selecione **todos os**e, em seguida, clique em Olá  **+**  botão toocreate um novo perfil. Isso inicia o hello **adicionar perfil Provisiong iOS** Assistente
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Selecione **o desenvolvimento de aplicativos do iOS** em **desenvolvimento** como tipo de perfil provisiong hello e clique em **continuar**. 
3. Em seguida, selecione a ID do aplicativo hello você acabou de criar na Olá **ID do aplicativo** lista suspensa e clique em **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. Em Olá **selecionar certificados** tela, selecione o certificado de desenvolvimento comum usado para assinatura de código e clique em **continuar**. Isso não é um certificado de push Olá que você acabou de criar.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Em seguida, selecione Olá **dispositivos** toouse para teste e clique em **continuar**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Por fim, escolha um nome para o perfil de saudação em **nome do perfil**, clique em **gerar**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Quando Olá novo perfil de provisionamento é criado clique toodownload-lo e instale-o em sua máquina de desenvolvimento do Xcode. Em seguida, clique em **Concluído**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
