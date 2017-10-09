### <a name="app-service-plan"></a>Plano do Serviço de Aplicativo
Cria o plano do serviço Olá para hospedar o aplicativo web de saudação. Fornecer nome Olá Olá plano por meio de saudação **hostingPlanName** parâmetro. local de saudação do plano de saudação é hello mesmo local usado para o grupo de recursos de saudação. tamanho preços Olá camada e de trabalho estão especificados na Olá **sku** e **workerSize** parâmetros

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

