Você pode verificar se a conexão foi bem-sucedida usando o cmdlet Olá 'Get-AzureVNetConnection'.

1. Olá Use cmdlet de exemplo a seguir, a configuração Olá valores toomatch seus próprios. nome de saudação da rede virtual Olá deve estar entre aspas se contiver espaços.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Após cmdlet hello, exiba os valores de saudação. O exemplo hello abaixo, mostra o estado de conectividade hello como 'Conectado' e você pode ver os bytes de entrada e saída.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal