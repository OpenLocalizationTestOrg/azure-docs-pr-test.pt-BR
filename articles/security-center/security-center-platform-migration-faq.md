---
title: "migração de plataforma aaaSecurity Center perguntas Frequentes | Microsoft Docs"
description: "Perguntas Frequentes responde perguntas sobre Olá migração de plataforma da Central de segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Perguntas frequentes sobre a migração da plataforma da Central de Segurança
No início de junho de 2017, Central de segurança do Azure começou usando dados de toocollect e armazenamento do Microsoft Monitoring Agent hello. mais, consulte toolearn [migração da plataforma Azure Security Center](security-center-platform-migration.md). Perguntas Frequentes respostas a perguntas sobre a migração de plataforma de saudação.

## <a name="data-collection-agents-and-workspaces"></a>Coleta de dados, agentes e espaços de trabalho

### <a name="how-is-data-collected"></a>Como os dados são coletados?
Central de segurança usa dados de segurança de toocollect Olá Microsoft Monitoring Agent de suas VMs. dados de segurança de saudação incluem informações sobre as configurações de segurança, que são usados tooidentify vulnerabilidades, e eventos de segurança, que são usados toodetect ameaças. Dados coletados pelo agente de saudação são armazenados em um toohello de espaço de trabalho conectado de análise de Log VM existente ou um novo espaço de trabalho criado pela Central de segurança. Quando a Central de segurança cria um novo espaço de trabalho, localização geográfica de saudação do hello VM é levada em conta.

> [!NOTE]
> Olá Microsoft Monitoring Agent é hello mesmo agente usado pelo serviço de análise de Log de saudação Operations Management Suite (OMS) e System Center Operations Manager (SCOM).
>
>

Quando a coleta de dados está habilitada para Olá primeira vez ou quando as assinaturas são migradas, Central de segurança verifica toosee se Olá Microsoft Monitoring Agent já está instalado como uma extensão do Azure em cada uma das suas VMs. Se Olá Microsoft Monitoring Agent não estiver instalado, será a Central de segurança:

- instalar o agente do Microsoft Monitoring Olá Olá VM
   - Se um espaço de trabalho criado pelo Centro de segurança já existe no hello mesma localização geográfica como Olá VM, Olá agente está conectado toothis espaço de trabalho
   - Se não existir um espaço de trabalho, a Central de segurança cria um novo grupo de recursos padrão do espaço de trabalho que localização geográfica e conecte-se o espaço de trabalho do hello agente toothat. convenção de nomenclatura de saudação para Olá espaço de trabalho e grupo de recursos são:

       Espaço de trabalho: DefaultWorkspace-[ID da assinatura]-[localização geográfica]

       Grupo de recursos: DefaultResouceGroup-[localização geográfica]
- instalar uma solução de segurança central no espaço de trabalho de saudação

local de saudação do espaço de trabalho Olá baseia-se na localização de saudação do hello VM. mais, consulte toolearn [segurança de dados](security-center-data-security.md).

> [!NOTE]
> Migração tooplatform anterior, a Central de segurança coletados dados de segurança de suas VMs usando Olá agente de monitoramento do Azure e dados foram armazenados na sua conta de armazenamento. Após a migração de plataforma hello, Central de segurança usa Olá Microsoft Monitoring Agent e armazenamento e espaço de trabalho toocollect Olá mesmos dados. conta de armazenamento Olá pode ser removida após a migração de saudação.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Sou cobrado para análise de Log ou do OMS em espaços de trabalho de saudação criados pela Central de segurança?
Não. Os espaços de trabalho criados pela Central de Segurança, embora sejam configurados para cobrança de OMS por nó, não incorrerão em encargos do OMS. Cobrança da Central de segurança sempre é baseada em suas soluções Central de segurança de saudação e política de segurança instaladas em um espaço de trabalho:

- **Camada gratuita** – Central de segurança instala a solução de 'SecurityCenterFree' de saudação no espaço de trabalho saudação padrão. Você não será cobrado pela camada gratuita hello.
- **Camada padrão** – Central de segurança instala Olá 'SecurityCenterFree' e soluções 'Security' hello espaço de trabalho padrão.

Para saber mais sobre preços, confira [preços da Central de Segurança](https://azure.microsoft.com/pricing/details/security-center/). Olá endereços de página de preços altera toosecurity armazenamento de dados e iniciar cobrança pro rata em junho de 2017.

> [!NOTE]
> camada de preços do OMS Olá de espaços de trabalho criados pela Central de segurança não afeta a cobrança da Central de segurança.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Excluir espaços de trabalho padrão Olá criados pela Central de segurança?
**Não é recomendável excluir o espaço de trabalho do saudação padrão.** Central de segurança usa dados de segurança de toostore saudação padrão espaços de trabalho de suas VMs.  Se você excluir um espaço de trabalho, a Central de segurança é não é possível toocollect esses dados e algumas recomendações de segurança e alertas não estão disponíveis

toorecover, Olá remover agente de monitoramento da Microsoft no espaço de trabalho do hello VMs conectado toohello excluído. Central de segurança reinstala agente hello e cria novos espaços de trabalho padrão.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>E se Olá Microsoft Monitoring Agent já foi instalado como uma extensão em Olá VM?
Central de segurança não substitui os espaços de trabalho de toouser conexões existentes. Central de segurança armazena dados de segurança do hello VM no espaço de trabalho de saudação já conectado.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>E se eu tinha um agente de monitoramento da Microsoft instalado no computador hello, mas não como uma extensão?
Se Olá Microsoft Monitoring Agent está instalado diretamente em Olá VM (não como uma extensão do Azure), a Central de segurança não instalará Olá Microsoft Monitoring Agent e monitoramento de segurança será limitada.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>O que é o impacto de saudação de remover essas extensões?
Se você remover Olá extensão de monitoramento da Microsoft, Central de segurança não é capaz de toocollect dados de segurança de saudação VM e algumas recomendações de segurança e alertas não estão disponíveis. Dentro de 24 horas, a Central de segurança determina que Olá VM não tem extensão hello e reinstala Olá extensão.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Como parar criação de espaço de trabalho e instalação de agente automático Olá?
Você pode desativar a coleta de dados para suas assinaturas na política de segurança hello, mas isso não é recomendado. A desativação da coleta de dados limita as recomendações e os alertas da Central de Segurança. Coleta de dados é necessária para as assinaturas na faixa de preços padrão hello. coleta de dados de toodisable:

1. Se sua assinatura estiver configurada para a camada padrão hello, abra a política de segurança de saudação para essa assinatura e selecione Olá **livre** camada.

   ![Tipo de preço ][1]

2. Em seguida, desative a coleta de dados selecionando **Off** em Olá **política de segurança – a coleta de dados** folha.

   ![Coleta de dados][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Como fazer para remover as extensões do OMS instaladas pela Central de Segurança?
Você pode remover manualmente Olá Microsoft Monitoring Agent. Isso não é recomendado, pois limita as recomendações e os alertas da Central de Segurança.

> [!NOTE]
> Se a coleta de dados estiver habilitada, a Central de segurança reinstalar o agente Olá após ela ser removida.  É necessário toodisable a coleta de dados antes de remover manualmente o agente de saudação. Consulte [como interromper a criação de espaço de trabalho e a instalação automática de agentes Olá?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) para obter instruções sobre como desabilitar a coleta de dados.
>
>

toomanually remover agente hello:

1.  No portal de hello, abra **análise de Log**.
2.  Na folha de análise de Log hello, selecione um espaço de trabalho:
3.  Selecione cada máquina virtual que você não deseja toomonitor e selecione **Disconnect**.

   ![Remover agente Olá][3]

> [!NOTE]
> Se uma VM do Linux já tiver um agente do OMS não extensão, removendo a extensão de saudação remove agent Olá também e cliente Olá tem tooreinstall-lo.
>
>

## <a name="existing-oms-customers"></a>Clientes existentes do OMS

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>A Central de Segurança substitui todas as conexões existentes entre as VMs e os espaços de trabalho?
Se uma VM já tiver Olá Microsoft Monitoring Agent instalado como uma extensão do Azure, Central de segurança não substituirá a conexão de área de trabalho existente hello. Em vez disso, a Central de segurança usa o espaço de trabalho existente do hello.

Uma solução central de segurança está instalado no espaço de trabalho de saudação se não apresentar já e solução de saudação é aplicado toohello somente máquinas virtuais relevantes. Quando você adiciona uma solução, ele será automaticamente implantado por tooall Windows e Linux agentes conectados tooyour análise de Log espaço de trabalho padrão. [Direcionamento de solução](../operations-management-suite/operations-management-suite-solution-targeting.md), que é um recurso, o OMS permite que você tooapply um escopo tooyour soluções.

Se Olá Microsoft Monitoring Agent está instalado diretamente em Olá VM (não como uma extensão do Azure), a Central de segurança não instalará Olá Microsoft Monitoring Agent e monitoramento de segurança é limitado.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>O que devo fazer se suspeitar de que a migração de plataforma de dados Olá rompeu conexão Olá entre uma das minhas VMs e meu espaço de trabalho?
Isso não deve ocorrer. Se isso acontecer, em seguida, [criar uma solicitação de suporte do Azure](../azure-supportability/how-to-create-azure-support-request.md) e incluir Olá detalhes a seguir:

- ID de recurso do Azure de saudação do hello afetado VM
- ID de recurso do Azure de saudação do espaço de trabalho de saudação configurado na extensão de saudação antes de conexão Olá foi interrompida
- Agente de saudação e a versão instalada anteriormente

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>A Central de Segurança instala soluções em meus espaços de trabalho existentes do OMS? Quais são as implicações de cobranças Olá?
Quando a Central de segurança identifica uma VM já está conectado tooa espaço de trabalho que é criado, a Central de segurança permite que soluções neste espaço de trabalho de acordo com o preço de tooyour. Olá soluções é aplicada toohello somente máquinas virtuais do Azure relevantes, por meio de [solução direcionamento](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), portanto, permanece cobrança Olá Olá mesmo.

- **Camada gratuita** – Central de segurança instala a solução de 'SecurityCenterFree' de saudação no espaço de trabalho de saudação. Você não será cobrado pela camada gratuita hello.
- **Camada padrão** – Central de segurança instala Olá 'SecurityCenterFree' e soluções 'Security' hello espaço de trabalho.

   ![Soluções no espaço de trabalho padrão][4]

> [!NOTE]
> Olá solução 'Segurança' na análise de Log é Olá segurança & solução de auditoria do OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Eu já tenho espaços de trabalho em meu ambiente, posso usar-os dados de segurança toocollect?
Se uma VM já tiver Olá Microsoft Monitoring Agent instalado como uma extensão do Azure, Central de segurança usa Olá conectado espaço de trabalho existente. Uma solução central de segurança está instalado no espaço de trabalho de saudação se não apresentar já e solução de saudação é aplicado toohello somente relevantes VMs através de [solução direcionamento](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Quando a Central de segurança Olá Microsoft Monitoring Agent é instalado em máquinas virtuais, use saudação padrão espaço criado pela Central de segurança. Assim, os clientes serão tooconfigure capaz de qual espaço é usados.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Já tenho a solução de segurança em meus espaços de trabalho. Quais são as implicações de cobranças Olá?
Saudação da solução de segurança e auditoria é Security Center Standard recursos de camada tooenable usado para VMs do Azure. Se a solução de segurança e auditoria Olá já estiver instalada em um espaço de trabalho, a Central de segurança usa solução existente de saudação. Não há nenhuma alteração na cobrança.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a migração da plataforma Olá Central de segurança, consulte

- [Migração de plataforma da Central de Segurança do Azure](security-center-platform-migration.md)
- [Guia de solução de problemas da Central de Segurança do Azure](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
