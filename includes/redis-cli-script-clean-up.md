## <a name="clean-up-deployment"></a><span data-ttu-id="2f9ad-101">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2f9ad-101">Clean up deployment</span></span> 

<span data-ttu-id="2f9ad-102">Após a execução do exemplo de script hello, Olá siga comando pode ser usado tooremove grupo de recursos de saudação, instância de Cache Redis do Azure e os recursos relacionados no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f9ad-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```