#### <a name="toostop-and-start-a-virtual-device"></a>toostop e iniciar um dispositivo virtual
toostop um dispositivo virtual, clique em seu nome e, em seguida, clique em **desligamento**. Quando o dispositivo virtual hello está desligando, seu status é **parando**. Depois que o dispositivo virtual Olá for interrompido, seu status é **parado**.

Use Olá toostop cmdlets a seguir e inicie um dispositivo virtual.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart um dispositivo virtual
Quando um dispositivo virtual está em execução e você deseja toorestart-la, clique em seu nome e, em seguida, clique em **reiniciar**. Quando o dispositivo virtual hello está reiniciando, seu status é **reiniciando**. Quando o dispositivo virtual hello está pronto para você toouse, seu status é **executando**.

Use Olá cmdlet toorestart um dispositivo virtual a seguir.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

