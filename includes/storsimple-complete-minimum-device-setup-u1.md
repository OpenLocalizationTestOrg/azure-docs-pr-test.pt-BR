<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>configuração de dispositivos de StorSimple mínimo do toocomplete Olá
1. Selecione o dispositivo hello e clique em **início rápido**. Clique em **concluir a instalação do dispositivo** Assistente do toostart Olá Configurar dispositivo.
2. No Assistente de dispositivo de configurar Olá **configurações básicas** caixa de diálogo caixa, Olá a seguir:
   
   1. Forneça um **nome amigável** para seu dispositivo. nome do dispositivo padrão Olá reflete informações como o número de série e modelo do dispositivo hello. Você pode atribuir um nome amigável do backup too64 caracteres toomanage seu dispositivo.
   2. Saudação de conjunto **fuso horário** com base em localização geográfica hello, no qual Olá dispositivo está sendo implantado. Seu dispositivo usará esse fuso horário para todas as operações agendadas.
   3. Em **Configurações DNS**, forneça um endereço para o **Servidor DNS Secundário**. Se você estiver usando IPv6, o campo de saudação será preenchido com base no prefixo de IPv6 Olá fornecido na interface do Windows PowerShell hello. 
      Se o servidor DNS secundário de saudação não está configurado, não será permitido toosave sua configuração de dispositivo.
   4. Em interfaces habilitadas para o iSCSI, habilite pelo menos uma rede para o iSCSI. Pelo menos uma interface de rede precisa toobe habilitado para a nuvem e uma interface precisa toobe habilitada com iSCSI. Os DADOS 0 são automaticamente habilitados para a nuvem.
      
      ![Definições básicas da instalação mínima do dispositivo do StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Clique no ícone de seta hello. ![Ícone de seta do StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. Em Olá **Interfaces de rede** caixa de diálogo caixa, forneça Olá fixa endereços IP para o controlador 0 e 1. **endereços IP fixos do controlador de saudação toobe liberar IPs de sub-rede de saudação acessível pelo endereço IP do dispositivo hello.** Se hello interface DATA 0 foi configurada para IPv4, hello fixa toobe de necessidade de endereços IP fornecido no hello formato IPv4. Se você tiver fornecido um prefixo para a configuração de IPv6, Olá endereços IP fixos será preenchido automaticamente nesses campos.

    ![Interfaces de rede da instalação mínima do dispositivo do StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Olá fixo de endereços IP para o controlador de saudação são usados para manutenção de dispositivo de toohello atualizações hello e portanto Olá IPs fixo deve ser roteáveis e capazes de tooconnect toohello da Internet. Você pode verificar se o controlador fixo IPs são roteáveis usando Olá [Test-HcsmConnection] [ Test] cmdlet. Olá seguinte exemplo mostra IPs de controlador fixa é roteada toohello Internet e pode acessar Olá servidores do Microsoft Update. 

     ![Test-HcsmConnection mostrando IPs roteáveis](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Clique o ícone de verificação Olá ![ícone de verificação de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Você irá retornar o dispositivo toohello **início rápido** página.
   
   > [!NOTE]
   > Você pode modificar Olá todas as outras configurações de dispositivo a qualquer momento acessando Olá **configurar** página.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx