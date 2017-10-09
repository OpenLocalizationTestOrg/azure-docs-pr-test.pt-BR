<span data-ttu-id="b15a8-101">Se você usar um valores de parâmetro de toopass de arquivo de parâmetro durante a implantação, você precisa toocreate um arquivo JSON com um toohello semelhante formato exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b15a8-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="b15a8-102">tamanho de saudação do arquivo de parâmetro hello não pode ser mais de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b15a8-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="b15a8-103">Se você precisar tooprovide um valor confidencial para um parâmetro (como uma senha), adicione esse valor tooa chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="b15a8-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="b15a8-104">Recupere o Cofre de chaves Olá durante a implantação, conforme mostrado no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="b15a8-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="b15a8-105">Para obter mais informações, veja [Transmitir valores seguros durante a implantação](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="b15a8-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

