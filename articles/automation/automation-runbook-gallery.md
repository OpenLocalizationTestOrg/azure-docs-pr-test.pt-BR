---
title: "galerias aaaRunbook e módulo de automação do Azure | Microsoft Docs"
description: "Runbooks e módulos da comunidade Microsoft e hello estão disponíveis para você tooinstall e usam em seu ambiente de automação do Azure.  Este artigo descreve como você pode acessar esses recursos e toocontribute Galeria toohello runbooks."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Galerias de runbook e de módulos para a Automação do Azure
Em vez de criar seus próprios runbooks e módulos na automação do Azure, você pode acessar uma variedade de cenários que já foram criados pela Microsoft e hello comunidade.  É possível usar esses cenários sem modificação ou usá-los como um ponto de partida e editá-los para seus requisitos específicos.

Você pode obter runbooks da saudação [Galeria de Runbook](#runbooks-in-runbook-gallery) e módulos de saudação [Galeria do PowerShell](#modules-in-powerShell-gallery).  Você também pode contribuir toohello comunidade compartilhando cenários em que você desenvolve.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks na Galeria de Runbook
Olá [Galeria de Runbook](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) fornece diversos runbooks da comunidade Microsoft e hello que você pode importar para automação do Azure. Você pode baixar um runbook da Galeria de saudação que está hospedada no hello [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), ou você pode diretamente importar runbooks da Galeria de Olá Olá portal clássico do Azure ou no portal do Azure.

Você só pode importar diretamente da Galeria de Runbook hello usando Olá portal clássico do Azure ou o portal do Azure. Não é possível executar essa função usando o Windows PowerShell.

> [!NOTE]
> Você deve validar o conteúdo de saudação de todos os runbooks que você recebe do hello Galeria de runbooks e ter muito cuidado na instalação e executá-los em um ambiente de produção. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport um runbook de saudação Galeria de runbooks com hello portal clássico do Azure
1. Em Olá Portal do Azure, clique em, **novo**, **serviços de aplicativos**, **automação**, **Runbook**, **da galeria**.
2. Selecione uma categoria tooview relacionadas a runbooks e selecione um runbook tooview seus detalhes. Quando você seleciona Olá runbook desejado, clique botão de seta para a direita hello.
   
    ![Galeria de Runbook](media/automation-runbook-gallery/runbook-gallery.png)
3. Examine o conteúdo de saudação do hello runbook e observe quaisquer requisitos na descrição de saudação. Quando terminar, clique botão de seta para a direita hello.
4. Insira detalhes de runbook de hello e, em seguida, clique o botão de marca de saudação. nome do runbook Olá já será preenchido.
5. Olá runbook será exibido no hello **Runbooks** guia Olá conta de automação.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport um runbook de saudação Galeria de runbooks com hello portal do Azure
1. No Portal do Azure do hello, abra sua conta de automação.
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.
3. Clique no botão **Procurar na galeria** .
   
    ![Botão Procurar na galeria](media/automation-runbook-gallery/browse-gallery-button.png)
4. Localize o item da Galeria Olá desejado e selecione-tooview seus detalhes.
   
    ![Procurar na galeria](media/automation-runbook-gallery/browse-gallery.png)
5. Clique em **projeto do modo de exibição fonte** tooview item Olá Olá [TechNet Script Center](http://gallery.technet.microsoft.com/).
6. tooimport um item, clique nele tooview seus detalhes e, em seguida, clique em Olá **importação** botão.
   
    ![Botão Importar](media/automation-runbook-gallery/gallery-item-detail.png)
7. Opcionalmente, alterar nome de saudação do hello runbook e, em seguida, clique em **Okey** tooimport Olá runbook.
8. Olá runbook será exibido no hello **Runbooks** guia Olá conta de automação.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Adicionar uma galeria de runbook do runbook toohello
A Microsoft incentiva tooadd runbooks toohello Galeria de runbooks que você acha que seriam úteis tooother clientes.  Você pode adicionar um runbook por [carregá-lo toohello Script Center](http://gallery.technet.microsoft.com/site/upload) considerando Olá conta detalhes a seguir.

* Você deve especificar *do Windows Azure* para Olá **categoria** e *automação* para Olá **subcategoria** para Olá runbook toobe exibido no Assistente de saudação.  
* carregamento de saudação deve ser um único arquivo. ps1 ou. graphrunbook.  Se o runbook Olá requer quaisquer módulos, runbooks filho ou ativos, você deve listar aqueles na descrição de saudação do envio de saudação e na seção de comentários de saudação do runbook hello.  Se você tiver um cenário que exigem vários runbooks, carregue cada uma separadamente e nomes de saudação da lista de saudação relacionadas a runbooks em cada uma das suas descrições. Certifique-se de que você use Olá mesmo marcas para que elas apareçam no hello mesma categoria. Um usuário terá tooread Olá descrição tooknow outros runbooks são necessários Olá cenário toowork.
* Adicionar marca hello "GraphicalPS" Se você estiver publicando um **runbook gráfico** (não um fluxo de trabalho gráfico). 
* Inserir o trecho de código a um fluxo de trabalho do PowerShell ou do PowerShell em Olá descrição usando **Inserir seção de código** ícone.
* Olá resumo de carregamento de saudação será exibido no hello que Galeria de Runbook resultados para que você deve fornecer informações detalhadas que ajudam um usuário a identificar a funcionalidade de saudação do runbook hello.
* Você deve atribuir um toothree de saudação após o carregamento de toohello de marcas.  Olá runbook será listado no Assistente de saudação em categorias de saudação que corresponderem às suas marcas.  Marcas não incluídos nesta lista serão ignoradas pelo Assistente de saudação. Se você não especificar marcas correspondentes, Olá runbook será listado em Olá outra categoria.
  
  * Backup
  * Gerenciamento de Capacidade
  * Controle de Alterações
  * Conformidade
  * Ambientes de Desenvolvimento/Teste
  * Recuperação de desastre
  * Monitoramento
  * Aplicação de patch
  * Provisionamento
  * Correção
  * Gerenciamento do ciclo de vida de VMs
* A automação atualiza Olá galeria uma vez por hora, portanto você não verá suas contribuições imediatamente.

## <a name="modules-in-powershell-gallery"></a>Módulos na Galeria do PowerShell
Módulos do PowerShell contêm cmdlets que você pode usar em seus runbooks e módulos existentes que você pode instalar na automação do Azure estão disponíveis no hello [Galeria do PowerShell](http://www.powershellgallery.com).  Você pode iniciar esta galeria da saudação portal do Azure e instalá-los diretamente na automação do Azure, ou você pode baixá-los e instalá-los manualmente.  Você não poderá instalar módulos Olá diretamente Olá portal clássico do Azure, mas você pode baixá-los instalá-los como faria com qualquer outro módulo.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport um módulo da saudação Galeria de módulo de automação com hello portal do Azure
1. No Portal do Azure do hello, abra sua conta de automação.
2. Clique em Olá **ativos** bloco tooopen Olá lista de ativos.
3. Clique em Olá **módulos** bloco tooopen Olá lista de módulos.
4. Clique em Olá **procurar galeria** botão e hello blade de galeria de navegação é iniciado.
   
    ![Galeria de módulos](media/automation-runbook-gallery/modules-blade.png) <br>
5. Depois que você tiver iniciado blade de navegação da Galeria hello, você pode pesquisar por Olá campos a seguir:
   
   * Nome do Módulo
   * Marcas
   * Autor
   * Nome do recurso do DSC/cmdlet
6. Localizar um módulo que você está interessado e selecioná-lo tooview seus detalhes.  
   Quando você analisar um módulo específico, você pode exibir mais informações sobre o módulo hello, incluindo um toohello voltar do link Galeria do PowerShell, as dependências de necessárias, e todos os cmdlets de saudação e/ou recursos de DSC que Olá módulo contém.
   
    ![Detalhes do módulo do PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. módulo de saudação tooinstall diretamente para a automação do Azure, clique em Olá **importação** botão.
   
    ![Botão Importar módulo](media/automation-runbook-gallery/module-import-button.png)
8. Quando você clica em um botão de importar Olá, você verá o nome do módulo Olá que você está prestes a tooimport. Se todas as dependências de saudação estiverem instaladas, Olá **Okey** botão estará ativo. Se você não tem dependências, você precisa tooimport aqueles antes de poder importar este módulo.
9. Clique em **Okey** tooimport Olá módulo e folha de módulo Olá serão iniciado. Quando a automação do Azure importa uma conta de tooyour do módulo, ele extrai metadados sobre o módulo de saudação e Olá cmdlets.
   
    ![Folha Importar módulo](media/automation-runbook-gallery/module-import-blade.png)
   
    Isso pode levar alguns minutos, desde que cada atividade precisa toobe extraído.
10. Você receberá uma notificação de que o módulo hello está sendo implantado e uma notificação quando ele for concluído.
11. Depois Olá módulo é importado, você verá atividades disponíveis Olá, e você pode usar seus recursos em seus runbooks e a configuração de estado desejado.

## <a name="requesting-a-runbook-or-module"></a>Solicitando um runbook ou um módulo
Você pode enviar solicitações muito[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Se precisar de ajuda para gravar um runbook ou tiver uma pergunta sobre o PowerShell, poste uma pergunta tooour [fórum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks, consulte [criando ou importando um runbook na automação do Azure](automation-creating-importing-runbook.md)
* diferenças de saudação toounderstand entre o fluxo de trabalho do PowerShell e PowerShell com runbooks, consulte [fluxo de trabalho do PowerShell de aprendizado](automation-powershell-workflow.md)

