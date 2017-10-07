---
title: "aaaGetting de Introdução ao Operations Management Suite solução de segurança e auditoria | Microsoft Docs"
description: "Este documento Introdução você tooget com toomonitor de recursos de solução de segurança do Operations Management Suite e auditoria sua nuvem híbrida."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Introdução à solução de Segurança e Auditoria do Operations Management Suite
Este documento o ajuda a se familiarizar rapidamente com as funcionalidades da solução de Auditoria e Segurança do OMS (Operations Management Suite) explicando cada uma das opções.

## <a name="what-is-oms"></a>O que é o OMS?
O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Para obter mais informações sobre o OMS, leia o artigo de saudação [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Painel Segurança e Auditoria do OMS
Olá solução do OMS segurança e auditoria fornece uma visão abrangente da sua organização postura de segurança de TI com consultas de pesquisa interna para problemas importantes que exigem sua atenção. Olá **segurança e auditoria** dashboard é a tela inicial Olá para tudo relacionado toosecurity no OMS. Ele fornece informações de alto nível em estado de segurança de saudação de seus computadores. Ele também inclui Olá capacidade tooview todos os eventos de saudação nas últimas 24 horas, 7 dias, ou qualquer outro período de tempo personalizado. Olá tooaccess **segurança e auditoria** painel, siga estas etapas:

1. Em Olá **Microsoft Operations Management Suite** clique de painel principal **configurações** lado a lado no hello esquerdo.
2. Em Olá **configurações** folha, em **soluções** clique **segurança e auditoria** opção.
3. Olá **segurança e auditoria** painel é exibido:
   
    ![Painel Segurança e Auditoria do OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Se você estiver acessando este painel para Olá primeira vez e você não tem dispositivos monitorados pelo OMS, Olá blocos não serão populados com dados obtidos do agente de saudação. Depois de instalar o agente hello, pode levar algum tempo toopopulate, portanto, o que é exibido inicialmente pode estar faltando alguns dados conforme eles ainda estão carregando toohello nuvem.  Nesse caso, é normal toosee alguns blocos sem informações tangíveis. Leitura [conectar computadores Windows diretamente tooOMS](https://technet.microsoft.com/library/mt484108.aspx) para obter mais informações sobre como agente do OMS tooinstall em um sistema Windows e [tooOMS de computadores Linux conectar](https://technet.microsoft.com/library/mt622052.aspx) para obter mais informações sobre como tooperform esta tarefa em um sistema Linux.

> [!NOTE]
> agente Olá coleta informações de saudação com base em Olá atual eventos que são habilitados, por exemplo, nome do computador, nome de usuário e endereço IP. No entanto, nenhum documento/arquivo, nome de banco de dados ou dado privado será coletado.   
> 
> 

as soluções são uma coleção de regras de lógica, de visualização e de aquisição de dados que abordam os principais desafios dos clientes. Segurança e Auditoria é uma solução; outras podem ser adicionadas separadamente. Leia o artigo Olá [adicionar soluções](https://technet.microsoft.com/library/mt674635.aspx) para obter mais informações sobre como tooadd uma nova solução.

painel do OMS segurança e auditoria Olá é organizada em quatro categorias principais:

* **Domínios de segurança**: nesta área, você será capaz de toofurther explorar registros de segurança ao longo do tempo, acessar avaliação de malware, atualize a avaliação, segurança de rede, informações de identidade e acesso, computadores com eventos de segurança e ter rapidamente Painel de Central de segurança do acesso tooAzure.
* **Problemas importantes**: esta opção permitirá tooquickly identificar Olá número de problemas ativos e Olá severidade desses problemas.
* **Detecções (visualização)**: permite que os padrões de ataque tooidentify visualizando alertas de segurança conforme eles ocorrem em relação a seus recursos.
* **Inteligência de ameaça**: permite que os padrões de ataque tooidentify visualizando o número total de saudação de servidores com saída tráfego IP mal-intencionado, tipo de ameaça mal-intencionado hello e um mapa que mostra onde esses IPs são provenientes. 
* **Consultas comuns de segurança**: essa opção fornece uma lista de segurança mais comuns de saudação consultas que você pode usar toomonitor seu ambiente. Quando você clicar em uma das consultas, ele abre Olá **pesquisa** folha com resultados Olá para a consulta.

> [!NOTE]
> para obter mais informações sobre como o OMS mantém seus dados seguros, leia Como o OMS protege seus dados.
> 
> 

## <a name="security-domains"></a>Domínios de segurança
Quando o monitoramento de recursos, é importante toobe tooquickly capaz de acesso Olá estado atual do seu ambiente. No entanto também é toobe importante tootrack capaz de eventos back que ocorreram em Olá anterior que pode levar tooa melhor compreensão do que está acontecendo em seu ambiente em determinado ponto no tempo. 

> [!NOTE]
> retenção de dados está de acordo com toohello plano de preços do OMS. Para obter mais informações, visite Olá [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) página de preços.
> 
> 

Cenários de investigação de resposta e análise forense incidente diretamente se beneficiará de resultados de saudação disponíveis no hello **registros de segurança ao longo do tempo** lado a lado.

![Registros de segurança ao longo do tempo](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Quando você clicar nesse bloco, Olá **pesquisa** folha será aberta, mostrando um resultado de consulta para **eventos de segurança** (tipo = SecurityEvents) com dados com base em Olá últimos sete dias, conforme mostrado abaixo:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Registros de segurança ao longo do tempo](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

resultado da pesquisa Olá é dividido em dois painéis: painel esquerdo Olá fornece uma análise do número de saudação de eventos de segurança que foram encontrados, Olá computadores em que esses eventos foram encontradas, número de saudação de contas que foram descobertos nesses computadores e tipos de saudação de atividades. painel direito da saudação fornece resultados totais hello e uma exibição cronológica Olá de eventos de segurança com atividade de evento e de nome do computador hello. Você também pode clicar em **Mostrar mais** tooview mais detalhes sobre esse evento, como dados de evento de saudação, ID de evento hello e origem do evento hello.

> [!NOTE]
> Para obter mais informações sobre a consulta de pesquisa do OMS, leia a [referência de pesquisa do OMS](https://technet.microsoft.com/library/mt450427.aspx).
> 
> 

### <a name="antimalware-assessment"></a>Avaliação antimalware
Este permite opção tooquickly você identificar os computadores com proteção insuficiente e computadores que são comprometidos por um programa mal-intencionado. Avaliação de malware, status e ameaças detectadas nos servidores de saudação monitorada são lidas e hello, em seguida, os dados é enviada toohello serviço do OMS na nuvem Olá para processamento. Servidores com ameaças detectadas e servidores com proteção insuficiente são mostrados no painel de avaliação de malware hello, que pode ser acessada em hello **avaliação Antimalware** lado a lado. 

![avaliação de malware](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Assim como qualquer outro bloco dinâmico disponíveis no painel do OMS, quando você clica nele, Olá **pesquisa** folha será aberta com o resultado da consulta hello. Para essa opção, se você clicar em Olá **Reporting não** opção em **Status de proteção**, você terá que mostra essa única entrada que contém o nome do computador hello e sua classificação, como resultado da consulta Olá como mostrado abaixo:

![resultado da pesquisa](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *classificação* é uma classificação fornecendo o status de saudação do tooreflect de proteção de saudação (on, off, atualizado, etc.) e ameaças encontrados. Com que como um número toomake agregações da Ajuda.
> 
> 

Se você clicar no nome do computador hello, você terá a exibição cronológica saudação do status de proteção de saudação para este computador. Isso é muito útil para cenários em que você precisa toounderstand se Olá antimalware foi instalado e em algum momento ele foi removido.   

### <a name="update-assessment"></a>Avaliação de atualização
Isso permite que a opção tooquickly você determinar Olá problemas de segurança de toopotential exposição geral e se ou de quão crítica essas atualizações são para o seu ambiente. OMS solução de segurança e auditoria fornecem apenas visualização Olá dessas atualizações, os dados reais Olá vêm de [soluções de gerenciamento de atualização](oms-solution-update-management.md), que é um módulo diferente no OMS. Veja um exemplo de hello atualizações:

![atualizações do sistema](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Para obter mais informações sobre soluções de Gerenciamento de Atualizações, leia [Solução de Gerenciamento de Atualizações no OMS](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Identidade e Acesso
Identidade deve ser um controle de saudação plano para a sua empresa, protegendo sua identidade deve ser sua prioridade. Enquanto em Olá anterior, havia perímetro em torno de organizações e esse perímetro foi um dos limites de defesa primária hello, hoje em dia com mais dados e aplicativos mais movendo nuvem toohello identidade Olá torna-se perímetro novo hello. 

> [!NOTE]
> atualmente dados saudação baseia-se apenas em dados de logon de eventos de segurança (evento ID 4624) em logons de Office365 futuros hello e dados do Azure AD também serão incluídos.
> 
> 

Ao monitorar as atividades de identidade será medidas proativas capaz de tootake antes de um incidente local ou ações reativo toostop uma tentativa de ataque. Olá **de identidade e acesso** painel fornece uma visão geral do seu estado de identidade, incluindo o número de saudação de toolog tentativas com falha na conta do usuário Olá que foram usadas durante as tentativas, contas que foram bloqueadas, contas com alterado ou redefinição de senha e, no momento, o número de contas que são registrados no. 

Quando você clica em Olá **de identidade e acesso** bloco, você verá Olá painel a seguir:

![identidade e acesso](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

informações de saudação disponíveis neste painel imediatamente podem ajudar a tooidentify uma atividade suspeita potencial. Por exemplo, há 338 toolog de tentativas em como **administrador** e 100% dessas tentativas de falha. Isso pode ser causado por um ataque de força bruta nessa conta. Se você clicar nesta conta você obterá mais informações que podem ajudá-lo toodetermine recurso de destino Olá para esse ataque potencial:

![pesquisar resultados](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

relatório detalhado Hello fornece informações importantes sobre esse evento, incluindo: o computador de destino hello, tipo de Olá de logon (no logon de rede neste caso), a atividade de saudação (por esse evento caso 4625) e um cronograma abrangente de cada tentativa. 

### <a name="computers"></a>Computadores
Este bloco pode ser usado tooaccess todos os computadores que têm ativamente os eventos de segurança. Quando você clica neste bloco você verá a lista de saudação de computadores com eventos de segurança e o número de saudação de eventos em cada computador:

![Computadores](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Você pode continuar sua investigação clicando em cada computador e examinar os eventos de segurança de saudação que foram sinalizados.

### <a name="threat-intelligence"></a>Inteligência contra ameaças

Usando a opção de inteligência de ameaça de saudação disponível no OMS segurança e auditoria, os administradores de TI pode identificar ameaças de segurança em ambiente hello, por exemplo, identificar se um determinado computador fizer parte de uma botnet. Computadores podem ser nós em uma botnet quando os invasores forma ilícita instalar malware que secretamente se conecta a esse comando de toohello do computador e o controle. Ela também pode identificar ameaças potenciais recebidas de canais de comunicação underground, como darknet. Saiba mais sobre a inteligência de ameaça lendo [toosecurity de monitoramento e resposta alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md) artigo.

Em alguns cenários, você pode observar um potencial IP mal-intencionado que foi acessado de um computador monitorado:

![mapa do threat intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Este alerta e outros em Olá mesma categoria, são gerados por meio da segurança do OMS, aproveitando [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). Olá dados de inteligência de ameaça é coletada pela Microsoft, bem como adquirido dos principais provedores de inteligência de ameaça. Esses dados forem atualizados frequentemente e adaptada movendo toofast ameaças. Devido a natureza tooits, ele deve ser combinado com outras fontes de informações de segurança ao [investigando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) um alerta de segurança. 

### <a name="baseline-assessment"></a>Avaliação de linha de base

A Microsoft, juntamente com organizações governamentais e do setor no mundo todo, define uma configuração do Windows que representa implantações de servidor altamente seguras. Essa configuração é um conjunto de chaves do registro, configurações de política de auditoria e configurações de política de segurança, juntamente com os valores recomendados da Microsoft para essas configurações. Esse conjunto de regras é conhecido como linha de base de Segurança. Leia [Avaliação de Linha de Base na Solução de Auditoria e Segurança do Operations Management Suite](oms-security-baseline.md) para saber mais informações sobre esta opção.

### <a name="azure-security-center"></a>Central de Segurança do Azure
Esse bloco é basicamente um painel do atalho tooaccess Central de segurança do Azure. Leia [Introdução à Central de Segurança do Azure](../security-center/security-center-get-started.md) para obter mais informações sobre essa solução.

## <a name="notable-issues"></a>Problemas importantes
Olá intenção principal neste grupo de opções é tooprovide uma exibição rápida de problemas de saudação que você tem em seu ambiente, categorizando-los em crítico, aviso e informativo. Olá bloco de tipo de problema ativo é uma visualização desses problemas, mas ele não permite que você tooexplore mais detalhes sobre eles, para que você precisa toouse Olá parte inferior esse bloco que contém o nome de saudação do problema de saudação (nome), quantos objetos tinha isso acontecer (contagem) e como é essencial (GRAVIDADE).

![Problemas importantes](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Você pode ver que esses problemas já foram abordados em áreas diferentes do hello **domínios de segurança** grupo, o que reforça a intenção de saudação dessa exibição: visualizar problemas mais importantes de saudação em seu ambiente de um único local.

## <a name="detections-preview"></a>Detecções (visualização)
Olá, intenção principal dessa opção é tooallow IT tooquickly identificar ambiente de tootheir ameaças potenciais por meio e a severidade Olá essa ameaça.

![Threat Intel](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Essa opção também pode ser usada durante uma [investigação de resposta a incidentes](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform Olá avaliação e obter mais informações sobre ataques de saudação.

> [!NOTE]
> Para obter mais informações sobre como toouse do OMS para resposta de incidente, assista a este vídeo: [como tooLeverage Olá Central de segurança do Azure & Microsoft Operations Management Suite para uma resposta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Inteligência contra ameaças
Olá ameaça nova seção de inteligência de solução de segurança e auditoria Olá visualiza padrões de ataque de saudação de várias maneiras: Olá número total de servidores com saída tráfego IP mal-intencionado, Olá tipo de ameaça mal-intencionados e um mapa que mostra onde esses IPs são provenientes. Você pode interagir com o mapa de saudação e clique no hello IPs para obter mais informações.

Pinos amarelos no mapa de saudação indicam o tráfego de entrada de IPs mal-intencionado. Não é incomum para servidores que são expostos toohello internet toosee mal-intencionado tráfego de entrada, mas é recomendável analisar esses toomake de tentativas se nenhum deles foi bem-sucedida. Esses indicadores são baseados nos logs do IIS, no WireData e nos logs do Firewall do Windows.  

![Threat Intel](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Consultas comuns de segurança
lista de saudação de consultas comuns de segurança disponíveis pode ser útil para você toorapidly acesso informações sobre o recurso e personalizá-lo com base nas necessidades do seu ambiente. Essas consultas comuns são:

* Todas as Atividades de Segurança
* Atividades de segurança no computador "computer01.contoso.com hello" (Substituir pelo nome do seu computador)
* Atividades de segurança no computador "computer01.contoso.com hello" conta "Administrador" (substituir pelos seus próprios nomes de computador e da conta)
* Atividade de Logon por Computador
* Contas que encerraram o antimalware da Microsoft em qualquer computador
* Computadores nos quais Olá processo antimalware da Microsoft foi encerrado
* Computadores em que “hash.exe” foi executado (substituir pelo nome de outro processo)
* Todos os nomes de Processos que foram executados
* Atividade de Logon por Conta
* Contas que fizeram logon remotamente no computador "computer01.contoso.com hello" (Substituir pelo nome do seu computador)

## <a name="see-also"></a>Consulte também
Neste documento, você foram introduzidas tooOMS solução de segurança e auditoria. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

