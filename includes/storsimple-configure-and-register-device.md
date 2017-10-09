<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de saudação tooconfigure e registrar
1. Acesse a interface do Windows PowerShell Olá no seu console serial do dispositivo StorSimple. Consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de saudação toofollow-se ou não será capaz de tooaccess console de saudação.**
2. Na sessão de saudação que é aberta, pressione Enter de um tempo tooget um prompt de comando. 
3. Será solicitada toochoose Olá idioma que você deseja tooset para seu dispositivo. Especifique o idioma de saudação e pressione Enter. 
   
    ![O StorSimple configura e registra o dispositivo 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. No menu do console serial Olá que é apresentado, escolha toolog opção 1 em com acesso completo. 
   
    ![Dispositivo de registro do StorSimple 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Conclua as etapas 5-12 tooconfigure Olá mínima necessária as configurações de rede para seu dispositivo. **Essas etapas de configuração necessário toobe realizada no controlador active de saudação do dispositivo Olá.** menu do console serial Olá indica o estado do controlador de saudação na mensagem de saudação do banner. Se você não estiver conectado toohello de controlador ativo, desconecte e, em seguida, conecte-se o controlador ativo toohello.
5. No prompt de comando hello, digite sua senha. senha do dispositivo padrão Olá é **Password1**.
6. Digite hello comando a seguir:
   
     `Invoke-HcsSetupWizard` 
7. Um Assistente de instalação será exibido toohelp você definir configurações de rede de saudação para dispositivo hello. Forneça Olá Olá informações a seguir: 
   
   * Endereço IP hello dados 0 interface de rede
   * Máscara da sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário
   * Endereço IP do servidor NTP Primário
     
     > [!NOTE]
     > Você pode ter toowait por alguns minutos para máscara de sub-rede hello e toobe de configurações de DNS Olá aplicado. Se você receber um "hello dispositivo não está pronto." mensagem de erro, conexão de rede física de Olá seleção na interface de rede 0 de dados de saudação do seu controlador ativo.
     > 
     > 
8. (Opcional) configure seu servidor proxy da Web. Embora a configuração do proxy da Web seja opcional, **saiba que se você usar um proxy da Web, poderá apenas configurá-lo aqui**. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). Se você tiver problemas durante esta etapa, consulte diretrizes de tootroubleshooting para [erros durante a configuração de proxy da web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Você pode pressionar Ctrl + C a qualquer assistente de instalação do tempo tooexit hello. As configurações aplicadas antes de você dar esse comando serão mantidas.

1. Por motivos de segurança, senha de administrador de dispositivo de saudação expira após Olá primeira sessão, e você precisará toochange-lo para sessões posteriores. Quando solicitado, forneça uma senha de administrador do dispositivo. Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres. senha de saudação deve conter uma combinação de caracteres minúsculos, caracteres em maiusculas, números e caracteres especiais.
2. senha do StorSimple Snapshot Manager Olá também é definida aqui. Use essa senha ao autenticar um dispositivo com o host do Windows executando o Gerenciador de Instantâneos StorSimple. Quando solicitado, forneça uma senha do 14 too15 caracteres. Olá senha deve conter uma combinação de três das seguintes Olá: caracteres minúsculo, maiusculo, numéricos e especiais. 
   
   ![Dispositivo de registro do StorSimple 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Você pode redefinir a senha de Gerenciador de instantâneos StorSimple de saudação da interface do serviço StorSimple Manager hello. Para obter etapas detalhadas, consulte muito[alterar senhas de StorSimple hello usando Olá serviço StorSimple Manager](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot problemas durante esta etapa, consulte diretrizes de tootroubleshooting para [erros relacionados toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. a etapa final Olá no Assistente de instalação Olá registra seu dispositivo com hello serviço StorSimple Manager. Para isso, você precisará Olá chave de registro que você obteve na etapa 2. Depois que você fornecer a chave de registro de saudação, talvez seja necessário toowait 2 a 3 minutos antes de saudação dispositivo está registrado.
   
   tootroubleshoot de falhas de registro de dispositivo, consulte muito[erros durante o registro de dispositivo](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Para obter a solução de problemas, você também pode consultar muito[exemplo passo a passo de solução de problemas](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Depois de saudação dispositivo estiver registrado, uma chave de criptografia de dados de serviço será exibida. Copie essa chave e salve-a em um local seguro.
   
   > [!WARNING]
   > Essa chave será exigida com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço StorSimple Manager. Consulte também[segurança de StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.
   > 
   > 
   
    ![Dispositivo de registro do StorSimple 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    texto de saudação toocopy da janela de console serial hello, basta selecionar o texto de saudação. Em seguida, você deve ser capaz de toopaste-la na área de transferência de saudação ou qualquer editor de texto. Não use Ctrl + a chave de criptografia de dados de serviço C toocopy hello. Usar Ctrl + C fará com que você tooexit Olá Assistente de instalação. Como resultado, senha de administrador do dispositivo hello e senha do StorSimple Snapshot Manager Olá não serão alteradas e dispositivo Olá reverterá toohello senhas de padrão.
5. Console serial da saudação de saída.
6. Retorno toohello portal clássico do Azure e Olá concluir as etapas a seguir:
   
   1. Clique duas vezes em sua saudação do Gerenciador do StorSimple service tooaccess **início rápido** página.
   2. Clique em **Exibir dispositivos conectados**.
   3. Em Olá **dispositivos** , verifique se o dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação. status de saudação do dispositivo deve ser **Online**. Se o status do dispositivo Olá **Offline**, aguarde alguns minutos para Olá online toocome de dispositivo.
   
   ![Página dos Dispositivos StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Depois que o dispositivo hello está online, conecte os cabos de rede de saudação que você tinha desconectado no início desta etapa hello.
   > 
   > 

Depois que o dispositivo Olá for registrado com êxito e não ficar online, você pode executar Olá `Test-HcsmConnection -Verbose` tooensure que Olá conectividade de rede está íntegro. Para Olá detalhadas de uso desse cmdlet, vá muito[referência cmdlet para Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Vídeo disponível](./media/storsimple-configure-and-register-device/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como tooconfigure e registrar seu dispositivo por meio do Windows PowerShell para StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

