<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>atualizações regulares de tooinstall por meio do Windows PowerShell para StorSimple
1. Abra o console serial do dispositivo hello e selecione a opção 1, **entrar com acesso completo**. Digite a senha de saudação. a senha padrão Olá é *Password1*. 
2. No prompt de comando hello, digite:
   
     `Get-HcsUpdateAvailability`
   
    Você será notificado se houver atualizações disponíveis e se as atualizações de saudação são interrompidas ou interrupções.
3. No prompt de comando hello, digite:
   
     `Start-HcsUpdate`
   
    processo de atualização de saudação será iniciado.

> [!IMPORTANT]
> * Esse comando se aplica apenas atualizações de tooregular. Executar esse comando em apenas um controlador, mas ambos os controladores serão atualizados. 
> * Você pode perceber um failover de controlador durante o processo de atualização de saudação; No entanto, Olá failover não afetará a disponibilidade do sistema ou a operação.
> 
> 

