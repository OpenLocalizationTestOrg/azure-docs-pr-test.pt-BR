---
title: "aaaGet iniciada com um espaço de trabalho de análise de logs do Azure | Microsoft Docs"
description: "Você pode começar a trabalhar rapidamente com um espaço de trabalho na Log Analytics em minutos."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Introdução a um espaço de trabalho de Log Analytics
Você pode começar a trabalhar rapidamente com Azure Log Analytics, que ajuda a avaliar inteligência operacional coletada da infraestrutura de TI. Usando este artigo, você pode facilmente começar a explorar, analisar e agir em relação aos dados coletados *gratuitamente*.

Este artigo serve como uma introdução tooLog análise usando um breve toowalk tutorial você por meio de uma implantação mínima no Azure para que você pode começar a usar o serviço de saudação. contêiner lógico Hello, onde os dados de gerenciamento no Azure são armazenados é chamado de um espaço de trabalho. Depois que você já leu essas informações e concluiu sua própria avaliação, você pode remover o espaço de trabalho de avaliação de saudação. Como este artigo é um tutorial, ela não aborda requisitos de negócios, planejamento ou diretrizes de arquitetura.

>[!NOTE]
>Se você usar Olá nuvem do Microsoft Azure Government, use [monitoramento do Azure governamental + documentação de gerenciamento](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) em vez disso.

Aqui está uma visão geral de saudação processo usado tooget iniciado:

![diagrama do processo](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Criar uma conta do Azure e entrar

Se você ainda não tiver uma conta do Azure, será necessário toocreate um toouse análise de Log. Você pode criar uma [conta gratuita](https://azure.microsoft.com/free/) que é válida por 30 dias e permite acessar qualquer serviço do Azure.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate uma conta gratuita e entrar
1. Siga as orientações de saudação em [criar sua conta gratuita do Azure](https://azure.microsoft.com/free/).
2. Vá toohello [portal do Azure](https://portal.azure.com) e entrar.

## <a name="2-create-a-workspace"></a>2 Criar um espaço de trabalho

Olá próxima etapa é toocreate um espaço de trabalho.

1. Em Olá portal do Azure, pesquisar a lista de saudação de serviços no hello Marketplace para *análise de Log*e, em seguida, selecione **análise de Log**.  
    ![Portal do Azure](./media/log-analytics-get-started/log-analytics-portal.png)
2. Clique em **criar**, em seguida, selecione opções para Olá itens a seguir:
   * **Espaço de trabalho OMS** - digite um nome para o espaço de trabalho.
   * **Assinatura** - se você tiver várias assinaturas, escolha Olá aquele que você deseja tooassociate com o novo espaço de trabalho de saudação.
   * **Grupo de recursos**
   * **Localidade**
   * **Tipo de preços**  
       ![criação rápida](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Clique em **Okey** toosee uma lista dos espaços de trabalho.
4. Selecione um espaço de trabalho toosee seus detalhes na Olá portal do Azure.       
    ![detalhes do espaço de trabalho](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>Pesquisa de log de toonew do espaço de trabalho de atualização 3
Foi lançada uma nova linguagem de consulta de análise de Log e na ordem tootake vantagens, você precisa tooconvert seu espaço de trabalho.  Se região Olá hospedado em seu espaço de trabalho tiver sido atualizado, você verá um banner roxo na parte superior de saudação do seu espaço de trabalho convidar você tooconvert. atualização de saudação é totalmente voluntária e não afeta a sua experiência com a análise de Log e as soluções que você adicionar.  

Para mais benefícios do informações toounderstand hello, considerações e tooupgrade de processo, consulte [pesquisa de log do Azure Log Analytics atualizando toonew](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Adicionar soluções e ofertas de soluções

Em seguida, adicione soluções de gerenciamento e ofertas de soluções. As soluções de gerenciamento são uma coleção de lógica, visualização e regras de aquisição de dados que fornecem as métricas que giram em torno de uma área de problema específica. Uma oferta de solução é um pacote de soluções de gerenciamento.

Adicionar espaço de trabalho de tooyour soluções permite toocollect de análise de Log vários tipos de dados de computadores que estão conectados tooyour de espaço de trabalho usando agentes. Abordaremos os agentes de integração posteriormente.

### <a name="tooadd-solutions-and-solution-offerings"></a>soluções de tooadd e ofertas de solução

1. No portal do Azure, clique em **novo** e, em seguida, em Olá **marketplace de saudação pesquisa** , digite **análise de Log de atividade** e pressione ENTER.
2. Em Olá tudo folha, selecione **análise de Log de atividade** e, em seguida, clique em **criar**.  
    ![Log Analytics de Atividade](./media/log-analytics-get-started/activity-log-analytics.png)  
3. Em Olá *nome de solução de gerenciamento* folha, selecione um espaço de trabalho que você deseja tooassociate com solução de gerenciamento de saudação.
4. Clique em **Criar**.  
    ![espaço de trabalho da solução](./media/log-analytics-get-started/solution-workspace.png)  
5. Repita as etapas 1 a 4 tooadd:
    - Olá **segurança e conformidade** oferta de serviço com soluções de avaliação de Antimalware e segurança e auditoria hello.
    - Olá **controle e automação** oferta de serviço com hello Hybrid Worker de automação, controle de alterações e soluções de avaliação de atualização do sistema (também chamado de gerenciamento de atualizações). Quando você adicionar a oferta de solução hello, você deve criar uma conta de automação.  
        ![Conta de automação](./media/log-analytics-get-started/automation-account.png)  
6. Você pode exibir hello soluções de gerenciamento que você adicionou o espaço de trabalho tooyour navegando muito**análise de Log** > **assinaturas** > ***denomedeespaçodetrabalho***  >  **Visão geral**. Blocos Olá soluções de gerenciamento que você adicionou são mostrados.  
    >[!NOTE]
    >Porque estamos ainda não se conectou qualquer espaço de trabalho de toohello de agentes, você não vir todos os dados para soluções de saudação que você adicionou.  

    ![blocos de solução sem dados](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 Criar uma VM e integrar um agente

Em seguida, crie uma máquina virtual simples no Azure. Depois de criar uma VM, Olá integrado OMS agente tooenable-lo. Habilitar agente de saudação inicia a coleta de dados de saudação VM e envia dados tooLog análise.

### <a name="toocreate-a-virtual-machine"></a>toocreate uma máquina virtual

- Siga as orientações de saudação em [criar sua primeira máquina virtual do Windows no portal do Azure de saudação](../virtual-machines/virtual-machines-windows-hero-tutorial.md) e iniciar a máquina virtual da nova hello.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Conecte-se Olá máquina virtual tooLog análise

- Siga as orientações de saudação em [tooLog de máquinas virtuais do Azure conectar análise](log-analytics-azure-vm-extension.md) tooconnect Olá VM tooLog análise usando Olá portal do Azure.

## <a name="6-view-and-act-on-data"></a>6 Exibir e agir sobre os dados

Anteriormente, você ativou a solução de análise de Log de atividade de saudação e ofertas de serviços de segurança e conformidade e automação e controle de saudação. Em seguida, vamos começar a examinar os dados coletados pelas soluções e os resultados em pesquisas de log.

toostart, examine os dados que são exibidos no dentro de soluções. Em seguida, examine algumas pesquisas de log que são acessadas por meio de pesquisas de log. Pesquisas de log permitem toocombine e correlacionam dados de computador de várias fontes em seu ambiente. Para obter mais informações, consulte [pesquisas de Log na análise de Log](log-analytics-log-searches.md) ou se você converteu a espaço de trabalho toohello nova linguagem de consulta, consulte [log Noções básicas sobre pesquisa na análise de Log](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview dados Antimalware

1. Olá portal do Azure no, navegue muito**análise de Log** > ***seu espaço de trabalho***.
2. Na folha de saudação para seu espaço de trabalho em **geral**, clique em **visão geral**.  
    ![Visão geral](./media/log-analytics-get-started/overview.png)
3. Clique em Olá **avaliação Antimalware** lado a lado. Neste exemplo, você pode ver que o Windows Defender está instalado em um computador, mas sua assinatura está desatualizada.  
    ![Antimalware](./media/log-analytics-get-started/solution-antimalware.png)
4. Neste exemplo, em **status de proteção**, clique em **assinatura desatualizada** tooopen pesquisa de Log e exibir os detalhes sobre os computadores de saudação que têm assinaturas desatualizadas. Neste exemplo, observe que esse computador Olá é denominado *getstarted*. Se houver mais de um computador com assinaturas desatualizadas, todos os apareceriam na pesquisa de Log de saudação resultados.  
    ![Antimalware desatualizado](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview dados de segurança e auditoria

1. Na folha de saudação para seu espaço de trabalho em **geral**, clique em **visão geral**.  
2. Clique em Olá **segurança e auditoria** lado a lado. Neste exemplo, você pode ver que há dois problemas importantes: há um computador com atualizações críticas ausentes e há um computador com proteção insuficiente.  
    ![Segurança e Auditoria](./media/log-analytics-get-started/security-audit.png)
3. Neste exemplo, em **problemas importantes**, clique em **computadores com atualizações críticas ausentes** tooopen pesquisa de Log e exibir os detalhes sobre os computadores com atualizações críticas ausentes. Neste exemplo, há uma atualização crítica ausente e 63 outras atualizações ausentes.  
    ![Pesquisa de Logs de Auditoria e Segurança](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview e agir sobre dados de atualização do sistema

1. Na folha de saudação para seu espaço de trabalho em **geral**, clique em **visão geral**.  
2. Clique em Olá **avaliação de atualização do sistema** lado a lado. Neste exemplo, você pode ver que há um computador Windows chamado *getstarted* que precisa de atualizações críticas e um que precisa de atualizações de definição.  
    ![Atualizações do Sistema](./media/log-analytics-get-started/system-updates.png)
3. Neste exemplo, em **atualizações ausentes**, clique em **atualizações críticas** tooopen pesquisa de Log e exibir os detalhes sobre os computadores com atualizações críticas ausentes. Neste exemplo, há uma atualização ausente e há uma atualização necessária.  
    ![Pesquisa de Logs de Atualizações do Sistema](./media/log-analytics-get-started/system-updates-log-search.png)
4. Vá toohello [Operations Management Suite](http://microsoft.com/oms) site e entre com sua conta do Azure. Quando conectado, observe que as informações de solução de saudação são semelhante toowhat consulte Olá portal do Azure.  
    ![Portal do OMS](./media/log-analytics-get-started/oms-portal.png)
5. Clique em Olá **Update Management** lado a lado.
6. No painel de gerenciamento de atualização de hello, observe que informações de atualização de sistema Olá toohello atualização do sistema informações semelhantes que você viu no hello portal do Azure. No entanto, Olá **gerenciar implantações de atualização** lado a lado é nova. Clique em Olá **gerenciar implantações de atualização** lado a lado.  
    ![Bloco de Gerenciamento de Atualização](./media/log-analytics-get-started/update-management.png)
7. Em Olá **atualizar implantações** , clique em **adicionar** toocreate um *execução de atualização*.  
    ![Implantações de Atualização](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  Em Olá **nova implantação de atualização** página, digite um nome para a implantação de atualização de saudação, selecione computadores tooupdate (neste exemplo, *getstarted*), escolha uma agenda e, em seguida, clique em **salvar**.  
    ![Nova Implantação](./media/log-analytics-get-started/new-deployment.png)  
    Depois de salvar a implantação de atualização de saudação, você ver Olá agendado atualizar.  
    ![atualização agendada](./media/log-analytics-get-started/scheduled-update.png)  
    Após a execução de atualização hello, Olá status mostra **concluído**.
    ![atualização concluída](./media/log-analytics-get-started/completed-update.png)
9. Após a execução de atualização hello, você pode exibir se Olá executar foi bem-sucedida ou não, e você pode exibir detalhes sobre quais atualizações onde aplicado.

## <a name="after-evaluation"></a>Após a avaliação

Neste tutorial, você instalou um agente em uma máquina virtual e começou a trabalhar rapidamente. etapas de saudação que você seguiu foram rápida e simples. No entanto, a maioria das grandes organizações e empresas tem infraestruturas de TI locais complexas. Portanto, coleta de dados em ambientes complexos leva adicionais de planejamento e esforço que o tutorial hello. Revise as informações de Olá Olá próxima seção etapas para artigos de toohelpful links a seguir.

Você também pode remover o espaço de trabalho de saudação que você criou com este tutorial.

## <a name="next-steps"></a>Próximas etapas
* Saiba como conectar [agentes do Windows](log-analytics-windows-agents.md) tooLog análise.
* Saiba como conectar [agentes do Operations Manager](log-analytics-om-agents.md) tooLog análise.
* [Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.
* Familiarize-se com [pesquisas de log](log-analytics-log-searches.md) tooview detalhadas informações coletadas por meio de soluções.
