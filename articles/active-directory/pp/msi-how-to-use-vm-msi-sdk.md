---
title: "Como usar uma Identidade de Serviço Gerenciado atribuída pelo usuário de SDKs do Azure em uma VM"
description: "Exemplos de código para usar SDKs do Azure com uma MSI atribuída pelo usuário em uma VM."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/22/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: f9a31a0500a6f5f1c49fc45d5811e28788e6f2b1
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="use-azure-sdks-with-a-user-assigned-managed-service-identity-msi"></a>Usar SDKs do Azure com uma MSI (Identidade de Serviço Gerenciado) atribuída pelo usuário

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)] Este artigo fornece uma lista de exemplos de SDK que demonstram o uso do suporte do respectivo SDK do Azure para a MSI atribuída pelo usuário.

## <a name="prerequisites"></a>pré-requisitos

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

> [!IMPORTANT]
> - Todo código/script de exemplo neste artigo supõe que o cliente esteja sendo executado em uma Máquina Virtual habilitada para MSI. Use o recurso "Conectar" da VM no Portal do Azure para conectar-se remotamente à sua VM. Para obter detalhes de como habilitar a MSI em uma VM, consulte [Configurar uma MSI (Identidade de Serviço Gerenciado) de VM usando a CLI do Azure](msi-qs-configure-cli-windows-vm.md) ou um dos artigos variantes (usando o PowerShell, o Portal do Azure, um modelo ou um SDK do Azure). 

## <a name="sdk-code-samples"></a>Exemplos de código do SDK

| .             | Exemplo de código |
| --------------- | ----------- |
| Python          | [Use o MSI para autenticar de modo simples de dentro de uma VM](https://azure.microsoft.com/resources/samples/resource-manager-python-manage-resources-with-msi/) |
| Ruby            | [Gerenciar recurso de uma VM habilitada para MSI](https://azure.microsoft.com/resources/samples/resources-ruby-manage-resources-with-msi/) |

## <a name="next-steps"></a>Próximas etapas

- Consulte [Azure SDKs](https://azure.microsoft.com/downloads/) (SDKs do Azure) para ver a lista completa de recursos de SDK do Azure, incluindo downloads da biblioteca, documentação e mais.

Use a seção de comentários a seguir para fornecer seus comentários e nos ajudar a aprimorar e adaptar nosso conteúdo.








