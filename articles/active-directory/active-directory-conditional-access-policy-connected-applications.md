---
title: "políticas de acesso condicional com base no dispositivo do Active Directory do Azure aaaConfigure | Microsoft Docs"
description: "Saiba como políticas de acesso condicional com base no dispositivo do tooconfigure Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Configurar políticas de acesso condicional com base no dispositivo do Azure Active Directory

Com o [acesso condicional do Azure AD (Active Directory)](active-directory-conditional-access-azure-portal.md), você pode ajustar como usuários autorizados podem acessar seus recursos. Por exemplo, você pode limitar Olá acessem toocertain recursos tootrusted dispositivos. Uma política de acesso condicional que exige um dispositivo confiável também é conhecida como política de acesso condicional com base no dispositivo.

Este tópico fornece informações sobre como tooconfigure condicional de dispositivos com políticas de acesso para aplicativos conectados AD do Azure. 


## <a name="before-you-begin"></a>Antes de começar

O acesso condicional com base no dispositivo associa o **acesso condicional do Azure AD** e o **gerenciamento de dispositivos do Azure AD**. Se você ainda não estiver familiarizado com uma dessas áreas, você deve ler Olá tópicos a seguir primeiro:

- **[Acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal.md)**  -este tópico fornece uma visão geral conceitual de condicional acessar e Olá terminologia relacionada.

- **[Gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)**  -este tópico fornece uma visão geral de saudação várias opções que tooconnect dispositivos com o Azure AD. 


## <a name="trusted-devices"></a>Dispositivos confiáveis

Em um mundo móveis, primeiro, a nuvem, o Active Directory do Azure permite toodevices de logon único, os aplicativos e serviços de qualquer lugar. Para determinados recursos no seu ambiente, concedendo acesso a usuários toohello podem não ser suficiente. Além disso toohello usuários, você pode também requer que um dispositivo confiável toobe usado tooaccess um recurso. Em seu ambiente, você pode definir que um dispositivo confiável é com base em Olá seguintes componentes:

- Olá [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) em um dispositivo
- Se um dispositivo está em conformidade
- Se um dispositivo foi adicionado ao domínio 

Olá [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) é caracterizado por sistema operacional Olá que está em execução no seu dispositivo. Em sua política de acesso condicional baseado em dispositivo, você pode limitar acesso toocertain recursos toospecific as plataformas de dispositivos.



Em uma política de acesso condicional baseado em dispositivo, você pode exigir toobe dispositivos confiáveis marcado como compatível.

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Dispositivos podem ser marcados como compatível no diretório Olá por:

- Intune 
- Um sistema de gerenciamento de dispositivo móvel de terceiros que se integre ao Azure AD  

Apenas dispositivos que estão conectado tooAzure AD podem ser marcados como compatíveis. tooconnect tooAzure um dispositivo do Active Directory, você tem Olá as opções a seguir: 

- Registrado no Azure AD
- Adicionado ao Azure AD
- Adicionado ao Azure AD híbrido

    ![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Se você tiver um volume de AD (Active Directory) no local, você pode considerar os dispositivos que não estão conectado tooAzure AD mas toobe tooyour unidas AD confiável.

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Próximas etapas

Antes de configurar uma política de acesso condicional com base no dispositivo em seu ambiente, você deve dar uma olhada em Olá [as práticas recomendadas para acesso condicional no Active Directory do Azure](active-directory-conditional-access-best-practices.md).

