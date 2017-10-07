---
title: aaaCreate FQDN para uma VM do Linux no hello portal do Azure | Microsoft Docs
description: "Saiba como toocreate um nome de domínio totalmente qualificado, ou FQDN, para um Gerenciador de recursos com base em máquina virtual no portal do Azure de saudação."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Criar um nome de domínio totalmente qualificado no hello portal do Azure para uma VM do Linux

Quando você cria uma máquina virtual (VM) no hello [portal do Azure](https://portal.azure.com), um recurso IP público para a máquina virtual de saudação é criado automaticamente. Você usa essa saudação de acesso de tooremotely do endereço IP VM. Embora o portal de saudação não cria um [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou o FQDN, você pode adicionar um depois hello VM é criada. Este artigo demonstra Olá etapas toocreate um nome DNS ou o FQDN.

## <a name="create-a-fqdn"></a>Criar um FQDN
Este artigo pressupõe que você já tenha criado uma VM. Se necessário, você pode [criar uma máquina virtual no portal de saudação](quick-create-portal.md) ou [com hello CLI do Azure](quick-create-cli.md). Siga estas etapas depois que a VM estiver em execução:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Você pode se conectar remotamente toohello VM usando este DNS nome, como com `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Próximas etapas
Agora que sua VM tem um IP público e um nome DNS, é possível implantar estruturas comuns do aplicativo ou serviços, como o nginx, MongoDB, Docker, etc.

Leia mais sobre como [usar o Resource Manager](../../azure-resource-manager/resource-group-overview.md) para obter dicas sobre a criação de implantações do Azure.

