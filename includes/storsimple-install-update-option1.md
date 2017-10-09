<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>hotfixes toodownload
Execute Olá etapas toodownload Olá software update a seguir.

1. Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.
    ![Instalar o catálogo](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de saudação de saudação hotfix que você deseja toodownload, por exemplo **3063418**e, em seguida, clique em **pesquisa**.
4. Você verá Olá **StorSimple atualização 1.2 Appliance atualização** pacote. Clique em **Adicionar**. atualização de saudação será adicionada toohello carrinho.
5. Procure os hotfixes adicionais listadas na tabela de saudação acima (**3043005** e **3063416**) e adicionar cada carrinho hello.
6. Clique em **Exibir carrinho**.
   
    ![Exibir carrinho](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Clique em **Download**. Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear. Olá as atualizações são baixadas toohello local especificado e colocada em uma subpasta com mesmo nome como atualização de saudação do hello. pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.

> [!NOTE]
> Olá hotfixes deve ser acessíveis de ambos os toodetect controladores mensagens de qualquer erro em potencial do controlador de par de saudação.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall e verifique se os hotfixes do modo normal
Executar Olá tooinstall as etapas a seguir e verifique se Olá hotfixes do modo normal. Se você já instalou usando Olá Portal do Azure, vá em frente muito[instalar e verificar os hotfixes do modo de manutenção](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall Olá de atualização de software, interface do acesso saudação do Windows PowerShell no seu console serial do dispositivo StorSimple. Siga Olá detalhadas instruções [console serial do PuTTy Use tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). No prompt de comando hello, pressione **Enter**.
2. Selecione **opção 1** toolog toohello dispositivo com acesso completo.
3. tooinstall Olá pacote de atualização, no prompt de comando hello, digite:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Use o IP em vez de DNS no caminho de compartilhamento Olá acima de comando. parâmetro de credencial de saudação é usado somente se você estiver acessando um compartilhamento autenticado.
   
    É recomendável que você use compartilhamentos de tooaccess de parâmetro de credencial de saudação. Mesmo compartilhamentos que estão abertos muito "everyone" é normalmente não abrir toounauthenticated usuários.
   
    Um exemplo de saída é mostrado abaixo.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Tipo **Y** quando tooconfirm solicitada Olá a instalação do hotfix.
5. Monitorar atualização hello usando Olá `Get-HcsUpdateStatus` cmdlet.
   
    Olá seguinte saída de exemplo mostra Olá atualização em andamento. Olá `RunInprogress` será `True` quando a atualização de saudação está em andamento.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Olá saída de exemplo a seguir indica que a atualização Olá foi concluída. Olá `RunInProgress` será `False` quando a atualização de saudação foi concluída.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > Ocasionalmente, Olá cmdlet relatórios `False` quando a atualização de saudação está em andamento. tooensure que Olá hotfix for concluída, aguarde alguns minutos, execute o comando novamente e verificar que Olá `RunInProgress` é `False`. Se for, Olá hotfix foi concluída.
   > 
   > 
6. Após a conclusão da atualização de software Olá, verificar se as versões de software de sistema hello. Digite hello comando a seguir:
   
    `Get-HcsSystem`
   
    Você deve ver Olá versões a seguir:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Se números de versão de saudação não serão alterados após a aplicação de atualização de hello, indica que esse hotfix Olá falhou tooapply. Caso isso aconteça, entre em contato com o [Suporte da Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) para obter mais ajuda.
7. Repita as etapas 3 a 5 tooinstall Olá restantes hotfix do modo regular (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall e verifique se os hotfixes do modo de manutenção
Use atualizações de firmware de disco KB3063416 tooinstall. Essas atualizações precisam de interrupção e levar em torno de 30 a 45 minutos toocomplete. Você pode escolher tooinstall em uma janela de manutenção planejada, console serial do dispositivo de toohello conexão.

atualizações de firmware de disco de saudação tooinstall, siga as instruções de saudação abaixo.

1. Coloque o dispositivo Olá no modo de manutenção. Observe que você não deve usar o Windows PowerShell remoto ao conectar-se o dispositivo tooa no modo de manutenção. Você precisará toorun esse cmdlet no controlador de dispositivo hello quando conectados por meio do console serial do dispositivo hello. Tipo:
   
    `Enter-HcsMaintenanceMode`
   
    Um exemplo de saída é mostrado abaixo.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
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
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Usando o monitor Olá instalar progresso `Get-HcsUpdateStatus` comando. Olá atualização é concluída quando hello `RunInProgress` muda muito`False`.
4. Após a conclusão da instalação hello, controlador Olá no qual o hotfix do modo de manutenção Olá foi instalado será reinicializado. Faça logon como opção 1 com acesso completo e verifique se a versão de firmware de disco hello. Tipo:
   
   `Get-HcsFirmwareVersion`
   
   Olá esperado versões de firmware de disco são:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Executar Olá `Get-HcsFirmwareVersion` comando Olá segundo controlador tooverify que Olá a versão do software foi atualizado. Em seguida, você pode sair do modo de manutenção de saudação. Digite hello comando para cada controlador de dispositivo a seguir:
   
   `Exit-HcsMaintenanceMode`
5. controladores de saudação reiniciar quando você sair do modo de manutenção. Depois de firmware de disco Olá atualizações são aplicadas com êxito e dispositivo Olá saiu do modo de manutenção, toohello retorno portal clássico do Azure. Observe que esse portal Olá não pode mostrar que você instalou as atualizações do modo de manutenção Olá por 24 horas.

