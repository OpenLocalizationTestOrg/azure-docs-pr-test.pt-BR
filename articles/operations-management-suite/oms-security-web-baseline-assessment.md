---
title: "aaaWeb avaliação de linha de base na linha de base de solução de auditoria e de segurança do Operations Management Suite | Microsoft Docs"
description: "Este documento explica como toouse web avaliação de linha de base na solução de segurança da OMS e auditoria tooperform uma avaliação de linha de base de todos os servidores da web monitorados para fins de conformidade e segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Avaliação de linha de base de Web na Solução de Segurança e Auditoria do Operations Management Suite
Este documento ajuda você a usar o OMS segurança e auditoria da web da linha de base avaliação recursos tooaccess Olá estado seguro de seus recursos monitorados.

## <a name="what-is-web-baseline-assessment"></a>O que é a avaliação de linha de base da Web?
Atualmente a Segurança do OMS oferece uma avaliação de linha de base para os sistemas operacionais. Ele examina as configurações de sistema operacional Olá dos servidores a cada 24 horas e fornece um modo de exibição para configurações potencialmente vulneráveis. Leia [Avaliação de Linha de Base na Solução de Segurança e Auditoria do Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) para saber mais informações sobre esta opção.

objetivo Olá Olá avaliação de linha de base da Web é toofind configurações do servidor de web vulnerável. Olá três fontes principais para as configurações de linha de base de web hello: configuração do .NET, ASP.NET e IIS.  Apenas como hello avaliação de linha de base do sistema operacional, o OMS segurança será tooscan seus servidores web todas as próximas 24 horas e fornecer uma exibição de estado de segurança-los.  No serviço de informações da Internet (IIS), as configurações são altamente personalizáveis, que permite que vários toobe níveis site e aplicativo substituído. o scanner Olá verifica as configurações de saudação em cada nível de site do aplicativo no nível de raiz adição toohello padrão. Isso ajuda você a configurações vulnerável tooidentify e corrigir rapidamente, juntamente com nossas recomendações para essas configurações.

>[!NOTE] 
>Você pode baixar Olá identificadores de configuração comuns e regras de linha de base usados pelo OMS segurança nesta [página](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Avaliação de linha de base de segurança da Web

Para essa visualização recurso Olá pode ser acessado via hello opção de pesquisa do OMS e Olá OMS segurança e auditoria painel. Siga as próximas etapas, Olá tooperform consulta de saudação apropriada:

1. Em Olá **Microsoft Operations Management Suite** painel principal, clique em **segurança e auditoria** lado a lado.
2. Em Olá **segurança e auditoria** painel, você pode ver a perspectiva de linha de base do Olá Web de linha de base perspectiva próxima toohello sistema operacional.
   
    ![Avaliação de linha de base de segurança na Web da Segurança e Auditoria do OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. painel esquerdo Olá mostra o número de saudação de servidores Web em comparação com toohello da linha de base, porcentagem média de saudação de regras que passaram em todos os servidores de saudação avaliada e Olá lista de servidores que são avaliadas.
4. Olá direita Olá exclusivo do painel lista de regras que falharam por *severidade*, e *RuleType*. Clicar em qualquer uma das regras do painel direito Olá mostrará detalhes Olá dessa regra. Um exemplo é mostrado no hello abaixo de imagem. regra de saudação que é avaliada é listada em *configuração de regra*. Olá *AzId* campo que é um identificador exclusivo para cada regra usado pela Microsoft para regras de linha de base de saudação de acompanhamento. Além disso toothat usuários podem ver Olá *resultado esperado* (valor de recomendado da Microsoft), e outros detalhes sobre o impacto de segurança de saudação de regra de saudação.
    
    ![Consultar](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Você pode criar suas próprias consultas tooreview resultados de saudação. 

Olá primeira consulta que você pode usar é Olá **Resumo da avaliação da linha de base**. Em Olá **Iniciar pesquisa aqui** , digite esta consulta: *tipo = SecurityBaselineSummary BaselineType = Web*. a seguir Olá é um exemplo de saída:

![Resultado da consulta](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>Nesta consulta, cada registro indica o resumo da avaliação em um único servidor.

Quando estiver no hello **pesquisa de Log**, você pode digitar tooobtain consultas diferentes para obter mais informações sobre a avaliação de linha de base Olá web. Além disso toohello de consulta anterior, você também pode usar Olá aqueles nesta visualização a seguir:

**Avaliação da regra de linha de base de Web**: Cada registro representa uma avaliação da regra de linha de base única Web em um único servidor. Ele inclui todos os dados para uma regra com falha, hello *SitePath* na qual Olá regra foi avaliada, hello *resultado esperado*e hello *resultado real*.

Consulta: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Resultado da consulta 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Mostrar todos os resultados para um servidor específico**: esta consulta mostra como toosee os resultados de um servidor específico: consulta: *tipo = SecurityBaseline BaselineType = computador Web = BaselineTestVM1*

![Resultado da consulta 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Você pode usar esses registros/consultas toocreate seus próprios painéis, relatórios ou alertas. Aqui está um exemplo de controle de interface do usuário que você pode adicionar tooyour painel. Você pode aprender como toovisualize os dados usando o Designer de exibição do OMS [aqui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). tela Hello abaixo é um exemplo de como Olá bloco se parecerá com depois de fazer essa personalização.

![painel Transações da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu sobre a avaliação de linha de base de Web da Segurança e Auditoria do OMS. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

