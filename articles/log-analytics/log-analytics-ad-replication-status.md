---
title: "aaaMonitor status de replicação do Active Directory com o Azure Log Analytics | Microsoft Docs"
description: "saudação de pacote de solução de Status de replicação do Active Directory regularmente monitora o ambiente do Active Directory para as falhas de replicação e relata os resultados de saudação em seu painel do OMS."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Monitorar o status da replicação do Active Directory com o Log Analytics

![Símbolo do Status de Replicação do AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

O Active Directory é um componente-chave de um ambiente de TI corporativo. tooensure alta disponibilidade e alto desempenho, cada controlador de domínio tem sua própria cópia do banco de dados do Active Directory hello. Controladores de domínio repliquem uns com os outros em ordem toopropagate será alterado empresa Olá. Falhas neste processo de replicação podem causar uma variedade de problemas na empresa hello.

saudação de pacote de solução de Status de replicação do AD monitora o ambiente do Active Directory para as falhas de replicação e relata os resultados de saudação em seu painel do OMS regularmente.

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação.

* Você deve instalar agentes em controladores de domínio que são membros de saudação domínio toobe avaliada. Ou, você deve instalar agentes em servidores membros e configurar Olá agentes toosend AD replicação dados tooOMS. toounderstand como tooconnect tooOMS de computadores Windows, consulte [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md). Se o controlador de domínio já é parte de um ambiente existente do System Center Operations Manager que você deseja tooconnect tooOMS, consulte [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md).
* Adicionar tooyour de solução de Status de replicação do Active Directory Olá espaço de trabalho do OMS usando Olá processo descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).  Não é necessária nenhuma configuração.

## <a name="ad-replication-status-data-collection-details"></a>Detalhes de coleta de dados do Status de Replicação do AD
Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o Status da replicação do AD.

| plataforma | Agente direto | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |a cada cinco dias |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Se desejar, habilite um tooOMS de dados do controlador de domínio não toosend AD
Se não quiser tooconnect qualquer um dos seus controladores de domínio diretamente tooOMS, você pode usar qualquer outro computador conectado OMS em toocollect seu domínio, dados de saudação solução de Status de replicação do AD do pacote e que envie dados saudação.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable um tooOMS de dados do controlador de domínio não toosend AD
1. Verifique se o que computador Olá é um membro do domínio Olá que você deseja toomonitor usando o Gerenciador de Status de replicação Olá AD.
2. [Conecte-se tooOMS de computador do Windows hello](log-analytics-windows-agents.md) ou [conectá-lo usando o tooOMS de ambiente existente do Operations Manager](log-analytics-om-agents.md), se ainda não está conectado.
3. No computador, defina Olá chave do registro a seguir:

   * Chave: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * Valor: **IsTarget**
   * Dados do Valor: **true**

   > [!NOTE]
   > Essas alterações não entram em vigor até que sua saudação de reinicialização do serviço Microsoft Monitoring Agent (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Entendendo erros de replicação
Uma vez que dados de status de replicação do AD enviados tooOMS, você verá um toohello semelhante de bloco de imagem a seguir no painel do OMS Olá indicando quantos erros de replicação no momento.  
![Bloco do Status de Replicação do AD](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Erros de replicação crítica** erros que estão em ou acima de 75% de saudação [desativação](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) para a floresta do Active Directory.

Quando você clica em bloco hello, você pode exibir mais informações sobre erros de saudação.
![Painel Status de Replicação do AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Status do Servidor de Destino e Status do Servidor de Origem
Essas colunas mostram o status de saudação do servidores de destino e os servidores de origem que estão apresentando erros de replicação. número de saudação depois de cada nome de controlador de domínio indica o número de saudação de erros de replicação no controlador de domínio.

erros de saudação para servidores de destino e os servidores de origem são mostrados como alguns problemas são tootroubleshoot mais fácil da perspectiva de servidor de origem hello e outras pessoas da perspectiva de servidor de destino de saudação.

Neste exemplo, você pode ver que muitos servidores de destino têm aproximadamente Olá o mesmo número de erros, mas não há um servidor de origem (ADDC35) que tem muitos mais erros que Olá todos os outros. É provável que haja algum problema no ADDC35 que está causando parceiros de replicação toofail toosend dados tooits. Corrigir problemas de saudação em ADDC35 pode resolver muitos dos erros de saudação que aparecem na área de servidor de destino de saudação.

### <a name="replication-error-types"></a>Tipos de Erros de Replicação
Esta área fornece informações sobre tipos de saudação de erros detectados em toda a empresa. Cada erro tem um código numérico exclusivo e uma mensagem que pode ajudá-lo a determinar a causa raiz de saudação do erro de saudação.

rosca Olá na parte superior da saudação fornece uma ideia do que os erros aparecem mais e menos frequentemente em seu ambiente.

Ele mostra quando vários controladores de domínio experimentam Olá mesmo erro de replicação. Nesse caso, você pode ser capaz de toodiscover ou identificar uma solução em um controlador de domínio e repita-o em outros controladores de domínio afetados por Olá mesmo erro.

### <a name="tombstone-lifetime"></a>tempo de vida da marca de exclusão
tempo de vida de desativação Olá determina quanto tempo um objeto excluído, chamado tooas uma marca de exclusão, é mantido no banco de dados do Active Directory hello. Quando um tempo de desativação do objeto excluído passa hello, um processo de coleta de lixo automaticamente a remove do banco de dados do Active Directory hello.

tempo de vida de desativação do saudação padrão é de 180 dias para versões mais recentes do Windows, mas era 60 dias em versões anteriores e pode ser alterado explicitamente por um administrador do Active Directory.

É importante tooknow se você estiver tendo erros de replicação que estão se aproximando ou ultrapassaram o tempo de desativação de saudação. Se dois controladores de domínio tiver um erro de replicação que persiste após a desativação Olá, é desabilitar a replicação entre os dois controladores de domínio, mesmo se Olá erro de replicação subjacente é fixo.

Olá área de desativação ajuda a identificar os locais onde o desabilitado a replicação está em risco de acontecer. Cada erro no hello **mais de 100% TSL** categoria representa uma partição que não foi replicado entre seu servidor de origem e destino para em menos tempo de desativação de saudação para floresta hello.

Nessa situação, simplesmente corrigir o erro de replicação de saudação não será suficiente. No mínimo, você precisa toomanually investigar tooidentify e limpar os objetos remanescentes, antes de reiniciar a replicação. Até mesmo talvez seja necessário toodecommission um controlador de domínio.

Em adição tooidentifying os erros de replicação tem persistido após o tempo de vida de desativação Olá, você também quer que toopay atenção tooany os erros se enquadram Olá **TLS de 50 a 75%** ou **TSL 100 75%** categorias.

Esses são erros que são claramente remanescentes, não é transitório, portanto, provavelmente precisam tooresolve sua intervenção. Olá boa notícia é que não tenham ainda atingido o tempo de desativação hello. Se você corrigir esses problemas imediatamente e *antes de* atingem o tempo de desativação hello, a replicação pode reiniciar com mínima intervenção manual.

Conforme observado anteriormente, o bloco do dashboard Olá para solução de Status de replicação Olá AD mostra o número de Olá de *crítico* erros de replicação em seu ambiente, que é definido como erros que são mais de 75% de tempo de vida de desativação (incluindo erros que são mais de 100% de TLS). Buscar tookeep esse número em 0.

> [!NOTE]
> Todos os cálculos de porcentagem Olá tombstone tempo de vida se baseiam em tempo de desativação real de saudação para a floresta do Active Directory, para que você pode confiar que essas porcentagens são precisas, mesmo se você tiver um valor de tempo de vida de desativação personalizado definido.
>
>

### <a name="ad-replication-status-details"></a>Detalhes do status de Replicação do AD
Quando você clicar em qualquer item em uma das listas de Olá, você pode ver detalhes adicionais sobre ele usando a pesquisa de Log. resultados de saudação são item do tooshow filtrado somente Olá erros toothat relacionados. Por exemplo, se você clicar no primeiro controlador de domínio Olá listado em **o Status do servidor de destino (ADDC02)**, você verá resultados filtrados tooshow erros com esse controlador de domínio listado como servidor de destino de saudação:

![Erros de status de replicação do AD nos resultados da pesquisa](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

A partir daqui, você pode filtrar ainda mais, modificar a consulta de pesquisa hello e assim por diante. Para obter mais informações sobre como usar o hello pesquisa de Log, consulte [pesquisas de Log](log-analytics-log-searches.md).

Olá **HelpLink** campo mostra a URL de saudação de uma página do TechNet com detalhes adicionais sobre esse erro específico. Você pode copiar e colar esse link em suas informações de toosee de janela de navegador sobre solução de problemas e corrigindo erros de saudação.

Você também pode clicar em **exportar** tooexport Olá tooExcel os resultados. Exportando dados Olá pode ajudar a visualizar dados de erro de replicação de qualquer forma que você deseja.

![erros de status de replicação de AD exportados no Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>Perguntas frequentes do Status de Replicação do AD
**P: Com que frequência os dados de status de replicação do AD são atualizados?**
R: Olá informações são atualizadas a cada cinco dias.

**P: há um tooconfigure de forma que a frequência com que esses dados são atualizados?**
R: Não no momento.

**P: é necessário tooadd todos meu domínio controladores toomy OMS espaço de trabalho no status de replicação de toosee ordem?**
R: Não, apenas um único controlador de domínio deve ser adicionado. Se você tiver vários controladores de domínio em seu espaço de trabalho do OMS, dados de todos eles são enviados tooOMS.

**P: eu não quero tooadd qualquer espaço de trabalho OMS de toomy de controladores de domínio. É possível ainda usar Olá solução de Status de replicação do AD?**
R: Sim. Você pode definir o valor de saudação de um tooenable de chave do registro-lo. Consulte [tooenable um tooOMS de dados do controlador de domínio não toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**P: qual é o nome de saudação do processo Olá Olá a coleta de dados?**
R: AdvisorAssessment.exe

**P: quanto tempo leva para toobe dados coletado?**
R: tempo de coleta de dados depende do tamanho de saudação do ambiente do Active Directory hello, mas geralmente leva menos de 15 minutos.

**P: Que tipo de dados é coletado?**
R: Informações de replicação são coletadas por meio do LDAP.

**P: há uma maneira tooconfigure quando os dados são coletados?**
R: Não no momento.

**P: o que fazem permissões preciso toocollect dados?**
R: permissões de usuário normal de tooActive diretório são suficientes.

## <a name="troubleshoot-data-collection-problems"></a>Solucionar problemas de coleta de dados
Dados de pedidos toocollect, o pacote de soluções de Status de replicação Olá AD requer pelo menos um domínio controlador toobe conectado tooyour OMS espaço de trabalho. Até você conectar um controlador de domínio, será exibida uma mensagem indicando que os **dados ainda estão sendo coletados**.

Se você precisar de assistência para conectar um dos seus controladores de domínio, você pode exibir a documentação em [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md). Como alternativa, se o controlador de domínio já está conectado tooan ambiente System Center Operations Manager, você pode exibir a documentação em [tooLog conectar o System Center Operations Manager análise](log-analytics-om-agents.md).

Se você não quiser tooconnect qualquer um dos seus controladores de domínio diretamente tooOMS ou tooSCOM, consulte [tooenable um tooOMS de dados do controlador de domínio não toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de status de replicação do Active Directory.
