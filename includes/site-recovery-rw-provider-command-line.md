UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ Unidade_de_instalação <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe de endereço IP usado para transferência de dados] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parâmetros:

* /ServerMode: obrigatório. Especifica se devem ser instalados de ambos os servidores de configuração e o processo de saudação ou apenas o servidor do processo hello. Valores de entrada: CS, PS.
* InstallLocation: obrigatório. pasta Olá quais Olá componentes são instalados.
* /MySQLCredsFilePath. Obrigatório. caminho do arquivo Hello no qual Olá MySQL credenciais do servidor são armazenadas. Olá arquivo deve estar neste formato:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Obrigatório. local de saudação do arquivo de credenciais de cofre Olá
* /EnvType. Obrigatório. tipo de saudação da instalação. Valores: VMware, NonVMware
* /PSIP e /CSIP. Obrigatório. endereço IP de saudação do servidor de processo hello e o servidor de configuração.
* /PassphraseFilePath. Obrigatório. local de saudação do arquivo de senha de saudação.
* /BypassProxy. Opcional. Especifica que se o servidor configuração Olá conecta tooAzure sem um proxy.
* /ProxySettingsFilePath. Opcional. Configurações de proxy (proxy de padrão de saudação requer autenticação, ou um proxy personalizado). Olá arquivo deve estar neste formato:
* [ProxySettings]
* ProxyAuthentication = "Sim/Não"
* IP do Proxy = "Endereço IP>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. Opcional. número da porta Olá para replicação de dados.
* SkipSpaceCheck. Opcional. Ignorar verificação para o cache do espaço.
* AcceptThirdpartyEULA. Obrigatório. Aceita o EULA de terceiros hello.
* ShowThirdpartyEULA. Obrigatório. Exibe o EULA de terceiros. Se fornecido como entrada, todos os outros parâmetros serão ignorados.
