---
title: "aaaEnable Microsoft Windows Hello para empresas em sua organização | Microsoft Docs"
description: "Implantação instruções tooenable Microsoft Passport em sua organização."
services: active-directory
documentationcenter: 
keywords: "configurar o Microsoft Passport, implantação do Microsoft Windows Hello for Business"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Habilitar o Microsoft Windows Hello for Business em sua organização
Depois de [conectar dispositivos de domínio do Windows 10 com o Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), Olá tooenable Microsoft Windows Hello para empresas em sua organização a seguir:

1. Implantar o System Center Configuration Manager  
2. Definir as configurações de política
3. Configurar perfil de certificado Olá  

## <a name="deploy-system-center-configuration-manager"></a>Implantar o System Center Configuration Manager
toodeploy certificados de usuário com base em Windows Hello para chaves de negócio, você precisa seguir hello:

* **Ramificação atual do System Center Configuration Manager** -você precisa tooinstall versão 1606 ou melhor. Para obter mais informações, consulte Olá [documentação para o System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) e [Blog da equipe do System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Infraestrutura de chave pública (PKI)** -tooenable Microsoft Windows Hello para empresas usando certificados de usuário, você deve ter uma PKI em vigor. Se você não tiver um, ou você não deseja toouse-lo para certificados de usuário, você pode implantar um novo controlador de domínio que tenha o Windows Server 2016 build 10551 (ou superior) instalado. Execute as etapas de saudação muito[instalar um controlador de domínio de réplica em um domínio existente](https://technet.microsoft.com/library/jj574134.aspx) ou muito[instalar uma nova floresta do Active Directory, se você estiver criando um novo ambiente](https://technet.microsoft.com/library/jj574166). (Olá ISOs estão disponíveis para download em [Signiant mídia Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Definir as configurações de política
Olá tooconfigure Microsoft Windows Hello para configurações de política de negócios, você tem duas opções:

* Política de grupo no Active Directory 
* Olá System Center Configuration Manager 

Política de grupo no Active Directory é hello recomendado método tooconfigure Microsoft Windows Hello para configurações de política de negócios. 

Usar o System Center Configuration Manager é o método preferido de hello quando você também o usa toodeploy certificados. Este cenário:

* Assegura a compatibilidade com cenários de implantação mais recentes Olá
* Requer a saudação do lado do cliente Windows 10 versão 1607 ou superior.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Configurar o Microsoft Windows Hello para Empresas usando a Política de Grupo no Active Directory
**Etapas**:

1. Abra o Gerenciador do servidor e navegue muito**ferramentas** > **Group Policy Management**.
2. No gerenciamento de política de grupo, navegue toohello nó do domínio que corresponde a toohello domínio no qual você deseja tooenable junção do Azure AD.
3. Clique com o botão direito do mouse em **Objetos de Política de Grupo** e selecione **Novo**. Dê um nome ao seu Objeto de Política de Grupo, por exemplo, Habilitar o Windows Hello for Business. Clique em **OK**.
4. Clique com o botão direito do mouse em seu novo Objeto de Política de Grupo e selecione **Editar**.
5. Navegue muito**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **Windows Hello para empresas**.
6. Clique com o botão direito em **Habilitar o Windows Hello para Empresas** e, em seguida, selecione **Editar**.
7. Selecione Olá **habilitado** botão de opção e, em seguida, clique em **aplicar**. Clique em **OK**.
8. Agora você pode vincular o local de tooa Olá objeto de diretiva de grupo de sua escolha. tooenable essa política para todos os dispositivos com Windows 10 Olá ingressado no domínio em sua organização, o domínio de toohello link Olá diretiva de grupo. Por exemplo:
   * Uma UO (unidade organizacional) específica no Active Directory onde os computadores ingressados no domínio do Windows 10 estejam localizados.
   * Um grupo de segurança específico com computadores ingressados no domínio do Windows 10 que serão registrados automaticamente no AD do Azure.

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Configurar o Windows Hello for Business usando o System Center Configuration Manager
**Etapas**:

1. Olá abrir **System Center Configuration Manager**e, em seguida, navegue muito**ativos e conformidade > configurações de conformidade > acesso a recursos da empresa > Windows Hello para perfis de negócios**.
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Na barra de ferramentas de saudação na parte superior do hello, clique em **criar Windows Hello para empresas perfil**.
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. Em Olá **geral** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. Em Olá **nome** caixa de texto, digite um nome para seu perfil, por exemplo, **meu perfil WHfB**.
   
    b. Clique em **Avançar**.
4. Em Olá **plataformas com suporte** caixa de diálogo, plataformas Olá select que serão provisionadas com este Windows Hello para o perfil de negócios e, em seguida, clique em **próximo**.
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. Em Olá **configurações** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Em **Configurar o Windows Hello para Empresas**, selecionar **Habilitado**.
   
    b. Em **Usar um TPM (Trusted Platform Module)**, selecione **Obrigatório**. 
   
    c. Em **Método de autenticação**, selecione **Baseado em certificado**.
   
    d. Clique em **Avançar**.
6. Em Olá **resumo** caixa de diálogo, clique em **próximo**.
7. Em Olá **conclusão** caixa de diálogo, clique em **fechar**.
8. Na barra de ferramentas de saudação na parte superior do hello, clique em **implantar**.
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Configurar perfil de certificado Olá
Se você estiver usando autenticação baseada em certificado para autenticação local, você precisa tooconfigure e implanta um perfil de certificado. Esta tarefa exige tooset backup de um servidor NDES e a função de site do ponto de registro de certificado no hello System Center Configuration Manager. Para obter mais detalhes, consulte Olá [pré-requisitos para perfis de certificado no Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Olá abrir **System Center Configuration Manager**e, em seguida, navegue muito**ativos e conformidade > configurações de conformidade > acesso a recursos da empresa > perfis de certificado**.
2. Selecione um modelo que tenha EKU (uso estendido da chave) para entrada com cartão inteligente.

Em Olá **registro do protocolo SCEP** página Olá perfil de certificado, você precisa toochoose **instalar tooPassport for Work caso contrário falha** como Olá **Key Storage Provider**.

## <a name="next-steps"></a>Próximas etapas
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

