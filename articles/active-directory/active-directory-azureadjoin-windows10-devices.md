---
title: dispositivos aaaUsing Windows 10 em seu local de trabalho | Microsoft Docs
description: "Fornece um instantâneo de recursos para usuários e equipe de TI, contrastantes maneiras diferentes de saudação um dispositivo pode ser configurado e usado em uma empresa com o Windows 10."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Usando dispositivos com Windows 10 no local de trabalho
Aplica-se a: PCs com Windows 10

Windows 10 oferece três modelos para organizações que permitem que os usuários tooaccess os recursos de trabalho de forma segura e conveniente.

* **Azure junção do Active Directory** (junção do Azure AD), para os funcionários que acessam recursos como o Office 365 principalmente na nuvem de saudação. O Ingresso no Azure AD é uma experiência de provisionamento de trabalho de autoatendimento no Windows 10.
* **Ingresso no domínio**, para organizações com investimentos em aplicativos e recursos locais. Ingresso no domínio oferece uma experiência aprimorada no Windows 10 quando conectado tooAzure AD.
* **Uma nova experiência BYOD de simplificado**, para que os usuários que desejam tooadd um trabalho ou contam escolar tooWindows e acessar facilmente os recursos em dispositivos pessoais.

Olá tabela a seguir apresenta um instantâneo dos recursos para usuários e administradores de TI, contrastantes maneiras diferentes de saudação um dispositivo pode ser configurado e usado em uma empresa com o Windows 10:

|  | Ingresso no domínio | Ingresso no AD do Azure | Dispositivo pessoal |
| --- | --- | --- | --- |
| Entrada em dispositivo com o Windows para contas corporativas ou de estudante. |Sim |Sim |Não |
| Usuário single-sign-on (SSO) tooOffice 365 e aplicativos do AD do Azure. SSO é Olá capacidade toosign em apenas uma vez tooaccess recursos organizacionais. |Sim |Sim |Sim |
| Aplicativos de tooKerberos/NTLM de SSO de usuário. |Sim |Limitado |Sim, via VPN |
| Autorização forte e entrada conveniente para a conta corporativa ou de estudante com o Microsoft Passport e o Windows Hello. |Sim |Sim |Sim |
| Acesse tooenterprise Windows Store com uma conta corporativa ou escolar (não uma conta da Microsoft). |Sim |Sim |Sim |
| Roaming de configurações de usuário entre dispositivos em conformidade com a empresa usando contas corporativas ou de estudante. |Sim |Sim |Sim |
| Olá capacidade toorestrict acesso tooorganizational aplicativos toodevices que são compatíveis com políticas de dispositivo organizacional. |Sim |Sim |Sim |
| Provisionamento de autoatendimento pelo usuário de dispositivos para o "trabalho em qualquer lugar". |Não |Sim |Sim |
| Dispositivos de toomanage de capacidade. |Sim, via GP/SCCM |Sim |Sim |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Usar dispositivos corporativos com Ingresso no Azure AD e ingresso no domínio no Windows 10
Windows 10 oferece recursos de trabalho do trabalho dispositivos tooaccess de duas maneiras:

* Ingresso no AD do Azure
* Ingresso no domínio
  
  Ambos podem ser opções válidas, dependendo das necessidades e dos requisitos de uma organização. Em alguns casos, as organizações podem se beneficiar habilitando os dois métodos de implantação.

## <a name="when-toouse-azure-active-directory-join"></a>Quando toouse Active Directory do Azure Join
O ingresso no AD do Azure é uma nova experiência de provisionamento de autoatendimento no Windows 10.  Ele se destina a funcionários que acessam os recursos de trabalho como o Office 365 principalmente na nuvem hello. É uma maneira simples de tooconfigure computadores, tablets e telefones para a empresa hello. Os dispositivos são gerenciados por meio do gerenciamento de dispositivo móvel, usando controles consistentes em plataformas Windows.

**Use o ingresso no Azure AD por qualquer um destes motivos**:

* Você deseja tooenable Olá provisionamento de autoatendimento de dispositivos para os operadores de saudação ir.
* Você fornece aos usuários dispositivos móveis corporativos, como tablets e telefones.
* Você deseja toomanage um conjunto de usuários no AD do Azure, em vez de no Active Directory, como sazonais funcionários, prestadores de serviço ou os alunos.
* Você deseja tooprovide junção recursos tooworkers em filiais remotas com a infraestrutura limitada local.
* Você não tem um Active Directory local.

Algumas organizações usará junção do Azure AD como Olá principal maneira toodeploy trabalho dispositivos, especialmente à medida que eles migram a maioria ou todos os seu nuvem toohello de recursos. Organizações híbrido com o Active Directory e o AD do Azure também podem escolher toodeploy um método ou outro dependendo usuário hello ou departamento.

Escolas e universidades, por exemplo, podem gerenciar funcionários no Active Directory e alunos no Azure AD. Algumas empresas podem querer escritórios remotos toomanage ou departamentos de vendas em AD do Azure. O Ingresso no Azure AD e o ingresso no domínio são métodos que podem ser utilizados em uma organização híbrida. Associação de AD do Azure pode ser uma junção de toodomain complemento importante para a implantação de dispositivos em um ambiente de trabalho.

**Se for hello mais comum acessar tooenterprise os recursos por meio da nuvem hello, sua organização pode aproveite os benefícios adicionais se**:

* Você puder remover dependências na infraestrutura de identidade local.
* Você puder simplificar o modelo de implantação de dispositivos afastando-se das soluções de geração de imagens, permitindo a configuração de autoatendimento.
* Você pode usar toomanage de gerenciamento de dispositivo móvel todos os seus dispositivos em plataformas diferentes.

Para obter mais informações sobre a junção do Azure AD, consulte [estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Azure Active Directory](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Quando o domínio toouse join (ou manter o uso)
Para Olá últimos 15 anos, muitas organizações têm usados dispositivos de trabalho de tooconnect de junção de domínio. Isso permite que os usuários toosign em dispositivos de tootheir com seu Active Directory ou de estudante contas. Ingresso no domínio também permite IT toocentrally e totalmente gerenciar esses dispositivos. As organizações normalmente dependem de métodos tooprovision dispositivos de imagem e geralmente usam o System Center Configuration Manager (SCCM) ou a diretiva de grupo (GP) toomanage-los.

**Sua empresa deve usar o ingresso no domínio (ou continuar a usá-o) por qualquer um dos seguintes motivos**:

* Você tem dispositivos Win32 de toothese implantado de aplicativos que usam o Kerberos/NTLM.
* Você requer que os dispositivos toomanage GP ou SCCM/DCM.
* Você deseja que os dispositivos toocontinue tooconfigure soluções, geração de imagens toouse para seus funcionários.

**Ingresso no domínio no Windows 10 também oferece benefícios do seguinte hello quando conectado tooAzure AD**:

* Autenticação forte associada ao dispositivo e entrada conveniente para contas corporativas ou de estudante com o Microsoft Passport e o Windows Hello.
* Acesse toohello empresa da Windows Store para dispositivos que usam o trabalho ou escola contas (nenhuma conta da Microsoft necessários).
* Roaming compatível com a empresa de configurações de usuário entre dispositivos que usam contas corporativas ou de estudante (não é necessária uma conta da Microsoft).
* Olá capacidade toorestrict acesso tooorganizational aplicativos toodevices que são compatíveis com políticas de dispositivo organizacional.

Para obter mais informações sobre a junção do Azure AD, consulte [estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Azure Active Directory](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Habilitar o ingresso de dispositivos pessoais para o trabalho ou a escola
toosupport BYOD empresa hello, Windows 10 fornece Olá usuário Olá capacidade tooadd um trabalho ou computador de tootheir de conta de escola, tablet ou telefone. Depois de saudação usuário adiciona um trabalho ou conta de estudante, dispositivo hello está registrada com o Azure AD e opcionalmente registrada no sistema de gerenciamento do dispositivo móvel Olá Olá organização configurou. diretório Olá exibirão esses dispositivos como 'Registrado' vs. 'Ingressado no AD do Azure'. Os administradores de TI podem aplicar políticas diferentes de acordo com essas informações, oferecendo um toque mais informal em dispositivos pessoais do que em dispositivos corporativos, caso desejem.

Os usuários podem adicionar uma ou escolar dispositivo pessoal do conta tootheir muito conveniente. Eles podem fazer isso ao acessar um aplicativo de trabalho para Olá primeira vez, ou eles podem fazê-lo manualmente por meio do menu de configurações de saudação. Essa conta fornece recursos de tooorganizational SSO.

Para obter mais informações sobre a junção do Azure AD, consulte [conectar dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Habilitar o ingresso no domínio ou o Ingresso no Azure AD
Todos os métodos descritos anteriormente (ingresso no domínio, associação de AD do Azure e adicionar trabalho ou conta escolar) têm pontos de entrada na experiência do usuário Olá Windows 10. No entanto, exigem uma IT tooenable Olá a funcionalidade de administrador na infraestrutura de saudação antes de experiência de saudação funcionará.

## <a name="requirements-for-deploying-azure-ad-join"></a>Requisitos para a implantação do Ingresso no Azure AD
toodeploy junção do Azure AD para qualquer conjunto de usuários, você precisa Olá a seguir:

* Uma assinatura do Azure AD.
* Uma assinatura do Azure AD Premium, como registro automático de gerenciamento de dispositivos móveis, se você precisar de mais recursos.
* Gerenciamento de dispositivo móvel – por exemplo, uma assinatura Microsoft Intune, gerenciamento de dispositivo móvel para Office 365 ou qualquer um de fornecedores gerenciamento de dispositivo móvel de parceiro de saudação que se integram com o AD do Azure. (Consulte Olá [seção de perguntas Frequentes](#frequently-asked-questions) final Olá deste artigo para obter mais informações).

Se suas instalações estiverem híbrido, é altamente recomendado que você implantar o Azure AD Connect tooextend Olá local diretório tooAzure AD.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Requisitos para usar o ingresso no domínio com o Azure AD
Ingresso no domínio continua toowork como sempre tem. No entanto, tooget benefícios de saudação do Azure AD será necessário Olá a seguir:

* Uma assinatura do Azure AD.
* Uma implantação do Azure AD Connect tooextend Olá tooAzure diretório AD no local.
* Uma política que permite que dispositivos que ingressaram no domínio toohave acesso condicional tooAzure AD.
* Uma política que permite acesso muito "" dispositivos de domínio se você desejar toobe toorestrict capaz de acesso para alguns dispositivos.
* System Center Configuration Manager versão 1509 para visualização técnica, tooenable regras para exigir que dispositivos compatíveis. (Consulte hello na documentação do TechNet e postagem de blog).

Para obter mais informações sobre associação de domínio no Windows 10, consulte [conectar dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Requisitos para usar BYOD e "Adicionar uma conta corporativa ou de estudante"
tooenable "traga seu próprio dispositivo" (BYOD) com contas corporativa ou escolar, você precisa seguir hello:

* Uma assinatura do Azure AD.
* Uma assinatura do Azure AD Premium, como registro automático de gerenciamento de dispositivos móveis, se você precisar de mais recursos.

## <a name="requirements-for-using-microsoft-passport"></a>Requisitos para usar o Microsoft Passport
tooenable Microsoft Passport, você precisará seguir hello:

* Uma PKI (infraestrutura de chave pública) para suporte a autenticação baseada em certificado que usa o Microsoft Passport.
* Uma assinatura do Intune para suporte a autenticação baseada em certificado que usa o Microsoft Passport para ingresso para o Ingresso no Azure AD e contas corporativas ou de estudante.
* Versão 1509 para visualização técnica do System Center Configuration Manager (consulte hello na documentação do TechNet e postagem de blog) para suporte a autenticação baseada em certificado que usa o Microsoft Passport para ingresso no domínio.
* Uma política para habilitar o Microsoft Passport na organização hello.

Como uma alternativa toousing uma PKI, você pode habilitar baseada em chave Microsoft Passport fazendo Olá seguinte:

* Implante controladores de domínio do Windows Server 2016 "Visualização de Produção 1" (sem a necessidade de níveis funcionais de domínio ou floresta; vários controladores de domínio para redundância servindo a cada site do Active Directory serão suficientes).
* Defina política tooenable Microsoft Passport na organização hello.

Para saber mais sobre o Microsoft Passport e o Windows Hello no Windows 10, confira <link-to-MS-Passport-and-Windows-Hello-document>.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Quais produtos de gerenciamento de dispositivos móveis de parceiro são integrados ao Azure AD?
Olá seguintes produtos de fornecedor integram com o AD do Azure para registro unificado e acesso condicional no Windows 10:

* AirWatch da VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* Gerenciamento de dispositivos móveis locais SOTI
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>E quanto a Ingressar no local de trabalho no Windows 10?
Ingresso no local foi usado no Windows 8.1 tooenable BYOD. No Windows 10, o BYOD é habilitado usando "Adicionar conta corporativa ou de estudante", conforme explicado anteriormente neste documento. Para organizações que não integram o gerenciamento de dispositivos móveis com o AD do Azure, os usuários podem registrar dispositivo Olá no gerenciamento manualmente por meio de **configurações** > **contas**  >  **Acesso corporativo**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Os usuários podem se conectar a sua conta de domínio Microsoft conta tootheir no Windows 10?
Não no Windows 10. No Windows 8.1, os usuários de dispositivos que ingressaram no domínio foi "conectar" seu tooenable de conta de domínio do Microsoft conta (por exemplo, Hotmail, Live, Outlook, Xbox, etc.) tootheir determinadas experiências como serviços tooLive SSO, uso de saudação da Windows Store e roaming de configurações do usuário em todos os dispositivos. No Windows 10, Olá "conectar" funcionalidade de conta da Microsoft foi descontinuado. usuário Olá pode adicionar uma ou mais contas da Microsoft como serviços de tooconsumer SSO de tooenable de contas adicionais como saudação da Windows Store. Isso é feito em **Configurações** > **Contas** > **Sua conta**.

Os usuários que estão atualizando do Windows 8.1 dispositivos que ingressaram no domínio e que teve sua conta da Microsoft conectado, será automaticamente conectado à conta da Microsoft adicionou toohello lista de contas adicionais, que eles usam.

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

