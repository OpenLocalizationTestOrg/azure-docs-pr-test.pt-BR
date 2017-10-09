Antes de começar essa configuração, você deve fazer logon no tooyour conta do Azure. Olá cmdlet solicita as credenciais de logon de saudação para sua conta do Azure. Após o logon, ele baixa as configurações de conta para que eles fiquem disponível tooAzure PowerShell. Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../articles/powershell-azure-resource-manager.md).

toolog, abra o console do PowerShell com privilégios elevados e conectar-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

```powershell
Login-AzureRmAccount
```

Se você tiver várias assinaturas do Azure, verificar as assinaturas de saudação para conta de saudação.

```powershell
Get-AzureRmSubscription
```

Especifique que você deseja toouse de assinatura de saudação.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```