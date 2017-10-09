<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>configuração de dispositivos de StorSimple mínimo do toocomplete Olá
1. Em Olá **dispositivos** página dispositivo selecione hello, clique em seta para baixo Olá na página de dispositivo específico Olá dispositivo nome toogo toohello. 
   
    ![Página de dispositivos com o dispositivo online](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Clique em início rápido do ícone ![ícone de início rápido](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess Olá página de início rápido do dispositivo. Clique em **concluir a instalação do dispositivo** toostart Olá **Configurar dispositivo** assistente.
   
    ![Página de início rápido do dispositivo](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Em Olá **configurações básicas** página, Olá a seguir:
   
   1. Forneça um **nome amigável** para seu dispositivo. nome do dispositivo padrão Olá reflete informações como o número de série e modelo do dispositivo hello. Você pode atribuir um nome amigável do backup too64 caracteres toomanage seu dispositivo.
   2. Saudação de conjunto **fuso horário** com base em localização geográfica hello, no qual Olá dispositivo está sendo implantado. Seu dispositivo usará esse fuso horário para todas as operações agendadas.
   3. Em **Configurações DNS**, forneça um endereço para o **Servidor DNS Secundário**. Se você estiver usando IPv6, o campo de saudação será preenchido com base no prefixo de IPv6 Olá fornecido na interface do Windows PowerShell hello. 
      Se o servidor DNS secundário de saudação não está configurado, não será permitido toosave sua configuração de dispositivo.
   4. Em interfaces habilitadas para o iSCSI, habilite pelo menos uma rede para o iSCSI. Pelo menos uma interface de rede precisa toobe habilitado para a nuvem e uma interface precisa toobe habilitada com iSCSI. Os DADOS 0 são automaticamente habilitados para a nuvem.
      
      ![Definições básicas da instalação mínima do dispositivo do StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Clique no ícone de seta hello. ![Ícone de seta do StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Em Olá **Interfaces de rede** , forneça Olá fixa endereços IP para o controlador 0 e 1. Se hello interface DATA 0 foi configurada para IPv4, hello fixa toobe de necessidade de endereços IP fornecido no hello formato IPv4. Se você tiver fornecido um prefixo para a configuração de IPv6, Olá endereços IP fixos será preenchido automaticamente nesses campos.

    > [!NOTE] 
    > - endereços IP fixos do controlador de saudação toobe liberar IPs de sub-rede de saudação acessível pelo endereço IP do dispositivo hello.
    > - Olá fixo de endereços IP para o controlador de saudação são usados para manutenção de dispositivo de toohello atualizações hello e portanto Olá IPs fixo deve ser roteáveis e capazes de tooconnect toohello da Internet.

    ![Interfaces de rede da instalação mínima do dispositivo do StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Clique o ícone de verificação Olá ![ícone de verificação de StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Você irá retornar o dispositivo toohello **início rápido** página.
   
   > [!NOTE]
   > Você pode modificar Olá todas as outras configurações de dispositivo a qualquer momento acessando Olá **configurar** página.
   > 
   > 

![Vídeo disponível](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocomplete Olá configuração mínima do dispositivo, clique em [aqui](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

