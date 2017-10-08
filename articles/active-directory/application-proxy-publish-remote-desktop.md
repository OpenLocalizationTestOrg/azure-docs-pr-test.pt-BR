---
title: "aaaPublish área de trabalho remota com o Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Abrange Olá Noções básicas sobre conectores de Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Publicar a Área de Trabalho Remota com o Proxy de Aplicativo do Azure AD

Este artigo aborda como toodeploy serviços de área de trabalho remota (RDS) com o Proxy de aplicativo para que os usuários remotos podem ainda ser produtivos.

o objetivo da saudação público para este artigo é:
- Proxy de aplicativo do AD do Azure aos clientes que deseja que os usuários finais tootheir aplicativos mais toooffer publicando aplicativos locais através dos serviços de área de trabalho remota.
- Serviços de área de trabalho remota aos clientes que desejarem tooreduce Olá a ataques de sua implantação usando o Proxy de aplicativo do Azure AD. Este cenário fornece um conjunto limitado de verificação em duas etapas e tooRDS de controles de acesso condicional.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Como o Proxy de aplicativo se encaixa na implantação de RDS padrão Olá

Uma implantação do RDS padrão inclui vários serviços de função da Área de Trabalho Remota em execução no Windows Server. Olhando Olá [arquitetura dos serviços de área de trabalho remota](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), há várias opções de implantação. Olá a diferença mais notável entre hello [implantação de RDS com Proxy de aplicativo do Azure AD](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (mostrado no diagrama a seguir de saudação) e hello outras opções de implantação é esse cenário de Proxy de aplicativo hello tem uma saída de permanente conexão do servidor de saudação executando o serviço do conector hello. Outras implantações deixam conexões de entrada abertas por meio de um balanceador de carga.

![Fica de Proxy de aplicativo entre Olá RDS VM e Olá internet pública](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

Em uma implantação de RDS, a função da Web da área de trabalho remota de saudação e função do Gateway de área de trabalho remota Olá executados em máquinas de voltado para a Internet. Esses pontos de extremidade são expostos para Olá motivos a seguir:
- Web da área de trabalho remota oferece usuário Olá toosign um ponto de extremidade público no e exibição Olá vários aplicativos locais e áreas de trabalho que eles possam acessar. Ao selecionar um recurso, uma conexão de RDP é criado usando o aplicativo nativo Olá Olá sistema operacional.
- Gateway de área de trabalho remota entra em imagem hello quando um usuário inicia a conexão de RDP hello. Hello Gateway RD manipula o tráfego RDP Olá criptografado provenientes de saudação à Internet e converte toohello servidor local que Olá usuário está se conectando. Nesse cenário, Olá Olá de tráfego que gateway de área de trabalho remota está recebendo proveniente Olá Proxy de aplicativo do Azure AD.

>[!TIP]
>Se você ainda não implantou o RDS antes, ou obter mais informações antes de começar, saiba como muito[implantar perfeitamente RDS com o Gerenciador de recursos do Azure e o Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Requisitos

- Ambos Olá Web da área de trabalho remota e os pontos de extremidade devem estar localizados no servidor Gateway RD Olá mesmo computador e com uma raiz comum. Web da área de trabalho remota e Gateway de área de trabalho remota serão publicado como um único aplicativo para que você tenha uma experiência de logon único entre aplicativos Olá dois.

- Você já deverá ter [implantado o RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) e [habilitado o Proxy de Aplicativo](active-directory-application-proxy-enable.md).

- Este cenário pressupõe que seus usuários finais passar pelo Internet Explorer no Windows 7 ou Windows 10 desktops que se conectam por meio de página da Web da área de trabalho remota de saudação. Se você precisar toosupport outros sistemas operacionais, consulte [suporte para outras configurações de cliente](#support-for-other-client-configurations).

  >[!NOTE]
  >No momento, não há suporte para atualização do Criador do Windows 10.

- No Internet Explorer, habilitá-Olá ActiveX RDS.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Implantar Olá cenário comum de RDS e o Proxy de aplicativo

Depois de configurar o RDS e o Proxy de aplicativo do Azure AD para o seu ambiente, siga Olá etapas toocombine Olá duas soluções. Essas etapas explicam publicar Olá duas web voltados RDS pontos de extremidade (Web da área de trabalho remota e Gateway de área de trabalho remota) como aplicativos e direcionar o tráfego em seu toogo RDS por meio do Proxy de aplicativo.

### <a name="publish-hello-rd-host-endpoint"></a>Publicar o ponto de extremidade de host de área de trabalho remota Olá

1. [Publicar um novo aplicativo de Proxy de aplicativo](application-proxy-publish-azure-portal.md) com hello valores a seguir:
   - URL interna: https://\<rdhost\>.com /, onde \<rdhost\> é Olá raiz comum que compartilham Web da área de trabalho remota e Gateway de área de trabalho remota.
   - URL externa: Este campo é preenchido automaticamente com base no nome de saudação do aplicativo hello, mas você pode modificá-lo. Os usuários irá toothis URL quando acessarem RDS.
   - Método de pré-autenticação: Azure Active Directory
   - Converter cabeçalhos de URL: não
2. Atribuir usuários toohello publicado o aplicativo de área de trabalho remota. Verifique se que todos eles têm acesso tooRDS, muito.
3. Olá método de logon único para o aplicativo hello como Leave **AD do Azure SSO desabilitado**. Os usuários são frequentes tooauthenticate quando tooAzure AD e uma vez tooRD da Web, mas possuem tooRD de logon único Gateway.
4. Vá muito**Active Directory do Azure** > **registros do aplicativo** > *seu aplicativo* > **configurações**.
5. Selecione **propriedades** e atualização hello **URL da Home page** o ponto de extremidade do campo toopoint tooyour Web da área de trabalho remota (como https://\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Direcionar o tráfego RDS tooApplication Proxy

Conecte-se a implantação do RDS toohello como um administrador e altere o nome do servidor de Gateway de área de trabalho remota Olá para implantação de saudação. Isso garante que as conexões passam por Olá Proxy de aplicativo do Azure AD.

1. Conecte o servidor RDS toohello executando a função de agente de Conexão de área de trabalho de saudação.
2. Inicie o **Gerenciador do Servidor**.
3. Selecione **Remote Desktop Services** Olá no painel de saudação esquerda.
4. Selecione **Visão geral**.
5. Na seção Visão geral da implantação do hello, selecione o menu suspenso de saudação e escolha **editar propriedades de implantação**.
6. Na guia de Gateway de área de trabalho remota hello, alterar Olá **nome do servidor** toohello campo URL externa que você definiu para o ponto de extremidade de host de saudação área de trabalho remota no Proxy de aplicativo.
7. Saudação de alteração **método de Logon** campo muito**autenticação de senha**.

  ![Tela Propriedades de Implantação no RDS](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Para cada coleção, execute Olá comando a seguir. Substitua *\<yourcollectionname\>* e *\<proxyfrontendurl\>* por suas próprias informações. Este comando habilita o logon único entre a Web da Área de Trabalho Remota e Gateway de Área de Trabalho Remota e otimiza o desempenho:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Por exemplo:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. modificação de saudação tooverify de propriedades personalizadas de RDP hello, bem como exibir hello RDP conteúdo do arquivo que será baixado da RDWeb para esta coleção, execute Olá comando a seguir:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Agora que você configurou a área de trabalho remota, o Proxy de aplicativo do Azure AD tem assumido como componente de voltados à internet de saudação do RDS. Você pode remover Olá outros pontos de extremidade para a internet públicos em suas máquinas da Web da área de trabalho remota e Gateway de área de trabalho remota.

## <a name="test-hello-scenario"></a>Cenário de teste de saudação

Testar o cenário de saudação com o Internet Explorer no Windows 7 ou o computador de 10.

1. Vá toohello URL externa que você configurar ou localizar seu aplicativo hello [MyApps painel](https://myapps.microsoft.com).
2. Você será solicitado tooauthenticate tooAzure do Active Directory. Use uma conta que você atribuiu toohello aplicativo.
3. Você será solicitado tooauthenticate tooRD da Web.
4. Se a autenticação de RDS for bem-sucedida, você pode selecionar desktop saudação ou aplicativo que você deseja e começa a trabalhar.

## <a name="support-for-other-client-configurations"></a>Suporte para outras configurações de cliente

configuração de saudação descrita neste artigo é para usuários no Windows 7 ou 10, Internet Explorer além de complemento de RDS ActiveX hello. Se for necessário, no entanto, você poderá dar suporte a outros sistemas operacionais ou navegadores. diferença de saudação está no método de autenticação de saudação que você usar.

| Método de autenticação | Configuração de cliente com suporte |
| --------------------- | ------------------------------ |
| Pré-autenticação    | Windows 7/10 usando o Internet Explorer + complemento ActiveX do RDS |
| Passagem | Qualquer outro sistema operacional que dá suporte ao aplicativo de área de trabalho remota Microsoft hello |

fluxo de pré-autenticação Olá oferece mais benefícios de segurança que o fluxo de passagem de saudação. Com a pré-autenticação, você pode aproveitar os recursos de autenticação do Azure AD, como o logon único, acesso condicional e verificação em duas etapas, para os seus recursos locais. Você também pode garantir que somente tráfego autenticado alcance sua rede.

autenticação de passagem de toouse, há apenas duas modificações toohello etapas que são listadas neste artigo:
1. Em [publica o ponto de extremidade de host Olá RD](#publish-the-rd-host-endpoint) etapa 1, defina o método de pré-autenticação Olá muito**passagem**.
2. Em [tooApplication Proxy de tráfego direto RDS](#direct-rds-traffic-to-application-proxy), ignore a etapa 8 inteiramente.

## <a name="next-steps"></a>Próximas etapas

[Habilitar acesso remoto tooSharePoint com Proxy de aplicativo do Azure AD](application-proxy-enable-remote-access-sharepoint.md)  
[Considerações de segurança para acessar aplicativos remotamente usando o Proxy de Aplicativo do Azure AD](application-proxy-security-considerations.md)
