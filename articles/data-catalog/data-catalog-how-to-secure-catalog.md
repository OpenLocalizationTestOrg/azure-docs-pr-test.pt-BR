---
title: "aaaHow toosecure acesso tooAzure catálogo de dados | Microsoft Docs"
description: "Este artigo explica como toosecure catálogo de dados e seus ativos de dados."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Como toosecure acessar ativos de dados e o catálogo de toodata
> [!IMPORTANT]
> Este recurso está disponível somente na edição standard de saudação do catálogo de dados do Azure.

Catálogo de dados do Azure permite que você toospecify quem pode acessar o catálogo de dados hello e quais operações (registrar, anotar, apropriar-se) eles podem executar em metadados no catálogo de saudação. 

## <a name="catalog-users-and-permissions"></a>Usuários e permissões do catálogo
toogive um usuário ou uma saudação grupo acessar o catálogo de dados tooa e definir permissões:

1. Em Olá [home page do seu catálogo de dados](http://www.azuredatacatalog.com), clique em **configurações** na barra de ferramentas de saudação.

    ![catálogo de dados – configurações](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Na página de configurações de Olá, expanda Olá **usuários catálogo** seção.
    ![Catálogo de Usuários – Adicionar](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Clique em **Adicionar**.
4. Digite hello totalmente qualificado **nome de usuário** ou nome de saudação **grupo de segurança** no hello Azure AAD (Active Directory) associado com o catálogo de saudação. Use vírgula (', ') como um separador se você estiver adicionando mais de um usuário ou grupo.
    ![Usuários do Catálogo – usuários ou grupos](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Pressione **ENTER** ou **guia** fora da caixa de texto de saudação. 
6.  Confirme se todas as permissões (**anotar**, **registrar**, e **Take Ownership**) são atribuídos toothese usuários ou grupos por padrão. Ou seja, Olá usuário ou grupo pode [registrar ativos de dados]( data-catalog-how-to-register.md), [anotar os ativos de dados]( data-catalog-how-to-annotate.md), e [assumir a propriedade de ativos de dados]( data-catalog-how-to-manage.md). 
    ![Usuários do Catálogo – permissões padrão](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive um usuário ou grupo apenas Olá leitura acessar toohello catálogo, desmarque Olá **anotar** opção para esse usuário ou grupo. Quando você fizer isso, Olá usuário ou grupo não é possível anotar os ativos de dados no catálogo de hello, mas eles podem exibi-los. 
8.  toodeny um usuário ou grupo do registro de recursos de dados, desmarque Olá **registrar** opção para esse usuário ou grupo.
9.  toodeny um usuário de assumir a propriedade de um ativo de dados, desmarque Olá **apropriar** opção para esse usuário ou grupo. 
10. toodelete um usuário/grupo de usuários do catálogo, clique em **x** para Olá/grupo de usuário final Olá Olá lista. 
    ![Usuários do Catálogo – excluir usuário](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > É recomendável que você adiciona usuários de toocatalog de grupos de segurança em vez de adicionar usuários diretamente e atribuir permissões. Em seguida, adicione os grupos de segurança de toohello de usuários que correspondem ao seu catálogo de toohello de acesso necessários e suas funções.

## <a name="special-considerations"></a>Considerações especiais

- permissões de saudação atribuídas a grupos de toosecurity são aditivas. Digamos que um usuário esteja em dois grupos. Um grupo tem permissões para anotar e outro grupo não tem permissões para anotar. Nesse caso, o usuário tem permissões para anotar. 
- permissões de saudação atribuídas explicitamente tooa Olá de substituição de usuário as permissões atribuídas toogroups toowhich Olá usuário pertence. No exemplo anterior de saudação, digamos que você adicionou o hello usuário toocatalog usuários explicitamente e não atribua permissões de anotar. usuário Olá não pode anotar os ativos de dados mesmo que o usuário Olá é um membro de um grupo que tenha permissões de anotar.

## <a name="next-steps"></a>Próximas etapas
- [Introdução ao Catálogo de Dados do Azure](data-catalog-get-started.md)

