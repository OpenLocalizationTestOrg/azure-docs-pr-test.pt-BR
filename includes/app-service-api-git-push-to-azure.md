Use o URL de implantação remota do hello CLI do Azure tooget Olá para sua API App. Olá a seguir de comando, substitua  *\<app_name >* com o nome do seu aplicativo web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configure seu local Git implantação toobe toopush capaz de toohello remoto.

```bash
git remote add azure <URI from previous step>
```

Enviar seu aplicativo por push toohello toodeploy remoto do Azure. Você será solicitado para senha Olá criado anteriormente ao criar usuário de implantação de saudação. Certifique-se de que você criou anteriormente no início rápido de saudação de senha de Olá e Olá a senha não use toolog em toohello portal do Azure.

```bash
git push azure master
```
