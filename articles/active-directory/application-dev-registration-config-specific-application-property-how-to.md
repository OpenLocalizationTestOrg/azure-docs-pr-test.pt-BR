---
title: "toofill aaaHow os campos específicos para um aplicativo personalizado | Microsoft Docs"
description: "Orientação sobre como campos toofill out específicas quando você está registrando um aplicativo desenvolvido personalizado com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Como toofill os campos específicos para um aplicativo personalizado

Este artigo fornecerá uma breve descrição de todos os campos disponíveis do hello no formulário de registro de aplicativo hello em Olá [portal do Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Registrar um novo aplicativo

-   tooregister um novo aplicativo, navegar toohello [portal do Azure](https://portal.azure.com).

-   Olá à esquerda no painel de navegação, clique em **do Active Directory do Azure.**

-   Escolha **Registros do aplicativo** e clique em **Adicionar**.

-   Abra esse formulário de registro de aplicativo hello.

## <a name="fields-in-hello-application-registration-form"></a>Campos no formulário de registro de aplicativo hello


| Campo            | Descrição                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nome             | nome de saudação do aplicativo hello. Ele deve ter um mínimo de quatro caracteres.                |
| Tipo de aplicativo | **Aplicativo Web/API Web**: um aplicativo que representa um aplicativo Web, uma API Web ou ambos 
| |**Nativo**: um aplicativo que pode ser instalado no dispositivo ou no computador de um usuário           |
| URL de logon      | Olá URL onde os usuários possam entrar toouse seu aplicativo                                  |

Depois de preencher Olá acima campos, aplicativo hello ser registrado no portal do Azure de saudação e redirecionado toohello página de aplicativo. Olá **configurações** botão no painel de aplicativo hello abre a página de configurações de saudação, que tem mais campos para você toocustomize seu aplicativo. Olá tabela a seguir descreve todos os campos de saudação na página de configurações de saudação. Observe que você verá apenas um subconjunto desses campos, dependendo tipo de aplicativo que você criou, um aplicativo Web ou um aplicativo nativo.

| Campo           | Descrição                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID do aplicativo  | Quando você registra um aplicativo, o Azure AD atribui a seu aplicativo uma ID de aplicativo. ID do aplicativo Hello pode ser usado toouniquely identificar seu aplicativo em tooAzure de solicitações de autenticação AD, bem como recursos de tooaccess como Olá API do Graph.                                                          |
| URI de ID do aplicativo      | Isso deve ser um URI exclusivo, normalmente de forma Olá **https://&lt;locatário\_nome&gt;/&lt;aplicativo\_nome&gt;.** Isso é usado durante o fluxo de concessão de autorização hello, como um recurso de saudação do identificador exclusivo toospecify qual token Olá deve ser emitido para. Ele também se torna Olá 'aud' declaração no token de acesso de saudação emitida. |
| Carregar novo logotipo | Você pode usar este tooupload um logotipo para seu aplicativo. logotipo de saudação deve estar no formato. bmp,. jpg ou. PNG e tamanho do arquivo hello deve ser menor que 100KB. dimensões de saudação para imagem Olá deverão ser 215 x 215 pixels, com as dimensões da imagem central de 94 x 94 pixels.                                                       |
| URL da home page   | Isso é Olá URL de logon especificado durante o registro do aplicativo.                                                                                                                                                                                                                                              |
| URL de logoff      | Essa URL de logout de logout único hello. AD do Azure envia uma solicitação de logout toothis URL quando o usuário Olá limpa toda a sessão com o Azure AD usando qualquer outro aplicativo registrado.                                                                                                                                       |
| Multilocatário  | Essa opção especifica se o aplicativo hello pode ser usado por vários locatários. Normalmente, isso significa que organizações externas podem usar seu aplicativo registrando-o em seu locatário e conceder acesso tootheir dados de organização.                                                                   |
| URLs de resposta      | Olá URLs de resposta são pontos de extremidade de saudação onde o AD do Azure retornam todos os tokens que solicita a seu aplicativo.                                                                                                                                                                                                          |
| URIs de redirecionamento   | Para aplicativos nativos, isso é onde o usuário Olá ser autorização bem-sucedida toofollowing enviados. Verificação AD do Azure que Olá redirecione o URI de solicitação fontes seu aplicativo no hello OAuth 2.0 corresponde a um dos valores de saudação registrado no portal de saudação.                                                            |
| simétricas            | Você pode criar APIs protegido pelo AD do Azure sem qualquer interação do usuário da web do acesso chaves tooprogrammatically. De saudação \* \*chaves\* \* página, insira uma data de expiração de descrição e hello chave e salvar toogenerate Olá chave. Não se toosave em algum lugar seguro, pois não será capaz de tooaccess-lo mais tarde.             |

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
