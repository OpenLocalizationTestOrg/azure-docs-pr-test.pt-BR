---
title: "relatório de inteligência de ameaça de Central de segurança do aaaAzure | Microsoft Docs"
description: "Este documento ajuda a toouse Azure segurança Center ameaça Intelligent relatórios durante uma investigação toofind obter mais informações sobre um alerta de segurança."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Relatório de Inteligência de Ameaças da Central de Segurança do Azure
Este documento explica como os Relatórios Inteligentes de Ameças da Central de Segurança do Azure podem ajudá-lo a saber mais sobre uma ameaça que gerou um alerta de segurança.

## <a name="what-is-a-threat-intelligence-report"></a>O que é um relatório de inteligência de ameaças?
Detecção de ameaças de segurança central funciona pelo monitoramento de informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado. Ele analisa essas informações, geralmente correlacionando informações de várias fontes, tooidentify ameaças. Esse processo é parte da saudação Central de segurança [recursos de detecção de](security-center-detection-capabilities.md).

Quando a Central de Segurança identifica uma ameaça, ele dispara um [alerta de segurança](security-center-managing-and-responding-alerts.md), que contém informações sobre um evento específico, incluindo sugestões de correção detalhadas. as equipes de resposta a incidentes tooassist investigam e corrigir ameaças, Central de segurança inclui um relatório de inteligência de ameaça que contém informações sobre a ameaça de saudação que foi detectada, incluindo informações como o:

* Identidade ou associações do invasor (se essas informações estiverem disponíveis)
* Objetivos dos invasores
* Campanhas de ataque atuais e históricas (se essas informações estiverem disponíveis)
* Táticas, ferramentas e procedimentos dos invasores
* Indicadores associados de comprometimento (IoC), como URLs e hashes de arquivo
* Victimology, setor hello e tooassist predominância geográfica é determinar se os recursos do Azure estão em risco
* Informações de atenuação e correção

> [!NOTE]
> Olá quantidade de informações em qualquer relatório determinado irá variar; nível de saudação de detalhe baseia-se na atividade e a predominância saudação do malware.
>
>

Central de segurança tem três tipos de relatórios de ameaça, que podem variar de acordo ataque de toohello. Olá relatórios disponíveis são:

* **Relatório de Grupo de Atividades**: fornece análises avançadas sobre os invasores, seus objetivos e táticas.
* **Relatório de Campanha**: concentra-se nos detalhes de campanhas de ataque específicas.
* **Relatório de resumo de ameaças**: abrange todos os itens de saudação em dois relatórios de saudação anterior.

Esse tipo de informação é muito útil durante a saudação [resposta a incidentes](security-center-incident-response.md) processados, onde há uma fonte de saudação toounderstand investigação em andamento de ataque hello, motivações do invasor hello e o que toodo toomitigate isso problema no futuro.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Como tooaccess Olá relatório de inteligência de ameaça?
Você pode examinar os alertas atuais examinando Olá **alertas de segurança** lado a lado. Abra Olá Portal do Azure e siga as etapas de saudação abaixo toosee mais detalhes sobre cada alerta:

1. No painel de Central de segurança hello, você verá Olá **alertas de segurança** lado a lado.
2. Clique em Olá bloco tooopen Olá **alertas de segurança** folha que contém mais detalhes sobre alertas de saudação e clique no alerta de segurança Olá que você deseja tooobtain obter mais informações sobre.

    ![Alertas de segurança](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. Nesse caso Olá **suspeito processo executado** folha mostra detalhes Olá Olá alerta conforme mostrado na figura abaixo a saudação:

    ![Detalhes do alerta de segurança](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. quantidade de saudação das informações disponíveis para cada alerta de segurança variam de acordo tipo toohello de alerta. Em Olá **relatórios** campo tem um relatório de inteligência de ameaça de toohello do link. Clique nele e outra janela do navegador será exibida com o arquivo PDF.

   ![Seleção de armazenamento](./media/security-center-threat-report/security-center-threat-report-fig3.png)

Aqui você pode baixar Olá PDF para esse relatório e ler que mais sobre a segurança de saudação problema que foi detectado e executar ações com base nas informações de saudação fornecidas.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como os Relatórios de Inteligência de Ameaças da Central de Segurança do Azure podem ajudar durante uma investigação sobre alertas de segurança. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md). Localize as perguntas frequentes sobre como usar o serviço de saudação.
* [Aproveitando a Central de Segurança do Azure para a resposta a incidentes](security-center-incident-response.md)
* [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md). Saiba como tooplan e entender a Central de segurança do hello design considerações tooadopt do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md). Saiba como alertas de toosecurity toomanage e responder.
* [Manipulação de incidente de segurança na Central de Segurança do Azure](security-center-incident.md)
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre postagens no blog sobre a conformidade e segurança do Azure.
