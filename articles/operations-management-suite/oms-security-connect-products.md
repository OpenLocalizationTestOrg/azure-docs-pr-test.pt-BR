---
title: "aaaConnecting sua solução de auditoria e segurança produtos toohello segurança Operations Management Suite (OMS) | Microsoft Docs"
description: "Este documento ajuda você tooconnect sua tooOperations de produtos de segurança usando o formato de evento comuns de solução de auditoria e segurança do pacote de gerenciamento."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Conectar-se a sua solução de auditoria e segurança produtos toohello segurança Operations Management Suite (OMS) 
Este documento ajuda você a se conectar a seus produtos de segurança Olá segurança da OMS e solução de auditoria. Olá as origens a seguir têm suporte:

- Eventos de Formato de Evento Comum (CEF)
- Eventos do Cisco ASA


## <a name="what-is-cef"></a>O que é CEF?
Formato de evento comuns (CEF) é um formato padrão da indústria sobre mensagens de Syslog, usado por muitos segurança fornecedores tooallow evento interoperabilidade entre plataformas diferentes. Suportam a ingestão de dados usando os produtos de segurança CEF, que permite que você tooconnect com segurança de OMS OMS solução de segurança e auditoria. 

Conectando-se a tooOMS de fonte de dados, você está tootake capaz de aproveitar Olá recursos que fazem parte dessa plataforma a seguir:

- Pesquisa e Correlação
- Auditoria
- Alerta
- Inteligência contra ameaças
- Problemas importantes

## <a name="collection-of-security-solution-logs"></a>Coleção de logs da solução de segurança

A Segurança do OMS dá suporte à coleta de logs usando CEF em Syslogs e de logs do [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). Neste exemplo, origem hello (computador que gera logs de saudação) é um computador Linux executando o daemon do syslog-ng e destino de saudação é segurança do OMS. tarefas do computador com Linux tooprepare Olá que precisará Olá tooperform a seguir:

- Baixe Olá agente do OMS para Linux, versão 1.2.0-25 ou superior.
- Siga a seção de saudação **guia de instalação rápida** de [neste artigo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall e Olá integrar agente tooyour espaço de trabalho.

Normalmente, Olá é instalado em um computador diferente da saudação um no qual logs Olá são gerados. O computador de agente do encaminhamento Olá logs toohello geralmente exigirá Olá etapas a seguir:

- Configure Olá log produto/máquina tooforward Olá eventos necessários toohello o syslog daemon (rsyslog ou syslog-ng) no computador do agente de saudação.
- Habilite o daemon do syslog Olá em mensagens de tooreceive de máquina de agente de saudação de um sistema remoto.

No computador do agente hello, eventos de saudação necessário toobe enviado do hello syslog daemon toolocal a porta UDP 25226. Olá agente está escutando para eventos de entrada nessa porta. a seguir Olá é um exemplo de configuração para envio de todos os eventos do agente de toohello do sistema local hello (você pode modificar Olá configuração toofit as configurações locais):

1. Janela do terminal Olá aberta e vá toohello directory */etc/syslog-ng /* 
2. Criar um novo arquivo *omsagent de configuração de segurança* e adicione Olá conteúdo a seguir: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Baixe o arquivo hello *security_events.conf* e colocar em */etc/opt/microsoft/omsagent/conf/omsagent.d/* no computador do agente do OMS hello.
4. Digite comando Olá abaixo daemon do syslog Olá toorestart: *para syslog-ng executar:*
    
    ```
    sudo service rsyslog restart
    ```

    *For rsyslog run:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Digite o comando abaixo toorestart Olá agente do OMS hello:

    *For syslog-ng run:*
    
    ```
    sudo service omsagent restart
    ```

    *For rsyslog run:*
    
    ```
    systemctl restart omsagent
    ```
6. Digite o comando de saudação abaixo e revise Olá tooconfirm de resultado que não há nenhum erro no log de agente do OMS hello:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Revisando os eventos de segurança coletados

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Após hello configuração, eventos de segurança Olá iniciará toobe incluído por segurança do OMS. toovisualize esses eventos, abra Olá pesquisa de Log, digite o comando de saudação *tipo = CommonSecurityLog* em Olá campo de pesquisa e pressione ENTER. Olá, exemplo a seguir mostra Olá resultado desse comando, observe que nesse caso OMS segurança já incluídos logs de segurança de vários fornecedores:
   
![Avaliação de Linha de Base de Auditoria e Segurança do OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Você pode refinar essa pesquisa para um único fornecedor, por exemplo, toovisualize Cisco online logs, digite: *tipo = CommonSecurityLog DeviceVendor = Cisco*. Olá "CommonSecurityLog" possui predefinido campos para qualquer cabeçalho CEF incluindo extensios básica hello, durante qualquer outra extensão seja "Extensão personalizada" ou não, será inserido no campo "AdditionalExtensions". Você pode usar campos de tooget dedicado de recurso de campos personalizados de saudação dele. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Acessando computadores sem avaliação de linha de base
OMS dá suporte para perfil de linha de base de membro de domínio Olá no Windows Server 2008 R2 até tooWindows Server 2012 R2. A linha de base do Windows Server 2016 ainda não é final e será adicionada assim que for publicada. Todos os outros sistemas operacionais verificados por meio de avaliação de linha de base de segurança da OMS e auditoria aparecem sob Olá **computadores ausente avaliação de linha de base** seção.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como tooconnect seu tooOMS de solução CEF. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

