---
title: "aaaAzure Linux Máquina Virtual DotNet Core Tutorial 1 | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b3652e86-0c44-4ac9-8cd1-27abdeaea4d4
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e6f047197336de1e93c50413b6eabb718230bc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-application-deployments-toolinux-virtual-machines"></a>Automatizando implantações de aplicativo tooLinux máquinas virtuais 

Esta série de quatro partes detalha como implantar e configurar recursos e aplicativos do Azure que usam modelos do Azure Resource Manager. Nesta série, um modelo é implantado e Olá examinado de modelo de implantação. Olá objetivo esta série é tooeducate na relação de saudação entre os recursos do Azure e tooprovide passa na experiência de implantação de modelos do Azure Resource Manager totalmente integrada. Este documento presume um nível básico de conhecimento com o Azure Resource Manager. Antes de iniciar este tutorial, familiarize-se com os conceitos básicos do Azure Resource Manager. 

## <a name="music-store-application"></a>Aplicativo de loja de música
Olá, exemplo usado nesta série é .net aplicativo Core simulando uma experiência de compra do repositório de música. Este aplicativo pode ser implantado tooeither um sistema virtual Linux ou Windows, exemplo implantações foram criadas para ambos. aplicativo Hello inclui um aplicativo web e um banco de dados SQL. Antes de ler artigos Olá nesta série, implante o aplicativo hello usando o botão de implantação Olá encontrado nesta página. Quando totalmente implantado, hello arquitetura de aplicativo / Azure parece Olá diagrama a seguir. 

modelo do Gerenciador de recursos do repositório de música Olá pode ser encontrado aqui, [modelo de Linux do repositório de música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)

![Aplicativo de loja de música](./media/dotnet-core-1-landing/music-store.png)

Cada um desses componentes, incluindo Olá associar o modelo JSON é examinado em Olá quatro artigos a seguir.

* [**Arquitetura do aplicativo** ](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – os componentes de aplicativos, como de sites da web e bancos de dados necessário toobe hospedado em recursos do computador do Azure como máquinas virtuais e bancos de dados do SQL Azure. Este documento explica como a necessidade de computação de mapeamento, tooAzure recursos e implantar esses recursos com um modelo do Gerenciador de recursos do Azure. 
* [**Acesso e segurança** ](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – ao hospedar aplicativos no Azure, é necessário tooconsider como aplicativo hello é acessado, e os componentes de aplicativo diferente acessarem umas às outras. Este documento detalha fornecendo e proteger o acesso entre componentes de aplicativos e aplicativos de tooan de acesso à internet.
* [**Disponibilidade e escalabilidade** ](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – disponibilidade e escalabilidade consulte toohello toostay de capacidade de aplicativos em execução durante o tempo de inatividade da infraestrutura e Olá capacidade tooscale demanda de aplicativos de toomeet de recursos de computação. Esses componentes de saudação documento detalhes necessários toodeploy uma carga balanceada e aplicativo altamente disponível.
* [**Implantação de aplicativo** ](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - ao implantar aplicativos em máquinas virtuais do Azure, método hello por quais Olá binários do aplicativo são instalados no hello Máquina Virtual deve ser considerado. Este documento detalha como automatizar a instalação de aplicativos usando extensões de script personalizado da máquina virtual do Azure.

meta de saudação durante o desenvolvimento de modelos do Gerenciador de recursos do Azure é tooautomate implantação de saudação da infraestrutura do Azure e a instalação de saudação e a configuração de qualquer aplicativo que está sendo hospedado dessa infraestrutura do Azure. Trabalhar com estes artigos fornece um exemplo dessa experiência.

## <a name="deploy-hello-music-store-application"></a>Implantar o aplicativo de repositório de música hello
saudação de aplicativo de repositório de música pode ser implantada usando este botão.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fdotnet-core-sample-templates%2Fmaster%2Fdotnet-core-music-linux%2Fazuredeploy.json" target="_blank"> <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

modelo do Gerenciador de recursos do Azure Olá requer Olá valores de parâmetro a seguir.

| Nome do Parâmetro | Descrição |
| --- | --- |
| SSHKEYDATA |Dados de chave SSH usada toosecure acesso toohello Máquina Virtual. Para saber mais sobre como criar uma chave aérea SSH, consulte [Criação de chaves SSH para VMs do Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). |
| ADMINUSERNAME |Nome de usuário de administrador usada na máquina virtual de saudação e hello Azure SQL Database. |
| SQLADMINPASSWORD |Senha usada no hello Azure SQL Database. |
| NUMBEROFINSTANCES |número de saudação de máquinas virtuais toobe criado. Cada aplicativo de web de repositório de música essas máquinas virtuais host hello e todo o tráfego tem a carga balanceada entre eles. |
| PUBLICIPADDRESSDNSNAME |Nome DNS globalmente exclusivo associado a saudação endereço IP público. |

Quando tiver concluído a implantação de modelo hello, procure toohello usando qualquer navegador da internet de endereço IP público. Olá .net site música principal será exibida.

## <a name="next-steps"></a>Próximas etapas
<hr>

[Etapa 1 – Arquitetura de aplicativos com modelos do Azure Resource Manager](dotnet-core-2-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Etapa 2 – Acesso e segurança em modelos do Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Etapa 3 – Disponibilidade e escala em modelos do Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Etapa 4 – Implantação de aplicativos com modelos do Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

