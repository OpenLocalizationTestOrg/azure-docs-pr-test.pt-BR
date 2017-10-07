---
title: aplicativos aaaProvisioning com filtros de escopo | Microsoft Docs
description: "Saiba como os filtros de escopo toouse tooprevent objetos em aplicativos que dão suporte ao provisionamento automatizado de usuários, na verdade, está sendo provisionado se um objeto não atender às suas necessidades de negócios."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Provisionamento de aplicativo com base em atributo com filtros de escopo
Olá objetivo desta seção é tooexplain como toouse escopo filtra toodefine com base em atributo regras que determinam quais usuários são provisionados toohello aplicativo.

## <a name="clauses-and-scope-groups"></a>Cláusulas e grupos de escopo
![Filtro de Escopo][1] 

Filtros de escopo são definidos por um ou mais **grupos de escopo** e cada um deles contém uma ou mais **cláusulas**. cláusulas de saudação toosee para um grupo de escopo específico, expandi-lo clicando em Olá seta à esquerda da toohello saudação do nome do grupo.

Um **cláusula** determina quais usuários podem toopass por meio de saudação filtro de escopo, avaliando os atributos de cada usuário. Por exemplo, você pode ter uma cláusula que requer que 'estado' atributo igual Nova York um usuário, para que somente os usuários de Nova York serão provisionados no aplicativo hello.

![Nome do grupo de escopo][2] 

Cada **grupo de escopo** inicia com um obrigatório **cláusula**, conforme mostrado na captura de tela de saudação acima. Essa cláusula declara que o usuário Olá deve ser atribuído primeiro aplicativo toohello antes de ser avaliado pelos filtros de escopo. Essa cláusula não pode ser excluída nem modificada.

Você pode adicionar novas cláusulas ou novos grupos de escopo, pressionando o botão adequado hello. Você pode dar um nome a cada grupo de escopo editando sua propriedade **Nome do Grupo de Escopo** .

## <a name="how-scoping-filters-are-evaluated"></a>Como os filtros de escopo são avaliados
Durante o provisionamento, podemos testar cada usuário atribuído em relação a seu escopo toodetermine de filtros, se esse usuário merece acesso toohello aplicativo. Você pode pensar em cada cláusula como sendo um teste que deve ser passado para Olá usuário tooavoid ser filtrado. 

Se você tiver vários grupos de escopo definidos, cada usuário deve passar pelo menos um deles tooaccess aplicativo hello. Em cada grupo de escopo, no entanto, Olá usuário deve passar cada cláusula toopass desse grupo de escopo específico. 

Em outras palavras, você pode pensar como os grupos sendo OR juntos, e você pode pensar em cláusulas de saudação dentro deles como sendo AND juntos. Por exemplo, considere Olá abaixo do filtro de escopo:

![Nome do grupo de escopo][3]  

De acordo com toothis filtro de escopo, os usuários devem atender a seguir Olá critérios, toobe provisionado:

1. Eles devem ser atribuídos toohello aplicativo.
2. Eles devem trabalhar no departamento de engenharia Olá
3. Eles devem trabalhar em São Francisco ou no Canadá.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md)
* [Personalizando os mapeamentos de atributos para provisionamento de usuários](active-directory-saas-customizing-attribute-mappings.md)
* [Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Notificações de provisionamento de conta](active-directory-saas-account-provisioning-notifications.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
