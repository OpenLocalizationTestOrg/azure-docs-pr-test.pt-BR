---
title: "aaaRADIUS autenticação e o servidor Azure MFA | Microsoft Docs"
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação de autenticação RADIUS e servidor Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Integrar a autenticação RADIUS com o Servidor de Autenticação Multifator do Azure
Use a seção de autenticação RADIUS de saudação do servidor Azure MFA tooenable e configurar a autenticação de RADIUS. RADIUS é um padrão de protocolo tooaccept solicitações de autenticação e tooprocess essas solicitações. Olá servidor Azure multi-Factor Authentication atua como um servidor RADIUS. Insira-o entre o cliente RADIUS (dispositivo de VPN) e o destino de autenticação, que pode ser do Active Directory (AD), um diretório LDAP ou outro tooadd de servidor RADIUS do Azure multi-Factor Authentication. Para o Azure multi-Factor Authentication (MFA) toofunction, configure Olá servidor Azure MFA para que ele possa se comunicar com servidores de saudação do cliente e o destino de autenticação hello. Olá servidor Azure MFA aceita solicitações de um cliente RADIUS, valida as credenciais usando o destino de autenticação hello, adiciona o Azure multi-Factor Authentication e envia uma resposta ao cliente toohello back RADIUS. solicitação de autenticação Olá só terá êxito se autenticação primária hello e hello Azure multi-Factor Authentication for bem-sucedida.

> [!NOTE]
> Olá servidor MFA só oferece suporte a PAP (protocolo de autenticação de senha) e MSCHAPv2 (da Microsoft Challenge Handshake Authentication Protocol) RADIUS protocolos agindo como um servidor RADIUS.  Outros protocolos, como o EAP (protocolo de autenticação extensível), podem ser usados quando o servidor MFA de saudação atua como um servidor RADIUS de tooanother de proxy RADIUS que dá suporte a esse protocolo.
>
> Nessa configuração, tokens OATH e de SMS unidirecionais não funcionam como Olá servidor MFA não é possível iniciar uma resposta de desafio de RADIUS com êxito usando protocolos alternativos.

![Autenticação Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Adicionar um cliente RADIUS
autenticação de RADIUS tooconfigure, Olá instalar servidor Azure multi-Factor Authentication em um servidor Windows. Se você tiver um ambiente do Active Directory, o servidor de saudação deve ser toohello ingressado no domínio dentro da rede de saudação. Use Olá Olá do procedimento tooconfigure servidor Azure multi-Factor Authentication a seguir:

1. No hello servidor Azure multi-Factor Authentication, clique em ícone de autenticação RADIUS Olá no menu esquerdo hello.
2. Verificar Olá **habilitar autenticação RADIUS** caixa de seleção.
3. Na guia de clientes hello, altere hello autenticação e portas de contabilização se Olá serviço Azure MFA RADIUS precisa toolisten solicitações RADIUS em portas não padrão.
4. Clique em **Adicionar**.
5. Insira o endereço IP de saudação do hello dispositivo/servidor que irá autenticar toohello servidor Azure multi-Factor Authentication, um nome de aplicativo (opcional) e um segredo compartilhado.

  nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.

  Olá compartilhada secreta necessidades toobe Olá mesmo em ambos os saudação do servidor Azure multi-Factor Authentication e no dispositivo/servidor.

6. Verificar Olá **correspondência do usuário exigir multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e autenticação de fator de toomulti da entidade. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da verificação em duas etapas, marque caixa hello.
7. Verificar Olá **token OATH de fallback habilitar** caixa se desejar toouse OATH senhas de aplicativos móveis de verificação como um fallback toohello fora de banda telefonema, SMS, ou notificação por push.
8. Clique em **OK**.

Repita as etapas 4 a 8 tooadd quantos clientes RADIUS adicionais conforme necessário.

## <a name="configure-your-radius-client"></a>Configurar o cliente RADIUS

1. Clique em Olá **destino** guia.
2. Se Olá servidor Azure MFA é instalado em um servidor de domínio em um ambiente do Active Directory, selecione o domínio do Windows.
3. Se os usuários devem ser autenticados em um diretório LDAP, selecione **Associação LDAP**.

  ligação LDAP toouse, clique em ícone de integração de diretórios hello e Editar configuração de LDAP Olá na guia Configurações de saudação de forma que hello servidor possa ligar tooyour directory. Instruções para configurar o LDAP podem ser encontradas no hello [guia de configuração de Proxy de LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Se os usuários forem autenticados em outro servidor RADIUS, selecione servidores RADIUS.
5. Clique em **adicionar** solicitações tooconfigure Olá toowhich Olá servidor Azure MFA será proxy saudação do servidor RADIUS.
6. Na caixa de diálogo Adicionar servidor RADIUS Olá, insira o endereço IP de saudação do servidor RADIUS de saudação e um segredo compartilhado.

  Olá compartilhada secreta necessidades toobe Olá mesmo em ambos os saudação do servidor Azure multi-Factor Authentication e o servidor RADIUS. Alterar a porta de autenticação hello e porta de contabilização se portas diferentes são usadas pelo servidor RADIUS de saudação.

7. Clique em **OK**.
8. Adicione Olá servidor Azure MFA como um cliente RADIUS no hello outro servidor RADIUS para que ele possa processar solicitações de acesso enviadas tooit de saudação servidor Azure MFA. Use Olá que mesmo compartilhado configurado no servidor Azure multi-Factor Authentication de saudação do segredo.

Repita essas etapas tooadd mais servidores RADIUS e configurar Olá ordem na qual Olá servidor Azure MFA deve chamá-los com hello **mover para cima** e **mover para baixo** botões.

Isso conclui a configuração do servidor Azure multi-Factor Authentication hello. Olá servidor agora está escutando nas portas de saudação configurada para solicitações de acesso RADIUS dos clientes de saudação configurado.   

## <a name="radius-client-configuration"></a>Configuração do cliente RADIUS
Olá tooconfigure cliente RADIUS, use as diretrizes de saudação:

* Configure seu tooauthenticate dispositivo/servidor por meio do endereço IP do servidor de autenticação multifator do Azure RADIUS toohello, o que irá agir como servidor RADIUS de saudação.
* Use Olá que mesmo compartilhado segredo que foi configurado anteriormente.
* Configurar o tempo limite too30-60 segundos do hello RADIUS para que haja tempo toovalidate Olá as credenciais de usuário, executar a verificação em duas etapas, receber a resposta e, em seguida, responder a solicitação de acesso RADIUS toohello.
