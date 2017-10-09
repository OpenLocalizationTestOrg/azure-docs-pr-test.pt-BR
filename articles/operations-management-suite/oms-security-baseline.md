---
title: "aaaOperations segurança do pacote de gerenciamento e de linha de base de solução de auditoria | Microsoft Docs"
description: "Este documento explica como toouse solução de segurança da OMS e auditoria tooperform uma avaliação de linha de base de todos os computadores monitorados para fins de conformidade e segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Avaliação de linha de base na Solução de Auditoria e Segurança do Operations Management Suite
Este documento ajuda toouse [Operations Management Suite (OMS) solução de segurança e auditoria](operations-management-suite-overview.md) tooaccess recursos Olá estado seguro de seus recursos monitorados de avaliação de linha de base.

## <a name="what-is-baseline-assessment"></a>O que é a Avaliação de Linha de Base?
A Microsoft, juntamente com organizações governamentais e do setor no mundo todo, define uma configuração do Windows que representa implantações de servidor altamente seguras. Essa configuração é um conjunto de chaves do registro, configurações de política de auditoria e configurações de política de segurança, juntamente com os valores recomendados da Microsoft para essas configurações. Esse conjunto de regras é conhecido como linha de base de Segurança. Recursos de avaliação da linha de base de Segurança e Auditoria do OMS podem examinar perfeitamente todos os seus computadores para fins de conformidade. 

Há três tipos de regras:

* **Regras de registro**: verificar se as chaves do registro estão definidas corretamente.
* **Regras de política de auditoria**: regras referentes à política de auditoria.
* **As regras de política de segurança**: regras sobre Olá permissões de usuário no computador de saudação.

> [!NOTE]
> Leitura [tooassess de segurança de uso do OMS Olá base de configuração de segurança](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) uma visão geral desse recurso.
> 
> 

## <a name="security-baseline-assessment"></a>Avaliação de Linha de Base de Segurança
Você pode examinar a avaliação da linha de base de segurança atual para todos os computadores que são monitorados pelo OMS segurança e auditoria usando o painel de saudação.  Execute Olá painel de avaliação de linha de base etapas tooaccess Olá segurança a seguir:

1. Em Olá **Microsoft Operations Management Suite** painel principal, clique em **segurança e auditoria** lado a lado.
2. Em Olá **segurança e auditoria** painel, clique em **avaliação de linha de base** em **domínios de segurança**. Olá **avaliação de linha de base de segurança** painel é exibido conforme mostrado no Olá a imagem a seguir:
   
    ![Avaliação de Linha de Base de Auditoria e Segurança do OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Este painel é dividido em três áreas principais:

* **Computadores em comparação com toobaseline**: Esta seção fornece um resumo do número de saudação de computadores que foram acessados e Olá percentual de computadores que passaram por avaliação de saudação. Ela também oferece Olá top 10 computadores e resultados de porcentagem Olá para avaliação de saudação.
* **Regras Status Requerido**: Esta seção tem reconhecimento de intenção toobring Olá Olá falha regras por gravidade e regras de tipo de falha. Procurando toohello primeiro gráfico que você pode identificar rapidamente se Olá a maioria das regras de falha são críticos, ou não. Ele também fornece uma lista de saudação 10 regras principais que falhou e severidade. gráfico segundo Olá mostra o tipo de saudação da regra que falhou durante a avaliação de saudação. 
* **Computadores sem a avaliação da linha de base**: Esta seção lista os computadores de saudação que não foram acessados devido a incompatibilidade de sistema toooperating ou falhas. 

### <a name="accessing-computers-compared-toobaseline"></a>Acessando computadores comparada toobaseline
Idealmente, todos os computadores estiverem ser compatível com a avaliação de linha de base de segurança hello. No entanto, é esperado que, em algumas circunstâncias, isso não aconteça. Como parte do processo de gerenciamento de segurança Olá, é importante tooinclude revisando computadores Olá falha toopass todos os testes de avaliação de segurança. Um toovisualize de maneira rápida está selecionando a opção de saudação **computadores acessados** localizado em Olá **computadores com toobaseline** seção. Você deve ver Olá log pesquisa resultados mostrando Olá a lista de computadores como mostra a saudação de tela a seguir:

![Resultados de computadores acessados](./media/oms-security-baseline/oms-security-baseline-fig2.png)

resultado da pesquisa Olá é mostrado em um formato de tabela, onde Olá primeira coluna tem o nome do computador hello e cor de segundo Olá tem o número de saudação de regras que falhou. informações de saudação tooretrieve relativa ao tipo de saudação da regra que falhou, clique no número de saudação de regras com falha, além do nome do computador hello. Você verá um toohello semelhante de resultado mostrada na Olá a imagem a seguir:

![Detalhes dos resultados de computadores acessados](./media/oms-security-baseline/oms-security-baseline-fig3.png)

Nesse resultado de pesquisa, você tem total de saudação de regras de acessadas, Olá número de regras essenciais que falharam, Olá regras de aviso e Olá regras Falha ao registrar informações.

### <a name="accessing-required-rules-status"></a>Acessando o status das regras necessárias
Depois de obter informações de saudação relativas a saudação de número de porcentagem de computadores que passaram por avaliação de saudação, talvez você queira tooobtain para obter mais informações sobre quais regras estão falhando criticidade de toohello de acordo. Isso o ajuda a visualização tooprioritize quais computadores devem ser abordados primeiro tooensure serão compatíveis na avaliação de Avançar hello. Passe o mouse sobre a parte fundamental Olá Olá gráfico localizado em Olá **falha regras por severidade** lado a lado, em **necessário status regras** e clique nele. Você verá um toohello semelhante resultado tela a seguir:

![Regras com falha por detalhes de gravidade](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

Esse resultado do log, você verá tipo hello da regra de linha de base que falharam, descrição Olá desta regra e a ID de enumeração de configuração comuns (CCE) Olá desta regra de segurança. Esses atributos deve ser suficiente tooperform toofix uma ação corretiva esse problema no computador de destino hello.

> [!NOTE]
> Para obter mais informações sobre o CCE, acessar Olá [banco de dados de vulnerabilidade National](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Acessando computadores sem avaliação de linha de base
OMS dá suporte para o membro de domínio hello e perfil de linha de base do controlador de domínio no Windows Server 2008 R2 até tooWindows Server 2012 R2. A linha de base do Windows Server 2016 ainda não é final e será adicionada assim que for publicada. Todos os outros sistemas operacionais verificados por meio de avaliação de linha de base de segurança da OMS e auditoria aparece sob Olá **computadores ausente avaliação de linha de base** seção.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu sobre a avaliação de linha de base da Segurança e Auditoria do OMS. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

