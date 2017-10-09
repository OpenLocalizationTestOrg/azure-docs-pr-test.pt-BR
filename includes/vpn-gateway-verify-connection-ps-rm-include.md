<span data-ttu-id="92b93-101">Você pode verificar se a conexão foi bem-sucedida usando o cmdlet de saudação 'Get-AzureRmVirtualNetworkGatewayConnection', com ou sem o '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="92b93-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="92b93-102">Olá Use cmdlet de exemplo a seguir, a configuração Olá valores toomatch seus próprios.</span><span class="sxs-lookup"><span data-stu-id="92b93-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="92b93-103">Se solicitado, selecione 'A' em ordem toorun 'Todos'.</span><span class="sxs-lookup"><span data-stu-id="92b93-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="92b93-104">No exemplo hello, '-nome ' refere-se o nome de toohello de conexão de saudação que você deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="92b93-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="92b93-105">Após cmdlet hello, exiba os valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="92b93-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="92b93-106">O exemplo hello abaixo, o status de conexão de Olá mostra como 'Conectado' e você pode ver os bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="92b93-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```