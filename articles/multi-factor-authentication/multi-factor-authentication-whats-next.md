---
title: aaaConfigure MFA do Azure | Microsoft Docs
description: "Esta é hello Azure multi-factor authentication página que descreve quais toodo lado com MFA.  Isso inclui relatórios, alerta de fraude, desvio único, mensagens de voz personalizadas, cache, senhas de ips e aplicativos confiáveis."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: 7f6d0b0975a2c1da2de9b52e978b84475c79b218
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Configurar a Autenticação Multifator do Azure
Este artigo ajuda a gerenciar o Autenticação Multifator do Azure, agora que tudo está funcionando.  Ele abrange vários tópicos que ajudarão a saudação tooget mais fora do Azure multi-Factor Authentication.  Alguns desses recursos não estão disponíveis em todas as versões da Autenticação Multifator do Azure.

| Recurso | Descrição | 
|:--- |:--- |
| [Alerta de fraude](#fraud-alert) |Alerta de fraude pode ser definida e configurada para que os usuários podem relatar tentativas fraudulentas tooaccess seus recursos. |
| [Desvio único](#one-time-bypass) |Um bypass avulso permite tooauthenticate um usuário uma vez por "Ignorar" autenticação multifator. |
| [Mensagens de voz personalizadas](#custom-voice-messages) |Mensagens de voz personalizadas permitem que você toouse sua própria gravações ou saudações com autenticação multifator. |
| [Cache](#caching-in-azure-multi-factor-authentication) |O cache permite que você tooset um período de tempo específico para que as tentativas de autenticação subsequentes tenha êxito automaticamente. |
| [IPs Confiáveis](#trusted-ips) |Os administradores de um locatário gerenciado ou federado podem usar IPs confiáveis toobypass verificacao de usuários que entram da intranet local da empresa hello. |
| [Senhas de aplicativo](#app-passwords) |Uma senha de aplicativo permite que um aplicativo que não seja a autenticação multifator toobypass com reconhecimento de MFA e continuar trabalhando. |
| [Lembrar da Autenticação Multifator para dispositivos e navegadores lembrados](#remember-multi-factor-authentication-for-devices-that-users-trust) |Permite que você tooremember dispositivos para um determinado número de dias depois que um usuário entrou com êxito usando o MFA. |
| [Métodos de verificação selecionáveis](#selectable-verification-methods) |Permite que você toochoose métodos de autenticação de saudação que estão disponíveis para usuários toouse. |

## <a name="access-hello-azure-mfa-management-portal"></a>Acessar o Portal de gerenciamento de MFA de saudação

recursos de saudação abordados neste artigo são configurados no Portal de gerenciamento do Azure multi-Factor Authentication da saudação. Há duas maneiras tooaccess Olá portal de gerenciamento de MFA por meio de saudação portal clássico do Azure. Olá primeiro é por meio do gerenciamento de um provedor de autenticação multifator. Olá segundo é por meio de configurações do serviço MFA de saudação. 

### <a name="use-an-auth-provider"></a>Usar um provedor de autenticação

Se você usar um provedor de autenticação multifator para MFA com base em consumo, use este portal de gerenciamento do método tooaccess hello.

tooaccess Olá Portal de gerenciamento de MFA por meio de um provedor de autenticação multifator do Azure, entrar Olá portal clássico do Azure como um administrador e a opção do Active Directory Olá select. Clique em Olá **provedores de autenticação multifator** guia, selecione seu diretório e clique em Olá **gerenciar** botão na parte inferior da saudação.

### <a name="use-hello-mfa-service-settings-page"></a>Use a página de configurações do serviço de MFA de saudação 

Se você tiver um provedor de autenticação multifator ou um Azure MFA, o Azure AD Premium, ou Enterprise Mobility + licença de segurança, use esta página de configurações do método tooaccess Olá MFA serviço.

tooaccess Olá Portal de gerenciamento de MFA por meio da página de configurações do serviço de MFA, o logon no portal clássico do Azure como um administrador de saudação do hello e selecione opção do Active Directory hello. Clique no diretório e, em seguida, clique em Olá **configurar** guia. Na seção de autenticação multifator hello, selecione **gerenciar configurações de serviço**. Na parte inferior de saudação da página de configurações do serviço de MFA de saudação, clique em Olá **Go toohello portal** link.


## <a name="fraud-alert"></a>Alerta de fraude
Alerta de fraude pode ser definida e configurada para que os usuários podem relatar tentativas fraudulentas tooaccess seus recursos.  Os usuários podem relatar fraude com aplicativo móvel hello ou por meio de seu telefone.

### <a name="set-up-fraud-alert"></a>Configurar o alerta de fraude
1. Navegue toohello Portal de gerenciamento de MFA por instruções de saudação na parte superior da saudação desta página.
2. No Portal de gerenciamento do Azure multi-Factor Authentication do hello, clique em **configurações** na seção Configuração de saudação.
3. Em Olá alerta de fraude seção da página de configurações de saudação, verifique Olá **permitem que os usuários alertas de fraudes toosubmit** caixa de seleção.
4. Selecione **salvar** tooapply suas alterações. 

### <a name="configuration-options"></a>Opções de configuração

- **Bloquear usuário quando fraude for relatada** - se de um usuário relatar uma fraude, sua conta será bloqueada.
- **Código tooReport fraude durante a saudação inicial** -os usuários normalmente pressionam verificação do # tooconfirm em duas etapas. Se desejar tooreport fraude, eles inserir um código antes de pressionar #. Esse código é **0** por padrão, mas você pode personalizá-lo.

> [!NOTE]
> Saudações de voz padrão da Microsoft, instrua os usuários toopress 0# toosubmit um alerta de fraude. Se você quiser toouse um código diferente de 0, você deve registrar e carregar seus próprio saudações de voz personalizadas com as instruções apropriadas.

![Opções de alerta de fraude - captura de tela](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Como os usuários podem relatar fraudes 
O alerta de fraude pode ser informado de duas maneiras.  Um por meio de aplicativos móveis hello ou telefone hello.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Relatar fraude com aplicativo móvel Olá
1. Quando uma verificação é enviada tooyour telefone, selecione tooopen Olá Microsoft Authenticator aplicativo.
2. Selecione **Deny** na notificação de saudação. 
3. Clique em **Relatar fraude**.
4. Aplicativo hello fechar.

#### <a name="report-fraud-with-a-phone"></a>Relatar fraude com um telefone
1. Quando uma chamada de verificação chega tooyour telefone, atenda-o.  
2. tooreport fraude, insira o código de fraude hello (o padrão é 0) e, em seguida, Olá sinal #. Você será notificado de que um alerta de fraude foi enviado.
3. Encerrar a chamada de saudação.

### <a name="view-fraud-reports"></a>Exibir relatórios de fraude
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Olá esquerda, selecione Active Directory.
3. Em select top Olá **provedores de autenticação multifator**. Isso trará uma lista de seus provedores de autenticação multifator.
4. Selecione o provedor de autenticação multifator e clique em **gerenciar** final Olá Olá página. Olá Portal de gerenciamento do Azure multi-Factor Authentication é aberto.
5. No hello Azure multi-Factor Authentication Portal de gerenciamento, em Exibir um relatório, clique em **alerta de fraude**.
6. Especifique o intervalo de datas de saudação que você deseja tooview no relatório de saudação. Você também pode especificar nomes de usuário, números de telefone e status de saudação do usuário.
7. Clique em **Executar**. Isso abre um relatório de alertas de fraude. Clique em **exportar tooCSV** se desejar que o relatório de saudação tooexport.

## <a name="one-time-bypass"></a>Desvio único
Um bypass avulso permite que um usuário tooauthenticate uma única vez sem realizar a verificação em duas etapas. Olá bypass é temporário e expira após um número especificado de segundos. Em situações em que aplicativo móvel hello ou telefone não está recebendo uma notificação ou chamada telefônica, você pode habilitar um desvio único para que usuário Olá possa acessar recursos de saudação desejado.

### <a name="create-a-one-time-bypass"></a>Criar um bypass avulso
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue toohello Portal de gerenciamento de MFA por instruções de saudação na parte superior da saudação desta página.
3. No hello Portal de gerenciamento do Azure multi-Factor Authentication, se você vir o nome de saudação do seu locatário ou o provedor do Azure MFA no hello esquerda com um  **+**  tooit Avançar, clique em Olá  **+**  Consulte diferentes grupos de replicação do servidor MFA e o grupo de saudação padrão do Azure. Selecione grupo apropriado hello.
4. Em Administração do Usuário, clique em **Bypass Avulso**.
5. Na página de Bypass avulso hello, clique em **novo desvio único**.

  ![Nuvem](./media/multi-factor-authentication-whats-next/create1.png)

6. Insira o nome de usuário de saudação, o número de Olá de segundos que Olá bypass será existe e Olá motivo para ignorar hello. Clique em **Bypass**.
7. Olá tempo limite entra em vigor imediatamente, portanto usuário Olá toosign necessidades em antes de saudação avulsa bypass expira. 

### <a name="view-hello-one-time-bypass-report"></a>Saudação de exibição única ignorar o relatório
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Olá esquerda, selecione Active Directory.
3. Em select top Olá **provedores de autenticação multifator**. Isso trará uma lista de seus provedores de autenticação multifator.
4. Selecione o provedor de autenticação multifator e clique em **gerenciar** final Olá Olá página. Olá Portal de gerenciamento do Azure multi-Factor Authentication é aberto.
5. No Portal de gerenciamento do Azure multi-Factor Authentication de Olá Olá esquerda, em Exibir um relatório, clique em **Bypass avulso**.
6. Especifique o intervalo de datas de saudação que você deseja tooview no relatório de saudação. Você também pode especificar nomes de usuário, números de telefone e status de saudação do usuário.
7. Clique em **Executar**. Isso abre um relatório de bypasses. Clique em **exportar tooCSV** se desejar que o relatório de saudação tooexport.

## <a name="custom-voice-messages"></a>Mensagens de voz personalizadas
Mensagens de voz personalizadas permitem que você toouse sua própria gravações ou saudações de verificação em duas etapas. Elas podem ser usadas em registros da Microsoft hello adição tooor tooreplace.

Antes de começar a estar ciente do seguinte hello:

* formatos de arquivo Hello com suporte são. wav e. mp3.
* limite de tamanho de arquivo Hello é 5 MB.
* As mensagens de autenticação devem ter menos de 20 segundos. Nada mais do que isso poderia causar Olá verificação toofail porque o usuário Olá pode não responder antes Olá mensagem concluído, provocando Olá verificação tootime-out.

### <a name="set-up-a-custom-message"></a>Configurar uma mensagem personalizada

Há dois toocreating de partes de sua mensagem personalizada. Primeiro, você carrega a mensagem de saudação e, em seguida, ligá-lo para seus usuários.

tooupload sua mensagem personalizada:

1. Crie uma mensagem de voz personalizada usando um dos formatos de arquivo hello com suporte.
2. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
3. Navegue toohello Portal de gerenciamento de MFA por instruções de saudação na parte superior da saudação desta página.
4. No Portal de gerenciamento do Azure multi-Factor Authentication do hello, clique em **mensagens de voz** na seção Configuração de saudação.
5. Em Olá configurar: página de mensagens de voz, clique em **nova mensagem de voz**.
   ![Nuvem](./media/multi-factor-authentication-whats-next/custom1.png)
6. Em Olá configurar: página novas mensagens de voz, clique em **gerenciar arquivos de som**.
   ![Nuvem](./media/multi-factor-authentication-whats-next/custom2.png)
7. Em Olá configurar: página arquivos de som, clique em **carregar arquivo de som**.
   ![Nuvem](./media/multi-factor-authentication-whats-next/custom3.png)
8. Em Olá configurar: carregar o arquivo de som, clique em **procurar** e navegue tooyour mensagem de voz, clique em **abrir**.
9. Adicione uma Descrição e clique em **Carregar**.
10. Depois que isso for concluído, uma mensagem confirmará que você carregou com êxito arquivo hello.

mensagem de saudação tooturn em para seus usuários:

1. Olá esquerda, clique em **mensagens de voz**.
2. Em Olá seção de mensagens de voz, clique em **nova mensagem de voz**.
3. De Olá suspenso idioma, selecione um idioma.
4. Se essa mensagem for para um aplicativo específico, especifique-o na caixa de saudação do aplicativo.
5. Na lista suspensa tipo de mensagem de saudação, selecione toobe de tipo de mensagem hello substituído com sua nova mensagem personalizada.
6. De Olá suspensa do arquivo de som, selecione o arquivo de som de saudação que você carregou na primeira parte do hello.
7. Clique em **Criar**. Uma mensagem confirma que você criou com êxito uma mensagem de voz.
    ![Nuvem](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Cache na Autenticação Multifator do Azure
O cache permite que você tooset um período de tempo específico para que as tentativas de autenticação subsequentes dentro desse período de tempo tenha êxito automaticamente. Isso é usado principalmente quando os sistemas locais, como VPN enviam várias solicitações de verificação durante a primeira solicitação de saudação ainda está em andamento. Isso permite Olá solicitações subsequentes toosucceed automaticamente após usuário Olá concluído com êxito a verificação primeiro Olá em andamento. 

O cache não é pretendido toobe usado para entradas tooAzure AD.

### <a name="set-up-caching"></a>Configurar o cache 
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue toohello Portal de gerenciamento de MFA por instruções de saudação na parte superior da saudação desta página.
3. No Portal de gerenciamento do Azure multi-Factor Authentication do hello, clique em **cache** na seção Configuração de saudação.
4. Na saudação Configurar página cache, clique em **novo Cache**.
5. Selecione o tipo de Cache hello e segundos de cache de saudação. Clique em **Criar**.

<center>![Nuvem](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>IPs confiáveis
IPs confiáveis é um recurso do Azure MFA que os administradores de um locatário gerenciado ou federado podem usar toobypass verificacao para usuários que estão entrando pela intranet local da empresa hello. Este recurso está disponível com a versão completa de saudação do Azure multi-Factor Authentication, não Olá versão gratuita para administradores. Para obter detalhes sobre como tooget Olá versão completa do Azure multi-Factor Authentication, consulte [Azure multi-Factor Authentication](multi-factor-authentication.md).

| Tipo de locatário do Azure AD | Opções disponíveis de IPs confiáveis |
|:--- |:--- |
| Gerenciada |<li>Intervalos de endereços IP específicos – os administradores podem especificar um intervalo de endereços IP que podem ignorar a verificação em duas etapas para usuários que estão entrando pela intranet da empresa hello.</li> |
| Federado |<li>Todos os usuários federados - todos os usuários federados que estão entrando de dentro de saudação organização vai ignorar a verificação em duas etapas usando uma declaração emitida pelo AD FS.</li><br><li>Intervalos de endereços IP específicos – os administradores podem especificar um intervalo de endereços IP que podem ignorar a verificação em duas etapas para usuários que estão entrando pela intranet da empresa hello. |

Esse desvio só funciona dentro da intranet da empresa. Por exemplo, se você selecionou usuários federados tudo, e um usuário entra intranet da empresa Olá fora, esse usuário tem tooauthenticate verificação em duas etapas usando o mesmo que o usuário Olá apresenta uma declaração do AD FS. 

**Experiência do usuário final dentro da rede corporativa:**

Quando o recurso IPs confiáveis estiver desabilitado, será necessário utilizar a verificação em duas etapas para fluxos de navegador e senhas de aplicativo para antigos aplicativos clientes avançados. 

Quando IPs confiáveis estiver habilitado, a verificação em duas etapas é *não* necessárias para fluxos de navegador e as senhas de aplicativo são *não* necessário para aplicativos de cliente avançado mais antigos, desde que hello usuário não já criou um senha do aplicativo. Se uma senha de aplicativo for usada, ela será necessária. 

**Experiência do usuário final fora da rede corporativa:**

Não importa se o recurso IPs confiáveis está habilitado ou não, será necessário utilizar a verificação em duas etapas para fluxos de navegador e senhas de aplicativo para antigos aplicativos clientes avançados. 

### <a name="tooenable-trusted-ips"></a>tooenable IPs confiáveis
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue a página de configurações do serviço de MFA toohello por instruções Olá início Olá deste artigo.
3. Na página de configurações do serviço de hello, em IPs confiáveis, você tem duas opções:
   
   * **Para solicitações de usuários federados provenientes da minha intranet** – caixa de saudação da seleção. Todos os usuários federados que estão fazendo logon rede corporativa Olá vão ignorar a verificação em duas etapas usando uma declaração emitida pelo AD FS.
   * **Para solicitações de um intervalo específico de IPs públicos** – digite os endereços IP de saudação na caixa de texto de saudação fornecida usando a notação CIDR. Por exemplo: xxx.xxx.xxx.0/24 para endereços IP da saudação intervalo xxx.xxx.xxx.1 – xxx.xxx.xxx. 254 ou xxx.xxx.xxx.xxx/32 para um único endereço IP. Você pode inserir até too50 os intervalos de endereços IP. Os usuários que acessam desses endereços IP ignoram verificação em duas etapas.
4. Clique em **Salvar**.
5. Depois de saudação atualizações foram aplicadas, clique em **fechar**.

![IPs confiáveis](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Senhas de aplicativo
Alguns aplicativos, como o Office 2010 ou anterior e o Apple Mail, não oferecem suporte à verificação em duas etapas. Eles não são tooaccept configurado uma verificação de segundo. toouse esses aplicativos, você precisa toouse "senhas de aplicativo" no lugar de sua senha tradicional. senha de aplicativo Hello permite Olá aplicativo toobypass verificação em duas etapas e continuar trabalhando.

> [!NOTE]
> Autenticação moderna para Olá clientes do Office 2013
> 
> Clientes do Office 2013 (incluindo Outlook) e protocolos de autenticação moderna de suporte mais recentes e pode ser habilitado toowork com verificação em duas etapas. Depois de habilitada, não será mais necessário fornecer as senhas de aplicativo para esses clientes.  Para saber mais, veja [Anúncio da visualização pública da autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Tooknow coisas importantes sobre senhas de aplicativo
a seguir Olá é uma lista importante de coisas que você deve saber sobre senhas de aplicativo.

* As senhas de aplicativo só será necessário toobe inserida uma vez por aplicativo. Os usuários não tem controle tookeep deles e inseri-las toda vez.
* senha real Olá é gerada automaticamente e não é fornecida pelo usuário hello. Isso ocorre porque a senha gerada automaticamente Olá é mais difícil para um invasor tooguess e é mais segura.
* Há um limite de 40 senhas por usuário. 
* Aplicativos que armazena em cache as senhas e uso em cenários locais pode começar a falhar, pois a senha de aplicativo hello não é conhecida fora de id organizacional hello. Um exemplo é emails do Exchange que estão no local, mas Olá arquivado ficam na nuvem Olá. Olá a mesma senha não funciona.
* Assim que a autenticação multifator é habilitada na conta de um usuário, as senhas do aplicativo podem ser usadas com a maioria dos clientes sem navegador, como Outlook e Lync, mas as ações administrativas não podem ser executadas usando senhas do aplicativo por meio de aplicativos sem navegador, como o Windows PowerShell, mesmo se o usuário tiver uma conta administrativa.  Certifique-se de criar uma conta de serviço com scripts do PowerShell de toorun uma senha forte e não habilitar essa conta para verificação em duas etapas.

> [!WARNING]
> As senhas de aplicativo não funcionam em ambientes híbridos onde os clientes se comunicam com pontos de extremidade de descoberta automática local e na nuvem. Isso ocorre porque senhas do domínio são necessários tooauthenticate local e as senhas de aplicativo são necessário tooauthenticate com a nuvem de saudação.

### <a name="naming-guidance-for-app-passwords"></a>Nomeando orientação para senhas de aplicativo
Nomes de senha de aplicativo reflitam Olá dispositivo no qual eles são usados. Por exemplo, se você tiver um laptop com aplicativos que não são navegadores, como Outlook, Word e Excel, basta criar uma senha de aplicativo chamada Laptop e usar essa senha em todos esses aplicativos. Em seguida, crie outra senha de aplicativo chamada área de trabalho para Olá mesmos aplicativos em seu computador desktop. 

A Microsoft recomenda criar uma senha de aplicativo por dispositivo, e não uma senha de aplicativo por aplicativo.

### <a name="federated-sso-app-passwords"></a>Senhas de aplicativo federado (SSO)
O Azure AD oferece suporte à federação (logon único) com os Serviços de Domínio do Active Directory Domain Services (AD DS) locais do Windows Server. Se sua organização for federada com o Azure AD e vai toobe usando o Azure multi-Factor Authentication, então Olá seguintes informações sobre senhas de aplicativo são importantes para você. Esta seção se aplica somente a clientes toofederated (SSO).

* As senhas de aplicativo são verificadas Azure AD e, portanto, ignoram a federação. A federação só é usada ativamente na configuração das senhas de aplicativo.
* Para os usuários federados (SSO), nunca vamos toohello provedor de identidade (IdP), ao contrário do fluxo passivo hello. Olá senhas são armazenadas na id organizacional hello. Se o usuário Olá deixa a empresa hello, essas informações tem tooflow tooorganizational id usando o DirSync em tempo real. Desabilitar/excluir a conta pode levar até toothree horas toosync, atrasando o desabilitar/excluir da senha do aplicativo no AD do Azure.
* As configurações do Controle de Acesso do Cliente local não são consideradas pela senha de aplicativo.
* Nenhum recurso de registro de autenticação/auditoria local está disponível para a Senha de aplicativo.
* Alguns projetos arquitetônicos avançados podem exigir o uso de uma combinação de nome de usuário e senhas da organização e senhas de aplicativo com a verificação em duas etapas em clientes, dependendo de onde eles são autenticados. Para clientes que fazem a autenticação em uma infraestrutura local, você usaria um nome de usuário e senha organizacional. Para clientes que autenticam no Azure AD, você usaria a senha de aplicativo hello.

  Por exemplo, suponha que você tem uma arquitetura que consiste Olá seguinte:

  * Você está federando sua instância local do Active Directory com o Azure AD
  * Você está usando o Exchange online
  * Você está usando o Lync que é especificamente local
  * Você está usando a Autenticação Multifator do Azure

  ![Prova](./media/multi-factor-authentication-whats-next/federated.png)

  Nesses casos, você deve fazer a seguir hello:

  * Quando a assinatura-no tooLync, use o nome de usuário e a senha de sua organização.
  * Durante a tentativa de catálogo de endereços de saudação tooaccess por meio de um cliente do Outlook que se conecta tooExchange online, use uma senha de aplicativo.

### <a name="allow-app-password-creation"></a>Permitir a criação de senha de aplicativo
Por padrão, os usuários não podem criar senhas de aplicativo. Esse recurso deve ser ativado. usuários tooallow Olá senhas de aplicativo toocreate de capacidade, use Olá procedimento a seguir:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue a página de configurações do serviço de MFA toohello por instruções Olá início Olá deste artigo.
3. Selecione o botão de opção de saudação Avançar muito**permitem que os usuários toocreate aplicativo senhas toosign em aplicativos sem navegador**.

![Criar senhas de aplicativo](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Criar senhas de aplicativo
Os usuários podem criar senhas de aplicativo durante o registro inicial. É fornecida uma opção final Olá Olá do processo de registro que permite que eles toocreate senhas de aplicativo.

Usuários também podem criar senhas de aplicativo após o registro alterando suas configurações de saudação do Azure portal ou hello portal do Office 365. Para obter mais informações e etapas detalhadas para os usuários, consulte [O que são senhas de aplicativo na Autenticação Multifator do Azure](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Lembrar a autenticação multifator em dispositivos de confiança dos usuários
Lembrar Autenticação Multifator para dispositivos e navegadores de confiança dos usuários é um recurso gratuito para todos os usuários do MFA. Ele permite toogive opção de saudação de usuários MFA tooby passa para um determinado número de dias depois de executar um bem-sucedida entrar usando o MFA. Isso pode aumentar a usabilidade, minimizando o número de saudação de vezes que um usuário pode executar a verificação em duas etapas em Olá mesmo dispositivo.

No entanto, se um dispositivo ou a conta for comprometido, lembrar a autenticação multifator em dispositivos confiáveis pode colocar sua segurança em risco. Caso uma conta corporativa seja comprometida ou um dispositivo confiável seja perdido ou roubado, você deve [restaurar a Autenticação Multifator em todos os dispositivos](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Essa ação revoga Olá confiável status de todos os dispositivos e usuário Olá é necessário tooperform verificacao novamente. Você também pode instruir o toorestore usuários MFA em seus próprios dispositivos com instruções de saudação em [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Como ele funciona

Lembre-se a autenticação multifator funciona definindo um cookie persistente no navegador hello quando verifica se um usuário hello "não pergunte novamente por **X** dias" caixa na entrada. Olá usuário não será avisado para MFA novamente do que o navegador até Olá cookie expira. Se o usuário Olá abre um navegador diferente em Olá mesmo dispositivo ou limpa seus cookies, eles são solicitado tooverify novamente. 

Olá "não pergunte novamente por **X** dias" caixa de seleção não é mostrada em aplicativos sem navegador, ou não suporte a autenticação moderna. Esses aplicativos usam tokens de atualização que fornecem novos tokens de acesso a cada hora. Quando um token de atualização for validado, verificações de AD do Azure que Olá última verificação de tempo de duas etapas foi executada foi no número de saudação configurado de dias. 

Portanto, lembre-se de MFA em dispositivos confiáveis reduz o número de Olá de autenticações em aplicativos web (que normalmente solicitar sempre), mas aumenta Olá número de autenticações para clientes de autenticação moderna (que normalmente solicitar a cada 90 dias).

> [!NOTE]
>Este recurso não é compatível com o recurso de "Mantenha-me conectado" hello do AD FS quando os usuários executam a verificação em duas etapas para o AD FS por meio do servidor Azure MFA de saudação ou uma solução MFA de terceiros. Se seus usuários Selecione "Mantenha-me conectado" no AD FS e também marcar seus dispositivos como confiável para MFA, eles não será tooverify capaz depois Olá número "Lembre-se de MFA" de dias expira. AD do Azure solicita uma verificação de novo em duas etapas, mas o AD FS retorna um token de declaração MFA original hello e a data em vez de executar novamente a verificação em duas etapas. Isso define um loop de verificação entre o Azure AD e AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Habilitar a opção Lembrar autenticação multifator
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue a página de configurações do serviço de MFA toohello por instruções Olá início Olá deste artigo.
3. Na página de configurações de serviço do hello, em Gerenciar configurações de dispositivo de usuário, verifique Olá **permitir que os usuários tooremember a autenticação multifator em dispositivos que eles confiam** caixa.
   ![Lembrar dispositivos](./media/multi-factor-authentication-whats-next/remember.png)
4. Definir Olá número de dias que você deseja tooallow Olá confiável dispositivos toobypass verificacao. padrão de saudação é de 14 dias.
5. Clique em **Salvar**.
6. Clique em **fechar**

### <a name="mark-a-device-as-trusted"></a>Marcar um dispositivo como confiável

Depois de habilitar esse recurso, os usuários poderão marcar um dispositivo como confiável quando fizerem logon e marcarem a opção **Não perguntar novamente**.

![Não perguntar novamente - captura de tela](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Métodos de verificação selecionáveis
Você pode escolher quais métodos de verificação estarão disponíveis para os usuários. Olá tabela a seguir fornece uma visão geral de cada método.

Quando os usuários registram suas contas para MFA, escolham seu método preferido de verificação sem opções Olá ativado. diretrizes de saudação para seu processo de registro é abordado em [configurar minha conta para verificação em duas etapas](multi-factor-authentication-end-user-first-time.md)

| Método | Descrição |
|:--- |:--- |
| Chamar toophone |Faz uma chamada de voz automatizada para o usuário. saudação de respostas do usuário Olá chamada e pressiona # no tooauthenticate de teclado do telefone hello. O número de telefone não é sincronizado do local de tooon Active Directory. |
| Toophone de mensagem de texto |Envia para o usuário uma mensagem de texto que contém um código de verificação. usuário de saudação é solicitada tooeither toohello texto a mensagem de resposta com o código de verificação de saudação ou código de verificação tooenter Olá Olá logon na interface. |
| Notificação pelo aplicativo móvel |Envia um telefone de tooyour de notificação por push ou um dispositivo registrado. Olá usuário exibições notificação hello e seleciona **verificar** toocomplete verificação. <br>Olá Microsoft Authenticator aplicativo está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Código de verificação de aplicativo móvel |aplicativo do Microsoft Authenticator Hello gera um novo código de verificação de OATH cada trinta segundos. usuário de saudação insere esse código de verificação Olá logon na interface.<br>Olá Microsoft Authenticator aplicativo está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Como os métodos de autenticação tooenable/desabilitar
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue a página de configurações do serviço de MFA toohello por instruções Olá início Olá deste artigo.
3. Na página de configurações do serviço de hello, em Opções de verificação, marque/desmarque opções Olá desejar toouse.
   ![Opções de verificação](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Clique em **Salvar**.
5. Clique em **fechar**

