---
title: "dispositivos de tooWindows 10 de recursos de nuvem de aaaExtending por meio de junção do Active Directory do Azure | Microsoft Docs"
description: "Fornece uma visão geral detalhada de como os dispositivos Windows 10 podem utilizar tooget junção do Azure AD registrado no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure
## <a name="what-is-azure-active-directory-join"></a>O que é o Ingresso no Active Directory do Azure?
Azure junção do Active Directory (junção do Azure AD) é a funcionalidade de saudação que registra um dispositivo da empresa no Active Directory do Azure tooenable centralizado gerenciamento de dispositivo de saudação. Ele torna possível para os usuários, como funcionários e alunos tooconnect toohello enterprise nuvem por meio do Active Directory do Azure. Isso permite simplificado implantações do Windows e acesso tooorganizational aplicativos e recursos de dispositivos Windows, ambos corporativos e pessoais de (BYOD).

O Ingresso no Azure AD destina-se a empresas que priorizam a nuvem/usam somente a nuvem (normalmente, pequenas e médias empresas), que não têm uma infraestrutura do Active Directory do Windows Server local. Que ingresso no AD do Azure, tal pode e também ser usados por organizações grandes em dispositivos que não são capazes de fazer uma junção de domínio tradicional (dispositivos móveis, por exemplo), ou para usuários que precisam principalmente tooaccess Office 365 ou outros aplicativos SaaS integrados ao AD do Azure.

Embora o ingresso no domínio tradicional Olá ainda oferece Olá local melhor experiência em dispositivos que são capazes de junção de domínio, ingresso no Azure AD é adequado para dispositivos que não é possível o ingresso no domínio. Ingresso no AD do Azure também é adequado para gerenciamento de usuários em nuvem hello. Ele faz isso usando recursos de gerenciamento de dispositivos móveis em vez de ferramentas de gerenciamento de domínio tradicionais, como a Política de Grupo e o SCCM (System Center Configuration Manager).

![Visão geral de dispositivos corporativos e pessoais com o Active Directory local e o Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Por que as empresas devem adotar o Ingresso no Azure AD?
* **As empresas que são amplamente em Olá nuvem**: se você moveu ou estiver movendo tooa modelo no qual você está reduzindo o volume no local e deseja toooperate mais na nuvem hello, junção do Azure AD podem se beneficiar você. Você pode ter criado contas do Azure AD manualmente ou sincronizando seu Active Directory local. De qualquer forma, você tem uma conta no AD do Azure, e você pode usá-lo toosign tooWindows 10. Os usuários podem ingressar seu tooAzure computadores AD por meio de qualquer experiência de fora da caixa de saudação (OOBE) ou por meio do menu de configurações de saudação. Depois de ingressar, os usuários apreciarão o único sign-on (SSO) acesso toocloud recursos como o Office 365, em seus navegadores ou aplicativos do Office.
* **Instituições educacionais**: um dos cenários de saudação ouvimos sobre geralmente é que as instituições educacionais têm dois tipos de usuário: docentes e alunos. Os membros são considerados membros de longo prazo da organização Olá, para a criação de contas locais para eles é desejável. Mas os alunos são shorter-term membros da organização hello e, portanto, podem ser gerenciados no AD do Azure. Isso significa que a escala de diretório pode ser enviada nuvem toohello em vez de armazenada localmente. Isso também significa que os alunos podem entrar tooWindows com suas contas do AD do Azure e obter acesso tooOffice 365 recursos em seus navegadores ou aplicativos do Office.
* **As empresas de varejo**: outro cenário fomos informados sobre clientes é seus funcionários sazonais de toomanage desejo mais facilmente.  Novamente, as contas para funcionários em tempo integral de longo prazo geralmente são criadas como contas locais em computadores que ingressaram no domínio. Mas sazonais trabalhadores são membros shorter-term de org hello, portanto, é desejável toomanage-los onde licenças de usuário podem ser movidas mais facilmente ao redor. Criar essas contas de usuário na nuvem Olá com licenças do Office 365 permite que os benefícios de saudação do hello usuários tooget da assinatura tooWindows e aplicativos do Office com uma conta do AD do Azure. Enquanto isso, você mantém mais flexibilidade com suas licenças depois que eles partem.
* **Outras empresas**: embora você mantenha os usuários no Active Directory local, ainda poderia se beneficiar se os usuários ingressassem no Azure AD. Isso ocorre porque o Azure AD oferece uma experiência simplificada de ingresso, gerenciamento de dispositivos eficiente, registro de gerenciamento automático de dispositivos móveis e capacidade de logon único para o Azure AD e recursos locais.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Quais recursos o Ingresso no Azure AD oferece?
Com a junção do Azure AD, você obtém seguinte hello:

* **O provisionamento de dispositivos corporativos**: com o Windows 10, os usuários podem configurar um dispositivo novo, têm embalagem na experiência de out-of-box hello, sem o envolvimento de TI.
* **Suporte para formatos modernos**: ingresso no Azure AD funciona em dispositivos que não têm domínio tradicional Olá ingressar recursos.  
* **Suporte para contas organizacionais existentes**: os usuários são mais necessários toocreate e manter um um tooget de conta pessoal do Microsoft hello melhor experiência em dispositivos da empresa emitido, como ocorria com o Windows 8. Em vez disso, eles podem usar suas contas corporativas existentes no Azure AD. Para muitas organizações, isso significa basicamente que os usuários podem configurar e entrar tooWindows com hello mesmo credenciais que usam tooaccess Office 365.
* **Registro de gerenciamento de dispositivo móvel automática**: dispositivos podem ser registrados automaticamente no gerenciamento de dispositivo móvel quando conectado tooAzure AD. Esse processo funciona com o Microsoft Intune e as soluções de gerenciamento de dispositivos móveis de parceiros. Quando o gerenciamento de dispositivos é feito com o Intune, os administradores de TI podem monitorar/gerenciar dispositivos que ingressaram no AD do Azure junto com dispositivos de domínio no console de gerenciamento do SCCM hello.
* **Um único logon toocompany recursos**: usuários aproveitam o logon único do tooapps área de trabalho do Windows hello e recursos na nuvem hello, como Office 365 e milhares de aplicativos de negócios que dependem do AD do Azure para autenticação por meio de [Do azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Dispositivos corporativos que são unida tooAzure AD também aproveitar recursos de locais de tooon SSO quando dispositivo hello está em uma rede corporativa e de qualquer lugar, quando esses recursos são expostos por meio de saudação [Proxy de aplicativo do Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Roaming de estado do sistema operacional**: configurações de acessibilidade, sites, senhas de Wi-Fi e outras configurações são sincronizados entre dispositivos corporativos sem a necessidade de uma conta da Microsoft pessoal.
* **Pronto para empresas Windows Store**: Olá da Windows Store dá suporte a aquisição de aplicativo e licenciamento com contas do AD do Azure. As organizações podem aplicativos de licença de volume e torná-los disponíveis toohello usuários em sua organização.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Como diferentes dispositivos funcionam com o Ingresso no Azure AD?
| Dispositivo corporativo (domínio local tooon unida) | Dispositivo corporativo (toohello unidas nuvem) | Dispositivo pessoal |
| --- | --- | --- |
| Os usuários podem entrar no Windows com credenciais corporativas (como fazem hoje) |Os usuários podem entrar no tooWindows com as credenciais de trabalho que são gerenciadas no AD do Azure. Isso é relevante para dispositivos corporativos em três casos: <ol><li>organização de saudação não tiver o Active Directory no local (por exemplo, uma pequena empresa).</li><li>organização de saudação não cria todas as contas de usuário no Active Directory (por exemplo, contas de alunos, consultores ou sazonais trabalhadores não são criadas no Active Directory).</li><li>organização de saudação tem todos os dispositivos que não podem ser domínio associado tooan (local), como telefones ou tablets que executam uma SKU móvel (por exemplo, um chão de fábrica/varejo dispositivo secundário tomado tooa).</li></ol> O Ingresso do Azure AD dá suporte ao ingresso de dispositivos corporativos para organizações gerenciadas e federadas. |Os usuários entram no tooWindows com suas credenciais de conta da Microsoft pessoais (sem alteração). |
| Os usuários têm acesso tooroaming configurações e enterprise Olá da Windows Store. Esses serviços funcionam com contas corporativas e não exigem uma conta da Microsoft pessoal. Isso exige que as organizações tooconnect seu tooAzure do Active Directory local AD. |Os usuários podem fazer a instalação de autoatendimento. Eles poderão acessar por meio de experiência de primeira execução da saudação (FRX) por meio de sua conta de trabalho como uma alternativa toohaving IT provisionar Olá dispositivos, embora os dois métodos têm suporte. |Os usuários podem adicionar facilmente uma conta corporativa que é gerenciada no Active Directory ou no Azure AD. |
| Os usuários têm a capacidade SSO de aplicativos de área de trabalho toowork hello, sites e recursos--incluindo recursos locais e aplicativos de nuvem que usam o AD do Azure para autenticação. |Dispositivos são registrados automaticamente no diretório de empresa hello (AD do Azure) e automaticamente registrados no gerenciamento de dispositivos móveis. (Recurso do Azure AD Premium). |Os usuários têm a capacidade SSO entre aplicativos e toowebsites/recursos com esta conta corporativa. |
| Os usuários podem adicionar seus tooaccess de contas pessoais Microsoft seus arquivos e imagens pessoais sem afetar os dados da empresa. (Configurações de roaming continuam toowork com suas contas de trabalho.) Olá conta da Microsoft permite SSO e não mais unidades Olá roaming de configurações. |Os usuários podem executar uma SSPR (redefinição de senha de autoatendimento) no winlogon, o que significa que podem redefinir uma senha esquecida. (Recurso do Azure AD Premium). |Os usuários têm acesso toohello enterprise Windows Store para que eles podem adquirir e usar aplicativos de linha de negócios em seus dispositivos pessoais. |

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

