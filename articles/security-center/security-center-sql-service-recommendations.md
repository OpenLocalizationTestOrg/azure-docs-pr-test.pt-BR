---
title: "Protegendo os dados e o serviço SQL do Azure na Central de Segurança do Azure | Microsoft Docs"
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
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="e54b6-103">Proteção dos dados e do serviço SQL do Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e54b6-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="e54b6-104">A Central de Segurança do Azure analisa o estado de segurança de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e54b6-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="e54b6-105">Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, ela cria recomendações que orientam você durante o processo de configuração dos controles necessários.</span><span class="sxs-lookup"><span data-stu-id="e54b6-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="e54b6-106">As recomendações se aplicam aos tipos de recurso do Azure: VMs (máquinas virtuais), rede, SQL e dados, e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e54b6-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="e54b6-107">Este artigo aborda as recomendações que se aplicam aos dados e serviço SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="e54b6-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="e54b6-108">As recomendações giram em torno de como habilitar a auditoria para os bancos de dados e servidores SQL do Azure, como habilitar a criptografia para bancos de dados SQL e como habilitar a criptografia da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e54b6-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="e54b6-109">Use a tabela abaixo como referência para entender as recomendações de dados e serviço SQL disponíveis e a ação de cada uma delas se forem aplicadas.</span><span class="sxs-lookup"><span data-stu-id="e54b6-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="e54b6-110">Recomendações de dados e serviço SQL disponíveis</span><span class="sxs-lookup"><span data-stu-id="e54b6-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="e54b6-111">Recomendações</span><span class="sxs-lookup"><span data-stu-id="e54b6-111">Recommendation</span></span> | <span data-ttu-id="e54b6-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="e54b6-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e54b6-113">Habilitar a detecção de ameaças e auditoria em servidores SQL</span><span class="sxs-lookup"><span data-stu-id="e54b6-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="e54b6-114">Recomenda que você habilite auditoria e detecção de ameaças para servidores Azure SQL (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="e54b6-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="e54b6-115">Habilitar a detecção de ameaças e auditoria em bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e54b6-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="e54b6-116">Recomenda que você habilite auditoria e detecção de ameaças para bancos de dados SQL do Azure (somente serviço Azure SQL; não inclui SQL em execução em máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="e54b6-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="e54b6-117">Habilitar Transparent Data Encryption em bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e54b6-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="e54b6-118">Recomenda que você habilite a criptografia para bancos de dados SQL (apenas serviço do Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="e54b6-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="e54b6-119">Confira também</span><span class="sxs-lookup"><span data-stu-id="e54b6-119">See also</span></span>
<span data-ttu-id="e54b6-120">Para saber mais sobre as recomendações que se aplicam aos outros tipos de recursos do Azure, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e54b6-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="e54b6-121">Protegendo suas máquinas virtuais na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e54b6-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="e54b6-122">Protegendo seus aplicativos na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e54b6-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="e54b6-123">Protegendo sua rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e54b6-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="e54b6-124">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e54b6-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e54b6-125">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) : saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e54b6-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e54b6-126">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="e54b6-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e54b6-127">[Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="e54b6-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
