## <a name="set-up-azure-cli-for-azure-dns"></a>Configurar a CLI do Azure para DNS do Azure

### <a name="before-you-begin"></a>Antes de começar

Verifique se você tem Olá itens a seguir antes de começar a configuração.

* Uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale a versão mais recente Olá de saudação CLI do Azure, disponível para Windows, Linux ou Mac. Mais informações estão disponíveis em [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Entrar tooyour conta do Azure

Abra uma janela do console e autentique com suas credenciais. Para obter mais informações, consulte [login tooAzure de saudação CLI do Azure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Mudar para o modo CLI

O DNS do Azure usa o Azure Resource Manager. Verifique se que você alternar comandos modo toouse Gerenciador de recursos do Azure.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Selecione a assinatura de saudação

Verificar as assinaturas de saudação para conta de saudação.

```azurecli
azure account list
```

Escolha qual toouse suas assinaturas do Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Gerenciador de Recursos do Azure requer que todos os grupos de recursos especifiquem um local. Isso é usado como o local padrão de saudação para recursos desse grupo de recursos. No entanto, como todos os recursos DNS são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto no DNS do Azure.

Você pode ignorar esta etapa se está usando um grupo de recursos existente.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Registrar provedor de recursos

Olá serviço DNS do Azure é gerenciado pelo provedor de recursos Microsoft. Network hello. Sua assinatura do Azure deve ser registrado toouse este provedor de recursos antes de usar o DNS do Azure. Essa operação deve ser executa apenas uma vez para cada assinatura.

```azurecli
azure provider register --namespace Microsoft.Network
```

