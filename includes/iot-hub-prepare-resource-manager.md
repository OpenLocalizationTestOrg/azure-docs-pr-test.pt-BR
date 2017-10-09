## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Preparar tooauthenticate solicitações do Gerenciador de recursos do Azure
Você deve autenticar todas as operações de saudação que podem ser executadas em recursos usando Olá [do Azure Resource Manager] [ lnk-authenticate-arm] com o Azure AD (Active Directory). Olá tooconfigure de maneira mais fácil é toouse PowerShell ou CLI do Azure.

Instalar Olá [cmdlets do PowerShell do Azure] [ lnk-powershell-install] antes de continuar.

Olá mostram as etapas a seguir como tooset a autenticação de senha para um aplicativo do AD usando o PowerShell. Você pode executar esses comandos em uma sessão do PowerShell padrão.

1. Faça logon no tooyour assinatura do Azure usando Olá comando a seguir:

    ```powershell
    Login-AzureRmAccount
    ```

1. Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais. Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:

    ```powershell
    Get-AzureRMSubscription
    ```

    Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toomanage seu hub IoT a seguir. Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Anote seu **TenantId** e **SubscriptionId**. Você precisará dessa informação mais tarde.
3. Crie um novo aplicativo do Active Directory do Azure usando Olá comando a seguir, substituindo espaços reservados de saudação:
   
   * **{Display name}:** um nome de exibição para seu aplicativo, como **MySampleApp**
   * **{URL da Home page}:** Olá URL da página inicial de saudação do seu aplicativo, como **http://mysampleapp/home**. Essa URL não precisa de aplicativo real do toopoint tooa.
   * **{Application identifier}:** um identificador exclusivo, como **http://mysampleapp**. Essa URL não precisa de aplicativo real do toopoint tooa.
   * **{Password}:** uma senha que você use tooauthenticate com seu aplicativo.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Anote Olá **ApplicationId** do aplicativo hello criado por você. Você precisa dessa informação mais tarde.
5. Criar uma nova entidade de serviço usando Olá comando a seguir, substituindo **{MyApplicationId}** com hello **ApplicationId** da etapa anterior hello:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configurar uma atribuição de função usando Olá comando a seguir, substituindo **{MyApplicationId}** com seus **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Agora terminar de criar o aplicativo do AD do Azure hello que permite que você tooauthenticate do seu aplicativo c# personalizado. Você precisa Olá seguinte valores posteriormente neste tutorial:

* TenantId
* SubscriptionId
* ApplicationId
* Senha

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
