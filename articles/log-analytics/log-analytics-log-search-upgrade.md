---
title: pesquisa de log aaaUpgrading Azure Log Analytics toonew | Microsoft Docs
description: "nova linguagem de consulta de análise de Log Olá é quase aqui e você pode participar de visualização pública Olá.  Este artigo descreve as vantagens de saudação da nova linguagem de saudação e como tooconvert seu espaço de trabalho."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Atualizar sua pesquisa de log de toonew de espaço de trabalho de análise de logs do Azure

> [!NOTE]
> Atualização toohello nova linguagem de consulta de análise de Log é opcional no momento, dando muito tempo[aumentam em nova linguagem de saudação](https://go.microsoft.com/fwlink/?linkid=856078).  

nova linguagem de consulta de análise de Log Hello está aqui e você precisa tooupgrade seu espaço de trabalho tootake vantagens.  Este artigo descreve as vantagens de saudação da nova linguagem de saudação e como tooconvert seu espaço de trabalho.  Se você não escolher tooupgrade agora, seu espaço de trabalho continuarão toooperate exatamente como ele sempre fez, mas ele será convertido automaticamente em uma data posterior.  Você receberá a devida notificação e um tempo significativo quando essa data for definida.

Este artigo fornece detalhes sobre a nova linguagem de saudação e o processo de atualização de saudação.

## <a name="why-hello-new-language"></a>Olá por que o novo idioma?
Compreendemos que há problemas em qualquer transição e não são apenas alterar linguagem de consulta de saudação para diversão hello.  Há várias razões que essa alteração fornecem valor significativo tooour clientes de análise de Log.

- **Simples mas poderosa.** Olá novo idioma está toounderstand mais fácil e semelhante tooSQL com construções mais como natural idioma Olá herdado.
- **Linguagem totalmente por piping.**  nova linguagem de saudação tem recursos de pipe mais amplo de linguagem herdada hello.  Praticamente qualquer saída pode ser toocreate de comando canalizado tooanother consultas mais complexas do que era possível anteriormente.
- **Extrações de campo de tempo de pesquisa.**  nova linguagem de saudação dá suporte a mais avançados campos calculado em tempo de execução que linguagem herdados Olá.  Você pode usar cálculos complexos para os campos estendidos e, em seguida, usar campos de saudação calculado para comandos adicionais, incluindo junções e agregações.
- **Junções avançadas.**  nova linguagem de saudação fornece junções mais avançadas que linguagem herdados hello, incluindo Olá capacidade toojoin tabelas em vários campos, use junções internas e externas e associar campos estendidos.
- **Funções de data/hora.**  nova linguagem de saudação tem mais avançados funções de data/hora que linguagem herdados hello.
- **Análise inteligente.**  nova linguagem de saudação avançou padrões de tooevaluate algoritmos em conjuntos de dados e compare diferentes conjuntos de dados.
- **Portal Análise Avançada.**  portal de análise avançada Hello oferece recursos de análise não disponíveis no portal de análise de Log de Olá, incluindo várias linhas edição de consultas, visualizações adicionais e diagnósticos avançados.
- **Consistência com outros aplicativos.**  Olá Olá e nova linguagem de Portal da análise avançada já são usados para análise no Application Insights.  Implementá-la para o Log Analytics proporciona consistência entre os serviços do Azure.
- **Melhor integração com o Power BI.** Consultas em linguagem novo Olá podem ser exportado tooPower BI Desktop, portanto, você pode utilizar seus recursos de transformação de dados avançados.
- **E muito mais.** Consulte toohello [linguagem de consulta do Azure Log Analytics](https://docs.loganalytics.io) detalhes completos e tutoriais sobre a nova linguagem de saudação do site.


## <a name="when-can-i-upgrade"></a>Quando posso fazer a atualização?
atualização de saudação será lançada em todas as regiões do Azure para que ele pode estar disponível em algumas regiões antes de outros.  Você saberá quando o seu espaço de trabalho é atualizado quando você vir a faixa de saudação roxas na parte superior de saudação do seu espaço de trabalho convidar você tooupgrade de toobe disponível.

![Atualização 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>O que acontece quando eu faço a atualização?
Quando você converte seu espaço de trabalho, qualquer pesquisas salvas, regras de alerta e modos de exibição que você criou com hello Designer de exibição são automaticamente convertidos toohello novo idioma.  Pesquisas incluídas em soluções não são convertidas automaticamente, mas em vez disso estiver convertidos imediatamente hello quando você abri-los.  Isso é completamente transparente tooyou.

## <a name="can-i-go-back-after-i-upgrade"></a>Posso voltar atrás depois de atualizar?
Quando você atualiza, é feito um backup completo de seu espaço de trabalho que inclui um instantâneo de todas as pesquisas, regras de alerta e exibições salvas.  Isso permite toorestore seu espaço de trabalho antigo se deve mais tarde desejar.

toorestore seu espaço de trabalho herdado, ir muito**configurações** no espaço de trabalho e, em seguida, **Resumo da atualização**.  Você pode selecionar a opção de saudação muito**restauração do espaço de trabalho herdado**.  

![Restaurar herdado](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Como executar a atualização Olá?
Você pode atualizar seu espaço de trabalho quando você vir a faixa de saudação roxas na parte superior de saudação do portal de saudação.  

1.  Iniciar o processo de atualização de saudação clicando na faixa de saudação roxo que diz **saber mais e atualizar**.<br>![Atualização 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Leia Olá obter informações adicionais sobre atualização Olá na página de informações de atualização de saudação.<br>![Atualização 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Clique em **atualizar agora** toostart atualização de saudação.<br>![Atualização 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Uma caixa de notificação no canto superior direito da saudação mostra o status de saudação.<br>![Atualização 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  É isso!  Examine toohave de página de pesquisa de Log de toohello uma olhada em seu espaço de trabalho atualizado.<br>![Atualização 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Se você encontrar um problema que causa Olá toofail de atualização, você pode ir toohello [Fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) e poste sua pergunta ou [criar uma solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md) de saudação portal do Azure.

## <a name="how-do-i-learn-hello-new-language"></a>Como saber o novo idioma de Olá?
Já que ela é usada por vários serviços, criamos um [documentação de saudação do site externo toohost](https://docs.loganalytics.io/) para nova linguagem de saudação.  Isso inclui os tutoriais, exemplos e toohelp uma referência completa que você criar toospeed. Você pode percorrer um tutorial do novo idioma Olá em [guia de Introdução com consultas](https://go.microsoft.com/fwlink/?linkid=856078) e acessar a referência de linguagem de saudação em [idioma de consulta de análise de Log](https://go.microsoft.com/fwlink/?linkid=856079).  

Se você já estiver familiarizado com hello herdados de análise de Log de linguagem de consulta que, então você pode usar o conversor de idioma Olá que foi adicionado tooyour espaço de trabalho como parte da atualização de saudação.

Basta digitar sua consulta herdada e, em seguida, clique em **converter** toosee Olá convertido versão.  Você pode clicar em Olá pesquisa botão toorun Olá pesquisa ou copiar e colar toouse de consulta Olá convertido em outro lugar, como uma regra de alerta.

![Conversor de linguagem](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Próximas etapas
- Check-out de um [tutorial sobre a nova linguagem de saudação](https://go.microsoft.com/fwlink/?linkid=856078).
- Percorrer um [tutorial sobre como usar o portal de pesquisa de Log de saudação](log-analytics-log-search-log-search-portal.md) com a nova linguagem de consulta hello.
- Obter uma introdução toohello novo [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587).
