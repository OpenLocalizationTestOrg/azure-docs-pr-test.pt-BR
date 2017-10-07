---
title: "aaaAzure serviço Web do aplicativo móvel de servidor do MFA | Microsoft Docs"
description: "aplicativo do Microsoft Authenticator Olá oferece uma opção de autenticação fora de banda adicional.  Ele permite Olá toousers de notificações de envio por push do MFA servidor toouse."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Habilitar a autenticação de aplicativo móvel com o Servidor de Autenticação Multifator do Azure

aplicativo do Microsoft Authenticator Olá oferece uma opção de verificação adicional de fora da banda. Em vez de fazer uma chamada telefônica automática ou usuário do SMS toohello durante o logon, o Azure multi-Factor Authentication envia um aplicativo de Microsoft Authenticator notificação toohello no smartphone ou tablet saudação do usuário. Olá usuário simplesmente toca **verificar** (ou digita um PIN e toca em "Autenticar") no hello aplicativo toocomplete sua entrada.

É preferível a utilização de um aplicativo móvel para a verificação em duas etapas quando a recepção do telefone não é confiável. Se você usar o aplicativo hello como um gerador de token OATH, ele não requer qualquer conexão de rede ou internet.

Dependendo do seu ambiente, convém toodeploy Olá móvel da web do serviço de aplicativo em Olá mesmo servidor como servidor de autenticação multifator do Azure ou em outro servidor voltado para a internet.

## <a name="requirements"></a>Requisitos

toouse Olá Microsoft Authenticator aplicativo, a seguir Olá é necessária para que hello aplicativo pode se comunicar com êxito com o serviço Web aplicativos móveis:

* Servidor de Autenticação Multifator do Azure v6.0 ou superior
* Instalar o Serviço Web do Aplicativo Móvel em um servidor Web da Internet executando o [IIS (Serviços de Informações da Internet) IIS 7.x ou superior](http://www.iis.net/) da Microsoft®
* ASP.NET v 4.0.30319 é instalado, registrado e definido tooAllowed
* Os serviços de função obrigatórios incluem o ASP.NET e a Compatibilidade de Metabase do IIS 6
* O Serviço Web do Aplicativo Móvel está acessível por meio de uma URL pública
* O Serviço Web do Aplicativo Móvel está protegido com um certificado SSL.
* Instalar Olá SDK do serviço Web do Azure multi-Factor Authentication no IIS 7. x ou superior no hello **mesmo servidor Olá servidor Azure multi-Factor Authentication**
* Olá SDK do serviço Web do Azure multi-Factor Authentication é protegida por um certificado SSL.
* Serviço Web aplicativos móveis podem se conectar toohello SDK do serviço Web do Azure multi-Factor Authentication sobre SSL
* Serviço Web aplicativos móveis podem se autenticar toohello SDK de serviço Web do Azure MFA usando Olá credenciais de uma conta de serviço que seja membro do grupo de segurança "Administradores" hello. Essa conta de serviço e o grupo existem no Active Directory se Olá servidor Azure multi-Factor Authentication estiver em um servidor ingressado no domínio. Essa conta de serviço e o grupo existem localmente no hello servidor Azure multi-Factor Authentication se não for tooa ingressado no domínio.

## <a name="install-hello-mobile-app-web-service"></a>Instalar serviço de web do aplicativo móvel Olá

Antes de instalar o serviço de web do aplicativo móvel hello, lembre-se de saudação detalhes a seguir:

* Você precisa de uma conta de serviço que faça parte do grupo "Administradores do PhoneFactor". Essa conta pode ser Olá mesmo Olá um usado para a instalação do Portal do usuário de saudação.
* É útil tooopen um navegador da web no servidor de web hello voltado para a Internet e navegue toohello URL do SDK do serviço Web que foi inserida no arquivo Web. config de saudação do hello. Se o navegador Olá pode obter o serviço web de toohello com êxito, ele deve solicitar credenciais. Insira a saudação de nome de usuário e senha que foram inseridas no arquivo Web. config de saudação exatamente como ele aparece no arquivo hello. Certifique-se de que nenhum aviso de certificado ou erro seja exibido.
* Se um proxy reverso ou firewall estiver à frente do servidor de web do serviço Web aplicativos móveis hello e execução de descarregamento de SSL, você pode editar o arquivo de Web. config do serviço Web aplicativos móveis Olá para que hello serviço Web aplicativos móveis possa usar http em vez de https. SSL ainda é exigido do hello aplicativo móvel toohello firewall/proxy reverso. Adicionar Olá toohello chave a seguir \<appSettings\> seção:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Instalar o SDK do serviço web Olá

Em qualquer cenário, se hello SDK do serviço Web do Azure multi-Factor Authentication é **não** já instalado no hello servidor Azure multi-Factor Authentication (MFA), seguir as etapas de saudação concluída.

1. Abra o console do servidor multi-Factor Authentication hello.
2. Vá toohello **SDK do serviço Web** e selecione **instalar o SDK do serviço Web**.
3. Instalação concluída hello usando padrões de saudação, a menos que você precisa toochange-los por alguma razão.
4. Vincule a um site de toohello do certificado SSL no IIS.

Se você tiver dúvidas sobre como configurar um certificado SSL em um servidor IIS, consulte o artigo Olá [como tooSet o SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Olá SDK do serviço Web deve ser protegido com um certificado SSL. Um certificado autoassinado é suficiente para essa finalidade. Importe o certificado de Olá no repositório de "Autoridades de certificação confiáveis" Olá Olá Local da conta do computador no servidor de web do Portal do usuário Olá para que ele confia no certificado ao iniciar a conexão de SSL hello.

![SDK do serviço Web de configuração do Servidor MFA](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Instalar serviço de saudação

1. **No servidor MFA de saudação**, Procurar caminho de instalação toohello.
2. Navegue toohello pasta onde o Olá servidor Azure MFA é o padrão de saudação instalado é **C:\Program Files\Azure multi-Factor Authentication**.
3. Localize o arquivo de instalação Olá **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Se o servidor de saudação **não** para a Internet, servidor de voltados para Internet toohello do arquivo de instalação de Olá cópia.
4. Se hello servidor MFA é **não** comutador da internet toohello **servidor voltado para a internet**.
5. Executar Olá **MultiFactorAuthenticationMobileAppWebServiceSetup64** instalar o arquivo como um administrador, alterar Olá Site se desejado e altere o nome curto de tooa Olá de diretório Virtual se você deseja.
6. Após concluir instalação de Olá, procurar muito**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (ou diretório adequado com base no nome do diretório virtual Olá) e edite o arquivo Web. config de saudação.

   * Localizar chave Olá **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** e alterar **valor = ""** muito**valor = "Domínio \ usuário"** onde o domínio é uma conta de serviço que faz parte de Grupo "Administradores".
   * Localizar chave Olá **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** e alterar **valor = ""** muito**valor = "Senha"** onde a senha é senha Olá Olá serviço Conta inserida na linha anterior hello.
   * Localize Olá **configuração pfserviço Web de aplicativos** definir e alterar o valor de saudação do **http://localhost:4898/PfWsSdk.asmx** toohello URL do SDK do serviço Web (exemplo: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Salve o arquivo Web. config de saudação e feche o bloco de notas.

   > [!NOTE]
   > Como o SSL é usado para esta conexão, você deve fazer referência Olá SDK do serviço Web por **o nome de domínio totalmente qualificado (FQDN)** e **não o endereço IP**. Hello certificado SSL seria tiver sido emitido para Olá FQDN e hello URL usada deve corresponder Olá nome no certificado de saudação.

7. Se o site de saudação que o serviço Web aplicativos móveis foi instalado em já não estiver associado com um certificado assinado publicamente, instalar certificado Olá no servidor de saudação, abra o Gerenciador do IIS e associar Olá certificate toohello da.
8. Abra um navegador da web de qualquer computador e navegue toohello URL onde o serviço Web aplicativos móveis foi instalado (exemplo: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Certifique-se de que nenhum aviso de certificado ou erro seja exibido.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Definir configurações de aplicativo móvel de saudação no hello servidor Azure multi-Factor Authentication

Agora que o serviço de web do aplicativo móvel Olá estiver instalado, você precisa tooconfigure Olá servidor Azure multi-Factor Authentication toowork com o portal de saudação.

1. No console do servidor multi-Factor Authentication hello, clique em ícone do Portal do usuário hello. Verifique se os usuários têm permissão toocontrol de seus métodos de autenticação, **aplicativo móvel** na guia Configurações de hello, em **permitir que os usuários tooselect método**. Sem esse recurso habilitado, os usuários finais são necessário toocontact a ativação de toocomplete Help Desk para Olá aplicativo móvel.
2. Verificar Olá **permitem que os usuários tooactivate aplicativo móvel** caixa.
3. Verificar Olá **permitir registro de usuário** caixa.
4. Clique em Olá **aplicativo móvel** ícone.
5. Inserir URL hello está sendo usado com o diretório virtual de saudação que foi criado durante a instalação MultiFactorAuthenticationMobileAppWebServiceSetup64 (exemplo: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) no campo Olá  **URL do serviço Web aplicativos móveis:**.
6. Popular Olá **nome da conta** campo com hello toodisplay nome da empresa ou organização no aplicativo móvel hello para esta conta.
   ![Configurações de Aplicativo Móvel de configuração do Servidor MFA](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Próximas etapas

- [Cenários avançados com a Autenticação Multifator do Azure e VPNs de terceiros](multi-factor-authentication-advanced-vpn-configurations.md).