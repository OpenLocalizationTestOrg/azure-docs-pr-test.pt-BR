---
title: "aaaAzure Glossário de proteção do Active Directory identidade | Microsoft Docs"
description: "Glossário do Azure Active Directory Identity Protection"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança, glossário"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Glossário do Azure Active Directory Identity Protection
### <a name="at-risk-user"></a>Em risco (Usuário)
Um usuário com um ou mais eventos de risco ativos. 

### <a name="atypical-sign-in-location"></a>Local de entrada atípico
Uma entrada de um local geográfico que não é comum para usuário específico hello, usuários semelhantes ou Locatário hello.

### <a name="azure-ad-identity-protection"></a>Azure AD Identity Protection
Um módulo de segurança do Azure Active Directory que fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades de uma organização.

### <a name="conditional-access"></a>Acesso condicional
Uma política para a proteção de acesso tooresources. Regras de acesso condicional são armazenadas em Olá Active Directory do Azure e são avaliadas pelo AD do Azure antes de conceder acesso toohello recursos.  As regras de exemplo incluem restrição baseada na localização do usuário, integridade do dispositivo ou método de autenticação do usuário.

### <a name="credentials"></a>Credenciais
Informações que incluem identificação e prova de identificação que é usado toogain acesso toolocal e recursos de rede. Exemplos de credenciais são nomes de usuário e senhas, cartões inteligentes e certificados.

### <a name="event"></a>Evento
Um registro de uma atividade no Azure Active Directory.

### <a name="false-positive-risk-event"></a>Falsos positivos (evento de risco)
Um status de evento de risco definido manualmente por um usuário de proteção de identidade, que indica que eventos de risco Olá foi investigado e foi marcado incorretamente como um evento de risco.

### <a name="identity"></a>Identidade
Uma pessoa ou entidade que deve ser verificada por meio de autenticação com base em critérios como senha ou certificado.

### <a name="identity-risk-event"></a>Evento de risco de identidade
Um evento AAD que foi marcado como anômalo pelo Identity Protection e pode indicar que uma identidade foi comprometida.

### <a name="ignored-risk-event"></a>Ignorado (evento de risco)
Um status de evento de risco definido manualmente por um usuário de proteção de identidade, que indica que eventos de risco hello está fechado sem executar uma ação de correção.

### <a name="impossible-travel-from-atypical-locations"></a>Viagem impossível de locais atípicos
Um evento de risco disparado quando duas entradas para Olá mesmo usuário são detectados, onde pelo menos um deles é um logon local atípico e onde o tempo de saudação entre Olá entradas é menor que Olá mínimo tempo levaria toophysically passam entre eles locais.  

### <a name="investigation"></a>Investigação
Olá processo de revisão Olá atividades, logs e outras informações relevantes relacionados tooa toodecide de evento de risco se são necessárias etapas de correção ou de redução, compreender se e como identidade Olá foi comprometido e compreender como Olá identidade comprometida foi usada.

### <a name="leaked-credentials"></a>Credenciais vazadas
Um evento de risco disparado quando as credenciais do usuário atual (nome de usuário e senha) são encontradas lançado publicamente no Olá web escuro pelos nossos pesquisadores.

### <a name="mitigation"></a>Redução
Uma ação toolimit ou elimine a capacidade de saudação de um invasor tooexploit uma identidade comprometida ou dispositivo sem estado de restauração Olá identidade ou dispositivo tooa seguro. Uma redução não resolver anterior eventos de risco associados à identidade hello ou dispositivo.

### <a name="multi-factor-authentication"></a>Autenticação multifator
Um método de autenticação que requer dois ou mais métodos de autenticação, que podem incluir algo Olá usuário tem, certificado; algo usuário Olá sabe, como nomes de usuário, senhas ou frases secretas; atributos físicos, como uma impressão digital; e atributos pessoais, como uma assinatura pessoal.

### <a name="offline-detection"></a>Detecção offline
detecção de saudação de anomalias e avaliação de risco de saudação de um evento, como a tentativa de logon depois de fato hello, para um evento que já tenha ocorrido.

### <a name="policy-condition"></a>Condição da política
Uma parte de uma política de segurança que define as entidades de saudação (grupos, usuários, aplicativos, plataformas de dispositivo, estados de dispositivo, os intervalos de IP, tipos de clientes) incluída na política de saudação ou excluídos dela.

### <a name="policy-rule"></a>Regra de política
parte de saudação de uma política de segurança que descreve circunstâncias Olá que irá disparar política Olá e as ações de Olá tomadas quando Olá política é acionada.

### <a name="prevention"></a>Prevenção
Uma ação tooprevent danos toohello organização por abuso de um dispositivo ou a identidade suspeita ou saber toobe comprometida. Uma ação de prevenção não proteger o dispositivo hello ou identidade e não resolve os eventos de risco anteriores.

### <a name="privileged-user"></a>Privilegiado (usuário)
Um usuário em tempo de saudação de um evento de risco tooone de permissões de administrador permanente ou temporária ou mais recursos no Azure Active Directory, como um Administrador Global, administrador de cobrança, administrador de serviço, o administrador de usuário e senha Administrador. 

### <a name="real-time"></a>Tempo real
Consulte Detecção em tempo real.

### <a name="real-time-detection"></a>Detecção em tempo real.
a detecção de anomalias Hello e avaliação de risco de saudação de um evento, como a tentativa de logon antes do evento de saudação é permitida tooproceed.

### <a name="remediated-risk-event"></a>Corrigido (evento de risco)
Um status de evento de risco definido automaticamente pela proteção de identidade, que indica que eventos de risco Olá foi corrigido usando a ação de correção padrão Olá para esse tipo de evento de risco. Por exemplo, quando a redefinição de senha de usuário do hello, muitos eventos de risco que indicam a que senha anterior Olá foi comprometida são automaticamente reparados.

### <a name="remediation"></a>Correção
Uma ação toosecure uma identidade ou um dispositivo que foram anteriormente suspeita ou toobe comprometidos. Uma ação de correção restaura Olá identidade ou dispositivo tooa seguro estado e resolve anterior eventos de risco associados à identidade hello ou dispositivo.

### <a name="resolved-risk-event"></a>Resolvido (evento de risco)
Um status de evento de risco definido manualmente por um usuário de proteção de identidade, indicando que o usuário Olá levou a uma ação de correção apropriada sem proteção de identidade e esse evento de risco Olá deve ser considerado fechadas.

### <a name="risk-event-status"></a>Status de evento de risco
Uma propriedade de um evento de risco, que indica se o evento hello está ativo e se fechado, motivo Olá para fechá-lo.

### <a name="risk-event-type"></a>Tipo de evento de risco
Uma categoria para Olá corre o risco de evento, indicando que o tipo de saudação de anomalias que causou a saudação evento toobe considerado arriscado.

### <a name="risk-level-risk-event"></a>Nível de risco (evento de risco)
Uma indicação (alto, médio ou baixo) de severidade de saudação de usuários de proteção de identidade Olá risco evento toohelp priorizar ações de saudação que levam a organização de tootheir tooreduce Olá risco. 

### <a name="risk-level-sign-in"></a>Nível de risco (entrada)
Uma indicação (alto, médio ou baixo) de probabilidade Olá que para um sign-in específico, alguém está tentando toouse Olá a identidade de usuário.

### <a name="risk-level-user-compromise"></a>Nível de risco (comprometimento do usuário)
Uma indicação (alto, médio ou baixo) de probabilidade Olá que uma identidade tiver sido comprometida.

### <a name="risk-level-vulnerability"></a>Nível de risco (vulnerabilidade)
Uma indicação (alto, médio ou baixo) de severidade de saudação de usuários de proteção de identidade Olá vulnerabilidade toohelp priorizar ações de Olá que levam a organização de tootheir tooreduce Olá risco.

### <a name="secure-identity"></a>Proteger (identidade)
Correção de agir como uma alteração de senha ou máquina Refazer toorestore um estado de tooan seguras identidade potencialmente comprometidos.

### <a name="security-policy"></a>Política de segurança
Uma coleção de regras e condição da política. Uma política pode ser aplicada tooentities como usuários, grupos, aplicativos, dispositivos, plataformas de dispositivo, estados de dispositivo, intervalos de IP e os tipos de cliente Auth2.0. Quando uma política estiver habilitada, ela é avaliada sempre que uma entidade incluída na política de saudação é emitida um token para um recurso.

### <a name="sign-in-v"></a>Entrar (v)
identidade de tooan tooauthenticate no Active Directory do Azure.

### <a name="sign-in-n"></a>Entrada (n)
processo de saudação ou ação de autenticar uma identidade no Active Directory do Azure e evento Olá que essa operação de captura.

### <a name="sign-in-from-anonymous-ip-address"></a>Entrada de um endereço IP anônimo
Um evento de risco disparado após uma entrada bem-sucedida de um endereço IP que foi identificado como um endereço IP de proxy anônimo.

### <a name="sign-in-from-infected-device"></a>Entradas de um dispositivo infectado
Um evento de risco disparado quando uma entrada se origina de um endereço IP que é conhecido toobe usado por um ou mais dispositivos comprometidos, que são ativamente tentar toocommunicate com um servidor de bot.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Entrada de um endereço IP com atividade suspeita
Um evento de risco acionado depois de uma entrada bem-sucedida de um endereço IP com um grande número de tentativas de logon com falha em várias contas de usuário em um curto período de tempo.

### <a name="sign-in-from-unfamiliar-location"></a>Entrada de um local desconhecido
Um evento de risco disparado quando um usuário entra com êxito de um novo local (IP, Latitude/Longitude e ASN).

### <a name="sign-in-risk"></a>Risco de entrada
Consulte Nível de risco (entrada)

### <a name="sign-in-risk-policy"></a>Política de risco de entrada
Uma política de acesso condicional que é avaliada Olá risco tooa sign-in específico e aplica atenuações com base em regras e condições predefinidas.

### <a name="user-compromise-risk"></a>Risco de comprometimento do usuário
Consulte Nível de risco (comprometimento do usuário)

### <a name="user-risk"></a>Risco do usuário
Consulte Nível de risco (comprometimento do usuário).

### <a name="user-risk-policy"></a>Política de risco do usuário
Uma política de acesso condicional que considera Olá entrar e aplica atenuações com base em regras e condições predefinidas.

### <a name="users-flagged-for-risk"></a>Usuários sinalizados por risco
Usuários que têm eventos de risco ativos ou corrigidos

### <a name="vulnerability"></a>Vulnerabilidade
Uma configuração ou a condição no Active Directory do Azure que torna Olá directory suscetíveis tooexploits ou ameaças.

## <a name="see-also"></a>Consulte também
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

