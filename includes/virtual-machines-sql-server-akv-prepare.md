## <a name="prepare-for-akv-integration"></a>Preparar-se para a integração de AKV
toouse tooconfigure de integração do Cofre de chave do Azure VM do SQL Server, existem vários pré-requisitos: 

1. [Instalar o Azure Powershell](#install-azure-powershell)
2. [Criar um Active Directory do Azure](#create-an-azure-active-directory)
3. [Criar um cofre de chave](#create-a-key-vault)

Olá seções a seguir descrevem esses pré-requisitos e as informações de saudação precisar cmdlets do PowerShell toocollect toolater executar hello.

### <a name="install-azure-powershell"></a>Instalar o Azure Powershell
Verifique se você instalou Olá SDK mais recente do PowerShell do Azure. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Criar um Active Directory do Azure
Primeiro, é necessário toohave um [Active Directory do Azure](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) em sua assinatura. Entre muitos benefícios, isso permite que você toogrant permissão tooyour Cofre de chaves para determinados aplicativos e usuários.

Em seguida, registre um aplicativo com o AAD Isso lhe dará uma conta de entidade de serviço que tenha acesso tooyour Cofre de chaves que a VM será necessário. Artigo de Cofre de chaves do Azure hello, você pode encontrar estas etapas no hello [registrar um aplicativo com o Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) seção, ou você pode ver as etapas de saudação com capturas de tela hello **obter uma identidade para o aplicativo hello seção** de [esta postagem de blog](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Antes de concluir essas etapas, observe que você precisa Olá toocollect informações durante o registro que é necessário mais tarde, quando você habilitar a integração do cofre da chave do Azure em sua VM do SQL a seguir.

* Depois que o aplicativo hello é adicionado, localize Olá **ID do cliente** em Olá **configurar** guia.   ![ID de cliente do Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    ID de saudação do cliente é atribuído posterior toohello **$spName** parâmetro (nome da entidade de serviço) em Olá PowerShell script tooenable integração do cofre da chave do Azure. 
* Além disso, durante essas etapas quando você cria sua chave, o copie o segredo Olá para sua chave como é mostrado Olá captura de tela a seguir. Essa chave secreta é atribuída posterior toohello **$spSecret** parâmetro (entidade de serviço secreto) no script do PowerShell hello.  
    ![Segredo do Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* É necessário autorizar este novo saudação de toohave de ID de cliente as seguintes permissões de acesso: **criptografar**, **descriptografar**, **wrapKey**, **unwrapKey**, **sinal**, e **verificar**. Isso é feito com hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. Para obter mais informações, consulte [autorizar Olá aplicativo toouse Olá chave ou segredo](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Criar um cofre de chave
Em ordem toouse Azure Key Vault toostore Olá chaves que será usado para criptografia na sua VM, você precisa de Cofre de chaves de tooa de acesso. Se você ainda não definiu o seu Cofre de chaves, crie um seguindo as etapas Olá Olá [guia de Introdução ao Azure Key Vault](../articles/key-vault/key-vault-get-started.md) tópico. Antes de concluir essas etapas, observe que há algumas informações necessárias toocollect durante esse conjunto de backup que é necessário mais tarde, quando você habilitar a integração do cofre da chave do Azure em sua VM do SQL.

Quando você obter toohello criar uma etapa de Cofre de chaves, Olá Observação retornado **vaultUri** propriedade, que é a URL do Cofre de chaves de saudação. No exemplo hello fornecido na etapa, mostrada abaixo, nome do Cofre de chaves de saudação é ContosoKeyVault, portanto, a URL de Cofre de chaves de saudação seria https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

URL de Cofre de chaves Olá recebe toohello posterior **$akvURL** parâmetro hello PowerShell script tooenable integração do cofre da chave do Azure.

