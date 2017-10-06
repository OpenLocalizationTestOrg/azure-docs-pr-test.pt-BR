---
title: aaaLog perguntas frequentes sobre o Analytics | Microsoft Docs
description: "Toofrequently respostas perguntas frequentes sobre Olá serviço de análise de logs do Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Perguntas frequentes do Log Analytics
Essas Perguntas Frequentes da Microsoft são uma lista de perguntas frequentes sobre o Log Analytics no Microsoft Operations Management Suite (OMS). Se você tiver alguma dúvida sobre a análise de Log, vá toohello [Fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) e publique suas perguntas. Quando uma pergunta é frequentes, vamos adicioná-lo toothis artigo para que ele pode ser encontrado rapidamente e facilmente.

## <a name="general"></a>Geral

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>P. Usar a análise de Log Olá mesmo agente como Central de segurança do Azure?

R. No início de junho de 2017, Central de segurança do Azure começou usando dados de toocollect e armazenamento do Microsoft Monitoring Agent hello. mais, consulte toolearn [perguntas frequentes sobre o Azure Security Center plataforma migração](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>P. Quais verificações são executadas por hello AD e soluções de avaliação de SQL?

R. Olá, consulta a seguir mostra uma descrição de todas as verificações executadas no momento:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Olá resultados podem ser exportado tooExcel para análise adicional.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>P: Por que vejo algo diferente de *OMS* no console do System Center Operations Manager?

R: Dependendo do Pacote Cumulativo de Atualizações do Operations Manager em que você estiver, poderá ver um nó para *System Center Advisor*, *Insights Operacionais* ou *Log Analytics*.

Olá atualização de cadeia de caracteres de texto muito*OMS* está incluído no pacote de gerenciamento, que deve toobe importado manualmente. texto atual do toosee hello e funcionalidade, siga as instruções de Olá Olá mais recente System Center Operations Manager Update Rollup KB artigo e atualização Olá console.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>P: Há uma versão *local* do Log Analytics?

R: não. O Log Analytics processa e armazena grandes quantidades de dados. Como um serviço de nuvem, análise de Log é capaz de tooscale o se necessário e evitar qualquer ambiente de tooyour do impacto de desempenho.

Benefícios adicionais incluem:
- Microsoft executando a infraestrutura de análise de Log hello, economizando custos
- Implantação regular de atualizações e correções de recurso.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>P. Como fazer para realizar a solução de problemas quando o Log Analytics não está mais coletando dados?

R: se você estiver no hello livre de preço e enviou mais de 500 MB de dados em um dia, para de coleta de dados para o resto de saudação do dia de saudação. Limite diário de saudação alcance é um motivo comum de análise de Log interromperá a coleta de dados ou dados aparecem toobe ausente.

O Log Analytics cria um evento de tipo *Operação* quando a coleta de dados inicia e para. 

Execute Olá consulta no toocheck de pesquisa a seguir se você atingir o limite diário hello e dados ausentes:`Type=Operation OperationCategory="Data Collection Status"`

Quando a coleta de dados para, hello *OperationStatus* é **aviso**. Quando a coleta de dados é iniciada, hello *OperationStatus* é **êxito**. 

Olá, tabela a seguir descreve os motivos que interrompe a coleta de dados e um conjunto de dados tooresume ação sugerida:

| Motivo para a coleta de dados ser interrompida                       | coleta de dados tooresume |
| -------------------------------------------------- | ----------------  |
| Limite diário de dados gratuito atingido<sup>1</sup>       | Aguarde Olá após um dia para a coleção tooautomatically reinicialização, ou<br> Alterar tooa paga o preço |
| Assinatura do Azure está em um estado suspenso devido a: <br> A avaliação gratuita terminou <br> O Azure Pass expirou <br> Limite de gastos mensal atingido (por exemplo, em uma assinatura do MSDN ou do Visual Studio)                          | Converter tooa assinatura paga <br> Converter tooa assinatura paga <br> Remova o limite ou espere o limite ser redefinido |

<sup>1</sup> se o seu espaço de trabalho está Olá livre de preço, está limitado toosending 500 MB de dados por serviço de toohello do dia. Quando você atingir o limite diário hello, coleta de dados para até Olá dia seguinte. Dados enviados enquanto a coleta de dados está interrompida não são indexados e não ficam disponíveis para pesquisa. Quando a coleta de dados é retomada, o processamento ocorre apenas para os novos dados enviados. 

O Log Analytics usa o horário UTC e cada dia inicia à meia-noite UTC. Se o espaço de trabalho de saudação atinge o limite diário hello, o processamento será retomado durante a saudação primeira hora de saudação dia UTC.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>P. Como posso ser notificado quando a coleta de dados for interrompida?

R: siga etapas Olá descritas em [criar uma regra de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notificado quando a coleta de dados é interrompida.

Ao criar o alerta Olá para quando a coleta de dados para, defina o:
- **Nome** muito*parada de coleta de dados*
- **Severidade** muito*aviso*
- **Consulta de pesquisa** muito`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Janela de tempo** muito*2 horas*.
- **Frequência de alerta** toobe uma hora, como dados de uso de saudação atualiza somente uma vez por hora.
- **Gerar alerta com base em** toobe *número de resultados*
- **Número de resultados** toobe *maior que 0*

Usar Olá etapas descritas [adicionar regras de tooalert ações](log-analytics-alerts-actions.md) configurar uma ação de email, webhook ou runbook para regra de alerta de saudação.


## <a name="configuration"></a>Configuração
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>P. Alterar nome de saudação do hello tabela/blob contêiner usado tooread do diagnóstico do Azure (WAD)?

R. Não, não é possível no momento tooread de tabelas arbitrárias ou contêineres no armazenamento do Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>P. Quais endereços IP hello o uso do serviço de análise de Log? Como garantir que meu firewall permita apenas serviço de análise de logs do tráfego toohello?

R. saudação de serviço de análise de Log é criada no Azure. Endereços de IP de análise de log estão em Olá [intervalos de IP de Datacenter do Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653).

As implantações de serviço são feitas, alterar endereços IP reais de saudação do hello serviço de análise de Log. Olá tooallow de nomes DNS através do firewall são documentados em [definir configurações de proxy e firewall na análise de Log](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>P. Usar o ExpressRoute para conectar-se tooAzure. O meu tráfego do Log Analytics usará minha conexão ExpressRoute?

R. Olá diferentes tipos de tráfego de rota expressa são descritos em Olá [documentação de rota expressa](../expressroute/expressroute-faqs.md#supported-services).

Tráfego tooLog Analytics usa o circuito de rota expressa de emparelhamento público hello.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>P. Há uma maneira simples e fácil toomove um tooanother de espaço de trabalho de análise de Log assinatura do Azure/espaço de trabalho de análise de Log existente?

R. Olá `Move-AzureRmResource` cmdlet permite que você mova um espaço de trabalho de análise de Log, além de uma conta de automação de tooanother de uma assinatura do Azure. Para obter mais informações, consulte [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Essa alteração pode ser feita também no hello portal do Azure.

Você não pode mover dados de um tooanother de espaço de trabalho de análise de Log, ou alterar a região Olá que dados de análise de Log são armazenados em.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>P: como adicionar Log Analytics tooSystem Center Operations Manager?

R: a atualização de pacote cumulativo de atualização mais recente toohello e importar pacotes de gerenciamento permite que você tooconnect do Operations Manager tooLog análise.

>[!NOTE]
>saudação do Operations Manager conexão tooLog análise só está disponível para o System Center Operations Manager 2012 SP1 e posterior.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>P: como posso confirmar que um agente é capaz de toocommunicate com análise de Log?

R: tooensure que o agente Olá pode se comunicar com o OMS, vá para: painel de controle, segurança e configurações, **Microsoft Monitoring Agent**.

Em Olá **Azure Log Analytics (OMS)** guia, procure por uma marca de seleção verde. Um ícone de marca de seleção verde confirma que o agente de saudação é capaz de toocommunicate com hello serviço OMS.

Um ícone de aviso amarelo significa que o agente de saudação está tendo problemas de comunicação com o OMS. Uma razão comum é Olá serviço Microsoft Monitoring Agent foi interrompido. Use o serviço de saudação toorestart do Gerenciador de controle de serviço.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>P: Como fazer para impedir que um agente de se comunicar com o Log Analytics?

R: no System Center Operations Manager, remova o computador de Olá da lista de computadores gerenciados do Advisor hello. Atualizações do Operations Manager Olá configuração de saudação agente toono mais relatório tooLog análise. Para agentes conectados diretamente a tooLog análise, você pode interrompê-los de se comunicar por meio de: painel de controle, segurança e configurações, **Microsoft Monitoring Agent**.
Em **Azure Log Analytics (OMS)**, remova todos os espaços de trabalho listados.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>P: por que estou recebendo um erro quando tento toomove meu espaço de trabalho em uma assinatura do Azure tooanother?

R: se você estiver usando Olá portal do Azure, certifique-se de espaço de trabalho apenas Olá é selecionado para mover hello. Não selecione soluções Olá - moverá automaticamente depois que o espaço de trabalho Olá move. 

Verifique se você tem permissão em ambas as assinaturas do Azure.

## <a name="agent-data"></a>Dados do agente
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>P. A quantidade de dados pode enviar por meio de saudação agente tooLog análise? Existe uma quantidade máxima de dados por cliente?
R. plano gratuito Olá define uma capacidade diária de 500 MB por espaço de trabalho. saudação padrão e planos premium não têm limite na quantidade de saudação de dados que são carregados. Como um serviço de nuvem, destina-se a análise de Log escala tooautomatically toohandle volume de hello proveniente de um cliente, mesmo que sejam terabytes por dia.

Agente de análise de Log Olá foi projetado tooensure tem uma superfície pequena. Um de nossos clientes escreveu um blog sobre testes de saudação que executaram em nosso agente e como ficaram impressionados. o volume de dados Olá varia de acordo com soluções de saudação que habilitar. Você pode encontrar informações detalhadas sobre o volume de dados hello e ver a divisão de saudação por solução Olá [uso](log-analytics-usage.md) página.

Para obter mais informações, você pode ler um [blog do cliente](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) sobre a baixa superfície saudação do agente do OMS hello.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>P. Quanta largura de banda de rede é usada pelo agente de gerenciamento da Microsoft (MMA) de saudação ao enviar dados tooLog análise?

R. Largura de banda é uma função na quantidade de saudação de dados enviados. Dados são compactados à medida que são enviados pela rede hello.

### <a name="q-how-much-data-is-sent-per-agent"></a>P. Qual a quantidade de dados enviada por agente?

R. saudação de dados enviados por agente depende:

* soluções de saudação habilitadas
* número de saudação de logs e contadores de desempenho coletados
* volume de saudação de dados nos logs de saudação

Olá livre de preço é uma boa maneira tooonboard vários servidores e volume de dados típicos de saudação do medidor. O uso geral é mostrado em Olá [uso](log-analytics-usage.md) página.

Para computadores que for possível toorun Olá WireData agente, use Olá toosee consulta quantos dados estão sendo enviados a seguir:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Próximas etapas
* [Introdução à análise de Log](log-analytics-get-started.md) toolearn mais sobre análise de logs e get em funcionamento em minutos.
