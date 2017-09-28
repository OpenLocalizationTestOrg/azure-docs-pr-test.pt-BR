---
title: Arquivo de teste Sipi | Microsoft Docs
description: "Arquivo de teste para verificar dependências de ReadyForTest"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Arquivo de teste Sipi

Este Guia de início rápido ajuda você a registrar um aplicativo em um locatário do Microsoft Azure Active Directory (Azure AD) B2C em poucos minutos. Quando terminar, seu aplicativo estará registrado para uso no locatário B2C do Azure.

## <a name="prerequisites"></a>Pré-requisitos

Para compilar um aplicativo que aceite a inscrição e a entrada do consumidor, primeiro será necessário registrar o aplicativo em um locatário do Azure Active Directory B2C. Obtenha seu próprio locatário usando as etapas descritas em [Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md).

Os aplicativos criados da folha Azure AD B2C no portal do Azure devem ser gerenciados do mesmo local. Se você editar os aplicativos B2C usando o PowerShell ou outro portal, eles deixarão de ter suporte e não funcionarão com o Azure AD B2C. Consulte os detalhes da seção [aplicativos com falha](#faulted-apps). 

## <a name="navigate-to-b2c-settings"></a>Navegue até as configurações de B2C

Entre no [Portal do Azure](https://portal.azure.com/) como Administrador Global do locatário B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Escolha as próximas etapas com base no tipo de aplicativo que você está registrando:
