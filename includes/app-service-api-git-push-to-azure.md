<span data-ttu-id="120f2-101">Use o URL de implantação remota do hello CLI do Azure tooget Olá para sua API App.</span><span class="sxs-lookup"><span data-stu-id="120f2-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="120f2-102">Olá a seguir de comando, substitua  *\<app_name >* com o nome do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="120f2-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="120f2-103">Configure seu local Git implantação toobe toopush capaz de toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="120f2-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="120f2-104">Enviar seu aplicativo por push toohello toodeploy remoto do Azure.</span><span class="sxs-lookup"><span data-stu-id="120f2-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="120f2-105">Você será solicitado para senha Olá criado anteriormente ao criar usuário de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="120f2-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="120f2-106">Certifique-se de que você criou anteriormente no início rápido de saudação de senha de Olá e Olá a senha não use toolog em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="120f2-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
