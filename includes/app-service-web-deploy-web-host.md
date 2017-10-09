### <a name="app-service-plan"></a><span data-ttu-id="28139-101">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="28139-101">App Service plan</span></span>
<span data-ttu-id="28139-102">Cria o plano do serviço Olá para hospedar o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="28139-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="28139-103">Fornecer nome Olá Olá plano por meio de saudação **hostingPlanName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="28139-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="28139-104">local de saudação do plano de saudação é hello mesmo local usado para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="28139-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="28139-105">tamanho preços Olá camada e de trabalho estão especificados na Olá **sku** e **workerSize** parâmetros</span><span class="sxs-lookup"><span data-stu-id="28139-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

