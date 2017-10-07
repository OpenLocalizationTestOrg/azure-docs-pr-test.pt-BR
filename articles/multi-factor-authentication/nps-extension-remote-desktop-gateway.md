---
title: "aaaRemote integração do Gateway de área de trabalho com a extensão do Azure MFA NPS | Microsoft Docs"
description: "Este artigo aborda a integração de sua infraestrutura de Gateway de área de trabalho remota com o Azure MFA usando a extensão de servidor de diretivas de rede (NPS) de saudação do Microsoft Azure."
services: active-directory
keywords: "Azure MFA, integrar o Gateway de Área de Trabalho Remota, Azure Active Directory, extensão do Servidor de Políticas de Rede"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Integrar sua infraestrutura de Gateway de área de trabalho remota usando a extensão do servidor de diretivas de rede (NPS) hello e o Azure AD

Este artigo fornece detalhes para a integração com o Azure multi-Factor Authentication (MFA) de sua infraestrutura de Gateway de área de trabalho remota usando a extensão de servidor de diretivas de rede (NPS) de saudação do Microsoft Azure. 

Olá extensão de serviço de diretiva de rede (NPS) para o Azure permite a autenticação de cliente clientes toosafeguard Remote Authentication Dial-In serviço RADIUS (User) usando o Azure's baseado em nuvem [multi-Factor Authentication (MFA)](multi-factor-authentication.md). Essa solução fornece verificação em duas etapas para adicionar uma segunda camada de segurança toouser entradas e transações.

Este artigo fornece instruções passo a passo para a integração de infraestrutura NPS Olá com o Azure MFA usando a extensão NPS de saudação do Azure. Isso permite que a verificação de segurança para usuários que tentam toolog em tooa Gateway de área de trabalho remota. 

Olá política de rede e serviços de acesso (NPS) oferece às organizações Olá seguinte de saudação do toodo de capacidade:
* Definir locais centrais para controle de solicitações de rede e gerenciamento de saudação especificando quem pode se conectar, Olá a que horas do dia que as conexões são permitidas, duração das conexões e Olá nível de segurança que os clientes devem usar tooconnect e assim por diante. Em vez de especificar essas políticas em cada servidor VPN ou Gateway de Área de Trabalho Remota (RD), essas políticas podem ser especificadas uma vez em um local central. Olá protocolo RADIUS fornece Olá centralizado autenticação, autorização e contabilização (AAA). 
* Estabelecer e impor políticas de integridade do cliente de proteção de acesso à rede (NAP) que determinam se os dispositivos recebem acesso restrita ou irrestrita toonetwork recursos.
* Fornecem um meio tooenforce autenticação e autorização para acessar os pontos de acesso sem fio compatíveis com too802.1x e switches Ethernet.    

Normalmente, as organizações usar toosimplify de NPS (RADIUS) e centralizar o gerenciamento de saudação de VPN políticas. No entanto, muitas organizações também usam o NPS toosimplify e centralizam o gerenciamento de saudação de diretivas de autorização de Conexão de área de trabalho da área de trabalho remota (RD CAPs). 

As organizações também podem integrar a segurança do Azure MFA tooenhance NPS e fornecer um alto nível de conformidade. Isso ajuda a garantir que os usuários estabelecer toolog de verificação em duas etapas no toohello Gateway de área de trabalho remota. Para usuários toobe de acesso, eles devem fornecer a combinação nome de usuário e senha com informações que Olá usuário tem em seu controle. Essas informações devem ser confiáveis e não facilmente duplicadas, como um número de telefone celular, o número de telefone fixo, o aplicativo em um dispositivo móvel e assim por diante.

Disponibilidade de toohello anterior de saudação extensão NPS para o Azure, os clientes que desejavam tooimplement verificação de duas etapas para integrado NPS e ambientes do Azure MFA tinham tooconfigure e mantêm um servidor separado do MFA no ambiente local Olá documentado no [Gateway de área de trabalho remota e servidor Azure multi-Factor Authentication usando RADIUS](multi-factor-authentication-get-started-server-rdg.md).

disponibilidade de saudação da extensão NPS Olá para o Azure agora oferece organizações Olá escolha toodeploy uma solução MFA com base no local ou um baseado em nuvem MFA solução toosecure RADIUS autenticação do cliente.

## <a name="authentication-flow"></a>Fluxo de autenticação

Para os usuários a toobe concedido acesso toonetwork recursos por meio de um Gateway de área de trabalho remota, devem atender às condições de saudação especificadas na diretiva de autorização uma Conexão de área de trabalho remota (RD CAP) e uma diretiva de autorização de recurso de área de trabalho remota (RD RAPS). RD CAPs especifique quem está autorizado tooconnect tooRD Gateways. Esse usuário Olá RD RAPs especificar recursos de rede hello, como áreas de trabalho remotas ou aplicativos remotos, é permitido tooconnect toothrough Olá Gateway de área de trabalho remota. 

Um Gateway de área de trabalho remota pode ser configurado toouse um repositório de política central para RD CAPs. RD RAPs não pode usar uma política central, como elas são processadas no hello Gateway de área de trabalho remota. Um exemplo de uma configuração de Gateway de área de trabalho remota toouse um repositório de política central para RD CAPs é um servidor NPS de tooanother de cliente RADIUS que serve como armazenamento de política central hello.

Quando Olá extensão NPS para o Azure é integrado com hello NPS e o Gateway de área de trabalho remota, o fluxo de autenticação bem-sucedida de saudação é o seguinte:

1. servidor de Gateway de área de trabalho remota de Olá recebe uma solicitação de autenticação de um recurso de tooa de tooconnect de usuário da área de trabalho remota, como uma sessão de área de trabalho remota. Servidor de Gateway de área de trabalho remota de Olá agindo como um cliente RADIUS, converte a mensagem de solicitação de acesso RADIUS Olá solicitação tooa e envia Olá mensagem toohello RADIUS servidor NPS () em que a extensão NPS hello está instalado. 
2. Olá nome de usuário e combinação de senha é verificada no Active Directory e Olá usuário é autenticado.
3. Se todos os Olá condições conforme especificado no Olá a solicitação de Conexão do NPS e Olá diretivas de rede são atendidas (por exemplo, hora do dia ou grupo de restrições de associação), Olá extensão NPS dispara uma solicitação de autenticação secundária com o Azure MFA. 
4. MFA do Azure se comunica com o Azure AD, recupera os detalhes do usuário hello e executa a autenticação secundária hello, usando o método hello configurado pelo usuário hello (mensagem de texto, aplicativo móvel e assim por diante). 
5. Após o sucesso da saudação desafio MFA, o Azure MFA se comunica extensão NPS Olá resultado toohello.
6. servidor NPS Olá onde extensão hello está instalado envia uma mensagem de aceitação de acesso RADIUS para o servidor de Gateway de área de trabalho remota do hello RD CAP política toohello.
7. Olá usuário recebe acesso toohello solicitou o recurso de rede por meio de saudação Gateway de área de trabalho remota.

## <a name="prerequisites"></a>Pré-requisitos
Esta seção detalha os pré-requisitos de saudação necessários para integrar o Azure MFA com hello Gateway de área de trabalho remota. Antes de começar, você deve ter Olá pré-requisitos no local a seguir.  

* Infraestrutura de Serviços de Área de Trabalho Remota (RDS)
* Licença do Azure MFA
* Software do Windows Server
* Função de Serviços de Acesso (NPS) e Política de Rede
* Azure AD sincronizado com o AD local 
* ID do GUID do Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infraestrutura de Serviços de Área de Trabalho Remota (RDS)
Você deve ter uma infraestrutura de Serviços de Área de Trabalho Remota (RDS) em vigor. Se você não fizer isso, em seguida, você pode criar essa infraestrutura rapidamente no Azure usando os seguintes Olá de início rápido modelo: [implantação Criar coleção de sessão de área de trabalho remota](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

Se desejar toomanually criar uma local RDS infraestrutura rapidamente para fins de teste, siga Olá etapas toodeploy um. 
**Saiba mais**: [Implantar RDS com início rápido do Azure](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) e [Implantação de infraestrutura de RDS básica](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Licenças
É necessário uma licença para o Azure MFA, que está disponível por meio de um Azure AD Premium, Enterprise Mobility + Security (EMS) ou uma assinatura de MFA. Para obter mais informações, consulte [como tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). Para fins de teste, você pode usar uma assinatura de avaliação.

### <a name="software"></a>Software
Olá extensão NPS requer o Windows Server 2008 R2 SP1 ou superior com o serviço de função NPS Olá instalado. Todas as etapas de saudação nesta seção foram realizadas usando o Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>Função de Serviços de Acesso (NPS) e Política de Rede
Olá, serviço de função NPS fornece cliente e servidor RADIUS de saudação funcionalidade, bem como o serviço de integridade de política de acesso de rede. Essa função deve ser instalada em pelo menos dois computadores em sua infraestrutura: Olá Gateway de área de trabalho remota e outro servidor membro ou controlador de domínio. Por padrão, a função hello já está presente no computador de saudação configurado como Olá Gateway de área de trabalho remota.  Também você deve instalar função do NPS Olá pelo menos em outro computador, como um controlador de domínio ou servidor membro.

Para obter informações sobre como instalar a função do NPS de saudação do serviço Windows Server 2012 ou anterior, consulte [instalar um servidor de política de integridade de NAP](https://technet.microsoft.com/library/dd296890.aspx). Para obter uma descrição de práticas recomendadas para NPS, inclusive tooinstall de recomendação de saudação NPS em um controlador de domínio, consulte [práticas recomendadas para NPS](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory sincronizado com o Active Directory local 
Olá toouse extensão NPS local usuários devem ser sincronizados com o Azure AD e habilitados para MFA. Esta seção pressupõe que os usuários locais são sincronizados com o Azure AD usando o AD Connect. Para obter informações sobre o Azure AD Connect, consulte [Integrar seus diretórios locais com o Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID do GUID do Azure Active Directory
tooinstall NPS, é necessário tooknow Olá GUID de saudação do AD do Azure. As instruções para localizar Olá GUID de saudação do AD do Azure são fornecidas abaixo.

## <a name="configure-multi-factor-authentication"></a>Configurar Autenticação Multifator 
Esta seção fornece instruções para integração do Azure MFA com hello Gateway de área de trabalho remota. Como administrador, você deve configurar o serviço de Azure MFA Olá antes que os usuários podem registrar seus dispositivos multifatores ou aplicativos.

Siga as etapas de saudação em [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](multi-factor-authentication-get-started-cloud.md) tooenable MFA para os usuários do AD do Azure. 

### <a name="configure-accounts-for-two-step-verification"></a>Configurar contas para verificação em duas etapas
Depois que uma conta foi habilitada para MFA, você não pode entrar tooresources regida Olá política da MFA até que você configurou com êxito um dispositivo confiável toouse para o segundo fator de autenticação Olá autenticado usando a verificação em duas etapas.

Siga as etapas de saudação em [o Azure multi-Factor Authentication significa para mim?](./end-user/multi-factor-authentication-end-user.md) toounderstand e configurar corretamente os dispositivos para MFA com sua conta de usuário.

## <a name="install-and-configure-nps-extension"></a>Instalar e configurar a extensão do NPS
Esta seção fornece instruções para configurar o RDS infraestrutura toouse MFA do Azure para autenticação de cliente com hello Gateway de área de trabalho remota.

### <a name="acquire-azure-active-directory-guid-id"></a>Obter a ID do GUID do Azure Active Directory

Como parte da configuração de saudação do hello extensão do NPS, você precisa toosupply credenciais de administrador e a ID do AD do Azure de saudação para seu locatário do AD do Azure. Olá, as etapas a seguir mostra como ID de locatário de saudação tooget.

1. Entrar toohello [portal do Azure](https://portal.azure.com) como administrador global de saudação do hello Azure locatário.
2. No hello barra de navegação esquerda, selecione Olá **Active Directory do Azure** ícone.
3. Selecione **Propriedades**.
4. Na folha de propriedades de saudação, ao lado de saudação ID de diretório, clique em Olá **cópia** ícone, conforme mostrado abaixo, toocopy Olá ID tooclipboard.

 ![Propriedades](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Instalar a extensão NPS Olá
Instale extensão do NPS Olá em um servidor que tem hello política de rede e a função Serviços de acesso (NPS) instalado. Isso funciona como servidor RADIUS de saudação para seu design. 

>[!Important]
> Certifique-se de que você não instalar extensão do hello NPS no servidor de Gateway de área de trabalho remota.
> 

1. Baixar Olá [extensão NPS](https://aka.ms/npsmfa). 
2. Copie o servidor NPS do hello instalação arquivo executável (NpsExtnForAzureMfaInstaller.exe) toohello.
3. No servidor NPS hello, clique duas vezes em **NpsExtnForAzureMfaInstaller.exe**. Se solicitado, clique em **Executar**.
4. Na Olá NPS extensão para a caixa de diálogo de Azure MFA, examinar os termos de licença de software hello, verifique **aceito os termos de licença toohello e condições**e clique em **instalar**.
 
  ![Instalação do Azure MFA](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Em Olá NPS extensão para a caixa de diálogo de MFA do Azure, clique em Fechar. 

  ![Extensão NPS para o Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurar certificados para uso com a extensão NPS hello usando um script do PowerShell
Em seguida, você precisa tooconfigure certificados para uso por Olá NPS extensão tooensure proteger as comunicações e garantia. componentes NPS Olá incluem um script do Windows PowerShell que configura um certificado autoassinado para uso com o NPS. 

script Hello executa Olá ações a seguir:

* Cria um certificado autoassinado
* Associa a chave pública do certificado tooservice principal no AD do Azure
* Olá de repositórios de certificado no repositório de computador local Olá
* Concede acesso de usuário de rede toohello chave privada do certificado toohello
* Reinicia o serviço do Servidor de Políticas de Rede

Se você quiser toouse seus próprios certificados, você precisa tooassociate Olá público de sua entidade de serviço de toohello de certificado no AD do Azure e assim por diante.

script de saudação toouse, forneça extensão Olá com suas credenciais de administrador do AD do Azure e Olá ID de locatário do AD do Azure que você copiou anteriormente. Execute o script de saudação em cada servidor NPS onde você instalou a extensão NPS hello. Em seguida, Olá a seguir:

1. Abra um prompt do Windows PowerShell administrativo.
2. No prompt do PowerShell hello, digite **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**e pressione **ENTER**.
3. Digite _.\AzureMfsNpsExtnConfigSetup.ps1_ e pressione **ENTER**. script Hello verifica toosee se o módulo do Azure Active Directory PowerShell hello está instalado. Se não estiver instalado, o script hello instala o módulo de saudação para você.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Depois que o script hello verifica a instalação de saudação do módulo do PowerShell Olá, ele exibe a caixa de diálogo de módulo hello Azure Active Directory PowerShell. Na caixa de diálogo hello, insira suas credenciais de administrador do AD do Azure e a senha e clique em **entrar**.

  ![Abra a conta do PowerShell](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Quando solicitado, cole a ID de locatário Olá copiado na área de transferência toohello antes e pressione **ENTER**.

  ![Inserir a ID do locatário](./media/nps-extension-remote-desktop-gateway/image6.png)

6. script Hello cria um certificado autoassinado e executa outras alterações de configuração. saída de Hello deve ser como imagem Olá mostrada abaixo.

  ![Certificado autoassinado](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Configurar componentes NPS no Gateway de Área de Trabalho Remota
Nesta seção, você pode configurar políticas de autorização de conexão de Gateway de área de trabalho remota hello e outras configurações de RADIUS.

o fluxo de autenticação Olá requer que as mensagens RADIUS sejam trocados entre Olá Gateway de área de trabalho remota e hello servidor NPS onde Olá servidor NPS está instalado. Isso significa que você deve configurar as configurações do cliente RADIUS no servidor NPS de Gateway de área de trabalho remota e hello em que a extensão NPS hello está instalado. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Configurar o Gateway de área de trabalho remota conexão autorização políticas toouse repositório central
Diretivas de autorização de conexão de área de trabalho remota (RD CAPs) especificam os requisitos de saudação para conectando tooa para o servidor de Gateway de área de trabalho remota. As RD CAPs podem ser armazenadas localmente (padrão) ou podem ser armazenadas em um repositório de RD CAP central que está executando o NPS. tooconfigure integração do Azure MFA com RDS, é necessário toospecify uso de saudação de um repositório central.

1. No servidor de Gateway de área de trabalho remota hello, abra **Gerenciador do servidor**. 
2. No menu de saudação, clique em **ferramentas**, ponto muito**Remote Desktop Services**e, em seguida, clique em **Gerenciador de Gateway de área de trabalho remota**.

  ![Serviços da Área de Trabalho Remota](./media/nps-extension-remote-desktop-gateway/image8.png)

3. Em Olá Gerenciador de Gateway de área de trabalho remota, clique com botão direito  **\[nome do servidor\] (Local)**e clique em **propriedades**.

  ![Nome do Servidor](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Na caixa de diálogo de propriedades de saudação, selecione Olá **RD CAP** guia repositório.
5. Na guia repositório RD CAP de saudação, selecione **servidor Central que executa o NPS**. 
6. Em Olá **Insira um nome ou endereço IP para o servidor de saudação que executa o NPS** campo, tipo hello endereço IP ou servidor de nome do servidor de saudação onde você instalou a extensão NPS hello.

  ![Insira o Nome ou o Endereço IP](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Clique em **Adicionar**.
8. Em Olá **segredo compartilhado** caixa de diálogo, digite um segredo compartilhado e, em seguida, clique em **Okey**. Certifique-se de registrar esse segredo compartilhado e armazene o registro de saudação com segurança.

 >[!NOTE]
 >Segredo compartilhado é usado tooestablish confiança entre clientes e servidores RADIUS de saudação. Crie uma senha longa e complexa.
 >

 ![Segredo compartilhado](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Clique em **Okey** tooclose caixa de diálogo de saudação.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Configurar o valor de tempo limite do RADIUS no NPS de Gateway de Área de Trabalho Remota
tooensure existe é as credenciais do usuário toovalidate de tempo, executar a verificação em duas etapas, receber respostas e responde a mensagens tooRADIUS, é necessário tooadjust valor de tempo limite RADIUS de saudação.

1. No servidor de Gateway de área de trabalho remota hello, no Gerenciador do servidor, clique em **ferramentas**e, em seguida, clique em **Network Policy Server**. 
2. Em Olá **NPS (Local)** de console, expanda **clientes e servidores RADIUS**e selecione **servidor RADIUS remoto**.

 ![Servidor RADIUS remoto](./media/nps-extension-remote-desktop-gateway/image12.png)

3. No painel de detalhes de saudação, clique duas vezes em **o grupo de servidor de GATEWAY TS**.

 >[!NOTE]
 >Este grupo de servidores RADIUS foi criado quando você configurou o servidor central de saudação para políticas NPS. Olá Gateway RD encaminha servidor RADIUS de toothis de mensagens ou grupo de servidores, se mais de um grupo de saudação.
 >

4. Em Olá **propriedades de grupo de servidores de GATEWAY TS** caixa de diálogo, o endereço IP hello select ou o nome de Olá servidor NPS configurado toostore RD CAPs e, em seguida, clique em **editar**. 

 ![Grupo de servidores Gateway TS](./media/nps-extension-remote-desktop-gateway/image13.png)

5. Em Olá **Editar servidor RADIUS** caixa de diálogo, selecione Olá **balanceamento de carga** guia.
6. Em hello **balanceamento de carga** guia Olá **o número de segundos sem resposta antes que uma solicitação é considerada ignorados** campo, altere o valor padrão de saudação do valor de 3 tooa entre 30 e 60 segundos.
7. Em Olá **número de segundos entre as solicitações ao servidor é identificado como indisponível** campo, altere o valor padrão de saudação do valor de tooa de 30 segundos é igual tooor maior que o valor de saudação especificado na etapa anterior hello.

 ![Editar servidor RADIUS](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Clique em Okey duas vezes tooclose caixas de diálogo de saudação.

### <a name="verify-connection-request-policies"></a>Verifique as Políticas de Solicitação de Conexão 
Por padrão, quando você configura o Gateway de área de trabalho remota de saudação toouse um repositório central de política para políticas de autorização de conexão, Olá Gateway de área de trabalho remota é servidor NPS configurado tooforward CAP solicitações toohello. servidor NPS Olá com extensão de Azure MFA Olá instalado, solicitação de acesso processos Olá RADIUS. Olá, as etapas a seguir mostra como diretiva de solicitação de conexão do tooverify saudação padrão. 

1. Em Olá Gateway de área de trabalho remota no console do NPS (Local) hello, expanda **políticas**e selecione **diretivas de solicitação de Conexão**.
2. Clique com o botão direito em **Políticas de Solicitação de Conexão** e clique duas vezes em **POLÍTICA DE AUTORIZAÇÃO DE GATEWAY TS**.
3. Em Olá **propriedades de diretiva de autorização de GATEWAY TS** caixa de diálogo, clique em Olá **configurações** guia.
4. Na guia **Configurações**, em Encaminhamento de Solicitação de Conexão, clique em **Autenticação**. Cliente RADIUS é configurado tooforward solicitações de autenticação.

 ![Configurações de Autenticação](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Clique em **Cancelar**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Configurar o NPS no servidor de saudação onde Olá extensão NPS está instalado
servidor NPS Olá onde a extensão NPS Olá é necessidades instalado toobe tooexchange capaz de RADIUS mensagens com servidor NPS Olá Olá Gateway de área de trabalho remota. tooenable essa mensagem do exchange, você precisará tooconfigure Olá NPS componentes no servidor de saudação onde Olá serviço de extensão do NPS está instalado. 

### <a name="register-server-in-active-directory"></a>Registrar o Servidor no Active Directory
toofunction corretamente nesse cenário, o servidor NPS de saudação precisa toobe registrado no Active Directory.

1. Abra o **Gerenciador do Servidor**.
2. No Gerenciador do Servidor, clique em **Ferramentas**e, em seguida, clique em **Servidor de Políticas de Rede**. 
3. No console do servidor de políticas de rede hello, clique com botão direito **NPS (Local)**e, em seguida, clique em **registrar servidor no Active Directory**. 
4. Clique em **OK** duas vezes.

 ![Registrar servidor no AD](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Deixe o console de saudação aberta para o procedimento a seguir hello.

### <a name="create-and-configure-radius-client"></a>Criar e configurar o cliente RADIUS 
saudação de Gateway de área de trabalho remota deve toobe configurado como servidor RADIUS cliente toohello NPS. 

1. No servidor NPS Olá onde Olá extensão NPS está instalado no hello **NPS (Local)** console, clique com botão direito **clientes RADIUS** e clique em **novo**.

 ![Novos clientes RADIUS](./media/nps-extension-remote-desktop-gateway/image17.png)

2. Em Olá **cliente RADIUS novo** caixa de diálogo caixa, forneça um nome amigável, como _Gateway_, e Olá endereço IP ou nome DNS do servidor de Gateway de área de trabalho remota hello. 
3. Em Olá **segredo compartilhado** e hello **Confirmar segredo compartilhado** campos, digite Olá mesmo segredo usado anteriormente.

 ![Nome e Endereço](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Clique em **Okey** caixa de diálogo tooclose Olá RADIUS novo cliente.

### <a name="configure-network-policy"></a>Configurar Política de Rede
Lembre-se de servidor NPS Olá com hello extensão do Azure MFA é Olá política central designado armazenamento Olá diretiva de autorização de Conexão (CAP). Portanto, você precisa tooimplement um limite em Olá NPS server tooauthorize conexões válidas solicitações.  

1. No console do NPS (Local) hello, expanda **políticas**e clique em **políticas de rede**.
2. Clique com botão direito **servidores de acesso para conexões tooother**e clique em **duplicado política**. 

 ![Duplicar Política](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Clique com botão direito **servidores de acesso à cópia de conexões tooother**e clique em **propriedades**.

 ![Propriedades da Rede](./media/nps-extension-remote-desktop-gateway/image20.png)

4. Em Olá **servidores de acesso à cópia de conexões tooother** caixa de diálogo, no nome da diretiva, insira um nome adequado, como **RDG_CAP**. Marque **Política Habilitada** e selecione **Conceder acesso**. Opcionalmente, em Tipo de acesso à rede, selecione **Gateway de Área de Trabalho Remota**, ou você pode deixá-lo como **Não especificado**.

 ![Cópia de Conexões](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Clique em Olá **restrições** guia e verificar **permitir que os clientes tooconnect sem negociar um método de autenticação**.

 ![Permitir que os clientes tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Opcionalmente, clique em Olá **condições** guia e adicionar as condições que devem ser atendidas para Olá conexão toobe autorizado, por exemplo, a associação em um grupo específico do Windows.

 ![Condições](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Clique em **OK**. Quando solicitada tooview hello tópico da Ajuda correspondente, clique em **não**.
8. Certifique-se de que a nova política é na parte superior de saudação da lista de saudação, que a política de saudação está habilitada, e que ele concede acesso.

 ![Políticas de Rede](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Verificar a configuração
configuração de saudação tooverify, é necessário toolog em Olá Gateway de área de trabalho remota com um cliente RDP adequado. Ser toouse-se de uma conta que é permitida por suas políticas de autorização de Conexão e está habilitada para o Azure MFA. 

Como é mostrado na imagem de saudação abaixo, você pode usar o hello **Remote Desktop Web Access** página.

![Acesso via Web da Área de Trabalho Remota](./media/nps-extension-remote-desktop-gateway/image25.png)

Ao entrar com êxito suas credenciais para autenticação primária, a caixa de diálogo de conexão de área de trabalho remota Olá mostra um status de iniciar a conexão remota, conforme mostrado abaixo. 

Se autenticar com êxito com o método de autenticação secundário Olá que previamente configurados no Azure MFA, você está conectado toohello recursos. No entanto, se a autenticação secundária Olá não for bem-sucedida, recebem acesso tooresource. 

![Iniciar conexão remota](./media/nps-extension-remote-desktop-gateway/image26.png)

Exemplo hello abaixo, Olá autenticador de aplicativo em um Windows phone é autenticação secundária do hello tooprovide usado.

![Contas](./media/nps-extension-remote-desktop-gateway/image27.png)

Depois de autenticado com êxito usando o método de autenticação secundário hello, você está conectado ao Olá Gateway de área de trabalho remota como normal. No entanto, como é necessário toouse um método de autenticação secundário usando um aplicativo móvel em um dispositivo confiável, Olá log no processo é mais seguro do que seria caso contrário.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Exibir logs do Visualizador de Eventos para eventos de logon com sucesso
tooview Olá bem-sucedida entrar eventos nos logs do Visualizador de eventos do Windows hello, você pode emitir Olá Olá tooquery de comando do Windows PowerShell dos serviços de Terminal do Windows e logs de segurança do Windows a seguir.

tooquery eventos de entrada bem-sucedida em logs operacionais do Gateway Olá _(eventos\logs e serviços Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, use Olá comandos a seguir:

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | onde {$_.ID -eq '300'} | FL 
* Este comando exibe os eventos do Windows que mostram o usuário Olá atendido os requisitos de diretiva de autorização de recursos (RD RAPS) e foi concedido acesso.

![Exibir Visualizador de Eventos](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | onde {$_.ID -eq '200'} | FL
* Este comando exibe os eventos de saudação que aparecem quando o usuário atendeu aos requisitos de diretiva de autorização de conexão.

![Autorização de conexão](./media/nps-extension-remote-desktop-gateway/image29.png)

Você também pode exibir esse log e o filtro nas IDs de evento, 300 e 200. eventos de logon bem-sucedidos tooquery em logs do Visualizador de eventos de segurança de hello, use Olá comando a seguir:

* _Get-WinEvent -Logname Security_ | onde {$_.ID -eq '6272'} | FL 
* Este comando pode ser executado em uma Olá NPS central ou Olá servidor de Gateway de área de trabalho remota. 

![Eventos de logon com sucesso](./media/nps-extension-remote-desktop-gateway/image30.png)

Você também pode exibir o log de segurança hello ou Olá exibição personalizada serviços de acesso e política de rede, conforme mostrado abaixo:

![Serviços de Acesso (NPS) e Política de Rede](./media/nps-extension-remote-desktop-gateway/image31.png)

No servidor de saudação onde você instalou a extensão NPS Olá para o Azure MFA, você pode encontrar os logs de aplicativo de Visualizador de eventos extensão toohello específico em _aplicativos e serviços Logs\Microsoft\AzureMfa_. 

![Logs de aplicativo do Visualizador de Eventos](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Guia de Solução de Problemas

Se a configuração de saudação não está funcionando conforme o esperado, Olá primeiro lugar toostart tootroubleshoot é tooverify que Olá usuário toouse configurado o Azure MFA. Tem usuário Olá conectar toohello [portal do Azure](https://portal.azure.com). Se os usuários são solicitados para verificação secundária e são autenticados com sucesso, você pode eliminar uma configuração incorreta do Azure MFA.

Se estiver funcionando Azure MFA para usuários Olá, você deve revisar logs de eventos relevantes Olá. Isso inclui logs de eventos de segurança, o Gateway operacional e o Azure MFA Olá que são discutidos na seção anterior hello. 

Abaixo está um exemplo de saída do log de segurança mostrando um evento de logon com falha (Evento ID 6273).

![Eventos de logon com falha](./media/nps-extension-remote-desktop-gateway/image33.png)

Abaixo está um evento relacionado de saudação AzureMFA logs:

![Log do Azure MFA](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform avançado solucionar problemas de opções, consulte Olá NPS banco de dados formato arquivos de log onde Olá serviço NPS está instalado. Esses arquivos de log são criados na pasta _%SystemRoot%\System32\Logs_ como arquivos de texto separado por vírgula. 

Para obter uma descrição desses arquivos de log, consulte [Interpretar arquivos de log de formato de banco de dados de NPS](https://technet.microsoft.com/library/cc771748.aspx). entradas de saudação nesses arquivos de log podem ser difícil toointerpret sem importá-los em uma planilha ou um banco de dados. Você pode encontrar vários analisadores de IAS tooassist online você interpretar Olá arquivos de log. 

Olá, imagem abaixo mostra a saída Olá de um para esse download [shareware aplicativo](http://www.deepsoftware.com/iasviewer). 

![Aplicativo shareware](./media/nps-extension-remote-desktop-gateway/image35.png)

E, por último, para mais opções de solução de problemas, você pode usar um analisador de protocolo, como o [Analisador de Mensagens da Microsoft](https://technet.microsoft.com/library/jj649776.aspx). 

a imagem abaixo da Microsoft Message Analyzer Hello mostra filtrado no protocolo RADIUS que contém o nome de usuário de saudação do tráfego de rede **Contoso\AliceC**.

![Analisador de Mensagens da Microsoft](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Próximas etapas
[Como tooget autenticação multifator do Azure](multi-factor-authentication-versions-plans.md)

[Gateway de Área de Trabalho Remota e Servidor Azure Multi-Factor Authentication usando RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrar seus diretórios locais no Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
