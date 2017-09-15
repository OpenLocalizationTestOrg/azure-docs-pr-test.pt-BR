<span data-ttu-id="e2786-101">Você pode verificar se a conexão foi bem-sucedida usando o cmdlet "Get-AzureVNetConnection".</span><span class="sxs-lookup"><span data-stu-id="e2786-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="e2786-102">Use o seguinte exemplo de cmdlet, configurando os valores para coincidirem com os seus.</span><span class="sxs-lookup"><span data-stu-id="e2786-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="e2786-103">O nome da rede virtual deve ficar entre aspas se contiver espaços.</span><span class="sxs-lookup"><span data-stu-id="e2786-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="e2786-104">Após o cmdlet ter sido concluído, exiba os valores.</span><span class="sxs-lookup"><span data-stu-id="e2786-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="e2786-105">No exemplo abaixo, o Estado de Conectividade é exibido como ‘Conectado’ e é possível ver os bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="e2786-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal