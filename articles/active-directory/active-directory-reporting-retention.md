---
title: "políticas de retenção de relatórios do Active Directory aaaAzure | Microsoft Docs"
description: "Políticas de retenção sobre dados de relatório no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Políticas de retenção de relatório do Azure Active Directory


Este tópico fornece respostas a perguntas mais comuns toohello em conjunto com a retenção de dados Olá para relatórios de atividade diferente Olá no Active Directory do Azure. 

**P: como você pode obter a coleção Olá de dados da atividade iniciados?**

**R:**

| Edição do Azure AD | Início da Coleta |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Quando você se inscreve para uma assinatura |
| AD do Azure Gratuito | Olá a primeira vez que abrir Olá [folha do Active Directory do Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou use Olá [reporting APIs](https://aka.ms/aadreports)  |

---
**P: quando seus dados de atividade está disponível no portal do Azure de saudação?**

**R:**

- **Imediatamente** - se você já estiver trabalhando com relatórios no hello portal clássico do Azure
- **Dentro de 2 horas** - se você não tiver ativado reporting em Olá portal clássico do Azure

---
**P: como você pode obter a coleção Olá de sinais de segurança iniciado?**  

**R:** para sinais de segurança, o processo de coleta Olá inicia quando você participar do Centro de proteção de identidade toouse hello. 


---
**P: por quanto tempo hello coletados dados são armazenados?**

**R:**

**Relatórios de atividades**    

| Relatório                 | AD do Azure Gratuito | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Auditoria de Diretório        | 7 dias        | 30 dias             | 30 dias             |
| Atividade de Entrada       | 7 dias        | 30 dias             | 30 dias             |

**Sinais de Segurança**

| Relatório         | AD do Azure Gratuito | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Usuários em risco  | 7 dias        | 30 dias             | 90 dias             |
| Entradas de risco | 7 dias        | 30 dias             | 90 dias             |

---