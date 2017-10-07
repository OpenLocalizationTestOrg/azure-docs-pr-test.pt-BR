---
title: recursos de nuvem aaaSecure com o Azure MFA e AD FS | Microsoft Docs
description: "Esta é hello Azure multi-Factor authentication página que descreve como tooget iniciada com o Azure MFA e AD FS na nuvem hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Protegendo os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS
Se sua organização for federada com o Active Directory do Azure, use o Azure multi-Factor Authentication ou os recursos de toosecure os serviços de Federação do Active Directory (AD FS) que são acessados pelo AD do Azure. Saudação de usar recursos do Active Directory do Azure procedimentos toosecure com autenticação multifator do Azure ou os serviços de Federação do Active Directory a seguir.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteger recursos do Azure AD usando o AD FS
toosecure seu recurso de nuvem, configurar uma regra de declarações para que os serviços de Federação do Active Directory emite a declaração de multipleauthn hello quando um usuário executa a verificação em duas etapas com êxito. Esta declaração é passada no tooAzure AD. Siga este toowalk procedimento etapas hello:


1. Abra o gerenciamento do AD FS.
2. Olá esquerda, selecione **terceira parte confiável**.
3. Clique com o botão direito do mouse na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Declaração**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **passar ou filtrar uma declaração de entrada** de Olá suspensa e clique em **próximo**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Dê um nome para a regra. 
7. Selecione **referências de métodos de autenticação** como Olá entrada o tipo de declaração.
8. Selecione **Passar todos os valores de declaração**.
    ![Assistente para Adicionar Regra de Declaração de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Clique em **Concluir**. Feche o console de gerenciamento FS Olá AD.

## <a name="trusted-ips-for-federated-users"></a>IPs confiáveis para usuários federados
IPs confiáveis permitem que os administradores tooby passagem verificação de duas etapas para endereços IP específicos, ou para usuários federados que têm as solicitações originadas dentro de sua própria intranet. Olá seções a seguir descrevem como tooconfigure autenticação multifator do Azure confiável IPs com usuários federados e verificação em duas etapas de desviar quando uma solicitação se origina de dentro de uma intranet de usuários federados. Isso é conseguido por meio da configuração do AD FS toouse passagem ou filtro de um modelo de declaração de entrada com hello tipo de declaração de dentro da rede corporativa.

Este exemplo usa o Office 365 para a relação de confiança com terceira parte confiável.

### <a name="configure-hello-ad-fs-claims-rules"></a>Configurar regras de declarações de saudação do AD FS
Olá primeira coisa a toodo é tooconfigure declarações de saudação do AD FS. Crie duas regras de declarações, um para hello dentro da rede corporativa de declaração de tipo e um adicional para manter nossos usuários conectados.

1. Abra o gerenciamento do AD FS.
2. Olá esquerda, selecione **terceira parte confiável**.
3. Clique com o botão direito do mouse na **Plataforma de Identidade Microsoft Office 365** e selecione **Editar Regras de Declaração...**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **passar ou filtrar uma declaração de entrada** de Olá suspensa e clique em **próximo**.
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Em Olá caixa próxima tooClaim nome da regra, nomeie a regra. Por exemplo: InsideCorpNet.
7. No hello suspenso, tooIncoming próximo tipo de declaração, selecione **dentro da rede corporativa**.
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Clique em **Concluir**.
9. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.
10. Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **enviar declarações usando uma regra personalizada** de Olá suspensa e clique em **próximo**.
11. Na caixa Nome da regra de declaração Olá: insira *manter usuários assinado em*.
12. Na caixa de regra personalizada hello, digite:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Clique em **Concluir**.
14. Clique em **Aplicar**.
15. Clique em **OK**.
16. Feche o gerenciamento do AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configurar IPs confiáveis do Azure Multi-Factor Authentication com usuários federados
Agora que as declarações de saudação entram em vigor, é possível configurar IPs confiáveis.

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Olá esquerda, clique em **do Active Directory**.
3. Em diretório, selecione o diretório de saudação onde você deseja tooset backup IPs confiáveis.
4. No hello diretório que você selecionou, clique em **configurar**.
5. Na seção de autenticação multifator hello, clique em **gerenciar configurações de serviço**.
6. Na página de configurações do serviço de hello, em IPs confiáveis, selecione **ignorar o multi-factor-autenticação de solicitações de usuários federados na minha intranet**.  

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Clique em **Salvar**.
8. Depois de saudação atualizações foram aplicadas, clique em **fechar**.

É isso! Neste ponto, os usuários federados do Office 365 devem ter somente toouse MFA quando uma reivindicação tem origem fora da intranet corporativa hello.
