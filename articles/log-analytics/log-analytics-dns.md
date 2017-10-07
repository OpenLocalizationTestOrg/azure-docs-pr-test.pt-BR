---
title: "aaaDNS solução de análise na análise de Log do Azure | Microsoft Docs"
description: "Configurar e usar a solução de análise de DNS de saudação na análise de Log toogather um panorama de infraestrutura de DNS em operações de segurança e desempenho."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Coletar informações sobre sua infraestrutura DNS com hello solução da visualização de análise do DNS

![Símbolo da Análise de DNS](./media/log-analytics-dns/dns-analytics-symbol.png)

Este artigo descreve como tooset backup e use Olá solução de análise de DNS do Azure no Azure Log Analytics toogather um panorama de infraestrutura de DNS em operações de segurança e desempenho.

A Análise de DNS ajuda você a:

- Identificar clientes que tentam tooresolve nomes de domínio mal-intencionado.
- Identificar registros de recursos obsoletos.
- Identificar os nomes de domínio consultados com frequência e clientes DNS comunicativos.
- Exibir a carga de solicitação em servidores DNS.
- Exibir falhas de registro de DNS dinâmico.

solução de saudação coleta, analisa e correlaciona analítica de DNS do Windows e logs de auditoria e outros dados relacionados de seus servidores DNS.

## <a name="connected-sources"></a>Fontes conectadas

Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução:

| **Fonte conectada** | **Suporte** | **Descrição** |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Sim | solução de saudação coleta informações de DNS de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | solução de saudação não coletará informações de DNS de agentes do Linux diretos. |
| [Grupo de gerenciamento do System Center Operations Manager](log-analytics-om-agents.md) | Sim | solução de saudação coleta informações de DNS de agentes em um grupo de gerenciamento conectado do Operations Manager. Uma conexão direta de saudação do Operations Manager agent toohello Operations Management Suite não é necessária. Dados são encaminhados do repositório de Operations Management Suite toohello do grupo de gerenciamento de saudação. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | Armazenamento do Azure não é usado pela solução de saudação. |

### <a name="data-collection-details"></a>Detalhes da coleta de dados

solução Olá coleta de inventário DNS e dados relacionados a eventos do DNS dos servidores DNS Olá onde um agente de análise de Log está instalado. Esses dados são, em seguida, carregados tooLog análise e exibidos no painel de solução de saudação. Dados relacionados ao estoque, como o número de saudação de servidores DNS, zonas e registros de recursos, são coletados por executar os cmdlets do PowerShell do DNS hello. dados de saudação são atualizados uma vez a cada dois dias. dados relacionados a eventos de saudação são coletados quase em tempo real de saudação [analítica e logs de auditoria](https://technet.microsoft.com/library/dn800669.aspx#enhanc) fornecida pelo registro de DNS e o diagnóstico no Windows Server 2012 R2 aprimorados.

## <a name="configuration"></a>Configuração

Use Olá solução de saudação tooconfigure informações a seguir:

- Você deve ter uma [Windows](log-analytics-windows-agents.md) ou [Operations Manager](log-analytics-om-agents.md) agent em cada servidor DNS que você deseja toomonitor.
- Você pode adicionar espaço de trabalho do hello DNS análise solução tooyour Operations Management Suite da saudação [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). Você também pode usar o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

solução de saudação inicia a coleta de dados sem necessidade de saudação de configuração adicional. No entanto, você pode usar o hello coleta de dados de toocustomize de configuração a seguir.

### <a name="configure-hello-solution"></a>Configurar a solução de saudação

No painel de solução de saudação, clique em **configuração** tooopen página de configuração de DNS da análise de saudação. Há dois tipos de alteração de configuração que podem ser feitos:

- **Nomes de Domínio na Lista de Permissões**. solução de saudação não processa todas as consultas de pesquisa de saudação. Ela mantém uma lista de permissões de sufixos de nome de domínio. consultas de pesquisa de saudação que resolvam nomes de domínio toohello correspondentes sufixos de nome de domínio em que esta lista de permissões não são processadas pela solução de saudação. Nomes de domínio na lista de permissões de processamento não ajuda a dados de saudação toooptimize enviados tooLog análise. lista branca de padrão de saudação inclui nomes de domínio público populares, como www.google.com e www.facebook.com. Você pode exibir a lista de conclusão padrão de saudação rolando.

 Você pode modificar Olá lista tooadd qualquer sufixo de nome de domínio que você deseja tooview insights de pesquisa para. Você também pode remover qualquer sufixo de nome de domínio que você não deseja tooview insights de pesquisa para.

- **Limite de Cliente Comunicativo**. Os clientes DNS que excedem o limite de saudação para número de saudação de solicitações de pesquisa é realçado no hello **clientes DNS** folha. limite do saudação padrão é 1.000. Você pode editar limite de saudação.

    ![Nomes de domínio na lista de permissões](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Pacotes de gerenciamento

Se você estiver usando o espaço de trabalho do hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite, hello seguinte pacote de gerenciamento é instalado:

- Pacote de Inteligência do Coletor de Dados DNS da Microsoft (Microsft.IntelligencePacks.Dns)

Se seu grupo de gerenciamento do Operations Manager é um espaço de trabalho conectada tooyour Operations Management Suite, hello seguintes pacotes de gerenciamento são instalados no Operations Manager quando você adicionar essa solução. Não há nenhuma manutenção nem configuração obrigatória destes pacotes de gerenciamento:

- Pacote de Inteligência do Coletor de Dados DNS da Microsoft (Microsft.IntelligencePacks.Dns)
- Configuração da Análise de DNS do Microsoft System Center Advisor (Microsoft.IntelligencePack.Dns.Configuration)

Para obter mais informações sobre como os pacotes de gerenciamento da solução são atualizados, consulte [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Usar a solução de análise de DNS de saudação

Esta seção explica todas as funções de painel hello e como toouse-los.

Depois de adicionar espaço de trabalho do hello solução tooyour, Olá solução lado a lado na página de visão geral do Operations Management Suite Olá fornece um resumo de sua infraestrutura DNS. Ele inclui o número de saudação de servidores DNS onde dados hello está sendo coletados. Ele também inclui o número de saudação de solicitações feitas por clientes tooresolve mal-intencionado domínios Olá últimas 24 horas. Quando você clica em bloco hello, painel de solução de saudação é aberto.

![bloco Análise de DNS](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Painel da solução

Painel de solução de saudação mostra informações resumidas para Olá vários recursos de solução de saudação. Ele também inclui links toohello detalhadas de exibição de diagnóstico e análise forense. Por padrão, dados de saudação são mostrados para Olá últimos sete dias. Você pode alterar o intervalo de data e hora hello usando Olá **controle de seleção de data e hora**, conforme mostrado no Olá a imagem a seguir:

![Controle de seleção de hora](./media/log-analytics-dns/dns-time.png)

Painel de solução Olá mostra Olá folhas a seguir:

**Segurança DNS**. Relatórios Olá clientes DNS que estão tentando toocommunicate com domínios mal-intencionados. Usando feeds do Microsoft threat intelligence, análise de DNS pode detectar IPs que estão tentando domínios mal-intencionado tooaccess de cliente. Em muitos casos, os dispositivos infectados por malware "discar" toohello "comando e controle" Centro de saudação mal-intencionado domínio Resolvendo Olá nome de domínio de malware.

![folha Segurança DNS](./media/log-analytics-dns/dns-security-blade.png)

Quando você clica em um IP de cliente na lista de hello, pesquisa de Log abre e mostra detalhes de pesquisa de saudação de consulta respectivos hello. Olá exemplo a seguir, análise de DNS detectados que comunicação Olá foi feita com um [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Resultados da pesquisa de logs mostrando ircbot](./media/log-analytics-dns/ircbot.png)

Olá informação ajuda você a tooidentify a:

- Cliente IP que iniciou a comunicação de saudação.
- Nome de domínio que seja resolvido IP mal-intencionado toohello.
- Resolve endereços IP que Olá nome de domínio.
- O endereço IP mal-intencionado.
- Severidade do problema de saudação.
- Motivo para a lista negra de IP mal-intencionado hello.
- O tempo de detecção.

**Domínios Consultados**. Fornece os nomes de domínio mais frequentes hello está sendo consultados por clientes do hello DNS em seu ambiente. Você pode exibir a lista de saudação de todos os nomes de domínio Olá consultada. Você também pode fazer drill down nos detalhes de solicitação de pesquisa Olá de um nome de domínio específico na pesquisa de Log.

![Folha Domínios Consultados](./media/log-analytics-dns/domains-queried-blade.png)

**Clientes DNS**. Relatórios Olá clientes *violação de limite de saudação* para o número de consultas em Olá escolhido o período de tempo. Você pode exibir a lista de saudação de todos os clientes DNS de saudação e detalhes de Olá Olá consultas feitas pelo-los na pesquisa de Log.

![Folha Clientes DNS](./media/log-analytics-dns/dns-clients-blade.png)

**Registros de DNS Dinâmico**. Relata as falhas de registro de nome. Todas as falhas de registro de endereço [registros de recursos](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (tipo A e AAAA) são realçados com cliente Olá IPs que são feitas solicitações de registro de saudação. Você pode usar este causa do informações toofind Olá de falha no registro de saudação seguindo estas etapas:

1. Localize a zona Olá autoritativo para nome Olá Olá cliente está tentando tooupdate.

2. Use informações de inventário de Olá Olá solução toocheck da zona.

3. Verifique se que a atualização dinâmica Olá zona Olá estiver ativado.

4. Verifique se a zona hello está configurada para atualização dinâmica, ou não.

    ![folha Registros de DNS Dinâmico](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Solicitações de registro de nome**. lado a lado superior Olá mostra uma linha de tendência de solicitações de atualização dinâmica de DNS bem-sucedidas e com falha. lado a lado inferior Olá lista clientes de 10 principais de saudação que estão enviando solicitações com falha de atualização DNS toohello os servidores DNS, classificados pelo número de saudação de falhas.

![folha Solicitações de registro de nome ](./media/log-analytics-dns/name-reg-req-blade.png)

**Consultas de Análise de DDI de Exemplo**. Contém uma lista hello mais comuns de consultas de pesquisa que buscar os dados brutos de análise diretamente.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de exemplo](./media/log-analytics-dns/queries.png)

Você pode usar essas consultas como um ponto de partida para criar suas próprias consultas para relatórios personalizados. consultas de saudação do link toohello página de pesquisa de Log de análise de DNS onde os resultados são exibidos:

- **Lista de Servidores DNS**. Mostra uma lista de todos os servidores DNS com seus FQDNs, nomes de domínio, nomes da floresta e IPs de servidor associados.
- **Lista de Zonas DNS**. Mostra uma lista de todas as zonas DNS com o nome da zona associada hello, status de atualização dinâmica, servidores de nome e status de assinatura de DNSSEC.
- **Registros de Recursos não Utilizados**. Mostra uma lista de todos os registros de recursos não utilizados/obsoleta hello. Essa lista contém o nome do registro de recurso hello, tipo de registro de recurso, Olá associado servidor DNS, o tempo de geração de registro e nome da zona. Você pode usar essa lista tooidentify Olá registros de recursos que não estão mais em uso. Com base nessas informações, você pode remover, em seguida, essas entradas de servidores DNS de saudação.
- **Carga de Consulta de Servidores DNS**. Mostra informações de forma que você pode obter uma perspectiva de saudação que carregar DNS nos servidores DNS. Essas informações podem ajudá-lo a planejar a capacidade de saudação para servidores de saudação. Você pode ir toohello **métricas** guia visualização gráfica do tooa toochange Olá exibição. Este modo de exibição o ajuda a entender como Olá carregar DNS é distribuído entre os servidores DNS. Ela mostra as tendências da taxa de consulta DNS para cada servidor.

    ![Resultados da pesquisa de logs de consulta de servidores DNS](./media/log-analytics-dns/dns-servers-query-load.png)

- **Carga de Consulta de Zonas DNS**. Mostra Olá estatísticas de consulta zona por segundo do DNS de todas as zonas de saudação em servidores DNS Olá sendo gerenciados pelo Gerenciador de saudação. Clique em Olá **métricas** guia toochange Olá modo de visualização de gráfico de tooa registros detalhados de resultados de saudação.
- **Eventos de Configuração**. Mostra todos os eventos de alteração de configuração de DNS hello e mensagens associadas. Em seguida, você pode filtrar esses eventos com base na hora do servidor DNS do evento, ID de evento, hello, ou a categoria da tarefa. dados de saudação podem ajudá-lo a auditoria dos servidores DNS de toospecific as alterações feitas em momentos específicos.
- **Log Analítico de DNS**. Mostra todos os eventos analíticos de saudação em todos os servidores DNS Olá gerenciados por solução hello. Em seguida, você pode filtrar esses eventos com base na hora do servidor DNS do evento, ID de evento, Olá, IP do cliente que fez Olá consulta de pesquisa e categoria de tipo de tarefa de consulta. Eventos analíticos do servidor DNS permitem atividade de controle no servidor DNS hello. Um evento analítico é registrado sempre que o servidor de saudação envia ou recebe informações de DNS.

### <a name="search-by-using-dns-analytics-log-search"></a>Pesquisar usando a Pesquisa de Logs da Análise de DNS

Na página de pesquisa de Log hello, você pode criar uma consulta. Você pode filtrar os resultados da pesquisa usando controles de faceta. Você também pode criar consultas avançadas tootransform, filtrar e relatar seus resultados. Iniciar usando Olá consultas a seguir:

1. Em Olá **caixa Pesquisa**, tipo `Type=DnsEvents` tooview todos Olá eventos DNS gerados por servidores DNS Olá gerenciados por solução hello. dados de log Olá para todos os eventos relacionados toolookup consultas, registros dinâmicos e alterações de configuração de lista de resultados de saudação.

    ![Pesquisa de logs de DnsEvents](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. dados de log de saudação tooview para consultas de pesquisa, selecione **LookUpQuery** como Olá **subtipo** filtro de controle de faceta Olá Olá esquerda. Uma tabela que lista todos os eventos de consulta de pesquisa Olá Olá para o período de tempo selecionado é exibida.

    b. dados de log de saudação tooview para registros dinâmicos, selecione **DynamicRegistration** como Olá **subtipo** filtro de controle de faceta Olá Olá esquerda. Uma tabela que lista todos os eventos de registro dinâmico Olá para Olá período de tempo selecionado é exibida.

    c. dados de log de saudação tooview para alterações de configuração, selecione **ConfigurationChange** como Olá **subtipo** filtro de controle de faceta Olá Olá esquerda. Uma tabela que lista todos os eventos de alteração de configuração Olá para Olá período de tempo selecionado é exibida.

2. Em Olá **caixa Pesquisa**, tipo `Type=DnsInventory` tooview todos Olá dados relacionados ao inventário DNS para os servidores DNS Olá gerenciados por solução hello. dados de log de saudação para servidores DNS, zonas DNS e registros de recursos de lista de resultados de saudação.

    ![Pesquisa de logs de DnsInventory](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Comentários

Há duas maneiras de enviar comentários:

- **UserVoice**. Poste ideias para toowork de recursos de análise de DNS no. Visite Olá [Operations Management Suite UserVoice página](https://aka.ms/dnsanalyticsuservoice).
- **Ingressar em nosso coorte**. Sempre estamos interessados em ter novos clientes ingressar nossos recursos de toonew acesso antecipado do tooget colaboradores e ajude-na melhorar a análise de DNS. Se estiver interessado em participar de nossos coortes, preencha esta [pesquisa rápida](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Próximas etapas

[Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas registros de log DNS.
