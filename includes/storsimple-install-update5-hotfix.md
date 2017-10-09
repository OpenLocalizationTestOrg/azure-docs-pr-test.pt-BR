<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a>hotfixes toodownload

Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.

1. Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.

    ![Instalar o catálogo](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de saudação de saudação hotfix que você deseja toodownload, por exemplo **4037264**e, em seguida, clique em **pesquisa**.
   
    Olá hotfix listagem aparece, por exemplo, **cumulativa 5.0 de atualização de pacote de Software para StorSimple 8000 Series**.
   
    ![Pesquisar o catálogo](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. Clique em **Download**. Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear. Clique em arquivos de saudação toodownload toohello especificado local e a pasta. pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.
5. Procure os hotfixes adicionais listadas na tabela de saudação acima (**4037266**), e correspondente de saudação do download arquivos pastas específicas toohello conforme listado na saudação anterior da tabela.

> [!NOTE]
> Olá hotfixes deve ser acessíveis de ambos os toodetect controladores mensagens de qualquer erro em potencial do controlador de par de saudação.
>
> Olá hotfixes devem ser copiados em pastas separadas e 3. Por exemplo, a atualização do agente de Cis/software/MDS de dispositivo Olá pode ser copiada em _FirstOrderUpdate_ Olá a pasta, todas as outras atualizações sem interrupção podem ser copiadas no hello _SecondOrderUpdate_ pasta, e atualizações do modo de manutenção copiadas na _ThirdOrderUpdate_ pasta.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e verifique se os hotfixes do modo normal

Executar Olá tooinstall as etapas a seguir e verifique se a hotfixes do modo normal. Se você já instalou usando Olá portal do Azure, vá em frente muito[instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Olá hotfixes, interface do acesso saudação do Windows PowerShell no seu console serial do dispositivo StorSimple. Siga Olá detalhadas instruções [console serial do PuTTy Use tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console). No prompt de comando hello, pressione **Enter**.
2. Selecione **opção 1** toolog toohello dispositivo com acesso completo. É recomendável que você instale o hotfix Olá no controlador passivo Olá primeiro.
3. tooinstall Olá hotfix, no prompt de comando hello, digite:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Use o IP em vez de DNS no caminho de compartilhamento Olá acima de comando. parâmetro de credencial de saudação é usado somente se você estiver acessando um compartilhamento autenticado.
   
    É recomendável que você use compartilhamentos de tooaccess de parâmetro de credencial de saudação. Mesmo compartilhamentos que estão abertos muito "everyone" é normalmente não abrir toounauthenticated usuários.
   
4. Fornece Olá senha quando solicitado. Uma saída de exemplo para instalar atualizações do hello primeira ordem é mostrada abaixo. Para a primeira atualização de ordem Olá, é necessário toopoint toohello determinado arquivo.

    >[!NOTE] 
    > Você deve instalar Olá _HcsSoftwareUpdate.exe_ primeiro. Após a conclusão dessa instalação, instale _CisMdsAgentUpdate.exe_.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. Tipo **Y** quando tooconfirm solicitada Olá a instalação do hotfix.
6. Monitorar atualização hello usando Olá `Get-HcsUpdateStatus` cmdlet. atualização de saudação primeiro será concluída em controlador passivo hello. Depois que o controlador passivo Olá é atualizado, haverá um failover e atualização hello, em seguida, será aplicada em Olá outro controlador. atualização de saudação é concluída quando ambos os controladores de saudação são atualizados.
   
    Olá seguinte saída de exemplo mostra Olá atualização em andamento. Olá `RunInprogress` é `True` quando a atualização de saudação está em andamento.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Olá saída de exemplo a seguir indica que a atualização Olá foi concluída. Olá `RunInProgress` é `False` quando a atualização de saudação é concluída.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Ocasionalmente, Olá cmdlet relatórios `False` quando a atualização de saudação está em andamento. tooensure que Olá hotfix for concluída, aguarde alguns minutos, execute o comando novamente e verificar que Olá `RunInProgress` é `False`. Se for, Olá hotfix foi concluída.

7. Após a conclusão da atualização de software Olá, verificar se as versões de software de sistema hello. Tipo:
   
    `Get-HcsSystem`
   
    Você deve ver Olá versões a seguir:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    Se o número de versão Olá não for alterada após a aplicação de atualização de saudação, indica que esse hotfix Olá falhou tooapply. Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) para obter mais ajuda.
     
    > [!IMPORTANT]
    > Você deve reiniciar o controlador ativo do hello via Olá `Restart-HcsController` Olá cmdlet antes de aplicar a próxima atualização.
     
8. Repita as etapas de 3 a 6 tooinstall Olá _CisMDSAgentupdate.exe_ agente baixado tooyour _FirstOrderUpdate_ pasta.
8. Repita as etapas 3 a 6 tooinstall Olá segundo atualizações da ordem. 

    > [!NOTE] 
    > Para atualizações de segunda ordem, várias atualizações podem ser instaladas executando apenas Olá `Start-HcsHotfix cmdlet` e toohello pasta onde se encontram segundo atualizações da ordem. Olá cmdlet executará todas as atualizações de saudação disponíveis na pasta hello. Se uma atualização já estiver instalada, a lógica de atualização de saudação detectar que e não aplicar essa atualização.

    Depois que todos os hotfixes Olá estiverem instalados, use Olá `Get-HcsSystem` cmdlet. Olá versões devem ser:
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e verifique se os hotfixes do modo de manutenção

Use atualizações de firmware de disco KB4037263 tooinstall. Essas atualizações precisam de interrupção e levar cerca de 30 minutos toocomplete. Você pode escolher tooinstall em uma janela de manutenção planejada, console serial do dispositivo de toohello conexão.

> [!NOTE] 
> Se o firmware de disco já está atualizado, você não precisará tooinstall essas atualizações. Executar Olá `Get-HcsUpdateAvailability` de toocheck de console serial do dispositivo Olá se atualizações estiverem disponíveis e se Olá atualiza são interrompida (modo de manutenção) ou interrupções (modo normal) atualizações.

atualizações de firmware de disco de saudação tooinstall, siga as instruções de saudação abaixo.

1. Coloque o dispositivo de saudação no modo de manutenção de saudação. 

    > [!NOTE] 
    > Não use a comunicação remota do Windows PowerShell ao conectar-se o dispositivo tooa no modo de manutenção. Em vez disso, execute este cmdlet no controlador de dispositivo hello quando conectados por meio do console serial do dispositivo hello.

    controlador de saudação tooplace no modo de manutenção, digite:
   
    `Enter-HcsMaintenanceMode`
   
    Um exemplo de saída é mostrado abaixo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Ambos os controladores Olá reinicie em modo de manutenção.
2. atualização de firmware de disco de saudação do tooinstall, tipo:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Um exemplo de saída é mostrado abaixo.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Usando o monitor Olá instalar progresso `Get-HcsUpdateStatus` comando. Olá atualização é concluída quando hello `RunInProgress` muda muito`False`.
4. Após a conclusão da instalação hello, reinicia controlador Olá no qual Olá hotfix do modo de manutenção foi instalado. Faça logon como opção 1 com acesso completo e verifique se a versão de firmware de disco hello. Tipo:
   
   `Get-HcsFirmwareVersion`
   
   Olá esperado versões de firmware de disco são:
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   Um exemplo de saída é mostrado abaixo.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    Executar Olá `Get-HcsFirmwareVersion` comando Olá segundo controlador tooverify que Olá a versão do software foi atualizado. Em seguida, você pode sair do modo de manutenção de saudação. toodo, digite Olá comando para cada controlador de dispositivo a seguir:
   
   `Exit-HcsMaintenanceMode`

5. controladores de saudação reiniciar quando você sair do modo de manutenção. Depois de firmware de disco Olá atualizações são aplicadas com êxito e dispositivo Olá saiu do modo de manutenção, toohello retorno portal do Azure. Observe que esse portal Olá não pode mostrar que você instalou as atualizações do modo de manutenção Olá por 24 horas.

