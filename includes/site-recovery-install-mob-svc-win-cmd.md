1. Copie a pasta local de tooa instalador da saudação (por exemplo, C:\Temp) no servidor de saudação que você deseja tooprotect. Execute Olá comandos a seguir como um administrador em um prompt de comando:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall serviço de mobilidade, executar Olá comando a seguir:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Agente Olá deve toobe registrado com hello servidor de configuração.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Argumentos de linha de comando do instalador do Serviço de Mobilidade

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|/Role|Obrigatório|Especifica se o Serviço de Mobilidade (MS) deve ser instalado ou se o MasterTarget (MT) deve ser instalado|MS </br> MT|
|/InstallLocation|Opcional|Local onde o Serviço de Mobilidade está instalado|Qualquer pasta no computador de saudação|
|/Platform|Obrigatório|Especifica a plataforma de saudação em qual Olá serviço de mobilidade está obtendo instalado </br> </br>- **VMware** : use esse valor se você estiver instalando o serviço de mobilidade em uma VM em execução no *Hosts do VMware vSphere ESXi*, *Hosts do Hyper-V* e *Servidores Físicos* </br> - **Azure** : use esse valor se você estiver instalando o agente em uma VM IaaS do Azure| VMware </br> As tabelas|
|/Silent|Opcional|Especifica o instalador de saudação toorun no modo silencioso| ND|

>[!TIP]
> Olá logs de instalação podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argumentos da linha de comando de registro do Serviço de Mobilidade

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parâmetro|Tipo|Descrição|Valores possíveis|
  |-|-|-|-|
  |/CSEndPoint |Obrigatório|Endereço IP do servidor de configuração de saudação| Qualquer endereço IP válido|
  |/PassphraseFilePath|Obrigatório|Local de senha Olá |Qualquer caminho de arquivo UNC ou local válido|


>[!TIP]
> Olá AgentConfiguration logs podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
