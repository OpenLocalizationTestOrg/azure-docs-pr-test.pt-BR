## <a name="clean-up-deployment"></a><span data-ttu-id="31476-101">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="31476-101">Clean up deployment</span></span> 

<span data-ttu-id="31476-102">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos, instância do Cache Redis do Azure e todos os recursos relacionados no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="31476-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```