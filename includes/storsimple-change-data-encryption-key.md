<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Etapa 1: Autorizar uma chave de criptografia do dispositivo toochange Olá serviço dados em Olá portal clássico do Azure
Normalmente, administrador do dispositivo Olá solicita esse administrador de serviço Olá autorizar chaves de criptografia de dados de serviço para toochange um dispositivo. administrador de serviço Hello, então, autorizará chave de Olá Olá dispositivo toochange.

Esta etapa é executada no hello portal clássico do Azure. administrador de serviço Olá pode selecionar um dispositivo na lista exibida de dispositivos de saudação que são qualificado toobe autorizado. dispositivo Olá é, em seguida, o processo de alteração da chave de criptografia de dados do serviço de saudação toostart autorizados.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Quais dispositivos podem ser autorizados toochange chaves de criptografia de dados de serviço?
Um dispositivo deve atender aos Olá critérios a seguir para que possa ser alterações de criptografia de dados chave serviço tooinitiate autorizados:

* dispositivo de saudação deve ser on-line toobe qualificado para autorização de alteração de chave de criptografia de dados de serviço.
* Você pode autorizar Olá mesmo dispositivo novamente após 30 minutos se a alteração da chave de saudação não foi iniciado.
* Você pode autorizar um dispositivo diferente, desde que a alteração da chave Olá não foi iniciada pelo dispositivo anteriormente autorizado hello. Depois que o novo dispositivo de saudação tiver sido autorizado, dispositivo antigo Olá não pode iniciar a alteração hello.
* Não é possível autorizar um dispositivo, enquanto Olá substituição de chave de criptografia de dados de serviço hello está em andamento.
* Você pode autorizar um dispositivo quando alguns dispositivos Olá registrados com o serviço de saudação tiveram substituído Olá criptografia enquanto outros não. Nesses casos, os dispositivos qualificados Olá são Olá aqueles que concluíram a alteração de criptografia de dados chave serviço hello.

> [!NOTE]
> Olá portal clássico do Azure, StorSimple dispositivos virtuais não são mostrados na lista de saudação de dispositivos que podem ser autorizado a alteração da chave toostart hello.
> 
> 

Executar Olá tooselect as etapas a seguir e autorizar uma dispositivo tooinitiate Olá serviço alteração criptografia de dados chave.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize uma chave de saudação do dispositivo toochange
1. Na página de painel de serviço hello, clique em **alterar chave de criptografia de dados de serviço**.
   
    ![Alterar chave de criptografia de serviço](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. Em Olá **alterar chave de criptografia de dados de serviço** caixa de diálogo caixa, selecione e autorize uma dispositivo tooinitiate Olá serviço alteração criptografia de dados chave. lista suspensa de saudação tem todos os dispositivos qualificados Olá que podem ser autorizados.
3. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Etapa 2: Usar o Windows PowerShell para StorSimple tooinitiate Olá serviço criptografia chave alteração de dados
Esta etapa é executada no saudação do Windows PowerShell para StorSimple interface Olá autorizado dispositivo StorSimple.

> [!NOTE]
> Nenhuma operação pode ser executada no hello portal clássico do Azure do seu serviço StorSimple Manager até que a substituição de chave Olá é concluída.
> 
> 

Se você estiver usando a interface do hello dispositivo console serial tooconnect toohello do Windows PowerShell, execute Olá etapas a seguir.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>alteração da chave de criptografia de dados de serviço do tooinitiate Olá
1. Selecione a opção 1 toolog com acesso completo.
2. No prompt de comando hello, digite:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Depois que o cmdlet Olá for concluída com êxito, você obterá uma nova chave de criptografia de dados de serviço. Copie e salve essa chave para uso na etapa 3 deste processo. Esta chave será usada tooupdate Olá todos os demais dispositivos registrados com o serviço StorSimple Manager hello.
   
   > [!NOTE]
   > Esse processo deve ser iniciado em quatro horas, a contar da autorização de um dispositivo StorSimple.
   > 
   > 
   
   Essa nova chave é enviada toohello toobe enviada por push tooall Olá dispositivos de serviço que são registrados com o serviço de saudação. Um alerta aparecerá no painel de serviço hello. serviço Olá desabilitará todas as operações de Olá Olá registrado dispositivos e administrador do dispositivo hello, em seguida, será necessário chave de criptografia de dados tooupdate Olá serviço em Olá outros dispositivos. No entanto, hello e/SS (hosts que enviam dados na nuvem toohello) não serão interrompidas.
   
   Se você tiver um único dispositivo registrado tooyour serviço, o processo de substituição Olá agora está concluído e você pode ignorar Olá próxima etapa. Se você tiver vários serviços de tooyour registrados de dispositivos, vá toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Etapa 3: Atualize a chave de criptografia de dados de serviço de saudação em outros dispositivos de StorSimple
Essas etapas devem ser executadas na interface do Windows PowerShell de saudação do seu dispositivo StorSimple, se você tiver vários dispositivos registrados tooyour StorSimple Manager service. chave de saudação que você obteve na etapa 2: usar o Windows PowerShell para StorSimple tooinitiate Olá serviço criptografia chave alteração de dados deve ser usado tooupdate todos Olá restante do dispositivo StorSimple registrado com hello serviço StorSimple Manager.

Execute Olá criptografia de dados de serviço do etapas tooupdate Olá a seguir em seu dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chave de criptografia de dados de serviço do tooupdate Olá
1. Use o Windows PowerShell para StorSimple tooconnect toohello console. Selecione a opção 1 toolog com acesso completo.
2. No prompt de comando hello, digite:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Forneça Olá serviço dados chave de criptografia que você obteve na [etapa 2: usar o Windows PowerShell para StorSimple tooinitiate Olá serviço alteração criptografia de dados chave](#to-initiate-the-service-data-encryption-key-change).

