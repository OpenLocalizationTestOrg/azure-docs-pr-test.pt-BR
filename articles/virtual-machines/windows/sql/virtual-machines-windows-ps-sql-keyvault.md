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
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configurar a Integração do Azure Key Vault para SQL Server em Máquinas Virtuais do Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](virtual-machines-windows-ps-sql-keyvault.md)
> * [Clássico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Visão geral
Há vários recursos de criptografia do SQL Server, como [TDE (Transparent Data Encryption)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE (criptografia de nível de coluna)](https://msdn.microsoft.com/library/ms173744.aspx) e [criptografia de backup](https://msdn.microsoft.com/library/dn449489.aspx). Esses formulários de criptografia exigem que você toomanage e armazenam chaves de criptografia Olá usado para criptografia. Olá serviço Azure Key Vault (AKV) é projetado tooimprove Olá segurança e o gerenciamento dessas chaves em um local seguro e altamente disponível. Olá [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse essas chaves do Cofre de chaves do Azure.

Se você está executando o SQL Server com o local de máquinas, há são [etapas que você pode seguir tooaccess Azure Key Vault da máquina local do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Mas para SQL Server em máquinas virtuais do Azure, você pode economizar tempo usando Olá *integração do cofre da chave do Azure* recurso.

Quando esse recurso está habilitado, ele automaticamente instala Olá conector do SQL Server, configura Olá EKM provedor tooaccess Cofre de chaves do Azure e cria Olá credencial tooallow você tooaccess seu cofre. Se você examinou etapas Olá Olá mencionado anteriormente documentação local, você pode ver que esse recurso automatiza as etapas 2 e 3. Olá única você ainda precisaria toodo manualmente é chaves e cofre da chave toocreate hello. A partir daí, a configuração inteira Olá da sua VM do SQL é automatizada. Depois que esse recurso foi concluída a instalação, você pode executar toobegin de instruções T-SQL criptografar seu ou backups de bancos de dados como faria normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Habilitando e configurando a integração de AKV
Você pode habilitar a integração de AKV durante o provisionamento ou configurá-la para VMs existentes.

### <a name="new-vms"></a>Novas VMs
Se estiver Provisionando uma nova máquina de virtual do SQL Server com o Gerenciador de recursos, Olá portal do Azure fornece um tooenable etapa integração do Cofre de chaves do Azure. recurso de Cofre de chaves do Azure Hello está disponível somente para Olá Enterprise, Developer e Evaluation edições do SQL Server.

![Integração do Cofre da Chave do SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Para obter uma explicação detalhada de provisionamento, consulte [provisionar uma máquina de virtual do SQL Server no hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VMs existentes
Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server. Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.

![Integração de AKV do SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

Em Olá **configuração do SQL Server** folha, clique em Olá **editar** botão na seção de integração do Cofre de chaves automatizada de saudação.

![Configurar uma Integração de AKV do SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.

> [!NOTE]
> Você também pode configurar a integração de AKV usando um modelo. Para saber mais, confira [Azure quickstart template for Azure Key Vault integration (Modelo de início rápido do Azure para integração com o Cofre de Chaves do Azure)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

