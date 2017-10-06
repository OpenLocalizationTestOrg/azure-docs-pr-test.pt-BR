---
title: "recursos de nuvem Shell (visualização) aaaAzure | Microsoft Docs"
description: "Visão geral dos recursos do Azure Cloud Shell"
services: 
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Recursos e ferramentas para o Azure Cloud Shell
Shell de nuvem do Azure é um toomanage de experiência do shell baseado no navegador e desenvolver recursos do Azure.

Shell de nuvem oferece um navegador acessível, pré-configurado experiência do shell de gerenciamento de recursos do Azure sem sobrecarga de saudação de instalação, controle de versão e a manutenção de uma máquina por conta própria.

O Cloud Shell provisiona máquinas com base em solicitação e, consequentemente, o estado da máquina não persistirá nas sessões. Como o Cloud Shell é compilado para sessões interativas, os shells são encerrados automaticamente após 20 minutos de inatividade do shell.

## <a name="bash-in-cloud-shell"></a>Bash no Cloud Shell
### <a name="tools"></a>Ferramentas
|Categoria   |Nome   |
|---|---|
|Intérprete de shell do Linux|Bash<br> sh               |
|Ferramentas do Azure            |CLI do Azure [1.0](https://github.com/Azure/azure-cli) e [2.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Shipyard de lote](https://github.com/Azure/batch-shipyard)     |
|Editores de texto           |vim<br> nano<br> emacs       |
|Controle do código-fonte         |git                    |
|Ferramentas de build            |make<br> maven<br> npm<br> pip         |
|Contêineres             |[CLI do Docker](https://github.com/docker/cli)/[Computador do Docker](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Escalação](https://github.com/Azure/draft)<br> [CLI DO DC/OS](https://github.com/dcos/dcos-cli)         |
|Bancos de dados              |Cliente do MySQL<br> Cliente do PostgreSql<br> [Utilitário SQLCMD](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|outro                  |Cliente do iPython<br> [CLI do Cloud Foundry](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Suporte ao idioma
|idioma   |Versão   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 e 3.5 (padrão)|

## <a name="secure-automatic-authentication"></a>Autenticação automática segura
Shell de nuvem com segurança e automaticamente autentica o acesso de conta para Olá 2.0 do CLI do Azure.

## <a name="azure-files-persistence"></a>Persistência de arquivos do Azure
Como o Cloud Shell é alocado com base em solicitação usando um computador temporário, os arquivos fora de $Home e o estado do computador não persistem entre as sessões.
arquivos de toopersist entre as sessões, movimentações de Shell de nuvem por meio de anexação de um arquivo do Azure compartilhar na primeira inicialização.
Após a conclusão, o Cloud Shell anexará automaticamente o armazenamento para todas as sessões futuras.

[Saiba mais sobre como anexar tooCloud de compartilhamentos de arquivos do Azure Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Próximas etapas
[Início rápido do Cloud Shell](quickstart.md) <br>
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>