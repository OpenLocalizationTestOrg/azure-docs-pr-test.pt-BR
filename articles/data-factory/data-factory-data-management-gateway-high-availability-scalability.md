---
title: disponibilidade de aaaHigh com o gateway de gerenciamento de dados no Azure Data Factory | Microsoft Docs
description: "Este artigo explica como você pode escalar horizontalmente um Gateway de Gerenciamento de Dados adicionando mais nós e escalar verticalmente com o aumento do número de trabalhos simultâneos que podem ser executados em um nó."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Gateway de Gerenciamento de Dados – alta disponibilidade e escalabilidade (versão prévia)
Este artigo lhe ajudará a configurar a solução de alta disponibilidade e escalabilidade com o Gateway de Gerenciamento de Dados.    

> [!NOTE]
> Este artigo pressupõe que você já esteja familiarizado com conceitos básicos do Gateway de Gerenciamento de Dados. Se você não estiver, consulte [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).

>**Esse recurso em versão prévia é oficialmente compatível com o Gateway de Gerenciamento de Dados versão 2.12.xxxx.x e superior**. Verifique se você está usando a versão 2.12.xxxx.x ou superior. Baixar a versão mais recente saudação do Gateway de gerenciamento de dados [aqui](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Visão geral
Você pode associar gateways de gerenciamento de dados que são instalados em vários computadores de locais com um único gateway lógico do portal de saudação. Esses computadores são chamados de **nós**. Você pode ter até muito**quatro nós** associados com um gateway lógico. Olá benefícios de ter vários nós (máquinas locais com o gateway instalado) para um gateway lógico são:  

- Melhorar o desempenho de movimentação de dados entre armazenamentos de dados local e na nuvem.  
- Se um de nós de saudação falhar por algum motivo, outros nós ainda estão disponíveis para mover dados de saudação. 
- Se um de nós de saudação precisar toobe colocado offline para manutenção, outros nós ainda estão disponíveis para mover dados de saudação.

Você também pode configurar o número de saudação do **trabalhos de movimentação de dados simultâneas** que pode ser executado em um tooscale de nó, o recurso de saudação de mover dados entre locais e na nuvem armazenamentos de dados. 

Usando Olá portal do Azure, você pode monitorar o status de saudação de nós, que ajuda você a decidir se tooadd ou remover um nó de gateway de lógica de saudação. 

## <a name="architecture"></a>Arquitetura 
Hello diagrama a seguir fornece visão geral da arquitetura de saudação de escalabilidade e o recurso de disponibilidade do hello Data Management Gateway: 

![Gateway de Gerenciamento de Dados – alta disponibilidade e escalabilidade](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

Um **gateway lógica** gateway Olá suplemento fábrica de dados tooa Olá portal do Azure. Anteriormente, você podia associar apenas um computador do Windows local com instalado com o Gateway de Gerenciamento de Dados instalado com um gateway de lógico. Esse computador de gateway local é chamado de nó. Agora, você pode associar o muito**quatro nós físicos** com um gateway lógico. Um gateway lógico com vários nós é chamado de **gateway com vários nós**.  

Todos esses nós estão **ativos**. Todos eles podem processar dados de toomove de trabalhos de movimentação de dados entre locais e na nuvem armazenamentos de dados. Um de nós de saudação atuam como distribuidor e de trabalho. Outros nós em grupos de saudação são nós de trabalho. Um **dispatcher** nó recebe tarefas/trabalhos de movimentação de dados do serviço de nuvem hello e expede nós tooworker (incluindo o próprio). Um **trabalho** nó executa movimentação trabalhos toomove dados entre locais e na nuvem armazenamentos de dados. Todos os nós são de trabalho. Apenas um nó pode ser expedição e de trabalho.    

Normalmente, você pode começar com um nó e **expansão** tooadd mais nós como Olá nós existentes são sobrecarregados com hello de carga de movimentação de dados. Você também pode **expandir** Olá recurso de movimentação de dados de um nó de gateway, aumentando o número de saudação de trabalhos simultâneos permitidos toorun no nó de saudação. Essa funcionalidade também está disponível com um gateway de único nó (mesmo quando o recurso de escalabilidade e disponibilidade Olá não está habilitado). 

Um gateway com vários nós mantém Olá credenciais do repositório de dados sincronizados em todos os nós. Se houver um problema de conectividade de nó para nó, credenciais Olá podem estar fora de sincronia. Quando você define as credenciais para um repositório de dados local que usa um gateway, ele salva as credenciais no nó do hello dispatcher/de trabalho. Olá dispatcher nó for sincronizado com os outros nós de trabalho. Esse processo é conhecido como **credenciais sincronização**. canal de comunicação de saudação entre os nós pode ser **criptografado** por um certificado SSL/TLS pública. 

## <a name="set-up-a-multi-node-gateway"></a>Configurar um gateway com vários nós
Esta seção pressupõe que você ter feito Olá dois artigos ou esteja familiarizado com conceitos nestes artigos a seguir: 

- [Gateway de gerenciamento de dados](data-factory-data-management-gateway.md) -fornece uma visão geral detalhada do gateway de saudação.
- [Mover dados entre locais e na nuvem armazenamentos de dados](data-factory-move-data-between-onprem-and-cloud.md) – contém um passo a passo com instruções passo a passo para usar um gateway com um único nó.  

> [!NOTE]
> Antes de instalar um gateway de gerenciamento de dados em uma máquina local do Windows, consulte os pré-requisitos listados em [artigo principal Olá](data-factory-data-management-gateway.md#prerequisites).

1. Em Olá [passo a passo](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), ao criar um gateway lógico, habilitar Olá **alta disponibilidade e escalabilidade** recurso. 

    ![Gateway de Gerenciamento de Dados – habilitar alta disponibilidade e escalabilidade](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. Em Olá **configurar** página, use uma **instalação expressa** ou **instalação Manual** link tooinstall um gateway no primeiro nó de saudação (uma máquina local do Windows).

    ![Gateway de Gerenciamento de Dados – instalação manual ou expressa](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Se você usar a opção de instalação expressa Olá, comunicação de nó para nó de saudação é feita sem criptografia. o nome do nó Olá é igual ao nome de máquina do hello. Use a instalação manual se precisa de comunicação entre nós de saudação toobe criptografado ou se desejar toospecify um nome de nó de sua escolha. Nomes de nó não podem ser editados posteriormente.
3. Se você escolher **instalação expressa**
    1. Você verá Olá seguinte mensagem depois de gateway de saudação for instalado com êxito:

        ![Gateway de Gerenciamento de Dados – êxito na instalação expressa](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Inicie o Gerenciador de configuração de gerenciamento de dados para o gateway de saudação seguindo [estas instruções](data-factory-data-management-gateway.md#configuration-manager). Consulte o nome do gateway Olá, nome do nó, status, etc.

        ![Gateway de Gerenciamento de Dados – instalação do gateway bem-sucedida](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Se você escolher **configuração manual**:
    1. Baixe o pacote de instalação de saudação do hello Microsoft Download Center, executá-lo tooinstall gateway em seu computador.
    2. Saudação de uso **chave de autenticação** de saudação **configurar** gateway de saudação do tooregister de página.
    
        ![Gateway de Gerenciamento de Dados – instalação do gateway bem-sucedida](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. Em Olá **novo nó gateway** página, você pode fornecer um personalizado **nome** toohello nó de gateway. Por padrão, o nome do nó é igual ao nome de máquina do hello.    

        ![Gateway de Gerenciamento de Dados – especificar nome](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. Na página seguinte do hello, você pode escolher se muito**habilitar a criptografia para comunicação de nó para nó**. Clique em **ignorar** toodisable criptografia (padrão).

        ![Gateway de Gerenciamento de Dados – habilitar criptografia](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Alteração do modo de criptografia só tem suporte quando você tem um nó único gateway no gateway lógico hello. modo de criptografia de saudação toochange quando um gateway tem vários nós, Olá seguintes etapas: excluir todos os nós de hello, exceto uma, alterar o modo de criptografia hello e adicione nós Olá novamente.
        > 
        > Consulte a seção [Requisitos de certificado TLS/SSL](#tlsssl-certificate-requirements) para obter uma lista de requisitos para usar um certificado TLS/SSL. 
    5. Depois de saudação gateway é instalado com êxito, clique em Iniciar o Configuration Manager:
    
        ![Instalação manual – iniciar gerenciador de configurações](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. Consulte o Gerenciador de configuração de Gateway de gerenciamento de dados no nó de saudação (máquina do Windows local), que mostra o status de conectividade, **nome do gateway**, e **o nome do nó**.  

        ![Gateway de Gerenciamento de Dados – instalação do gateway bem-sucedida](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Se estiver Provisionando gateway Olá em uma VM do Azure, você pode usar [este modelo do Gerenciador de recursos do Azure no GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Esse script cria um gateway lógico, configura as VMs com software de Gateway de gerenciamento de dados instalado e registrá-los com o gateway de lógica de saudação. 
6. No portal do Azure, inicie Olá **Gateway** página: 
    1. Na página de home Olá dados fábrica no portal de saudação, clique em **serviços vinculados**.
    
        ![Página inicial da data factory](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Selecione Olá **gateway** toosee Olá **Gateway** página:
    
        ![Página inicial da data factory](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Consulte Olá **Gateway** página:   

        ![Gateway com exibição de nó único](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Clique em **adicionar nó** em Olá barra de ferramentas tooadd um gateway de lógica de toohello do nó. Se você estiver planejando a configuração expressa toouse, siga esta etapa de máquina local Olá que será adicionada como um gateway de toohello do nó. 

    ![Gateway de Gerenciamento de Dados – menu adicionar nó](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. As etapas são semelhante toosetting o primeiro nó de saudação. Olá UI do Configuration Manager permite que você defina o nome do nó hello, se você escolher a opção de instalação manual de saudação: 

    ![Gerenciador de Configurações – instalar segundo gateway](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Depois de gateway de saudação é instalado com êxito no nó Olá, ferramenta Gerenciador de configurações de saudação exibe Olá tela a seguir:  

    ![Gerenciador de Configurações – instalação do segundo gateway bem-sucedida](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Se você abrir Olá **Gateway** página no portal de Olá, você verá dois nós de gateway agora: 

    ![Gateway com dois nós no portal de saudação](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete um nó do gateway, clique em **Excluir nó** na barra de ferramentas hello, selecione o nó de saudação você deseja toodelete e, em seguida, clique em **excluir** na barra de ferramentas de saudação. Essa ação exclui o nó selecionado de saudação do grupo hello. Observe que essa ação não desinstala software do gateway de gerenciamento de dados de saudação do nó da saudação (máquina do Windows local). Use **adicionar ou remover programas** no painel de controle no gateway de Olá Olá local toouninstall. Quando você desinstalar o gateway do nó hello, ele será automaticamente excluído no portal de saudação.   

## <a name="upgrade-an-existing-gateway"></a>Atualizar um gateway existente
Você pode atualizar um existente gateway toouse Olá alta disponibilidade e escalabilidade. Esse recurso funciona somente conosco que têm o gateway de gerenciamento de dados de saudação da versão > = 2.12.xxxx. Você pode ver a versão de saudação do gateway de gerenciamento de dados instalado em um computador em Olá **ajuda** guia da saudação Gerenciador de configuração de Gateway de gerenciamento de dados. 

1. Atualizar o gateway de Olá Olá local máquina toohello versão mais recente seguindo baixando e executando um pacote de instalação do MSI de saudação [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Consulte a seção [Instalação](data-factory-data-management-gateway.md#installation) para obter detalhes.  
2. Navegue toohello portal do Azure. Iniciar Olá **página de fábrica de dados** sua fábrica de dados. Clique em vinculado serviços bloco toolaunch Olá **página serviços vinculados**. Saudação de toolaunch gateway Olá selecione **página gateway**. Clique em e habilitar **recurso de visualização** conforme Olá a imagem a seguir: 

    ![Gateway de Gerenciamento de Dados – habilitar versão prévia do recurso](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Após habilitar o recurso de visualização Olá no portal de hello, feche todas as páginas. Reabra Olá **página gateway** toosee Olá nova visualização interface do usuário (IU).
 
    ![Gateway de Gerenciamento de Dados – versão prévia do recurso habilitada com êxito](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Gateway de Gerenciamento de Dados – interface do usuário da versão prévia](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Durante a atualização de Olá, nome do primeiro nó de saudação é nome de saudação da máquina de saudação. 
3. Agora, adicione um nó. Em Olá **Gateway** , clique em **adicionar nó**.  

    ![Gateway de Gerenciamento de Dados – menu adicionar nó](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Siga as instruções do hello anterior seção tooset o nó de saudação. 

### <a name="installation-best-practices"></a>Melhores práticas de instalação

- Configure plano de energia no computador de host Olá para o gateway de saudação para que hello máquina não entra em hibernação. Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata.
- Fazer backup de certificado Olá associado Olá gateway.
- Verifique se todos os nós são de configuração semelhante (recomendada) para um desempenho ideal. 
- Adicione a alta disponibilidade de tooensure de pelo menos dois nós.  

### <a name="tlsssl-certificate-requirements"></a>Requisitos de certificado TLS/SSL
Aqui estão os requisitos de saudação para certificados TLS/SSL Olá que é usado para proteger as comunicações entre os nós de gateway:

- saudação do certificado deve ser publicamente confiável X509 v3 certificado.
- Todos os nós de gateway devem confiar nesse certificado. 
- É recomendável que você use certificados emitidos por uma AC (autoridade de certificação) pública (de terceiros).
- Dá suporte a qualquer tamanho de chave com suporte pelo Windows Server 2012 R2 para certificados SSL.
- Não dá suporte a certificados que usam chaves CNG.
- Há suporte para certificados curinga. 


## <a name="monitor-a-multi-node-gateway"></a>Monitorar um gateway com vários nós
### <a name="multi-node-gateway-monitoring"></a>Monitoramento de gateway com vários nós
Olá portal do Azure, você verá o instantâneo quase em tempo real de utilização de recursos (CPU, memória, network(in/out), etc.) em cada nó junto com o status de nós de gateway. 

![Gateway de Gerenciamento de Dados – monitoramento de vários nós](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

Você pode habilitar **configurações avançadas** em Olá **Gateway** página toosee avançado métricas como **rede**(in/out), **função & Status de credencial**, que é útil na depuração de problemas do gateway, e **trabalhos simultâneos** (executando / limite) que pode ser modificado / alterado adequadamente durante a ajuste de desempenho. Olá, tabela a seguir fornece descrições das colunas no hello **Gateway nós** lista:  

Propriedade de monitoramento | Descrição
:------------------ | :---------- 
Nome | Nome do gateway lógico hello e nós associada Olá gateway.  
Status | Status do gateway lógico hello e nós de gateway de saudação. Exemplo: Online/Offline/Limitado/etc. Para obter informações sobre esses status, consulte a seção [Status do gateway](#gateway-status). 
Versão | Mostra a versão de saudação do gateway lógico hello e cada nó do gateway. versão de saudação do gateway de lógica de saudação é determinado com base na versão de maioria de nós no grupo de saudação. Se não houver nós com versões diferentes na instalação do gateway lógico hello, somente nós de saudação com hello mesmo número de versão da função de gateway lógico Olá corretamente. Outras pessoas estão no modo limitado hello e precisam toobe atualizado manualmente (somente no caso de falha de atualização automática). 
Memória disponível | Memória disponível em um nó do gateway. Esse valor é um instantâneo quase em tempo real. 
Utilização da CPU | Utilização da CPU de um nó de gateway. Esse valor é um instantâneo quase em tempo real. 
Rede (Entrada/Saída) | Utilização de rede de um nó de gateway. Esse valor é um instantâneo quase em tempo real. 
Trabalhos Simultâneos (Executando/Limite) | Número de trabalhos ou tarefas em execução em cada nó. Esse valor é um instantâneo quase em tempo real. Limite significa Olá máxima simultâneas de trabalhos para cada nó. Esse valor é definido com base no tamanho da máquina hello. Você pode aumentar Olá limite tooscale a execução de trabalho simultâneas em cenários avançados, onde CPU / memória / rede é subutilizado, mas as atividades são tempo limite. Essa funcionalidade também está disponível com um gateway de único nó (mesmo quando o recurso de escalabilidade e disponibilidade Olá não está habilitado). Para obter mais informações, consulte a seção [considerações de dimensionamento](#scale-considerations). 
Função | Há dois tipos de funções – Dispatcher e de trabalho. Todos os nós são operadores, o que significa que eles podem ser usados tooexecute trabalhos. Há apenas um nó de distribuidor, que é usado toopull tarefas/trabalhos dos serviços de nuvem e distribuição toodifferent nós de trabalho (incluindo o próprio). 

![Gateway de Gerenciamento de Dados – monitoramento avançado de vários nós](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Status do gateway

Olá, tabela a seguir fornece os status possíveis de um **nó gateway**: 

Status  | Comentários/Cenários
:------- | :------------------
Online | Nó conectado tooData serviço de fábrica.
Off-line | O nó está offline.
Atualizando | nó Hello está sendo atualizado automaticamente.
Limitado | Devido a problema de tooConnectivity. Pode ser devido a problema de porta 8050 tooHTTP, problema de conectividade do barramento de serviço ou problema de sincronização de credenciais. 
Inativo | Nó estiver em uma configuração diferente da configuração de saudação de outros nós de maioria.<br/><br/> Um nó pode ficar inativo quando ele não pode se conectar tooother nós. 


Olá, tabela a seguir fornece os status possíveis de um **gateway lógica**. status do gateway Olá depende do status de nós de gateway de saudação. 

Status | Comentários
:----- | :-------
Precisa de Registro | Nenhum nó ainda gateway lógica toothis registrados
Online | Nós de Gateway estão online
Off-line | Nenhum nó no status online.
Limitado | Nem todos os nós neste gateway estão em estado íntegro. Esse status é um aviso de que um nó pode estar inativo! <br/><br/>Pode ser devido a problema de sincronização toocredential no nó de dispatcher/de trabalho. 

### <a name="pipeline-activities-monitoring"></a>Monitoramento de atividades/de pipeline
Olá portal do Azure fornece um experiência com os detalhes de nível granular de nó de monitoramento de pipeline. Por exemplo, ele mostra quais atividades foram executadas em qual nó. Essas informações podem ser úteis para entender os problemas de desempenho em um nó específico, digamos devido a limitação de toonetwork. 

![Gateway de Gerenciamento de Dados – monitoramento de vários nós para pipelines](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Gateway de Gerenciamento de Dados – detalhes do pipeline](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Considerações de escala

### <a name="scale-out"></a>Expansão
Olá quando **memória disponível está baixa** e hello **uso da CPU é alto**, adicionando um novo nó ajuda a expansão da carga de saudação entre máquinas. Se as atividades estão falhando devido nó tootime-out ou o gateway está offline, é útil se você adicionar um gateway de toohello do nó.
 
### <a name="scale-up"></a>Escalar verticalmente
Quando a memória disponível hello e CPU também não são utilizados, mas a capacidade ociosa Olá é 0, você deve ser dimensionado com o aumento do número de saudação de trabalhos simultâneos que podem ser executados em um nó. Você pode também deseja tooscale quando atividades estão expirando porque gateway hello está sobrecarregado. Conforme mostrado na Olá a imagem a seguir, você pode aumentar a capacidade máxima Olá para um nó. Sugerimos duplicando-toostart com.  

![Gateway de Gerenciamento de Dados – considerações de escala](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Problemas conhecidas/últimas alterações

- No momento, você pode ter até toofour nós de gateway físico para um único gateway lógico. Se você precisar de mais de quatro nós por motivos de desempenho, envie um email muito[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Novamente, você não pode registrar um nó de gateway com a chave de autenticação de saudação do outro tooswitch de lógica de gateway do gateway lógico atual de saudação. toore o registro, desinstalar o gateway de saudação do nó hello, reinstale o gateway de saudação e registrá-lo com a chave de autenticação Olá para Olá outro gateway lógico. 
- Se o proxy HTTP é necessário para todos os seus nós de gateway, configurar proxy de saudação no diahost.exe.config e diawp.exe.config e use Olá server manager toomake-se de que todos os nós têm Olá mesmo diahost.exe.config e diawip.exe.config. Consulte a seção [definir configurações de proxy](data-factory-data-management-gateway.md#configure-proxy-server-settings) para obter detalhes. 
- toochange o modo de criptografia para comunicação de nó para nó no Gerenciador de configuração do Gateway, exclua todos os nós de saudação no portal de saudação exceto um. Em seguida, adicione nós após alterar o modo de criptografia de saudação.
- Se você escolher o canal de comunicação de nó para nó de saudação do tooencrypt, use um certificado SSL oficial. Certificado autoassinado pode causar problemas de conectividade como Olá mesmo certificado pode não ser confiável na lista de autoridade de certificação em outros computadores. 
- Você não pode registrar um gateway do gateway nó tooa lógico quando a versão do nó Olá é inferior à versão do gateway lógico de saudação. Excluir todos os nós do gateway de lógica de saudação do portal de forma que você pode registrar um node(downgrade) versão inferior-lo. Se você excluir todos os nós de um gateway lógico, manualmente instalar e registrar o novo gateway lógica toothat de nós. Não há suporte para a instalação expressa nesse caso.
- Você não pode usar a configuração expressa tooinstall nós tooan lógico gateway existente, que ainda está usando credenciais de nuvem. Você pode verificar onde armazenadas credenciais de saudação do hello Gateway Configuration Manager no guia de configurações de saudação.
- Você não pode usar a configuração expressa tooinstall nós tooan lógico gateway existente, que tem a criptografia de nó para nó habilitada. Como a configuração do modo de criptografia Olá envolve adicionar manualmente os certificados, instalação expressa é não mais uma opção. 
- Para obter uma cópia do arquivo do ambiente local, você não deve mais usar \\localhost ou C:\files, já que o localhost ou a unidade local podem não estar acessíveis por meio de todos os nós. Em vez disso, use \\local dos arquivos de toospecify ServerName\files.


## <a name="rolling-back-from-hello-preview"></a>Revertendo da visualização Olá 
tooroll da visualização hello, exclua todos os nós, mas um nó. Não importa quais nós, excluir, mas certifique-se de que você tem pelo menos um nó no gateway lógico hello. Desinstalando o gateway na máquina de saudação ou usando Olá portal do Azure, você pode excluir um nó. Em Olá portal do Azure, na Olá **Data Factory** , clique em Olá de toolaunch serviços vinculados **serviços vinculados** página. Saudação de toolaunch gateway Olá selecione **Gateway** página. Na página de saudação do Gateway, você pode ver nós Olá associadas Olá gateway. página de saudação permite que você excluir um nó do gateway de saudação.
 
Depois de excluir, clique em **recursos de visualização** Olá a mesma página de portal do Azure e desabilitar o recurso de visualização de saudação. Redefinir o gateway do gateway tooone nó GA (disponibilidade geral).


## <a name="next-steps"></a>Próximas etapas
Examine Olá artigos a seguir:
- [Gateway de gerenciamento de dados](data-factory-data-management-gateway.md) -fornece uma visão geral detalhada do gateway de saudação.
- [Mover dados entre locais e na nuvem armazenamentos de dados](data-factory-move-data-between-onprem-and-cloud.md) – contém um passo a passo com instruções passo a passo para usar um gateway com um único nó. 
