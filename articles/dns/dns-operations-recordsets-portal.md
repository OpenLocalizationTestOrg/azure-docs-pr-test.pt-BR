---
title: aaaManage DNS registram conjuntos e registros de DNS do Azure | Microsoft Docs
description: "DNS do Azure fornece o registro DNS do hello recurso toomanage define e registra ao hospedar seu domínio."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Gerenciar registros de DNS e conjuntos de registros usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-operations-recordsets-portal.md)
> * [CLI 1.0 do Azure](dns-operations-recordsets-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artigo mostra como toomanage conjuntos de registros e os registros para a zona DNS usando Olá portal do Azure.

É importante toounderstand diferença de saudação entre conjuntos de registros de DNS e registros DNS individuais. Um conjunto de registros é uma coleção de registros em uma zona ter Olá mesmo nome e são Olá mesmo tipo. Para obter mais informações, consulte [registros usando e conjuntos de registros de DNS criar hello portal do Azure](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Criar registro e um novo conjunto de registros

toocreate um conjunto de registros em Olá portal do Azure, consulte [Olá de registros de DNS criar usando o portal do Azure](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Exibir um conjunto de registros

1. No portal do Azure de Olá, vá toohello **zona DNS** folha.
2. Pesquisar o conjunto de registros hello e selecioná-lo. Isso abre as propriedades de conjunto de registros de saudação.

    ![Pesquisar um conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Adicionar um novo conjunto de registros de registro tooa

Você pode adicionar o conjunto de registros too20 registros tooany. Um conjunto de registros não pode conter dois registros idênticos. Conjuntos de registros vazios (com zero registros) podem ser criados, mas não aparecem nos servidores de nome DNS do Azure hello. Os conjuntos de registros do tipo CNAME podem conter, no máximo, um registro.

1. Em Olá **propriedades de conjunto de registros** folha para a zona DNS, clique em registro Olá definido que deseja tooadd um registro.

    ![Selecionar um conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. Especifica propriedades de conjunto de registros de saudação preenchendo os campos de saudação.

    ![Adicionar um registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Clique em **salvar** em Olá superior da saudação folha toosave suas configurações. Em seguida, feche a folha de saudação.
4. Canto hello, você verá que está salvando o registro de saudação.

    ![Salvando o conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

Depois que o registro Olá foi salvo, Olá valores hello **zona DNS** folha refletirá o novo registro de saudação.

## <a name="update-a-record"></a>Atualizar um registro

Quando você atualiza um registro em um conjunto de registros existente, campos de saudação, que você pode atualizar dependem do tipo de saudação do registro que o estiver trabalhando com.

1. Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, pesquise o registro de saudação.
2. Modificar o registro de saudação. Quando você modifica um registro, você pode alterar configurações disponíveis de saudação para registro de saudação. Em Olá exemplo a seguir, Olá **endereço IP** campo é selecionado, e o endereço IP de saudação está no processo de saudação do que está sendo modificado.

    ![Modificar um registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Clique em **salvar** em Olá superior da saudação folha toosave suas configurações. Olá no canto superior direito, você verá a notificação de Olá Olá registro foi salvo.

    ![Conjunto de registros salvo](./media/dns-operations-recordsets-portal/saved150.png)

Olá registro foi salvo, os valores de saudação para registro de saudação definidos em Olá **zona DNS** folha refletirá registro Olá atualizado.

## <a name="remove-a-record-from-a-record-set"></a>Remover um registro de um conjunto de registros

Você pode usar os registros Olá tooremove portal do Azure de um conjunto de registros. Observe que a remover o último registro de saudação de um conjunto de registros não exclui o conjunto de registros de saudação.

1. Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, pesquise o registro de saudação.
2. Clique em registro Olá que você deseja tooremove. Em seguida, selecione **Remover**.

    ![Remover um registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Clique em **salvar** em Olá superior da saudação folha toosave suas configurações.
4. Após a remoção do registro hello, Olá valores de registro de saudação em Olá **zona DNS** folha refletirá a remoção de saudação.

## <a name="delete"></a>Excluir um conjunto de registros

1. Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, clique em **excluir**.

    ![Excluir um conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Uma mensagem aparece perguntando se você quiser que o conjunto de registros toodelete hello.
3. Verifique se o conjunto de registros de Olá Olá nome corresponde ao que você deseja toodelete e, em seguida, clique em **Sim**.
4. Em Olá **zona DNS** folha, verifique se que o conjunto de registros Olá não está mais visível.

## <a name="work-with-ns-and-soa-records"></a>Trabalhar com registros NS e SOA

Os registros NS e SOA que são criados automaticamente são gerenciados de modo diferente de outros tipos de registro.

### <a name="modify-soa-records"></a>Modificar registros SOA

Você não pode adicionar ou remover registros da saudação criado automaticamente o registro SOA definido no ápice da zona de saudação (nome = "@"). No entanto, você pode modificar qualquer um dos parâmetros de saudação em Olá registro SOA (exceto "Host") e registro Olá definir o TTL.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Modificar os registros no ápice da zona de saudação NS

registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS. Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.

Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS. Você também pode modificar hello TTL e metadados para esse conjunto de registros. No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.

Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação. Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.

### <a name="delete-soa-or-ns-record-sets"></a>Excluir conjuntos de registros SOA ou NS

Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (nome = "@") que são criadas automaticamente quando a zona de saudação é criada. Eles são excluídos automaticamente quando você excluir a zona de saudação.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre DNS do Azure, consulte Olá [visão geral do DNS do Azure](dns-overview.md).
* Para obter mais informações sobre como automatizar o DNS, consulte [zonas DNS criando e usando conjuntos de registros Olá .NET SDK](dns-sdk.md).
* Para saber mais sobre os registros DNS reversos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).
