---
title: "Azure Active Directory B2C: criar um locatário do Azure Active Directory B2C | Microsoft Docs"
description: "Um tópico sobre como toocreate um B2C do Azure Active Directory de locatário"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Criar um locatário do Azure Active Directory B2C no hello portal do Azure

Editado por Sipi.

Este Guia de início rápido ajuda a criar um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos. Quando você terminar, você tem um toouse de locatário B2C para registrar aplicativos B2C.

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Faça logon no tooAzure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Criar um locatário do Azure AD B2C

Os recursos B2C não podem ser habilitados em seus locatários existentes. É necessário toocreate um locatário Azure AD B2C.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Parabéns, você criou um locatário do Azure Active Directory B2C. Você é um Administrador Global do locatário hello. Você pode adicionar outros Administradores Globais conforme necessário. tooswitch tooyour novo locatário, clique em Olá *gerenciar seu novo link de locatário*.

![Gerenciar seu novo link de locatário](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Se você estiver planejando toouse um locatário B2C para um aplicativo de produção, leia o artigo de saudação em [escala de produção versus locatários visualização B2C](active-directory-b2c-reference-tenant-type.md). Há conhecidos problemas quando você excluir um existente B2C do locatário e recriá-la com hello mesmo nome de domínio. É necessário toocreate um locatário B2C com um nome de domínio diferente.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Vincular sua assinatura do locatário tooyour

Você precisa toolink seu B2C do AD do Azure locatário tooyour assinatura do Azure tooenable todas as funcionalidades de B2C e pagar pelos encargos de uso. mais, leia toolearn [neste artigo](active-directory-b2c-how-to-enable-billing.md). Se você não vincular seu tooyour de locatário do Azure AD B2C assinatura do Azure, alguma funcionalidade será bloqueada e, você verá uma mensagem de aviso ("nenhuma assinatura toothis vinculados B2C locatário ou Olá assinatura precisa de atenção.") nas configurações de saudação B2C. É importante que você execute esta etapa antes de enviar seus aplicativos para produção.

## <a name="easy-access-toosettings"></a>Acesso fácil toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Você também pode acessar a folha de saudação inserindo `Azure AD B2C` na **pesquisar recursos** na parte superior de saudação do portal de saudação. Na lista de resultados de saudação, selecione **do Azure AD B2C** tooaccess Olá B2C folha de configurações.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Registrar seu aplicativo B2C em um locatário B2C](active-directory-b2c-app-registration.md)
