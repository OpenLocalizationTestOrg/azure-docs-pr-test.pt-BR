---
title: Recursos do Bash no Azure Cloud Shell | Microsoft Docs
description: "Visão geral dos recursos do Bash no Azure Cloud Shell"
services: Azure
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: juluk
ms.openlocfilehash: a6627ab6febc763ae3f1cd464f26ad641f7c717d
ms.sourcegitcommit: 5ac112c0950d406251551d5fd66806dc22a63b01
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="features--tools-for-bash-in-azure-cloud-shell"></a>Recursos e ferramentas para o Bash no Azure Cloud Shell

[!INCLUDE [features-introblock](../../includes/cloud-shell-features-introblock.md)]

> [!TIP]
> Ferramentas e recursos também estão disponíveis no [PowerShell](features-powershell.md).

O Bash no Cloud Shell é executado em `Ubuntu 16.04 LTS`.

## <a name="features"></a>Recursos

### <a name="secure-automatic-authentication"></a>Autenticação automática segura

O Bash no Cloud Shell protege e autentica automaticamente o acesso de conta da CLI do Azure 2.0.

### <a name="ssh-into-azure-linux-virtual-machines"></a>SSH em máquinas virtuais do Linux no Azure

Criar uma VM do Linux pela 2.0 do CLI do Azure pode criar uma chave SSH padrão e colocá-la no seu diretório `$Home`. Colocar chaves SSH em `$Home` permite direcionar conexões de SSH para máquinas virtuais Linux do Azure diretamente pelo Cloud Shell. As chaves são mantidas em acc_<user>.img no seu compartilhamento de arquivos, use as práticas recomendadas ao usar ou compartilhar acesso a seu compartilhamento de arquivos ou chaves.

### <a name="home-persistence-across-sessions"></a>Persistência de $Home entre as sessões

Para persistir arquivos entre as sessões, o Cloud Shell orienta você pela anexação de um compartilhamento de arquivos do Azure na primeira inicialização.
Após a conclusão, o Cloud Shell anexará automaticamente o armazenamento (montado como `$Home\clouddrive`) para todas as sessões futuras.
Além disso, no Bash no Cloud Shell, seu diretório `$Home` é mantido como .img em seu compartilhamento de arquivos do Azure.
Os arquivos fora de `$Home` e do estado da máquina não são mantidos entre sessões.

[Saiba mais sobre como manter arquivos no Bash no Cloud Shell](persisting-shell-storage.md)

## <a name="tools"></a>Ferramentas

|Categoria   |NOME   |
|---|---|
|Ferramentas do Linux            |bash<br> sh<br> tmux<br> dig<br>               |
|Ferramentas do Azure            |CLI do Azure [1.0](https://github.com/Azure/azure-cli) e [2.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Shipyard de lote](https://github.com/Azure/batch-shipyard) <br> [CLI do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cli) <br> [blobxfer](https://github.com/Azure/blobxfer#blobxfer) |
|Editores de texto           |vim<br> nano<br> emacs       |
|Controle do código-fonte         |git                    |
|Ferramentas de build            |make<br> maven<br> npm<br> pip         |
|Contêineres             |[CLI do Docker](https://github.com/docker/cli)/[Computador do Docker](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Helm](https://github.com/kubernetes/helm)<br> [CLI DO DC/OS](https://github.com/dcos/dcos-cli)         |
|Bancos de dados              |Cliente do MySQL<br> Cliente do PostgreSql<br> [Utilitário SQLCMD](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Outros                  |Cliente do iPython<br> [CLI do Cloud Foundry](https://github.com/cloudfoundry/cli)<br> [Terraform](https://www.terraform.io/docs/providers/azurerm/) |

## <a name="language-support"></a>Suporte ao idioma

|Linguagem   |Versão   |
|---|---|
|.NET       |2.0.0       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|PowerShell |[6.0 (beta)](https://github.com/PowerShell/powershell/releases)       |
|Python     |2.7 e 3.5 (padrão)|

## <a name="next-steps"></a>Próximas etapas
[Início rápido do Bash no Cloud Shell](quickstart.md) <br>
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)
