---
title: Proteger recursos de nuvem com o Azure MFA e o AD FS | Microsoft Docs
description: "Esta é a página do Azure Multi-Factor Authentication que descreve como começar a usar o Azure MFA e o AD FS na nuvem."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: joflore
ms.openlocfilehash: c94b20ec984c96cfb8e7339826ee933ea4194bfc
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Protegendo os recursos de nuvem usando a Autenticação Multifator do Azure e o AD FS
Se sua organização for federada com o Azure Active Directory, use a Autenticação Multifator do Azure ou os Serviços de Federação do Active Directory (AD FS) para proteger os recursos que são acessados pelo Azure AD. Use os procedimentos a seguir para proteger os recursos do Azure Active Directory com Autenticação Multifator do Azure ou os Serviços de Federação do Active Directory.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteger recursos do Azure AD usando o AD FS
Para proteger seus recursos de nuvem, configure uma regra de declaração para que os Serviços de Federação do Active Directory emitem a declaração multipleauthn quando um usuário executa a verificação em duas etapas com êxito. Essa declaração é passada para o Azure AD. Siga este procedimento para percorrer as etapas:


1. Abra o gerenciamento do AD FS.
2. À esquerda, selecione **Relações de Confiança com Terceira Parte Confiável**.
3. Clique com o botão direito do mouse na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Declaração**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. No Assistente Adicionar Regra de Declaração de Transformação, selecione **Passar ou filtrar uma Declaração de Entrada** na lista e clique em **Avançar**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Dê um nome para a regra. 
7. Selecione **Referências de Métodos de Autenticação** como o tipo de declaração Entrada.
8. Selecione **Passar todos os valores de declaração**.
    ![Assistente para Adicionar Regra de Declaração de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Clique em **Concluir**. Feche o Console de gerenciamento do AD FS.

## <a name="trusted-ips-for-federated-users"></a>IPs confiáveis para usuários federados
IPs confiáveis permitem aos administradores ignorar a verificação em duas etapas para endereços IP específicos ou para usuários federados que têm as solicitações originadas em seu próprios intranet. As seções a seguir descrevem como configurar IPs confiáveis da Autenticação Multifator do Azure com usuários federados e desviar a verificação em duas etapas quando uma solicitação se originar de dentro de uma intranet de usuários federados. Isso é conseguido por meio da configuração do AD FS para usar uma passagem ou filtrar um modelo de declaração de entrada com o tipo de declaração Dentro da rede corporativa.

Este exemplo usa o Office 365 para a relação de confiança com terceira parte confiável.

### <a name="configure-the-ad-fs-claims-rules"></a>Configurar as regras de declarações do AD FS
A primeira coisa que precisamos fazer é configurar as declarações do AD FS. Criamos duas regras declarações: uma para o tipo de declaração Dentro da rede corporativa e um adicional para manter nossos usuários conectados.

1. Abra o gerenciamento do AD FS.
2. À esquerda, selecione **Relações de Confiança com Terceira Parte Confiável**.
3. Clique com o botão direito do mouse na **Plataforma de Identidade Microsoft Office 365** e selecione **Editar Regras de Declaração...**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. No Assistente Adicionar Regra de Declaração de Transformação, selecione **Passar ou filtrar uma Declaração de Entrada** na lista e clique em **Avançar**.
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Na caixa ao lado do nome da regra de declaração, nomeie a regra. Por exemplo: InsideCorpNet.
7. Na lista suspensa, ao lado do tipo de declaração de entrada, selecione **Dentro da rede corporativa**.
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Clique em **Concluir**.
9. Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.
10. No Assistente Adicionar Regra de Declaração de Transformação, selecione **Enviar Declarações Usando uma Regra Personalizada** da lista suspensa e clique em **Avançar**.
11. Na caixa abaixo do nome da regra de declaração: insira *Manter Usuários Conectados*.
12. Na caixa de regra Personalizada, digite:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Clique em **Concluir**.
14. Clique em **Aplicar**.
15. Clique em **OK**.
16. Feche o gerenciamento do AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configurar IPs confiáveis da Autenticação Multifator do Azure com usuários federados
Agora que as declarações estão prontas, podemos configurar IPs confiáveis.

1. Entre no [portal do Azure](https://portal.com).
2. Selecione **Azure Active Directory** > **Acesso condicional** > **Locais nomeados**.
3. Na folha **Acesso condicional - Locais nomeados**, selecione **Configurar IPs confiáveis do MFA**

   ![Configurar IPs confiáveis do MFA de locais nomeados de acesso condicional do Azure AD](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)

4. Na página Configurações de Serviço, em **IPs confiáveis**, selecione **Ignorar autenticação multifator para solicitações de usuários federados na minha intranet**.  
5. Clique em **Salvar**.

É isso! Neste ponto, os usuários federados do Office 365 devem somente ter que usar MFA quando uma declaração for originada fora da intranet corporativa.
