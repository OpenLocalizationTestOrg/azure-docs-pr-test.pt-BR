---
title: "a integração com o Azure MFA usando a extensão NPS aaaVPN | Microsoft Docs"
description: "Este artigo aborda a integração de sua infraestrutura VPN com o Azure MFA usando a extensão de servidor de diretivas de rede (NPS) de saudação do Microsoft Azure."
services: active-directory
keywords: "Azure MFA, integrar VPN, Azure Active Directory, extensão do Servidor de Políticas de Rede"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Integrar sua infraestrutura VPN com o Azure multi-Factor Authentication (MFA) usando a extensão do servidor de diretivas de rede (NPS) de saudação do Azure

## <a name="overview"></a>Visão geral

Olá extensão de serviço de diretiva de rede (NPS) para o Azure permite que as organizações usando autenticação do cliente de Remote Authentication Dial-In serviço RADIUS (User) toosafeguard baseado em nuvem [Azure multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), que fornece verificação em duas etapas.

Este artigo fornece instruções para a integração de infraestrutura NPS Olá com o Azure MFA usando a extensão NPS Olá para verificação de duas etapas seguro tooenable do Azure para usuários tentando tooconnect tooyour rede usando uma VPN. 

Olá política de rede e serviços de acesso (NPS) fornece Olá organizações recursos a seguir:

* Especifica locais centrais para o gerenciamento de saudação e o controle de toospecify de solicitações de rede que pode se conectar, o tempo do dia que as conexões são permitidas, duração Olá de conexões e nível de saudação de segurança que os clientes devem usar tooconnect e assim por diante. Em vez de especificar essas políticas em cada servidor VPN ou Gateway de Área de Trabalho Remota (RD), essas políticas podem ser especificadas uma vez em um local central. Olá protocolo RADIUS é usado tooprovide Olá centralizado autenticação, autorização e contabilização (AAA). 
* Estabelecer e impor políticas de integridade do cliente de proteção de acesso à rede (NAP) que determinam se os dispositivos recebem acesso restrita ou irrestrita toonetwork recursos.
* Fornecem um meio tooenforce autenticação e autorização para acessar os pontos de acesso sem fio compatíveis com too802.1x e switches Ethernet.    

Para obter mais informações, consulte [Servidor de Políticas de Rede (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

segurança tooenhance e fornecer um alto nível de conformidade, as organizações podem integrar NPS com o Azure MFA tooensure que os usuários usem a verificação em duas etapas toobe capaz de se conectar toohello a porta virtual no servidor VPN hello. Para usuários toobe de acesso, eles devem fornecer a combinação nome de usuário e senha com informações que Olá usuário tem em seu controle. Essas informações devem ser confiáveis e não facilmente duplicadas, como um número de telefone celular, o número de telefone fixo, o aplicativo em um dispositivo móvel e assim por diante.

Disponibilidade de toohello anterior de saudação extensão NPS para o Azure, os clientes que desejavam tooimplement verificação de duas etapas para integrado NPS e ambientes do Azure MFA tinham tooconfigure e mantêm um servidor separado do MFA no ambiente local Olá documentados no Gateway de área de trabalho remota e servidor Azure multi-Factor Authentication usando RADIUS.

disponibilidade de saudação da extensão NPS Olá para o Azure agora oferece organizações Olá escolha toodeploy uma solução MFA com base no local ou um baseado em nuvem MFA solução toosecure RADIUS autenticação do cliente.
 
## <a name="authentication-flow"></a>Fluxo de autenticação
Quando um usuário se conecta a porta virtual tooa em um servidor VPN, eles devem primeiro autenticar usando uma variedade de protocolos que permita o uso de saudação de uma combinação de nome de usuário/senha e os métodos de autenticação baseada em certificado. 

Em adição tooauthenticating e verificar a identidade, os usuários devem ter Olá dial-in permissões adequadas. Em implantações simples, essas permissões dial-in que permitem acesso são definidas diretamente em objetos de usuário do Active Directory hello. 

 ![Propriedades do Usuário](./media/nps-extension-vpn/image1.png)

Para implantações simples, cada servidor VPN concede ou nega o acesso com base nas políticas definidas em cada servidor VPN local.

Em implementações maiores e mais escalonáveis, Olá políticas que conceder ou negar acesso a VPN são centralizados em servidores RADIUS. Nesse caso, o servidor VPN de saudação atua como um servidor de acesso (cliente RADIUS) que encaminha solicitações de conexão e o servidor RADIUS do conta mensagens tooa. tooconnect toohello porta virtual no servidor VPN hello, os usuários devem ser autenticados e atender às condições de saudação definidas centralmente em servidores RADIUS. 

Quando Olá extensão NPS para o Azure é integrado com hello NPS, o fluxo de autenticação bem-sucedida de saudação é o seguinte:

1. servidor VPN Olá recebe uma solicitação de autenticação de um usuário VPN que inclui Olá username e password tooconnect tooa recurso, como uma sessão de área de trabalho remota. 
2. Atua como um cliente RADIUS, servidor VPN converte a mensagem de solicitação de acesso RADIUS Olá solicitação tooa e envia Olá mensagem (a senha é criptografada) toohello RADIUS servidor NPS () onde Olá extensão NPS está instalado. 
3. Olá nome de usuário e combinação de senha é verificada no Active Directory. Se Olá nome de usuário / senha está incorreta, Olá servidor RADIUS envia uma mensagem de rejeição de acesso. 
4. Se todas as condições, como especificado em Olá a solicitação de Conexão do NPS e diretivas de rede são atendidas (por exemplo, hora do dia ou grupo de restrições de associação), Olá extensão NPS dispara uma solicitação de autenticação secundária com o Azure MFA. 
5. MFA do Azure se comunica com o Active Directory do Azure, recupera os detalhes do usuário hello e executa a autenticação secundária hello, usando o método hello configurado pelo usuário hello (mensagem de texto, aplicativo móvel e assim por diante). 
6. Após o sucesso da saudação desafio MFA, o Azure MFA se comunica extensão NPS Olá resultado toohello.
7. Após a tentativa de conexão de saudação é autenticada e autorizada, o servidor NPS de Olá onde extensão hello está instalado envia um aceitação de acesso RADIUS mensagem toohello servidor VPN (cliente RADIUS).
8. usuário Olá é concedido acesso toohello virtual porta no servidor VPN e estabelece um túnel VPN criptografado.

## <a name="prerequisites"></a>Pré-requisitos
Esta seção detalha os pré-requisitos de saudação necessários para integrar o Azure MFA com hello Gateway de área de trabalho remota. Antes de começar, você deve ter Olá pré-requisitos no local a seguir.

* Infraestrutura de VPN
* Função de Serviços de Acesso (NPS) e Política de Rede
* Licença do Azure MFA
* Software do Windows Server
* Bibliotecas
* Azure AD sincronizado com o AD local 
* ID do GUID do Azure Active Directory

### <a name="vpn-infrastructure"></a>Infraestrutura de VPN
Este artigo pressupõe que você tenha uma infraestrutura VPN de trabalho usando o Microsoft Windows Server 2016 no local e no momento, o servidor VPN Olá não é configurado tooforward conexão solicitações tooa RADIUS servidor. Você vai configurar Olá VPN infraestrutura toouse um servidor RADIUS central neste guia.

Se você não tiver uma infraestrutura de trabalho em vigor, você pode criar rapidamente essa infraestrutura pelo seguinte orientação Olá fornecida em vários tutoriais de configuração VPN que você pode encontrar no hello Microsoft e sites de terceiros. 

### <a name="network-policy-and-access-services-nps-role"></a>Função de Serviços de Acesso (NPS) e Política de Rede

Olá, serviço de função NPS fornece funcionalidade de cliente e servidor RADIUS de saudação. Este artigo pressupõe que você instalou o função do NPS Olá em um servidor membro ou controlador de domínio em seu ambiente. Você configurará o RADIUS para uma configuração de VPN neste guia. Instalar a função do NPS Olá em um servidor _outros_ que o servidor VPN.

Para obter informações sobre como instalar a função do NPS de saudação do serviço Windows Server 2012 ou superior, consulte [instalar um servidor de política de integridade de NAP](https://technet.microsoft.com/library/dd296890.aspx). Política de Acesso à Rede (NAP) foi preterido no Windows Server 2016. Para obter uma descrição de práticas recomendadas para NPS, inclusive tooinstall de recomendação de saudação NPS em um controlador de domínio, consulte [práticas recomendadas para NPS](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licenças

É necessário uma licença para o Azure MFA, que está disponível por meio de um Azure AD Premium, Enterprise Mobility + Security (EMS) ou uma assinatura de MFA. Para obter mais informações, consulte [como tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). Para fins de teste, você pode usar uma assinatura de avaliação.

### <a name="software"></a>Software

Olá extensão NPS requer o Windows Server 2008 R2 SP1 ou superior com o serviço de função NPS Olá instalado. Todas as etapas de saudação neste guia foram realizadas usando o Windows Server 2016.

### <a name="libraries"></a>Bibliotecas

Olá duas bibliotecas a seguir é necessária:

* [Pacotes redistribuíveis do Visual C++ para Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Módulo Microsoft Azure Active Directory para Windows PowerShell versão 1.1.166.0_ ou posterior. Para a versão mais recente do hello e instruções de instalação, consulte [Microsoft Azure Active Directory PowerShell módulo versão histórico de versão](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Essas bibliotecas não são compactadas com hello NPS extensão arquivos de instalação (versão 0.9.1.2), apesar da documentação existente que indique o contrário. No mínimo, você deve instalar os pacotes redistribuíveis do hello Visual C++ para Visual Studio 2013. Olá Microsoft Azure módulo Active Directory para Windows PowerShell é instalado, se ainda não estiver presente, por meio de um script de configuração que é executada como parte do processo de instalação de saudação. Há tooinstall sem necessidade esse módulo antecipadamente se já não estiver instalado.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory sincronizado com o Active Directory local 

Olá toouse extensão NPS local os usuários devem ser sincronizados com o Active Directory do Azure e habilitados para autenticação multifator. Este guia pressupõe que os usuários locais são sincronizados com o Azure Active Directory usando o AD Connect. As instruções para habilitar usuários para MFA são fornecidas abaixo.
Para obter informações sobre o Azure AD Connect, consulte [Integrar seus diretórios locais com o Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID do GUID do Azure Active Directory 
tooinstall Olá NPS, é necessário tooknow Olá GUID de saudação do Active Directory do Azure. Na próxima seção, Olá, são fornecidas instruções para localizar Olá GUID de saudação do Active Directory do Azure.

## <a name="configure-radius-for-vpn-connections"></a>Configurar RADIUS para conexões VPN

Se você tiver instalado a função de servidor NPS Olá em um servidor membro, você precisa tooconfigure tooauthenticate e autoriza o cliente VPN que solicitar conexões VPN. 

Esta seção pressupõe que você instalou a função de servidor de políticas de rede Olá mas não o configurou para uso em sua infraestrutura.

>[!NOTE]
>Se você já tiver um servidor VPN de trabalho que usa um servidor RADIUS centralizado para autenticação, você pode ignorar esta seção.
>

### <a name="register-server-in-active-directory"></a>Registrar o Servidor no Active Directory
toofunction corretamente nesse cenário, o servidor NPS de saudação precisa toobe registrado no Active Directory.

1. Abra o Gerenciador de Servidor.
2. No Gerenciador do Servidor, clique em **Ferramentas**e, em seguida, clique em **Servidor de Políticas de Rede**. 
3. No console do servidor de políticas de rede hello, clique com botão direito **NPS (Local)**e, em seguida, clique em **registrar servidor no Active Directory**. Clique em **OK** duas vezes.

 ![Servidor de Políticas de Rede](./media/nps-extension-vpn/image2.png)

4. Deixe o console de saudação aberta para o procedimento a seguir hello.

### <a name="use-wizard-tooconfigure-radius-server"></a>Use o Assistente de servidor RADIUS tooconfigure
Você pode usar um padrão (baseada em Assistente) ou configuração avançada opção tooconfigure Olá RADIUS server. Esta seção assume o uso de saudação da opção de configuração padrão baseada em Assistente de saudação.

1. No console do servidor de políticas de rede hello, clique em **NPS (Local)**.
2. Em Configuração Padrão, selecione **Servidor RADIUS para conexões VPN ou Conexões Discadas**e, em seguida, clique em **Configurar VPN ou Conexão Discada**.

 ![Configurar VPN](./media/nps-extension-vpn/image3.png)

3. Olá selecione Dial-up ou tipo de conexões de rede privada Virtual página, selecione **conexões de rede Virtual privada**e clique em **próximo**.

 ![Rede Virtual Privada](./media/nps-extension-vpn/image4.png)

4. Na página especificar Dial-Up ou um servidor VPN hello, clique em **adicionar**.
5. Em Olá **cliente RADIUS novo** caixa de diálogo, forneça um nome amigável, digite o nome pode ser resolvido hello ou endereço IP do servidor VPN de saudação e insira uma senha de segredo compartilhado. Essa senha de segredo compartilhado deve ser longa e complexa. Anote a senha, conforme necessário para as etapas na próxima seção, Olá.

 ![Novo Cliente RADIUS](./media/nps-extension-vpn/image5.png)

6. Clique em **OK**e, em seguida, **Seguinte**.
7. Em Olá **configurar métodos de autenticação** página, aceite a seleção padrão de saudação (autenticação criptografada da Microsoft versão 2 (MS-CHAPv2) ou escolha outra opção e clique em **próximo**.

  >[!NOTE]
  >Se você configurar o protocolo EAP (Extensible Authentication), você deve usar o MS CHAPv2 ou PEAP. Não há suporte para nenhum outro tipo de EAP.
 
8. Na página de especificar grupos de usuários hello, clique em **adicionar** e selecione um grupo apropriado, se houver. Caso contrário, deixe em branco toogrant acesso tooall usuários seleção hello.

 ![Especificar Grupos de Usuários](./media/nps-extension-vpn/image7.png)

9. Clique em **Avançar**.
10. Na página de especificar os filtros IP hello, clique em **próximo**.
11. Na página de configurações de criptografia de especificar hello, aceite as configurações padrão de saudação e clique em **próximo**.

 ![Especificar Criptografia](./media/nps-extension-vpn/image8.png)

12. Em Olá especifique um nome de Realm, deixar Olá nome em branco, aceite a configuração padrão de saudação e clique em **próximo**.

 ![Especificar um Nome de Realm](./media/nps-extension-vpn/image9.png)

13. Olá Concluindo novo Dial-up ou página de clientes RADIUS e conexões de rede Virtual privada, clique em **concluir**.

 ![Concluir as Conexões](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Verificar a configuração RADIUS
Esta seção fornece detalhes sobre configuração Olá criado usando o Assistente de saudação.

1. No servidor NPS hello, no console do NPS (Local) hello, expanda clientes RADIUS e selecione **clientes RADIUS**.
2. No painel de detalhes de saudação, clique com botão direito cliente RADIUS de saudação criado usando o assistente e, em seguida, clique em **propriedades**. Propriedades de saudação para o cliente RADIUS (servidor VPN Olá) devem ser semelhante toothose mostrado abaixo.

 ![Propriedades VPN](./media/nps-extension-vpn/image11.png)

3. Clique em **Cancelar**.
4. No servidor NPS hello, no console do NPS (Local) hello, expanda **políticas**e selecione **diretivas de solicitação de Conexão**. Você verá a política de conexões VPN de saudação que se parece com a imagem de saudação abaixo.

 ![Solicitações de Conexão](./media/nps-extension-vpn/image12.png)

5. Em Políticas, selecione **Políticas de Rede**. Você deve uma política de conexões de rede Virtual privada (VPN) que é semelhante a imagem de saudação abaixo.

 ![Propriedades da Rede](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>Configurar a autenticação de RADIUS do servidor VPN toouse
Nesta seção, você deve configurar autenticação de RADIUS Olá VPN server toouse. Esta seção pressupõe que você tenha uma configuração de trabalho do servidor VPN, mas não configurou a autenticação de RADIUS Olá VPN servidor toouse. Depois de configurar o servidor VPN hello, você confirmar que sua configuração está funcionando conforme o esperado.

>[!NOTE]
>Se você já tiver um servidor VPN em vigor que usa autenticação RADIUS, você pode ignorar esta seção.
>

### <a name="configure-authentication-provider"></a>Configurar provedor de autenticação
1. No servidor VPN Olá, abra o Gerenciador do servidor.
2. No Gerenciador do Servidor, clique em **Ferramentas** e, em seguida, **Roteamento e Acesso Remoto**.
3. No console de roteamento e acesso remoto hello, clique com botão direito  **\[nome do servidor\] (local)**e, em seguida, clique em **propriedades**.

 ![Roteamento e Acesso Remoto](./media/nps-extension-vpn/image14.png)
 
4. Em Olá **[Propriedades de nome do servidor} (local)** caixa de diálogo, clique em Olá **segurança** guia. 
5. Em Olá **segurança** , no provedor de autenticação, clique em **autenticação RADIUS**e, em seguida, **configurar**.

 ![Autenticação Radius](./media/nps-extension-vpn/image15.png)
 
6. Na caixa de diálogo de autenticação RADIUS hello, clique em **adicionar**.
7. Em Olá Adicionar servidor RADIUS, em nome do servidor, adicionar Olá nome ou Olá endereço IP do servidor RADIUS de saudação configurado na seção anterior hello.
8. Um segredo compartilhado, clique em **alteração** e adicione Olá compartilhada senha secreta criado e registrado anteriormente.
9. No tempo limite (segundos), altere o valor de tooa de valor Olá entre **30** e **60**. Isso é necessário tooallow tempo suficiente toocomplete Olá segundo fator de autenticação.
 
 ![Adicionar Servidor RADIUS](./media/nps-extension-vpn/image16.png)
 
10. Clique em **OK** até que você feche todas as caixas de diálogo.

### <a name="test-vpn-connectivity"></a>Testar Conectividade VPN
Nesta seção, você pode confirmar que o cliente VPN Olá é autenticado e autorizado pelo servidor RADIUS de saudação durante a tentativa de porta virtual de tooVPN tooconnect. Esta seção pressupõe que você está usando o Windows 10 como um cliente VPN. 

>[!NOTE]
>Se você já tiver configurado um servidor VPN VPN cliente tooconnect toohello e salva configurações de saudação, você poderá ignorar Olá etapas relacionadas tooconfiguring e salvar um objeto de conexão VPN.
>

1. No computador de cliente VPN, clique em **Iniciar** e, em seguida, **Configurações** (ícone de engrenagem).
2. Em Configurações de Janela, clique em **Rede e Internet**.
3. Clique em **VPN**.
4. Clique em **Adicionar uma conexão VPN**.
5. Em Adicionar uma conexão VPN, especifique (interno) do Windows como Olá provedor VPN, em seguida, Olá completo restantes campos, conforme apropriado e clique em **salvar**. 

 ![Adicionar Conexão VPN](./media/nps-extension-vpn/image17.png)
 
6. Olá abrir **Central de rede e compartilhamento** no painel de controle.
7. Clique em **Alterar as configurações do adaptador**.

 ![Alterar as Configurações do Adaptador](./media/nps-extension-vpn/image18.png)

8. Clique com botão direito conexão de rede VPN hello e clique em Propriedades. 

 ![Propriedades da Rede VPN](./media/nps-extension-vpn/image19.png)

9. Na caixa de diálogo de propriedades VPN hello, clique em Olá **segurança** guia. 
10. Na guia de segurança hello, certifique-se de que apenas **Microsoft CHAP Version 2 (MS-CHAP v2)** está selecionado e clique em Okey.

 ![Permitir Protocolos](./media/nps-extension-vpn/image20.png)

11. Clique a conexão de VPN Olá **conectar**.
12. Na página de configurações de saudação, clique em **conectar**.

Uma conexão bem-sucedida é exibida no log de segurança Olá no servidor RADIUS Olá 6272 de ID de evento, conforme mostrado abaixo.

 ![Propriedades do evento](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Guia de Solução de Problemas
Suponha que sua configuração de VPN estava funcionando antes que você configurou Olá VPN servidor toouse um servidor RADIUS centralizado para autenticação e autorização. Nesse caso, é provável que o problema de saudação pode ser causado por uma configuração incorreta da saudação servidor RADIUS ou hello uso de um nome de usuário inválido ou a senha. Por exemplo, se você usar o sufixo UPN alternativo Olá Olá username, tentativa de logon Olá pode falhar (você deve usar Olá o mesmo nome de conta para obter melhores resultados). 

tootroubleshoot esses problemas, um local ideal toostart é tooexamine logs de eventos de segurança de saudação em Olá servidor RADIUS. pesquisa de tempo de toosave para eventos, você pode usar o hello baseada em função servidor de acesso e política de rede exibição personalizada no Visualizador de eventos, como é mostrado abaixo. ID do evento 6273 indica onde hello Network Policy Server negado acesso tooa usuário de eventos. 

 ![Visualizador de Eventos](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Configurar Autenticação Multifator
Esta seção fornece instruções para habilitar usuários para MFA e para configurar contas para verificação em duas etapas. 

### <a name="enable-multi-factor-authentication"></a>Habilitar autenticação multifator
Nesta seção, você pode habilitar contas do Azure AD para MFA. Saudação de uso **portal clássico** usuários tooenable para MFA. 

1. Abra um navegador e navegue muito[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Faça logon como administrador de saudação.
3. No portal de hello, na navegação à esquerda do hello, clique em **do ACTIVE DIRECTORY**.

 ![Diretório Padrão](./media/nps-extension-vpn/image23.png)

4. Na coluna de nome de saudação, clique em **diretório padrão** (ou outro diretório, se apropriado).
5. Na página início rápido hello, clique em **configurar**.

 ![Configuração Padrão](./media/nps-extension-vpn/image24.png)

6. Na página Configurar de hello, role para baixo e, na seção de autenticação multifator hello, clique em **gerenciar configurações de serviço**.

 ![Gerenciar Configurações de MFA](./media/nps-extension-vpn/image25.png)
 
7. Na página de autenticação multifator hello, examine as configurações de serviço padrão hello e, em seguida, clique em **usuários**. 

 ![Usuários MFA](./media/nps-extension-vpn/image26.png)
 
8. Na página de usuários hello, selecione usuários Olá que você deseja tooenable para MFA e, em seguida, clique em **habilitar**.

 ![Propriedades](./media/nps-extension-vpn/image27.png)
 
9. Quando solicitado, clique em **Habilitar autenticação multifator**.

 ![Habilitar MFA](./media/nps-extension-vpn/image28.png)
 
10. Clique em **fechar** 
11. Atualize a página de saudação. Olá status MFA é tooEnabled alterado.

Para obter informações sobre como os usuários de tooenable para autenticação multifator, consulte [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Configurar contas para verificação em duas etapas
Depois que uma conta tiver sido habilitada para MFA, os usuários não são toosign capaz em tooresources controlado por política da MFA Olá até que eles configurou com êxito um toouse dispositivo confiável para Olá fator de autenticação ter usado a verificação em duas etapas.

Nesta seção, você pode configurar um dispositivo confiável para uso com a verificação em duas etapas. Há várias opções disponíveis para você tooconfigure esses, incluindo Olá seguinte:

* **Aplicativo móvel**. Você instalar o aplicativo do Microsoft Authenticator Olá em um dispositivo Windows Phone, Android ou iOS. Dependendo das políticas da sua organização, você está toouse necessário Olá aplicativo em um dos dois modos: receber notificações de verificações (uma notificação é enviada dispositivo tooyour) ou Use o código de verificação (é necessário tooenter uma verificação de código que Atualiza a cada 30 segundos). 
* **Chamada telefônica ou SMS de celular**. Você pode receber uma chamada telefônica automática ou mensagem de texto. Com a opção de chamada telefônica hello, você responde chamada hello e pressione Olá # sinal tooauthenticate. Com a opção de texto de saudação, responder a mensagem de texto toohello ou insira o código de verificação de Olá Olá logon na interface.
* **Ligação para telefone comercial**. Esse processo é Olá mesmo que o descrito para as chamadas telefônicas automatizadas acima.

Siga estas instruções para configurar uma notificação de envio do dispositivo toouse Olá aplicativo móvel tooreceive para verificação.

1. Logon muito[https://aka.ms/mfasetup](https://aka.ms/mfasetup) ou em qualquer site, como [https://portal.azure.com](https://portal.azure.com), onde necessário tooauthenticate usando suas credenciais de MFA habilitado. 
2. Ao fazer logon com seu nome de usuário e senha, você verá uma tela que solicita a você tooset conta Olá para verificação de segurança adicional.

 ![Segurança Adicional](./media/nps-extension-vpn/image29.png)

3. Clique em **Configurar agora**.
4. Na página de verificação de segurança adicional hello, selecione um tipo de contato (telefone de autenticação, telefone comercial ou aplicativo móvel). Em seguida, selecione um país ou região e selecione um método. método Hello varia de acordo com o tipo de contato que você selecionar. Por exemplo, se você escolher aplicativo móvel, você pode selecionar se tooreceive notificações de verificação ou toouse um código de verificação. etapas de saudação seguir pressupõem que você escolher **aplicativo móvel** como saudação entre em contato com o tipo.

 ![Autenticação por Telefone](./media/nps-extension-vpn/image30.png)

5. Selecione Aplicativo móvel, clique em **Receber notificações de verificação**e, em seguida, **Configurar**. 

 ![Verificação do Aplicativo Móvel](./media/nps-extension-vpn/image31.png)
 
6. Se você ainda não tiver feito isso, instale o aplicativo móvel do autenticador de saudação em seu dispositivo. 
7. Siga as instruções de Olá Olá aplicativo móvel tooscan Olá apresentado o código de barras ou inserir informações de saudação manualmente e, em seguida, clique em **feito**.

 ![Configurar Aplicativo Móvel](./media/nps-extension-vpn/image32.png)

8. Na página de verificação de segurança adicional hello, clique em **contato me** e resposta toonotification enviado tooyour dispositivo.
9. Na página de verificação de segurança adicional hello, insira um número de contato caso você perca o aplicativo móvel do acesso toohello e clique em **próximo**.

 ![Número de Telefone Celular](./media/nps-extension-vpn/image33.png)
 
10. No hello verificação de segurança adicional, clique em **feito**.

dispositivo de saudação agora está configurado tooprovide um segundo método de verificação. Para obter informações sobre como configurar contas de verificação em duas etapas, consulte [Configurar minha conta para verificação em duas etapas](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Instalar e configurar a extensão do NPS

Esta seção fornece instruções para configurar VPN toouse MFA do Azure para autenticação de cliente com hello servidor VPN.

Depois de instalar e configurar a extensão NPS Olá, todas as autenticações de cliente baseado em RADIUS é processado por este servidor é necessário toouse MFA do Azure. Se não for todos os usuários VPN são registrados no Azure MFA, é possível configurar outro RADIUS server tooauthenticate os usuários que não são configurada toouse MFA. Ou você pode criar uma entrada de registro que permite que usuários desafiados tooprovide um segundo fator de autenticação, apenas se eles são registrados no MFA. 

Criar um novo valor de cadeia de caracteres chamado _REQUIRE_USER_MATCH na HKLM\SOFTWARE\Microsoft\AzureMfa_e defina Olá valor tooTRUE ou FALSE. 

 ![Exigir Correspondência do Usuário](./media/nps-extension-vpn/image34.png)
 
Se valor Olá é tooTRUE conjunto ou não definida, todas as solicitações de autenticação são o desafio MFA de tooan de assunto. Se o valor de saudação é definido tooFALSE, MFA desafios são emitidos apenas toousers que estão registrados no MFA. Somente use Olá configuração FALSE no teste ou em ambientes de produção durante um período de integração.

### <a name="acquire-azure-active-directory-guid-id"></a>Obter a ID do GUID do Azure Active Directory

Como parte da configuração de saudação do hello extensão do NPS, você precisa toosupply credenciais de administrador e hello ID do Active Directory do Azure para seu locatário do AD do Azure. Olá etapas a seguir mostram como ID de locatário de saudação tooget.

1. Entrar no portal do Azure toohello [https://portal.azure.com](https://portal.azure.com) como administrador global de saudação do hello Azure locatário.
2. No hello barra de navegação esquerda, clique em Olá **Active Directory do Azure** ícone.
3. Clique em **Propriedades**.
4. toocopy sua área de transferência de toohello ID de diretório, selecione Olá **cópia** ícone.
 
 ![ID do Diretório](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Instalar a extensão NPS Olá
Olá extensão NPS precisa toobe instalado em um servidor que tenha Olá política de rede e a função Serviços de acesso (NPS) instalada e que funciona como servidor RADIUS de saudação em seu design. Não instale a extensão NPS Olá em seu servidor de área de trabalho remota.

1. Baixar a extensão NPS de saudação do [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Copie o servidor NPS do hello instalação arquivo executável (NpsExtnForAzureMfaInstaller.exe) toohello.
3. No servidor NPS hello, clique duas vezes em **NpsExtnForAzureMfaInstaller.exe**. Se solicitado, clique em **Executar**.
4. Na Olá NPS extensão para a caixa de diálogo de Azure MFA, examinar os termos de licença de software hello, verifique **aceito os termos de licença toohello e condições**e clique em **instalar**.

 ![Extensão NPS](./media/nps-extension-vpn/image36.png)
 
5. No hello NPS extensão para a caixa de diálogo de MFA do Azure, clique em **fechar**.  

 ![Instalação bem-sucedida](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurar certificados para uso com a extensão NPS hello usando um script do PowerShell
comunicações seguras tooensure e garantia, é necessário tooconfigure certificados para uso pela extensão NPS hello. componentes NPS Olá incluem um script do Windows PowerShell que configura um certificado autoassinado para uso com o NPS. 

script Hello executa Olá ações a seguir:

* Cria um certificado autoassinado
* Associa a chave pública do certificado tooservice principal no AD do Azure
* Olá de repositórios de certificado no repositório de computador local Olá
* Concede acesso toohello chave privada do certificado toohello usuário da rede
* Reinicia o serviço do Servidor de Políticas de Rede

Se você quiser toouse seus próprios certificados, você precisa tooassociate Olá público de sua entidade de serviço de toohello de certificado no AD do Azure e assim por diante.
script de saudação toouse, forneça extensão Olá com suas credenciais administrativas do Active Directory do Azure e Olá ID de locatário do Active Directory do Azure copiados anteriormente. Execute o script de saudação em cada servidor NPS onde você instala a extensão NPS hello.

1. Abra um prompt do Windows PowerShell administrativo.
2. No prompt do PowerShell hello, digite _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_e pressione **ENTER**.
3. Digite _.\AzureMfsNpsExtnConfigSetup.ps1_ e pressione **ENTER**. 
 * script Hello verifica toosee se o módulo do Azure Active Directory PowerShell hello está instalado. Se não estiver instalado, o script hello instala o módulo de saudação para você.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Depois que o script hello verifica a instalação de saudação do módulo do PowerShell Olá, ele exibe a caixa de diálogo de módulo hello Azure Active Directory PowerShell. Na caixa de diálogo hello, insira suas credenciais de administrador do AD do Azure e a senha e clique em **entrar**. 
 
 ![Entrar no PowerShell](./media/nps-extension-vpn/image39.png)
 
5. Quando solicitado, cole a ID de locatário Olá copiado na área de transferência toohello antes e pressione **ENTER**. 

 ![ID do locatário](./media/nps-extension-vpn/image40.png)

6. script Hello cria um certificado autoassinado e executa outras alterações de configuração. saída de Hello é como imagem Olá mostrada abaixo.

 ![Certificado Autoassinado](./media/nps-extension-vpn/image41.png)

7. Reinicialize o servidor de saudação.
 
### <a name="verify-configuration"></a>Verificar a configuração
configuração de saudação tooverify, você precisa tooestablish uma nova conexão de VPN com o servidor VPN. Ao entrar com êxito suas credenciais para autenticação primária, Olá conexão VPN aguarda Olá autenticação secundária toosucceed antes de estabelecer conexão hello, conforme mostrado abaixo. 

 ![Verificar a Configuração](./media/nps-extension-vpn/image42.png)

Se autenticar com êxito com o método de verificação secundária hello que previamente configurados no Azure MFA, você está conectado toohello recursos. No entanto, se a autenticação secundária Olá não for bem-sucedida, recebem acesso tooresource. 

Exemplo hello abaixo, Olá autenticador de aplicativo em um Windows phone é autenticação secundária do hello tooprovide usado.

 ![Verificar a Conta](./media/nps-extension-vpn/image43.png)

Depois de autenticado com êxito usando o método secundário hello, recebem acesso toohello virtual porta no servidor VPN hello. No entanto, como era necessário toouse um método de autenticação secundário usando um aplicativo móvel em um dispositivo confiável, Olá log no processo é mais segura do que ele usa apenas um nome de usuário / senha combinação.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Exibir logs do Visualizador de Eventos para eventos de logon com sucesso
eventos de logon bem-sucedidos tooview Olá nos logs do Visualizador de eventos do Windows hello, você pode emitir Olá após o log de segurança do Windows do Windows PowerShell comando tooquery Olá no servidor NPS de saudação.

eventos de logon bem-sucedidos tooquery em logs do Visualizador de eventos de segurança de hello, use Olá comando, a seguir
* _Get-WinEvent -Logname Security_ | onde {$_.ID -eq '6272'} | FL 

 ![Visualizador de Eventos de Segurança](./media/nps-extension-vpn/image44.png)
 
Você também pode exibir o log de segurança hello ou Olá exibição personalizada serviços de acesso e política de rede, conforme mostrado abaixo:

 ![Acesso à Política de Rede](./media/nps-extension-vpn/image45.png)

No servidor de saudação onde você instalou a extensão NPS Olá para o Azure MFA, você pode encontrar os logs de aplicativo de Visualizador de eventos extensão toohello específico em **aplicativos e serviços Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent -Logname Security_ | onde {$_.ID -eq '6272'} | FL

 ![Número de Eventos](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Guia de Solução de Problemas
Se a configuração de saudação não está funcionando conforme o esperado, tootroubleshoot de toostart um bom é tooverify que Olá usuário toouse configurado o Azure MFA. Tem usuário Olá conectar-se muito[https://portal.azure.com](https://portal.azure.com). Se os usuários forem solicitados a realizar uma verificação secundária e são autenticados com sucesso, você pode eliminar uma configuração incorreta do Azure MFA.

Se estiver funcionando Azure MFA para usuários Olá, você deve revisar logs de eventos relevantes Olá. Isso inclui logs de eventos de segurança, o Gateway operacional e o Azure MFA Olá que são discutidos na seção anterior hello. 

Abaixo está um exemplo de saída do log de segurança mostrando um evento de logon com falha (Evento ID 6273):

 ![Log de Segurança](./media/nps-extension-vpn/image47.png)

Abaixo está um evento relacionado de saudação AzureMFA logs:

 ![Logs do Azure MFA](./media/nps-extension-vpn/image48.png)

tooperform avançado solucionar problemas de opções, consulte Olá NPS banco de dados formato arquivos de log onde Olá serviço NPS está instalado. Esses arquivos de log são criados na pasta _%SystemRoot%\System32\Logs_ como arquivos de texto separado por vírgula. Para obter uma descrição desses arquivos de log, consulte [Interpretar arquivos de log de formato de banco de dados de NPS](https://technet.microsoft.com/library/cc771748.aspx). 

entradas de saudação nesses arquivos de log são difíceis toointerpret sem importá-los em uma planilha ou um banco de dados. Você pode encontrar um número de IAS analisadores online tooassist você interpretar Olá arquivos de log. Abaixo está a saída de saudação de um para esse download [shareware aplicativo](http://www.deepsoftware.com/iasviewer): 

 ![Aplicativo Shareware](./media/nps-extension-vpn/image49.png)

E, por último, para mais opções de solução de problemas, você pode usar um analisador de protocolo, como o Wireshark ou o [Analisador de Mensagens da Microsoft](https://technet.microsoft.com/library/jj649776.aspx). Olá imagem a seguir do Wireshark mostra mensagens de saudação do RADIUS entre servidores VPN hello e Olá NPS.

 ![Analisador de Mensagens da Microsoft](./media/nps-extension-vpn/image50.png)

Para obter mais informações, consulte [Integrar sua infraestrutura existente do NPS à Autenticação Multifator do Azure ](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Próximas etapas
[Como tooget autenticação multifator do Azure](multi-factor-authentication-versions-plans.md)

[Gateway de Área de Trabalho Remota e Servidor Azure Multi-Factor Authentication usando RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrar seus diretórios locais no Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

