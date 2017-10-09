<span data-ttu-id="96fa4-101">Você pode verificar se a conexão foi bem-sucedida usando o cmdlet Olá 'Get-AzureVNetConnection'.</span><span class="sxs-lookup"><span data-stu-id="96fa4-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="96fa4-102">Olá Use cmdlet de exemplo a seguir, a configuração Olá valores toomatch seus próprios.</span><span class="sxs-lookup"><span data-stu-id="96fa4-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="96fa4-103">nome de saudação da rede virtual Olá deve estar entre aspas se contiver espaços.</span><span class="sxs-lookup"><span data-stu-id="96fa4-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="96fa4-104">Após cmdlet hello, exiba os valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="96fa4-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="96fa4-105">O exemplo hello abaixo, mostra o estado de conectividade hello como 'Conectado' e você pode ver os bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="96fa4-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal