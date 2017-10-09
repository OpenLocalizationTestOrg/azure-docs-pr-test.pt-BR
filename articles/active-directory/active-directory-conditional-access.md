---
title: "acesso aaaConditional em Olá portal clássico do Azure | Microsoft Docs"
description: "Use controle de acesso condicional no hello toocheck de portal clássico do Azure para condições específicas ao autenticar para tooapplications de acesso."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Acesso condicional no hello portal clássico do Azure

Este tópico é sobre acesso condicional no hello portal clássico do Azure. Para obter informações mais recentes do hello sobre acesso condicional no hello Active Directory do Azure, consulte [acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal.md).


recursos de controle de saudação no acesso condicional do Azure Active Directory (AD do Azure) oferecem maneiras simples toohelp recursos de segurança na nuvem hello e local. Políticas de acesso condicional, como autenticação multifator pode ajudar a proteger contra riscos de saudação do roubo e capturados credenciais. Outras políticas de acesso condicional podem ajudar a proteger os dados de sua organização. Por exemplo, além disso toorequiring credenciais, você pode ter uma política que somente dispositivos que são registrados em um sistema de gerenciamento de dispositivo móvel como Microsoft Intune podem acessar os serviços de confidenciais da sua organização.

## <a name="prerequisites"></a>Pré-requisitos
O acesso condicional do Azure AD é um recurso do [Azure Active Directory Premium](http://www.microsoft.com/identity). Cada usuário que acessa um aplicativo com políticas de acesso condicional aplicadas deve ter uma licença do Azure AD Premium. Você pode saber mais sobre os requisitos de licença no [relatório de usuário sem licença](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Como o controle de acesso condicional é imposto?
Com controle de acesso condicional no local, AD do Azure verifica condições específicas Olá definida para um usuário tooaccess um aplicativo. Depois que os requisitos de acesso são atendidos, o usuário Olá é autenticado e pode acessar o aplicativo hello.  

![Visão geral do acesso condicional](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Conditions
Estas são as condições que podem ser incluídas em uma política de acesso condicional:

* **Associação de grupo**. Controle o acesso do usuário com base na associação em grupo.
* **Local**. Use local Olá Olá tootrigger vários fatores de autenticação do usuário e use o bloco de controles quando um usuário não estiver em uma rede confiável.
* **Plataforma de dispositivos**. Utilize a plataforma de dispositivo hello, como iOS, Android, Windows Mobile ou Windows, como uma condição para a aplicação de política.
* **Habilitado pelo dispositivo**. O estado do dispositivo, se está habilitado ou desabilitado, é validado durante a avaliação da política de dispositivo. Se você desativar um dispositivo perdido ou roubado no diretório hello, não possa atender os requisitos de política.
* **Risco de entrada e usuário**. Você pode usar o [Azure AD Identity Protection](active-directory-identityprotection.md) para políticas de risco de acesso condicional. Políticas de risco de acesso condicional ajudam a oferecer a proteção avançada da organização com base em eventos de risco e atividades de entrada incomuns.

## <a name="controls"></a>Controles
Estes são os controles que você pode usar tooenforce uma política de acesso condicional:

* **Autenticação multifator**. Você pode exigir autenticação forte por meio da autenticação multifator. Você pode usar a autenticação multifator com a autenticação multifator do Azure ou usando um provedor de autenticação multifator local, combinado a AD FS (Serviços de Federação do Active Directory). Usando a autenticação multifator ajuda a proteger os recursos que está sendo acessado por um usuário não autorizado pode ter obtido acesso toohello credenciais de um usuário válido.
* **Bloquear**. Você pode aplicar condições como acesso de usuário do usuário local tooblock. Por exemplo, você pode bloquear o acesso quando um usuário não está em uma rede confiável.
* **Dispositivos em conformidade**. Você pode definir políticas de acesso condicional no nível do dispositivo de saudação. Você pode configurar uma política para que somente os computadores que ingressaram no domínio ou dispositivos móveis que são registrados em um aplicativo de gerenciamento de dispositivo móvel possam acessar os recursos de sua organização. Por exemplo, você pode usar conformidade do dispositivo do Intune toocheck e, em seguida, relatá-lo tooAzure AD para a imposição quando o usuário Olá tentativas tooaccess um aplicativo. Para obter orientações detalhadas sobre como toouse Intune tooprotect aplicativos e dados, consulte [proteger aplicativos e dados com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Você também pode usar proteção de dados de tooenforce do Intune para dispositivos perdidos ou roubados. Para saber mais, confira [Ajudar a proteger seus dados com apagamento completo ou seletivo usando o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Aplicativos
Você pode impor uma política de acesso condicional no nível do aplicativo hello. Definir níveis de acesso para aplicativos e serviços em nuvem hello ou local. política de saudação é aplicado diretamente toohello site ou serviço. Olá política é aplicada para acesso toohello navegador e tooapplications que acessam o serviço de saudação.

## <a name="device-based-conditional-access"></a>Acesso condicional com base em dispositivo
Você pode restringir o acesso tooapplications de dispositivos que são registrados com o AD do Azure e que atendem a condições específicas. Dispositivos com acesso condicional protege os recursos de uma organização de usuários que tentam tooaccess recursos de saudação do:

* Dispositivos desconhecidos ou não gerenciados.
* Dispositivos que não atenderem às políticas de segurança Olá sua organização configurada.

Você pode definir políticas com base nestes requisitos:

* **Dispositivos associados ao domínio**. Defina um toodevices de acesso de toorestrict política que tooan ingressado no local do Active Directory domínio, e que também são registrados com o AD do Azure. Essa política se aplica a tooWindows desktops, laptops e tablets de empresa.
  Para obter mais informações sobre como tooset o registro automático de dispositivos que ingressaram no domínio com o AD do Azure, consulte [configurar o registro automático de dispositivos de domínio do Windows com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Dispositivos em conformidade**. Definir um toodevices acesso toorestrict de política que são marcados como **compatíveis** no diretório de sistema de gerenciamento de saudação. Essa política garante que apenas os dispositivos que atendam às políticas de segurança como imposição de criptografia de arquivos em um dispositivo tenham permissão para acesso. Você pode usar esta diretiva toorestrict acesso de saudação dispositivos a seguir:
  
  * **Dispositivos associados ao domínio do Windows**. Gerenciado pelo System Center Configuration Manager (na ramificação atual do hello) implantado em uma configuração híbrida.
  * **Dispositivos pessoais ou de trabalho do Windows Mobile 10**. Gerenciado pelo Intune ou por um sistema de gerenciamento de dispositivo móvel com suporte de terceiros.
  * **iOS and Android devices**. Gerenciado pelo Intune.

Os usuários que acessam aplicativos que são protegidos por um dispositivo com base em política de autoridade de certificação deve acessar o aplicativo hello de um dispositivo que atenda aos requisitos dessa política. Acesso negado se tentado em um dispositivo que não atende aos requisitos de política.

Para obter informações sobre como tooconfigure um baseado em dispositivo, política de autoridade de certificação no AD do Azure, consulte [definir a política de acesso condicional com base no dispositivo para aplicativos conectados do Active Directory do Azure](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Recursos
Consulte Olá toolearn de artigos e categorias de recursos mais sobre como configurar o acesso condicional para a sua organização a seguir.

### <a name="multi-factor-authentication-and-location-policies"></a>Políticas de local e de autenticação multifator
* [Introdução ao acesso condicional tooAzure conectada AD aplicativos com base no grupo, o local e as políticas de autenticação multifator](active-directory-conditional-access-azuread-connected-apps.md)
* [Aplicativos e navegadores com suporte](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Acesso condicional com base em dispositivo
* [Definir a política de acesso condicional com base no dispositivo para acesso de aplicativos conectados do Active Directory do controle tooAzure](active-directory-conditional-access-policy-connected-applications.md)
* [Configurar o registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Solução de problemas para problemas de acesso do Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Ajudar a proteger dados em dispositivos perdidos ou roubados usando o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Proteger recursos com base em risco de entrada
* [Azure AD Identity Protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Próximas etapas
* [Perguntas frequentes sobre acesso condicional](active-directory-conditional-faqs.md)
* [Referência técnica](active-directory-conditional-access-technical-reference.md)

