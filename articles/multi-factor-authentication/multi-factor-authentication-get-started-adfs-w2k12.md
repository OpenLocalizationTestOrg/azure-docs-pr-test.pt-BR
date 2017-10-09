---
title: aaaMFA servidor com o AD FS no Windows Server | Microsoft Docs
description: "Este artigo descreve como tooget iniciada com autenticação multifator do Azure e o AD FS no Windows Server 2012 R2 e 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Configurar o servidor Azure multi-Factor Authentication toowork com o AD FS no Windows Server
Se você usa os serviços de Federação do Active Directory (AD FS) e deseja que recursos de nuvem ou local toosecure, você pode configurar o servidor Azure multi-Factor Authentication toowork com o AD FS. Essa configuração dispara a verificação em duas etapas para pontos de extremidade de alto valor.

Neste artigo, discutimos o uso do Servidor de Autenticação Multifator do Azure com o AD FS no Windows Server 2012 R2 ou no Windows Server 2016. Para obter mais informações, leia sobre como muito[proteger recursos locais e de nuvem usando o servidor Azure multi-Factor Authentication com o AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Proteger o AD FS do Windows Server com o Servidor de Autenticação Multifator do Azure
Quando você instala o servidor Azure multi-Factor Authentication, você tem Olá as opções a seguir:

* Instalar o servidor Azure multi-Factor Authentication localmente no hello mesmo servidor do AD FS
* Instalar adaptador do Azure multi-Factor Authentication Olá localmente em saudação do servidor AD FS e, em seguida, instale o servidor multi-Factor Authentication em um computador diferente

Antes de começar, lembre-se de saudação informações a seguir:

* Você não é necessário tooinstall servidor Azure multi-Factor Authentication no seu servidor do AD FS. No entanto, você deve instalar o adaptador do multi-Factor Authentication de saudação do AD FS em um Windows Server 2012 R2 ou Windows Server 2016 que esteja executando o AD FS. Você pode instalar o servidor de saudação em um computador diferente se é uma versão com suporte e instalar Olá adaptador do AD FS separadamente no servidor de Federação do AD FS. Consulte Olá toolearn procedimentos a seguir como tooinstall Olá adaptador separadamente.
* Se sua organização estiver usando métodos de verificação de aplicativo móvel ou mensagem de texto, cadeias de caracteres de saudação definidas nas configurações da empresa contém um espaço reservado, <$*application_name*$>. No Servidor de MFA v7.1, você pode fornecer um nome de aplicativo que substitui esse espaço reservado. Na versão 7.0 ou anterior, esse espaço reservado não será substituído automaticamente quando você usar o adaptador do hello AD FS. Para as versões mais antigas, remova espaço reservado de saudação cadeias de caracteres apropriadas hello quando você proteger o AD FS.
* conta de saudação que usam toosign no deve ter grupos de segurança de toocreate de direitos de usuário no serviço do Active Directory.
* Assistente de instalação do adaptador de saudação do multi-Factor Authentication AD FS cria um grupo de segurança denominado PhoneFactor Admins na sua instância do Active Directory. Ele, em seguida, adiciona a conta de serviço de saudação do AD FS do seu grupo de toothis do serviço de Federação. Verifique no controlador de domínio que hello grupo PhoneFactor Admins realmente foi criado e a conta de serviço do hello AD FS é um membro desse grupo. Se necessário, adicione manualmente toohello de conta de serviço de saudação do AD FS grupo PhoneFactor Admins no controlador de domínio.
* Para obter informações sobre como instalar Olá SDK do serviço Web com o portal do usuário hello, leia sobre [Implantando o portal do usuário Olá para o servidor Azure multi-Factor Authentication.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Instalar o servidor Azure multi-Factor Authentication localmente no servidor de saudação do AD FS
1. Baixe e instale o Servidor de Autenticação Multifator do Microsoft Azure no servidor do AD FS. Para obter informações sobre instalação, leia sobre a [introdução ao Servidor Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. No console de gerenciamento do servidor Azure multi-Factor Authentication hello, clique em Olá **do AD FS** ícone. Selecione as opções de saudação **permitir a inscrição de usuário** e **permitir que os usuários tooselect método**.
3. Selecione as opções adicionais que você gostaria que toospecify para sua organização.
4. Clique em **Instalar Adaptador do AD FS**.
   
   <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Se a janela do Active Directory Olá for exibida, isso significa que duas coisas. O computador é tooa ingressado no domínio e configuração do Active Directory Olá para proteger a comunicação entre o adaptador do hello AD FS e o serviço de autenticação multifator hello está incompleta. Clique em **próximo** tooautomatically concluir esta configuração, ou selecione Olá **ignorar configuração automática do Active Directory e definir as configurações manualmente** caixa de seleção. Clique em **Avançar**.
6. Janelas do grupo Local de saudação for exibido, significa que duas coisas. Seu computador não é tooa ingressado no domínio e configuração de grupo local Olá para proteger a comunicação entre o adaptador do hello AD FS e o serviço de autenticação multifator hello está incompleta. Clique em **próximo** tooautomatically concluir esta configuração, ou selecione Olá **ignorar configuração automática do grupo Local e definir as configurações manualmente** caixa de seleção. Clique em **Avançar**.
7. No Assistente de instalação de saudação, clique em **próximo**. Servidor de autenticação multifator do Azure cria Olá grupo PhoneFactor Admins e adiciona toohello de conta de serviço de saudação do AD FS grupo PhoneFactor Admins.
   <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Em Olá **iniciar instalador** , clique em **próximo**.
9. No instalador do adaptador Olá multi-Factor Authentication AD FS, clique em **próximo**.
10. Clique em **fechar** quando a instalação de saudação for concluída.
11. Quando adaptador Olá tiver sido instalado, você deve registrá-lo com o AD FS. Abra o Windows PowerShell e execute Olá comando a seguir:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse seu adaptador registrado recentemente, Editar política de autenticação global de saudação do AD FS. No console de gerenciamento do hello AD FS, acesse toohello **políticas de autenticação** nó. Em Olá **multi-factor Authentication** seção, clique em Olá **editar** link próximo toohello **configurações globais** seção. Em Olá **Editar política de autenticação Global** janela, selecione **multi-Factor Authentication** como um método de autenticação adicional e clique **Okey**. Olá adaptador é registrado como WindowsAzureMultiFactorAuthentication. Reinicie serviço do hello AD FS para efeito de tootake de registro de saudação.

<center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

Neste ponto, o servidor de autenticação multifator é configurado toobe um toouse de provedor de autenticação adicional com o AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Instalar uma instância autônoma do adaptador de saudação do AD FS usando o SDK do serviço Web de saudação
1. Instale Olá SDK do serviço Web no servidor de saudação que está executando o servidor multi-Factor Authentication.
2. A seguir Olá copiar arquivos de Olá \Program Files\Multi-servidor Factor Authentication diretório toohello em que planeje adaptador do tooinstall Olá AD FS:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Execute o arquivo de instalação do hello MultiFactorAuthenticationAdfsAdapterSetup64.msi.
4. No instalador do adaptador Olá multi-Factor Authentication AD FS, clique em **próximo** toostart instalação de saudação.
5. Clique em **fechar** quando a instalação de saudação for concluída.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Editar o arquivo multifactorauthenticationadfsadapter. config de saudação
Execute o arquivo de Multifactorauthenticationadfsadapter essas etapas tooedit hello:

1. Saudação de conjunto **UseWebServiceSdk** nó muito**true**.  
2. Definir valor Olá **WebServiceSdkUrl** toohello URL de saudação SDK do serviço de Web do multi-Factor Authentication. Por exemplo: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, onde *certificatename* é o nome de saudação do seu certificado.  
3. Edite o script hello Register-multifactorauthenticationadfsadapter.ps1 adicionando *- ConfigurationFilePath &lt;caminho&gt;*  toohello final de saudação `Register-AdfsAuthenticationProvider` comando, onde  *&lt;caminho&gt;*  é o arquivo multifactorauthenticationadfsadapter. config do hello caminho completo toohello.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Configurar Olá SDK do serviço Web com um nome de usuário e senha
Há duas opções para configurar Olá SDK do serviço Web. Olá é primeiro com um nome de usuário e senha, Olá segundo com um certificado de cliente. Siga estas etapas para a opção primeira hello ou pular para Olá segundo.  

1. Definir valor Olá **WebServiceSdkUsername** tooan conta que seja membro de grupo de segurança PhoneFactor Admins de hello. Saudação de uso &lt;domínio&gt;&#92;&lt; nome de usuário&gt; formato.  
2. Definir valor Olá **WebServiceSdkPassword** toohello senha de conta apropriada.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Configurar Olá SDK do serviço Web com um certificado de cliente
Se você não quiser toouse um nome de usuário e senha, siga a saudação de tooconfigure essas etapas SDK do serviço Web com um certificado de cliente.

1. Obter um certificado de cliente de uma autoridade de certificação para o servidor de saudação que está executando o hello SDK do serviço Web. Saiba como muito[obter certificados de cliente](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importação Olá cliente certificado toohello local repositório de certificados pessoal no servidor de saudação que está executando o hello SDK do serviço Web. Verifique se o que certificado público da autoridade de certificação que hello está no repositório de certificados de certificados de raiz confiável.  
3. Exporte chaves públicas e privadas de Olá Olá cliente tooa. pfx do arquivo de certificado.  
4. Exporte a chave pública Olá no arquivo. cer do Base64 formato tooa.  
5. No Gerenciador do servidor, verifique se que esse recurso de autenticação de mapeamento de certificado de cliente \Web Server\Security\IIS Olá servidor Web (IIS) está instalado. Se não estiver instalado, selecione **adicionar funções e recursos** tooadd esse recurso.  
6. No Gerenciador do IIS, clique duas vezes em **Editor de configuração** no site de saudação que contém o diretório virtual do SDK do serviço Web hello. É importante tooselect Olá site, diretório virtual não hello.  
7. Vá toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** seção.  
8. Defina enabled muito**true**.  
9. Defina oneToOneCertificateMappingsEnabled muito**true**.  
10. Clique em Olá **...**  botão Avançar toooneToOneMappings e clique em Olá **adicionar** link.  
11. Abra o arquivo. cer de Base64 Olá exportado anteriormente. Remova *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* e todas as quebras de linha. Copie a cadeia de caracteres resultante hello.  
12. Cadeia de caracteres do conjunto de certificado toohello copiadas Olá anterior da etapa.  
13. Defina enabled muito**true**.  
14. Defina userName tooan conta que seja membro de grupo de segurança PhoneFactor Admins de hello. Saudação de uso &lt;domínio&gt;&#92;&lt; nome de usuário&gt; formato.  
15. Definir senha de conta apropriada Olá senha toohello e, em seguida, feche o Editor de configuração.  
16. Clique em Olá **aplicar** link.  
17. Diretório virtual do SDK do serviço Web de saudação, clique duas vezes em **autenticação**.  
18. Verifique se a autenticação básica e representação do ASP.NET estão definidas muito**habilitado**, e todos os outros itens definidos muito**desabilitado**.  
19. Diretório virtual do SDK do serviço Web de saudação, clique duas vezes em **configurações de SSL**.  
20. Defina certificados de cliente muito**aceitar**e, em seguida, clique em **aplicar**.  
21. Copie o arquivo do hello. pfx exportado anterior servidor toohello executando Olá adaptador do AD FS.  
22. Importar o repositório de certificados pessoais do hello. pfx arquivo toohello computador local.  
23. Clique com botão direito e selecione **gerenciar chaves privadas**e, em seguida, conceder acesso de leitura toohello à conta usada toosign no serviço do toohello AD FS.  
24. Abrir Olá cliente certificado e cópia Olá a impressão digital de saudação **detalhes** guia.  
25. No arquivo multifactorauthenticationadfsadapter. config de hello, defina **WebServiceSdkCertificateThumbprint** toohello de cadeia de caracteres copiada na etapa anterior hello.  

Por fim, tooregister Olá adaptador, execute \Program Files\Multi Olá-script Factor Authentication\register-multifactorauthenticationadfsadapter.ps1 no PowerShell. Olá adaptador é registrado como WindowsAzureMultiFactorAuthentication. Reinicie serviço do hello AD FS para efeito de tootake de registro de saudação.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteger recursos do Azure AD usando o AD FS
toosecure seu recurso de nuvem, configurar uma regra de declarações para que os serviços de Federação do Active Directory emite a declaração de multipleauthn hello quando um usuário executa a verificação em duas etapas com êxito. Esta declaração é passada no tooAzure AD. Siga este toowalk procedimento etapas hello:

1. Abra o gerenciamento do AD FS.
2. Olá esquerda, selecione **terceira parte confiável**.
3. Clique com o botão direito do mouse na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Declaração...**

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Em Regras de Transformação de Emissão, clique em **Adicionar Regra.**

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **passar ou filtrar uma declaração de entrada** de Olá suspensa e clique em **próximo**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Dê um nome para a regra.
7. Selecione **referências de métodos de autenticação** como Olá entrada o tipo de declaração.
8. Selecione **Passar todos os valores de declaração**.
    ![Assistente para Adicionar Regra de Declaração de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Clique em **Concluir**. Feche o console de gerenciamento FS Olá AD.

## <a name="related-topics"></a>Tópicos relacionados
Para obter ajuda de solução de problemas, consulte Olá [perguntas frequentes sobre o Azure multi-Factor Authentication](multi-factor-authentication-faq.md)
