---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Conecte-se a sua tooLog de computadores Linux análise
Usando o Log Analytics, você pode coletar os dados gerados em computadores Linux e tomar ações em relação a eles. Adicionar dados coletados do Linux tooOMS permite que você toomanage os sistemas Linux e soluções de contêiner como o Docker, independentemente de onde se encontram os computadores – praticamente em qualquer lugar. Fontes de dados podem residir em seu datacenter local como servidores físicos, os computadores virtuais em um serviço de nuvem hospedados como serviços AWS (Amazon Web) ou o Microsoft Azure, ou mesmo Olá laptop em sua mesa. Além disso, o OMS também coleta dados de computadores Windows da mesma forma e, portanto, oferece suporte a um ambiente de TI verdadeiramente híbrido.

Você pode exibir e gerenciar dados de todas essas fontes com o Log Analytics no OMS com um único portal de gerenciamento. Isso reduz a necessidade de saudação toomonitor usando vários sistemas diferentes, torna mais fácil tooconsume, e você pode exportar os dados que você deseja toowhatever solução de análise de negócios ou sistema que você já tiver.

Este artigo é um guia de início rápido que ajudarão você a coletar e gerenciar dados de seus computadores Linux usando Olá agente do OMS para Linux. Para obter mais detalhes técnicos, como a configuração do servidor proxy, informações sobre as métricas do CollectD e fontes de dados JSON personalizadas, acesse a [Visão geral do Agente OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) e a [Documentação completa do Agente OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) no GitHub.

No momento, você pode coletar Olá seguintes tipos de dados de computadores Linux:

* Métricas de desempenho
* Eventos de syslog
* Alertas do Nagios e do Zabbix
* Logs, inventário e métricas de desempenho do contêiner Docker

## <a name="supported-linux-versions"></a>Versões do Linux com suporte
As versões x86 e x64 têm suporte oficial em uma variedade de distribuições do Linux. No entanto, a saudação do agente do OMS para Linux também pode ser executado em outras distribuições não listadas.

* Amazon Linux 2012.09 a 2015.09
* CentOS Linux 5, 6 e 7
* Oracle Linux 5, 6 e 7
* Red Hat Enterprise Linux Server 5, 6 e 7
* Debian GNU/Linux 6, 7 e 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 e 12

## <a name="oms-agent-for-linux"></a>Agente do OMS para Linux
Olá agente do Operations Management Suite para Linux consiste em vários pacotes. versão de arquivo Hello contém Olá pacotes, disponíveis com o pacote de shell Olá em execução com a seguir `--extract`.

| **Pacote** | **Versão** | **Descrição** |
| --- | --- | --- |
| omsagent |1.1.0 |Olá agente do Operations Management Suite para Linux |
| omsconfig |1.1.1 |Agente de configuração para Olá agente do OMS |
| omi |1.0.8.3 |OMI (Open Management Infrastructure) – um servidor CIM leve |
| scx |1.6.2 |Provedores de CIM OMI para métricas de desempenho do sistema operacional |
| apache-cimprov |1.0.0 |Provedor de monitoramento de desempenho do Servidor HTTP Apache para OMI. Instalado somente se o Servidor HTTP Apache for detectado. |
| mysql-cimprov |1.0.0 |Provedor de monitoramento de desempenho do Servidor MySQL para OMI. Instalado somente se o servidor MySQL/MariaDB for detectado. |
| docker-cimprov |0.1.0 |Provedor do Docker para OMI. Instalado somente se o Docker for detectado. |

### <a name="additional-installation-artifacts"></a>Artefatos adicionais de instalação
Depois de instalar o agente do OMS Olá para pacotes Linux, hello seguintes alterações de configuração de todo o sistema adicionais são aplicadas. Esses artefatos são removidos quando o pacote do hello omsagent é desinstalado.

* Um usuário sem privilégios chamado: `omsagent` é criado. Isso é Olá conta Olá omsagent daemon executa como
* Um "inclusão" sudoers é criado em /etc/sudoers.d/omsagent. Isso autoriza o omsagent toorestart Olá syslog e omsagent daemons. Se as diretivas de "inclusão" do sudo não tiverem suporte na versão Olá instalada do sudo, essas entradas serão gravadas muito/etc/sudoers.
* configuração de syslog Olá é modificado tooforward um subconjunto do agente de toohello de eventos. Para obter mais informações, consulte Olá **configurar coleta de dados** seção abaixo

### <a name="linux-data-collection-details"></a>Detalhes da coleta de dados do Linux
Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados.

| fonte | Agente Direct | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minuto |
| Nagios |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |na chegada |
| syslog |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |do armazenamento do Azure: 10 minutos; do agente: na chegada |
| Contadores de desempenho do Linux |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |Como agendado, mínimo de 10 segundos |
| controle de alterações |![Sim](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Não](./media/log-analytics-linux-agents/oms-bullet-red.png) |por hora |

### <a name="package-requirements"></a>Requisitos de pacote
| **Pacote necessário** | **Descrição** | **Versão mínima** |
| --- | --- | --- |
| Glibc |Biblioteca GNU C |2.5-12 |
| Openssl |Bibliotecas OpenSSL |0.9.8e ou 1.0 |
| Curl |cliente Web cURL |7.15.5 |
| Python-ctypes |bibliotecas de função |n/d |
| PAM |Módulos de autenticação conectáveis |n/d |

> [!NOTE]
> O rsyslog ou syslog-ng é necessário toocollect mensagens de syslog. Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog. toocollect dados de syslog dessa versão de distribuições, Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog.
>
>

## <a name="quick-install"></a>Instalação rápida
Olá comandos toodownload Olá omsagent a seguir é executado, validar a soma de verificação Olá, em seguida, instalar e agente Olá integrado. Os comandos são para a versão de 64 bits. Olá ID do espaço de trabalho e chave primária são encontradas no portal do OMS Olá em **configurações** em Olá **fontes conectadas** guia.

![detalhes do espaço de trabalho](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Há uma variedade de outros métodos tooinstall Olá agente e atualizá-lo. Você pode ler mais sobre eles em [Olá tooinstall de etapas do agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Você também pode exibir uma saudação [orientação em vídeo do Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Escolha o método de coleta de dados do Linux
A escolha Olá tipos de dados que seria como toocollect depende se você deseja que o portal do OMS Olá toouse ou se quer editar vários arquivos de configuração diretamente nos clientes Linux. Se você escolher o portal de saudação toouse, configuração de saudação é enviada tooall clientes Linux automaticamente. Se você precisar de configurações diferentes para diferentes clientes Linux, será necessário tooedit arquivos de cliente individualmente – ou usar uma alternativa como PowerShell DSC, Chef ou Puppet.

Você pode especificar os eventos de syslog hello e contadores de desempenho que você deseja toocollect usando arquivos de configuração em computadores Linux de saudação. *Se você escolheu tooconfigure a coleta de dados editando arquivos de configuração do agente, você deve desabilitar a configuração de centralizado de saudação.*  As instruções são fornecidas abaixo de coleta de dados tooconfigure do agente Olá arquivos de configuração, bem como toodisable configuração central para todos os agentes do OMS para Linux ou computadores individuais.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Desabilitar o gerenciamento do OMS para um computador Linux individual
Coleta de dados centralizado para dados de configuração é desabilitada para um computador Linux individual com hello script OMS_MetaConfigHelper.py. Isso poderá ser útil se um subconjunto de computadores tiver uma configuração especializada.

configuração centralizada de toodisable:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Habilitar toore de configuração centralizada:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Contadores de desempenho do Linux
Contadores de desempenho de Linux são semelhantes contadores de desempenho de tooWindows – ambos operam da mesma forma. Você pode usar o hello tooadd procedimentos a seguir e configurá-los. Depois de serem adicionados tooOMS, dados são coletados da cada 30 segundos.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd um contador de desempenho do Linux no OMS
1. tooconfigure agentes do OMS para Linux usando o portal do OMS hello, você pode adicionar contadores de desempenho do Linux na página de configurações de saudação, clique em **dados**.  
2. Em Olá **configurações** página em **dados** , clique em **contadores de desempenho de Linux** e o nome de hello, em seguida, selecionar ou tipo de contador de saudação que você deseja tooadd.  
    ![dados](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Se você não souber o nome completo de saudação do contador Olá, você pode começar por digitar um nome parcial e será exibida uma lista de contadores disponíveis. Quando você encontrar o contador de saudação você deseja tooadd, clique Olá nome na lista de saudação e clique em hello mais saudação do ícone tooadd contador.
4. Depois de adicionar o contador de hello, ele aparece na lista de saudação de contadores realçado com uma barra colorida.
5. Por padrão, Olá **aplicar abaixo máquinas de toomy configuração** opção é selecionada. Se você quiser toodisable enviar dados de configuração, desmarque a seleção de saudação.
6. Quando você terminar de modificar os contadores de desempenho, final Olá Olá página clique **salvar** toofinalize suas alterações. Olá alterações de configuração feitas são enviadas tooall Olá agentes do OMS para Linux que são registrados com o OMS, normalmente em 5 minutos.

### <a name="configure-linux-performance-counters-in-oms"></a>Configurar contadores de desempenho do Linux no OMS
Para os contadores de desempenho do Windows, você pode escolher uma instância específica para cada contador de desempenho. No entanto, para contadores de desempenho do Linux, qualquer instância de um contador que você escolher aplica tooall contadores de filho do contador pai de saudação. Olá tabela a seguir mostra Olá instâncias comuns disponíveis tooboth contadores de desempenho do Linux e Windows.

| **Nome da instância** | **Significado** |
| --- | --- |
| \_Total |Total de todas as instâncias de saudação |
| \* |Todas as instâncias |
| (/&#124;/var) |Corresponde às instâncias chamadas: / ou /var |

Da mesma forma, o intervalo de amostragem de saudação que você escolher para um contador pai aplica tooall seus contadores filho. Em outras palavras, todos os intervalos de amostra do contador Olá filho e instâncias serão vinculadas.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Adicionar e configurar métricas de desempenho com o Linux
Toocollect de métricas de desempenho são controlados pela configuração de saudação em/etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf. Consulte [métricas de desempenho disponíveis](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) para classes e métricas de saudação do agente do OMS para Linux disponíveis.

Cada objeto ou categoria, de toocollect de métricas de desempenho deve ser definido no arquivo de configuração de saudação como um único `<source>` elemento. sintaxe de saudação segue o padrão de saudação abaixo.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

saudação de parâmetros configuráveis desse elemento é:

* **Objeto\_nome**: nome do objeto Olá coleção hello.
* **Instância\_regex**: um *expressão regular* definindo toocollect quais instâncias. Olá valor: `.*` especifica todas as instâncias. métricas de processador toocollect para apenas Olá \_instância Total, você poderia especificar `_Total`. as métricas do processo toocollect para hello apenas instâncias crond ou sshd, você pode especificar: `(crond|sshd)`.
* **Contador\_nome\_regex**: um *expressão regular* definindo toocollect quais contadores (para o objeto de saudação). Especifique de todos os contadores do objeto hello, toocollect: `.*`. toocollect trocas somente contadores de espaço para o objeto de memória hello, você pode especificar:`.+Swap.+`
* **Intervalo:**: Olá frequência na qual Olá contadores do objeto são coletados.

configuração padrão de saudação para métricas de desempenho é:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Habilitar os contadores de desempenho do MySQL usando os comandos do Linux
Se o servidor MySQL ou MariaDB for detectado no computador de saudação quando o pacote do hello omsagent estiver instalado, um provedor para o MySQL Server de monitoramento de desempenho é instalado automaticamente. Esse provedor se conecta toohello local MySQL/MariaDB tooexpose desempenho estatísticas do servidor. É necessário tooconfigure credenciais de usuário do MySQL para que hello provedor possa acessar saudação do MySQL Server.

toodefine um padrão conta de usuário para o MySQL server de saudação no localhost, use Olá exemplo de comando a seguir.

> [!NOTE]
> o arquivo de credenciais Olá deve ser legível por conta de omsagent hello. É recomendável executar o comando do hello mycimprovauth como omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Como alternativa, você pode especificar Olá necessárias credenciais do MySQL em um arquivo, Criando arquivo hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Para obter mais informações sobre o gerenciamento de credenciais do MySQL para o monitoramento por meio do arquivo mysql-auth de hello, consulte [monitoramento credenciais no arquivo de autenticação de saudação do MySQL gerenciar](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Consulte [permissões necessárias para contadores de desempenho do MySQL do banco de dados](#database-permissions-required-for-mysql-performance-counters) para obter detalhes sobre as permissões de objeto necessárias Olá MySQL usuário toocollect dados de desempenho do servidor MySQL.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Habilitar os contadores de desempenho do Servidor HTTP Apache usando os comandos do Linux
Se o Apache HTTP Server for detectado no computador de saudação quando o pacote do hello omsagent estiver instalado, um provedor para o Apache HTTP Server de monitoramento de desempenho é instalado automaticamente. Esse provedor baseia-se em um "módulo" que deve ser carregado no hello Apache HTTP Server nos dados de desempenho de tooaccess de ordem.

Você pode carregar o módulo de saudação com hello comando a seguir:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload Olá Apache módulo de monitoramento, execute Olá comando a seguir:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>dados de desempenho de tooview com análise de Log
1. No portal do Operations Management Suite hello, clique em bloco de pesquisa de Log de saudação.
2. Na barra de pesquisa hello, digite `* (Type=Perf)` tooview todos os contadores de desempenho.

Como o OMS também coleta dados de contador de desempenho do Windows, você deve escopo suspensa Olá dados tooLinux específico de pesquisa. Assim, hello exemplo a seguir mostraria servidor desempenho dados específicos tooan exemplo Linux chamado Chorizo21.

```
Type=Perf Computer=chorizo*
```

![servidor de exemplo mostrado nos resultados da pesquisa](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Nos resultados de saudação, você pode clicar em **métricas** contadores de saudação tooview que dados foram coletados. Os dados em tempo real são mostrados como gráficos para cada contador.

![Métricas](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog é um protocolo semelhante tooWindows logs de eventos de log de eventos – ambos funcionam de forma semelhante ao exibido no OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd um novo recurso de syslog do Linux no OMS
1. Em Olá **configurações** página em **dados** , clique em **Syslog** e toohello à esquerda do ícone de adição hello, digite Olá nome do recurso de syslog Olá que você deseja tooadd.
    ![Syslog do Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Se você não souber o nome completo de saudação do recurso hello, você pode começar por digitar um nome parcial e será exibida uma lista de instalações de syslog disponíveis. Quando você encontrar o recurso de syslog Olá deseja tooadd, clique Olá nome na lista de saudação e, em seguida, clique em hello mais saudação do ícone tooadd recurso de syslog.
3. Depois de adicionar instalação hello, ele aparece na lista de saudação do realçado com uma barra colorida. Em seguida, escolha as gravidades hello (categorias de informações de instalação de syslog) que você deseja toocollect.
4. Final Olá Olá página clique **salvar** toofinalize suas alterações. Olá alterações de configuração feitas são enviadas tooall Olá agentes do OMS para Linux que são registrados com o OMS, normalmente em 5 minutos.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Configurar recursos de syslog do Linux no Linux
Eventos de syslog são enviados do daemon do syslog hello, por exemplo rsyslog ou syslog-ng, porta local tooa que o agente hello está escutando. Por padrão, a porta 25224. Quando o agente de saudação é instalado, uma configuração de syslog padrão é aplicada. Isso é encontrado em:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng: /etc/syslog-ng/syslog-ng.conf

configuração de syslog do saudação padrão agente OMS carrega eventos de syslog de todas as instalações com uma severidade de aviso ou superior.

> [!NOTE]
> Se você editar configuração de syslog Olá, você deve reiniciar o daemon do syslog Olá Olá alterações tootake efeito.
>
>

Olá syslog configuração padrão de saudação do agente do OMS para Linux para OMS é:

#### <a name="rsyslog"></a>Rsyslog
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview todos os eventos de Syslog com análise de Log
1. No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.
2. Em Olá **gerenciamento de Log** de agrupamento, escolha uma pesquisa de syslog predefinida e, em seguida, selecione um toorun-lo.

Este exemplo mostra todos os eventos de Syslog.

![Eventos de Syslog mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Agora você pode analisar os resultados da pesquisa.

## <a name="linux-alerts"></a>Alertas do Linux
Se você usar Nagios ou Zabbix toomanage suas máquinas Linux, então o OMS pode receber alertas de saudação geradas a partir dessas ferramentas. No entanto, não há atualmente nenhum método tooconfigure alerta dados de entrada usando o portal do OMS hello. Em vez disso, você precisará tooedit um tooOMS config arquivo toostart enviar alertas.

### <a name="collect-alerts-from-nagios"></a>Coletar alertas a partir do Nagios
toocollect alertas de um servidor Nagios, você precisa de saudação toomake as seguintes alterações de configuração.

1. Usuário de saudação Grant **omsagent** acesso de leitura toohello arquivo de log Nagios (ou seja, /var/log/nagios/nagios.log). Supondo que o arquivo nagios.log de saudação pertencem ao grupo Olá **nagios** , você pode adicionar usuário Olá **omsagent** toohello **nagios** grupo.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Modificar o arquivo do hello confconfiguration (/ etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf). Certifique-se de saudação entradas a seguir está presentes e sem comentários:

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Reinicie o daemon omsagent hello:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Coletar alertas do Zabbix
toocollect alertas de um servidor Zabbix, você executará toothose de etapas semelhantes de Nagios acima, exceto que você precisará toospecify um usuário e senha em *limpar texto*. Isso não é o ideal, mas provavelmente será alterado em breve. tooaddress esse problema, recomendamos que você cria usuário hello e conceda permissão toomonitor somente.

Uma seção de exemplo do arquivo de configuração omsagent hello (/ etc/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/conf/omsagent.conf) para Zabbix deve ser semelhante à seguinte hello:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Exibir alertas na pesquisa do Log Analytics
Depois de configurar sua tooOMS de alertas de toosend de computadores Linux, você pode usar alguns log simples pesquisa consultas tooview Olá alertas. Olá seguinte exemplo de consulta de pesquisa retorna todos os alertas de saudação registrada que foram gerados. Por exemplo, se ocorrer algum tipo de problema em sua infraestrutura de TI, em seguida, resultados para Olá consulta pode indicar onde Olá problemas se originam do exemplo a seguir. Além disso, você pode facilmente fazer uma busca de alertas toohello por origem sistema toohelp estreita sua investigação. Hello vantagem é que você não necessariamente sistemas de gerenciamento de toovarious toogo do início da saudação — desde que os alertas são enviados tooOMS, você pode iniciar de lá.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios todos os alertas com análise de Log
1. No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.
2. Na barra de consulta hello, digite o seguinte Olá pesquisa consulta

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertas do Nagios mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Depois de ver os resultados da pesquisa hello, você pode analisar detalhes adicionais, como *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview todos os alertas de Zabbix com análise de Log
1. No portal do Operations Management Suite hello, clique em Olá **pesquisa de Log** lado a lado.
2. Na barra de consulta hello, digite o seguinte Olá pesquisa consulta

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertas do Zabbix mostrados na Pesquisa de Log](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Depois de ver os resultados da pesquisa hello, você pode analisar detalhes adicionais, como *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Compatibilidade com o System Center Operations Manager
Olá agente do OMS para Linux compartilha binários de agente com o agente do System Center Operations Manager hello. Atualizações de instalação Olá agente do OMS para Linux em um sistema gerenciado atualmente pelo Operations Manager Olá pacotes OMI e SCX na versão mais recente do hello computador tooa. Olá agente do OMS para Linux e do System Center 2012 R2 são compatíveis. No entanto, **System Center 2012 SP1 e versões anteriores atualmente não são compatíveis ou não tem suporte com hello agente do OMS para Linux.**

> [!NOTE]
> Se Olá agente do OMS para Linux for instalado tooa computador que não é atualmente gerenciado pelo Operations Manager e mais tarde quiser toomanage computador de saudação com o Operations Manager, você deve modificar a configuração do OMI Olá antes de descobrir o computador de saudação. **Essa etapa não é necessária se o agente do Operations Manager de saudação for instalado antes de saudação do agente do OMS para Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>Olá tooenable agente do OMS para Linux toocommunicate com o Operations Manager
1. Editar saudação arquivo /etc/opt/omi/conf/omiserver.conf
2. Certifique-se de que Olá linha a partir **httpsport =** define Olá porta 1270. Como `httpsport=1270`
3. Reinicie o servidor OMI de saudação:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Permissões de banco de dados necessárias para contadores de desempenho do MySQL
toogrant permissões tooa monitoramento usuário do MySQL, concedendo ao usuário Olá deve ter Olá privilégio 'GRANT option', bem como privilégio Olá sendo concedido.

Para que Olá MySQL usuário tooreturn desempenho dados Olá usuário precisará de acesso toohello consultas a seguir:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Além disso, usuário do MySQL toothese consultas Olá requer acesso SELECT toohello tabelas padrão a seguir:

* information_schema
* MySQL

Esses privilégios podem ser concedidos, executando Olá comandos de concessão a seguir.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Gerenciar as credenciais no arquivo de autenticação de saudação de monitoramento do MySQL
a seguir Olá seções ajudam você a gerenciar as credenciais do MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Configurar Olá provedor de OMI do MySQL
Hello provedor de OMI do MySQL requer um usuário do MySQL pré-configurado e bibliotecas de cliente de MySQL instaladas nas informações de integridade do desempenho de saudação ordem tooquery da instância do MySQL hello.

### <a name="mysql-omi-authentication-file"></a>Arquivo de autenticação de OMI do MySQL
Provedor de OMI do MySQL usa um toodetermine de arquivo de autenticação que instância do MySQL Olá endereço de associação e a porta está escutando e quais credenciais toouse toogather métricas. Durante a saudação de instalação de OMI do MySQL provedor verificar arquivos de configuração my.cnf do MySQL (locais padrão) para o endereço de associação e a porta e parcialmente conjunto Olá arquivo de autenticação de OMI do MySQL.

toocomplete monitoramento de uma instância do servidor MySQL, adicione um arquivo de autenticação de OMI do MySQL pré-gerado diretório correto hello.

### <a name="authentication-file-format"></a>Formato do arquivo de autenticação
Olá arquivo de autenticação de OMI do MySQL é um arquivo de texto que contém informações sobre:

* Porta
* Endereço de Ligação
* Nome de usuário do MySQL
* Senha codificada em Base64

Olá arquivo de autenticação de OMI do MySQL concede privilégios de usuário do Linux toohello leitura/gravação que o gerou.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Um padrão de arquivo de autenticação de OMI do MySQL contém uma instância padrão e um número de porta, dependendo de quais informações estão disponíveis e analisadas do hello encontrado o arquivo de configuração do MySQL.

instância padrão de saudação é um toomake significa gerenciar várias instâncias do MySQL em um host Linux mais fácil e é indicada pela instância de saudação com a porta 0. Todas as instâncias adicionadas herdarão as propriedades definidas da instância de padrão de saudação. Por exemplo, se a instância do MySQL escutando na porta '3308' for adicionada, endereço de associação da instância de saudação padrão, nome de usuário e senha codificada em Base64 serão ser tootry usado e monitorar Olá instância escuta na porta 3308. Se instância Olá em 3308 é o endereço de tooanother associado e usa Olá o mesmo nome de usuário do MySQL e par senha Olá apenas nova especificação de saudação endereço de associação é necessária e hello outras propriedades serão herdadas.

Exemplos de arquivo de autenticação Olá parecida com a seguinte hello.

Instância padrão e instância com porta 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Instância padrão e instância com porta 3308 + senha codificada em Base64 diferente:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Propriedade** | **Descrição** |
| --- | --- |
| Porta |A porta representa Olá Olá atual da porta escuta da instância do MySQL.  porta de saudação 0 significa que propriedades Olá a seguir são usadas para a instância padrão. |
| Endereço de Ligação |Olá endereço de associação é Olá atual MySQL endereço de associação |
| Nome de Usuário |Esse nome de usuário do usuário MySQL, Olá Olá desejar instância do servidor toouse toomonitor Olá MySQL. |
| Senha codificada em Base64 |Esta é a senha de saudação do usuário monitoramento do MySQL Olá codificada em Base64. |
| Atualização Automática |Quando Olá provedor de OMI do MySQL é atualizado o provedor Olá examinar novamente para que as alterações no arquivo my.cnf de saudação e substituir o arquivo de autenticação de OMI do MySQL Olá. Defina esse sinalizador tootrue ou false dependendo atualizações necessárias toohello OMI do MySQL arquivo de autenticação. |

#### <a name="authentication-file-location"></a>Local do arquivo de autenticação
Olá arquivo de autenticação de OMI do MySQL deve ser localizado na Olá local a seguir e chamado "mysql-auth":

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

arquivo de saudação (e o diretório auth/omsagent) devem ser de propriedade usuário omsagent de saudação.

## <a name="agent-logs"></a>Logs do Agente
logs de saudação do hello agente do OMS para Linux estão em:

/var/opt/microsoft/omsagent/&lt;id do espaço de trabalho&gt;/log/

logs de saudação do hello agente do OMS para Linux para o programa omsconfig (configuração do agente) estão em:

/var/opt/microsoft/omsconfig/log/

Os logs para Olá componentes OMI e SCX (que fornecem dados de métrica de desempenho) estão em:

/var/opt/omi/log/ e /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Saudação de solução de problemas do agente do OMS para Linux
Use Olá toodiagnose informações a seguir e solucionar problemas comuns.

Se nenhuma das informações contidas nesta seção de solução de problemas de saudação ajuda a você, você também pode usar Olá seguir recursos toohelp resolver seu problema.

* Os clientes com suporte Premier podem registrar um caso de suporte via [Premier](https://premier.microsoft.com/)
* Os clientes com contratos de suporte do Azure podem fazer o logon casos de suporte Olá [portal do Azure](https://manage.windowsazure.com/?getsupport=true)
* Arquive um [Problema no GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Fórum de comentários para ideias e um relatório de erros de toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Locais de log importantes
| Arquivo | Caminho |
| --- | --- |
| Agente do OMS para arquivo de log do Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Agente do OMS para arquivo de log de configuração |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Arquivos de configuração importantes
| Categoria | Local do arquivo |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf` ou `/etc/rsyslog.conf` ou `/etc/rsyslog.d/95-omsagent.conf` |
| Desempenho, Nagios, Zabbix, saída do OMS e agente geral |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Configurações adicionais |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Os arquivos de configuração de edição para contadores de desempenho e syslog serão substituídos se a Configuração do Portal do OMS estiver habilitada. Você pode desabilitar a configuração no Portal do OMS da saudação (para todos os nós) ou para nós únicos executando Olá seguinte:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Habilitar o log de depuração
depuração de tooenable log, você pode usar o plug-in do hello OMS saída e saída detalhada.

#### <a name="oms-output-plugin"></a>Plug-in de saída do OMS
FluentD permite Olá plug-in toospecify níveis de log para os níveis de log diferente para entradas e saídas. toospecify um nível de log diferente para a saída do OMS, edita a configuração de agente geral de saudação no hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` arquivo.

Inferior Olá Olá do arquivo de configuração, alterar Olá `log_level` propriedade `info` muito`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Log de depuração permite que você toosee em lote carregamentos toohello serviço OMS separado por tipo, o número de itens de dados e o tempo gasto toosend.

*Log habilitado para depuração de exemplo:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Saída detalhada
Em vez de usar o plug-in de saída OMS hello, você também pode gerar itens de dados diretamente muito`stdout`, que é visível no hello agente do OMS para o arquivo de log do Linux.

No arquivo de configuração de agente geral Olá OMS em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, fora de comentário hello OMS saída plug-in adicionando um `#` na frente de cada linha.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Abaixo Olá plug-in de saída, remova o comentário hello em Olá a seção seguinte, removendo Olá `#` símbolo no início de saudação de cada linha.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Mensagens de Syslog encaminhadas não aparecem no log de saudação
#### <a name="probable-causes"></a>Causas prováveis
* Olá configuração aplicada toohello Linux server não permitir a coleta de instalações de saudação enviada de e/ou níveis de log
* Syslog não é está sendo encaminhado corretamente toohello Linux server
* número de saudação de mensagens encaminhadas por segundo é muito grande para a configuração de base de saudação de saudação do agente do OMS para Linux toohandle

#### <a name="resolutions"></a>Resoluções
* Verifique se o essa configuração Olá no Portal do OMS de saudação de Syslog tem todos os recursos de saudação e níveis de log correto Olá
  * **Portal do OMS > Configurações > Dados > Syslog**
* Verifique se que mensagens daemons de syslog nativo (`rsyslog`, `syslog-ng`) é tooreceive capaz de mensagens de saudação encaminhada
* Verifique as configurações de firewall no hello Syslog server tooensure mensagens não estão sendo bloqueadas
* Simular uma tooOMS de mensagem Syslog usando Olá `logger` comando - por exemplo:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Problemas de conexão tooOMS ao usar um proxy
#### <a name="probable-causes"></a>Causas prováveis
* proxy de saudação especificado quando o agente de saudação instalando e configurando está incorreto
* pontos de extremidade de serviço do OMS Olá não são whitelistested em seu data center

#### <a name="resolutions"></a>Resoluções
* Reinstalar Olá agente do OMS para Linux usando Olá após o comando com a opção de saudação `-v` habilitado. Isso permite que a saída detalhada do agente de saudação se conectam por meio do proxy de saudação toohello serviço OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Revisar a documentação Olá para proxy OMS em [Configurando o agente de saudação para uso com um servidor proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Verifique se esse Olá pontos de extremidade de serviço do OMS a seguir estão na lista de permissões

| Recurso de agente | Portas |
| --- | --- |
| &#42;.ods.opinsights.azure.com |Porta 443 |
| &#42;.oms.opinsights.azure.com |Porta 443 |
| ods.systemcenteradvisor.com |Porta 443 |
| &#42;.blob.core.windows.net/ |Porta 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>É exibido um erro 403 durante a integração
#### <a name="probable-causes"></a>Causas prováveis
* saudação de data e hora estão incorretas no servidor Linux
* Olá ID do espaço de trabalho e a chave do espaço de trabalho usados estão incorretas

#### <a name="resolution"></a>Resolução
* Verifique se o tempo de saudação em seu servidor Linux com hello `date` comando. Se Olá dados for maiores ou menor que 15 minutos de hello hora atual, integração falhará. toocorrect isso, atualize date de hello e/ou fuso horário do servidor Linux.
* a versão mais recente Olá de saudação do agente do OMS para Linux notifica se uma diferença de hora está causando a falha de integração
* Usando re-carregar Olá ID correta do espaço de trabalho e a chave do espaço de trabalho. Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Um erro 500 ou erro 404 aparece no arquivo de log Olá após a integração
Esse é um problema conhecido que ocorre durante a saudação primeiro carregamento de dados do Linux em um espaço de trabalho do OMS. Ele não afeta os dados que estão sendo enviados ou outros problemas. Você pode ignorar erros hello quando inicialmente integração.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Dados de Nagios não aparecem no Portal do OMS de saudação
#### <a name="probable-causes"></a>Causas prováveis
* Olá omsagent o usuário não tem permissões tooread de arquivo de log Nagios Olá
* Olá Nagios origem e filtro seções ainda comentários no arquivo de omsagent Olá

#### <a name="resolutions"></a>Resoluções
* Adicione usuário omsagent de saudação em ordem tooread do arquivo de Nagios hello. Confira [Alertas do Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) para saber mais.
* No hello agente do OMS para o arquivo de configuração geral do Linux no `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, certifique-se de que **ambos** Olá Nagios seções de origem e filtro tem comentários removidos, semelhante toohello exemplo a seguir.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Dados do Linux não aparecem em Olá Portal do OMS
#### <a name="probable-causes"></a>Causas prováveis
* Falha de serviço do OMS toohello de integração
* Conexão toohello serviço OMS está bloqueado
* saudação de agente do OMS para Linux dados é armazenado em backup

#### <a name="resolutions"></a>Resoluções
* Verifique se que toohello integração serviço OMS foi bem-sucedida verificando que Olá `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.
* Usando re-carregar Olá a linha de comando omsadmin.sh. Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.
* Se usar um proxy, usar etapas para solução de problemas de proxy de saudação acima
* Em alguns casos, quando Olá agente do OMS para Linux não pode se comunicar com hello serviço OMS, dados de saudação Agent estão tamanho de buffer cheio toohello de backup de 50 MB. Reiniciar Olá agente do OMS para Linux executando Olá `/opt/microsoft/omsagent/bin/service_control restart` comando.
  >[AZURE.NOTE] Esse problema foi corrigido nas versões 1.1.0-28 e posteriores do Agente.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Configuração do contador de desempenho de syslog Linux não é aplicada no portal do OMS Olá
#### <a name="probable-causes"></a>Causas prováveis
* Agente de configuração de saudação de saudação do agente do OMS para Linux não recuperou configuração mais recente de saudação do portal do OMS hello.
* Olá revisadas configurações no portal de saudação não foram aplicadas

#### <a name="resolutions"></a>Resoluções
`omsconfig`é o agente de configuração de saudação de saudação do agente do OMS para Linux que recupera alterações de configuração do portal do OMS a cada 5 minutos. Essa configuração é então aplicado toohello agente do OMS para Linux arquivos de configuração localizado em `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* Em alguns casos, Olá agente do OMS para Linux agente de configuração talvez não seja capaz de toocommunicate com o serviço de configuração do portal Olá resultante na configuração mais recente não está sendo aplicada.
* Verifique se esse Olá `omsconfig` agente é instalado com o seguinte hello:

  * `dpkg --list omsconfig` ou `rpm -qi omsconfig`
  * Se não estiver instalado, reinstale a versão mais recente Olá de saudação do agente do OMS para Linux
* Verifique se esse Olá `omsconfig` agente possa se comunicar com hello serviço OMS

  * Executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
    * Olá comando acima retorna Olá configuração que o agente recupera do portal hello, incluindo configurações de Syslog, contadores de desempenho do Linux e logs personalizados
    * Se Olá comando acima falhar, executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Esse comando força Olá omsconfig agente toocommunicate com a configuração da mais recente de Olá Olá OMS serviço tooretrieve.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Dados de log personalizado do Linux não aparecem na Olá Portal do OMS
#### <a name="probable-causes"></a>Causas prováveis
* Falha do serviço de integração tooOMS
* Olá **Olá aplicar configuração toomy servidores Linux a seguir** configuração não tiver sido selecionada
* omsconfig não tem escolhidas log personalizado mais recente de saudação do portal de saudação
* Olá `omsagent` uso é log personalizado do hello tooaccess não é possível devido a problema de permissões tooa ou `omsagent` não foi encontrado. Nesse caso, você verá Olá saída a seguir:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Este é um problema conhecido com hello condição de corrida que foi corrigido hello agente do OMS para Linux versão 1.1.0-217

#### <a name="resolutions"></a>Resoluções
* Verifique se que você tenha com êxito incorporados, determinando se hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` arquivo existe.
  * Se necessário, integrar novamente usando a linha de comando omsadmin.sh hello. Consulte [integração usando a linha de comando Olá](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obter mais informações.
* Em Olá Portal do OMS em **configurações** em Olá **dados** guia, certifique-se de que Olá **Olá aplicar configuração toomy servidores Linux a seguir** configuração é selecionada  
  ![aplicar configuração](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Verifique se esse Olá `omsconfig` agente possa se comunicar com hello serviço OMS

  * Executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
  * Olá comando acima retorna Olá configuração que o agente recupera do hello Portal, incluindo configurações de Syslog, contadores de desempenho do Linux e Logs personalizados
  * Se Olá comando acima falhar, executar Olá `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Esse comando força Olá omsconfig agente toocommunicate com o serviço OMS e recuperar a configuração mais recente hello.

Em vez de saudação do agente do OMS para execução como um usuário com privilégios de usuário do Linux `root`, Olá agente do OMS para Linux como Olá `omsagent` usuário. Na maioria dos casos, a permissão explícita deve ser concedida usuário toohello em ordem tooread alguns arquivos.

permissão toogrant muito`omsagent` usuário, execute Olá comandos a seguir:

1. Adicionar Olá `omsagent` grupo específico do usuário tooa com`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Conceder acesso de leitura universal toohello necessários arquivos com`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Há um problema conhecido com hello condição de corrida que foi corrigido hello agente do OMS para Linux versão 1.1.0-217. Depois de atualizar o agente mais recente toohello, execute Olá versão mais recente do comando tooget saudação do plug-in do hello saída a seguir:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Limitações conhecidas
Examine Olá toolearn seções sobre as limitações atuais de saudação do agente do OMS para Linux a seguir.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure
Para máquinas virtuais do Linux em execução no Azure, etapas adicionais podem ser necessárias tooallow a coleta de dados pelo diagnóstico do Azure e Operations Management Suite. **Versão 2.2** da saudação extensão de diagnóstico para Linux é necessária para compatibilidade com hello agente do OMS para Linux.

Para obter mais informações sobre como instalar e configurar Olá extensão de diagnóstico para Linux, consulte [usar Olá CLI do Azure comando tooenable extensão de diagnóstico do Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Atualizando Olá extensão de diagnóstico do Linux do 2.0 too2.2 ASM da CLI do Azure:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Esses exemplos de comando fazem referência a um arquivo chamado PrivateConfig.json. formato de saudação do arquivo deve ser semelhante a saudação de exemplo a seguir.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Não há suporte para Sysklog.
O rsyslog ou syslog-ng é necessário toocollect mensagens de syslog. Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog. toocollect dados de syslog dessa versão de distribuições, Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog. Para obter mais informações sobre como substituir sysklog por rsyslog, consulte [instalar o RPM de rsyslog Olá recém-criadas](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Próximas etapas
* [Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.
* Familiarize-se com [pesquisas de log](log-analytics-log-searches.md) tooview detalhadas informações coletadas por meio de soluções.
* Use [painéis](log-analytics-dashboards.md) toosave e exibição procura próprios e personalizados.
