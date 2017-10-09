<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de saudação tooconfigure e registrar
1. Acesse a interface do Windows PowerShell Olá no seu console serial do dispositivo StorSimple. Consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de saudação toofollow-se ou não será capaz de tooaccess console de saudação.**
2. Na sessão de saudação que é aberta, pressione Enter de um tempo tooget um prompt de comando. 
3. Será solicitada toochoose Olá idioma que você deseja tooset para seu dispositivo. Especifique o idioma de saudação e pressione Enter. 
   
    ![O StorSimple configura e registra o dispositivo 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. No menu do console serial Olá que é apresentado, escolha toolog opção 1 em com acesso completo. 
   
    ![Dispositivo de registro do StorSimple 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. Execute Olá seguindo as etapas tooconfigure Olá mínima necessária as configurações de rede para seu dispositivo.
   
   > [!IMPORTANT]
   > Essas etapas de configuração necessário toobe realizada no controlador active de saudação do dispositivo Olá. menu do console serial Olá indica o estado do controlador de saudação na mensagem de saudação do banner. Se você não são conectar o controlador ativo toohello, desconecte e, em seguida, conecte-se o controlador ativo toohello.
   > 
   > 
   
   1. No prompt de comando hello, digite sua senha. senha do dispositivo padrão Olá é **Password1**.
   2. Digite hello comando a seguir:
      
        `Invoke-HcsSetupWizard`
   3. Um Assistente de instalação será exibido toohelp você definir configurações de rede de saudação para dispositivo hello. Saudação de fonte de informações a seguir: 
      
      * Endereço IP da interface de rede DADOS 0
      * Máscara da sub-rede
      * Gateway
      * Endereço IP do servidor DNS Primário
      * Endereço IP do servidor NTP Primário
      
      > [!NOTE]
      > Você pode ter toowait por alguns minutos para máscara de sub-rede hello e toobe de configurações de DNS aplicado. 
      > 
      > 
   4. Opcionalmente, configure seu servidor proxy da Web.
      
      > [!IMPORTANT]
      > Embora a configuração do proxy da Web seja opcional, saiba que se você usar um proxy da Web, só poderá configurá-lo aqui. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](../articles/storsimple/storsimple-configure-web-proxy.md). 
      > 
      > 
6. Pressione Ctrl + C tooexit Assistente de instalação de saudação.
7. Instale atualizações de saudação da seguinte maneira:
   
   1. Use Olá seguir cmdlet tooset IPs em ambos os controladores de saudação:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. No prompt de comando hello, execute `Get-HcsUpdateAvailability`. Você deve ser notificado de que há atualizações disponíveis.
   3. Execute `Start-HcsUpdate`. Você pode executar esse comando em qualquer nó. Atualizações serão aplicadas no primeiro controlador de hello, controlador Olá realizará o failover e, em seguida, Olá atualizações serão aplicadas em Olá outro controlador.
      
      Você pode monitorar o progresso de Olá Olá atualização executando `Get-HcsUpdateStatus`.    
      
      Olá seguinte saída de exemplo mostra Olá atualização em andamento.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      Olá saída de exemplo a seguir indica que a atualização Olá foi concluída.
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      Pode levar até horas too11 tooapply todas as atualizações, incluindo de Olá Olá atualizações do Windows.

8. Depois que todos os hello atualizações são instaladas com êxito, execute hello seguinte cmdlet tooconfirm que Olá software atualizações foram aplicadas corretamente:
   
     `Get-HcsSystem`
   
    Você deve ver Olá versões a seguir:
   
   * HcsSoftwareVersion: 6.3.9600.17491
   * CisAgentVersion: 1.0.9037.0
   * MdsAgentVersion: 26.0.4696.1433
9. Olá execução tooconfirm cmdlet que Olá atualização de firmware a seguir foi aplicada corretamente:
   
    `Start-HcsFirmwareCheck`.
   
     Olá firmware status deve ser **UpToDate**.
10. Execute Olá seguindo o portal do Microsoft Azure Government de cmdlet toopoint Olá dispositivo toohello (porque ele aponta pública portal clássico do Azure toohello por padrão). Isso reiniciará os dois controladores. É recomendável que você use duas sessões PuTTY toosimultaneously conectar tooboth controladores para que você possa ver quando cada controlador é reiniciado.
    
     `Set-CloudPlatform -AzureGovt_US`
    
    Você verá uma mensagem de confirmação. Aceite o padrão de saudação (**Y**).
11. Olá execução após a instalação do cmdlet tooresume:
    
     `Invoke-HcsSetupWizard`
    
     ![Retomar o assistente de instalação](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    Quando você continuar a instalação, o assistente Olá será versão Olá Update 1 (que corresponde a tooversion 17469). 
12. Aceite as configurações de rede hello. Você verá uma mensagem de validação depois que aceitar cada configuração.
13. Por motivos de segurança, senha de administrador de dispositivo de saudação expira após Olá primeira sessão, e você precisará toochange it agora. Quando solicitado, forneça uma senha de administrador do dispositivo. Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres. Olá senha deve conter três das seguintes Olá: caracteres minúsculo, maiusculo, numéricos e especiais.
    
    <br/>![Dispositivo de registro do StorSimple 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. a etapa final Olá no Assistente de instalação Olá registra seu dispositivo com hello serviço StorSimple Manager. Para isso, você será necessário Olá a chave de registro de serviço que você obteve na [etapa 2: chave de registro de serviço Get hello](#step-2-get-the-service-registration-key). Depois que você fornecer a chave de registro de saudação, talvez seja necessário toowait 2 a 3 minutos antes de saudação dispositivo está registrado.
    
    > [!NOTE]
    > Você pode pressionar Ctrl + C a qualquer assistente de instalação do tempo tooexit hello. Se você inseriu todas as configurações de rede de saudação (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    > 
    > 
    
    ![Progresso do registro do StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. Depois de saudação dispositivo estiver registrado, uma chave de criptografia de dados de serviço será exibida. Copie essa chave e salve-a em um local seguro. **Essa chave será exigida com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço StorSimple Manager.** Consulte também[segurança de StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.
    
    ![Dispositivo de registro do StorSimple 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > texto de saudação toocopy da janela de console serial hello, basta selecionar o texto de saudação. Em seguida, você deve ser capaz de toopaste-la na área de transferência de saudação ou qualquer editor de texto. 
    > 
    > Não use Ctrl + a chave de criptografia de dados de serviço C toocopy hello. Usar Ctrl + C fará com que você tooexit Olá Assistente de instalação. Como resultado, senha de administrador de dispositivo de saudação não será alterada e dispositivo Olá reverterá toohello senha de padrão.
    > 
    > 
16. Console serial da saudação de saída.
17. Retornar toohello Portal do Azure governamental e concluir Olá etapas a seguir:
    
    1. Clique duas vezes em sua saudação do Gerenciador do StorSimple service tooaccess **início rápido** página.
    2. Clique em **Exibir dispositivos conectados**.
    3. Em Olá **dispositivos** , verifique se o dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação. status de saudação do dispositivo deve ser **Online**.
       
        ![Página dos Dispositivos StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        Se o status do dispositivo Olá **Offline**, aguarde alguns minutos para Olá online toocome de dispositivo. 
       
        Se o dispositivo de saudação ainda está offline após alguns minutos, você precisará toomake-se de que seu firewall de rede foi configurado conforme descrito em [requisitos de rede para seu dispositivo StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Verifique se a porta 9354 é aberta para comunicação de saída como isso é usado pelo barramento de serviço Olá para comunicação de serviço para o dispositivo StorSimple Manager.

