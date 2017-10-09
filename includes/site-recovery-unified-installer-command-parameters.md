|Nome do Parâmetro| Tipo | Descrição| Valores possíveis|
|-|-|-|-|
| /ServerMode|Obrigatório|Especifica se devem ser instalados de ambos os servidores de configuração e o processo de saudação ou apenas o servidor do processo Olá|CS<br>PS|
|/InstallLocation|Obrigatório|pasta Olá quais Olá componentes são instalados| Qualquer pasta no computador de saudação|
|/MySQLCredsFilePath|Obrigatório|caminho do arquivo Hello no qual Olá MySQL credenciais de servidor são armazenadas|arquivo Hello deve estar no formato Olá especificado abaixo|
|/VaultCredsFilePath|Obrigatório|caminho de saudação do arquivo de credenciais de cofre Olá|Caminho de arquivo válido|
|/EnvType|Obrigatório|Tipo de ambiente que você deseja tooprotect |VMware<br>NonVMware|
|/PSIP|Obrigatório|Endereço IP do hello NIC toobe usado para transferir dados de replicação| Qualquer endereço IP válido|
|/CSIP|Obrigatório|endereço IP de saudação da NIC de saudação na qual Olá servidor de configuração está escutando em| Qualquer endereço IP válido|
|/PassphraseFilePath|Obrigatório|Olá toolocation de caminho completo do arquivo de senha Olá|Caminho de arquivo válido|
|/BypassProxy|Opcional|Especifica que se o servidor configuração Olá se conecta tooAzure sem um proxy|toodo obter esse valor de Venu|
|/ProxySettingsFilePath|Opcional|Configurações de proxy (proxy de padrão de saudação requer autenticação, ou um proxy personalizado)|arquivo Hello deve estar no formato de saudação especificado abaixo|
|DataTransferSecurePort|Opcional|Número da porta em Olá PSIP toobe usado para replicação de dados| Número da porta válido (o valor padrão é 9433)|
|/SkipSpaceCheck|Opcional|Ignorar verificação de espaço do disco de cache| |
|/AcceptThirdpartyEULA|Obrigatório|Sinalizar implica na aceitação do EULA de terceiros| |
|/ShowThirdpartyEULA|Opcional|Exibe o EULA de terceiros. Se fornecido como entrada, todos os outros parâmetros serão ignorados| |
