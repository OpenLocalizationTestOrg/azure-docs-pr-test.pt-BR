---
title: "Introdução aaaAzure App Proxy AD - instalar o conector | Microsoft Docs"
description: "Ativar o Proxy de aplicativo no portal do Azure de saudação e instalar Olá conectores de proxy reverso hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Introdução ao Proxy de aplicativo e instalar o conector Olá
Este artigo orienta Olá etapas tooenable Proxy de aplicativo do Microsoft Azure AD para seu diretório na nuvem no Azure AD.

Se você não tiver ainda traz Proxy de aplicativo com reconhecimento de benefícios de segurança e a produtividade de saudação organização tooyour, saiba mais sobre [como tooprovide proteger o acesso remoto aplicativos locais tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Pré-requisitos de Proxy de aplicativo
Antes de habilitar e usar os serviços de Proxy de aplicativo, você precisa toohave:

* Uma [assinatura premium ou básica](active-directory-editions.md) do Microsoft Azure AD e um diretório do Azure AD do qual você seja administrador global.
* Um servidor executando o Windows Server 2012 R2 ou 2016, no qual você pode instalar Olá conector de Proxy de aplicativo. servidor de saudação precisa toobe tooconnect capaz de toohello serviços de Proxy do aplicativo na nuvem hello e Olá aplicativos que você está publicando locais.
  * Para tooyour de logon único usando a delegação restrita de Kerberos, os aplicativos publicados nesta máquina deve ser domínio no domínio Olá mesmo AD como aplicativos de saudação que você está publicando. Para obter mais informações, consulte [KCD para logon único com o Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md).

Se sua organização usa o proxy de leitura da internet, servidores tooconnect toohello [funcionam com existente de servidores proxy no local](application-proxy-working-with-proxy-servers.md) para obter detalhes sobre como tooconfigure-los antes de obtém Introdução ao Proxy de aplicativo.

## <a name="open-your-ports"></a>Abrir as portas

tooprepare seu ambiente para o Proxy de aplicativo do AD do Azure, primeiro é necessário tooenable comunicação tooAzure data centers. Se houver um firewall no caminho de saudação, certifique-se de que ele está aberto para que Olá que conector pode tornar HTTPS (TCP) solicita toohello Proxy de aplicativo.

1. Seguir Olá abrir portas muito**saída** tráfego:

   | Número da porta | Como ele é usado |
   | --- | --- |
   | 80 | Baixando a revogação de certificado CRLs (listas) ao validar o certificado SSL Olá |
   | 443 | Toda a comunicação com hello serviço Proxy de aplicativo |

   Se o firewall reforça o tráfego de acordo com os usuários de toooriginating, abra essas portas para o tráfego dos serviços do Windows que são executados como um serviço de rede.

   > [!IMPORTANT]
   > tabela Olá reflete os requisitos de porta de saudação para versões do conector 1.5.132.0 e mais recente. Se você ainda tiver uma versão mais antiga do conector, você precisa também Olá tooenable seguintes portas em adição too80 e 443:5671, 8080, 9090-9091, 9350, 9352, 10100 – 10120.
   >
   >Para obter informações sobre como atualizar sua versão mais recente do toohello de conectores, consulte [conectores de Proxy de aplicativo do AD do Azure entender](application-proxy-understand-connectors.md#automatic-updates).

2. Se o firewall ou proxy permite que a lista branca DNS, você pode n e t e toomsappproxy.net de conexões da lista de permissões. Se não, você precisa tooallow acesso toohello [intervalos de IP de DataCenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653), que é atualizado a cada semana.

3. A Microsoft usa certificados de tooverify quatro endereços. Permitir acesso toohello URLs a seguir se você ainda não tiver feito isso para outros produtos:
   * mscrl.microsoft.com:80
   * crl.microsoft.com:80
   * ocsp.msocsp.com:80
   * www.microsoft.com:80

4. O conector precisa de acesso toologin.windows.net e login.microsoftonline.net para o processo de registro de saudação.

5. Saudação de uso [ferramenta de teste das portas conector do Azure AD aplicativo Proxy](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que seu conector possa acessar o serviço de Proxy de aplicativo hello. No mínimo, certifique-se de que que a região do hello centro dos EUA e Olá região mais próxima tooyou tenham todas as marcas de seleção verdes. Além disso, um número maior de marcas de seleção verdes significa maior resiliência.

## <a name="install-and-register-a-connector"></a>Instalar e registrar um conector
1. Entrar como um administrador no hello [portal do Azure](https://portal.azure.com/).
2. O diretório atual aparece em seu nome de usuário no canto superior direito da saudação. Se você precisar toochange diretórios, selecione esse ícone.
3. Vá muito**Active Directory do Azure** > **Proxy de aplicativo**.

   ![Navegue tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Selecione **Baixar o Conector**.

   ![Baixar o Conector](./media/active-directory-application-proxy-enable/download_connector.png)

5. Executar **AADApplicationProxyConnectorInstaller.exe** no servidor de saudação você preparou acordo toohello pré-requisitos.
6. Siga as instruções de Olá Olá Assistente tooinstall. Durante a instalação, você está tooregister solicitadas Olá conector com hello Proxy de aplicativo do seu locatário do AD do Azure.

   * Forneça suas credenciais de administrador global do AD do Azure. Seu locatário de administrador global pode ser diferente das suas credenciais do Microsoft Azure.
   * Verifique se o administrador Olá Olá de registros Olá conector está no mesmo diretório onde você habilitou Olá serviço Proxy de aplicativo. Por exemplo, se o domínio de locatário Olá for contoso.com, Olá administrador deve ser admin@contoso.com ou qualquer outro alias nesse domínio.
   * Se **configuração de segurança aprimorada do IE** está definido muito**em** no servidor de saudação onde você está instalando o conector hello, você poderá não ver a tela de registro hello. acesso de tooget, siga as instruções de saudação na mensagem de erro de saudação. Certifique-se de que a Segurança Melhorada do Internet Explorer está desativada.

Para fins de alta disponibilidade, você deve implantar pelo menos dois conectores. Cada conector deve ser registrado separadamente.

## <a name="test-that-hello-connector-installed-correctly"></a>Testar esse conector Olá instalado corretamente

Você pode confirmar que um novo conector instalado corretamente verificando-lo em qualquer Olá portal do Azure ou em seu servidor. 

Olá portal do Azure, entrar tooyour locatário e navegue muito**Active Directory do Azure** > **Proxy de aplicativo**. Todos os seus conectores e grupos de conector são exibidos nesta página. Selecione um conector toosee seus detalhes ou mova-o para um grupo diferente. 

No seu servidor, verifique a lista de saudação de serviços de ativo para o conector hello e atualizador do conector de saudação. dois serviços de saudação devem iniciar a execução imediatamente, mas se não, ligá-los: 

   * **Conector de Proxy de Aplicativo do Microsoft AAD** habilita a conectividade

   * O **Atualizador de conector do Proxy de Aplicativo do Microsoft AAD** é um serviço de atualização automática. atualizador de saudação verifica novas versões do conector hello e atualizações Olá conector conforme necessário.

   ![Serviços do Conector de Proxy de Aplicativo - captura de tela](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Para obter informações sobre como eles permanecem backup toodate e conectores, consulte [conectores de Proxy de aplicativo do AD do Azure entender](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Próximas etapas
Agora você está pronto muito[publicar aplicativos com Proxy de aplicativo](application-proxy-publish-azure-portal.md).

Se você tiver aplicativos que estão em redes separadas ou em locais diferentes, use conectores diferentes do conector grupos tooorganize Olá em unidades lógicas. Saiba mais sobre como [Trabalhar com conectores de Proxy de Aplicativo](active-directory-application-proxy-connectors-azure-portal.md).
