---
title: "aaaIntegrate Cofre de chaves com o SQL Server em máquinas virtuais do Windows no Azure (clássica) | Microsoft Docs"
description: "Saiba como tooautomate Olá configuração de criptografia do SQL Server para uso com o Cofre de chaves do Azure. Este tópico explica como toouse integração do cofre da chave do Azure com máquinas virtuais do SQL Server cria no modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configurar a Integração do Azure Key Vault para SQL Server em Máquinas Virtuais do Azure (Clássicas)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Clássico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Visão geral
Há vários recursos de criptografia do SQL Server, como [TDE (Transparent Data Encryption)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE (criptografia de nível de coluna)](https://msdn.microsoft.com/library/ms173744.aspx) e [criptografia de backup](https://msdn.microsoft.com/library/dn449489.aspx). Esses formulários de criptografia exigem que você toomanage e armazenam chaves de criptografia Olá usado para criptografia. Olá serviço Azure Key Vault (AKV) é projetado tooimprove Olá segurança e o gerenciamento dessas chaves em um local seguro e altamente disponível. Olá [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse essas chaves do Cofre de chaves do Azure.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Se você estiver executando o SQL Server com computadores locais, há [etapas que você pode seguir tooaccess Azure Key Vault da máquina local do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Mas para SQL Server em máquinas virtuais do Azure, você pode economizar tempo usando Olá *integração do cofre da chave do Azure* recurso. Com alguns tooenable de cmdlets do PowerShell do Azure esse recurso, você pode automatizar Olá seu Cofre de chaves de configuração necessárias para uma VM do SQL tooaccess.

Quando esse recurso está habilitado, ele automaticamente instala Olá conector do SQL Server, configura Olá EKM provedor tooaccess Cofre de chaves do Azure e cria Olá credencial tooallow você tooaccess seu cofre. Se você examinou etapas Olá Olá mencionado anteriormente documentação local, você pode ver que esse recurso automatiza as etapas 2 e 3. Olá única você ainda precisaria toodo manualmente é chaves e cofre da chave toocreate hello. A partir daí, a configuração inteira Olá da sua VM do SQL é automatizada. Depois que esse recurso foi concluída a instalação, você pode executar toobegin de instruções T-SQL criptografar seu ou backups de bancos de dados como faria normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configurar a integração de AKV
Use o PowerShell tooconfigure integração do cofre da chave do Azure. Olá seções a seguir fornece uma visão geral dos parâmetros de saudação necessárias e, em seguida, um exemplo de script do PowerShell.

### <a name="install-hello-sql-server-iaas-extension"></a>Instalar Olá extensão de IaaS do SQL Server
Primeiro, [instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Entender os parâmetros de entrada hello
Olá seguinte tabela lista Olá parâmetros necessários script do PowerShell Olá toorun na próxima seção, Olá.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| **$akvURL** |**URL de Cofre de chaves Olá** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Nome da Entidade de Serviço** |"fde2b411-33d5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Segredo da Entidade de Serviço** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=" |
| **$credName** |**Nome da credencial**: integração AKV cria uma credencial do SQL Server, permitindo que o cofre da chave de toohello Olá VM toohave acesso. Escolha um nome para essa credencial. |"mycred1" |
| **$vmName** |**Nome da máquina virtual**: nome de saudação de uma VM de SQL criado anteriormente. |"myvmname" |
| **$serviceName** |**Nome do serviço**: nome de serviço de nuvem Olá associado Olá VM do SQL. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>Habilitar a integração de AKV com o PowerShell
Olá **AzureVMSqlServerKeyVaultCredentialConfig novo** cmdlet cria um objeto de configuração para o recurso de integração do Azure Key Vault hello. Olá **conjunto AzureVMSqlServerExtension** configura essa integração com hello **KeyVaultCredentialSettings** parâmetro. Olá mostram as etapas a seguir como toouse esses comandos.

1. No Azure PowerShell primeiro configure parâmetros de entrada hello com seus valores específicos conforme descrito nas seções anteriores Olá neste tópico. saudação de script a seguir está um exemplo.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Em seguida, a seguir Olá use script tooconfigure e habilite a integração de AKV.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Olá extensão do agente SQL IaaS atualizará Olá VM do SQL com essa nova configuração.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

