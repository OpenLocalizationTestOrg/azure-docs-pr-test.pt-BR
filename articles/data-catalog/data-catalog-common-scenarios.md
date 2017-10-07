---
title: "cenários comuns de catálogo de dados aaaAzure | Microsoft Docs"
description: "Uma visão geral dos cenários comuns para o catálogo de dados do Azure, incluindo registro hello e descoberta de fontes de dados de alto valor, habilitar o autoatendimento de business intelligence e captura de dados de conhecimento existente sobre fontes de dados e processos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Cenários comuns de Catálogo de Dados do Azure
Este artigo apresenta cenários comuns nos quais o Catálogo de Dados do Azure pode ajudar a sua organização a obter mais valor de suas fontes de dados existentes.

## <a name="scenario-1-registration-of-central-data-sources"></a>Cenário 1 – Registro de fontes de dados centrais
As organizações costumam têm várias fontes de dados de alto valor. Essas fontes de dados incluem linha de negócios, sistemas OLTP (processamento de transações online), data warehouses e bancos de dados de business intelligence/análise. Olá número de sistemas e Olá sobreposição entre eles, geralmente cresce ao longo do tempo, como as empresas precisam evoluir e negócios Olá em si evoluem por meio de, por exemplo, fusões e aquisições.

Pode ser difícil para organização membros tooknow onde toolocate Olá dados dentro dessas fontes de dados. Perguntas como Olá a seguir são todas muito comuns:

* De Olá HR três sistemas usado dentro da empresa hello, o que devo usar toocreate nesse tipo de relatório?
* Onde posso ir a saudação tooget certificada números de vendas do ano fiscal de saudação que acabou de encerrar?
* Que devo fazer ou o que é o processo de saudação deve usar o data warehouse do toohello de acesso de tooget?
* Não sei se esses números estão corretos. Que posso fazer para mais informações sobre como esses dados deve toobe usado para compartilhar este painel com minha equipe?

toothese e outras perguntas, catálogo de dados do Azure pode fornecer respostas. Olá central, alto valor, fontes de dados gerenciada de TI que são usados entre organizações costumam ponto de partida lógico Olá para popular o catálogo de saudação. Embora qualquer usuário pode registrar uma fonte de dados, com o catálogo de saudação kick-started com fontes de dados de hello são provavelmente tooprovide valor toohello maior número de usuários ajuda a estimular a adoção e o uso do sistema de saudação. 

Se você está começando a usar o catálogo de dados do Azure, identificar e registrar fontes de dados de chave que são usadas por muitas equipes diferentes de consumidores de dados podem ser o primeiro toosuccess de etapa.

Este cenário também apresenta toomake de fontes de dados de alto valor uma oportunidade tooannotate Olá-los mais fácil toounderstand e acesso. Um aspecto fundamental desse esforço é tooinclude informações sobre como os usuários podem solicitar a fonte de dados do access toohello. No catálogo de dados do Azure, você pode fornecer o endereço de email de saudação do usuário Olá, equipe responsável para controlar o acesso de fonte de dados, ferramentas de tooexisting links ou documentação ou texto livre que descreve o processo de solicitação de acesso de saudação. Essas informações ajudam a membros que descobrir fontes de dados registrado, mas que ainda não têm permissões tooaccess Olá dados tooeasily solicitação de acesso usando processos Olá definidos e que são controlados pelos proprietários de fonte de dados de saudação.

## <a name="scenario-2-self-service-business-intelligence"></a>Cenário 2 – Business intelligence de autoatendimento
Embora tradicionais soluções de business intelligence corporativas continuam toobe cenários de uma parte inestimável dos dados de muitas organizações, Olá alterando o ritmo dos negócios fez BI de autoatendimento mais importante. Usando BI de autoatendimento, operadores e analistas de informações podem criar seus próprios relatórios, pastas de trabalho e painéis sem depender de uma equipe de TI central nem ficar restrito pela programação e pela disponibilidade dessa equipe de TI.

Em cenários de BI de autoatendimento, é comum os usuários combinarem dados de várias fontes, muitas das quais podem não ter sido usadas anteriormente para BI e análise. Embora algumas dessas fontes de dados podem já ser conhecidas, pode ser um desafio toodiscover que toolocate toodo e avaliar as possíveis fontes de dados para uma determinada tarefa.

Tradicionalmente, esse processo de descoberta é um manual: analistas usam seu tooidentify de conexões de rede ponto a ponto que outras pessoas que trabalham com dados de saudação que está sendo procurados. Depois de uma fonte de dados é encontrada e é usada, Olá processo se repete novamente para cada subsequentes Self-service BI esforço, com vários usuários executando um processo manual redundante de descoberta.

Com o Catálogo de Dados do Azure, sua organização pode quebrar esse ciclo de esforço. Depois de descobrir uma fonte de dados através de meios tradicionais, um analista pode registrá-lo toomake-lo mais facilmente descobertas por outros usuários em Olá futuras. Embora analista Olá pode adicionar mais valor anotando Olá registrado ativos de dados, esta anotação não precisa tootake local a saudação mesmo momento como o registro. Os usuários podem contribuir ao longo do tempo, como permitir suas agendas, gradualmente adicionar fontes de dados do valor toohello registrados no catálogo de saudação.

Esse crescimento sistemático de conteúdo do catálogo de saudação é um registro inicial do complemento natural toohello de fontes de dados central. Pré-popular catálogo Olá com dados que muitos usuários precisarão pode ser uma motivação para uso inicial e descoberta. Habilitando usuários tooregister e anote fontes adicionais podem ser um tookeep de maneira envolvidos-los e outros membros da organização.

Vale a pena observar que embora este cenário se concentra especificamente no BI de autoatendimento, hello mesmo desafios e padrões se aplicam toolarge escala corporativos projetos de BI também. Usando o Catálogo de Dados, sua organização pode melhorar qualquer esforço que envolva um processo manual de descoberta de fonte de dados.

## <a name="scenario-3-capturing-tribal-knowledge"></a>Cenário 3 – Capturando o conhecimento do grupo
Como você sabe quais dados você precisa toodo seu trabalho e onde toofind dados?

Se você estiver na sua função por algum tempo, você provavelmente já sabe. Você já passaram por um processo de aprendizado de gradual e ao longo do tempo aprendeu sobre fontes de dados de saudação são tooyour chave suas tarefas diárias.

Quando um novo funcionário ingressa em sua equipe, como faz essa pessoa saber quais dados são necessários para o trabalho Olá e onde toofind-lo?

Probabilidade é, Olá nova pessoa vem tooyou com essas perguntas.

Essa transferência contínua de conhecimento tribal faz parte do processo de descoberta de fonte de dados de saudação em organizações grandes e pequenos. Membros da equipe mais experientes e sênior criados conhecimento ao longo de anos de saudação e os membros da equipe mais recentes aprendeu tooask-los quando eles tiverem perguntas. informações mais importantes Olá geralmente existem apenas na cabeçotes de saudação de algumas pessoas chave, e quando as pessoas estão em férias ou deixam equipe Olá, organização de saudação será prejudicado.

Especialistas de dados normalmente fazer um esforço toodocument seus dados de Conhecimento, compartilhá-lo por email ou em documentos do Word em um site de equipe do SharePoint. Embora essa abordagem pode ser valiosa, ela introduz um novo problema de descoberta: como fazer as pessoas saber quais documentação existe e onde toofind-lo?

No Catálogo de Dados do Azure, sua organização tem um único local central para armazenar e compartilhar esse conhecimento de grupo e tornar fácil descobri-lo. No catálogo de dados, os seus especialistas de dados podem anotar os ativos de dados diretamente e fornecem links tooexisting documentação. Quando os membros de organização usar Olá catálogo toodiscover uma fonte de dados, eles encontrarão não apenas a fonte de saudação em si, mas também conhecimento Olá que existia anteriormente apenas em mente Olá de especialistas em sua organização.
