Você pode verificar se a conexão foi bem-sucedida usando o cmdlet de saudação 'Get-AzureRmVirtualNetworkGatewayConnection', com ou sem o '-Debug'. 

1. Olá Use cmdlet de exemplo a seguir, a configuração Olá valores toomatch seus próprios. Se solicitado, selecione 'A' em ordem toorun 'Todos'. No exemplo hello, '-nome ' refere-se o nome de toohello de conexão de saudação que você deseja tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Após cmdlet hello, exiba os valores de saudação. O exemplo hello abaixo, o status de conexão de Olá mostra como 'Conectado' e você pode ver os bytes de entrada e saída.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```