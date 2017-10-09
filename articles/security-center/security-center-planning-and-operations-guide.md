---
title: "aaaSecurity Center guia de planejamento e operações | Microsoft Docs"
description: "Este documento ajuda tooplan antes de adotar a Central de segurança do Azure e considerações sobre as operações diárias."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guia de planejamento e operações da Central de Segurança do Azure
Este guia destina-se a profissionais de tecnologia da informação, arquitetos IT, analistas de segurança de informações e os administradores de nuvem cujas organizações estiver planejando toouse Central de segurança do Azure.

>[!NOTE] 
>A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guia de planejamento
Este guia abrange um conjunto de etapas e tarefas que você pode seguir toooptimize que o uso da Central de segurança com base em requisitos de segurança da sua organização e o modelo de gerenciamento de nuvem. tootake proveito da Central de segurança, é importante toounderstand como diferentes pessoas ou equipes em sua organização usar desenvolvimento seguro da saudação serviço toomeet e operações, monitoramento, administração, e precisa de resposta a incidentes. Olá áreas principais tooconsider ao planejar toouse Central de segurança são:

* Funções de segurança e controles de acesso
* Políticas de segurança e recomendações 
* Coleta de dados e armazenamento
* Monitoramento contínuo de segurança
* Resposta a incidentes

Na próxima seção, Olá, você aprenderá como tooplan para cada uma dessas áreas e aplique essas recomendações com base nos seus requisitos.

> [!NOTE]
> Leitura [Central de segurança do Azure perguntas frequentes (FAQ)](security-center-faq.md) para obter uma lista das perguntas comuns que também podem ser úteis durante a saudação fases de planejamento e criação.
> 

## <a name="security-roles-and-access-controls"></a>Funções de segurança e controles de acesso
Dependendo do tamanho de saudação e estrutura de sua organização, vários indivíduos e equipes podem usar a Central de segurança tooperform diferentes tarefas de segurança. Olá diagrama a seguir, você tem um exemplo de personas fictícios e suas respectivas funções e responsabilidades de segurança:

![Funções](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Central de segurança permite que essas pessoas toomeet essas várias responsabilidades. Por exemplo:

**Jeff (proprietário de carga de trabalho de nuvem)**

* Gerenciar uma carga de trabalho de nuvem e seus recursos relacionados
* Responsáveis pela implementação e manutenção das proteções de acordo com a política de segurança da empresa

**Ellen (CISO/CIO)**

* Responsável por todos os aspectos de segurança para a empresa Olá
* Deseja postura de segurança da empresa do toounderstand Olá em cargas de trabalho de nuvem
* Necessidades toobe informado de riscos e ataques principais

**David (segurança de TI)**

* Conjuntos de políticas de segurança tooensure Olá apropriado proteções estejam em vigor da empresa
* Monitora a conformidade com as políticas
* Gera relatórios de liderança ou auditores

**Judy (Operações de Segurança)**

* Monitora e responde toosecurity alertas 24/7
* Escala tooCloud proprietário da carga de trabalho ou analista de segurança de TI

**Sam (Analista de Segurança)**

* Investiga os ataques
* Trabalhar com a correção de tooapply do proprietário da carga de trabalho de nuvem 

Central de segurança usa [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções internas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídos toousers, grupos e serviços no Azure. Quando um usuário abre a Central de segurança, eles veem somente informações relacionadas tooresources tiverem acesso à. O que significa usuário Olá é atribuído saudação do leitor, colaborador ou proprietário toohello assinatura ou grupo de recursos que o recurso pertence. Funções de toothese adição, há duas funções específicas da Central de segurança:

- **Leitor de segurança**: usuário que pertence a função toothis é ser capaz de tooview direitos tooSecurity Center, que inclui recomendações, alertas, política e integridade, mas ele não será capaz de toomake alterações.
- **Administrador de segurança**: mesmo como o leitor de segurança, mas ele também pode atualizar a política de segurança hello, ignorar recomendações e alertas.

funções de Central de segurança Olá descrita acima não tem acesso tooother áreas de serviço do Azure como armazenamento, Web e móveis ou Internet das coisas.  

> [!NOTE]
> Um usuário precisa toobe pelo menos uma assinatura, o proprietário do grupo de recursos ou o toosee do Colaborador toobe capaz de Central de segurança no Azure. 
> 
> 

Usar personas Olá explicados no diagrama anterior de hello, Olá RBAC seguir seria necessário:

**Jeff (proprietário de carga de trabalho de nuvem)**

* Proprietário/Colaborador do grupo de recursos

**David (segurança de TI)**

* Proprietário da assinatura/Colaborador ou o administrador de segurança

**Judy (Operações de Segurança)**

* Leitor de assinatura ou os alertas ao leitor de segurança tooview
* Proprietário da assinatura/Colaborador ou o administrador de segurança necessário toodismiss alertas

**Sam (Analista de Segurança)**

* Alertas de tooview de leitor de assinatura
* Proprietário da assinatura/Colaborador necessário toodismiss alertas
* O espaço de trabalho do Access toohello pode ser necessário

Alguns outros tooconsider informações importantes:

* Somente os Proprietários/Colaboradores da assinatura e Administradores de segurança podem editar uma política de segurança
* Somente os Proprietários e os Colaboradores da assinatura e do grupo de recursos podem aplicar recomendações de segurança para um recurso

Ao planejar o controle de acesso usando o RBAC para a Central de segurança, ser toounderstand-se de que estará usando a Central de segurança na sua organização. Além disso, quais tipos de tarefas irão executar, em seguida, configurar o RBAC de acordo.

> [!NOTE]
> É recomendável que você atribua Olá função menos permissiva necessários para os usuários toocomplete suas tarefas. Por exemplo, os usuários que precisam apenas tooview informações sobre o estado de segurança de saudação de recursos, mas não tome uma ação, como aplicar recomendações ou edição de políticas, devem ser atribuídos a função de leitor hello.
> 
> 

## <a name="security-policies-and-recommendations"></a>Políticas de segurança e recomendações 
Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura. Central de segurança, você definirá da empresa tooyour requisitos de segurança e tipo hello de aplicativos ou confidencialidade dos dados saudação de acordo com as políticas.

Políticas que estão habilitadas no nível de assinatura Olá automaticamente propaguem tooall grupos de recursos de assinatura do hello conforme mostrado no diagrama a seguir de saudação:

![Políticas de Segurança](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Se você precisar tooreview que foram alteradas, você pode usar [os Logs de auditoria do Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). As alterações na política são sempre registradas nos Logs de auditoria do Azure.
> 
> 

### <a name="security-recommendations"></a>Recomendações de segurança
Antes de configurar políticas de segurança, examine cada Olá [recomendações de segurança](security-center-recommendations.md)e determinar se essas políticas são apropriadas para suas várias assinaturas e grupos de recursos. Também é importante toounderstand que ação deve ser realizada tooaddress [recomendações de segurança](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) e quem na sua organização será responsável por novas recomendações e colocando Olá necessárias etapas de monitoramento.

A Central de Segurança recomendará que você forneça os detalhes de contato da segurança para sua assinatura do Azure. Essa informação será usada pelo Microsoft toocontact se Olá Microsoft Security Response Center (MSRC) descobre que seu cliente tiver sido acessado por uma parte ilegal ou não autorizada. Leitura [fornecer detalhes de contato de segurança na Central de segurança do Azure](security-center-provide-security-contact-details.md) para obter mais informações sobre como tooenable essa recomendação.

## <a name="data-collection-and-storage"></a>Coleta de dados e armazenamento
Central de segurança do Azure usa Olá Microsoft Monitoring Agent – isso é Olá mesmo agente usado pelo serviço de análise de Log – toocollect dados de segurança de suas máquinas virtuais e Olá Operations Management Suite. Os dados coletados por esse agente são armazenados nos seus espaços de trabalho do Log Analytics.

### <a name="agent"></a>Agente

Após a coleta de dados está habilitada na política de segurança hello, Olá Microsoft Monitoring Agent (para [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) ou [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) é instalado em todos os VMs do Azure e os novos que são criados.  Se Olá que VM já possui Olá Microsoft Monitoring Agent instalado, Central de segurança do Azure podem se beneficiar de saudação atual agente foi instalado. processo do agente de saudação é projetado toobe não invasivo e ter impacto mínimo no desempenho de VM.

Olá Microsoft Agent de monitoramento do Windows exige que usam a porta TCP 443. Consulte Olá [artigo de solução de problemas](security-center-troubleshooting-guide.md) para obter detalhes adicionais.

Se em algum momento você desejar toodisable coleta de dados, você pode desativá-lo na política de segurança de saudação. No entanto, como Olá Microsoft Monitoring Agent pode ser usado por outro gerenciamento do Azure e monitoramento de serviços, o agente de saudação não será desinstalado automaticamente quando você desativar a coleta de dados da Central de segurança. Você poderá desinstalar manualmente o agente de saudação se necessário.

> [!NOTE]
> toofind uma lista de máquinas virtuais com suporte, leia Olá [Central de segurança do Azure perguntas frequentes (FAQ)](security-center-faq.md).
> 

### <a name="workspace"></a>Espaço de trabalho

Dados coletados de saudação que Microsoft Monitoring Agent (em nome da Central de segurança do Azure) será armazenado em um espaço análise de Log existente associadas à sua assinatura do Azure ou um novo espaço, considerando Olá conta geográfica da saudação VM. 

Olá portal do Azure, você pode navegar toosee uma lista de seus espaços de trabalho de análise de Log, incluindo aqueles criados pela Central de segurança do Azure. Um grupo de recursos relacionados será criado para novos espaços de trabalho. Ambos seguirão esta convenção de nomenclatura: 

* Espaço de trabalho: *DefaultWorkspace-[ID da assinatura]-[localização geográfica]*
* Grupo de recursos: *DefaultResouceGroup-[localização geográfica]*

No caso de espaços de trabalho criados pela Central de Segurança do Azure, os dados serão retidos por 30 dias. Para sair de espaços de trabalho, retenção com base no espaço de trabalho de saudação de preço.

> [!NOTE]
> Microsoft tornar privacidade de saudação do investimento forte tooprotect e segurança de dados. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço. Para saber mais sobre manipulação de dados e privacidade, leia [Segurança de dados da Central de Segurança do Azure](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Monitoramento contínuo de segurança
Após a configuração inicial e o aplicativo de recomendações da Central de segurança, a próxima etapa de saudação está considerando processos operacionais da Central de segurança.

tooaccess Central de segurança do hello portal do Azure, você pode clicar em **procurar** e tipo **Central de segurança** em Olá **filtro** campo. exibições de saudação que Olá usuário obtém seguem filtros toothese aplicada, exemplo hello abaixo mostra um ambiente com muitos toobe problemas resolvidos:

![painel Transações da Web](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Central de segurança não interfere com os procedimentos operacionais normais, ele passivamente monitorar as implantações e fornecem recomendações com base nas políticas de segurança de saudação que é habilitado.

Quando você primeiro aceitar toouse Central de segurança para seu ambiente do Azure, certifique-se de que você examine todas as recomendações, que podem ser feitas no hello **recomendações** lado a lado ou por recurso (**de computação** **Rede**, **armazenamento & dados**, **aplicativo**).

Depois que você resolver todas as recomendações, Olá **prevenção** seção deverá ficar verde para todos os recursos que foram resolvidos. Monitoramento contínuo agora se torna mais fácil desde que só terão ações com base nas alterações nos blocos de integridade e as recomendações de segurança de recursos do hello.

Olá **detecção** seção é mais reativa, esses são alertas sobre problemas que são ambos ocorra agora, ou ocorreram em Olá anterior e foram detectados por sistemas de terceiros 3º e controles da Central de segurança. bloco de alertas de segurança de saudação mostrará os gráficos de barras que representam o número de saudação de alertas de detecção de ameaças encontradas em cada dia, bem como sua distribuição entre categorias diferentes de gravidade de saudação (baixa, média, alta). Para obter mais informações sobre alertas de segurança, leia [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Você também pode aproveitar o Microsoft Power BI toovisualize seus dados da Central de segurança. Leia [Obter informações nos dados da Central de Segurança do Azure com o Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Monitoramento de recursos novos ou alterados
A maioria dos ambientes do Azure são dinâmicos, com novos recursos gerados e excluídos regularmente, com configurações ou alterações etc. Central de segurança ajuda a garantir que você tenha visibilidade do estado de segurança Olá esses novos recursos.

Quando você adiciona novos recursos (VMs, bancos de dados SQL) tooyour ambiente do Azure, Central de segurança será descobrir esses recursos e começar toomonitor sua segurança automaticamente. Isso também inclui as funções Web do PaaS e as funções de trabalho. Se a coleta de dados estiver habilitada no hello [política de segurança](security-center-policies.md)adicionais recursos de monitoramento serão habilitado automaticamente para as máquinas virtuais.

![Principais áreas](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Nas máquinas virtuais, clique em **Computação**, na seção **Prevenção**. Problemas com a habilitação de dados ou recomendações relacionadas ocorrerá no hello **visão geral** guia e **monitoramento recomendações** seção.
2. Saudação de exibição **recomendações** toosee que, se houver, riscos de segurança foi identificados para o novo recurso de saudação.
3. É muito comum que quando novas VMs forem adicionadas tooyour ambiente, o sistema operacional somente de saudação inicialmente é instalado. proprietário do recurso Olá talvez seja necessário algum tempo toodeploy outros aplicativos que serão usados por essas VMs.  Idealmente, você deve saber o objetivo final Olá essa carga de trabalho. Toobe um servidor de aplicativos está acontecendo? Com base no qual essa nova carga de trabalho é toobe contínuo, você pode habilitar Olá apropriado **política de segurança**, que é a terceira etapa Olá nesse fluxo de trabalho.
4. À medida que novos recursos são adicionados tooyour ambiente do Azure, é possível que os novos alertas aparecem no hello **alertas de segurança** lado a lado. Sempre verifique se há novos alertas neste bloco e executar ações de acordo com as recomendações de tooSecurity Center.

Você também deve tooregularly Olá estado do monitor de alterações de configuração existente de tooidentify de recursos que criou os riscos de segurança, descompasso de linhas de base recomendadas e alertas de segurança. Iniciar no painel de controle do hello Central de segurança. A partir daí, você tem três tooreview principais áreas de forma consistente.

![Operações](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Olá **prevenção** painel seção fornece recursos principais de tooyour acesso rápido. Use essa opção toomonitor computação, rede, armazenamento e aplicativos e dados.
2. Olá **recomendações** painel permite que você tooreview recomendações de Central de segurança. Durante o monitoramento em andamento, você pode achar que você não tem as recomendações em uma base diária, que é normal, já que você resolveu todas as recomendações sobre a instalação do saudação inicial central de segurança. Por esse motivo, você pode não ter novas informações nesta seção diariamente e apenas será necessário tooaccess-lo conforme necessário.
3. Olá **detecção** seção pode ser alterado de forma muito frequente ou muito pouco frequentes. Sempre examine os alertas de segurança e tome ações com base nas recomendações da Central de Segurança.

## <a name="incident-response"></a>Resposta a incidentes
Central de segurança detecta e alerta você toothreats conforme elas ocorrem. As organizações devem monitorar novos alertas de segurança e agir como tooinvestigate necessário mais ou corrigir ataque hello. Para obter mais informações sobre como funciona a detecção de ameaças da Central de Segurança, leia [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md).

Enquanto este artigo não tem tooassist intenção Olá você criar seu próprio plano de resposta a incidentes, vamos toouse resposta de segurança do Microsoft Azure no ciclo de vida de nuvem hello como base Olá estágios de resposta a incidentes. estágios de saudação são mostrados na Olá diagrama a seguir:

![Atividade suspeita](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Você pode usar o hello Instituto Nacional de padrões e tecnologia (NIST) [guia de tratamento de incidente do computador segurança](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) como uma referência tooassist você criar seus próprios.
> 

Você pode usar os alertas da Central de segurança durante a saudação estágios a seguir:

* **Detectar**: identifica uma atividade suspeita em um ou mais recursos. 
* **Avaliar**: executar Olá avaliação inicial tooobtain obter mais informações sobre atividades suspeitas hello.
* **Diagnosticar**: usar Olá correção etapas tooconduct Olá procedimento técnica tooaddress Olá saídas.

Cada alerta de segurança fornece informações que podem ser usadas toobetter entender a natureza de saudação do ataque hello e sugere possíveis atenuações. Alguns alertas também fornecem links tooeither mais informações ou tooother fontes de informações dentro do Azure. Você pode usar informações de saudação fornecidas para pesquisa adicional e mitigação de toobegin, e você também pode pesquisar dados relacionados à segurança que são armazenados no espaço de trabalho.

Olá, exemplo a seguir mostra uma atividade suspeita de RDP ocorrendo:

![Atividade suspeita](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Como você pode ver, esta folha mostra detalhes sobre o tempo de saudação que Olá ataque ocorreu, Olá nome de host de origem, Olá VM de destino e também fornece as etapas de recomendação. Em alguns Olá circunstâncias informações de origem do ataque Olá podem estar vazias. Leia [Informações de Origem Ausentes nos Alertas da Central de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) para obter mais informações sobre esse tipo de comportamento.

Em Olá [como tooLeverage Olá Central de segurança do Azure & Microsoft Operations Management Suite para uma resposta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) vídeo pode ver algumas demonstrações que podem ajudá-lo toounderstand como a Central de segurança podem ser usada em cada um desses estágios.

> [!NOTE]
> Leitura [utilizando Central de segurança do Azure para a resposta a incidentes](security-center-incident-response.md) para obter mais informações sobre como toouse Central de segurança recursos tooassist você durante a resposta de incidente de processo. 
> 
> 

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como tooplan para a adoção da Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Gerenciando e responder a alertas toosecurity na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.

