---
title: Teste de Caneta | Microsoft Docs
description: "O artigo fornece uma visão geral do processo (teste) dos testes de penetração e de como executar o teste de caneta em seus aplicativos em execução na infraestrutura do Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2017
ms.author: yurid
ms.openlocfilehash: dd5c874406ec184a2526a9eb0843cd6f3b6b3aa1
ms.sourcegitcommit: 094061b19b0a707eace42ae47f39d7a666364d58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="pen-testing"></a>Teste de Caneta
Um dos benefícios do uso do Azure para implantação e testes de aplicativos é que você pode criar rapidamente ambientes.  Você não precisa se preocupar sobre requisição, aquisição e "posicionamento no rack e empilhamento" do seu próprio hardware local.

Isso é ótimo, mas você ainda precisará certificar-se de executar a inspeção de segurança normal. Uma das coisas que você precisa fazer é o teste de penetração para os aplicativos que implantar no Azure.

Talvez você já saiba que a Microsoft realiza [teste de penetração do nosso ambiente do Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). Isso ajuda a gerar melhorias no Azure. 

Nós não fazemos teste de caneta em seu aplicativo para você, mas entendemos que você desejará e precisará executar testes de caneta em seus próprios aplicativos. Isso é uma boa coisa, porque quando você aumenta a segurança de seus aplicativos, você ajuda a tornar todo o ecossistema do Azure mais seguro.

O que fazer?

Desde 15 de junho de 2017, a Microsoft não exige aprovação prévia para realizar testes de penetração com base nos recursos do Azure. Os clientes que desejam documentar formalmente futuros testes de penetração no Microsoft Azure são incentivados a preencher o [formulário Notificação de teste de penetração do Azure Service](https://portal.msrc.microsoft.com/engage/pentest). Esse processo só está relacionado ao Microsoft Azure e não se aplica a outro serviço do Microsoft Cloud. 

>[!IMPORTANT] 
>Embora a notificação da Microsoft da caneta as atividades de teste não é mais necessário clientes ainda devem estar de acordo com o [Microsoft nuvem unificado penetração teste regras](https://technet.microsoft.com/en-us/mt784683). 

Os testes padrão que você pode executar incluem:

* Testes em seus pontos de extremidade para revelar as [10 maiores vulnerabilidades do OWASP (Projeto de Segurança de Aplicativo Web Aberto)](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Teste de fuzzing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) de seus pontos de extremidade
* [Exame de portas](https://en.wikipedia.org/wiki/Port_scanner) de seus pontos de extremidade

Um tipo de teste que você não pode executar é qualquer tipo de ataque [DoS (negação de serviço)](https://en.wikipedia.org/wiki/Denial-of-service_attack) . Isso inclui iniciar um ataque DoS em si ou a realização de testes relacionados que podem determinar, demonstrar ou simular qualquer tipo de ataque DoS.

## <a name="next-steps"></a>Próximas etapas

- Você está pronto para começar com testes de caneta em seus aplicativos hospedados no Microsoft Azure? Se estiver, vá diretamente para a página [Visão Geral do Teste de Penetração](https://technet.microsoft.com/library/mt784683.aspx) (e clique no botão Criar uma Solicitação de Teste na parte inferior da página). 