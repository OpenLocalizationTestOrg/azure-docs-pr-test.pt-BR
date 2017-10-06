---
title: "Visão geral do processo de ciência de dados de equipe aaaAzure | Microsoft Docs"
description: "Fornece uma análise preditiva toodeliver de metodologia dados ciência soluções e aplicativos inteligentes."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Visão geral do Processo de Ciência de dados de Equipe

Olá processo de ciência de dados da equipe (TDSP) é um agile soluções de análise preditiva do toodeliver de metodologia de ciência de dados iterativos e aplicativos inteligentes com eficiência. O TDSP ajuda a melhorar a colaboração e o aprendizado em equipe. Ele contém um distillation de práticas recomendadas de saudação e estruturas da Microsoft e de outras pessoas no setor de saudação que facilitam a implementação bem-sucedida de saudação do iniciativas de ciência de dados. meta de saudação é toohelp empresas totalmente obter benefícios de saudação do seu programa de análise.

Este artigo fornece uma visão geral do TDSP e de seus principais componentes. Fornecemos uma descrição genérica do processo de saudação aqui o que pode ser implementada com uma variedade de ferramentas. Uma descrição mais detalhada das tarefas de projeto de saudação e funções envolvidas no ciclo de vida de saudação do processo de saudação é fornecida nos tópicos vinculados adicionais. Orientação sobre como Olá tooimplement TDSP usando um conjunto específico de ferramentas da Microsoft e a infraestrutura que usamos Olá tooimplement TDSP nossas equipes também é fornecida.

## <a name="key-components-of-hello-tdsp"></a>Os principais componentes da saudação TDSP

TDSP compreende Olá componentes-chave a seguir:

- Uma definição de **ciclo de vida de ciência de dados**
- Uma **estrutura de projeto padronizada**
- **Infraestrutura e recursos** para projetos de ciência de dados
- **Ferramentas e utilitários** para execução do projeto


## <a name="data-science-lifecycle"></a>Ciclo de vida de ciência de dados

Olá processo de ciência de dados da equipe (TDSP) fornece um desenvolvimento do ciclo de vida toostructure Olá de seus projetos de ciência de dados. ciclo de vida de saudação descreve as etapas de hello, do início toofinish, que projetos normalmente seguem quando eles são executados.

Se você estiver usando outro ciclo de ciência de dados, como [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) ou o processo personalizado da organização, você ainda pode usar Olá TDSP baseado em tarefas no contexto de saudação desses desenvolvimento ciclos de vida. Em um alto nível, essas metodologias diferentes têm muito em comum. 

Esse ciclo de vida foi projetado para projetos de ciência de dados que devem ser fornecidos como parte de aplicativos inteligentes. Esses aplicativos implantam modelos de machine learning ou de inteligência artificial para análise preditiva. Os projetos de ciência de dados exploratórios ou os projetos de análise ad hoc também podem se beneficiar do uso desse processo. Mas, nesses casos algumas das etapas de saudação descritas não podem ser necessária.    

ciclo de vida do Hello TDSP é composto de cinco etapas principais que são executadas de forma iterativa:

* **Noções básicas sobre negócios**
* **Aquisição de dados e reconhecimento**
* **Modelagem**
* **Implantação**
* **Aceitação do cliente**

Aqui está uma representação visual de saudação **ciclo de vida do processo de ciência de dados de equipe**. 

![Ciclo de vida do TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Olá metas, tarefas e artefatos de documentação para cada estágio do ciclo de vida de saudação em TDSP descritos Olá [ciclo de vida do processo de ciência de dados de equipe](data-science-process-lifecycle.md) tópico. Essas tarefas e artefatos estão associados a funções do projeto:

- Arquitetura da solução
- Gerenciamento de projetos
- Cientista de dados
- Líder de projeto 

Olá diagrama a seguir fornece uma exibição de grade de tarefas de saudação (em azul) e os artefatos (em verde) associados a cada estágio do ciclo de vida da saudação (no eixo horizontal da saudação) para essas funções (no eixo vertical do hello). 

![Funções e tarefas de TDSP](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>Estrutura de projeto padronizada

Ter todos os projetos que compartilham uma estrutura de diretório e usar modelos de documentos do projeto facilita para Olá equipe membros toofind obter informações sobre seus projetos. Todos os documentos e código são armazenados em um sistema de controle de versão (VCS) como o Git, TFS ou Subversão tooenable colaboração em equipe. Rastreamento de tarefas e recursos em um projeto agile no sistema como Jira de controle, Rally, Visual Studio Team Services permite que mais próximo de controle do código de saudação para recursos individuais. Esse controle também permite que as equipes tooobtain melhor estimativas de custo. TDSP recomenda a criação de um repositório separado para cada projeto no hello VCS para colaboração, segurança de informações e controle de versão. Olá padronizados estrutura para todos os projetos ajuda a compilação conhecimento institucional da organização hello.

Fornecemos modelos de estrutura de pasta hello e documentos necessários nos locais padrão. Essa estrutura de pasta organiza os arquivos de saudação que contêm o código para exploração de dados e de extração de recurso e que registram iterações do modelo. Esses modelos facilitam para trabalho toounderstand membros da equipe feito por outras pessoas e tooadd novos membros tooteams. É fácil modelos de documento tooview e atualização no formato de markdown. Use listas de verificação de tooprovide modelos com perguntas mais importantes para tooinsure cada projeto que problema Olá é bem definido e que produtos atender qualidade Olá esperada. Os exemplos incluem:

- um problema de negócios do projeto compromisso toodocument hello e o escopo do projeto Olá
- estrutura de saudação toodocument e estatísticas de dados brutos de saudação de relatórios de dados
- saudação de toodocument do relatórios modelo derivado de recursos
- modelar métricas de desempenho como curvas de ROC ou MSE


![Diretórios de TDSP](./media/data-science-process-overview/tdsp-dir-structure.png)

estrutura de diretórios Olá pode ser clonada de [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infraestrutura e recursos para projetos de ciência de dados

O TDSP fornece recomendações para o gerenciamento de infraestrutura compartilhada de análise e armazenamento, como:

- sistemas de arquivos de nuvem para armazenamento de conjuntos de dados, 
- databases
- clusters de big data (Hadoop ou Spark) 
- serviços de machine learning. 

infraestrutura de armazenamento e análise Olá pode estar em nuvem hello ou local. É nela que os conjuntos de dados brutos e processados são armazenados. Essa infraestrutura permite a reprodução da análise. Ele também evita a eliminação de duplicação, que pode levar tooinconsistencies e custos de infraestrutura desnecessários. Ferramentas são fornecidas tooprovision Olá recursos compartilhados, controlá-los e permitir que cada tooconnect de membro da equipe toothose recursos com segurança. Também é uma prática recomendada que os membros do projeto criem um ambiente de computação consistente. Assim, membros diferentes da equipe podem replicar e validar experiências.

Confira um exemplo de uma equipe que trabalha em vários projetos e compartilha vários componentes da infraestrutura de análise em nuvem.

![Infraestrutura do TDSP](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Ferramentas e utilitários para execução do projeto

A introdução de processos na maioria das organizações é um desafio. Ferramentas fornecidas ciclo de vida e o processo de ciência de dados tooimplement Olá ajudam inferior tooand barreiras de saudação aumentar a consistência de saudação da adoção. TDSP fornece um conjunto inicial de scripts e ferramentas de adoção de início de toojump de TDSP dentro de uma equipe. Ele também ajuda a automatizar algumas tarefas comuns de saudação no ciclo de vida de ciência de dados a saudação como exploração de dados e modelagem de linha de base. Há uma estrutura bem definida fornecido para pessoas físicas toocontribute compartilhado ferramentas e utilitários no repositório de código compartilhado da sua equipe. Esses recursos podem ser aproveitados por outros projetos com a equipe de saudação ou organização hello. TDSP também planos tooenable contribuições de saudação da comunidade de todo toohello ferramentas e utilitários. utilitários TDSP Olá podem ser clonados de [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Próximas etapas

[Processo de ciência de dados de equipe: Funções e tarefas](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) descreve as funções de equipe chave hello e as tarefas associadas para uma equipe de ciência de dados que padroniza neste processo. 
