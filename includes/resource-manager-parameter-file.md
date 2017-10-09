Se você usar um valores de parâmetro de toopass de arquivo de parâmetro durante a implantação, você precisa toocreate um arquivo JSON com um toohello semelhante formato exemplo a seguir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

tamanho de saudação do arquivo de parâmetro hello não pode ser mais de 64 KB.

Se você precisar tooprovide um valor confidencial para um parâmetro (como uma senha), adicione esse valor tooa chave de cofre. Recupere o Cofre de chaves Olá durante a implantação, conforme mostrado no exemplo anterior de saudação. Para obter mais informações, veja [Transmitir valores seguros durante a implantação](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

