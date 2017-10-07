---
title: "Tutorial: Integração do Azure Active Directory ao Central Desktop | Microsoft Docs"
description: "Saiba como toouse Central Desktop com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Tutorial: Integração do Active Directory do Azure ao Central Desktop
Olá objetivo deste tutorial é tooshow integração de saudação do Azure e área de trabalho Central. cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura habilitada para logon único do Central Desktop/locatário do Central Desktop

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

* Habilitando Olá integração de aplicativos de área de trabalho Central
* Configuração do SSO (logon único)
* Configurando o provisionamento de usuários
* Atribuindo usuários

![Cenário](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Cenário")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Habilitar a integração de aplicativo hello para área de trabalho Central
Olá objetivo desta seção é toooutline como tooenable Olá integração de área de trabalho Central.

**integração de aplicativos de saudação tooenable para área de trabalho Central, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
   ![Adicionar aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
   ![Adicionar um aplicativo da galeria](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Central Desktop**.
   
   ![Galeria de aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galeria de aplicativos")
7. No painel de resultados de saudação, selecione **Central Desktop**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Área de Trabalho Central](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Área de Trabalho Central")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCentral área de trabalho com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

Como parte desse procedimento, será necessário tooupload um locatário de área de trabalho Central tooyour certificado codificado em base 64.  
Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Central Desktop** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.
   
   ![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar logon único")
2. Em Olá **como você gostaria toosign usuários na área de trabalho de tooCentral** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar logon único")
3. Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**: 
   
   1. Em Olá **Central Desktop URL de entrada** caixa de texto, digite a URL do seu locatário Central Desktop saudação (por exemplo: *http://contoso.centraldesktop.com*).
   2. Na caixa de texto de URL de resposta do Central Desktop hello, digite a URL de AssertionConsumerService de área de trabalho Central (por exemplo: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Você pode obter o valor de saudação do hello metadados de área de trabalho central (por exemplo: *http://contoso.centraldesktop.com*).
   >  
   
   ![Configurar URL do Aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar URL do Aplicativo")
4. Em Olá **configurar logon único no Central Desktop** página, toodownload seu certificado, clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.
   
  ![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar logon único")
5. Faça logon no tooyour **Central Desktop** locatário.
6. Vá muito**configurações**, clique em **avançado**e, em seguida, clique em **Single Sign On**.
   
  ![Configuração – Avançada](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Configuração – Avançada")
7. Em Olá **logon único** página, execute Olá etapas a seguir:
   
  ![Configurações de Logon Único](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configurações de Logon Único")
   
  1. Selecione **Habilitar Logon Único do SAML v2**.
  2. Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL do emissor** valor e, em seguida, cole-Olá **URL SSO** caixa de texto.
  3. Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL de logon remoto** valor e, em seguida, cole-o em Olá **URL de logon SSO**caixa de texto.
  4. Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL do serviço de logon único** valor e, em seguida, cole-Olá **URL de logoff SSO** caixa de texto.
8. Em Olá **método de verificação de assinatura de mensagens** , execute Olá etapas a seguir:
   
   ![Método de Verificação de Assinatura da Mensagem](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de Verificação de Assinatura da Mensagem")
   
  1. Selecione **Certificado**.
  2. De saudação **certificado SSO** lista, selecione **RSH SHA256**.
  3. Criar um arquivo de texto do certificado Olá baixado, Olá de copiar conteúdo de arquivo de texto de saudação e, em seguida, cole-Olá **certificado SSO** campo.  
     >[!TIP]
     >Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Selecione **exibir uma página de logon do link tooyour SAMLv2**.
9. Clique em **Atualizar**.
10. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
    
    ![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar logon único")
    
## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário

Para AAD usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo de área de trabalho Central. Esta seção descreve como contas de usuário do AAD toocreate na área de trabalho Central.

**tooCentral de contas de usuário do tooprovision área de trabalho:**
1. Faça logon no tooyour locatário Central Desktop.
2. Vá muito**pessoas \> membros internos**.
3. Clique em **Adicionar Membros Internos**.
   
  ![Pessoas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Pessoas")
4. Em Olá **endereço de Email dos membros novos** caixa de texto, digite uma conta do AAD você deseja tooprovision e, em seguida, clique em **próximo**.
   
  ![Endereços de Email de Novos Membros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Endereços de Email de Novos Membros")
5. Clique em **Adicionar Membro(s) interno(s)**.
   
  ![Adicionar Membro Interno](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Adicionar Membro Interno")
   
   >[!NOTE]
   >usuários de Olá que você adicionou receberão um email que inclui um link de confirmação que precisam de conta de saudação do tooclick tooactivate.
   > 

>[!NOTE]
>Você pode usar qualquer outra área de trabalho Central usuário conta ferramenta de criação ou APIs fornecidas pela área de trabalho Central tooprovision contas de usuário do AAD
>  

## <a name="assign-users"></a>Atribuir usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooCentral área de trabalho, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em Olá **Central Desktop** página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir usuários](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Atribuir usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

