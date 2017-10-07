---
title: aaaAuthenticating identidades sem senhas com o Windows Hello for Business e AD do Azure | Microsoft Docs
description: "Fornece uma visão geral do Windows Hello for Business e informações adicionais sobre como implantar o Windows Hello for Business."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Autenticação de identidades sem senhas com o Windows Hello for Business
métodos de atual Olá de autenticação com somente senhas não são suficientes usuários tookeep seguros. Os usuários reutilizar e esquecem senhas. As senhas são breachable, phishable, sujeito a toocracks e fácil de adivinhar. Também obtêm tooremember difícil e propensas tooattacks, como "[passar o hash de saudação](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>Sobre o Hello for Business
O Windows Hello for Business é uma abordagem de autenticação com chave privada/pública ou baseada em certificados para empresas e consumidores que vai além de senhas. Essa forma de autenticação se baseia nas credenciais de par de chaves que podem substituir senhas e toobreaches são resistentes, thefts e phishing.

 Windows Hello para empresas permite ao usuário autenticar a conta da Microsoft tooa, uma conta do Active Directory do Windows Server, uma conta do Microsoft Azure Active Directory (AD do Azure) ou um serviço de terceiros que oferece suporte à autenticação rápido identidade Online (FIDO). Após uma verificação inicial em duas etapas durante a saudação do Windows para o registro de negócios, Windows Hello para empresas está configurado no dispositivo do usuário hello e usuário Olá define um gesto, que pode ser o Windows Hello ou um PIN. saudação de usuário fornece Olá gesto tooverify sua identidade. O Windows, em seguida, usa o Windows Hello para comercial tooauthenticate saudação do usuário e ajudá-los a serviços e recursos de tooaccess protegido.

chave privada Olá é disponibilizado apenas por meio de um "gesto do usuário" como um PIN, biometria ou um dispositivo remoto como um cartão inteligente que Olá usuário usa toosign toohello dispositivo. Essas informações são vinculados tooa certificado ou um par de chaves assimétrico. chave privada Olá é hardware attested se o dispositivo de saudação tem um chip Trusted Platform Module (TPM). chave privada Olá nunca deixa o dispositivo hello.

chave pública Hello está registrado no Active Directory do Azure e o Windows Server Active Directory (para local). Provedores de identidade (IDPs) Validar usuário Olá por chave pública de saudação mapeamento da chave privada do hello usuário toohello e fornecem informações de logon por meio de um tempo OTP (senha), PhoneFactor ou um mecanismo de notificação diferente.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Por que as empresas devem adotar o Windows Hello for Business
Ao habilitarem o Windows Hello for Business, as empresas podem tornar seus recursos ainda mais seguros ao:

* Configuração do Windows Hello for Business com uma opção preferencial de hardware. Isso significa que as chaves serão geradas no TPM 1.2 ou 2.0, quando estiverem disponíveis. Quando o TPM não estiver disponível, o software irá gerar chave hello.
* Comprimento de saudação e a complexidade de saudação definindo FIXAR, e se o uso de saudação está habilitado em sua organização.
* Configuração do Windows Hello para cenários de cartão inteligente como toosupport comerciais por meio de confiança com base em certificado.

## <a name="how-windows-hello-for-business-works"></a>Como o Windows Hello for Business funciona
1. As chaves são geradas no hardware Olá por um TPM ou software. Muitos dispositivos possuem um chip TPM interno que protege o hardware Olá integrando as chaves de criptografia em dispositivos. TPM 1.2 ou 2.0 gera chaves ou certificados que são criados a partir de chaves Olá gerado.
2. Olá TPM atesta essas chaves de hardware associado.
3. Um gesto de desbloqueio único desbloqueia dispositivo hello. Esse gesto permite acessar os recursos toomultiple se dispositivo Olá é ingressado no domínio ou do Azure ingressados no AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Como funciona o hello Windows Hello para o ciclo de vida de negócios
![Ciclo de vida do Windows Hello for Business](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Olá diagrama anterior ilustra par de chaves Olá privada/pública e a validação de saudação pelo provedor de identidade hello. Cada uma dessas etapas é explicada detalhadamente a seguir:

1. Olá usuário comprove sua identidade por meio de vários métodos internos de verificação (gestos, cartões inteligentes físicos, autenticação multifator) e envia essa tooan informações provedor de identidade (IDP) como o Azure Active Directory ou do Active Directory local.
2. dispositivo Olá, em seguida, cria a chave de saudação, atesta chave hello, usa a parte pública Olá dessa chave, anexa-o com as instruções de estação, entra em e envia a chave de saudação tooregister toohello IDP.
3. Como Olá IDP registra a parte pública de saudação da chave de hello, desafios de IDP Olá Olá toosign de dispositivo com parte da chave de saudação privada hello.
4. Olá IDP, em seguida, valida e problemas Olá token de autenticação que permite que o usuário hello e recursos de saudação protegido de acesso de dispositivo de saudação. IDPs pode gravar aplicativos de plataforma cruzada ou usar toocreate de suporte (por meio de APIs de JavaScript/Webcrypto) do navegador e usar o Windows Hello para credenciais de negócios para seus usuários.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Olá requisitos de implantação do Windows Hello para empresas
### <a name="at-hello-enterprise-level"></a>No nível de empresa Olá
* enterprise Olá tem uma assinatura do Azure.

### <a name="at-hello-user-level"></a>No nível de usuário Olá
* computador do usuário Olá executa o Windows 10 Professional ou Enterprise.

Para obter instruções detalhadas de implantação, consulte [habilitar Windows Hello para empresas na organização Olá](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

