### <a name="troubleshoot-azure-diagnostics"></a>Solucionar problemas de diagnóstico do Azure

Se você receber a seguinte mensagem de erro de saudação, o provedor de recursos do hello Insights não está registrado:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

provedor de recursos do tooregister hello, executar Olá etapas Olá portal do Azure:

1.  No painel de navegação Olá Olá esquerda, clique em *assinaturas*
2.  Selecionar assinatura Olá identificada na mensagem de saudação do erro
3.  Clique em *Provedores de Recursos*
4.  Localize Olá *Insights* provedor
5.  Clique em Olá *registrar* link

![Registrar o provedor de recursos microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Uma vez Olá *Insights* provedor de recursos está registrado, tente novamente a configuração de diagnóstico.


No PowerShell, se você receber Olá a seguinte mensagem de erro, será necessário tooupdate sua versão do PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Atualize sua versão do PowerShell toohello novembro de 2016 (v2.3.0) ou versão posterior, usando instruções Olá Olá [Introdução aos cmdlets do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artigo.
