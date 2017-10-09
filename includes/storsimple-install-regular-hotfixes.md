<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>hotfixes regulares de tooinstall por meio do Windows PowerShell para StorSimple
1. Conecte-se toohello console serial do dispositivo. Para obter mais informações, consulte [etapa 1: conectar-se o console serial toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. No menu do console serial hello, selecione a opção 1, **entrar com acesso completo**. Digite a senha de saudação. a senha padrão Olá é **Password1**.
3. No prompt de comando hello, digite:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Esse comando se aplica somente tooregular hotfixes. Executar esse comando em apenas um controlador, mas ambos os controladores serão atualizados.
    > Você pode perceber um failover de controlador durante o processo de atualização de saudação; No entanto, Olá failover não afetará a disponibilidade do sistema ou a operação.

4. Quando solicitado, forneça Olá caminho toohello pasta de rede compartilhada que contém os arquivos de hotfix hello.
5. Será solicitada a sua confirmação. Tipo **Y** tooproceed com a instalação do hotfix hello.

