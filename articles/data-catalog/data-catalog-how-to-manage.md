---
title: "ativos de dados aaaManage no catálogo de dados do Azure | Microsoft Docs"
description: "artigo Olá destaca como toocontrol visibilidade e a propriedade de ativos de dados registrados no catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Gerenciar ativos de dados no Catálogo de Dados do Azure
## <a name="introduction"></a>Introdução
Catálogo de dados do Azure é projetado para descoberta de fonte de dados, para que você pode facilmente descobrir e entender as fontes de dados Olá necessário tooperform analysis e tomar decisões. Esses recursos de descoberta tornam impacto maior hello quando você e outros usuários possam localizar e compreender o intervalo mais amplo de saudação de fontes de dados disponíveis. Com esses elementos em mente, o comportamento padrão de saudação do catálogo de dados é para todos os dados registrados fontes toobe visível tooand detectável por todos os usuários do catálogo.

Catálogo de dados não dá acesso a dados toohello em si. Acesso a dados é controlado pelo proprietário Olá Olá da fonte de dados. Com o catálogo de dados, você pode descobrir fontes de dados e exibir metadados Olá fontes toohello relacionados que estão registradas no catálogo de saudação.

Pode haver situações, porém, em que fontes de dados devem ser apenas usuários toospecific visível ou toomembers de grupos específicos. Nesses cenários, os usuários podem assumir a propriedade de ativos de dados registrados no catálogo hello e, em seguida, controlar a visibilidade de saudação de ativos de saudação que eles possuem.

> [!NOTE]
> funcionalidade de saudação descrita neste artigo está disponível apenas no hello Standard Edition do Data Catalog do Azure. Olá edição gratuita não fornece recursos para a propriedade e restringir a visibilidade de ativos de dados.
>
>

## <a name="manage-ownership-of-data-assets"></a>Gerenciar a propriedade de ativos de dados
Por padrão, ativos de dados registrados no Catálogo de Dados não têm proprietário. Qualquer usuário com permissão tooaccess Olá de catálogo pode descobrir e anotar esses ativos. Os usuários podem assumir a propriedade de ativos de dados sem proprietário e, em seguida, limitar a visibilidade de saudação de ativos de saudação que eles possuem.

Quando um ativo de dados no catálogo de dados é de propriedade, somente os usuários autorizados pelos proprietários de saudação podem descobrir ativos hello e exibir os metadados, e somente os proprietários de saudação podem excluir o ativo de saudação do catálogo de saudação.

> [!NOTE]
> Propriedade no catálogo de dados afeta apenas os metadados de saudação que são armazenados no catálogo de saudação. Propriedade não concede todas as permissões na fonte de dados subjacente hello.
>
>

### <a name="take-ownership"></a>Apropriar-se
Os usuários podem assumir a propriedade de ativos de dados selecionando Olá **Take Ownership** opção no portal do catálogo de dados de saudação. Nenhuma permissão especial é necessário tootake propriedade de um ativo de dados sem proprietário. Qualquer usuário pode apropriar-se de um ativo de dados sem proprietário.

### <a name="add-owners-and-co-owners"></a>Adicionar proprietários e coproprietários
Se um ativo de dados já tiver um proprietário, outros usuários não poderão simplesmente assumir a propriedade. Eles deverão ser adicionados como coproprietários por um proprietário existente. Qualquer proprietário pode adicionar outros usuários ou grupos de segurança como coproprietários.

> [!NOTE]
> Ele é um toohave de prática recomendada pelo menos duas pessoas como proprietários para qualquer propriedade ativo de dados.
>
>

### <a name="remove-owners"></a>Remover proprietários
Assim como qualquer proprietário ativo pode adicionar coproprietários, qualquer proprietário ativo pode remover qualquer coproprietário.

Um proprietário do ativo que remove a mesmo como um proprietário não poderá mais gerenciar ativos de saudação. Se o proprietário do ativo Olá remove a mesmo como um proprietário e não há nenhum outros co-proprietários, ativo Olá reverte tooan sem proprietário estado.

## <a name="control-visibility"></a>Controlar a visibilidade
Os proprietários dos ativos de dados podem controlar a visibilidade de Olá Olá de ativos de dados que eles possuem. visibilidade toorestrict como padrão Olá, onde todos os usuários podem descobrir de catálogo de dados e exibição Olá ativo de dados, proprietário do ativo Olá pode alternar a configuração de visibilidade de saudação do **todos** muito**proprietários e esses usuários** nas propriedades de saudação para ativo hello. Em seguida, os proprietários podem adicionar usuários e grupos de segurança específicos.

> [!NOTE]
> Sempre que possível, devem ser atribuídas permissões de propriedade e visibilidade de ativos toosecurity grupos e usuários de tooindividual não.
>
>

## <a name="catalog-administrators"></a>Administradores do Catálogo
Os administradores do catálogo de dados são implicitamente co-proprietários de todos os ativos no catálogo de saudação. Os proprietários dos ativos não é possível remover a visibilidade dos administradores, e os administradores podem gerenciar propriedade e visibilidade de todos os ativos de dados no catálogo de saudação.

## <a name="summary"></a>Resumo
Olá catálogo de dados crowdsourcing modelo toometadata e os dados ativos descoberta permite que todos os toocontribute de usuários do catálogo e descobrir. Olá edição Standard do catálogo de dados destina-se a visibilidade de saudação toolimit propriedade e o gerenciamento e o uso de ativos de dados específico.
