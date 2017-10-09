#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop e iniciar um dispositivo de nuvem

1. toostop um dispositivo de nuvem, vá toohello VM para sua solução de nuvem.
    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Na barra de comandos de saudação, clique em **parar**.

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Quando solicitado a confirmar, clique em **Sim**.

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Quando você para uma VM, ela é desalocada. Quando o dispositivo de nuvem hello está parando, seu status é **Deallocating**. Depois que o dispositivo de nuvem Olá é interrompido, seu status é **parado (desalocado)**.

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Depois que uma VM for interrompida, clique em **iniciar** (botão fica disponível) toostart Olá VM. Depois que o dispositivo de nuvem Olá tenha sido iniciado, seu status é **iniciado**.

    ![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Use Olá toostop cmdlets a seguir e iniciar um dispositivo de nuvem.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart um dispositivo de nuvem

toorestart um dispositivo de nuvem, vá toohello VM para sua solução de nuvem. Na barra de comandos de saudação, clique em **reiniciar**. Quando solicitado, confirme Olá reinicialização. Quando o dispositivo de nuvem hello está pronto para você toouse, seu status é **executando**.

![Máquina virtual do Dispositivo de nuvem StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Use Olá cmdlet toorestart um dispositivo de nuvem a seguir.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

