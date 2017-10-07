---
title: "aaaCollect e analisar as mensagens de Syslog na análise de logs do OMS | Microsoft Docs"
description: "Syslog é um protocolo de registro em log de eventos é tooLinux comuns. Este artigo descreve como tooconfigure coleção de mensagens de Syslog na análise de Log e os detalhes de registros de saudação criado no repositório do OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Fontes de dados de Syslog no Log Analytics
Syslog é um protocolo de registro em log de eventos é tooLinux comuns.  Aplicativos enviará mensagens que podem ser armazenadas no computador local hello ou entregues tooa Syslog coletor.  Olá agente do OMS para Linux for instalado, ele configura Olá Syslog daemon tooforward mensagens toohello agente local.  Olá agente envia mensagem de saudação tooLog Analytics onde um registro correspondente é criado no repositório do OMS hello.  

> [!NOTE]
> Análise de log dá suporte a coleção de mensagens enviadas por rsyslog ou syslog-ng, onde rsyslog é o daemon saudação padrão. Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog. Olá toocollect dados de syslog dessa versão de distribuições, [daemon de rsyslog](http://rsyslog.com) deve ser instalado e configurado tooreplace sysklog.
>
>

![Coleção do Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Configurando Syslog
Olá agente do OMS para Linux coletará apenas eventos com instalações de saudação e gravidades especificadas em sua configuração.  Você pode configurar o Syslog por meio do portal do OMS hello ou por meio do gerenciamento de arquivos de configuração em seus agentes do Linux.

### <a name="configure-syslog-in-hello-oms-portal"></a>Configurar o Syslog no portal do OMS Olá
Configurar o Syslog Olá [menu dados nas configurações de análise de Log](log-analytics-data-sources.md#configuring-data-sources).  Essa configuração é entregue toohello o arquivo de configuração em cada agente do Linux.

Você pode adicionar um novo recurso, digitando seu nome e clicando em **+**.  Para cada recurso, apenas as mensagens com severidades de saudação selecionada serão coletadas.  Verifique severidades Olá para que você deseja toocollect de recurso específico do hello.  Você não pode fornecer qualquer critérios adicionais toofilter mensagens.

![Configurar Syslog](media/log-analytics-data-sources-syslog/configure.png)

Por padrão, todas as alterações de configuração são enviadas automaticamente tooall agentes.  Se você quiser tooconfigure Syslog manualmente em cada agente do Linux, em seguida, desmarque a caixa Olá *aplicar abaixo máquinas de Linux toomy configuração*.

### <a name="configure-syslog-on-linux-agent"></a>Configurar o Syslog no agente do Linux
Olá quando [agente do OMS é instalado em um cliente Linux](log-analytics-linux-agents.md), ele instala um arquivo de configuração de syslog padrão que define o recurso de saudação e gravidade da saudação mensagens que são coletados.  Você pode modificar essa configuração de saudação do arquivo toochange.  arquivo de configuração de saudação é diferente dependendo Olá Syslog daemon que Olá cliente foi instalado.

> [!NOTE]
> Se você editar configuração de syslog Olá, você deve reiniciar o daemon do syslog Olá Olá alterações tootake efeito.
>
>

#### <a name="rsyslog"></a>rsyslog
Olá arquivo de configuração para rsyslog está localizado em **/etc/rsyslog.d/95-omsagent.conf**.  Seu conteúdo padrão é mostrado abaixo.  Isso reúne mensagens de syslog enviadas do agente local Olá para todos os recursos com um nível de aviso ou superior.

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

Você pode remover um recurso, removendo sua seção saudação do arquivo de configuração.  Você pode limitar severidades Olá que são coletadas para um recurso específico, modificando entrada desse recurso.  Por exemplo, toolimit Olá usuário recurso toomessages com uma severidade de erro ou maior que modificaria essa linha de saudação toohello de arquivo de configuração a seguir:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
arquivo de configuração de saudação do syslog-ng é local em **/etc/syslog-ng/syslog-ng.conf**.  Seu conteúdo padrão é mostrado abaixo.  Isso reúne mensagens de syslog enviadas de agente local Olá para todos os recursos e todas as gravidades.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Você pode remover um recurso, removendo sua seção saudação do arquivo de configuração.  Você pode limitar severidades Olá que são coletadas para um recurso específico, removendo-as da sua lista.  Por exemplo, toolimit Olá usuário recurso toojust mensagens de alerta e críticas, deverá modificar essa seção do hello toohello de arquivo de configuração a seguir:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Coletar dados de portas de Syslog adicionais
agente do OMS Olá escuta mensagens de Syslog no cliente local de saudação na porta 25224.  Quando Olá agente é instalado, uma configuração de syslog padrão é aplicada e encontrada no hello local a seguir:

* Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

Você pode alterar o número da porta Olá criando dois arquivos de configuração: um arquivo de configuração FluentD e um arquivo de ng de rsyslog ou syslog dependendo de ter instalado o daemon Syslog hello.  

* arquivo de configuração do Hello FluentD deve ser um novo arquivo localizado em: `/etc/opt/microsoft/omsagent/conf/omsagent.d` e substitua o valor Olá Olá **porta** entrada com o número da porta personalizada.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Para rsyslog, você deve criar um novo arquivo de configuração localizado em: `/etc/rsyslog.d/` e substitua Olá valor % SYSLOG_PORT % com o número da porta personalizada.  

    > [!NOTE]
    > Se você modificar esse valor no arquivo de configuração de saudação `95-omsagent.conf`, ele será substituído quando o agente de saudação aplica uma configuração padrão.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello syslog-ng config deve ser modificado, copiando a configuração de exemplo hello mostrada abaixo e adicionando Olá personalizado configurações modificadas toohello final do arquivo de configuração de syslog ng.conf Olá localizado em `/etc/syslog-ng/`.  Fazer **não** usar saudação padrão rótulo **% WORKSPACE_ID % _oms** ou **% WORKSPACE_ID_OMS**, definir um personalizado toohelp rótulo distinguir as alterações.  

    > [!NOTE]
    > Se você modificar os valores padrão de saudação no arquivo de configuração de hello, eles serão substituídos quando o agente de saudação aplica uma configuração padrão.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Depois de concluir as alterações hello, Olá Syslog e hello o serviço de agente do OMS precisa toobe reiniciado tooensure Olá configuração alterações entrarão em vigor.   

## <a name="syslog-record-properties"></a>Propriedades de registro do syslog
Registros de syslog têm um tipo de **Syslog** e têm propriedades de saudação em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Computador que Olá evento foi coletado do. |
| Recurso |Define a parte de saudação do sistema de saudação que gerou a mensagem de saudação. |
| HostIP |Endereço IP do sistema Olá enviar mensagem de saudação. |
| HostName |Nome do sistema de saudação enviar mensagem de saudação. |
| SeverityLevel |Nível de severidade do evento hello. |
| SyslogMessage |Texto da mensagem de saudação. |
| ProcessID |ID do processo de saudação que gerou a mensagem de saudação. |
| EventTime |Data e hora em que Olá evento foi gerado. |

## <a name="log-queries-with-syslog-records"></a>Consultas do log com registros do Syslog
Olá tabela a seguir fornece exemplos de diferentes de consultas de log que recuperam registros de Syslog.

| Consultar | Descrição |
|:--- |:--- |
| Type=Syslog |Todos os Syslogs. |
| Type=Syslog SeverityLevel=error |Todos os registros do Syslog com a severidade de erro. |
| Type=Syslog &#124; measure count() by Computer |Contagem de registros do Syslog por computador. |
| Type=Syslog &#124; measure count() by Facility |Contagem de registros do Syslog por recurso. |

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.

> | Consultar | Descrição |
|:--- |:--- |
| syslog |Todos os Syslogs. |
| Syslog &#124; where SeverityLevel == "error" |Todos os registros do Syslog com a severidade de erro. |
| Syslog &#124; summarize AggregatedValue = count() by Computer |Contagem de registros do Syslog por computador. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |Contagem de registros do Syslog por recurso. |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse dados de registros de syslog em campos individuais.
* [Configurar agentes do Linux](log-analytics-linux-agents.md) toocollect outros tipos de dados.
