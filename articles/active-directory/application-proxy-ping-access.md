---
title: "autenticação baseada em aaaHeader com PingAccess para Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Publica aplicativos com PingAccess e Proxy de aplicativo toosupport com base no cabeçalho de autenticação."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Autenticação baseada em cabeçalho para logon único com Proxy de Aplicativo e PingAccess

Azure Active Directory Application Proxy e PingAccess têm uma parceria junto aos clientes do Active Directory do Azure tooprovide tooeven acesso mais aplicativos. PingAccess expande Olá [ofertas de Proxy de aplicativo existentes](active-directory-application-proxy-get-started.md) tooinclude tooapplications de acesso de logon único que usam cabeçalhos para autenticação.

## <a name="what-is-pingaccess-for-azure-ad"></a>O que é PingAccess para Azure AD?

PingAccess para Active Directory do Azure é uma oferta de PingAccess que permite o acesso aos usuários toogive e único logon tooapplications que usam cabeçalhos para autenticação. Proxy de aplicativo trata esses aplicativos como qualquer outro, usando o acesso do AD do Azure tooauthenticate e, em seguida, passar o tráfego por meio do serviço de conector hello. PingAccess se encontra na frente de aplicativos hello e converte o token de acesso de saudação do AD do Azure em um cabeçalho para que o aplicativo hello recebe autenticação Olá no formato de saudação pode ler.

Os usuários não irá notar algo diferente quando eles entrarem toouse seus aplicativos corporativos. Eles ainda podem trabalhar de qualquer lugar e em qualquer dispositivo. 

Desde que os conectores de Proxy de aplicativo hello direcionam tráfego remoto tooall aplicativos independentemente do tipo de autenticação, eles continuará saldo tooload automaticamente, e também.

## <a name="how-do-i-get-access"></a>Como posso obter acesso?

Como esse cenário é oferecido por meio de uma parceria entre o Azure Active Directory e o PingAccess, você precisa de licenças para os dois serviços. No entanto, as assinaturas do Azure Active Directory Premium incluem uma licença básica PingAccess que abrange too20 aplicativos. Se você precisar de mais de 20 aplicativos baseados em cabeçalho toopublish, você pode adquirir uma licença adicional de PingAccess. 

Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Publicar seu aplicativo no Azure

Este artigo destina-se a pessoas que estiver publicando um aplicativo com este cenário para Olá primeira vez. Ele explica como tooget iniciada com o aplicativo e PingAccess, além de etapas de publicação toohello. Se você já tiver configurado os dois serviços, mas desejar uma atualização em Olá etapas de publicação, você pode ignorar a instalação do conector hello e mover muito[adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Como este cenário é uma parceria entre o Azure AD e PingAccess, algumas das instruções Olá existirem no hello site identidade de Ping.

### <a name="install-an-application-proxy-connector"></a>Instalar um conector do Proxy de Aplicativo

Se você já tem o Proxy de aplicativo habilitado e tenha um conector, você pode ignorar esta seção e mover muito[adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo](#add-your-app-to-azure-ad-with-application-proxy).

conector de Proxy de aplicativo Hello é um servidor Windows aplicativos publicados do serviço que direciona o tráfego de saudação do tooyour seus funcionários remotos. Para obter mais instruções de instalação, consulte [habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md).

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador global.
2. Selecione **Azure Active Directory** > **Proxy de aplicativo** .
3. Selecione **baixar conector** download do conector de Proxy de aplicativo toostart hello. Siga as instruções de instalação de saudação.

   ![Habilitar Proxy de aplicativo e baixar conector Olá](./media/application-proxy-ping-access/install-connector.png)

4. Baixando Olá connector automaticamente deve habilitar o Proxy de aplicativo para seu diretório, mas se não é possível selecionar **habilitar Proxy de aplicativo**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Adicionar tooAzure seu aplicativo AD com o Proxy de aplicativo

Há duas ações que você precisa tootake em Olá portal do Azure. Primeiro, você precisa toopublish seu aplicativo com o Proxy de aplicativo. Em seguida, você precisa toocollect algumas informações sobre o aplicativo hello que você pode usar durante as etapas de PingAccess hello.

Siga estas etapas toopublish seu aplicativo. Para um passo a passo mais detalhado das etapas 1 a 8, veja [Publicar aplicativos usando o Proxy de Aplicativo do Azure AD](application-proxy-publish-azure-portal.md).

1. Se você não fez isso na última seção do hello, entre no toohello [portal do Azure](https://portal.azure.com) como um administrador global.
2. Selecione **Azure Active Directory** > **Aplicativos empresariais**.
3. Selecione **adicionar** na parte superior de saudação da folha de saudação.
4. Selecione **Aplicativo local**.
5. Preencha os campos de saudação necessárias com informações sobre seu novo aplicativo. Use Olá diretrizes para configurações de saudação a seguir:
   - **URL interna**: normalmente você fornecer Olá URL que leva você de inscrição do aplicativo toohello na página quando você estiver na rede corporativa hello. Para este cenário conector Olá precisa tootreat Olá PingAccess proxy como página inicial de saudação do aplicativo hello. Use este formato: `https://<host name of your PA server>:<port>`. porta de saudação é 3000 por padrão, mas você pode configurá-lo no PingAccess.
   - **Método de Pré-autenticação**: Azure Active Directory
   - **Converter URL em cabeçalhos**: não

   >[!NOTE]
   >Se esse for o primeiro aplicativo, use a porta 3000 toostart e voltar tooupdate essa configuração se você alterar a configuração de PingAccess. Se esse for o seu aplicativo de segundo ou posterior, isso será necessário toomatch Olá ouvinte que você configurou no PingAccess. Saiba mais sobre [ouvintes no PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Selecione **adicionar** na parte inferior da saudação da folha de saudação. Seu aplicativo é adicionado e menu de início rápido de saudação é aberto.
7. No menu de início rápido do hello, selecione **atribuir um usuário para teste**e adicione pelo menos um usuário toohello aplicativo. Verifique se que essa conta de teste possui acesso toohello local aplicativo.
8. Selecione **atribuir** toosave atribuição de usuário de teste de saudação.
9. Na folha de gerenciamento de aplicativo hello, selecione **o logon único**.
10. Escolha **com base no cabeçalho de logon** do menu suspenso de saudação. Selecione **Salvar**.

   >[!TIP]
   >Se for a primeira vez usando com base no cabeçalho de logon único, você precisa tooinstall PingAccess. toomake-se de que sua assinatura do Azure é associada automaticamente a instalação do PingAccess, use link Olá toodownload essa página de logon único PingAccess. Você pode abrir o site de download de saudação agora ou voltar toothis página mais tarde. 

   ![Selecione o logon com base no cabeçalho](./media/application-proxy-ping-access/sso-header.PNG)

11. Feche a folha de aplicativos de empresa hello ou role menu de Active Directory do Azure do hello maneira toohello tooreturn esquerdo toohello todos os.
12. Selecione **Registros do Aplicativo**.

   ![Selecionar Registros de aplicativo](./media/application-proxy-ping-access/app-registrations.png)

13. Olá selecione aplicativo você acabou de adicionar, em seguida, **URLs de resposta**.

   ![Selecionar URLs de Resposta](./media/application-proxy-ping-access/reply-urls.png)

14. Verifique toosee se URL externa Olá esse aplicativo de tooyour atribuído você na etapa 5 estiver na lista de URLs de resposta de saudação. Se não estiver, adicione-a agora.
15. Na folha de configurações do aplicativo hello, selecione **as permissões necessárias**.

  ![Selecionar Permissões necessárias](./media/application-proxy-ping-access/required-permissions.png)

16. Selecione **Adicionar**. Para Olá API, escolha **Windows Azure Active Directory**, em seguida, **selecione**. Para permissões de saudação, escolha **leitura e gravar todos os aplicativos** e **entrar e ler o perfil de usuário**, em seguida, **selecione** e **feito**.  

  ![Selecionar permissões](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Coletar informações de etapas de PingAccess Olá

1. Na folha de configurações de seu aplicativo, selecione **Propriedades**. 

  ![Selecionar Propriedades](./media/application-proxy-ping-access/properties.png)

2. Salvar Olá **Id do aplicativo** valor. Isso é usado para a ID de cliente hello quando você configura PingAccess.
3. Na folha de configurações do aplicativo hello, selecione **chaves**.

  ![Selecionar Chaves](./media/application-proxy-ping-access/Keys.png)

4. Crie uma chave de inserir uma descrição de chave e escolhendo uma data de expiração no menu suspenso de saudação.
5. Selecione **Salvar**. Um GUID é exibida no hello **valor** campo.

  Salvar esse valor agora, pois não será capaz de toosee-lo novamente depois de fechar esta janela.

  ![Criar uma nova chave](./media/application-proxy-ping-access/create-keys.png)

6. Feche a folha de registros do aplicativo hello ou role menu de Active Directory do Azure do hello maneira toohello tooreturn esquerdo toohello todos os.
7. Selecione **Propriedades**.
8. Salvar Olá **ID de diretório** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Opcional - atualização GraphAPI toosend os campos personalizados

Para obter uma lista de tokens de segurança que o Azure AD envia para autenticação, confira [Referência de token do Azure AD](./develop/active-directory-token-and-claims.md). Se você precisar de uma declaração personalizada que envia outros tokens, use o campo de aplicativo GraphAPI tooset Olá *acceptMappedClaims* muito**True**. Você pode usar o Azure AD Graph Explorer ou MS Graph toomake essa configuração. 

Este exemplo usa o Explorador do Graph:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Baixar o PingAccess e configurar seu aplicativo

Agora que você concluiu todas as etapas de instalação do Active Directory do Azure hello, você pode mover em tooconfiguring PingAccess. 

Olá etapas detalhadas para Olá PingAccess parte deste cenário continuam Olá documentação de identidade de Ping, [PingAccess configurar o AD do Azure](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Essas etapas orientam você durante o processo de saudação de obter uma conta de PingAccess se você ainda não tiver um, a instalação Olá PingAccess Server e a criação de uma conexão de provedor do Azure AD OIDC com hello ID de diretório que você copiou da saudação portal do Azure. Em seguida, use Olá valores de ID do aplicativo e a chave toocreate uma sessão Web PingAccess. Em seguida, configure o mapeamento de identidade e crie um host virtual, site e aplicativo.

### <a name="test-your-app"></a>Testar seu aplicativo

Depois de concluir todas essas etapas, seu aplicativo estará pronto para execução. tootest-lo, abra um navegador e navegue toohello URL externa que você criou quando você publicou o aplicativo hello no Azure. Entre com a conta de teste de saudação que você toohello atribuído o aplicativo.

## <a name="next-steps"></a>Próximas etapas

- [Configurar o PingAccess para Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Como o Proxy de Aplicativo do Azure AD fornece logon único?](application-proxy-sso-overview.md)
- [Solucionar problemas de Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)
