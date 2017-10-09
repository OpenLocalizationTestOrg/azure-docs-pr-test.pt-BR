---
title: "aaaOperations linha de base de Web de solução de auditoria e de segurança do pacote de gerenciamento | Microsoft Docs"
description: "Este documento explica como toouse solução de segurança da OMS e auditoria tooperform uma avaliação de linha de base da web de todos os servidores da web monitorados para fins de conformidade e segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Avaliação de linha de base de Web na Solução de Segurança e Auditoria do Operations Management Suite
Este documento ajuda toouse [Operations Management Suite (OMS) solução de segurança e auditoria](operations-management-suite-overview.md) web tooaccess recursos Olá estado seguro de seus recursos monitorados de avaliação de linha de base.

## <a name="what-is-web-baseline-assessment"></a>O que é a Avaliação de Linha de Base da Web?
Atualmente a Segurança do OMS oferece uma avaliação de linha de base para os sistemas operacionais. Ele examina as configurações de sistema operacional Olá dos servidores a cada 24 horas e fornece um modo de exibição para configurações potencialmente vulneráveis. Leia [Avaliação de Linha de Base na Solução de Segurança e Auditoria do Operations Management Suite](oms-security-baseline.md) para saber mais informações sobre esta opção.

meta de saudação da avaliação de linha de base de web hello é configurações do servidor web vulnerável toofind. Olá três fontes principais para as configurações de linha de base de web hello: configuração do .NET, ASP.NET e IIS.  Apenas como hello avaliação de linha de base do sistema operacional, o OMS segurança será tooscan seus servidores web todas as próximas 24 horas e fornecer uma exibição de estado de segurança-los.  No serviço de informações da Internet (IIS), as configurações são altamente personalizáveis, que permite que vários toobe níveis site e aplicativo substituído. o scanner Olá verifica as configurações de saudação em cada nível de site do aplicativo no nível de raiz adição toohello padrão. Isso ajuda você a locais de configurações de vulnerabilidade potencial tooidentify e corrigir rapidamente.


## <a name="web-security-baseline-assessment"></a>Avaliação de Linha de Base de Segurança da Web
Para essa visualização, este recurso será toobe acessado usando a opção de pesquisa do OMS hello. Siga as próximas etapas, Olá tooperform consulta de saudação apropriada:

1. Em Olá **Microsoft Operations Management Suite** clique de painel principal **segurança e auditoria** lado a lado.
2. Em Olá **segurança e auditoria** painel, clique em **pesquisa de Log** botão.
3. Olá primeira consulta que você pode usar é Olá **Resumo da avaliação da linha de base**. Em Olá **Iniciar pesquisa aqui** , digite esta consulta: tipo*= SecurityBaselineSummary BaselineType = web*. saudação de tela a seguir tem um exemplo de saída:

![Avaliação de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> Nesta consulta, cada registro indica o resumo da avaliação em um único servidor.

Quando estiver no hello **pesquisa de Log**, você pode digitar tooobtain consultas diferentes para obter mais informações sobre a avaliação de linha de base Olá web. Além disso toohello de consulta anterior, você também pode usar Olá aqueles nesta visualização a seguir.

**Avaliação da regra de linha de base de Web**: Cada registro representa uma avaliação da regra de linha de base única Web em um único servidor. Ela inclui todos os dados de regra hello, local, resultado Olá esperado e resultado real hello.

**Consulta**: Type*=SecurityBaseline BaselineType=web*

![Avaliação de regra de linha de base da Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Mostrar todos os resultados para um servidor específico**: esta consulta mostra como toosee os resultados de um servidor específico.

**Consulta**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Todos os resultados](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Você também pode usar esses registros/consultas toocreate seus próprios painéis, relatórios ou alertas. tela Hello abaixo tem um controle de interface do usuário de exemplo que você pode adicionar tooyour painel. Você pode aprender como toovisualize os dados usando o Designer de exibição do OMS [aqui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). tela Hello abaixo é um exemplo de como Olá bloco se parecerá com depois de fazer essa personalização.

![Interface de usuário de exemplo](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Se você quiser que as configurações de saudação tooknow marcados para avaliação de linha de base de saudação, você pode baixar [essa planilha do Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) que contenha essas configurações.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu sobre a avaliação de linha de base de Web da Segurança e Auditoria do OMS. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

