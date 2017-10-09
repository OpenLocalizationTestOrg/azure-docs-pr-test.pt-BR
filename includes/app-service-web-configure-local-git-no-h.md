Configurar o aplicativo web local Git implantação toohello com hello [origem de implantação de aplicativo Web do az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.

Serviço de aplicativo oferece suporte a várias maneiras toodeploy tooa conteúdo aplicativo web, como FTP, Git local, GitHub, Visual Studio Team Services e Bitbucket. Para este início rápido, implante usando o Git local. Isso significa que você implantar usando um toopush de comando Git de um repositório de tooa repositório local no Azure. 

Olá a seguir de comando, substitua  *\<app_name >* com o nome do seu aplicativo web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

saída de Hello tem Olá formato a seguir:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Olá `<username>` é hello [usuário de implantação](#configure-a-deployment-user) que você criou na etapa anterior.

Copiar Olá URI mostrada; Você vai usá-lo na próxima etapa do hello.
