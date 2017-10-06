---
title: "Sincronização do Azure AD Connect: compreender e personalizar a sincronização | Microsoft Docs"
description: "Explica como funciona a sincronização do Azure AD Connect e como toocustomize."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Sincronização do Azure AD Connect: compreender e personalizar a sincronização
Serviços de sincronização do Azure Active Directory Connect da saudação (sincronização do Azure AD Connect) é um componente principal do Azure AD Connect. Cuida de todas as operações de saudação que estão relacionadas toosynchronize os dados de identidade entre o ambiente local e o AD do Azure. Sincronização do Azure AD Connect é o sucessor de saudação do DirSync, a sincronização do AD do Azure e o Forefront Identity Manager com hello que Azure Active Directory Connector configurado.

Este tópico é saudação inicial para **sincronização do Azure AD Connect** (também chamado de **mecanismo de sincronização**) e listas de links tooall outros tooit de tópicos relacionados. Para links tooAzure AD Connect, consulte [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

serviço de sincronização de saudação consiste em dois componentes, Olá local **sincronização do Azure AD Connect** lado do serviço de componente e hello no AD do Azure chamado **o serviço de sincronização do Azure AD Connect**. serviço de saudação é comum para DirSync, sincronização do AD do Azure e o Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Tópicos da sincronização do Azure AD Connect
| Tópico | O que ela abrange e quando tooread |
| --- | --- |
| **Noções básicas sobre a sincronização do Azure AD Connect** | |
| [Entendendo a arquitetura de saudação](active-directory-aadconnectsync-understanding-architecture.md) |Para aqueles que são o mecanismo de sincronização do novo toohello e deseja toolearn sobre a arquitetura de saudação e termos Olá usados. |
| [Conceitos técnicos](active-directory-aadconnectsync-technical-concepts.md) |Uma versão curta do tópico de arquitetura hello e brevemente explica Olá termos usados. |
| [Topologias para o Azure AD Connect](active-directory-aadconnect-topologies.md) |Descreve Olá diferentes topologias e cenários Olá sincronização mecanismo oferece suporte. |
| **Configuração personalizada** | |
| [Em execução Olá Assistente de instalação novamente](active-directory-aadconnectsync-installation-wizard.md) |Explica as opções que você tem disponível quando você executar novamente o Assistente de instalação do hello Azure AD Connect. |
| [Noções básicas sobre provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Descreve o modelo de configuração de saudação chamado provisionamento declarativo. |
| [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Descreve a sintaxe de Olá Olá idioma da expressão usado no provisionamento declarativo. |
| [Compreendendo a configuração padrão da saudação](active-directory-aadconnectsync-understanding-default-configuration.md) |Descreve as regras de fora da caixa de saudação e a configuração padrão de saudação. Também descreve como regras Olá funcionam juntos para Olá toowork de cenários de fora da caixa. |
| [Compreendendo usuários e contatos](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Continua no tópico anterior hello e descreve como configuração Olá para usuários e contatos funciona em conjunto, em particular em um ambiente de várias floresta. |
| [Como toomake toohello uma alteração de configuração padrão](active-directory-aadconnectsync-change-the-configuration.md) |Explica como os fluxos de toomake um tooattribute de alteração de configuração comuns. |
| [Práticas recomendadas para alterar a configuração padrão de saudação](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Limitações de suporte e para fazer alterações toohello out-of-box configuração. |
| [Configurar a filtragem](active-directory-aadconnectsync-configure-filtering.md) |Descreve Olá diferentes opções para como toolimit quais objetos estão sendo sincronizados tooAzure AD e passo a passo como tooconfigure essas opções. |
| **Recursos e cenários** | |
| [Impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Descreve Olá *impedir exclusões acidentais* recurso e como tooconfigure-lo. |
| [Agendador](active-directory-aadconnectsync-feature-scheduler.md) |Descreve o agendador interno hello, que está importando, sincronização e exportação de dados. |
| [Implementar a sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) |Descreve como funciona a sincronização de senha, como tooimplement e como toooperate e solucionar problemas. |
| [Write-back de dispositivo](active-directory-aadconnect-feature-device-writeback.md) |Descreve como o write-back de dispositivo funciona no Azure AD Connect. |
| [Extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md) |Descreve como tooextend Olá esquema do AD do Azure com seus próprios atributos personalizados. |
| **Serviço de Sincronização** | |
| [Recursos do serviço de sincronização do Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Descreve no lado do serviço de sincronização hello e como toochange configurações de sincronização no AD do Azure. |
| [Resiliência do atributo duplicado](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Descreve como tooenable e usar **userPrincipalName** e **proxyAddresses** resiliência de valores de atributo duplicado. |
| **Operações e interface do usuário** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Descreve Olá UI Synchronization Service Manager, incluindo [operações](active-directory-aadconnectsync-service-manager-ui-operations.md), [conectores](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Designer de metaverso](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), e [pesquisa Metaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) guias. |
| [Considerações e tarefas operacionais](active-directory-aadconnectsync-operations.md) |Descreve os problemas operacionais, como a recuperação de desastre. |
| **Como...** | |
| [Redefinir conta Olá AD do Azure](active-directory-aadconnectsync-howto-azureadaccount.md) |Como as credenciais de saudação de tooreset Olá da conta de serviço usadas tooconnect de tooAzure de sincronização de conexão do AD do Azure AD. |
| **Mais informações e referências** | |
| [Portas](active-directory-aadconnect-ports.md) |Lista quais portas precisa tooopen entre o mecanismo de sincronização de saudação e seus diretórios locais e do AD do Azure. |
| [Atributos sincronizados tooAzure do Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Lista todos os atributos que estão sendo sincronizados entre o AD local e o AD do Azure. |
| [Referência de funções](active-directory-aadconnectsync-functions-reference.md) |Lista todas as funções disponíveis no provisionamento declarativo. |

## <a name="additional-resources"></a>Recursos adicionais
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

