---
title: "aaaAzure latências de relatórios do Active Directory | Microsoft Docs"
description: Quantidade de tempo que leva para relatar eventos tooshow backup no Active Directory do Azure
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 14367d21dfb28359f991037cc924d416420be456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-latencies"></a>Latências de relatório do Active Directory do Azure
*Esta documentação é parte da saudação [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).*

| Relatório | Mínimo | Média | Máximo |
| --- | --- | --- | --- |
| **Relatórios de segurança** | | | |
| Atividades de entrada irregulares |2 horas |4 horas |8 horas |
| Entradas de fontes desconhecidas |2 horas |4 horas |8 horas |
| Entradas após várias falhas |2 horas |4 horas |8 horas |
| Entradas de várias geografias |2 horas |4 horas |8 horas |
| Entradas de endereços IP com atividade suspeita |2 horas |4 horas |8 horas |
| Entradas de dispositivos possivelmente infectados |2 horas |4 horas |8 horas |
| Usuários com atividade de entrada anômala |2 horas |4 horas |8 horas |
| Usuários com credenciais vazadas |2 horas |4 horas |8 horas |
| Toda a atividade de conexão do usuário |2 horas |4 horas |8 horas |
| **Relatórios de aplicativo** | | | |
| Atividade de provisionamento de conta |2 horas |4 horas |8 horas |
| Erros de provisionamento de conta |2 horas |4 horas |8 horas |
| Uso do aplicativo |2 horas |4 horas |8 horas |
| Status de substituição de senha |2 horas |4 horas |8 horas |
| **Relatórios de Atividade e Auditoria** | | | |
| Relatório de auditoria |1 minuto |15 minutos |30 minutos |
| Atividade de redefinição de senha (Azure AD) |2 horas |4 horas |8 horas |
| Atividade de redefinição de senha (Identity Manager) |2 horas |4 horas |8 horas |
| Atividade de registro de redefinição de senha (Azure AD) |2 horas |4 horas |8 horas |
| Atividade de registro de redefinição de senha (Identity Manager) |2 horas |4 horas |8 horas |
| Atividade de grupos de autoatendimento (Azure AD) |2 horas |4 horas |8 horas |
| Atividade de grupos de autoatendimento (Identity Manager) |2 horas |4 horas |8 horas |
| **Relatórios RMS** | | | |
| Usuários RMS mais ativos |2 horas |4 horas |8 horas |
| Uso do RMS |2 horas |4 horas |8 horas |
| Uso de dispositivo do RMS |2 horas |4 horas |8 horas |
| Uso de aplicativos habilitados para RMS |2 horas |4 horas |8 horas |

