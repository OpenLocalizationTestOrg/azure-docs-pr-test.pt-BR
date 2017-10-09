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
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="ab509-103">Proteção dos dados e do serviço SQL do Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ab509-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="ab509-104">Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab509-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="ab509-105">Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações que o guiam pelo processo de saudação de Configurando controles de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="ab509-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="ab509-106">Recomendações se aplicam a tipos de recurso tooAzure: máquinas virtuais (VMs), redes, aplicativos e dados e SQL.</span><span class="sxs-lookup"><span data-stu-id="ab509-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="ab509-107">Este artigo aborda as recomendações que se aplicam a dados e o serviço do SQL tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ab509-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="ab509-108">As recomendações giram em torno de como habilitar a auditoria para os bancos de dados e servidores SQL do Azure, como habilitar a criptografia para bancos de dados SQL e como habilitar a criptografia da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab509-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="ab509-109">Uso tabela Olá abaixo como uma referência toohelp entender Olá recomendações disponíveis de serviço e os dados do SQL e o que faz cada uma se você aplicá-lo.</span><span class="sxs-lookup"><span data-stu-id="ab509-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="ab509-110">Recomendações de dados e serviço SQL disponíveis</span><span class="sxs-lookup"><span data-stu-id="ab509-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="ab509-111">Recomendações</span><span class="sxs-lookup"><span data-stu-id="ab509-111">Recommendation</span></span> | <span data-ttu-id="ab509-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="ab509-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ab509-113">Habilitar a detecção de ameaças e auditoria em servidores SQL</span><span class="sxs-lookup"><span data-stu-id="ab509-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="ab509-114">Recomenda que você habilite auditoria e detecção de ameaças para servidores Azure SQL (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="ab509-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="ab509-115">Habilitar a detecção de ameaças e auditoria em bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ab509-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="ab509-116">Recomenda que você habilite auditoria e detecção de ameaças para bancos de dados SQL do Azure (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="ab509-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="ab509-117">Habilitar Transparent Data Encryption em bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ab509-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="ab509-118">Recomenda que você habilite a criptografia para bancos de dados SQL (apenas serviço do Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="ab509-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="ab509-119">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ab509-119">See also</span></span>
<span data-ttu-id="ab509-120">toolearn mais informações sobre recomendações que se aplicam a tipos de recursos do Azure tooother, consulte Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab509-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="ab509-121">Protegendo suas máquinas virtuais na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ab509-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="ab509-122">Protegendo seus aplicativos na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ab509-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="ab509-123">Protegendo sua rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="ab509-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="ab509-124">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ab509-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ab509-125">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ab509-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ab509-126">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="ab509-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ab509-127">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab509-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
