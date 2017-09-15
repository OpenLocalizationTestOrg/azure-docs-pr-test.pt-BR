### <a name="app-service-plan"></a><span data-ttu-id="e4957-101">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e4957-101">App Service plan</span></span>
<span data-ttu-id="e4957-102">Cria o plano de serviço para hospedar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e4957-102">Creates the service plan for hosting the web app.</span></span> <span data-ttu-id="e4957-103">Forneça o nome do plano por meio do parâmetro **hostingPlanName** .</span><span class="sxs-lookup"><span data-stu-id="e4957-103">You provide the name of the plan through the **hostingPlanName** parameter.</span></span> <span data-ttu-id="e4957-104">O local do plano é o mesmo usado para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e4957-104">The location of the plan is the same location used for the resource group.</span></span> <span data-ttu-id="e4957-105">O tipo de preços e o tamanho do trabalhador são especificados nos parâmetros **sku** e **workerSize**</span><span class="sxs-lookup"><span data-stu-id="e4957-105">The pricing tier and worker size are specified in the **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

