---
title: aaaUnderstand arquitetura do Active Directory do Azure | Microsoft Docs
description: "Explica o que é um locatário do AD do Azure e como toomanage Azure através do Active Directory do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Compreender a arquitetura do Azure Active Directory
Habilita o Active Directory (AD do Azure) do Azure toosecurely você gerenciar acesso tooAzure serviços e recursos para os usuários. Está incluído no Azure AD um conjunto completo de recursos de gerenciamento de identidade. Para obter informações sobre os recursos do Azure AD, confira [O que é o Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

Com o AD do Azure, você pode criar e gerenciar usuários e grupos e habilitar permissões tooallow e negar acesso a recursos de tooenterprise. Para obter informações sobre o gerenciamento de identidade, consulte [Olá conceitos básicos do gerenciamento de identidades do Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Arquitetura do Azure AD
Arquitetura distribuída geograficamente do AD do Azure combina monitoramento abrangente, redirecionamento automatizado, failover e recursos de recuperação nos permitem toodeliver nível corporativo disponibilidade e desempenho tooour os clientes.

Olá elementos de arquitetura a seguir é abordado neste artigo:
 *  Design de arquitetura de serviço
 *  Escalabilidade 
 *  Disponibilidade contínua
 *  Data centers

### <a name="service-architecture-design"></a>Design de arquitetura de serviço
Olá mais comuns toobuild de maneira é um sistema altamente disponíveis, escalonável e ricas em dados por meio de blocos de construção independentes ou unidades de escala para a camada de dados de saudação do AD do Azure, são chamadas de unidades de escala *partições*. 

camada de dados Olá tem vários serviços de front-end que fornecem a capacidade de leitura-gravação. Olá diagrama a seguir mostra como os componentes de saudação de uma partição de diretório de único são distribuídas em datacenters geograficamente-distribuídas ao. 

  ![Partições de Diretório Único](./media/active-directory-architecture/active-directory-architecture.png)

componentes de saudação da arquitetura do AD do Azure incluem uma réplicas primária e secundária.

**Réplica primária**

Olá *réplica primária* recebe todas as *grava* para partição Olá pertence a. Qualquer gravação operação é a réplica secundária tooa imediatamente replicadas em um datacenter diferente antes de retornar o chamador de toohello êxito, garantindo a durabilidade de gravações com redundância geográfica.

**Réplicas secundárias**

Todas as *leituras* de diretório são realizadas por meio de *réplicas secundárias*, que estão em data centers fisicamente localizados em regiões diferentes. Há várias réplicas secundárias, pois os dados são replicados de forma assíncrona. Leituras de diretório, como solicitações de autenticação são atendidas de data centers que são clientes tooour fechar. réplicas secundárias Olá são responsáveis por escalabilidade de leitura.

### <a name="scalability"></a>Escalabilidade

Escalabilidade é a capacidade de saudação do toomeet de tooexpand serviço aumentando as demandas de desempenho. Escalabilidade é obtida por meio do particionamento dados saudação de gravação. Escalabilidade de leitura é obtida com a replicação de dados de réplicas secundárias de toomultiple uma partição distribuídas Olá, mundo.

Solicitações de aplicativos de diretório são geralmente roteados toohello datacenter que eles são fisicamente mais próximos. Gravações são consistência de leitura-gravação toohello transparentemente redirecionado réplica primária tooprovide. Réplicas secundárias significativamente estendem escala Olá de partições como diretórios Olá geralmente são leituras atendendo a maioria do tempo de saudação.

Catálogo de aplicativos conecte-se toohello mais próximo da data centers. Isso melhora o desempenho e, portanto, o dimensionamento é possível. Como uma partição de diretório pode ter várias réplicas secundárias, réplicas secundárias podem ser colocadas clientes de diretório toohello mais próximos. Somente interno componentes do serviço são a réplica primária do destino de uso intensivo de gravação Olá active diretamente.

### <a name="continuous-availability"></a>Disponibilidade contínua

Disponibilidade (ou tempo de atividade) define a capacidade de saudação de um tooperform sistema ininterrupta. Olá chave tooAzure do AD de alta disponibilidade é que nossos serviços podem mudar rapidamente o tráfego entre vários centros de dados distribuídos geograficamente. Cada data center é independente, o que habilita modos de falha não correlacionados.

Design de partição do AD do Azure é simplificada toohello comparados enterprise design do AD, que é essencial para a expansão do sistema de saudação. Adotamos um design de mestre único que inclui um processo de failover de réplica primária cuidadosamente orquestrada e determinística.

**Tolerância a falhas**

Um sistema está mais disponível se é tolerante a falhas de software, rede e toohardware. Para cada partição de diretório Olá, existe uma réplica mestre altamente disponível: réplica primária hello. Somente gravações toohello de partição são executadas nessa réplica. Esta réplica está sendo atentamente e continuamente monitorados e gravações podem ser imediatamente deslocadas tooanother réplica (que se torna Olá novo primário) se for detectada uma falha. Durante o failover, pode haver uma perda de disponibilidade de gravação normalmente de 1 a 2 minutos. A disponibilidade de leitura não é afetada durante esse tempo.

As operações de leitura (o que ultrapassa o número de gravações por várias ordens de magnitude) apenas vá toosecondary réplicas. Como réplicas secundárias são idempotentes, perda de qualquer uma réplica em uma determinada partição é compensada facilmente por meio do direcionamento Olá leituras tooanother réplica, geralmente em Olá mesmo datacenter.

**Durabilidade dos dados**

Uma gravação seja tooat permanentemente confirmado pelo menos dois data centers anterior tooit que está sendo confirmada. Isso acontece por primeiro confirmar gravação Olá Olá primário e, em seguida, imediatamente replicando tooat de gravação da saudação pelo menos um outro data center. Isso garante que uma potencial perda catastrófica de saudação data center hospedagem Olá primário não resulta na perda de dados.

O AD do Azure mantém um zero [objetivo de tempo de recuperação (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) para emissão de token e diretório leituras e gravações em ordem de saudação de minutos (~ 5 minutos) RTO por diretório. Também mantemos um [RPO (Objetivo de Ponto de Recuperação)](https://en.wikipedia.org/wiki/Recovery_point_objective) zero e não perderemos dados em failovers.

### <a name="data-centers"></a>Data centers

Réplicas do AD do Azure são armazenadas em data centers localizados em todo o mundo de saudação. Para obter mais informações, confira [Datacenters do Azure](https://azure.microsoft.com/en-us/overview/datacenters).

AD do Azure funciona em data centers com hello características a seguir:

 * Autenticação, gráfico e outros serviços do AD estão atrás de saudação serviço de Gateway. Olá Gateway gerencia o balanceamento de carga desses serviços. O failover ocorrerá automaticamente se todos os servidores não íntegros forem detectados usando testes de integridade transacional. Com base nesses testes de integridade, Olá Gateway encaminha dinamicamente tráfego toohealthy data centers.
 * Para *lê*, diretório de saudação tem réplicas secundárias e serviços de front-end correspondentes em uma configuração ativo-ativo operacional em vários data centers. Em caso de falha de um data center inteiro, o tráfego será automaticamente roteado tooa um datacenter diferente.
 *  Para *grava*, Olá diretório será failover (mestre) réplica primária em data centers via planejado (novo primário é sincronizada tooold primário) ou os procedimentos de failover de emergência. Durabilidade dos dados é obtida por meio da replicação qualquer tooat pelo menos dois data centers de confirmação.

**Consistência de dados**

modelo de diretório de saudação é uma consistência eventual. Um problema comum com replicação assíncrona de sistemas distribuídos é que dados Olá retornados de uma réplica "específica" podem não ser o toodate. 

AD do Azure proporciona consistência de leitura e gravação para aplicativos voltados para uma réplica secundária pelo roteamento sua réplica primária de toohello gravações e extração de forma síncrona Olá grava réplica secundária toohello.

Aplicativo grava usando Olá Graph API do Azure AD são removidas de manter afinidade tooa directory réplica para consistência de leitura / gravação. saudação de serviço do Azure AD Graph mantém uma sessão lógica, que tem afinidade tooa réplica secundária usada para leituras; a afinidade é capturada em um "token de réplica" hello caches de serviço do gráfico usando um cache distribuído. Esse token é usado para as operações subsequentes na Olá mesma sessão lógica. 

 >[!NOTE]
 >As gravações são replicadas imediatamente leituras toohello réplica secundária toowhich Olá lógica da sessão foram emitidas.
 >

**Proteção de backup**

diretório de saudação implementa exclusões a quente, em vez de disco rígidas exclusões, para usuários e locatários para fácil recuperação no caso de exclusões acidentais por um cliente. Se o administrador de inquilinos acidentalmente exclui os usuários, eles facilmente podem desfazer e restaurar usuários Olá excluído. 

O Azure AD implementa backups diários de todos os dados e, assim, pode restaurar os dados em caso de quaisquer exclusões lógicas ou corrupção. Nossa camada de dados utiliza códigos de correção de erros para que possa verificar se há erros e corrigir automaticamente os tipos específicos de erros de disco.

**Métricas e monitores**

Executar um serviço de alta disponibilidade requer métricas de classe mundial e recursos de monitoramento. O Azure AD analisa e relata continuamente critérios de sucesso e métricas de integridade de serviço principais para cada um de seus serviços. Desenvolvemos e ajustamos continuamente as métricas, monitorando e alertando para cada cenário, em cada serviço do Azure AD e em todos os serviços.

Se qualquer serviço do AD do Azure não está funcionando conforme o esperado, imediatamente faremos funcionalidade de toorestore ação assim que possível. Olá mais importante que controla a métrica do AD do Azure é a rapidez pode detectar e reduzir a um cliente ou live problema de site. Investimos intensamente no monitoramento e alertas toominimize tempo toodetect (destino TTD: < 5 minutos) e prontidão operacional toominimize tempo toomitigate (destino anual: < 30 minutos).

**Operações seguras**

Adotamos controles operacionais como MFA (autenticação multifator) para qualquer operação, bem como a auditoria de todas as operações. Além disso, usamos um elevação just-in-time sistema toogrant necessário acesso temporário para qualquer operacional tarefa sob demanda continuamente. Para obter mais informações, consulte [Olá nuvem confiável](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Próximas etapas
[Guia do desenvolvedor do Active Directory do Azure](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

