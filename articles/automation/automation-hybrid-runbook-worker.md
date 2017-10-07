---
title: "aaaAzure automação Hybrid Runbook Workers | Microsoft Docs"
description: "Este artigo fornece informações sobre como instalar e usar Hybrid Runbook Worker, que é um recurso de automação do Azure que permite toorun runbooks em computadores no seu datacenter local ou o provedor de nuvem."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Automatizar recursos em seu data center ou nuvem com Hybrid Runbook Worker
Runbooks na automação do Azure não pode acessar recursos em outras nuvens ou em seu ambiente local, já que são executados na nuvem do Azure de saudação.  Olá Hybrid Runbook Worker recurso de automação do Azure permite toorun runbooks diretamente no computador de saudação hospeda função hello e com base nos recursos em Olá ambiente toomanage esses recursos locais. Runbooks são armazenados e gerenciados na automação do Azure e, em seguida, entregue tooone ou mais computadores designados.  

Essa funcionalidade é ilustrada no Olá a imagem a seguir:<br>  

![Visão geral do Runbook Worker Híbrido](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Para obter uma visão geral técnica de saudação Hybrid Runbook Worker função e considerações de implantação, consulte [visão geral da arquitetura automação](automation-offering-get-started.md#automation-architecture-overview).    

## <a name="hybrid-runbook-worker-groups"></a>Grupos de Runbook Worker Híbrido
Cada Hybrid Runbook Worker é membro de um grupo do Hybrid Runbook Worker que você especifica ao instalar o agente de saudação.  Um grupo pode conter um único agente, mas você pode instalar vários agentes em um grupo para ter alta disponibilidade.

Quando você iniciar um runbook em um trabalho de Runbook híbrido, você especificar o grupo de saudação que é executado.  membros de saudação do grupo de saudação determinam qual trabalho serviços de solicitação de saudação.  Você não pode especificar um trabalhador específico.

## <a name="relationship-tooservice-management-automation"></a>Relação tooService automação de gerenciamento
[Service Management Automation (SMA)](https://technet.microsoft.com/library/dn469260.aspx) permite que você toorun Olá mesmo runbooks de automação do Azure no seu data center local com suporte. O SMA geralmente é implantado junto com o Pacote do Microsoft Azure, pois este contém uma interface gráfica para gerenciamento de SMA. Ao contrário de automação do Azure, SMA requer uma instalação local que inclui Olá toohost de servidores da web API, runbooks de toocontain um banco de dados e configuração do SMA e trabalhos de runbook do Runbook Workers tooexecute. Automação do Azure fornece esses serviços na nuvem de saudação e requer apenas toomaintain Olá Hybrid Runbook Workers em seu ambiente local.

Se você for um usuário existente do SMA, você pode mover seu toobe de automação de tooAzure runbooks usado com Hybrid Runbook Worker sem alterações, supondo que eles executam seus próprios tooresources autenticação conforme descrito em [executar runbooks em um Runbook híbrido Trabalho](automation-hrw-run-runbooks.md).  Runbooks no SMA executadas no contexto de Olá Olá da conta de serviço no servidor de trabalho de saudação que pode fornecer a que a autenticação para Olá runbooks.

Você pode usar o hello toodetermine critérios a seguir se a automação do Azure com o operador de Runbook híbrido ou Service Management Automation é mais apropriada para suas necessidades.

* SMA requer uma instalação local de seus componentes subjacentes que estão conectados tooWindows pacote do Azure se uma interface gráfica de gerenciamento é necessária. Haverá necessidade de mais recursos locais, com custos mais altos de manutenção do que a Automação do Azure, que só precisa de um agente instalado nos trabalhos de runbook locais. agentes de saudação são gerenciados pelo Operations Management Suite, reduzindo os custos de manutenção.
* Automação do Azure armazena seus runbooks na nuvem hello e entrega local tooon Hybrid Runbook Workers. Se a sua política de segurança não permite esse comportamento, você deve usar o SMA.
* O SMA está incluído no System Center; logo, ele exige uma licença do System Center 2012 R2. A Automação do Azure se baseia em um modelo de assinatura em camadas.
* A Automação do Azure tem recursos avançados, tais como runbooks gráficos, que não estão disponíveis no SMA.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Instalando Olá Windows Hybrid Runbook Worker 

tooinstall e configurar um Hybrid Runbook Worker do Windows, há dois métodos disponíveis.  Olá recomendado método é usar uma automação de runbook toocompletely automatizar o processo de saudação necessário tooconfigure um computador com Windows.  Olá segundo método é após uma instalação de toomanually procedimento passo a passo e configurar a função hello.  

> [!NOTE]
> configuração de saudação toomanage dos seus servidores com suporte a função de operador de Runbook híbrido Olá com a configuração de estado desejado (DSC), você precisa tooadd-los como nós de DSC.  Para saber mais sobre a integração deles para gerenciamento com DSC, confira [Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure](automation-dsc-onboarding.md).           
><br>
>Se você habilitar Olá [solução de gerenciamento de atualizações](../operations-management-suite/oms-solution-update-management.md), qualquer computador com Windows conectado tooyour espaço de trabalho do OMS é configurado automaticamente com runbooks Hybrid Runbook Worker toosupport incluído nesta solução.  No entanto, ele não estará registrado com nenhum grupo Hybrid Worker que você já tenha definido em sua Conta de automação.  Olá computador pode ser adicionado grupo do Hybrid Runbook Worker tooa na sua conta de automação toosupport runbooks de automação enquanto você estiver usando Olá a mesma conta para solução de saudação e associação de grupo do Hybrid Runbook Worker.  Essa funcionalidade foi adicionada tooversion 7.2.12024.0 de saudação Hybrid Runbook Worker.  

Olá revisar informações sobre Olá a seguir [requisitos de hardware e software](automation-offering-get-started.md#hybrid-runbook-worker) e [informações para preparar a sua rede](automation-offering-get-started.md#network-planning) antes de você começar a implantar um Hybrid Runbook Worker.  Depois que você implantou com êxito um runbook worker, examinar [executar runbooks em um trabalho de Runbook híbrido](automation-hrw-run-runbooks.md) toolearn como tooconfigure tooautomate seus runbooks processa em seu datacenter local ou em outro ambiente de nuvem.  
 
### <a name="automated-deployment"></a>Implantação automatizada

Executar Olá seguinte as etapas de instalação de saudação do tooautomate e a configuração da função de operador de híbrido do Windows hello.  

1. Baixar Olá *New-OnPremiseHybridWorker.ps1* script hello [Galeria do PowerShell](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) diretamente do computador Olá executando a função de operador de Runbook híbrido hello ou de outro computador na sua ambiente e copie-o trabalho de toohello.  

    Olá *OnPremiseHybridWorker.ps1 novo* Olá parâmetros a seguir durante a execução do script requer:

  * *AutomationAccountName* (obrigatório) - nome de saudação da sua conta de automação.  
  * *ResourceGroupName* (obrigatório) - nome Olá Olá do grupo de recursos associado à sua conta de automação.  
  * *HybridGroupName* (obrigatório) - nome de saudação de um grupo de trabalho de Runbook híbrido que você especificar como um destino para runbooks Olá dando suporte a esse cenário. 
  *  *SubscriptionID* (obrigatório) - Olá Id de assinatura do Azure que sua conta de automação está em.
  *  *Nomedoespaçodetrabalho* (opcional) - Olá OMS nome do espaço de trabalho.  Se você não tiver um espaço de trabalho do OMS, o script hello cria e configura um.  

     > [!NOTE]
     > No momento Olá somente regiões de automação com suporte para a integração com o OMS são - **Sudeste da Austrália**, **Leste dos EUA 2**, **Sudeste da Ásia**, e **Oeste Europa**.  Se sua conta de automação não está em uma dessas regiões, script hello cria um espaço de trabalho do OMS, mas ela avisará que ela não é possível vinculá-los juntos.
     > 
2. Em seu computador, inicie **do Windows PowerShell** de saudação **iniciar** tela no modo de administrador.  
3. Olá shell de linha de comando do PowerShell, navegar toohello pasta, que contém o script hello baixado e executá-lo alterando valores hello parâmetros *- AutomationAccountName*, *- ResourceGroupName* , *- HybridGroupName*, *- SubscriptionId*, e *- WorkspaceName*.

     > [!NOTE] 
     > Você está tooauthenticate solicitado com o Azure depois de executar o script hello.  Você **deve** entrar com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. São solicitadas tooagree tooinstall **NuGet** e são solicitado tooauthenticate com suas credenciais do Azure.<br><br> ![Execução do script New-OnPremiseHybridWorker](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Após a conclusão do script hello, folha de grupos de trabalho híbrida Olá mostrará Olá novo grupo e o número de membros ou se um grupo existente, o número de saudação de membros é incrementado.  Você pode selecionar o grupo de saudação na lista Olá Olá **grupos de trabalho híbrida** folha e selecione Olá **Hybrid Workers** lado a lado.  Em Olá **Hybrid Workers** folha, verá que cada membro do grupo de saudação listado.  

### <a name="manual-deployment"></a>Implantação manual 
Executa Olá duas primeiras etapas de uma vez para o seu ambiente de automação e repita Olá restantes etapas para cada computador de trabalho.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Criar o espaço de trabalho do Operations Management Suite
Se você ainda não tiver um espaço de trabalho do Operations Management Suite, crie um usando as instruções em [Gerenciar seu espaço de trabalho](../log-analytics/log-analytics-manage-access.md). Você pode usar um espaço de trabalho existente se já tiver um.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. Adicionar a solução de automação tooOperations espaço de trabalho do pacote de gerenciamento
As soluções adicionam funcionalidade tooOperations Management Suite.  solução de automação de saudação adiciona a funcionalidade para automação do Azure incluindo suporte para operador de Runbook híbrido.  Quando você adicionar espaço de trabalho do hello solução tooyour, ele envia automaticamente trabalho componentes toohello computador do agente que você instalará na próxima etapa de saudação.

Siga as instruções de saudação em [tooadd uma solução usando a Galeria de soluções Olá](../log-analytics/log-analytics-add-solutions.md) tooadd Olá **automação** espaço de trabalho solução tooyour Operations Management Suite.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Instalar Olá Microsoft Monitoring Agent
Olá Microsoft Monitoring Agent se conecta computadores tooOperations Management Suite.  Quando você instala o agente de saudação em seu computador local e conecte-o espaço de trabalho tooyour, ele baixará automaticamente componentes de Olá necessários para o operador de Runbook híbrido.

Siga as instruções de saudação em [Windows conectar computadores tooLog análise](../log-analytics/log-analytics-windows-agents.md) agente de saudação tooinstall no computador do local de saudação.  Você pode repetir esse processo para tooadd de vários computadores tooyour ambiente com vários operadores.

Quando o agente Olá se conectou com êxito tooOperations Management Suite, ele será listado em Olá **fontes conectadas** guia da saudação Operations Management Suite **configurações** painel.  Você pode verificar que o agente Olá baixou solução de automação de saudação corretamente quando ele tem uma pasta chamada **AzureAutomationFiles** em C:\Program Files\Microsoft monitoramento Agent\Agent.  tooconfirm Olá versão Olá Hybrid Runbook Worker, você pode navegar Olá de monitoramento Agent\Agent\AzureAutomation\ e observe tooC:\Program Files\Microsoft \\ *versão* subpasta.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Instalar o ambiente de runbook hello e conecte-se tooAzure automação
Quando você adicionar um agente tooOperations Management Suite, Olá solução de automação envia Olá **HybridRegistration** módulo do PowerShell, que contém a saudação **Add-HybridRunbookWorker** cmdlet.  Usar este ambiente de runbook cmdlet tooinstall Olá Olá computador e registrá-lo na automação do Azure.

Abra uma sessão do PowerShell no modo de administrador e execute Olá módulo de saudação tooimport comandos a seguir.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

Em seguida, execute Olá **Add-HybridRunbookWorker** cmdlet usando Olá sintaxe a seguir:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Você pode obter informações de saudação necessárias para este cmdlet do hello **gerenciar chaves** folha em Olá portal do Azure.  Abra esta folha selecionando Olá **chaves** opção de saudação **configurações** folha em sua conta de automação.

![Visão geral do Runbook Worker Híbrido](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** é Olá nome de grupo do Hybrid Runbook Worker do hello. Se esse grupo já existe na conta de automação Olá, o computador atual Olá é adicionado tooit.  Se ele não existir, será adicionado.
* **Ponto de extremidade** é hello **URL** campo Olá **gerenciar chaves** folha.
* **Token** é hello **chave de acesso primária** em Olá **gerenciar chaves** folha.  

Saudação de uso **-Verbose** alternar com **Add-HybridRunbookWorker** tooreceive informações detalhadas sobre instalação hello.

#### <a name="5-install-powershell-modules"></a>5. Instalar módulos do PowerShell
Runbooks pode usar qualquer uma das atividades de saudação e cmdlets definidos em módulos Olá instalados em seu ambiente de automação do Azure.  Esses módulos não são computadores locais tooon automaticamente implantado, você deve instalá-los manualmente.  exceção de saudação é hello módulo do Azure, que é instalado por padrão, fornecendo acesso toocmdlets para todos os serviços do Azure e as atividades de automação do Azure.

Como objetivo principal de saudação do recurso do Hybrid Runbook Worker Olá recursos locais toomanage, você provavelmente precisa módulos de saudação tooinstall que dão suporte a esses recursos.  Você pode consultar muito[instalar módulos](http://msdn.microsoft.com/library/dd878350.aspx) para obter informações sobre como instalar os módulos do Windows PowerShell.  Módulos instalados devem estar em um local referenciado pela variável de ambiente PSModulePath, para que eles são importados automaticamente pelo trabalhador híbrido de saudação.  Para obter mais informações, consulte [Olá modificando o caminho de instalação PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx). 

## <a name="removing-hybrid-runbook-worker"></a>Removendo o Hybrid Runbook Worker 
Você pode remover um ou mais trabalhadores de Runbook híbrido de um grupo ou você pode remover o grupo de hello, dependendo dos seus requisitos.  tooremove um Hybrid Runbook Worker em um computador local, execute Olá etapas a seguir.

1. No portal do Azure de Olá, navegue tooyour conta de automação.  
2. De saudação **configurações** folha, selecione **chaves** e observe os valores de saudação para o campo **URL** e **chave de acesso primário**.  Você precisará dessas informações para a próxima etapa de saudação.
3. Abra uma sessão do PowerShell no modo de administrador e execute a seguinte Olá command - `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`.  Saudação de uso **-Verbose** alternar para um log detalhado do processo de remoção de saudação.

> [!NOTE]
> Isso não remove o hello Microsoft Monitoring Agent computador hello, apenas a funcionalidade de saudação e a configuração da função de operador de Runbook híbrido hello.  

## <a name="remove-hybrid-worker-groups"></a>Remover grupos do Hybrid Worker
tooremove um grupo, você primeiro precisa tooremove Olá Hybrid Runbook Worker de cada computador que seja membro do grupo de saudação usando Olá procedimento mostrado anteriormente e, em seguida, você pode executar Olá grupo de saudação do tooremove as etapas a seguir.  

1. Abra conta de automação Olá no hello portal do Azure.
2. Selecione Olá **híbrida grupos de trabalho** lado a lado e em Olá **híbrida grupos de trabalho** folha, grupo de saudação selecione desejar toodelete.  Depois de selecionar um grupo específico de hello, Olá **grupo do Hybrid worker** folha de propriedades é exibida.<br> ![Folha do grupo Hybrid Runbook Worker](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Na folha de propriedades de saudação para o grupo selecionado de saudação, clique em **excluir**.  Será exibida uma mensagem perguntando você tooconfirm esta ação, selecione **Sim** se tiver certeza de que deseja tooproceed.<br> ![Caixa de diálogo de confirmação de exclusão de grupo](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> Esse processo pode levar vários segundos toocomplete e você pode acompanhar seu progresso em **notificações** menu hello.  

## <a name="troubleshooting"></a>Solucionar problemas 
Olá Hybrid Runbook Worker depende Olá toocommunicate Microsoft Monitoring Agent com o trabalho de saudação automação conta tooregister, recebe trabalhos de runbook e status do relatório. Se o registro do trabalhador Olá falhar, aqui estão algumas das possíveis causas para o erro hello:  

1. hybrid worker de saudação estiver atrás de um proxy ou firewall.  
    Verifique se Olá tem too*.azure-automation.net de acesso de saída na porta 443.  

2. Olá hybrid worker de saudação do computador está em execução no possui menos que o hardware mínimo Olá [requisitos](automation-offering-get-started.md#hybrid-runbook-worker).  
    Computadores que executam o hello Hybrid Runbook Worker devem atender Olá requisitos mínimos de hardware antes de designar a ele toohost esse recurso. Caso contrário, dependendo da utilização de recursos de saudação de outros processos em segundo plano e a contenção provocada por runbooks durante a execução, o computador de hello serão fiquem sobrecarregados e causar tempos limites ou atrasos de trabalho de runbook.
   Verifique computador Olá designado de recurso de Hybrid Runbook Worker Olá toorun atende aos requisitos mínimos de hardware de saudação.  Se isso acontecer, monitore toodetermine de utilização de CPU e memória correlação entre desempenho de saudação de processos de trabalho de Runbook híbrido e Windows.  Se não houver memória ou a pressão da CPU, isso pode indicar Olá necessidade tooupgrade ou adicione mais processadores ou aumento de memória tooaddress Olá afunilamento de recurso e resolver o erro de saudação. Como alternativa, selecione um recurso de computação diferentes que pode dar suporte aos requisitos mínimos de hello e escala quando a carga de trabalho indica que um aumento é necessário.
    
3. Olá serviço Microsoft Monitoring Agent não está em execução.  
    Se Olá serviço do Microsoft Windows de agente de monitoramento não está em execução, isso impede Olá Hybrid Runbook Worker de se comunicar com a automação do Azure.  Verifique se está executando agente Olá inserindo Olá comando do PowerShell a seguir: `get-service healthservice`.  Se Olá serviço for interrompido, digite Olá comando no serviço de saudação toostart PowerShell a seguir: `start-service healthservice`.  

4. Em hello **aplicativo e o Gerenciador de serviços de Logs\Operations** log de eventos, consulte o evento 4502 e EventMessage contendo **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**com hello descrição a seguir: *certificado Olá apresentado pelo serviço Olá <wsid>. oms.opinsights.azure.com não foi emitido por uma autoridade de certificação usada para serviços da Microsoft. Entre em contato com seu toosee do administrador de rede se eles estiverem executando um proxy que intercepta comunicação TLS/SSL. artigo Olá KB3126513 tem informações adicionais de solução de problemas para problemas de conectividade.*
    Isso pode ser causado por seu proxy ou rede firewall blockking comunicação tooMicrosoft do Azure.  Verifique se Olá tem acesso de saída too*.azure-automation.net nas portas 443.

Os logs são armazenados localmente em cada hybrid worker, em C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Você pode verificar se há qualquer aviso ou eventos de erro gravados toohello **aplicativos e serviços Logs\Microsoft-SMA\Operations** e **aplicativo e o Gerenciador de serviços de Logs\Operations** log de eventos indica uma conectividade ou outros problemas que afetam a integração de saudação função tooAzure automação ou problema ao executar operações normais.  

## <a name="next-steps"></a>Próximas etapas
Revisão [executar runbooks em um trabalho de Runbook híbrido](automation-hrw-run-runbooks.md) toolearn como tooconfigure tooautomate seus runbooks processa em seu datacenter local ou em outro ambiente de nuvem.
