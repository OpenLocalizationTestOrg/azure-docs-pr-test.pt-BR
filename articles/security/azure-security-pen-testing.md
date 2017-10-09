---
title: aaaPen teste | Microsoft Docs
description: "artigo Olá fornece uma visão geral do processo (teste) de testes de invasão de saudação e como executar o teste em relação a seus aplicativos em execução na infraestrutura do Azure."
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
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Teste de Caneta
Uma das melhores coisas Olá sobre como usar o Microsoft Azure para implantação e testes de aplicativos é que você não precisa tooput juntos uma toodevelop de infraestrutura local, testar e implantar seus aplicativos. Toda a infra-estrutura de saudação é resolvido por serviços da plataforma Microsoft Azure hello. Você não tem tooworry sobre requisição, aquisição e "posicionamento no rack e empilhamento" seu próprio hardware local.

Isso é ótimo – mas você ainda precisa toomake se você executar a segurança normal Inspeções. Uma das coisas Olá precisar toodo é aplicativos de saudação de teste de penetração implantar no Azure.

Talvez você já saiba que a Microsoft realiza [teste de penetração do nosso ambiente do Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). Isso nos ajuda a melhorar nossa plataforma e guia as nossas ações em termos de melhorar os controles de segurança, introduzindo novos controles de segurança e melhorando nossos processos de segurança.

Nós não caneta testar seu aplicativo para você, mas, entendemos desejados e precisar de teste de caneta tooperform em seus próprios aplicativos. Que é bom, pois quando você aumentar a segurança de saudação de seus aplicativos, você ajudar a proteger melhor o ecossistema do Azure hello.

Quando você caneta testar seus aplicativos, pode parecer um ataque toous. Nós [monitoramos continuamente](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) em busca de padrões de ataque e iniciaremos um processo de resposta a incidente, se necessário. Isso não ajuda e ele não ajude-nos se podemos acionar uma resposta a incidentes vencimento tooyour próprio devido cuidado caneta teste.

Quais toodo?

Quando você está pronto toopen testar seus aplicativos hospedados do Azure, você tem uma opção muito[Fale conosco](https://portal.msrc.microsoft.com/en-us/engage/pentest). Depois que sabemos que você vai toobe realizar testes específicos, nós não inadvertidamente desligar (tal como endereço IP de saudação que você está testando de), como toohello do Azure está de acordo com seus testes da caneta teste termos e condições descritas em [Nuvem da Microsoft Unified regras de teste de penetração](https://technet.microsoft.com/en-us/mt784683).
Os testes padrão que você pode executar incluem:

* Os testes em seu Olá toouncover de pontos de extremidade [Web aplicativo segurança projeto (OWASP) abra top 10 vulnerabilidades](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Teste de fuzzing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) de seus pontos de extremidade
* [Exame de portas](https://en.wikipedia.org/wiki/Port_scanner) de seus pontos de extremidade

Um tipo de teste que você não pode executar é qualquer tipo de ataque [DoS (negação de serviço)](https://en.wikipedia.org/wiki/Denial-of-service_attack) . Isso inclui iniciar um ataque DoS em si ou a realização de testes relacionados que podem determinar, demonstrar ou simular qualquer tipo de ataque DoS.

São que pronto tooget iniciado com caneta para testar seus aplicativos hospedados no Microsoft Azure? Se assim, vá diretamente toohello [visão geral de teste de penetração](https://technet.microsoft.com/library/mt784683.aspx) página (e clique em Olá botão Criar uma solicitação de teste final Olá Olá página. Você também encontrará mais informações sobre caneta Olá teste termos e condições e links úteis em como você pode relatar tooAzure relacionados de falhas de segurança ou qualquer outro serviço da Microsoft.
