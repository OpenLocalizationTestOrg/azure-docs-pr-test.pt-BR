1. Copie Olá instalador tooa pasta local (por exemplo, /tmp) no servidor de saudação que você deseja tooprotect. Em um terminal, execute Olá comandos a seguir:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall serviço de mobilidade, executar Olá comando a seguir:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Após a conclusão da instalação, Olá serviço de mobilidade precisa de servidor de configuração tooget toohello registrado. Execute Olá Olá tooregister de comando, serviço de mobilidade com o servidor de configuração a seguir.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Linha de comando do instalador do Serviço de Mobilidade

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|-r |Obrigatório|Especifica se o Serviço de Mobilidade (MS) deve ser instalado ou se o MasterTarget (MT) deve ser instalado|MS </br> MT|
|-d |Opcional|Local onde o Serviço de Mobilidade será instalado|/usr/local/ASR|
|-v|Obrigatório|Especifica a plataforma de saudação em qual Olá serviço de mobilidade está obtendo instalado </br> </br>- **VMware** : use esse valor se você estiver instalando o serviço de mobilidade em uma VM em execução no *Hosts do VMware vSphere ESXi*, *Hosts do Hyper-V* e *Servidores Físicos* </br> - **Azure** : use esse valor se você estiver instalando o agente em uma VM IaaS do Azure| VMware </br> As tabelas|
|-q|Opcional|Especifica o instalador toorun no modo silencioso| N/D|


#### <a name="mobility-service-configuration-command-line"></a>Linha de comando de configuração do Serviço de Mobilidade

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parâmetro|Tipo|Descrição|Valores possíveis|
|-|-|-|-|
|-i |Obrigatório|Olá, servidor de configuração de IP|Qualquer endereço IP válido|
|-P |Obrigatório|Arquivo de Olá do caminho completo do arquivo onde a senha de conexão de saudação é salvo|Qualquer pasta válida|
