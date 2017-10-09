---
title: "aaaEnable Proxy de aplicativo do Azure AD no portal clássico Olá | Microsoft Docs"
description: "Ativar o Proxy de aplicativo no portal clássico do Azure de saudação e instalar Olá conectores de proxy reverso hello."
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
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Habilitar Proxy de aplicativo no portal clássico do hello e baixar conectores
Este artigo orienta Olá etapas tooenable Proxy de aplicativo do Microsoft Azure AD para seu diretório na nuvem no Azure AD.

Se você não estiver familiarizado com o Proxy de aplicativo podem ajudá-lo, saiba mais sobre [como tooprovide proteger o acesso remoto aplicativos locais tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Pré-requisitos de Proxy de aplicativo
Antes de habilitar e usar os serviços de Proxy de aplicativo, você precisa toohave:

* Uma [assinatura premium ou básica](active-directory-editions.md) do Microsoft Azure AD e um diretório do Azure AD do qual você seja administrador global.
* Um servidor executando o Windows Server 2012 R2 ou 2016, no qual você pode instalar Olá conector de Proxy de aplicativo. servidor Olá envia solicitações toohello serviços de Proxy do aplicativo na nuvem hello e precisa de um aplicativo de toohello de conexão HTTP ou HTTPS que você está publicando.
  * Para um único logon tooyour aplicativos publicados, esta máquina deve ser domínio no domínio Olá mesmo AD como aplicativos de saudação que você está publicando. Para obter mais informações, consulte [Logon único com o Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md)
* Se sua organização usa o proxy de leitura da internet, servidores tooconnect toohello [funcionam com existentes servidores proxy local](application-proxy-working-with-proxy-servers.md) para obter detalhes sobre como tooconfigure-los.

## <a name="open-your-ports"></a>Abrir as portas

tooprepare seu ambiente para o Proxy de aplicativo do AD do Azure, primeiro é necessário tooenable comunicação tooAzure data centers. Se houver um firewall no caminho de saudação, certifique-se de que ele está aberto para que Olá que conector pode tornar HTTPS (TCP) solicita toohello Proxy de aplicativo.

1. Seguir Olá abrir portas muito**saída** tráfego:

   | Número da porta | Como ele é usado |
   | --- | --- |
   | 80 | Baixando a revogação de certificado CRLs (listas) ao validar o certificado SSL Olá |
   | 443 | Toda a comunicação com hello serviço Proxy de aplicativo |

   Se o firewall reforça o tráfego de acordo com os usuários de toooriginating, abra essas portas para o tráfego proveniente dos serviços do Windows em execução como um serviço de rede.

   > [!IMPORTANT]
   > tabela Olá reflete os requisitos de porta de saudação para versões do conector 1.5.132.0 e mais recente. Se você ainda tiver uma versão mais antiga do conector, você também precisa Olá tooenable portas a seguir: 5671, 8080, 9090, 9091, 9350, 9352 e 10100 – 10120.
   >
   >Para obter informações sobre como atualizar sua versão mais recente do toohello de conectores, consulte [conectores de Proxy de aplicativo do AD do Azure entender](application-proxy-understand-connectors.md#automatic-updates).

2. Se o firewall ou proxy permite que a lista branca DNS, você pode n e t e toomsappproxy.net de conexões da lista de permissões. Se não, você precisa tooallow acesso toohello [intervalos de IP de DataCenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653), que é atualizado a cada semana.

3. Saudação de uso [ferramenta de teste das portas conector do Azure AD aplicativo Proxy](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que seu conector possa acessar o serviço de Proxy de aplicativo hello. No mínimo, certifique-se de que que a região do hello centro dos EUA e Olá região mais próxima tooyou tenham todas as marcas de seleção verdes. Além disso, um número maior de marcas de seleção verdes significa maior resiliência.

## <a name="enable-application-proxy-in-azure-ad"></a>Habilitar o Proxy de Aplicativo no Azure AD
1. Entrar como um administrador no hello [portal clássico do Azure](https://manage.windowsazure.com/).
2. Vá tooActive diretório e selecione Olá diretório no qual você deseja tooenable Proxy de aplicativo.

    ![Active Directory - ícone](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Selecione **configurar** da página de diretório Olá e role para baixo demais**Proxy de aplicativo**.
4. Ativar/desativar **habilitar serviços de Proxy de aplicativo para este diretório** muito**habilitado**.

    ![Habilitar Proxy de aplicativo](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Selecione **Baixar agora**. Olá **do Azure AD Proxy conector baixar o aplicativo** é aberto. Leia e aceite os termos de licença hello e clique em **baixar** arquivo do Windows Installer toosave hello (.exe) para o conector de saudação.

## <a name="install-and-register-hello-connector"></a>Instalar e registrar Olá conector
1. Executar **AADApplicationProxyConnectorInstaller.exe** no servidor de saudação você preparou acordo toohello pré-requisitos.
2. Siga as instruções de Olá Olá Assistente tooinstall.
3. Durante a instalação, você está tooregister solicitadas Olá conector com hello Proxy de aplicativo do seu locatário do AD do Azure.

   * Forneça suas credenciais de administrador global do AD do Azure. Seu locatário de administrador global pode ser diferente das suas credenciais do Microsoft Azure.
   * Verifique se o administrador Olá Olá de registros Olá conector está no mesmo diretório onde você habilitou Olá serviço Proxy de aplicativo. Por exemplo, se o domínio de locatário Olá for contoso.com, Olá administrador deve ser admin@contoso.com ou qualquer outro alias nesse domínio.
   * Se **configuração de segurança aprimorada do IE** está definido muito**em** no servidor de saudação, tela de saudação do registro poderá estar bloqueada. acesso de tooallow, siga as instruções de saudação na mensagem de erro de saudação. Certifique-se de que a Segurança Melhorada do Internet Explorer está desativada.
   * Se o registro do conector não for bem-sucedido, confira [Solucionar problemas de Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md).  
4. Quando Olá instalação for concluída, dois novos serviços serão adicionados tooyour server:

   * **Conector de Proxy de Aplicativo do Microsoft AAD** habilita a conectividade

     * O **Atualizador de conector do Proxy de Aplicativo do Microsoft AAD** é um serviço de atualização automática. Periodicamente, ele verifica se há novas versões do conector de saudação e atualiza o conector Olá conforme necessário.

     ![Serviços do Conector de Proxy de Aplicativo - captura de tela](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Clique em **concluir** na janela de instalação hello.

Para saber mais sobre conectores, veja [Noções básicas sobre conectores de proxy de aplicativo do Azure AD](application-proxy-understand-connectors.md).

Para fins de alta disponibilidade, você deve implantar pelo menos dois conectores. toodeploy mais conectores, repita as etapas 2 e 3. Cada conector deve ser registrado separadamente.

Se você quiser toouninstall Olá conector, desinstale o serviço de conector hello e o serviço do atualizador hello. Reinicie o serviço de saudação do computador toofully remover.

## <a name="next-steps"></a>Próximas etapas
Agora você está pronto muito[publicar aplicativos com Proxy de aplicativo](active-directory-application-proxy-publish.md).

Se você tiver aplicativos que estão em redes separadas ou em locais diferentes, você pode usar conectores diferentes do conector grupos tooorganize Olá em unidades lógicas. Saiba mais sobre como [Trabalhar com conectores de Proxy de Aplicativo](active-directory-application-proxy-connectors.md).
