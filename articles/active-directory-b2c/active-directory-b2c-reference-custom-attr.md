---
title: 'Azure Active Directory B2C: atributos personalizados | Microsoft Docs'
description: "Como os atributos de toouse personalizado no Azure Active Directory B2C toocollect informações sobre seus consumidores"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>B2C de diretório ativo do Azure: Use informações de toocollect de atributos personalizados sobre seus consumidores
O diretório do Azure AD (Azure Active Directory) B2C é fornecido com um conjunto interno de informações (atributos): Nome, Sobrenome, Cidade e CEP, entre outros atributos. No entanto, todos os aplicativos voltados para o consumidor tem requisitos exclusivos em toogather quais atributos de consumidores. Com o Azure AD B2C, você pode estender o conjunto de saudação de atributos armazenados em cada conta de consumidor. Você pode criar atributos personalizados em Olá [portal do Azure](https://portal.azure.com/) e usá-lo em suas políticas de inscrição, conforme mostrado abaixo. Você também pode ler e gravar esses atributos usando Olá [do Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Os atributos personalizados usam as [Extensões de Esquema de Diretório da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Como criar um atributo personalizado
1. [Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Clique em **Atributos de usuário**.
3. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
4. Forneça um **nome** para atributo personalizado de saudação (por exemplo, "ShoeSize") e, opcionalmente, um **descrição**. Clique em **Criar**.
   
   > [!NOTE]
   > Somente hello "Cadeia de caracteres" **tipo de dados** está disponível no momento.
   > 
   > 

atributo personalizado Olá agora está disponível na lista de saudação do **atributos de usuário**e para uso em suas políticas de inscrição.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Usar um atributo personalizado na sua política de inscrição
1. [Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Clique em **Políticas de inscrição**.
3. Clique em sua política de inscrição (por exemplo, "B2C_1_SiUp") tooopen-lo. Clique em **editar** na parte superior de saudação da folha de saudação.
4. Clique em **inscrição atributos** e selecione Olá personalizada (por exemplo, "ShoeSize"). Clique em **OK**.
5. Clique em **declarações de aplicativo** e atributo personalizado Olá select. Clique em **OK**.
6. Clique em **salvar** na parte superior de saudação da folha de saudação.

Você pode usar o recurso de "Executar agora" hello na experiência do consumidor Olá política tooverify hello. Agora você deve vê "ShoeSize" hello lista de atributos coletados durante a inscrição do consumidor e vê-lo no aplicativo de token tooyour back enviados hello.

## <a name="notes"></a>Observações
* Juntamente com as políticas de inscrição, os atributos personalizados também podem ser usados nas políticas de inscrição ou de entrada e também nas políticas de edição de perfil.
* Há uma limitação conhecida de atributos personalizados. É somente criado Olá primeira vez que ele é usado em qualquer política e não quando você adicionar lista de toohello de **atributos de usuário**.

