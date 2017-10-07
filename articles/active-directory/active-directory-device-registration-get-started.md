---
title: "aaaHow tooconfigure o registro automático de dispositivos de domínio do Windows com o Active Directory do Azure | Microsoft Docs"
description: "Configure seu tooregister de dispositivos do Windows ingressado no domínio automática e silenciosa com o Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introdução ao registro de dispositivos do Azure Active Directory

Registro de dispositivo do Active Directory do Azure é a base de saudação para cenários de acesso condicional com base no dispositivo. Quando um dispositivo é registrado, registro de dispositivo do Active Directory do Azure fornece dispositivo Olá com uma identidade que é o dispositivo de saudação do tooauthenticate usado quando Olá usuário faz logon. dispositivo Olá autenticado e atributos de saudação do dispositivo hello, podem ser usado tooenforce políticas de acesso condicional para aplicativos hospedados na nuvem hello e local.

Quando combinado com uma solução de management(MDM) de dispositivo móvel como Microsoft Intune, os atributos de dispositivo Olá no Active Directory do Azure são atualizados com informações adicionais sobre o dispositivo de saudação. Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade. Para saber mais sobre o registro de dispositivos no Microsoft Intune, veja Registrar dispositivos para gerenciamento no Intune.
Os cenários habilitados pelo Registro de Dispositivos do Azure Active Directory inclui suporte para dispositivos iOS, Android e Windows. cenários de saudação individuais que utilizam o registro de dispositivo do AD do Azure podem ter requisitos e suporte de plataforma mais específicos. 

Esses cenários são os seguintes:

- **Acesso condicional para aplicativos do Office 365 com o Microsoft Intune:** administradores de TI podem provisionar o acesso condicional dispositivo políticas toosecure recursos corporativos, enquanto a saudação mesmo momento que permite aos operadores de informações em dispositivos compatíveis Serviços de saudação tooaccess. Para saber mais, veja Políticas de dispositivo de acesso condicional para serviços do Office 365.

- **Tooapplications de acesso condicional que estão hospedados no local:** você pode usar dispositivos registrados com políticas de acesso para aplicativos que são configurados toouse do AD FS com o Windows Server 2012 R2. Para obter mais informações sobre como configurar o acesso condicional para local, consulte [Configurando o acesso condicional local usando o registro do dispositivo do Azure Active Directory](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuração do registro de dispositivos Active Directory do Azure

registro de dispositivo toosetup, você tem várias opções:

- Dispositivos podem se registrem ao domínio tooAzure ingressado no AD. Para obter mais informações sobre este tópico, você pode aprender mais sobre as configurações de junção do Azure AD e hello necessárias para usuários de domínio de toojoin AD do Azure.

- Dispositivos podem ser registrados quando usuários adicionarem trabalho ou escola contas tooWindows em um dispositivo pessoal ou dispositivos móveis se conectam tooa recursos de trabalho que exigem o registro. tooensure isso, você deve habilitar o registro de dispositivo do AD do Azure no hello Portal do Azure. 

- Os dispositivos podem ser registrados usando o registro automático de dispositivo para computadores tradicionais ingressados em domínio. tooensure isso, você deve primeiro configurar Azure AD Connect antes de continuar com o registro automático do dispositivo.

Para obter instruções mais recentes, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).  
Você também pode revisar e habilitar ou desabilitar os dispositivos registrados usando Olá Portal do administrador no Active Directory do Azure.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Habilitar o serviço de registro de dispositivo do Active Directory do Azure Olá

**Olá tooenable serviço de registro de dispositivo do Active Directory do Azure:**

1.  Entre em toohello portal do Microsoft Azure como administrador.

2.  No painel esquerdo do hello, selecione **do Active Directory**.

3.  Na guia de diretório hello, selecione seu diretório.

4.  Clique em **Configurar**.

5.  Role muito**dispositivos**.

6.  Selecione TODOS para OS USUÁRIOS PODEM REGISTRAR SEUS DISPOSITIVOS COM O AZURE AD.

7.  Selecione o número máximo de saudação de dispositivos que você deseja tooauthorize por usuário.

registro de saudação com Microsoft Intune ou gerenciamento de dispositivo móvel para Office 365 requer o registro de dispositivos. Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NONE** estará desabilitado. Certifique-se de que eles estão configurados corretamente e tem Olá apropriado de licenciamento.

Por padrão, a autenticação de dois fatores não está habilitada para o serviço de saudação. No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo.

- Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de usuário para autenticação multifator, consulte Adicionar autenticação multifator tooAzure do Active Directory

- Se estiver usando o AD FS com o Windows Server 2012 R2, configure um módulo de autenticação de dois fatores no AD FS. Confira Usar a Autenticação Multifator com os Serviços de Federação do Active Directory.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Exibir e gerenciar objetos de dispositivo no Active Directory do Azure

No portal do administrador do Azure hello, exibir, bloquear e desbloquear dispositivos. Um dispositivo que está bloqueado não terá mais acesso tooapplications que são configurados tooallow apenas dispositivos registrados.

**tooview e gerenciar objetos de dispositivo no Active Directory do Azure:**
 
1.  Faça logon no toohello portal do Microsoft Azure como administrador.

2.  No painel esquerdo do hello, selecione **do Active Directory**.

3.  Selecione seu diretório.

4.  Selecione **Usuários**. 

5.  Clique em usuário Olá para o qual você deseja que os dispositivos de saudação toosee.

6.  Selecione **Dispositivos**.

7.  Selecione **Dispositivos Registrados**.

Agora, você pode revisar, bloquear ou desbloquear os dispositivos registrados do usuário hello.
Dispositivos Windows 10 que estão em locais ingressado no domínio e registrados automaticamente não aparecem na guia de usuários de saudação. Use toofind de comando do PowerShell Get-MsolDevice Olá todos os seus dispositivos da empresa. 


## <a name="next-steps"></a>Próximas etapas

toosetup automatizada de registro do dispositivo, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).


