---
title: aaaManage DNS zonas no DNS do Azure - portal do Azure | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando Olá portal do Azure. Este artigo descreve como tooupdate, excluir e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Como zonas DNS toomanage Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI 1.0 do Azure](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)

Este artigo mostra como toomanage suas zonas DNS usando Olá portal do Azure. Você também pode gerenciar as zonas DNS usando multiplataforma Olá [CLI do Azure](dns-operations-dnszones-cli.md) ou hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

1. Entrar toohello portal do Azure
2. No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:


   | **Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|contoso.com|nome de saudação da zona do DNS de saudação|
   |**Assinatura**|[Sua assinatura]|Selecione uma zona DNS assinatura toocreate Olá no.|
   |**Grupo de recursos**|**Criar um novo:** contosoDNSRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

> [!NOTE]
> grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá sempre é "global" e não é mostrado.

## <a name="list-dns-zones"></a>Listar as zonas DNS

Olá portal do Azure no, navegue muito**mais serviços** > **rede** > **zonas DNS**. Cada zona DNS é seu próprio recurso, informações como o número de conjuntos de registro e servidores de nomes são visíveis nesse modo de exibição. coluna Olá **servidores de nome** não está no modo de exibição de padrão de saudação, tooadd ele clique **colunas**, selecione **servidores de nome** e clique em **feito**.

![listagem de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Excluir uma zona DNS

Navegue tooa zona DNS no portal de saudação. Em Olá **zona DNS** folha, clique em **Excluir zona**. Você está tooconfirm solicitado são desejarem zona DNS toodelete hello. Também excluir uma zona DNS exclui todos os registros de saudação que estão contidos na zona de saudação.

## <a name="next-steps"></a>Próximas etapas

Saiba como toowork com a zona DNS e registros visitando [Introdução ao DNS do Azure usando o portal do Azure de saudação](dns-getstarted-portal.md).
