---
title: "aaaProtecting SQL Azure serviço e os dados na Central de segurança do Azure | Microsoft Docs"
description: "Este documento aborda as recomendações na Central de Segurança do Azure que ajudam a proteger seus dados e o serviço SQL do Azure, bem como a cumprir as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Proteção dos dados e do serviço SQL do Azure na Central de Segurança do Azure
Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações que o guiam pelo processo de saudação de Configurando controles de saudação necessário.  Recomendações se aplicam a tipos de recurso tooAzure: máquinas virtuais (VMs), redes, aplicativos e dados e SQL.

Este artigo aborda as recomendações que se aplicam a dados e o serviço do SQL tooAzure. As recomendações giram em torno de como habilitar a auditoria para os bancos de dados e servidores SQL do Azure, como habilitar a criptografia para bancos de dados SQL e como habilitar a criptografia da conta de armazenamento do Azure.  Uso tabela Olá abaixo como uma referência toohelp entender Olá recomendações disponíveis de serviço e os dados do SQL e o que faz cada uma se você aplicá-lo.

## <a name="available-sql-service-and-data-recommendations"></a>Recomendações de dados e serviço SQL disponíveis
| Recomendações | Descrição |
| --- | --- |
| [Habilitar a detecção de ameaças e auditoria em servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomenda que você habilite auditoria e detecção de ameaças para servidores Azure SQL (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais). |
| [Habilitar a detecção de ameaças e auditoria em bancos de dados SQL](security-center-enable-auditing-on-sql-databases.md) |Recomenda que você habilite auditoria e detecção de ameaças para bancos de dados SQL do Azure (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais). |
| [Habilitar Transparent Data Encryption em bancos de dados SQL](security-center-enable-transparent-data-encryption.md) |Recomenda que você habilite a criptografia para bancos de dados SQL (apenas serviço do Azure SQL). |

## <a name="see-also"></a>Consulte também
toolearn mais informações sobre recomendações que se aplicam a tipos de recursos do Azure tooother, consulte Olá seguinte:

* [Protegendo suas máquinas virtuais na Central de Segurança do Azure](security-center-virtual-machine-recommendations.md)
* [Protegendo seus aplicativos na Central de segurança do Azure](security-center-application-recommendations.md)
* [Protegendo sua rede na Central de Segurança do Azure](security-center-network-recommendations.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
