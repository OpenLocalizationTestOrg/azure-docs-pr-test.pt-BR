<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>dispositivo de saudação tooconfigure e registrar

1. Acesse a interface do Windows PowerShell Olá no seu console serial do dispositivo StorSimple. Consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) para obter instruções. **Ser exatamente o procedimento de saudação toofollow-se ou não será capaz de tooaccess console de saudação.**

2. Na sessão de saudação que é aberta, pressione **Enter** tooget de tempo de um prompt de comando.

3. Será solicitada toochoose Olá idioma que você deseja tooset para seu dispositivo. Especificar o idioma de saudação e, em seguida, pressione **Enter**.

4. No menu do console serial Olá que é apresentado, escolha a opção 1 muito**entrar com acesso completo**.
     Conclua as etapas 5-12 tooconfigure Olá mínima necessária as configurações de rede para seu dispositivo. **Essas etapas de configuração necessário toobe realizada no controlador active de saudação do dispositivo Olá.** menu do console serial Olá indica o estado do controlador de saudação na mensagem de saudação do banner. Se você não estiver conectado toohello de controlador ativo, desconecte e, em seguida, conecte-se o controlador ativo toohello.

5. No prompt de comando hello, digite sua senha. senha do dispositivo padrão Olá é **Password1**.

6. Saudação de tipo comando a seguir: `Invoke-HcsSetupWizard`.

7. Um Assistente de instalação será exibido toohelp você definir configurações de rede de saudação para dispositivo hello. Forneça Olá Olá informações a seguir:
   
   * Endereço IP hello dados 0 interface de rede
   * Máscara da sub-rede
   * Gateway
   * Endereço IP do servidor DNS Primário

   Veja abaixo um exemplo de saída.

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    Olá precede a saída de exemplo, você pode ver que sistema hello está validando as configurações de rede depois de cada etapa no processo de saudação.

     > [!NOTE]
     > Você pode ter toowait por alguns minutos para máscara de sub-rede hello e toobe de configurações de DNS Olá aplicado. Se você receber uma mensagem de erro de "Verificação Olá rede conectividade tooData 0", verifique a conexão de rede física Olá na interface de rede 0 de dados de saudação do seu controlador ativo.

8. (Opcional) configure seu servidor proxy da Web. Embora a configuração do proxy da Web seja opcional, **saiba que se você usar um proxy da Web, poderá apenas configurá-lo aqui**. Para obter mais informações, vá muito[configurar o proxy da web para seu dispositivo](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configure um servidor NTP primário para seu dispositivo. Os servidores NTP são necessários, pois seu dispositivo deve sincronizar a hora para que ele possa se autenticar com seus provedores de serviço de nuvem. Certifique-se de que sua rede permite toopass de tráfego NTP do toohello seu data center da Internet. Se isso não for possível, especifique um servidor NTP interno.

    Um exemplo de saída é mostrado abaixo.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Por motivos de segurança, senha de administrador de dispositivo de saudação expira após Olá primeira sessão, e você precisará toochange it agora. Quando solicitado, forneça uma senha de administrador do dispositivo. Uma senha de administrador do dispositivo válida deve ter entre 8 e 15 caracteres. Olá senha deve conter três das seguintes Olá: caracteres minúsculo, maiusculo, numéricos e especiais.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. a etapa final Olá no Assistente de instalação Olá registra seu dispositivo com hello serviço do Gerenciador de dispositivos do StorSimple. Para isso, você precisará Olá chave de registro que você obteve na etapa 2. Depois que você fornecer a chave de registro de saudação, talvez seja necessário toowait 2 a 3 minutos antes de saudação dispositivo está registrado.
    
    > [!NOTE]
    > Você pode pressionar Ctrl + C a qualquer assistente de instalação do tempo tooexit hello. Se você inseriu todas as configurações de rede de saudação (endereço IP para Data 0, máscara de sub-rede e Gateway), as entradas serão mantidas.
    
    Um exemplo de saída é mostrado abaixo.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Depois de saudação dispositivo estiver registrado, uma chave de criptografia de dados de serviço será exibida. Copie essa chave e salve-a em um local seguro. **Essa chave será exigida com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço do Gerenciador de dispositivos do StorSimple.** Consulte também[segurança de StorSimple](../articles/storsimple/storsimple-security.md) para obter mais informações sobre essa chave.
    
    ![Dispositivo de registro do StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > texto de saudação toocopy da janela de console serial hello, basta selecionar o texto de saudação. Em seguida, você deve ser capaz de toopaste-la na área de transferência de saudação ou qualquer editor de texto. Não use Ctrl + a chave de criptografia de dados de serviço C toocopy hello. Usar Ctrl + C fará com que você tooexit Olá Assistente de instalação. Como resultado, senha de administrador de dispositivo de saudação não será alterada e dispositivo Olá reverterá toohello senha de padrão.
    
13. Console serial da saudação de saída.
14. Retorno toohello portal do Azure e Olá concluir as etapas a seguir:
    
    1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour.
    2. Clique em **Dispositivos**.
    3. No hello tabela lista de dispositivos, verifique se que esse dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação. status de saudação do dispositivo deve ser **pronto tooset backup**.
       
        ![Página dos Dispositivos StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Você pode precisar toowait para alguns minutos para Olá dispositivo status toochange muito**pronto tooset backup**.
       
        Se o dispositivo de saudação não aparece nessa lista, você precisará toomake-se de que seu firewall de rede foi configurado conforme descrito em [requisitos de rede para seu dispositivo StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Verifique se a porta 9354 é aberta para comunicação de saída como isso é usado pelo barramento de serviço Olá para comunicação de dispositivo de serviço do Gerenciador de dispositivos do StorSimple.

