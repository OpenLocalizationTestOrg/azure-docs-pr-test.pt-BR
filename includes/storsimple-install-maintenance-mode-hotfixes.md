<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall hotfixes do modo de manutenção por meio do Windows PowerShell para StorSimple
> [!IMPORTANT]
> No modo de manutenção, precisa tooapply Olá hotfix primeiro em um controlador e, em seguida, em Olá outro controlador.
> 
> 

1. Coloque o dispositivo de saudação em modo de manutenção. Consulte [etapa 2: modo de manutenção insira](../articles/storsimple/storsimple-update-device.md#step2) para obter instruções sobre como o modo de manutenção tooenter.
2. tooapply Olá hotfix, tipo:
   
     `Start-HcsHotfix` 
3. Quando solicitado, forneça Olá caminho toohello pasta de rede compartilhada que contém os arquivos de hotfix hello.
4. Será solicitada a sua confirmação. Tipo **Y** tooproceed com a instalação do hotfix hello.
5. Após ter aplicado Olá hotfix em um controlador, logon toohello outro controlador. Aplique o hotfix de saudação de controlador de saudação anterior.
6. Após Olá hotfixes forem aplicados, saia do modo de manutenção. Veja a [Etapa 4: Sair do modo de manutenção](../articles/storsimple/storsimple-update-device.md#step4) para obter instruções.

