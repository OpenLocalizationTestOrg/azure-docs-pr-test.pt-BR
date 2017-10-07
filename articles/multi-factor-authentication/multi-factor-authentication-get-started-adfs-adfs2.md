---
title: aaaUse servidor Azure MFA com AD FS 2.0 | Microsoft Docs
description: "Esta é hello Azure multi-Factor authentication página que descreve como tooget iniciada com o Azure MFA e AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Configurar o servidor Azure multi-Factor Authentication toowork com o AD FS 2.0
Este artigo é para organizações que estão agrupadas com o Active Directory do Azure e deseja toosecure recursos que estão no local ou na nuvem hello. Proteger seus recursos, usando Olá servidor Azure multi-Factor Authentication e configurá-lo toowork com o AD FS para que a verificação em duas etapas é disparada para pontos de extremidade de alto valor.

Esta documentação aborda usando Olá servidor Azure multi-Factor Authentication com o AD FS 2.0. Para saber mais sobre o AD FS, veja [Proteger recursos de nuvem e locais usando o Servidor de Autenticação Multifator do Azure com o Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Proteger o AD FS 2.0 com um proxy
toosecure do AD FS 2.0 com um proxy, instale Olá servidor Azure multi-Factor Authentication no servidor de proxy Olá AD FS.

### <a name="configure-iis-authentication"></a>Configurar a autenticação IIS
1. No hello servidor Azure multi-Factor Authentication, clique em Olá **autenticação IIS** ícone no menu esquerdo hello.
2. Clique em Olá **baseado em formulário** guia.
3. Clique em **Adicionar**.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. variáveis de nome de usuário, senha e domínio toodetect automaticamente, insira o URL de logon hello (como https://sso.contoso.com/adfs/ls) na caixa de diálogo Configurar automaticamente site Olá e clique em **Okey**.
5. Verificar Olá **correspondência de usuários exigir Azure multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e verificação de etapa tootwo de assunto. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da verificação em duas etapas, marque caixa hello.
6. Se as variáveis de página de saudação não podem ser detectadas automaticamente, clique em Olá **especificar manualmente...** botão na caixa de diálogo Configurar automaticamente site hello.
7. Na caixa de diálogo Adicionar site hello, insira a página de logon do hello URL toohello AD FS no campo de URL de envio de saudação (como https://sso.contoso.com/adfs/ls) e insira um nome de aplicativo (opcional). nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.
8. Defina o formato da solicitação de saudação muito**POST ou GET**.
9. Insira a variável de nome de usuário de saudação (ctl00$ ContentPlaceHolder1$ UsernameTextBox) e senha (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Se a página de logon baseada em formulário exibe uma caixa de texto de domínio, insira Olá domínio variável também. nomes de saudação toofind das caixas de entrada hello na página de logon hello, vá toohello a página de logon em um navegador da web, clique com o botão direito na página hello e selecione **Exibir código-fonte**.
10. Verificar Olá **correspondência de usuários exigir Azure multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e verificação de etapa tootwo de assunto. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da verificação em duas etapas, marque caixa hello.
    <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Clique em **Avançado...** tooreview configurações avançada. As configurações que você pode definir incluem:

    - Selecionar um arquivo de página de negação personalizado
    - Site de toohello as autenticações bem-sucedidas de cache usando cookies
    - Selecione como tooauthenticate Olá credenciais primárias

12. Desde que o servidor de proxy Olá AD FS não é provavelmente toobe ingressados no domínio toohello, você pode usar o controlador de domínio do LDAP tooconnect tooyour para pré-autenticação e importação de usuário. Na caixa de diálogo site baseado hello, clique em Olá **autenticação primária** guia e selecione **LDAP Bind** para Olá pré-autenticação do tipo.
13. Ao concluir, clique em **Okey** caixa de diálogo de Adicionar site tooreturn toohello.
14. Clique em **Okey** tooclose caixa de diálogo de saudação.
15. Uma vez Olá URL e variáveis de página forem detectadas ou inseridas e dados do site de saudação é exibido no hello painel baseado em formulário.
16. Clique em Olá **módulo nativo** guia e selecione servidor hello, site de saudação do proxy Olá AD FS em execução em (como "Default Web Site"), ou Olá do AD FS proxy aplicativo (como "ls" em "adfs") tooenable Olá plug-in no hello IIS nível desejado.
17. Clique em Olá **autenticação IIS habilitar** caixa na parte superior de saudação da tela hello.

autenticação do IIS Olá agora está habilitada.

### <a name="configure-directory-integration"></a>Configurar a integração de diretório
Você habilitou a autenticação do IIS, mas tooperform Olá pré-autenticação tooyour Active Directory (AD) via LDAP, você deve configurar Olá controlador de domínio de toohello de conexão LDAP.

1. Clique em Olá **integração de diretórios** ícone.
2. Na guia Configurações de saudação, selecione Olá **usar configuração LDAP específica** botão de opção.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Clique em **Editar**.
4. Na caixa de diálogo Editar configuração de LDAP hello, preencha os campos de saudação com o controlador de domínio do hello informações necessárias tooconnect toohello AD. Descrições dos campos de saudação são incluídas no arquivo de Ajuda do servidor Azure multi-Factor Authentication hello.
5. Testar conexão de LDAP Olá clicando Olá **teste** botão.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Se o teste de conexão LDAP Olá foi bem-sucedido, clique em **Okey**.

### <a name="configure-company-settings"></a>Definir configurações da empresa
1. Em seguida, clique em Olá **configurações da empresa** ícone e selecione Olá **resolução de nome de usuário** guia.
2. Selecione Olá **atributo de identificador exclusivo de usar LDAP para correspondência de nomes de usuário** botão de opção.
3. Se os usuários inserirem seu nome de usuário no formato "domínio \ nome_de_usuário", Olá servidor precisa de domínio de saudação toobe toostrip capaz de logoff nomedeusuário hello quando ele cria a consulta LDAP de saudação. Isso pode ser feito por meio de uma configuração do registro.
4. Abra o editor do registro hello e vá tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive redes/PhoneFactor em um servidor de 64 bits. Se estiver em um servidor de 32 bits, levar hello "Wow6432Node" fora do caminho de saudação. Crie um DWORD chave do Registro chamada "UsernameCxz_stripPrefixDomain" e defina Olá too1 de valor. O Azure multi-Factor Authentication está agora protegendo proxy de saudação do AD FS.

Certifique-se de que os usuários foram importados do Active Directory no servidor de saudação. Consulte Olá [seção IPs confiáveis](#trusted-ips) se você deseja que toowhitelist endereços IP internos para que a verificação em duas etapas não é necessária ao entrar no site toohello desses locais.

<center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct sem um proxy
Você pode proteger o AD FS quando Olá AD FS proxy não for usado. Instalar Olá servidor Azure multi-Factor Authentication no servidor de saudação do AD FS e configurar Olá servidor por Olá seguindo as etapas:

1. Dentro de Olá servidor Azure multi-Factor Authentication, clique em Olá **autenticação IIS** ícone no menu esquerdo hello.
2. Clique em Olá **HTTP** guia.
3. Clique em **Adicionar**.
4. Na caixa de diálogo Adicionar URL Base hello, insira o URL de Olá Olá site do AD FS onde a autenticação HTTP é executada (como https://sso.domain.com/adfs/ls/auth/integrated) no campo URL Base de saudação. Em seguida, insira um nome de aplicativo (opcional). nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.
5. Se desejar, ajuste o tempo limite de ociosidade hello e máximo horas de sessão.
6. Verificar Olá **correspondência de usuários exigir Azure multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e verificação de etapa tootwo de assunto. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou estará isento da verificação em duas etapas, marque caixa hello.
7. Marque a caixa de cache de cookie de saudação se desejado.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Clique em **OK**.
9. Clique em Olá **módulo nativo** guia e selecione Olá servidor, Olá site (como "Default Web Site") ou Olá do AD FS aplicativo (como "ls" em "adfs") tooenable Olá IIS plug-in no hello desejado nível.
10. Clique em Olá **autenticação IIS habilitar** caixa na parte superior de saudação da tela hello.

Agora a Autenticação Multifator do Azure está protegendo o ADFS.

Certifique-se de que os usuários foram importados do Active Directory no servidor de saudação. Consulte Olá IPs confiáveis seção se você deseja que o endereço IP interno toowhitelist endereços para que a verificação em duas etapas não é necessária ao entrar no site toohello desses locais.

## <a name="trusted-ips"></a>IPs confiáveis
IPs confiáveis permitem que os usuários toobypass Azure multi-Factor Authentication para solicitações de sites provenientes de específico de endereços IP ou sub-redes. Por exemplo, convém tooexempt usuários de verificação em duas etapas quando eles entrarem no departamento de saudação. Para isso, você deve especificar a sub-rede de escritório hello como uma entrada de IPs confiáveis.

### <a name="tooconfigure-trusted-ips"></a>IPs confiáveis de tooconfigure
1. Na seção autenticação IIS do hello, clique em Olá **IPs confiáveis** guia.
2. Clique em Olá **adicionar...** .
3. Quando for exibida a caixa de diálogo Adicionar IPs confiáveis hello, selecione uma das Olá **IP único**, **intervalo IP**, ou **sub-rede** botões de opção.
4. Insira o endereço IP hello, intervalo de endereços IP ou sub-rede que deve estar na lista de permissões. Se inserir uma subrede, selecione Olá Olá apropriado de máscara de rede e clique em **Okey** botão. Olá confiável que IP agora foi adicionado.

<center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
