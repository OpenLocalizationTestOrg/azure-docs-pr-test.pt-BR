---
title: "aaaAzure AD conectar histórico de versão de integridade"
description: "Este documento descreve as versões Olá para integridade de conexão do AD do Azure e o que foi incluído nessas versões."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health: histórico de lançamento de versão
equipe do Active Directory do Azure Olá atualiza regularmente o Azure AD Connect Health com novos recursos e funcionalidade. Este artigo lista as versões de saudação e recursos que foram lançados.

## <a name="october-2016"></a>Outubro de 2016
**Atualização do agente:**

* Agente do Azure AD Connect Health para AD FS \(versão 2.6.408.0\)
  1. Aprimoramento da detecção de endereços IP do cliente nas solicitações de autenticação
  2. Correções de bugs relacionadas tooAlerts
* Agente do Azure AD Connect Health para AD DS (versão 2.6.408.0)
  1. Correções de bug relacionado tooAlerts.
* O agente do Azure AD Connect Health for Sync (versão 2.6.353.0) lançado com a versão 1.1.281.0 do Azure AD Connect
  1. Fornecer dados Olá necessário Olá relatórios de erros de sincronização
  2. Correções de bugs relacionadas tooAlerts

**Novos recursos de visualização:**

* Relatórios de erros de sincronização do Azure AD Connect

**Novos recursos:**

* O Azure AD Connect Health para AD FS - campo de endereço IP está disponível no relatório de saudação sobre superiores 50 usuários com nome de usuário e senha incorreto.

## <a name="july-2016"></a>Julho de 2016
**Novos recursos de visualização:**

* [Azure AD Connect Health para AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>Janeiro de 2016
**Atualização do agente:**

* Agente do Azure AD Connect Health para AD FS (versão 2.6.91.1512)

**Novos recursos:**

* [Ferramenta de Teste de Conectividade para agentes do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>Novembro de 2015
**Novos recursos:**

* Suporte ao [Controle de Acesso Baseado em Função](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**Novos recursos de visualização:**

* [Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md).

**Problemas corrigidos:**

* Correções de bug para erros exibidos durante os registros de agente.

## <a name="september-2015"></a>Setembro de 2015
**Novos recursos:**

* Relatório de senha de nome de usuário incorreto para o AD FS
* Suporte tooconfigure não autenticado HTTP Proxy
* Agente de tooconfigure suporte no Server core
* TooAlerts melhorias do AD FS
* Aprimoramentos no Agente do Azure AD Connect Health Agent para AD FS em conectividade e no upload de dados.

**Problemas corrigidos:**

* Correções de bugs em informações de uso para tipos de Erro do AD FS.

## <a name="june-2015"></a>Junho de 2015
**Versão inicial do Azure AD Connect Health para AD FS e para o Proxy do AD FS.**

**Novos recursos:**

* Alertas para o monitoramento de servidores do AD FS e do Proxy do AD FS com notificações por email.
* Topologia de tooAD FS acesso fácil e padrões nos contadores de desempenho do AD FS.
* A tendência em solicitações bem-sucedidas de token em servidores do AD FS agrupadas por Aplicativos, Métodos de Autenticação, Local de Rede da Solicitação etc.
* Tendências em solicitações com falha em servidores do AD FS agrupadas por Aplicativos, Tipos de Erro etc.
* Implantação mais simples de agente usando credenciais de Administrador Global do AD do Azure.  

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [monitorar seus serviços locais de infraestrutura e sincronização de identidade na nuvem Olá](active-directory-aadconnect-health.md).

