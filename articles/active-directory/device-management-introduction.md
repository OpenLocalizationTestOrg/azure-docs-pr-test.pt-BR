---
title: gerenciamento de toodevice aaaIntroduction no Active Directory do Azure | Microsoft Docs
description: "Saiba como o gerenciamento de dispositivos pode ajudá-lo tooget controle os dispositivos de saudação que estão acessando os recursos em seu ambiente."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Gerenciamento de toodevice de Introdução no Active Directory do Azure

Em um mundo móveis, primeiro, a nuvem, o Azure Active Directory (AD do Azure) permite toodevices de logon único, os aplicativos e serviços de qualquer lugar. Com a proliferação de saudação de dispositivos - incluindo BYOD traga seu próprio dispositivo (), profissionais de TI enfrentam dois objetivos opostos:

- Capacitar Olá os usuários finais toobe produtivo sempre e
- Proteger os ativos corporativos Olá a qualquer momento

Por meio de dispositivos, os usuários recebem acesso tooyour os ativos corporativos. tooprotect seus recursos corporativos, como um administrador de TI, você deseja toohave controle sobre esses dispositivos. Isso permite que você toomake-se de que os usuários estão acessando os recursos de dispositivos que atendem aos padrões de segurança e conformidade. 

Gerenciamento de dispositivo também é foundation Olá para [acesso condicional baseado em dispositivo](active-directory-conditional-access-policy-connected-applications.md). Com acesso condicional com base no dispositivo, você pode garantir que acesso tooresources em seu ambiente só é possível com dispositivos confiáveis.   

Este tópico explica como funciona o gerenciamento de dispositivo no Azure Active Directory.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Obtendo dispositivos sob o controle de saudação do AD do Azure

tooget um dispositivo sob o controle de saudação do AD do Azure, você tem duas opções:

- Registro 
- Adição

**Registrando** tooAzure um dispositivo AD permite que você toomanage identidade do dispositivo. Quando um dispositivo é registrado, o registro de dispositivos do AD do Azure fornece dispositivo Olá com uma identidade que é usada tooauthenticate Olá dispositivo quando um usuário entrar tooAzure AD. Você pode usar o hello identidade tooenable ou desativar um dispositivo.

Quando combinado com uma solução de management(MDM) de dispositivo móvel como Microsoft Intune, os atributos de dispositivo Olá no AD do Azure são atualizados com informações adicionais sobre o dispositivo de saudação. Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade. Para saber mais sobre o registro de dispositivos no Microsoft Intune, confira Enroll devices for management in Intune (Registrar dispositivos para gerenciamento no Intune).

**Unindo** um dispositivo é uma extensão tooregistering um dispositivo. Isso significa, ele fornece todos os benefícios de saudação de registrar um dispositivo e em adição toothis, ele também altera o estado de um dispositivo local hello. A alteração do estado local Olá permite que o dispositivo de tooa toosign-in de usuários usando uma conta de escola ou trabalho organizacional em vez de uma conta pessoal.

## <a name="azure-ad-registered-devices"></a>Dispositivos registrados no Azure AD   

Olá, meta de dispositivos do AD do Azure registrado é tooprovide suporte Olá **BYOD traga seu próprio dispositivo ()** cenário. Nesse cenário, um usuário pode acessar os recursos controlados pelo Azure Active Directory da sua organização usando um dispositivo pessoal.  

![Dispositivos registrados no Azure AD](./media/device-management-introduction/03.png)

acesso de saudação baseia-se em uma conta corporativa ou de estudante que foi digitada no dispositivo de saudação.  
Por exemplo, Windows 10 permite que os usuários tooadd um trabalho ou escola conta tooa PC, tablet ou telefone.  
Quando um usuário tiver adicionado um trabalho ou a conta de escola, o dispositivo Olá é registrado com o Azure AD e opcionalmente registrado no sistema de gerenciamento (MDM) do dispositivo móvel Olá sua organização tiver configurado. Os usuários da organização podem adicionar um ou escolar dispositivo pessoal do conta tooa convenientemente:

- Ao acessar um aplicativo de trabalho para Olá primeira vez
- Manualmente por meio de saudação **configurações** menu no caso de saudação do Windows 10 

Você pode configurar dispositivos registrados no Azure AD para Windows 10, iOS, Android e macOS.

## <a name="azure-ad-joined-devices"></a>Dispositivos adicionados ao Azure AD

meta de saudação de dispositivos do AD do Azure associado é toosimplify:

- As implantações de dispositivos Windows que pertencem à organização 
- Acesso tooorganizational aplicativos e recursos de dispositivos Windows

![Dispositivos registrados no Azure AD](./media/device-management-introduction/02.png)


Essas metas são realizadas por fornecer aos usuários uma experiência de autoatendimento para obtenção de dispositivos de propriedade do trabalho sob o controle de saudação do AD do Azure.  
A **adição ao Azure AD** destina-se a organizações que usam somente a nuvem/priorizam a nuvem. Normalmente, são pequenas e médias empresas, que não têm uma infraestrutura do Active Directory local para Windows Server. 

Dispositivos do AD do Azure associado a implementação fornece Olá benefícios a seguir:

- **Logon único (SSO)** tooyour Azure gerenciados serviços e aplicativos SaaS. Os usuários não visualizam solicitações adicionais de autenticação ao acessar recursos de trabalho. Olá funcionalidade de SSO é mesmo quando não estiverem conectados toohello rede de domínio disponível.

- **Roaming em conformidade corporativa** das configurações de usuário entre dispositivos adicionados. Os usuários não precisam tooconnect configurações de toosee de conta (por exemplo, Hotmail) um Microsoft em todos os dispositivos.

- **Acesso tooWindows Store para empresas** usando a conta do AD. Os usuários podem escolher entre um inventário dos aplicativos pré-selecionada pela organização hello.

- **Windows Hello** suporte para recursos de toowork acesso seguro e conveniente.

- **Restrição de acesso** tooapps de apenas os dispositivos que atendem à política de conformidade.

Embora a adição ao Azure AD se destine basicamente às organizações que não têm uma infraestrutura do Active Directory local para Windows Server, você certamente também pode usá-la em cenários em que:

- Você não pode usar uma junção de domínio local, por exemplo, se você precisar de tooget de dispositivos móveis, como tablets e celulares sob controle.

- Os usuários precisam ter principalmente tooaccess Office 365 ou outros aplicativos SaaS integrados ao AD do Azure.

- Você deseja toomanage um grupo de usuários no AD do Azure, em vez de no Active Directory. Isso pode se aplicar, por exemplo, tooseasonal funcionários, prestadores de serviço ou os alunos.

- Você deseja tooprovide junção recursos tooworkers em filiais remotas com a infraestrutura limitada local.

Você pode configurar dispositivos adicionados ao Azure AD para dispositivos com Windows 10.


## <a name="hybrid-azure-ad-joined-devices"></a>Dispositivos adicionados ao Azure AD híbrido

Para mais de uma década, muitas organizações usou Olá domínio junção tootheir local do Active Directory tooenable:

- IT departamentos toomanage trabalho dispositivos de propriedade de um local central.

- Os usuários toosign em dispositivos de tootheir com seu Active Directory ou de estudante contas. 

Normalmente, as organizações com um volume no local dependem de métodos tooprovision dispositivos de imagem e geralmente usam **System Center Configuration Manager (SCCM)** ou **(GP) da política de grupo** toomanage -los.

Se seu ambiente tiver um local espaço AD e você também desejar que se beneficiam de recursos de saudação fornecidos pelo Active Directory do Azure, você pode implementar dispositivos do AD do Azure associado híbrida. Esses são dispositivos que são ambos, tooyour ingressado no Active Directory local e o Active Directory do Azure.

![Dispositivos registrados no Azure AD](./media/device-management-introduction/01.png)


Você deverá usar dispositivos adicionados ao Azure AD híbrido se:

- Você tem dispositivos Win32 de toothese implantado de aplicativos que usam NTLM / Kerberos.

- Você precisar de GP ou SCCM / dispositivos de toomanage do DCM.

- Você deseja que os dispositivos toocontinue tooconfigure soluções, geração de imagens toouse para seus funcionários.

É possível configurar dispositivos adicionados ao Azure AD para dispositivos com Windows 10 e de nível inferior, como Windows 8 e Windows 7.

## <a name="summary"></a>Resumo

Com o gerenciamento de dispositivo no Azure AD, é possível: 

- Simplificar o processo de saudação de colocar os dispositivos sob o controle de saudação do AD do Azure

- Fornecer aos usuários com recursos de baseado em nuvem da organização toouse fácil acesso tooyour

Como uma regra prática, você deve usar:

- Dispositivos registrados no Azure AD para dispositivos pessoais

- AD do Azure associado dispositivos para dispositivos que não estão ligados tooan AD local 

- Híbrido do AD do Azure associado dispositivos para dispositivos que estão ligados tooan AD local     




## <a name="next-steps"></a>Próximas etapas

- tooget uma visão geral de como o dispositivo toomanage no hello Azure portal, consulte [gerenciamento de dispositivos usando Olá portal do Azure](device-management-azure-portal.md)

- toolearn mais sobre o acesso condicional com base no dispositivo, consulte [configurar políticas de acesso condicional com base no dispositivo do Active Directory do Azure](active-directory-conditional-access-policy-connected-applications.md).

- toosetup híbrido do Azure AD associado dispositivos, consulte [como tooconfigure híbrida do Active Directory do Azure associados dispositivos](device-management-hybrid-azuread-joined-devices-setup.md).


