---
title: aaaAzure estudo de caso do Azure do banco de dados SQL - Daxko/CSI | Microsoft Docs
description: "Saiba como Daxko/CSI usa o banco de dados SQL tooaccelerate seu ciclo de desenvolvimento e tooenhance seus serviços de cliente e o desempenho"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI usado tooaccelerate Azure seu ciclo de desenvolvimento e tooenhance seus serviços de cliente e o desempenho
![Logotipo da CSI/Daxko](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Software Daxko/CSI enfrentam um desafio: sua base de clientes de centros de adequação e recreação foi crescendo rapidamente, Obrigado toohello sucesso de sua solução abrangente de software corporativo, mas acompanhando Olá infraestrutura de TI precisa para esse crescimento base de clientes foi testes da empresa Olá a equipe de TI. empresa Olá foi cada vez mais restrito pelo aumento sobrecarga de operações, particularmente para gerenciar seus bancos de dados em expansão. Pior, essa sobrecarga de operações foi Recortar em recursos de desenvolvimento para novas iniciativas, como novos recursos de mobilidade para o software da empresa hello.

De acordo com tooDavid Molina, diretor de desenvolvimento do produto em Daxko/CSI Azure Software CSI fornecido com hello plataforma como serviço (PaaS) modelo que ela toosimplify gerenciamento de banco de dados, aumentar a escalabilidade e liberar recursos toofocus em software em vez de operações. "O Banco de Dados SQL do Azure foi uma ótima opção para nós. Não ter tooworry sobre a manutenção de um SQL Server, um cluster de failover e Olá todas as outras necessidades de infraestrutura era ideal para nós."

Como migrar tooAzure, CSI Software precisa de uma equipe de operações de apenas dois toomanage em 600 bancos de dados do cliente. empresa de saudação usa pools de banco de dados do Azure SQL Elástico toomove bancos de dados do cliente com base no tamanho e precisam.

Continuar Molina, "nossos clientes acharam Olá alterar imediatamente. Antes dos pools elásticos, de vez em quando eles tinham tempos limite e outros problemas durante os períodos de intermitência. Com pools Elásticos do Azure, podem disparar conforme necessário e use o software de saudação sem problemas."

Além disso tooimproving o desempenho para os clientes, Azure pools Elásticos liberados recursos CSI Software toofocus sobre o desenvolvimento de novos serviços e recursos, em vez de lidar com operações e gerenciamento. Os recursos de TI ajudaram CSI Software melhorar seus softwares de enterprise oferta, SpectrumNG, toohelp envolver membros Academia, melhorar a eficiência da equipe e oferecem acesso móvel de equipe e membros para tarefas interativas e notificações em tempo real.

Azure também ajudou CSI Software acelerar e melhorar o desenvolvimento de saudação e ciclo de qualidade (QA) habilitando opções de automação. Com a implementação do Azure da empresa hello, gerenciadores de compilação podem empacotar componentes com hello clique de um botão. Como descrito Molina, "como parte do ciclo de lançamento do hello, controle de qualidade é agora capaz de toodeploy tooa ambiente de teste no Azure, que imita estreitamente nossa pilha de produção. Podemos implantar builds imediatamente tooour toovet de ambiente de desenvolvimento é alterado. Uma grande vitória para nós, pois não tínhamos paridade para testar antes disso".

## <a name="offloading-toohello-cloud"></a>Descarregamento de nuvem toohello
Antes de mover nuvem toohello, Software CSI tinha criados com êxito sua própria infraestrutura de multilocatária em um datacenter local em Houston. Empresa Olá expandida, ele enfrentados crescentes problemas crescentes de compra, provisionamento e manter todo o hardware hello e software necessário toosupport seus clientes. As operações de TI equipes toohandle tornou-se outro afunilamento que levaram tooa lentidão no provisionamento de novos recursos e implantar o novo toocustomers de serviços.

A CSI Software investigou as opções de nuvem para eliminar essa sobrecarga, de modo que ela pudesse focar em seu código, e não nas operações. empresa de saudação descobriu que muitos dos provedores de nuvem superior Olá oferecem apenas as soluções de infraestrutura como serviço (IaaS) que ainda exigem um grande conjunto de IaaS de TI equipe toomanage hello. No final do hello, Software CSI determinado que solução do Azure PaaS Olá Olá melhor opção para suas necessidades. Explica Molina, "Azure obtém software de hardware e sistema Olá fora do modo de hello, para que possa se concentrar em nossas ofertas de software, além de reduzir a sobrecarga de TI."

## <a name="making-hello-transition-tooazure"></a>Tornando Olá transição tooAzure
Depois de selecionar o Azure para sua solução de PaaS, Software CSI começou a migrar sua nuvem de toohello de infraestrutura e de bancos de dados back-end. TooAzure anterior, clientes SpectrumNG necessária tooinstall um aplicativo cliente que se comunicou com um serviço do Windows Communication Foundation (WCF) no back-end hello. TooMolina, de acordo com "Embora alguns clientes hospedado tudo em seus datacenters, criamos out multilocatário de toobe produto hello. Realizamos, tudo em um datacenter em Houston, usando o SQL Server como repositório de dados de saudação.

"Nossa oferta de produto também incluído um membro voltados portal da web (escrito em ASP.net), que era a presença de web do cliente do toobe projetado rotulada branco toomatch Olá e um páginas do SOAP API toosupport Olá online e nenhuma integração de terceiros".

nuvem de toohello de migração de saudação não continha longo para arquitetura de saudação. De acordo com tooMolina, "maioria de saudação do esforço Olá tratadas modificando a forma de saudação que podemos ler informações do arquivo de configuração, uma modificação de cadeia de conexão centralizado, e automatizar Olá empacotamento, o carregamento e a implantação do nosso versões."

automação de compilação toodevelop Olá, engenheiros de Software CSI usadas Azure PowerShell e APIs REST toocreate pacotes e carregá-los em ambiente de preparo tooa versão todas as noites.
Olá geral transição tooan implantação baseada em nuvem do Azure deu rapidamente e sem problemas para a equipe de TI de Software CSI hello. Explica Molina, "em todas, tivemos um ambiente beta na nuvem hello dentro de três semanas toofour de fazer em um projeto de saudação. Foi uma surpreendente vitória para nós".

Depois de configurar e testar hello ambiente, Software CSI começou a migração de clientes. Para clientes que já usam Software CSI hospedagem, transição Olá era quase contínua. Para migrar de uma implantação de local de clientes, nuvem de toohello de migração Olá levou algum tempo adicional, mas era ainda principalmente sem complicações para os clientes e Software CSI.

Para da novos clientes, Software CSI equipe de TI use Olá seguindo o processo tooon-placa-los tooAzure:

1. Scripts do PowerShell do Azure são usado toospin o novo banco de dados para o cliente Olá; todos os clientes iniciam em um tooensure de camada premium suficiente inicial de produtividade para transição hello.
2. Quando possível, CSI Software usa Olá Assistente de migração do SQL Azure toomove existente dados tooan Azure SQL Database instância.
3. Por fim, o Microsoft SQL Server Integration Services (SSIS) são usado tooreconcile quaisquer discrepâncias em dados saudação ou tooperform qualquer limpeza de dados como necessário.

Hoje, aproximadamente 99% dos clientes da CSI Software são hospedados no Azure, distribuídos em quatro datacenters regionais (Centro-Norte, Centro-Sul, Leste e Oeste). Tendo datacenters na região geográfica do cliente, a latência é mantida tooa mínimo.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Pools elásticos do Azure liberam recursos de TI
Vários recursos do Azure ajudaram CSI Software shift sejam recurso toobeing focada de infraestrutura e as operações e desenvolvimento com foco. Talvez o maior benefício de saudação foi de pools elásticos.

Atualmente, a CSI Software fornece aproximadamente 550 bancos de dados para os clientes. Antes de pools Elásticos, foi difícil toomanage que muitos bancos de dados em uma estrutura em camadas. Os gerentes de operações tinham tooassign níveis de desempenho com base nas necessidades de intermitência de saudação de clientes, o que é necessário significativo recursos de TI sobrecarga. Com os pools elásticos, os gerentes podem atribuir locatários a um pool premium ou standard, conforme apropriado e mover os clientes com base no tamanho e na necessidade. Os clientes acharam efeitos de saudação de pools Elásticos Olá quase imediatamente. antes de pools Elásticos, os clientes tinham tempos limite e outras questões durante períodos de uso de disparo, mas com pools Elásticos, os clientes podem enfrentar intermitências de atividade conforme necessário e eles poderão continuar toouse SpectrumNG sem problemas.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>A replicação geográfica ativa do Azure acelera a geração de relatórios
Vários clientes da CSI Software também estão se beneficiando com a replicação geográfica ativa do Azure. Com replicação geográfica, o toofour bancos de dados secundários legíveis podem ser configurados no hello datacenter mesmos ou em diferentes regiões. CSI Software faz uso de replicação geográfica de duas maneiras: primeiro, bancos de dados secundários Olá estão disponíveis no caso de saudação do datacenter interrupção ou hello dificuldades tooconnect toohello banco de dados primário; e, em segundo lugar, bancos de dados secundários Olá são legíveis e podem ser usado toooffload cargas de trabalho somente leitura, como trabalhos de relatório. Alguns clientes de Software CSI usar este tooaccelerate benefício fluxos de trabalho de emissão de relatórios.

## <a name="csi-software-application-logic-and-architecture"></a>Arquitetura e lógica de aplicativo da CSI Software
O SpectrumNG usa funções web. Como o aplicativo hello é multilocatário, um serviço WCF é usado toohandle solicitação de conexão inicial Olá de clientes. Como os estados de Molina "solicitação Olá identifica cada cliente, que permite que, em seguida, nos construir uma cadeia de caracteres de conexão out tootheir toodo de bancos de dados que precisamos toodo."

Para a camada da web de saudação do seu serviço, Software CSI tira proveito de dimensionamento automático do Azure, com base em dia e hora. Recursos disponíveis são automaticamente maior tooaccommodate maior uso durante o horário comercial, de acordo com o fuso horário toohello de cada data center regional. Recursos também são definidos tooscale para baixo nos finais de semana, quando as necessidades do cliente são inferiores.

![Arquitetura da Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Figura 1. Uma função de trabalho dos serviços de nuvem extrai dados estruturados do Banco de Dados SQL do Azure e dados semiestruturados do armazenamento de tabelas. Os usuários do SpectrumNG interagem com esses dados por meio de uma função web dos serviços de nuvem.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Usando aplicativos Web e uma camada de plano da Web para aplicativos móveis
Usando o banco de dados do SQL Azure liberação de recursos para o Software CSI tooenable novas iniciativas, incluindo uma plataforma móvel completa com base em uma API personalizada hospedada em aplicativos web do Azure. plataforma de saudação permite que os membros de Academia e agendas de toocheck de dispositivos móveis de toouse de equipe, classes de livro e receber mensagens.

plataforma Hello usa um único componente de tootake de arquitetura orientada a serviços (SOA) — como um sistema de ponto de venda (PDV) ou um sistema de vendas — movê-la para o plano para web tooanother Deslizar hello e acionamos um toosupport de serviço desse componente, deixando todos os outros elementos plano para web original Hello. Essa capacidade proporciona uma enorme flexibilidade à CSI Software, além de ajudar a reduzir os custos.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>O Azure permite que os desenvolvedores da CSI Software se concentram em aplicativos e serviços
Banco de dados SQL do Azure não é apenas um boon tooSpectrumNG os clientes que aproveite o serviço de saudação rápida e confiável, também é uma grande vantagem do software CSI equipe de TI e desenvolvedores. Descarregando tooAzure ops na nuvem hello, CSI Software reduziu a sua sobrecarga para recursos e a infraestrutura, muito acelerada seus ciclos de desenvolvimento e não precisa mais toomicromanage desempenho de toooptimize de bancos de dados para seus locatários.

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre pools Elásticos do Azure, consulte [pools Elásticos](sql-database-elastic-pool.md).
* toolearn mais sobre as ferramentas de banco de dados e a escala elástica, consulte [ferramentas de banco de dados Elástico e dimensionamento Elástico](sql-database-elastic-scale-get-started.md).
* Consulte toolearn mais sobre como migrar um banco de dados do SQL Server, consulte [migrar um tooAzure de banco de dados do SQL Server](sql-database-cloud-migrate.md).
* toolearn mais sobre a replicação geográfica, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md).
* toolearn mais informações sobre funções Web e funções de trabalho, consulte [funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais sobre o barramento de serviço do Azure, consulte [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn mais sobre o dimensionamento automático, consulte [dimensionando serviços de nuvem](../cloud-services/cloud-services-how-to-scale.md).

