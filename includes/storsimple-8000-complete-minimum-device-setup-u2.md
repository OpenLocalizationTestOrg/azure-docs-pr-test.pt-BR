<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>configuração de dispositivos de StorSimple mínimo do toocomplete Olá

   > [!NOTE]
   > Você não pode alterar o nome de dispositivo de Olá depois que a instalação mínima do dispositivo Olá é concluída.
   
1. Na lista de tabela Olá dos dispositivos de saudação de **dispositivos** folha, selecione e clique em seu dispositivo. Olá dispositivo está em um **pronto tooset backup** estado. Olá **Configurar dispositivo** folha é aberta.

     ![Interfaces de rede da instalação mínima do dispositivo do StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. Em Olá **Configurar dispositivo** folha:
   
   1. Forneça um **nome amigável** para seu dispositivo. nome do dispositivo padrão Olá reflete informações como o número de série e modelo do dispositivo hello. Você pode atribuir um nome amigável do backup too64 caracteres toomanage seu dispositivo.
   2. Saudação de conjunto **fuso horário** com base em localização geográfica hello, no qual Olá dispositivo está sendo implantado. Seu dispositivo usa esse fuso horário para todas as operações agendadas.
   3. Em Olá **DATA 0 configurações**:

       1. O DATA 0 mostra de interface de rede como habilitada com hello rede (IP, sub-rede, gateway) configuradas por meio do Assistente de instalação de saudação. DATA 0 também é habilitada automaticamente para a nuvem e iSCSI.

       2. Fornecem Olá fixos endereços IP para o controlador 0 e 1. **endereços IP fixos do controlador de saudação toobe liberar IPs de sub-rede de saudação acessível pelo endereço IP do dispositivo hello.** Se hello interface DATA 0 foi configurada para IPv4, hello fixa toobe de necessidade de endereços IP fornecido no hello formato IPv4. Se você tiver fornecido um prefixo para a configuração de IPv6, Olá endereços IP fixos são preenchidos automaticamente nesses campos.

            ![Interfaces de rede da instalação mínima do dispositivo do StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Olá endereços IP para o controlador de saudação fixos são usados para atender dispositivo de toohello atualizações hello. Portanto, Olá IPs fixo deve ser roteáveis e capazes de tooconnect toohello da Internet. Você pode verificar se o controlador fixo IPs são roteáveis usando Olá [Test-HcsmConnection] [ Test] cmdlet. Olá seguinte exemplo mostra IPs de controlador fixa é roteada toohello Internet e pode acessar Olá servidores do Microsoft Update.

            ![Test-HcsmConnection mostrando IPs roteáveis](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Clique em **OK**. configuração do dispositivo Olá inicia. Quando a configuração do dispositivo Olá for concluída, você será notificado. Olá alterações de status de dispositivo muito**Online** em Olá **dispositivos** folha.

    ![Interfaces de rede da instalação mínima do dispositivo do StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
