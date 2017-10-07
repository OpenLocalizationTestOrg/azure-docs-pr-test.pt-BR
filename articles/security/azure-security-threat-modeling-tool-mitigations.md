---
title: "aaaMitigations - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "Página de atenuantes para Olá a ferramenta de modelagem de ameaças do Microsoft realce possíveis soluções toohello mais exposto gerada ameaças."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Mitigações do Microsoft Threat Modeling Tool

Olá, ferramenta de modelagem de ameaça é um elemento de núcleo do hello Microsoft Security Development Lifecycle (SDL). Ele permite que o software arquitetos tooidentify e atenuar problemas potenciais de segurança no início, quando eles são tooresolve relativamente fácil e econômica. Como resultado, ele reduz significativamente o custo total de desenvolvimento de saudação. Além disso, projetamos ferramenta Olá com especialistas de segurança não em mente, facilitando a modelagem de ameaças para todos os desenvolvedores, fornecendo uma orientação clara sobre como criar e analisar os modelos de risco.

Visite Olá  **[ferramenta de modelagem de ameaça](./azure-security-threat-modeling-tool.md)**  tooget iniciado hoje mesmo!

## <a name="mitigation-categories"></a>Categorias de mitigação

reduções de ferramenta de modelagem de ameaça Olá são categorizadas toohello quadro de segurança do aplicativo da Web, que consiste nos seguintes Olá de acordo com:

| Categoria | Descrição |
| -------- | ----------- |
| **[Auditoria e Log](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Quem fez o que e quando? Auditoria e log Consulte toohow seus eventos relacionados à segurança do aplicativo registros |
| **[Autenticação](./azure-security-threat-modeling-tool-authentication.md)** | Quem é você? Autenticação é o processo de saudação qual uma entidade comprova a identidade de saudação de outra entidade, normalmente por meio de credenciais, como um nome de usuário e senha |
| **[Autorização](./azure-security-threat-modeling-tool-authorization.md)** | O que você pode fazer? A autorização é como o seu aplicativo fornece controles de acesso para recursos e operações |
| **[Segurança da Comunicação](./azure-security-threat-modeling-tool-communication-security.md)** | Que você está falando com? Segurança de comunicação garante que toda a comunicação feita é tão segura quanto possível |
| **[Gerenciamento da Configuração](./azure-security-threat-modeling-tool-configuration-management.md)** | Que seu aplicativo executar como? Quais bancos de dados ele se conecta ao? Como o seu aplicativo é administrado? Como essas configurações são protegidas? Gerenciamento de configuração se refere a toohow seu aplicativo lida com esses problemas operacionais |
| **[Criptografia](./azure-security-threat-modeling-tool-cryptography.md)** | Como você mantém os segredos (confidencialidade)? Como são à prova de adulteração seus dados ou bibliotecas (integridade)? Como você gera valores aleatórios que devem ser criptograficamente forte? Criptografia refere-se toohow seu aplicativo impõe a integridade e confidencialidade |
| **[Gerenciamento de Exceções](./azure-security-threat-modeling-tool-exception-management.md)** | Quando uma chamada de método no seu aplicativo falha, o que ele faz? Quanto você revela? Você retorna erro amigável informações tooend os usuários? Você passa o chamador de toohello back informações úteis de exceção? Seu aplicativo não consegue normalmente? |
| **[Validação da Entrada](./azure-security-threat-modeling-tool-input-validation.md)** | Como você sabe que entrada hello recebe seu aplicativo é válidos e seguros? Validação de entrada refere-se toohow seu aplicativo filtra, limpa ou recusa dados antes do processamento adicional. Considere a restrição de entrada por meio de pontos de entrada e a codificação de saída por meio de pontos de saída. Você confia em dados de fontes, como bancos de dados e compartilhamentos de arquivos? |
| **[Dados Confidenciais](./azure-security-threat-modeling-tool-sensitive-data.md)** | Como o seu aplicativo lida com dados confidenciais? Dados confidenciais se refere a toohow seu aplicativo lida com dados que precisam ser protegidos na memória, rede hello, ou no armazenamento persistente |
| **[Gerenciamento da Sessão](./azure-security-threat-modeling-tool-session-management.md)** | Como o seu aplicativo controlar e proteger as sessões de usuário? Uma sessão refere-se a série de tooa de interações relacionadas entre um usuário e seu aplicativo da Web |

Isso ajuda a identificar:

* Onde está mais comuns cometidos Olá
* Onde está as melhorias mais viáveis Olá

Como resultado, você pode usa essas categorias toofocus e priorizar seu trabalho de segurança, para que se você souber de problemas de segurança mais frequente Olá ocorrem nas categorias de validação, autenticação e autorização de entrada de saudação, você pode iniciar de lá. Para saber mais, visite **[este link patenteado](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Próximas etapas

Visite  **[ameaças de ferramenta de modelagem de ameaça](./azure-security-threat-modeling-tool-threats.md)**  toolearn mais sobre Olá ameaça ferramenta de saudação categorias usa toogenerate ameaças de design possíveis.
