---
title: "Tecnologias e serviços de segurança do Azure | Microsoft Docs"
description: "O artigo fornece uma lista estruturada das tecnologias e serviços de segurança do Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: a5a7f60a-97e2-49b4-a8c5-7c010ff27ef8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/02/2016
ms.author: yurid
ms.openlocfilehash: 0bea62a43cf6cac9132fe64f2d6c54e52def4c55
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-security-services-and-technologies"></a><span data-ttu-id="b7024-103">Tecnologias e serviços de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-103">Azure Security Services and Technologies</span></span>
<span data-ttu-id="b7024-104">Em nossas discussões com clientes do Azure atuais e futuros, frequentemente nos fazem a seguinte pergunta “você tem uma lista de todas as tecnologias e serviços relacionados à segurança que o Azure tem a oferecer?”</span><span class="sxs-lookup"><span data-stu-id="b7024-104">In our discussions with current and future Azure customers, we’re often asked “do you have a list of all the security related services and technologies that Azure has to offer?”</span></span>

<span data-ttu-id="b7024-105">Sabemos que, quando você estiver avaliando as opções técnicas do provedor de serviço de nuvem, é útil ter essa lista disponível para que você pode usá-la para se aprofundar ainda mais quando for o momento adequado para você.</span><span class="sxs-lookup"><span data-stu-id="b7024-105">We understand that when you’re evaluating your cloud service provider technical options, it’s helpful to have such a list available that you can use to dig down deeper when the time is right for you.</span></span>

<span data-ttu-id="b7024-106">A seguir está o nosso esforço inicial no fornecimento de uma lista.</span><span class="sxs-lookup"><span data-stu-id="b7024-106">The following is our initial effort at providing a list.</span></span> <span data-ttu-id="b7024-107">Ao longo do tempo, essa lista será alterada e aumentará, exatamente como o Azure.</span><span class="sxs-lookup"><span data-stu-id="b7024-107">Over time, this list will change and grow, just as Azure does.</span></span> <span data-ttu-id="b7024-108">A lista é categorizada e a lista de categorias também aumentará ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="b7024-108">The list is categorized, and the list of categories will also grow over time.</span></span> <span data-ttu-id="b7024-109">Lembre-se de visitar essa página regularmente para se manter atualizado sobre nossas tecnologias e serviços relacionados à segurança.</span><span class="sxs-lookup"><span data-stu-id="b7024-109">Make sure to check this page on a regular basis to stay up-to-date on our security-related services and technologies.</span></span>

## <a name="azure-security---general"></a><span data-ttu-id="b7024-110">Segurança do Azure: geral</span><span class="sxs-lookup"><span data-stu-id="b7024-110">Azure Security - General</span></span>
* [<span data-ttu-id="b7024-111">Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-111">Azure Security Center</span></span>](https://azure.microsoft.com/documentation/services/security-center/)
* [<span data-ttu-id="b7024-112">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-112">Azure Key Vault</span></span>](https://azure.microsoft.com/documentation/services/key-vault/)
* [<span data-ttu-id="b7024-113">Criptografia de Disco do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-113">Azure Disk Encryption</span></span>](azure-security-disk-encryption.md)
* [<span data-ttu-id="b7024-114">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b7024-114">Log Analytics</span></span>](../log-analytics/log-analytics-overview.md)
* [<span data-ttu-id="b7024-115">Azure Dev/Test Labs</span><span class="sxs-lookup"><span data-stu-id="b7024-115">Azure Dev/Test Labs</span></span>](https://azure.microsoft.com/documentation/services/devtest-lab/)

## <a name="azure-storage-security"></a><span data-ttu-id="b7024-116">Segurança do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-116">Azure Storage Security</span></span>
* [<span data-ttu-id="b7024-117">Criptografia do serviço de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-117">Azure Storage Service Encryption</span></span>](../storage/common/storage-service-encryption.md)
* [<span data-ttu-id="b7024-118">Armazenamento híbrido criptografado StorSimple</span><span class="sxs-lookup"><span data-stu-id="b7024-118">StorSimple Encrypted Hybrid Storage</span></span>](https://azure.microsoft.com/documentation/services/storsimple/)
* [<span data-ttu-id="b7024-119">Criptografia do lado do cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-119">Azure Client-Side Encryption</span></span>](../storage/common/storage-client-side-encryption.md)
* [<span data-ttu-id="b7024-120">Assinaturas de Acesso Compartilhado do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-120">Azure Storage Shared Access Signatures</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="b7024-121">Chaves de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-121">Azure Storage Account Keys</span></span>](../storage/common/storage-create-storage-account.md)
* [<span data-ttu-id="b7024-122">Compartilhamentos de arquivos do Azure com criptografia SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="b7024-122">Azure File shares with SMB 3.0 Encryption</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="b7024-123">Análise do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-123">Azure Storage Analytics</span></span>](https://msdn.microsoft.com/library/hh343270.aspx)

## <a name="azure-database-security"></a><span data-ttu-id="b7024-124">Segurança de banco de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-124">Azure Database Security</span></span>
* [<span data-ttu-id="b7024-125">Firewall do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-125">Azure SQL Firewall</span></span>](../sql-database/sql-database-firewall-configure.md)
* [<span data-ttu-id="b7024-126">Criptografia de nível de célula do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-126">Azure SQL Cell Level Encryption</span></span>](https://blogs.msdn.microsoft.com/sqlsecurity/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database/)
* [<span data-ttu-id="b7024-127">Criptografia de conexão do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-127">Azure SQL Connection Encryption</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="b7024-128">Autenticação do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-128">Azure SQL Authentication</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="b7024-129">Criptografia sempre ativa do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-129">Azure SQL Always Encryption</span></span>](https://msdn.microsoft.com/library/mt163865.aspx)
* [<span data-ttu-id="b7024-130">Criptografia de nível de coluna do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-130">Azure SQL Column Level Encryption</span></span>](https://msdn.microsoft.com/library/ms179331.aspx)
* [<span data-ttu-id="b7024-131">Transparent Data Encryption do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-131">Azure SQL Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/dn948096.aspx)
* [<span data-ttu-id="b7024-132">Auditoria do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-132">Azure SQL Database Auditing</span></span>](../sql-database/sql-database-auditing.md)

## <a name="azure-identity-and-access-management"></a><span data-ttu-id="b7024-133">Gerenciamento de acesso e identidade do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-133">Azure Identity and Access Management</span></span>
* [<span data-ttu-id="b7024-134">Controle de acesso baseado em função do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-134">Azure Role Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
* [<span data-ttu-id="b7024-135">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-135">Azure Active Directory</span></span>](../active-directory/active-directory-whatis.md)
* [<span data-ttu-id="b7024-136">Active Directory B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-136">Azure Active Directory B2C</span></span>](../active-directory-b2c/active-directory-b2c-get-started.md)
* [<span data-ttu-id="b7024-137">Serviços de Domínio do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-137">Azure Active Directory Domain Services</span></span>](../active-directory-domain-services/active-directory-ds-overview.md)
* [<span data-ttu-id="b7024-138">Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-138">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="backup-and-disaster-recovery"></a><span data-ttu-id="b7024-139">Backup e recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="b7024-139">Backup and Disaster Recovery</span></span>
* [<span data-ttu-id="b7024-140">Serviço de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-140">Azure Backup</span></span>](https://azure.microsoft.com/documentation/services/backup/)
* [<span data-ttu-id="b7024-141">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b7024-141">Azure Site Recovery</span></span>](https://azure.microsoft.com/documentation/services/site-recovery/)

## <a name="azure-networking"></a><span data-ttu-id="b7024-142">Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-142">Azure Networking</span></span>
* [<span data-ttu-id="b7024-143">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="b7024-143">Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b7024-144">Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-144">Azure VPN Gateway</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="b7024-145">Gateway de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-145">Azure Application Gateway</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="b7024-146">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-146">Azure Load Balancer</span></span>](../load-balancer/load-balancer-overview.md)
* [<span data-ttu-id="b7024-147">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b7024-147">Azure ExpressRoute</span></span>](../expressroute/expressroute-introduction.md)
* [<span data-ttu-id="b7024-148">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-148">Azure Traffic Manager</span></span>](../traffic-manager/traffic-manager-overview.md)
* [<span data-ttu-id="b7024-149">Proxy de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b7024-149">Azure Application Proxy</span></span>](../active-directory/active-directory-application-proxy-enable.md)
