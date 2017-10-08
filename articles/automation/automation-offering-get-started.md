---
title: "AAA Introdução à automação do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral do serviço de automação do Azure examinando Olá detalhes de design e implementação em Olá tooonboard de preparação da oferta do Azure Marketplace."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Introdução à Automação do Azure

Este guia de Introdução ao obter apresenta os principais conceitos relacionados toohello implantação de automação do Azure. Se você estiver tooAutomation novo no Azure ou têm experiência com o software de fluxo de trabalho de automação como o System Center Orchestrator, este guia ajuda a entender como tooprepare e automação integrada.  Posteriormente, você estará preparado toobegin runbooks para oferecer suporte a suas necessidades de automação do processo de desenvolvimento. 


## <a name="automation-architecture-overview"></a>Visão geral de arquitetura de automação

![Visão geral da Automação do Azure](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Automação do Azure é um software como um aplicativo de serviço (SaaS) que fornece um multilocatário escalonável e confiável, ambiente tooautomate processa com runbooks e gerenciar tooWindows de alterações de configuração e os sistemas Linux usando a configuração de estado desejado (DSC) do Azure, serviços de nuvem ou local. Entidades contidas dentro de sua conta de automação, como runbooks, ativos, contas executar como são isoladas de outras contas de automação em sua assinatura e outras assinaturas.  

Runbooks que são executados no Azure são executados em áreas restritas de automação, que são hospedadas na plataforma do Azure como uma máquina virtual de serviço (PaaS).  Áreas restritas de automação fornecem isolamento de locatários para todos os aspectos de execução de runbook – módulos, armazenamento, memória, comunicação de rede, fluxos de trabalho etc. Essa função é gerenciada pelo serviço hello e não está acessível da sua conta do Azure ou a automação do Azure para você toocontrol.         

implantação de saudação tooautomate e gerenciamento de recursos em seu datacenter local ou outros serviços em nuvem, depois de criar uma conta de automação, você pode designar Olá de toorun de máquinas de um ou mais [Hybrid Runbook Worker (HRW)](automation-hybrid-runbook-worker.md) função.  Cada HRW requer Olá Microsoft Management Agent com um espaço de trabalho de análise de Log de tooa de conexão e uma conta de automação.  Análise de log é usado toobootstrap Olá instalação, manter Olá Microsoft Management Agent e monitorar a funcionalidade de saudação do hello HRW.  entrega de saudação de runbooks e hello toorun de instrução, que elas são executadas por automação do Azure.

Você pode implantar vários HRW tooprovide alta disponibilidade para seus runbooks, trabalhos de runbook de balanceamento de carga e em alguns casos dedicá-los para cargas de trabalho específicas ou ambientes.  Olá Microsoft Monitoring Agent em Olá HRW inicia a comunicação com o serviço de automação de hello pela porta TCP 443 e não há requisitos de firewall de entrada.  Depois de você ter runbook em execução em um HRW no ambiente de saudação e você deseja que as tarefas de gerenciamento de tooperform Olá runbook em relação a outras máquinas ou serviços no ambiente, pode haver outras portas que Olá runbook precisa acessar.  Se suas políticas de segurança de TI não permitir que os computadores em sua toohello tooconnect de rede da Internet, examine o artigo Olá [OMS Gateway](../log-analytics/log-analytics-oms-gateway.md), que atua como um proxy para Olá HRW toocollect status do trabalho e receber informações de configuração sua conta de automação.

Runbooks em execução em um HRW executado no contexto de saudação de conta do sistema local Olá no computador de saudação, que é Olá recomendado contexto de segurança ao executar ações administrativas no computador local de Windows hello. Se desejar que tarefas de toorun runbook Olá contra recursos fora do computador local hello, talvez seja necessário toodefine ativos de credencial seguro Olá conta de automação que você pode acessar de runbook hello e usar tooauthenticate com recursos externos hello. Você pode usar [credencial](automation-credentials.md), [certificado](automation-certificates.md), e [Conexão](automation-connections.md) ativos no seu runbook com os cmdlets que permitem que você toospecify credenciais para que você possa autenticá-los.

As configurações de DSC armazenadas na automação do Azure podem ser máquinas virtuais de tooAzure aplicadas diretamente. Outras máquinas físicas e virtuais podem solicitar configurações do servidor de pull de DSC de automação do Azure hello.  Para gerenciar configurações de seu local físicos ou virtuais sistemas Windows e Linux, você não precisa toodeploy qualquer servidor de pull de DSC de automação no infraestrutura toosupport hello, acesso à Internet somente saído em cada toobe sistema gerenciado pelo DSC de automação , se comunicar por serviço OMS do TCP porta 443 toohello.   

## <a name="prerequisites"></a>Pré-requisitos

### <a name="automation-dsc"></a>DSC de automação
DSC de automação do Azure pode ser usado toomanage várias máquinas:

* Máquinas virtuais do Azure (clássico) executando Windows ou Linux
* Máquinas virtuais do Azure executando Windows ou Linux
* Máquinas virtuais da Amazon Web Services (AWS) executando Windows ou Linux
* Máquinas locais físicas/virtuais do Windows, ou em uma nuvem diferente do Azure/AWS
* Máquinas locais físicas/virtuais do Linux, ou em uma nuvem diferente do Azure/AWS

versão mais recente de saudação do WMF 5 deve ser instalado para agente do DSC do PowerShell Olá para Windows toobe capaz de toocommunicate na automação do Azure. versão mais recente de saudação do hello [agente do DSC do PowerShell para Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) deve estar instalado para Linux toobe capaz de toocommunicate na automação do Azure.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
Ao designar um runbook do computador toorun híbrido trabalhos, este computador deve ter o seguinte hello:

* Windows Server 2012 ou posterior
* Windows PowerShell 4.0 ou posterior.  É recomendável instalar o Windows PowerShell 5.0 no computador Olá para aumentar a confiabilidade. Você pode baixar a versão nova de saudação do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Mínimo de dois núcleos
* Mínimo de 4 GB de RAM

### <a name="permissions-required-toocreate-automation-account"></a>Permissões necessárias toocreate conta de automação
toocreate ou atualização de uma conta de automação, você deve ter Olá privilégios específicos a seguir e as permissões necessárias toocomplete neste tópico.   
 
* Em ordem toocreate uma conta de automação, sua conta de usuário do AD precisa toobe tooa adicionado função com a função de proprietário de toohello equivalente de permissões para recursos do Microsoft conforme descrito no artigo [controle de acesso baseado em função na automação do Azure ](automation-role-based-access-control.md).  
* Se os registros do aplicativo hello configuração está definido muito**Sim**, usuários não administradores em seu locatário do AD do Azure podem [registrar aplicativos AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Se os registros do aplicativo hello configuração está definido muito**não**, usuário Olá executar essa ação deve ser um administrador global no AD do Azure. 

Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello administrador/coadministrador função global da assinatura hello, são adicionados o tooActive diretório como convidado. Nessa situação, você receberá um "você não tem permissões toocreate..." saudação de aviso **adicionar conta de automação** folha. Os usuários que foram adicionados toohello administrador/coadministrador função global primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory. tooverify nesta situação, do hello **Active Directory do Azure** painel Olá portal do Azure, selecione **usuários e grupos**, selecione **todos os usuários** e, depois de selecionar Olá usuário específico, selecione **perfil**. Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.

## <a name="authentication-planning"></a>Planejamento de autenticação
Automação do Azure permite que você tooautomate tarefas com base nos recursos no Azure, no local e com outros provedores de nuvem.  Para que um runbook tooperform suas ações requeridas, ele deve ter permissões toosecurely acessar Olá recursos com direitos mínimos do hello exigidos na assinatura de saudação.  

### <a name="what-is-an-automation-account"></a>O que é uma Conta de Automação 
Todas as tarefas de automação Olá que executar com base nos recursos usando Olá cmdlets do Azure na automação do Azure autenticam tooAzure usando a autenticação baseada em credenciais do Active Directory do Azure identidade organizacional.  Uma conta de automação é separada da conta Olá uso toosign em tooconfigure portal toohello e o uso de recursos do Azure.  Os recursos de automação incluídos com uma conta são seguinte hello:

* **Certificados** - contém um certificado usado para autenticação de um runbook ou a configuração DSC ou adicioná-los.
* **Conexões** -contém a autenticação e a configuração de informações necessárias tooconnect tooan serviço ou aplicativo de um runbook ou a configuração DSC.
* **Credenciais** -é um objeto PSCredential que contém as credenciais de segurança, como um nome de usuário e senha necessária tooauthenticate de um runbook ou a configuração DSC.
* **Módulos de integração** -são módulos do PowerShell incluídos com um uso de cmdlets em runbooks e as configurações DSC toomake de conta de automação do Azure.
* **Agendas** - contém agendamentos que iniciam ou interrompem um runbook em um horário especificado, incluindo frequências recorrentes.
* **Variáveis** - contêm valores que estão disponíveis de um runbook ou configuração DSC.
* **Configurações DSC** -são scripts do PowerShell que descreve como tooconfigure um recurso do sistema operacional ou a configuração ou instalar um aplicativo em um computador Windows ou Linux.  
* **Runbooks** -são um conjunto de tarefas que executa um processo automatizado na Automação do Azure baseado no Windows PowerShell.    

recursos de automação Olá para cada conta de automação estão associados uma única região do Azure, mas as contas de automação podem gerenciar todos os recursos de saudação em sua assinatura. Crie contas de automação em regiões diferentes, se você tiver políticas que exigem que dados e recursos toobe tooa isolado específico região.

> [!NOTE]
> Contas de automação e recursos Olá contiverem que são criados no hello portal do Azure, não pode ser acessado no hello portal clássico do Azure. Se você quiser toomanage essas contas ou seus recursos com o Windows PowerShell, você deve usar os módulos do Azure Resource Manager hello.
> 

Quando você cria uma conta de automação em Olá portal do Azure, você cria automaticamente duas entidades de autenticação:

* Uma conta Executar como. Essa conta cria uma entidade de serviço no Azure AD (Azure Active Directory) e um certificado. Ele também atribui Olá Colaborador acesso baseado em função RBAC (controle), que gerencia os recursos do Gerenciador de recursos por meio de runbooks.
* Uma conta Executar como clássica. Essa conta carrega um certificado de gerenciamento, que é usado toomanage os recursos clássicos usando runbooks.

Controle de acesso baseado em função está disponível com o Azure Resource Manager toogrant permitido a conta de usuário do AD do Azure de tooan de ações e conta executar como e autenticar essa entidade de serviço.  Leitura [controle de acesso baseado em função no artigo de automação do Azure](automation-role-based-access-control.md) para obter mais informações toohelp desenvolver seu modelo para gerenciar permissões de automação.  

#### <a name="authentication-methods"></a>Métodos de autenticação
Olá tabela a seguir resume os métodos de autenticação diferentes Olá para cada ambiente com o suporte de automação do Azure.

| Método | Ambiente 
| --- | --- | 
| Contas Executar como do Azure e Executar como clássica |Implantação clássica do Azure de Azure Resource Manager |  
| Conta de Usuário do Azure AD |Implantação clássica do Azure de Azure Resource Manager |  
| Autenticação do Windows |Data center local ou outro provedor de nuvem usando Olá Hybrid Runbook Worker |  
| Credenciais do AWS |Amazon Web Services |  

Em Olá **como to\Authentication e segurança** seção, oferece suporte a artigos fornecendo etapas de implementação e visão geral da autenticação tooconfigure para esses ambientes, com um existente ou nova conta Dedique para esse ambiente.  Olá executar como do Azure e clássico executar como conta, Olá tópico [atualização automação conta executar como do](automation-create-runas-account.md) descreve como tooupdate sua conta de automação existente com hello executados como contas do portal de saudação ou usando o PowerShell se não foi originalmente configurado com uma conta executar como ou clássico executar como. Se você desejar toocreate executar como e uma conta clássico executar como com um certificado emitido por sua autoridade de certificação (CA), examine este toolearn artigo como toocreate Olá contas usando essa configuração.     
 
## <a name="network-planning"></a>Planejamento da rede
Para Olá register tooand de tooconnect Hybrid Runbook Worker com o Microsoft Operations Management Suite (OMS), ele deve ter acesso toohello número da porta e URLs de saudação descritos abaixo.  Além disso, isso é toohello [portas e URLs necessárias para Olá Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Se você usar um servidor proxy para comunicação entre o agente hello e serviço OMS Olá, é necessário tooensure que os recursos adequados Olá estejam acessíveis. Se você usar um toohello de acesso do firewall toorestrict da Internet, você precisa tooconfigure seu firewall toopermit acesso.

informações de saudação abaixo a porta da lista hello e URLs que são necessários para Olá Hybrid Runbook Worker toocommunicate com automação.

* Porta: somente a TCP 443 é necessária para acesso de Internet de saída
* URL global: *.azure-automation.net

Se você tiver uma conta de automação definida para uma região específica e você desejar toorestrict comunicação com esse data center regional, hello tabela a seguir fornece o registro de DNS Olá para cada região.

| **Região** | **Registro DNS** |
| --- | --- |
| Centro-Sul dos Estados Unidos |scus-jobruntimedata-prod-su1.azure-automation.net |
| Leste dos EUA 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Centro-Oeste dos EUA | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europa Ocidental |we-jobruntimedata-prod-su1.azure-automation.net |
| Norte da Europa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Canadá Central |cc-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste da Ásia |sea-jobruntimedata-prod-su1.azure-automation.net |
| Índia Central |cid-jobruntimedata-prod-su1.azure-automation.net |
| Leste do Japão |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste da Austrália |ase-jobruntimedata-prod-su1.azure-automation.net |
| Sul do Reino Unido | uks-jobruntimedata-prod-su1.azure-automation.net |
| Gov. dos EUA – Virgínia | usge-jobruntimedata-prod-su1.azure-automation.us |

Para obter uma lista de endereços IP em vez de nomes, baixe e leia Olá [endereço IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) arquivo xml de saudação Microsoft Download Center. 

> [!NOTE]
> Este arquivo contém Olá intervalos de endereços IP (inclusive intervalos de computação, SQL e armazenamento) usados em Olá data centers do Microsoft Azure. Um arquivo atualizado é postado semanal que reflete os intervalos de saudação atualmente implantado e quaisquer intervalos IP toohello alterações futuras. Novos intervalos que aparecem no arquivo hello não serão usados em datacenters Olá pelo menos uma semana. . Download Olá novo xml toda semana de arquivos e realizar as alterações necessárias Olá em seu site toocorrectly identificar os serviços em execução no Azure. Usuários de rota expressos podem observar que esse arquivo usado tooupdate Olá anúncio de BGP de espaço do Azure em Olá primeira semana de cada mês. 
> 

## <a name="creating-an-automation-account"></a>Criação de uma conta de automação

Há diferentes maneiras de que criar uma conta de automação em Olá portal do Azure.  Olá a tabela a seguir apresenta cada tipo de experiência de implantação e as diferenças entre eles.  

|Método | Descrição |
|-------|-------------|
| Selecione o controle e automação da saudação Marketplace | Uma oferta, que cria uma conta de automação e o espaço de trabalho do OMS vinculado tooone outro em Olá mesmo grupo de recursos e região.  Integração com o OMS também inclui o benefício de saudação do uso de análise de Log toomonitor e analisar os fluxos de trabalho e o status do trabalho de runbook ao longo do tempo e utilizar recursos avançados tooescalate ou investigar problemas. Olá oferta também implanta Olá controle de alterações e gerenciamento de atualização de soluções, que são habilitadas por padrão. |
| Selecione a automação da saudação Marketplace | Cria uma conta de automação em um grupo de recursos novos ou existentes que não está vinculado tooan espaço de trabalho do OMS e não inclui todas as soluções disponíveis na oferta de automação e controle de saudação. Isso é uma configuração básica que apresenta tooAutomation e pode ajudá-lo a aprender como toowrite runbooks, configurações de DSC e use Olá recursos de serviço de saudação. |
| Soluções de gerenciamento selecionadas | Se você escolher uma solução –  **[Update Management](../operations-management-suite/oms-solution-update-management.md)**,  **[VMs iniciar/parar durante horários](automation-solution-vm-management.md)**, ou  **[ Controle de alterações](../log-analytics/log-analytics-change-tracking.md)**  eles solicitará que você tooselect uma automação existente e o espaço de trabalho do OMS ou oferecer Olá toocreate opção tanto conforme necessário para Olá solução toobe implantado na sua assinatura. |

Este tópico orienta a criação de uma conta de automação e o espaço de trabalho do OMS pela oferta de automação e controle de integração hello.  toocreate uma conta de automação para o serviço de saudação testes ou toopreview, Olá revisão artigo a seguir independente [criar conta de automação autônomo](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Como criar uma Conta de automação integrada com o OMS
Olá recomendado tooonboard método que automação é selecionando oferta de automação e controle de saudação do hello Marketplace.  Isso cria uma conta de automação ambos e estabelece integração Olá com um espaço de trabalho do OMS, incluindo Olá opção tooinstall Olá soluções de gerenciamento que estão disponíveis com a oferta de saudação.  

1. Entrar toohello portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.

2. Clique em **Novo**.<br><br> ![Selecione a opção Novo no portal do Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Procurar **automação** e, em seguida, em Olá resultados da pesquisa selecione **controle e automação***.<br><br> ![Pesquise e selecione Automação e controle no Marketplace](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Depois de ler a descrição de saudação para oferta hello, clique em **criar**.  

5. Em Olá **controle e automação** folha de configurações, selecione **espaço de trabalho do OMS**.  Em Olá **espaços de trabalho do OMS** folha, selecione um toohello de espaço de trabalho vinculado OMS mesma assinatura do Azure que Olá conta de automação está em ou crie um espaço de trabalho do OMS.  Se você não tem um espaço de trabalho do OMS, selecione **criar novo espaço de trabalho** e Olá **espaço de trabalho do OMS** folha executar seguinte hello: 
   - Especifique um nome para Olá novo **espaço de trabalho do OMS**.
   - Selecione um **assinatura** toolink tooby selecionando na lista suspensa de saudação se padrão Olá selecionado não é apropriado.
   - Em **Grupo de Recursos**, você pode selecionar um grupo de recursos existente ou criar um novo.  
   - Selecione um **Local**.  Atualmente o hello únicos locais disponíveis são **Sudeste da Austrália**, **Leste dos EUA**, **Sudeste da Ásia**, **Central Oeste dos EUA**e  **Europa Ocidental**.
   - Selecione um **tipo de preço**.  solução de saudação é oferecida em duas camadas: gratuito e de camada por nó (OMS).  camada gratuita Olá tem um limite na quantidade de saudação dos dados coletados diariamente, período de retenção e minutos de tempo de execução do trabalho de runbook.  Olá por nó (OMS) nível não tem um limite na quantidade de saudação de dados coletados diariamente.  
   - Selecione **Conta de Automação**.  Se você estiver criando um novo espaço de trabalho do OMS, é necessário tooalso criar uma conta de automação está associada com hello novo espaço de trabalho OMS especificado anteriormente, incluindo sua assinatura do Azure, o grupo de recursos e a região.  Você pode selecionar **criar uma conta de automação** e Olá **conta de automação** folha, fornecer Olá seguintes: 
  - Em Olá **nome** campo, digite nome Olá Olá conta de automação.

    Todas as outras opções são preenchidas automaticamente com base no espaço de trabalho do OMS Olá selecionado e essas opções não podem ser modificadas.  Uma conta executar como do Azure é o método de autenticação de padrão de saudação para oferta hello.  Depois de clicar em **Okey**, opções de configuração de saudação são validadas e Olá conta de automação é criado.  Você pode acompanhar seu progresso em **notificações** menu hello. 

    Caso contrário, selecione uma conta Executar como de Automação existente.  conta de saudação selecionada não pode ser vinculado tooanother espaço de trabalho do OMS, caso contrário, uma mensagem de notificação é apresentada na folha de saudação.  Se já estiver vinculado, você precisa tooselect uma conta executar como automação diferente ou crie uma.

    Depois de concluir as informações de saudação necessárias, clique em **criar**.  informações de saudação são verificadas e Olá conta de automação contas executar como e são criadas.  Você retorna toohello **espaço de trabalho do OMS** folha automaticamente.  

6. Depois de fornecer informações de saudação necessárias em Olá **espaço de trabalho do OMS** folha, clique em **criar**.  Enquanto as informações de saudação são verificadas e espaço de trabalho de saudação é criado, você pode acompanhar seu progresso em **notificações** menu hello.  Você retorna toohello **adicionar solução** folha.  

7. Em Olá **controle e automação** folha de configurações, confirme tooinstall Olá recomendado soluções previamente selecionadas. Se você anular a seleção, você pode instalá-los individualmente mais tarde.  

8. Clique em **criar** tooproceed com automação de integração e um espaço de trabalho do OMS. Todas as configurações são validadas e, em seguida, ele tenta toodeploy Olá oferta em sua assinatura.  Esse processo pode levar vários segundos toocomplete e você pode acompanhar seu progresso em **notificações** menu hello. 

Após a oferta de saudação incorporados, você pode começar a criar soluções de gerenciamento que você habilitou de runbooks, trabalhar com hello, implantar um [Hybrid Runbook worker](automation-hybrid-runbook-worker.md) função, ou começar a trabalhar com [análise de Log](https://docs.microsoft.com/azure/log-analytics) dados de toocollect gerados por recursos no seu ambiente de nuvem ou local.   

## <a name="next-steps"></a>Próximas etapas
* Você pode confirmar que a sua nova conta de automação pode autenticar em recursos do Azure em [Como testar a autenticação da conta Executar como de Automação do Azure](automation-verify-runas-authentication.md).
* tooget iniciado com a criação de runbooks, primeiro examine Olá [tipos de automação de runbook](automation-runbook-types.md) com suporte e relacionados considerações antes de você começar a criar.


