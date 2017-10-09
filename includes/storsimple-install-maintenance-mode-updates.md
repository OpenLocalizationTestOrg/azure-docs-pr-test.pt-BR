<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>atualizações do modo de manutenção tooinstall por meio do Windows PowerShell para StorSimple
1. Se você ainda não tiver feito isso, acesse o console serial do dispositivo hello e selecione a opção 1, **entrar com acesso completo**. 
2. Digite a senha de saudação. a senha padrão Olá é **Password1**.
3. No prompt de comando hello, digite:
   
     `Get-HcsUpdateAvailability` 
4. Você será notificado se houver atualizações disponíveis e se as atualizações de saudação são interrompidas ou interrupções. atualizações de interrupção tooapply, é necessário que tooput Olá dispositivo no modo de manutenção. Consulte [Etapa 2: Entrar no modo de manutenção](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções.
5. Quando o dispositivo está em modo de manutenção, no prompt de comando hello, digite:`Start-HcsUpdate`
6. Será solicitada a sua confirmação. Depois de confirmar atualizações hello, eles serão instalados no controlador de saudação que você está acessando. Após Olá atualizações são instaladas, controlador Olá será reiniciado. 
7. Monitorar o status de saudação de atualizações. Tipo:
   
    `Get-HcsUpdateStatus`
   
    Se hello `RunInProgress` é `True`, atualização Olá ainda está em andamento. Se `RunInProgress` é `False`, ele indica que a atualização Olá foi concluída.  
8. Quando Olá atualização está instalada no controlador atual hello e for reiniciado, conecte-se toohello outro controlador e execute as etapas 1 a 6.
9. Depois que ambos os controladores estiverem atualizados, saia do modo de Manutenção. Veja a [Etapa 4: Sair do modo de manutenção](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.

