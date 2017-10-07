---
title: "aaaChoose uma solução de identidade híbrida do Azure | Microsoft Docs"
description: "Obter um entendimento básico de soluções de identidade híbridas disponíveis hello e recomendações para você toomake Olá melhor identidade governança decisão para sua organização."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Soluções de identidade híbrida da Microsoft
[Microsoft Azure Active Directory (AD do Azure)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) soluções de identidade híbrida habilitar toosynchronize objetos de diretório local com o Azure AD enquanto ainda gerencia seus usuários locais. Olá primeiro decisão toomake ao planejar toosynchronize seu local no Windows Server Active Directory com o Azure AD é se você quer toouse sincronizado identidade ou identidade federada. Identidades sincronizadas e, opcionalmente, hashes de senha, permitem que os usuários toouse Olá mesmo tooaccess de senha local e baseado em nuvem recursos organizacionais. Para requisitos do cenário mais avançados, como logon único (SSO) ou MFA local, você precisa de identidades de toofederate toodeploy os serviços de Federação do Active Directory (AD FS). 

Há várias opções disponíveis para a configuração de identidade híbrida. Este artigo fornece informações toohelp que escolha Olá uma melhor para sua organização com base em facilidade de implantação e o gerenciamento de identidades e acesso específico precisa. Ao considerar qual modelo de identidade melhor atenda às necessidades de sua organização, você também precisa toothink sobre o tempo, a infraestrutura existente, a complexidade e custo. Esses fatores são diferentes para cada organização e podem mudar ao longo do tempo. No entanto, se alterar seus requisitos, você também tem o modelo de identidade diferente do hello flexibilidade tooswitch tooa.

> [!TIP]
> Essas soluções são todas entregues pelo [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Identidade sincronizada 
Identidade sincronizada é Olá toosynchronize de maneira mais simples de objetos de diretório (usuários e grupos) no local com o Azure AD. 

![Identidade híbrida sincronizada](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Enquanto identidade sincronizada é o método mais fácil e rápido de hello, os usuários ainda precisam toomaintain uma senha separada para os recursos baseados em nuvem. tooavoid isso, você também pode (opcionalmente) [sincronizar um hash das senhas dos usuários](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) directory tooyour AD do Azure. Sincronização de senha hashes permite que os usuários toolog nos recursos organizacionais com base em toocloud com hello o mesmo nome de usuário e senha que eles usam no local. O Azure AD Connect verifica periodicamente seu diretório local quanto a alterações e mantém seu diretório do Azure AD sincronizado. Quando um atributo de usuário ou senha é alterado no Active Directory local, ele é automaticamente atualizado no Azure AD. 

Para a maioria das organizações que precisam apenas tooenable toosign seus usuários em tooOffice 365, aplicativos SaaS e outros recursos do Azure baseado no AD, opção de sincronização de senha saudação padrão é recomendada. Se isso não funcionar para você, você precisará toodecide entre autenticação de passagem e o AD FS.

> [!TIP]
> As senhas de usuário são armazenadas no local no Windows Server Active Directory na forma de saudação de um valor de hash que representa a senha de usuário real hello. Um valor de hash é um resultado de uma função matemática unidirecional (Olá algoritmo de hash). Não há nenhum resultado do método toorevert saudação de uma versão de texto sem formatação toohello função unidirecional de uma senha. Você não pode usar um toosign de hash de senha na rede de local de tooyour. Quando você optar por toosynchronize senhas, hashes de senha do Azure AD Connect extrai de saudação do Active Directory local e se aplica segurança extra processamento toohello hash de senha antes que seja sincronizado tooAzure AD. Sincronização de senha também pode ser usada junto com a senha tooenable de write-back de autoatendimento redefinição de senha no AD do Azure. Além disso, você pode habilitar logon único (SSO) para os usuários nos computadores de domínio que são a rede corporativa toohello conectado. Com o logon único, habilitado os usuários só precisam tooenter uma toosecurely de nome de usuário acesse recursos de nuvem. 

## <a name="pass-through-authentication"></a>Autenticação de passagem
A [Autenticação de passagem do Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) fornece uma solução de validação de senha simples para serviços baseados no Azure AD usando o Active Directory local. Se as políticas de conformidade e segurança para a sua organização não permitem enviar as senhas dos usuários, mesmo em um formulário de hash, e você só precisa de área de trabalho toosupport SSO para dispositivos ingressados no domínio, é recomendável que você avalie usando a autenticação de passagem. Autenticação de passagem não exige qualquer implantação no hello rede de Perímetro, que simplifica a infraestrutura de implantação hello quando comparado com o AD FS. Quando os usuários entram usando o Azure AD, esse método de autenticação valida as senhas dos usuários diretamente no seu Active Directory local.

![Autenticação de passagem](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Com a autenticação de passagem, não é necessário para uma infraestrutura de rede complexa e não é necessário toostore senhas de locais na nuvem hello. Combinado com o logon único, autenticação de passagem fornece uma experiência totalmente integrada ao entrar tooAzure AD ou outros serviços em nuvem.

A autenticação de passagem é configurada por meio do Azure AD Connect, que utiliza um agente local simples que escuta solicitações de validação de senha. Agente de saudação pode ser implantado facilmente toomultiple máquinas tooprovide alta disponibilidade e balanceamento de carga. Desde que todas as comunicações são somente saídas, não há nenhum requisito para Olá conector toobe instalado na rede de Perímetro. requisitos de computador do servidor de saudação para conector de saudação são da seguinte maneira:

- Windows Server 2012 R2 ou posterior
- Ingressado tooa domínio na floresta Olá por meio do qual os usuários são validados

> [!NOTE]
> A autenticação de passagem do Azure AD está na versão prévia no momento e tem suporte para clientes baseados em navegador da Web e clientes do Office que dão suporte à autenticação moderna. Para clientes que não têm suporte, como herdado clientes do Office e do Exchange ActiveSync (incluindo clientes de email nativos em dispositivos móveis), ele é recomendado toouse Olá autenticação moderna equivalente. Autenticação moderna não só permite a autenticação de passagem, mas também permite toobe de políticas de acesso condicional aplicado, como autenticação multifator. 

Autenticação de passagem não é suportada atualmente quando usando dispositivos Windows 10 associadas tooAzure AD. No entanto, você pode usar a sincronização de hash de senha como um toosupport fallback automático Windows 10 e clientes herdados de saudação mencionado anteriormente. Durante a visualização de hello, sincronização de hash de senha é habilitada por padrão quando a autenticação de passagem é selecionada como Olá opção de entrada no Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Identidade federada (AD FS)
Para obter mais controle sobre como os usuários acessam o Office 365 e outros serviços de nuvem, você pode configurar a sincronização de diretórios com SSO (logon único) usando os [Serviços de Federação do Active Directory (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Federação entradas do usuário com o AD FS delegados autenticação tooan no servidor local que valida as credenciais do usuário. Nesse modelo, as credenciais do Active Directory local nunca são transmitidas tooAzure AD.

![Identidade federada](./media/choose-hybrid-identity-solution/federated-identity.png)

Também chamado federação de identidade, esse método garante que todas as autenticações de usuário são controlado no local e permite que os administradores tooimplement níveis mais rigorosos de controle de acesso. Federação de identidade com o AD FS é a opção hello mais complicado e exige a implantação de servidores adicionais no seu ambiente local. Federação de identidade também confirma suporte tooproviding 24x7 para sua infraestrutura do Active Directory e o AD FS. Esse nível alto de suporte é necessário porque se acessar o local da Internet, controlador de domínio ou servidores do AD FS não estão disponíveis, os usuários não é possível entrar nos serviços de toocloud.

> [!TIP]
> Se você decidir toouse federação com os serviços de Federação do Active Directory (AD FS), você pode definir opcionalmente a sincronização de senha como um backup no caso de falha de infraestrutura do AD FS.


## <a name="common-scenarios-and-recommendations"></a>Cenários e recomendações comuns
Aqui estão alguns identidade híbrida comuns e cenários de gerenciamento de acesso com recomendações como opção de identidade híbrida toowhich (ou opções) podem ser apropriados para cada um.

|Eu preciso de:|PWS e SSO<sup>1</sup>| PTA e SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Sincronizar um novo usuário, contato e contas de grupo criadas automaticamente no meu nuvem de toohello do Active Directory local.|![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Configurar meu locatário para cenários híbridos do Office 365|![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Habilitar toosign meus usuários no e acessar os serviços de nuvem usando suas senhas locais|![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Implementar o logon único usando credenciais corporativas|![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Certifique-se de que nenhum hashes de senha são armazenados na nuvem Olá| |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Habilitar soluções de autenticação multifator locais| | |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Suporte à autenticação de cartão inteligente para meus usuários<sup>4</sup>| | |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|
|Exibir notificações de expiração de senha em Olá Portal do Office e na área de trabalho Olá Windows 10| | |![Recomendadas](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Sincronização de senha com logon único. 

> <sup>2</sup> Autenticação de passagem e Logon único. 

> <sup>3</sup> Logon único federado com o AD FS.

> <sup>4</sup> do AD FS pode ser integrado ao seu tooallow PKI corporativa usando certificados. Esses certificados podem ser certificados suaves implantados por meio dos canais de provisionamento confiáveis como certificados de cartão inteligente (incluindo cartões PIV/CAC), MDM, GPO ou Hello for Business (certificado confiável). Para obter mais informações sobre o suporte à autenticação de cartão inteligente, consulte [este blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Próximas etapas
[Saiba mais em um ambiente de prova de conceito do Azure](https://aka.ms/aad-poc)

[Instalar o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[Monitorar a sincronização de identidade híbrida](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

