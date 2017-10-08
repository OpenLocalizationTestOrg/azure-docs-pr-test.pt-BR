---
title: "aaaGet iniciado com o DNS do Azure usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toocreate um DNS zona e registro de DNS do Azure. Isso é um guia passo a passo toocreate e gerenciar sua primeira zona DNS e o registro usando Olá portal do Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Introdução ao DNS do Azure usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI 1.0 do Azure](dns-getstarted-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-getstarted-cli.md)

Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando Olá portal do Azure. Você também pode executar essas etapas usando o Azure PowerShell ou Olá CLI do Azure de plataforma cruzada.

Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio. Cada registro DNS para seu domínio é criado dentro dessa zona DNS. Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação. Cada uma dessas etapas é descrita em Olá etapas a seguir.

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

1. Entrar toohello portal do Azure
2. No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.

    ![Zona DNS](./media/dns-getstarted-portal/openzone650.png)

4. Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:


   | **Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|contoso.com|nome de saudação da zona do DNS de saudação|
   |**Assinatura**|[Sua assinatura]|Selecione uma zona DNS assinatura toocreate Olá no.|
   |**Grupo de recursos**|**Criar um novo:** contosoDNSRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

> [!NOTE]
> grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá sempre é "global" e não é mostrado.

## <a name="create-a-dns-record"></a>Criar um registro DNS

Olá exemplo a seguir orienta Olá processo de criação de novo registro de 'A'. Para outros tipos de registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md). 

1. Com hello zona DNS criado, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **contoso.com** da zona DNS em Olá folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **contoso.com** em Olá **filtrar por nome...** caixa tooeasily acessar Olá zona de DNS.

1. Na parte superior de saudação do hello **zona DNS** folha, selecione **+ registrar conjunto** tooopen Olá **Adicionar conjunto de registros** folha.

1. Em Olá **Adicionar conjunto de registros** folha, digite Olá valores a seguir e clique em **Okey**. Neste exemplo, você está criando um registro A.

   |**Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|www|Nome do registro Olá|
   |**Tipo**|Uma| Tipo de toocreate de registro de DNS, os valores aceitáveis são A, AAAA, CNAME, MX, NS, SRV, TXT e PTR.  Para obter mais informações sobre tipos de registro, visite [Visão geral sobre registros e zonas DNS](dns-zones-records.md)|
   |**TTL**|1|Tempo de vida da solicitação DNS hello.|
   |**Unidade de TTL**|Horas|Medição de tempo para o valor de TTL.|
   |**Endereço IP**|ipAddressValue| Esse valor é o endereço IP de saudação que resolve o registro de DNS hello.|

## <a name="view-records"></a>Exibir registros

Na parte inferior de saudação da folha de zona do DNS hello, você pode ver registros Olá para a zona DNS de saudação. Você deve ver o saudação padrão DNS e SOA registros que são criados em cada região, além de quaisquer novos registros que você criou.

![zona](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Atualizar servidores de nome

Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello. Isso permite que outros usuários no hello Internet toofind seus registros DNS.

servidores de nome de saudação para sua zona são fornecidos em Olá portal do Azure:

![zona](./media/dns-getstarted-portal/viewzonens500.png)

Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá). Seu registrador oferece Olá opção tooset os servidores de nome Olá para o domínio de saudação. Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:

1. No portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **MyResourceGroup** grupo de recursos no hello folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **MyResourceGroup** em Olá **filtrar por nome...** grupo de recursos do hello caixa tooeasily acesso.
1. Em Olá **MyResourceGroup** folha, clique em Olá **excluir** botão.
1. Hello portal exige que você tootype nome de saudação do hello tooconfirm de grupo de recursos que você deseja toodelete-lo. Clique em **excluir**, tipo *MyResourceGroup* para o nome do grupo de recursos hello, em seguida, clique em **excluir**. Excluir um grupo de recursos exclui todos os recursos no grupo de recursos de saudação, portanto, sempre tooconfirm-se de conteúdo de saudação de um grupo de recursos antes de excluí-lo. portal de saudação exclui todos os recursos contidos no grupo de recursos hello, em seguida, exclui o grupo de recursos de saudação em si. Esse processo leva vários minutos.


## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).

toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md).

