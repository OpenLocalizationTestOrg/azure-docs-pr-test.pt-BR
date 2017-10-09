---
title: "aaaIntegrate Cofre de chaves com o SQL Server em máquinas virtuais do Windows no Azure (Gerenciador de recursos) | Microsoft Docs"
description: "Saiba como tooautomate Olá configuração de criptografia do SQL Server para uso com o Cofre de chaves do Azure. Este tópico explica como toouse integração do cofre da chave do Azure com máquinas virtuais do SQL Server criados com o Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="7f430-104">Configurar a Integração do Azure Key Vault para SQL Server em Máquinas Virtuais do Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7f430-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f430-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="7f430-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="7f430-106">Clássico</span><span class="sxs-lookup"><span data-stu-id="7f430-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7f430-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7f430-107">Overview</span></span>
<span data-ttu-id="7f430-108">Há vários recursos de criptografia do SQL Server, como [TDE (Transparent Data Encryption)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE (criptografia de nível de coluna)](https://msdn.microsoft.com/library/ms173744.aspx) e [criptografia de backup](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f430-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="7f430-109">Esses formulários de criptografia exigem que você toomanage e armazenam chaves de criptografia Olá usado para criptografia.</span><span class="sxs-lookup"><span data-stu-id="7f430-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="7f430-110">Olá serviço Azure Key Vault (AKV) é projetado tooimprove Olá segurança e o gerenciamento dessas chaves em um local seguro e altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="7f430-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="7f430-111">Olá [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse essas chaves do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f430-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="7f430-112">Se você está executando o SQL Server com o local de máquinas, há são [etapas que você pode seguir tooaccess Azure Key Vault da máquina local do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f430-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="7f430-113">Mas para SQL Server em máquinas virtuais do Azure, você pode economizar tempo usando Olá *integração do cofre da chave do Azure* recurso.</span><span class="sxs-lookup"><span data-stu-id="7f430-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="7f430-114">Quando esse recurso está habilitado, ele automaticamente instala Olá conector do SQL Server, configura Olá EKM provedor tooaccess Cofre de chaves do Azure e cria Olá credencial tooallow você tooaccess seu cofre.</span><span class="sxs-lookup"><span data-stu-id="7f430-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="7f430-115">Se você examinou etapas Olá Olá mencionado anteriormente documentação local, você pode ver que esse recurso automatiza as etapas 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="7f430-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="7f430-116">Olá única você ainda precisaria toodo manualmente é chaves e cofre da chave toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="7f430-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="7f430-117">A partir daí, a configuração inteira Olá da sua VM do SQL é automatizada.</span><span class="sxs-lookup"><span data-stu-id="7f430-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="7f430-118">Depois que esse recurso foi concluída a instalação, você pode executar toobegin de instruções T-SQL criptografar seu ou backups de bancos de dados como faria normalmente.</span><span class="sxs-lookup"><span data-stu-id="7f430-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="7f430-119">Habilitando e configurando a integração de AKV</span><span class="sxs-lookup"><span data-stu-id="7f430-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="7f430-120">Você pode habilitar a integração de AKV durante o provisionamento ou configurá-la para VMs existentes.</span><span class="sxs-lookup"><span data-stu-id="7f430-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="7f430-121">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="7f430-121">New VMs</span></span>
<span data-ttu-id="7f430-122">Se estiver Provisionando uma nova máquina de virtual do SQL Server com o Gerenciador de recursos, Olá portal do Azure fornece um tooenable etapa integração do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f430-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="7f430-123">recurso de Cofre de chaves do Azure Hello está disponível somente para Olá Enterprise, Developer e Evaluation edições do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7f430-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integração do Cofre da Chave do SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="7f430-125">Para obter uma explicação detalhada de provisionamento, consulte [provisionar uma máquina de virtual do SQL Server no hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="7f430-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="7f430-126">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="7f430-126">Existing VMs</span></span>
<span data-ttu-id="7f430-127">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7f430-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="7f430-128">Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="7f430-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Integração de AKV do SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="7f430-130">Em Olá **configuração do SQL Server** folha, clique em Olá **editar** botão na seção de integração do Cofre de chaves automatizada de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f430-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Configurar uma Integração de AKV do SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="7f430-132">Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="7f430-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="7f430-133">Você também pode configurar a integração de AKV usando um modelo.</span><span class="sxs-lookup"><span data-stu-id="7f430-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="7f430-134">Para saber mais, confira [Azure quickstart template for Azure Key Vault integration (Modelo de início rápido do Azure para integração com o Cofre de Chaves do Azure)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="7f430-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

