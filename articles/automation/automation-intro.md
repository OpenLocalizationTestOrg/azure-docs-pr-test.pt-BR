---
title: "aaaWhat é automação do Azure | Microsoft Docs"
description: "Saber qual é o valor fornece automação do Azure e obter respostas toocommon perguntas para que você pode começar criar, usar runbooks e DSC de automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "o que é automação, automação do azure, exemplos de automação do azure"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Visão geral da Automação do Azure
Automação do Microsoft Azure fornece uma maneira para os usuários tooautomate tarefas Olá manuais demoradas, propensas a erros e repetidas com frequência que geralmente são executadas em um ambiente de nuvem e enterprise. Economiza tempo e aumenta a confiabilidade de saudação de tarefas administrativas regulares e até mesmo agenda essas toobe automaticamente executada em intervalos regulares. Você pode automatizar processos usando runbooks ou automatizar o gerenciamento de configuração usando Configuração de Estado Desejado. Este artigo fornece uma visão geral da Automação do Azure e responde a perguntas comuns. Você pode consultar tooother artigos na biblioteca para obter mais informações sobre tópicos diferentes hello.

## <a name="automating-processes-with-runbooks"></a>Automatizando processos com runbooks
Um runbook é um conjunto de tarefas que executa um processo automatizado na Automação do Azure. Pode ser um processo simples, como iniciar uma máquina virtual e criar uma entrada de log, ou você pode ter um runbook complexo que combina outra tooperform de runbooks menor um processo complexo em vários recursos ou até mesmo várias nuvens e ambientes locais.  

Por exemplo, você pode ter um manual existente processar para truncar um banco de dados SQL se ele está chegando ao tamanho máximo que inclui várias etapas como conectar o servidor de toohello, conectar toohello banco de dados, obter o tamanho atual de saudação do banco de dados, verifique se limite foi excedido e trunque-o e notificar o usuário. Em vez de executar cada uma dessas etapas manualmente, você pode criar um runbook que executa todas essas tarefas como um único processo. Seria iniciar runbook hello, fornecem informações de saudação necessárias, como nome do servidor SQL Olá, nome do banco de dados e email do destinatário e, em seguida, ficam enquanto Olá processo for concluído. 

## <a name="what-can-runbooks-automate"></a>O que os runbooks podem automatizar?
Os runbooks na Automação do Azure são baseados no Windows PowerShell ou Fluxo de Trabalho do Windows PowerShell, portanto eles fazem tudo o que o PowerShell pode fazer. Se um aplicativo ou serviço tiver uma API, um runbook pode trabalhar com ele. Se você tiver um módulo do PowerShell para o aplicativo hello, você pode carregar o módulo para a automação do Azure e incluem esses cmdlets em seu runbook. Runbooks de automação do Azure executados em Olá nuvem do Azure e podem acessar quaisquer recursos de nuvem ou a recursos externos que podem ser acessados da nuvem de saudação. Usando [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), runbooks podem ser executados em seus dados locais recursos locais do centro toomanage. 

## <a name="getting-runbooks-from-hello-community"></a>Obtendo runbooks da comunidade Olá
Olá [Galeria de Runbook](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contém runbooks da comunidade Microsoft e hello que você pode usar inalterado em seu ambiente ou personalizá-los para seus próprios fins. Eles também são úteis tooas referências toolearn como toocreate seus próprios runbooks. Você mesmo pode contribuir sua própria galeria toohello de runbooks que você acha que outros usuários poderão ser úteis. 

## <a name="creating-runbooks-with-azure-automation"></a>Criação de Runbooks com a Automação do Azure
Você pode [criar seus próprios runbooks](automation-creating-importing-runbook.md) de rascunho ou modificar runbooks do hello [Galeria de Runbook](http://msdn.microsoft.com/library/azure/dn781422.aspx) para seus próprios requisitos. Há quatro [tipos de runbook](automation-runbook-types.md) diferentes entre os quais você pode escolher com base em seus requisitos e experiência do PowerShell. Se você preferir toowork diretamente com hello código do PowerShell, você pode usar um [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) ou [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) você editar offline ou com hello [editor textual](http://msdn.microsoft.com/library/azure/dn879137.aspx) em Olá portal do Azure. Se você preferir tooedit um runbook sem ser exposto toohello base de código, você pode criar um [runbook gráfico](automation-runbook-types.md#graphical-runbooks) usando Olá [editor gráfico](automation-graphical-authoring-intro.md) em Olá portal do Azure. 

Preferir assistir tooreading? Dê uma olhada nos Olá abaixo vídeo da sessão do Microsoft Ignite em maio de 2015. Observação: Enquanto hello conceitos e recursos abordados neste vídeo estão corretos, a que automação do Azure avançou muito desde que este vídeo foi registrado, ele agora tem uma interface de usuário mais extensas em hello portal do Azure e oferece suporte a outros recursos.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Automatizando o gerenciamento de configuração com a Configuração de Estado Desejado
[DSC do PowerShell](https://technet.microsoft.com/library/dn249912.aspx) é uma plataforma de gerenciamento que permite que você toomanage, implantar e reforçar a configuração para hosts físicos e máquinas virtuais usando uma sintaxe do PowerShell declarativa. Você pode definir configurações em um servidor de recepção DSC central que podem ser recuperadas e aplicadas automaticamente por computadores de destino. A DSC fornece um conjunto de cmdlets do PowerShell que você pode usar recursos e configurações de toomanage.  

[DSC de Automação do Azure](automation-dsc-overview.md) é uma solução baseada em nuvem para DSC do PowerShell que fornece os serviços necessários para ambientes corporativos.  Você pode gerenciar seus recursos de DSC na automação do Azure e aplicar configurações toovirtual ou computadores físicos que recuperá-los de um servidor de Pull de DSC em Olá nuvem do Azure.  Ele também fornece serviços de relatório que informam sobre eventos importantes, como nós que desviam de sua configuração atribuída e quando uma nova configuração foi aplicada. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Criando suas próprias configurações DSC com a Automação do Azure
[Configurações DSC](automation-dsc-overview.md) especificar estado Olá desejado de um nó.  Vários nós podem aplicar Olá tooassure de configuração mesmo que todos eles mantenham um estado idêntico.  Você pode criar uma configuração que usa qualquer editor de texto em seu computador local e importá-la para Automação do Azure, onde poderá compilá-la e aplicar nós.

## <a name="getting-modules-and-configurations"></a>Obtendo módulos e configurações
Você pode obter [módulos do PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) que contém cmdlets que você pode usar em seus runbooks e as configurações de DSC da saudação [Galeria do PowerShell](http://www.powershellgallery.com/). Você pode iniciar esta galeria da saudação portal do Azure e importar os módulos diretamente para a automação do Azure, ou você pode baixar e importá-los manualmente. Você não poderá instalar módulos Olá diretamente Olá portal do Azure, mas você pode baixá-los instalá-los como faria com qualquer outro módulo. 

## <a name="example-practical-applications-of-azure-automation"></a>Aplicações de exemplo da Automação do Azure
Seguem alguns exemplos de quais são os tipos de saudação de cenários de automação com a automação do Azure. 

* Criar e copiar máquinas virtuais em diferentes assinaturas do Azure. 
* Agendar cópias de arquivos de um contêiner de armazenamento de BLOBs do Azure de tooan do computador local. 
* Automatizar funções de segurança, como negar solicitações de um cliente, quando um ataque de negação de serviço é detectado. 
* Verifique se as máquinas se alinham continuamente com a política de segurança configurada.
* Gerencie a implantação contínua do código do aplicativo na nuvem e na infraestrutura local. 
* Crie uma floresta do Active Directory no Azure para seu ambiente de laboratório. 
* Truncar uma tabela em um banco de dados SQL se ele estiver se aproximando do tamanho máximo. 
* Atualize remotamente as configurações do ambiente de um Site do Azure 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Como a automação do Azure relacionados tooother ferramentas de automação?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) é pretendido tooautomate tarefas de gerenciamento na nuvem privada hello. Ele é instalado localmente em seu data center como um componente do [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/). SMA e automação do Azure usam Olá mesmo formato de runbook com base no Windows PowerShell e o fluxo de trabalho do Windows PowerShell, mas não oferece suporte a SMA [runbooks gráficos](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) destina-se à automação de recursos locais. Ele usa um formato diferente de runbook de automação do Azure e automação de gerenciamento de serviço e tem runbooks de toocreate uma interface gráfica sem a necessidade de qualquer script. Seus runbooks são compostos por atividades de Pacotes de Integração que são escritos especificamente para o Orchestrator. 

## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?
Uma variedade de recursos estão disponíveis para você toolearn mais informações sobre a automação do Azure e criar seus próprios runbooks. 

* **Biblioteca da Automação do Azure** é onde você está agora. artigos de Olá nesta biblioteca fornecem documentação completa sobre configuração de saudação e administração de automação do Azure e para a criação de seus próprios runbooks. 
* [Cmdlets do Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) fornece informações para automatizar operações do Azure usando o Windows PowerShell. Runbooks usar esses cmdlets toowork com recursos do Azure. 
* [Blog de gerenciamento](https://azure.microsoft.com/blog/tag/azure-automation/) fornece informações mais recentes de saudação na automação do Azure e outras tecnologias de gerenciamento da Microsoft. Você deve assinar toothis blog toostay backup toodate com hello mais recentes da equipe de automação do Azure hello. 
* [Fórum de automação](http://go.microsoft.com/fwlink/p/?LinkId=390561) permite que você toopost perguntas sobre a automação do Azure toobe abordados pela Microsoft e Olá comunidade de automação. 
* [Cmdlets de Automação do Azure](https://msdn.microsoft.com/library/mt244122.aspx) fornece informações sobre como automatizar tarefas administrativas. Ele contém as contas de automação toomanage cmdlets, ativos, runbooks, DSC.

## <a name="can-i-provide-feedback"></a>Posso fornecer comentários?
**Envie-nos comentários!** Se você estiver procurando por uma solução de runbook de Automação do Azure ou por um módulo de integração, poste uma Solicitação de script no Script Center. Se você tiver comentários ou solicitações de recurso para a Automação do Azure, poste-os em [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback). Obrigado! 

