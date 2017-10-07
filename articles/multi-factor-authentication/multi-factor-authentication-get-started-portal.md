---
title: portal de aaaUser para o servidor Azure MFA | Microsoft Docs
description: "Esta é hello Azure multi-factor authentication página que descreve como tooget iniciada com o Azure MFA e o portal do usuário hello."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portal do usuário para Olá servidor Azure multi-Factor Authentication

portal de saudação do usuário é um site do IIS que permite que os usuários tooenroll no Azure multi-Factor Authentication (MFA) e mantenham suas contas. Um usuário pode alterar o número de telefone, alterar o PIN ou escolha toobypass verificação em duas etapas durante seu próximo logon no.

Os usuários entrar no portal do usuário toohello com seu nome de usuário normal e a senha, em seguida, conclua uma chamada de verificação em duas etapas ou responder toocomplete de perguntas de segurança a autenticação. Se o registro de usuário é permitido, usuários configure seu número de telefone e saudação PIN pela primeira vez que entrar no portal do usuário toohello.

Portal de usuário administradores pode estar definido e concedeu permissão tooadd novos usuários e atualizar usuários existentes.

Dependendo do seu ambiente, convém portal do usuário Olá toodeploy em Olá mesmo servidor como servidor de autenticação multifator do Azure ou em outro servidor voltado para a internet.

![Portal do usuário MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portal do usuário Olá só está disponível com o servidor de autenticação multifator. Se você usar o multi-Factor Authentication na nuvem hello, consulte seu toohello usuários [sua conta para verificação em duas etapas de configuração](./end-user/multi-factor-authentication-end-user-first-time.md) ou [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Instalar o SDK do serviço web Olá

Em qualquer cenário, se hello SDK do serviço Web do Azure multi-Factor Authentication é **não** já instalado no hello servidor Azure multi-Factor Authentication (MFA), seguir as etapas de saudação concluída.

1. Abra o console do servidor multi-Factor Authentication hello.
2. Vá toohello **SDK do serviço Web** e selecione **instalar o SDK do serviço Web**.
3. Instalação concluída hello usando padrões de saudação, a menos que você precisa toochange-los por alguma razão.
4. Vincule a um site de toohello do certificado SSL no IIS.

Se você tiver dúvidas sobre como configurar um certificado SSL em um servidor IIS, consulte o artigo Olá [como tooSet o SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Olá SDK do serviço Web deve ser protegido com um certificado SSL. Um certificado autoassinado é suficiente para essa finalidade. Importe o certificado de Olá no repositório de "Autoridades de certificação confiáveis" Olá Olá Local da conta do computador no servidor de web do Portal do usuário Olá para que ele confia no certificado ao iniciar a conexão de SSL hello.

![SDK do serviço Web de configuração do Servidor MFA](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Implantar o portal de usuário Olá Olá mesmo servidor Olá servidor Azure multi-Factor Authentication

Hello, pré-requisitos a seguir são portal do usuário Olá tooinstall necessária em Olá **mesmo servidor** como Olá servidor Azure multi-Factor Authentication:

* O IIS, incluindo a compatibilidade da metabase do IIS 6 e ASP.NET (para o IIS 7 ou superior)
* Uma conta com direitos de administrador para o computador hello e domínio, se aplicável. conta de saudação precisa de grupos de segurança do Active Directory de toocreate de permissões.
* Portal do usuário Olá seguro com um certificado SSL.
* Proteger a saudação SDK do serviço Web do Azure multi-Factor Authentication com um certificado SSL.

toodeploy Olá siga portal, usuário estas etapas:

1. Abra o console do servidor Azure multi-Factor Authentication hello, clique em Olá **Portal do usuário** menu à esquerda do ícone no hello, em seguida, clique em **instalar Portal do usuário**.
2. Instalação concluída hello usando padrões de saudação, a menos que você precisa toochange-los por alguma razão.
3. Vincular a um site de toohello do certificado SSL no IIS

   > [!NOTE]
   > Esse Certificado SSL é geralmente um Certificado SSL assinado publicamente.

4. Abra um navegador da web de qualquer computador e navegue toohello URL onde o portal do usuário Olá foi instalado (exemplo: https://mfa.contoso.com/MultiFactorAuth). Certifique-se de que nenhum aviso de certificado ou erro seja exibido.

![Instalação do portal de usuário do Servidor MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Se você tiver dúvidas sobre como configurar um certificado SSL em um servidor IIS, consulte o artigo Olá [como tooSet o SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Implantar o portal de saudação do usuário em um servidor separado

Se o servidor Olá onde o servidor Azure multi-Factor Authentication está sendo executado não é voltado para a internet, você deve instalar o portal do usuário Olá em um **servidor separado, voltados para internet**.

Se sua organização usa Olá aplicativo Authenticator da Microsoft como um dos métodos de verificação hello e deseja portal do usuário Olá toodeploy em seu próprio servidor, conclua Olá requisitos a seguir:

* Use v 6.0 ou posterior do hello servidor Azure multi-Factor Authentication.
* Instalar o portal de saudação do usuário em um servidor de web voltados para internet executando o Microsoft internet Information Services (IIS) 6. x ou superior.
* Ao usar o IIS 6. x, verifique se o ASP.NET v 2.0.50727 está instalado, registrado e definido muito**permitidos**.
* Ao usar o IIS 7.x ou superior, o IIS, incluindo autenticação básica, ASP.NET e compatibilidade de metabase com o IIS 6.
* Portal do usuário Olá seguro com um certificado SSL.
* Proteger a saudação SDK do serviço Web do Azure multi-Factor Authentication com um certificado SSL.
* Certifique-se de que esse portal saudação do usuário pode se conectar a toohello SDK do serviço Web do Azure multi-Factor Authentication sobre SSL.
* Certifique-se de que esse portal do usuário Olá pode autenticar toohello SDK do serviço Web do Azure multi-Factor Authentication usando as credenciais de saudação de uma conta de serviço no grupo de segurança "Administradores" hello. Essa conta de serviço e o grupo devem existir no Active Directory se Olá servidor Azure multi-Factor Authentication estiver em execução em um servidor ingressado no domínio. Essa conta de serviço e o grupo existem localmente no hello servidor Azure multi-Factor Authentication se não for tooa ingressado no domínio.

Instalar portal do usuário Olá em um servidor diferente Olá servidor Azure multi-Factor Authentication requer Olá etapas a seguir:

1. **No servidor MFA de saudação**, Procurar caminho de instalação do toohello (exemplo: C:\Program programas\Servidor multi-Factor Authentication Server) e copiar o arquivo de saudação **MultiFactorAuthenticationUserPortalSetup64** tooa local toohello acessível o servidor da internet onde ele será instalado.
2. **No servidor de web voltados para internet Olá**, execute o arquivo de instalação de saudação MultiFactorAuthenticationUserPortalSetup64 como um administrador, alterar Olá Site se desejado e altere o nome curto de tooa Olá de diretório Virtual se você deseja.
3. Vincule a um site de toohello do certificado SSL no IIS.

   > [!NOTE]
   > Esse Certificado SSL é geralmente um Certificado SSL assinado publicamente.

4. Procurar muito**C:\inetpub\wwwroot\MultiFactorAuth**
5. Editar o arquivo Web. config de saudação no bloco de notas

    * Localizar chave Olá **"USE_WEB_SERVICE_SDK"** e alterar **valor = "false"** muito**valor = "true"**
    * Localizar chave Olá **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** e alterar **valor = ""** muito**valor = "Domínio \ usuário"** onde o domínio é uma conta de serviço que faz parte de Grupo "Administradores".
    * Localizar chave Olá **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** e alterar **valor = ""** muito**valor = "Senha"** onde a senha é senha Olá Olá serviço Conta inserida na linha anterior hello.
    * Localize o valor de saudação **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** e altere essa URL de espaço reservado toohello URL do SDK do serviço Web são instalados na etapa 2.
    * Salve o arquivo Web. config de saudação e feche o bloco de notas.

6. Abra um navegador da web de qualquer computador e navegue toohello URL onde o portal do usuário Olá foi instalado (exemplo: https://mfa.contoso.com/MultiFactorAuth). Certifique-se de que nenhum aviso de certificado ou erro seja exibido.

Se você tiver dúvidas sobre como configurar um certificado SSL em um servidor IIS, consulte o artigo Olá [como tooSet o SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurar definições do portal de usuário no servidor Azure multi-Factor Authentication da saudação

Agora esse portal do usuário Olá estiver instalado, você precisa tooconfigure Olá servidor Azure multi-Factor Authentication toowork com o portal de saudação.

1. No console do servidor Azure multi-Factor Authentication hello, clique em Olá **Portal do usuário** ícone. Na guia Configurações de Olá, insira o portal do usuário Olá URL toohello no Olá **URL do Portal do usuário** caixa de texto. Se tiver sido habilitada a funcionalidade de email, essa URL está incluído nos emails de saudação enviadas toousers quando eles são importados para Olá servidor Azure multi-Factor Authentication.
2. Escolha as configurações de saudação que você deseja toouse em Olá Portal do usuário. Por exemplo, se os usuários têm permissão toochoose os métodos de autenticação, certifique-se de que **permitir que os usuários tooselect método** estiver marcada, junto com os métodos de saudação que pode escolher.
3. Definir quem deve ser administradores em Olá **administradores** guia. Você pode criar permissões administrativas granulares usando Olá caixas de seleção e listas suspensas nas caixas de Adicionar/Editar saudação.

Configuração opcional:
- **Perguntas de segurança** -definir aprovadas perguntas de segurança para o idioma do ambiente e hello aparecem no.
- **Sessões Passadas**: configure a integração do portal do usuário com um site baseado em formulário usando a MFA.
- **IPs confiáveis** -permitir que usuários tooskip MFA quando a autenticação de uma lista de trusted IPs ou intervalos.

![Configuração do portal de usuário do Servidor MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Servidor de autenticação multifator do Azure fornece várias opções para o portal do usuário hello. Olá tabela a seguir fornece uma lista dessas opções e uma explicação do que elas são usadas.

| Configurações do Portal de Usuário | Descrição |
|:--- |:--- |
| URL do portal do usuário | Insira a URL de saudação do onde portal hello está sendo hospedado. |
| Autenticação primária | Especifique o tipo de saudação de autenticação toouse ao entrar no portal de toohello. Autenticação do Windows, Radius ou LDAP. |
| Permitir que os usuários toolog em | Permitir que usuários tooenter um nome de usuário e senha na página entrada Olá Olá para portal do usuário. Se essa opção não estiver selecionada, as caixas de saudação estão esmaecidas. |
| Permitir registro de usuário | Permitem que um usuário tooenroll na autenticação multifator fazendo-los tooa de tela de instalação que solicita-los para obter informações adicionais, como o número de telefone. Solicite telefone de backup permite que os usuários toospecify um número de telefone secundário. Prompt para terceiros token OATH permite que os usuários toospecify um token OATH de terceiros. |
| Permitir que os usuários tooinitiate Bypass avulso | Permitir que usuários tooinitiate um desvio único. Se um usuário configura essa opção, levará Olá efeito próximo tempo Olá usuário faz logon. Prompt para ignorar segundos fornece Olá usuário uma caixa para que eles podem alterar o padrão de saudação de 300 segundos. Caso contrário, o bypass avulso Olá só é bom para 300 segundos. |
| Permitir que os usuários tooselect método | Permitir que usuários toospecify o método de contato principal. Esse método pode ser uma chamada telefônica, uma mensagem de texto, um aplicativo móvel ou token OATH. |
| Permitir que os usuários tooselect idioma | Permitir que os usuários toochange idioma de saudação que é usado para Olá telefonema, mensagem de texto, aplicativo móvel ou token OATH. |
| Permitir que o aplicativo móvel de tooactivate de usuários | Permitir que usuários toogenerate um código toocomplete Olá aplicativo móvel ativação processo de ativação que é usado com o servidor de saudação.  Você também pode definir o número de saudação de dispositivos que eles podem ativar aplicativo hello, entre 1 e 10. |
| Usar perguntas de segurança para fallback | Permita perguntas de segurança caso a verificação em duas etapas falhe. Você pode especificar o número de saudação de perguntas de segurança que devem ser respondidas com sucesso. |
| Permitir que o token OATH de terceiros usuários tooassociate | Permitir que os usuários toospecify um token OATH de terceiros. |
| Usar token OATH para fallback | Permitir uso de saudação de um token OATH no caso de verificação em duas etapas não for bem-sucedida. Você também pode especificar o tempo limite da sessão Olá em minutos. |
| Habilitar o registro em log | Habilite registro em log no portal do usuário hello. Olá arquivos de log estão localizados em: C:\Program programas\Servidor multi-Factor Authentication server\logs.. |

Essas configurações se tornam visíveis toohello usuário no portal de saudação depois que elas estão habilitadas e são assinados no portal do usuário toohello.

![Configurações do Portal de Usuário](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Registro de usuário de autoatendimento

Se você quiser toosign seus usuários e registra, você deve selecionar Olá **permitem que os usuários toolog em** e **permitir a inscrição de usuário** opções na guia Configurações de saudação. Lembre-se de selecionar as configurações de saudação afetam experiência de entrada do usuário de saudação.

Por exemplo, quando um usuário entra no portal do usuário toohello para Olá primeira vez, eles são realizados toohello página de configuração de usuário do Azure multi-Factor Authentication. Dependendo de como você configurou a autenticação multifator do Azure, o usuário Olá pode ser capaz de tooselect seu método de autenticação.

Se selecionar o método de verificação de chamada de voz hello ou ter sido previamente configurada toouse esse método, página Olá solicita Olá usuário tooenter seu número de telefone principal e extensão, se aplicável. Eles também podem ser permitidos tooenter um número de telefone de backup.

![Registrar números de telefone principal e de backup](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Se o usuário de saudação toouse necessário um PIN ao autenticar, página Olá solicita toocreate um PIN. Depois de inserir seus números de telefone e PIN (se aplicável), o usuário de saudação clica Olá **tooAuthenticate chamar agora** botão. Número de telefone principal do usuário uma chamada telefônica verificação toohello executa a autenticação multifator do Azure. usuário Olá deve responder Olá telefonema e inserir o PIN (se aplicável) e pressione # toomove no toohello próxima etapa do processo de autoinscrição hello.

Se o usuário Olá seleciona o método de verificação de mensagem de texto de saudação ou tiver sido pré-configurado toouse esse método, página Olá solicita usuário Olá seu número de telefone celular. Se usuário Olá toouse necessário um PIN ao autenticar, Olá página também solicita que eles tooenter um PIN.  Depois de inserir o número de telefone e PIN (se aplicável), o usuário de saudação clica Olá **tooAuthenticate texto para mim agora** botão. Celular do usuário um SMS verificação toohello executa a autenticação multifator do Azure. Olá usuário recebe a mensagem de texto de saudação com uma única-tempo OTP (senha), em seguida, mensagem de toohello respostas com esta OTP mais seu PIN (se aplicável).

![SMS do portal do usuário](./media/multi-factor-authentication-get-started-portal/text.png)

Se o usuário Olá seleciona o método de verificação de aplicativo móvel hello, página Olá solicita o aplicativo hello usuário tooinstall Olá Microsoft Authenticator em seu dispositivo e gerar um código de ativação. Depois de instalar o aplicativo hello, Olá clicado botão Gerar código de ativação de saudação.

> [!NOTE]
> toouse Olá Microsoft Authenticator aplicativo, usuário Olá deve habilitar notificações por push para seu dispositivo.

Olá página exibe um código de ativação e uma URL com uma imagem de código de barras. Se usuário Olá toouse necessário um PIN ao autenticar, página Olá Além disso solicita tooenter um PIN. usuário Olá entra Olá código de ativação e URL no aplicativo do Microsoft Authenticator hello ou usa imagem de código de barras Olá código de barras scanner tooscan hello e cliques de botão de ativar hello.

Após a conclusão da ativação hello, Olá clicado Olá **autentique-Me agora** botão. Autenticação multifator do Azure executa o aplicativo móvel do usuário toohello uma verificação. usuário Olá deve inserir seu PIN (se aplicável) e pressione o botão de autenticar de saudação em seu aplicativo móvel toomove em toohello próxima etapa do processo de autoinscrição Olá.

Se tem configurado a administradores Olá Olá servidor Azure multi-Factor Authentication toocollect segurança perguntas e respostas, Olá usuário é levado toohello página de perguntas de segurança. usuário de saudação deve selecionar quatro perguntas de segurança e fornecer respostas a perguntas tootheir selecionado.

![Perguntas de segurança do portal do usuário](./media/multi-factor-authentication-get-started-portal/secq.png)

autorregistro do usuário Olá agora está concluído e Olá usuário está conectado no portal do usuário toohello. Usuários possam entrar no portal do usuário toohello a qualquer momento no toochange futuras Olá seus números de telefone, PINs, métodos de autenticação e perguntas de segurança se alterar seus métodos é permitido pelos seus administradores.

## <a name="next-steps"></a>Próximas etapas

- [Implantar hello Azure multi-Factor Authentication Server Mobile serviço de aplicativo Web](multi-factor-authentication-get-started-server-webservice.md)
