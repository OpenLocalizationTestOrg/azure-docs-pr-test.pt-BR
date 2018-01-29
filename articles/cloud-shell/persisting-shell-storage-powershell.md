---
title: "Persistir arquivos no PowerShell no Azure Cloud Shell (Versão prévia) | Microsoft Docs"
description: Passo a passo de como o Azure Cloud Shell persiste arquivos.
services: azure
documentationcenter: 
author: maertendmsft
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: damaerte
ms.openlocfilehash: d0bc16bc951fce17235d8070012de44ebab89888
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
[!include [features-introblock](../../includes/cloud-shell-persisting-shell-storage-introblock.md)]

## <a name="how-powershell-in-azure-cloud-shell-preview-works"></a>Como funciona o PowerShell no Azure Cloud Shell (versão prévia)
O PowerShell no Cloud Shell (Versão prévia) mantém arquivos usando o seguinte método: 
* Montagem do compartilhamento de arquivos do Azure especificado como `clouddrive` no diretório `$Home` para que haja interação direta com o compartilhamento de arquivos.

## <a name="list-cloud-drive-azure-file-shares"></a>Listar compartilhamentos de arquivos do Azure da unidade de nuvem
O comando `Get-CloudDrive` recupera as informações de compartilhamento de arquivos do Azure montadas no momento pela unidade de nuvem no Cloud Shell. <br>
![Executando Get-CloudDrive](media/persisting-shell-storage-powershell/Get-Clouddrive.png)

## <a name="unmount-cloud-drive"></a>Desmontar unidade de nuvem
Você pode desmontar um compartilhamento de arquivos do Azure que esteja montado no Cloud Shell a qualquer momento. Se o compartilhamento de arquivos do Azure tiver sido removido, será solicitado que você crie e monte um novo compartilhamento de arquivos do Azure na sessão seguinte.

O comando `Dismount-CloudDrive` desmonta um compartilhamento de arquivos do Azure da conta de armazenamento atual. Desmontar a unidade de nuvem encerra a sessão atual. O usuário precisará criar e montar um novo compartilhamento de arquivos do Azure durante a próxima sessão.
![Executando Dismount-CloudDrive](media/persisting-shell-storage-powershell/Dismount-Clouddrive.png)

[!include [features-endblock](../../includes/cloud-shell-persisting-shell-storage-endblock.md)]

## <a name="next-steps"></a>Próximas etapas
[Guia de início rápido para o PowerShell](quickstart-powershell.md) <br>
[Saiba mais sobre arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Saiba mais sobre marcas de armazenamento](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>