---
title: recursos aaaUse existentes NPS servidores tooprovide MFA do Azure | Microsoft Docs
description: "Olá extensão do servidor de políticas de rede para o Azure multi-Factor Authentication é uma solução simples tooadd baseado em nuvem em duas etapas vericiation recursos tooyour autenticação infraestrutura existente."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Integrar sua infraestrutura do NPS existente à Autenticação Multifator do Azure

saudação de extensão do servidor de diretivas de rede (NPS) para o Azure MFA adiciona baseado em nuvem MFA recursos tooyour infraestrutura de autenticação usando os servidores existentes. Com hello extensão do NPS, você pode adicionar chamada telefônica, mensagem de texto ou telefone aplicativo verificação tooyour existente fluxo de autenticação sem ter que tooinstall, configurar e manter os novos servidores. 

Esta extensão foi criada para as organizações que desejam tooprotect conexões de VPN sem implantar Olá servidor Azure MFA. Olá extensão NPS atua como um adaptador entre RADIUS e baseado em nuvem do Azure MFA tooprovide um segundo fator de autenticação para usuários federados ou sincronizados.

Ao usar a extensão NPS Olá para o Azure MFA, o fluxo de autenticação de saudação inclui Olá componentes a seguir: 

1. **Servidor VPN/NAS** recebe solicitações de clientes VPN e converte-os em servidores de tooNPS de solicitações do RADIUS. 
2. **Servidor NPS** conecta tooActive Directory tooperform Olá autenticação primária para Olá RADIUS solicita e, em caso de sucesso, passa as extensões do hello solicitação tooany instalado.  
3. **Extensão de NPS** dispara uma solicitação tooAzure MFA para autenticação secundária hello. Depois que a extensão Olá recebe a resposta hello e Olá desafio MFA for bem-sucedida, ele conclui a solicitação de autenticação hello, fornecendo o servidor NPS de saudação com tokens de segurança que incluem uma declaração de MFA, emitida pelo STS do Azure.  
4. **Azure MFA** se comunica com os detalhes do usuário do Active Directory do Azure tooretrieve hello e realiza a autenticação secundária hello, usando um usuário de toohello verificação método configurado.

Olá diagrama a seguir ilustra esse fluxo de solicitação de autenticação de alto nível: 

![Diagrama de fluxo de autenticação](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Planejar sua implantação

Olá extensão NPS controla automaticamente a redundância, que exige uma configuração especial.

Você pode criar quantos servidores NPS habilitados para o Azure MFA conforme necessário. Se você instalar vários servidores, use um certificado de cliente diferente para cada um deles. Ao criar um certificado para cada servidor, você pode atualizar cada certificado individualmente e não se preocupar com tempo de inatividade em todos eles.

Servidores VPN de rotear solicitações de autenticação, portanto, precisam toobe atento novos servidores NPS ativado o Azure MFA hello.

## <a name="prerequisites"></a>Pré-requisitos

Olá extensão NPS deve toowork com sua infraestrutura existente. Certifique-se de que ter Olá seguintes pré-requisitos antes de começar.

### <a name="licenses"></a>Licenças

Olá NPS extensão para o Azure MFA é disponível toocustomers com [licenças para o Azure multi-Factor Authentication](multi-factor-authentication.md) (incluído no Azure AD Premium, o EMS ou uma assinatura de MFA).

### <a name="software"></a>Software

Windows Server 2008 R2 SP1 ou superior.

### <a name="libraries"></a>Bibliotecas

Essas bibliotecas são instaladas automaticamente com a extensão de saudação.
-   [Pacotes redistribuíveis do Visual C++ para Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Módulo Microsoft Azure Active Directory para Windows PowerShell versão 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Qualquer pessoa que usa a extensão NPS Olá deve ser tooAzure sincronizado do Active Directory usando o Azure AD Connect e deve ser registrado para MFA.

Quando você instala a extensão de hello, terá as credenciais de administrador e a ID de diretório Olá para seu locatário do AD do Azure. Você pode encontrar sua ID de diretório no hello [portal do Azure](https://portal.azure.com). Entre como administrador, selecione Olá **Active Directory do Azure** ícone Olá esquerda, selecione **propriedades**. Saudação de cópia GUID em Olá **ID de diretório** caixa e salvá-lo. Você pode usar esse GUID como ID de locatário hello quando você instala o hello extensão do NPS.

![Localize sua ID de diretório em Propriedades do Azure Active Directory](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Prepare o seu ambiente

Antes de instalar a extensão NPS hello, você deseja tooprepare você ambiente toohandle Olá tráfego de autenticação.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Habilitar a função do NPS Olá em um servidor ingressado no domínio

servidor NPS Olá conecta tooAzure do Active Directory e autentica solicitações MFA de saudação. Escolha um servidor para essa função. É recomendável escolher um servidor que não lidar com solicitações de outros serviços, como Olá extensão NPS gera erros para todas as solicitações que não são RADIUS.

1. No seu servidor, abra Olá **assistente Adicionar funções e recursos** de saudação menu Quickstart Gerenciador do servidor.
2. Escolha **Instalação baseada em função ou recurso** para o tipo de instalação.
3. Selecione Olá **serviços de acesso e política de rede** função de servidor. Uma janela poderá ser exibido tooinform de recursos necessários toorun essa função.
4. Prossiga com o assistente Olá até a página de confirmação de saudação. Selecione **Instalar**.

Agora que você tem um servidor designado para NPS, você também deve configurar este servidor toohandle solicitações RADIUS do hello solução VPN.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Configurar seu toocommunicate de solução VPN com o servidor NPS de saudação

Dependendo de qual solução VPN que você usar, Olá tooconfigure etapas variam de sua política de autenticação de RADIUS. Configure o servidor de NPS RADIUS política toopoint tooyour.

### <a name="sync-domain-users-toohello-cloud"></a>Nuvem de toohello de usuários de domínio de sincronização

Esta etapa já poderá ser concluída no seu locatário, mas é bom verificação toodouble do Azure AD Connect foi sincronizado seus bancos de dados recentemente.

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Selecione **Azure Active Directory** > **Azure AD Connect**
3. Verifique se o status de sincronização está **Habilitado** e se a última sincronização foi há menos de uma hora.

Se você precisar tookick uma nova rodada de sincronização, nós Olá instruções [sincronização do Azure AD Connect: Agendador](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Determinar quais métodos de autenticação os usuários podem usar

Há dois fatores que afetam quais métodos de autenticação estão disponíveis com uma implantação de extensão do NPS:

1. algoritmo de criptografia de senha Olá usado entre o cliente RADIUS de saudação (VPN, Netscaler server, ou outros) e os servidores NPS hello.
   - **PAP** oferece suporte a todos os métodos de autenticação de saudação do Azure MFA na nuvem Olá: chamada telefônica, mensagem de texto unidirecional, notificação de aplicativo móvel e código de verificação de aplicativo móvel.
   - **CHAPV2** e **EAP** dão suporte a chamada telefônica e notificação de aplicativo móvel.
2. métodos que Olá aplicativo cliente de entrada Hello (VPN, Netscaler server, ou outros) pode manipular. Por exemplo, o cliente VPN Olá ter alguns meios tooallow Olá usuário tootype em um código de verificação de um texto ou aplicativo móvel?

Quando você implantar a extensão NPS hello, use essas tooevaluate fatores quais métodos estão disponíveis para os usuários. Se o cliente RADIUS oferece suporte a PAP, mas o cliente Olá UX não tem campos de entrada para um código de verificação, em seguida, chamada telefônica e notificação de aplicativo móvel são duas opções com suporte de saudação.

Você pode [desabilitar métodos de autenticação sem suporte](multi-factor-authentication-whats-next.md#selectable-verification-methods) no Azure.

### <a name="enable-users-for-mfa"></a>Habilitar usuários para a MFA

Antes de implantar a extensão NPS completo Olá, é necessário tooenable MFA para usuários de saudação que você deseja tooperform verificação de duas etapas. Mais imediatamente, extensão de saudação tootest como implantá-lo, você precisa de pelo menos um teste conta totalmente registrado para autenticação multifator.

Use esses tooget etapas iniciada de uma conta de teste:
1. Entrar muito[https://aka.ms/mfasetup](https://aka.ms/mfasetup) com uma conta de teste. 
2. Siga Olá prompts tooset um método de verificação.
3. Crie uma política de acesso condicional ou [alterar o estado do usuário Olá](multi-factor-authentication-get-started-user-states.md) toorequire verificação de duas etapas para a conta de teste de saudação. 

Os usuários também precisam ter toofollow tooenroll estas etapas antes de eles poderão autenticar com a extensão NPS hello.

## <a name="install-hello-nps-extension"></a>Instalar a extensão NPS Olá

> [!IMPORTANT]
> Instale a extensão NPS de saudação em um servidor diferente do ponto de acesso VPN hello.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Baixe e instale a extensão NPS Olá para o Azure MFA

1.  [Baixar Olá NPS extensão](https://aka.ms/npsmfa) de saudação Microsoft Download Center.
2.  Copie Olá binário toohello deseja tooconfigure do servidor de políticas de rede.
3.  Executar *setup.exe* e siga as instruções de instalação de saudação. Se você encontrar erros, verifique que Olá duas bibliotecas da seção de pré-requisitos Olá foram instaladas com êxito.

### <a name="run-hello-powershell-script"></a>Executar script do PowerShell Olá

instalador de saudação cria um script do PowerShell neste local: `C:\Program Files\Microsoft\AzureMfa\Config` (onde C:\ é a unidade de instalação). Este script do PowerShell executa Olá ações a seguir:

-   Crie um certificado autoassinado.
-   Associe a chave pública de saudação do serviço de toohello de certificado de saudação principal no AD do Azure.
-   Repositório cert Olá no repositório de certificados do computador local hello.
-   Particular chave tooNetwork conceder acesso toohello certificado usuário.
-   Reinicie Olá NPS.

A menos que você deseje toouse seus próprios certificados (em vez da saudação certificados autoassinados hello gera script do PowerShell), execute Olá Script do PowerShell toocomplete instalação de saudação. Se você instalar a extensão de saudação em vários servidores, cada um deve ter seu próprio certificado.

1. Execute o Windows PowerShell como um administrador.
2. Altere os diretórios.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Execute script do PowerShell Olá criado pelo instalador hello.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. O PowerShell solicitará a sua ID de locatário. Use Olá GUID de ID de diretório que você copiou da saudação portal do Azure, na seção de pré-requisitos de saudação.
5. Entrar tooAzure AD como um administrador.
6. PowerShell mostra uma mensagem de êxito quando Olá script for concluído.  

Repita essas etapas em quaisquer servidores NPS adicionais que você deseja tooset para balanceamento de carga.

>[!NOTE]
>Se você usar seus próprios certificados em vez de gerar certificados com hello script do PowerShell, certifique-se de que elas se alinham toohello convenção de nomenclatura de NPS. nome da entidade Olá deve ser **CN =\<TenantID\>, UO = Microsoft NPS extensão**. 

## <a name="configure-your-nps-extension"></a>Configurar sua extensão do NPS

Esta seção inclui considerações sobre o design e sugestões para implantações bem-sucedidas da extensão do NPS.

### <a name="configuration-limitations"></a>Limitações de configuração

- Olá extensão NPS para o Azure MFA não inclui os usuários toomigrate de ferramentas e configurações de nuvem do servidor MFA toohello. Por esse motivo, é aconselhável usar extensão Olá para novas implantações, em vez de implantação existente. Se você usar a extensão de saudação em uma implantação existente, os usuários tiverem o prova tooperform novamente toopopulate seu MFA detalhes na nuvem hello.  
- Olá extensão NPS usa Olá UPN da saudação usuário do Active directory tooidentify Olá no Azure MFA para executar a extensão de Olá Olá autenticação secundária pode ser configurado toouse um identificador diferente como logon alternativo ID personalizado do Active Directory ou ao local campo que não seja o UPN. Consulte [configuração Opções avançadas para Olá extensão NPS para autenticação multifator](multi-factor-authentication-advanced-vpn-configurations.md) para obter mais informações.
- Nem todos os protocolos de criptografia dão suporte a todos os métodos de verificação.
   - O **PAP** dá suporte a chamadas telefônicas, mensagens de texto unidirecionais, notificações de aplicativo móvel e códigos de verificação de aplicativo móvel
   - **CHAPV2** e **EAP** dão suporte a chamada telefônica e notificação do aplicativo móvel

### <a name="control-radius-clients-that-require-mfa"></a>Clientes RADIUS de controle que exigem MFA

Depois que você habilita a MFA para um cliente RADIUS usando Olá extensão do NPS, todas as autenticações desse cliente são necessário tooperform MFA. Se você quiser tooenable MFA para alguns clientes RADIUS, mas outros não, você pode configurar dois servidores NPS e instalar extensão Olá em apenas um deles. Configure clientes RADIUS que você deseja toorequire MFA toosend solicitações toohello servidor NPS configurado com a extensão de saudação e outro servidor RADIUS clientes toohello NPS não está configurado com a extensão de saudação.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Preparar usuários que não são registrados na MFA

Se você tiver usuários que não são registrados para MFA, é possível determinar o que acontece quando eles tentam tooauthenticate. Usar configuração de registro de saudação *REQUIRE_USER_MATCH* no caminho de registro Olá *HKLM\Software\Microsoft\AzureMFA* toocontrol o comportamento de recursos hello. Essa configuração tem uma opção de configuração única:

| Chave | Valor | Padrão |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | Não definido (tooTRUE equivalente) |

Olá propósito dessa configuração é toodetermine que toodo quando um usuário não estiver registrado para MFA. Quando Olá key não existe, não está definido ou está definido tooTRUE, Olá usuário não estiver registrado e extensão Olá falha desafio MFA de saudação. Quando a chave de saudação está definido tooFALSE e Olá usuário não estiver registrado, a autenticação continuará sem executar o MFA.

Você pode escolher toocreate essa chave e defini-lo tooFALSE enquanto os usuários estão integração e podem nem todas ser registradas para o Azure MFA ainda. No entanto, desde que a configuração da chave Olá permite que os usuários que não são registrados para toosign MFA no, você deve remover essa chave antes de ir tooproduction.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Como verificar o que certificado de cliente que hello está instalado, conforme o esperado?

Procure o certificado autoassinado do hello criado pelo instalador Olá no repositório de certificados de saudação e verifique se Olá chave privada tem permissões concedidas toouser **serviço de rede**. cert Olá tem um nome de assunto de **CN \<tenantid\>, UO = extensão do NPS da Microsoft**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Como verificar o certificado de cliente é locatário toomy associada no Active Directory do Azure?

Abra um prompt de comando do PowerShell e execute hello comandos a seguir:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Estes comandos imprimem todos os certificados de saudação associar seu locatário a sua instância do hello extensão NPS em sua sessão do PowerShell. Procure seu certificado exportando seu certificado de cliente como um arquivo "codificado na Base 64 X.509(.cer)" sem chave privada hello e compará-lo com a lista de saudação do PowerShell.

Válido- e de término válidas-até que os carimbos de hora, que estão no formato legível, podem ser usado toofilter out misfits óbvios se o comando Olá retorna mais de um certificado.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Por que minhas solicitações estão falhando, com erro de token ADAL?

Esse erro pode ter ocorrido tooone várias razões. Use essas etapas de solução de problemas de toohelp:

1. Reinicie o servidor NPS.
2. Verifique se o certificado do cliente está instalado conforme o esperado.
3. Verifique se que esse certificado hello está associado ao seu locatário no AD do Azure.
4. Verifique se que https://login.microsoftonline.com/ está acessível no servidor de saudação executando a extensão de saudação.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Por que a autenticação falha com um erro nos logs HTTP, indicando que o usuário Olá não foi encontrado?

Verifique se o AD Connect está em execução, e esse usuário hello está presente no Active Directory do Windows e o Active Directory do Azure.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>Por que vejo erros de conexão HTTP nos logs, com todas as minhas autenticações falhando?

Verifique se que esse https://adnotifications.windowsazure.com é acessível do servidor de saudação executando a extensão de NPS hello.


## <a name="next-steps"></a>Próximas etapas

- Configurar IDs alternativos para logon, ou configurar uma lista de exceções para IPs que não devem executar a verificação em duas etapas no [configuração Opções avançadas para Olá extensão NPS para autenticação multifator](nps-extension-advanced-configuration.md)

- [Resolver mensagens de erro de saudação extensão NPS para o Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
