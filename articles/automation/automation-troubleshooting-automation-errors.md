---
title: "aaaTroubleshooting problemas comuns automação do Azure | Microsoft Docs"
description: "Este artigo fornece informações toohelp solucionar e corrigir erros comuns de automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "erro de automação, solução de problemas, problema"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Solução de problemas comuns na Automação do Azure 
Este artigo fornece ajuda para solucionar problemas de erros comuns podem ser encontrados na automação do Azure e sugere soluções possíveis tooresolve-los.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Erros de autenticação ao trabalhar com runbooks da Automação do Azure
### <a name="scenario-sign-in-tooazure-account-failed"></a>Cenário: Falha na conta entrar tooAzure
**Erro:** erro hello "Unknown_user_type: tipo desconhecido de usuário" ao trabalhar com os cmdlets Add-AzureAccount ou AzureRmAccount de logon do hello.

**Motivo do erro Olá:** esse erro ocorrerá se o nome do ativo de credencial de saudação não é válido ou se hello nome de usuário e senha que você usou o ativo de credencial de automação de saudação toosetup não são válidos.

**Dicas de solução de problemas:** em ordem toodetermine o que há de errado, levar Olá etapas a seguir:  

1. Certifique-se de que você não tem caracteres especiais, incluindo Olá  **@**  caractere no nome de ativo Olá automação credencial que você está usando tooconnect tooAzure.  
2. Verifique que você pode usar a saudação de nome de usuário e senha que são armazenadas na credencial de automação do Azure Olá em seu editor de ISE do PowerShell local. Você pode fazer isso executando Olá Olá ISE do PowerShell cmdlets a seguir:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Se a autenticação falhar localmente, isso indicará que você não configurou corretamente as credenciais do Active Directory do Azure. Consulte também[autenticação tooAzure usando o Azure Active Directory](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) conta blog post tooget hello Azure Active Directory configurada corretamente.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Cenário: Saudação não é possível toofind assinatura do Azure
**Erro:** erro hello "hello assinatura chamada ``<subscription name>`` não pode ser encontrado" ao trabalhar com os cmdlets do Select-AzureSubscription ou selecione AzureRmSubscription hello.

**Motivo do erro Olá:** este erro ocorre se o nome da assinatura Olá não é válido ou se o usuário do Active Directory do Azure Olá que está tentando detalhes da assinatura Olá tooget não está configurado como um administrador de assinatura de saudação.

**Dicas de solução de problemas:** em ordem toodetermine se corretamente autenticado tooAzure e ter acesso toohello assinatura tentar tooselect, levar Olá etapas a seguir:  

1. Certifique-se de que você execute Olá **Add-AzureAccount** antes de executar Olá **Select-AzureSubscription** cmdlet.  
2. Se você vir essa mensagem de erro, modifique o código adicionando Olá **Get-AzureSubscription** cmdlet a seguir Olá **Add-AzureAccount** cmdlet e, em seguida, execute o código de saudação.  Agora, verifique se a saída de saudação do Get-AzureSubscription contém detalhes da sua assinatura.  

   * Se você não vir quaisquer detalhes de assinatura na saída de hello, isso significa que assinatura Olá não inicializada ainda.  
   * Se você vir os detalhes da assinatura Olá na saída de hello, confirme que você está usando Olá assinatura correta nome ou ID com hello **Select-AzureSubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Cenário: Autenticação tooAzure falhou porque a autenticação multifator é habilitada
**Erro:** erro hello "Add-AzureAccount: AADSTS50079: registro de autenticação forte (prova-up) é necessário" ao autenticar tooAzure com seu nome de usuário do Azure e a senha.

**Motivo do erro Olá:** se você tiver a autenticação multifator em sua conta do Azure, você não pode usar um tooAzure de tooauthenticate de usuário do Active Directory do Azure.  Em vez disso, você precisa toouse um certificado ou uma tooAzure tooauthenticate principal de serviço.

**Dicas de solução de problemas:** toouse um certificado com hello cmdlets de gerenciamento de serviços do Azure, consulte muito[criando e adicionando toomanage um certificado do Azure services.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse uma entidade de serviço com os cmdlets do Gerenciador de recursos do Azure, consulte muito[criação de serviço principal usando o portal do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) e [autenticar uma entidade de serviço com o Gerenciador de recursos do Azure.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Erros comuns ao trabalhar com runbooks
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Cenário: início do trabalho de runbook Olá foi tentado três vezes, mas houve uma falha toostart cada vez
**Erro:** seu runbook falha com erro hello "" trabalho Olá houve tentativa de três vezes, mas falhou."

**Motivo do erro Olá:** esse erro pode ser causado por Olá motivos a seguir:  

1. Limite de Memória.  Documentamos limites na quantidade de memória alocada tooa área restrita [limites de serviço de automação](../azure-subscription-service-limits.md#automation-limits) para um trabalho pode falhar se estiver usando mais de 400 MB de memória. 

2. Módulo Incompatível.  Isso poderá ocorrer se as dependências do módulo não estiverem corretas, caso em que seu runbook normalmente retornará uma mensagem de “Comando não encontrado” ou “Não é possível associar o parâmetro”. 

**Dicas de solução de problemas:** qualquer Olá soluções a seguir corrigirá o problema de saudação:  

* Métodos sugeridos toowork dentro do limite de memória de saudação são toosplit cargas de trabalho de saudação entre vários runbooks, não processar todos os dados na memória, toowrite a saída desnecessária de seus runbooks ou considere quantos pontos de verificação de gravação para o PowerShell runbooks do fluxo de trabalho.  

* Você precisa tooupdate seus módulos do Azure seguindo as etapas de saudação [como módulos do PowerShell do Azure tooupdate na automação do Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Cenário: O Runbook falha devido a objeto desserializado
**Erro:** seu runbook falha com erro hello "não é possível associar o parâmetro ``<ParameterName>``. Não é possível converter Olá ``<ParameterType>`` o valor do tipo Deserialized ``<ParameterType>`` tootype ``<ParameterType>``".

**Motivo do erro Olá:** se seu runbook for um fluxo de trabalho do PowerShell, ele armazena objetos complexos em um formato desserializado em ordem toopersist seu estado de runbook se o fluxo de trabalho de saudação é suspenso.  

**Dicas de solução de problemas:**  
Qualquer Olá três soluções a seguir corrigirá esse problema:

1. Se estiver direcionando objetos complexos de tooanother de um cmdlet, encapsule esses cmdlets em um InlineScript.  
2. Passe Olá nome ou um valor que você precisa do objeto complexo de saudação em vez de passar o objeto inteiro hello.  
3. Use um runbook do PowerShell em vez de um runbook de Fluxo de Trabalho do PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Cenário: O trabalho de Runbook falhou porque Olá alocada cota excedida
**Erro:** seu trabalho de runbook falha com erro de hello "hello cota para Olá mensal total do trabalho tempo de execução para esta assinatura foi atingida".

**Motivo do erro Olá:** esse erro ocorre quando hello a execução de trabalhos excede a cota de livre de 500 minutos Olá para sua conta. Essa cota se aplica a tipos de tooall de tarefas de execução de trabalho como um trabalho de teste, iniciando um trabalho do portal hello, executando um trabalho usando webhooks e agendar um trabalho tooexecute usando o portal do Azure hello, ou em seu data center. toolearn mais sobre preços de automação, consulte [preços de automação](https://azure.microsoft.com/pricing/details/automation/).

**Dicas de solução de problemas:** se você quiser toouse mais de 500 minutos de processamento por mês, você precisará toochange sua assinatura de nível básico do toohello Olá camada gratuita. Você pode atualizar a camada básica toohello por Olá colocar as etapas a seguir:  

1. Entrar tooyour assinatura do Azure  
2. Selecionar conta de automação Olá que desejar tooupgrade  
3. Clique em **Configurações** > **Tipo de preço e Uso** > **Tipo de preço**  
4. Em Olá **Escolher tipo de preços** folha, selecione **básica**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Cenário: cmdlet não reconhecido ao se executar um runbook
**Erro:** o trabalho de runbook falha com erro hello "``<cmdlet name>``: termo Olá ``<cmdlet name>`` não é reconhecido como nome de saudação de um cmdlet, função, arquivo de script ou programa operável."

**Motivo do erro Olá:** esse erro é causado quando o mecanismo do PowerShell Olá não é possível encontrar o cmdlet Olá que você está usando em seu runbook.  Isso pode ser porque o módulo Olá contendo Olá cmdlet está ausente na conta hello, há um conflito de nome com um nome de runbook, ou Olá cmdlet também existe em outro módulo e automação não é possível resolver o nome da saudação.

**Dicas de solução de problemas:** qualquer Olá soluções a seguir corrigirá o problema de saudação:  

* Verifique se você inseriu o nome de cmdlet Olá corretamente.  
* Certifique-se de cmdlet Olá existe em sua conta de automação e que não haja nenhum conflito. tooverify se Olá cmdlet estiver presente, abra um runbook no modo de edição e procure Olá cmdlet deseja toofind na biblioteca de saudação ou executar **Get-Command ``<CommandName>``** .  Após validar esse cmdlet Olá conta toohello disponíveis, e que não haja nenhum conflito de nome com outros cmdlets ou runbooks, adicioná-lo a tela de toohello e certifique-se de que você está usando um parâmetro inválido definido em seu runbook.  
* Se você tem um conflito de nome e Olá cmdlet está disponível em dois módulos diferentes, você pode resolver isso usando o nome totalmente qualificado Olá Olá cmdlet. Por exemplo, você pode usar **NomeDoMódulo\NomeDoCmdlet**.  
* Se você Olá runbook local está em execução em um grupo do hybrid worker, certifique-se de que Olá cmdlet do módulo é instalado na máquina de saudação que hospeda o trabalho de híbrida hello.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Cenário: Um runbook em tempo de execução consistentemente falhará com a exceção de saudação: "trabalho Olá não pode continuar em execução porque ele foi removido repetidamente a partir Olá mesmo ponto de verificação".
**Motivo do erro Olá:** esse é o comportamento do projeto devido toohello "Compartilhamento justo" monitoramento de processos de automação do Azure, que suspende automaticamente um runbook se ela é executada mais de 3 horas. Olá no entanto, a mensagem de erro retornada não oferece "quais próximo" opções. Um runbook pode ser suspenso por vários motivos. Suspende a acontecer principalmente tooerrors vencimento. Por exemplo, uma exceção não tratada em um runbook, uma falha de rede ou uma falha em Olá Runbook Worker executando o runbook hello, serão todas causar Olá toobe de runbook suspenso e iniciar a partir de seu último ponto de verificação quando retomado.

**Dicas de solução de problemas:** Olá documentado tooavoid solução desse problema é toouse pontos de verificação em um fluxo de trabalho.  toolearn mais consulte muito[fluxos de trabalho do aprendizado PowerShell](automation-powershell-workflow.md#checkpoints).  Veja uma explicação mais detalhada sobre a “Fração Justa” e sobre o Ponto de Verificação neste artigo de blog: [Uso de Pontos de Verificação em Runbooks](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Erros comuns durante a importação de módulos
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Cenário: O módulo não tooimport ou cmdlets não pode ser executados após a importação
**Erro:** um módulo falha tooimport ou importa com êxito, mas nenhum cmdlets são extraídos.

**Motivo do erro Olá:** algumas razões que um módulo não pode importar com êxito tooAzure automação são:  

* estrutura Olá não coincide com a estrutura de saudação que automação precisa toobe no.  
* módulo de saudação é dependente de outro módulo que não tenha sido implantado tooyour conta de automação.  
* módulo Olá tem suas dependências na pasta hello.  
* Olá **AzureRmAutomationModule novo** cmdlet está sendo módulo de saudação tooupload usado, e você não forneceu o caminho de armazenamento total de saudação ou não carregou o módulo de saudação usando uma URL publicamente acessível.  

**Dicas de solução de problemas:**  
Qualquer Olá soluções a seguir corrigirá o problema de saudação:  

* Certifique-se de que o módulo Olá segue Olá formato a seguir:  
  NomeMódulo.Zip **->** NomeMódulo ou Número de Versão **->** (NomeMódulo.psm1, NomeMódulo.psd1)
* Abra o arquivo. psd1 de saudação e veja se o módulo de saudação tem todas as dependências.  Em caso afirmativo, carregar toohello esses módulos conta de automação.  
* Certifique-se de que qualquer DLLs referenciados estão presentes na pasta de módulo hello.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Erros comuns ao trabalhar com DSC (Configuração de estado desejado)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Cenário: o nó está com um status de falha e um erro "Não encontrado"
**Erro:** nó Olá tem um relatório com **falha** status e que contém o erro hello "hello tentativa tooget Olá ação do servidor https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction falhou porque uma configuração válida ``<guid>`` não pode ser encontrado. "

**Motivo do erro Olá:** esse erro normalmente ocorre quando hello nó recebe o nome da configuração tooa (por exemplo, ABC) em vez de um nome de configuração de nó (por exemplo, ABC. Servidor Web).  

**Dicas de solução de problemas:**  

* Certifique-se de que você está atribuindo o nó Olá com "nome de configuração do nó" e não hello "nome de configuração".  
* Você pode atribuir uma configuração tooa nós usando o portal do Azure ou com um cmdlet do PowerShell.

  * Em ordem tooassign um nó de tooa de configuração do nó usando o portal do Azure, abra Olá **nós DSC** folha, em seguida, selecione um nó e clique em **configuração de nó de atribuir** botão.  
  * Em ordem tooassign um nó de tooa de configuração do nó usando o cmdlet do PowerShell, use **AzureRmAutomationDscNode conjunto** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Cenário: nenhuma configuração de nó (arquivos MOF) foi produzida quando uma compilação foi compilada
**Erro:** suspende o trabalho de compilação DSC com o erro Olá: "compilação concluída com êxito, mas nenhuma configuração de nó. MOFs gerados".

**Motivo do erro Olá:** hello quando a expressão a seguir Olá **nó** palavra-chave na configuração de saudação DSC avalia muito$ null e nenhuma configuração de nó será produzida.    

**Dicas de solução de problemas:**  
Qualquer Olá soluções a seguir corrigirá o problema de saudação:  

* Certifique-se de que toohello próximo de expressão Olá **nó** palavra-chave na definição de configuração de saudação não está avaliando muito null$.  
* Se você estiver passando ConfigurationData ao compilar a configuração de saudação, certifique-se de que você está passando valores esperados de saudação requer que a configuração saudação do [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Cenário: Olá relatório do nó DSC fica parado estado "em andamento"
**Erro:** o Agente DSC gera "Nenhuma instância encontrada com os valores de propriedade especificados".

**Motivo do erro Olá:** atualizar sua versão do WMF e ter corrompido WMI.  

**Dicas de solução de problemas:** siga instruções Olá Olá [limitações e problemas conhecidos do DSC](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix problema de saudação.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Cenário: Não é possível toouse uma credencial em uma configuração de DSC
**Erro:** o trabalho de compilação DSC foi suspenso com o erro Olá: "Erro System. InvalidOperationException propriedade credencial do tipo de processamento ``<some resource name>``: convertendo e armazenar uma senha criptografada como texto sem formatação é permitido somente se PSDscAllowPlainTextPassword é definido tootrue".

**Motivo do erro Olá:** você usou uma credencial em uma configuração, mas não adequada **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada nó configuração.  

**Dicas de solução de problemas:**  

* Fazer toopass-se em Olá adequada **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue para cada configuração de nó mencionada na configuração de saudação. Para obter mais informações, consulte muito[ativos no DSC de automação do Azure](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Próximas etapas
Se você seguiu Olá acima de etapas de solução de problemas e não é possível encontrar a resposta Olá, você pode revisar as opções adicionais de suporte de saudação abaixo.

* Obter ajuda de especialistas do Azure. Envie seu problema toohello [fóruns MSDN Azure ou estouro de pilha.](https://azure.microsoft.com/support/forums/).
* Registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **obter suporte** em **técnicas e suporte de cobrança**.
* Publique uma Solicitação de Script no [Script Center](https://azure.microsoft.com/documentation/scripts/) se estiver procurando uma solução de runbook ou um módulo de integração da Automação do Azure.
* Poste comentários ou solicitações de recursos para a Automação do Azure no [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
