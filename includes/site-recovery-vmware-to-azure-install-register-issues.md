
### <a name="installation-failures"></a>Falhas de instalação
| **Mensagem de erro de exemplo** | **Ação recomendada** |
|--------------------------|------------------------|
|Erro Falha tooload contas. Erro: System.IO. IOException: não é possível tooread dados de saudação conexão de transporte ao instalar e registrar Olá Hyper-v.| Certifique-se de que o protocolo TLS 1.0 está habilitado no computador de saudação. |

### <a name="registration-failures"></a>Falhas de registro
Falhas de registro podem ser depuradas por revisar os logs de saudação em Olá **%ProgramData%\ASRLogs** pasta.

| **Mensagem de erro de exemplo** | **Ação recomendada** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Mensagem: ACS50008: token SAML é inválido.<br>ID de rastreamento: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>ID de correlação: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>Carimbo de data/hora: **2016-12-12 14:50:08Z<br>** | Certifique-se de que o tempo de saudação no relógio do sistema não é mais de 15 minutos Olá local tempo. Execute novamente o registro de Olá Olá instalador toocomplete.|
|**35:09:27** : DRRegistrationException durante a tentativa de tooget todos os Cofre de recuperação de desastres para o certificado selecionado Olá:: Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException gerou, Exception.Message: ACS50008: Token SAML é inválido.<br>ID de rastreamento: e5ad1af1-2d39-4970-8eef-096e325c9950<br>ID de correlação: abe9deb8-3e64-464d-8375-36db9816427a<br>Carimbo de data/hora: **2016-05-19 01:35:39Z**<br> | Certifique-se de que o tempo de saudação no relógio do sistema não é mais de 15 minutos Olá local tempo. Execute novamente o registro de Olá Olá instalador toocomplete.|
|06:28:45: certificado toocreate com falha<br>06:28:45: A instalação não pode continuar. Um certificado necessário tooSite tooauthenticate que recuperação não pode ser criada. Executar a instalação novamente | Verifique se você está executando a instalação como um administrador local. |
