---
title: "aaaUse um SQL Server no local no aprendizado de máquina do Azure | Microsoft Docs"
description: "Use dados de uma análise de tooperform avançado banco de dados local do SQL Server com o aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Executar análises avançadas com o Azure Machine Learning usando os dados de um banco de dados do SQL Server local

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Geralmente as empresas que trabalham com dados locais que tootake de escala hello e agilidade da nuvem Olá para sua cargas de trabalho de aprendizado de máquina. Mas elas não toodisrupt seus processos de negócios atuais e fluxos de trabalho movendo sua nuvem de toohello de dados local. O Azure Machine Learning agora dá suporte à leitura de dados do banco de dados do SQL Server local e, em seguida, ao treinamento e à pontuação de um modelo com esses dados. Você não tem mais toomanually copiar e sincronização de dados de saudação entre Olá nuvem e o servidor de local. Em vez disso, Olá **importar dados** módulo no estúdio de aprendizado de máquina do Azure poderá ler diretamente do banco de dados do SQL Server local para o treinamento e pontuação trabalhos.

Este artigo fornece uma visão geral de como tooingress no local de dados do SQL server em aprendizado de máquina do Azure. Ele pressupõe que você esteja familiarizado com os conceitos de Azure Machine Learning, como espaços de trabalho, módulos, conjuntos de dados, experiências, *etc*.

> [!NOTE]
> Esse recurso não está disponível para os espaços de trabalho gratuitos. Para obter mais informações sobre preços e camadas do Machine Learning, consulte [Preços do Azure Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Instalar Olá Microsoft Data Management Gateway
tooaccess um banco de dados do SQL Server local no aprendizado de máquina do Azure, você precisa toodownload e hello de instalar o Gateway de gerenciamento de dados do Microsoft. Quando você configura a conexão de gateway Olá no estúdio de aprendizado de máquina, você terá a oportunidade de saudação para baixar e instalar o gateway de saudação usando Olá **Download e o gateway de dados de registro** diálogo descrita abaixo.

Você também pode instalar Olá Data Management Gateway antecipadamente baixando e executando o pacote de instalação do MSI Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Escolha a versão mais recente do hello, seleção de 32 bits ou 64 bits, conforme apropriado para seu computador. Olá MSI também pode ser usado tooupgrade uma Data Management Gateway toohello mais recente versão existente, com todas as configurações preservadas.

gateway de saudação tem Olá pré-requisitos a seguir:

* versões de sistema operacional do Windows Hello com suporte são Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Olá recomendado é de configuração para a máquina de gateway hello, pelo menos, 2 GHz, 4 núcleos, 8GB de RAM e disco de 80GB.
* Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata. Portanto, configure um plano de energia apropriadas no computador de saudação antes de instalar o gateway de saudação. Se a máquina Olá é toohibernate configurado, instalação do gateway Olá exibe uma mensagem.
* Como atividade de cópia ocorre em uma frequência específica, Olá uso de recursos (CPU, memória) no computador de saudação segue também Olá mesmo padrão com o horário de pico e ocioso. Utilização de recursos também depende intensamente Olá quantidade de dados que está sendo movidos. Quando vários trabalhos de cópia estiverem em andamento, você observará o uso do recurso aumentar durante horários de pico. Enquanto a configuração mínima de saudação listada acima é tecnicamente suficiente, talvez você queira toohave uma configuração com mais recursos do que a configuração mínima de saudação dependendo de sua carga específico para movimentação de dados.

Considere o seguinte de saudação quando configurar e usar um Gateway de gerenciamento de dados:

* Você pode instalar apenas uma instância do Gateway de Gerenciamento de Dados em um único computador.
* Você pode usar um único gateway para várias fontes de dados locais.
* Você pode se conectar a vários gateways em computadores diferentes toohello mesma fonte de dados local.
* Você configura um gateway para apenas um espaço de trabalho por vez. No momento, os gateways não podem ser compartilhados entre espaços de trabalho.
* Você pode configurar vários gateways para um único espaço de trabalho. Por exemplo, talvez você queira toouse um gateway que está conectada tooyour fontes de dados de teste durante o desenvolvimento e um gateway de produção quando você estiver pronto toooperationalize.
* gateway de saudação não precisa toobe em Olá mesmo computador como fonte de dados de saudação. Mas permanecer toohello mais fonte de dados reduz o tempo de Olá Olá gateway tooconnect toohello fonte de dados. É recomendável que você instale o gateway de saudação em um computador que é diferente da saudação uma fonte de dados local hosts Olá para que hello gateway e fonte de dados não competem por recursos.
* Se você já tiver um gateway instalado no computador atendendo cenários do Power BI ou Azure Data Factory, instale um gateway separado para o Azure Machine Learning em outro computador.

  > [!NOTE]
  > Você não pode executar o Gateway de gerenciamento de dados e o Gateway do Power BI em Olá mesmo computador.
  >
  >
* É necessário toouse Olá Gateway de gerenciamento de dados para o aprendizado de máquina do Azure mesmo se você estiver usando o rota expressa do Azure para outros dados. Trate a fonte de dados como uma fonte de dados local (protegida por um firewall) mesmo quando você usar a ExpressRoute. Usam Olá Data Management Gateway tooestablish conectividade entre o aprendizado de máquina e fonte de dados de saudação.

Você pode encontrar informações detalhadas sobre os pré-requisitos de instalação, as etapas de instalação e dicas de solução de problemas no artigo Olá [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a>
            <span id="using-the-data-gateway-step-by-step-walk" class="anchor">
            <span id="_Toc450838866" class="anchor">
            </span>
            </span>Ingressar dados do banco de dados SQL Server local no Azure Machine Learning
Nesse passo a passo, você vai configurar um Gateway de Gerenciamento de Dados em um espaço de trabalho de Azure Machine Learning, configurá-lo e, em seguida, ler os dados de um banco de dados do SQL Server local.

> [!TIP]
> Antes de começar, desabilite o bloqueador de pop-ups do navegador para `studio.azureml.net`. Se você estiver usando Olá navegador Google Chrome, baixe e instale a uma saudação vários plug-ins disponíveis no Google Chrome WebStore [clique uma vez da extensão do aplicativo](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Etapa 1: criar um gateway
Olá primeira etapa é toocreate e configurar Olá gateway tooaccess banco de dados SQL no local.

1. Faça logon no muito[estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/Home/) e espaço de trabalho Olá selecione que você deseja toowork.
2. Clique em hello **configurações** folha no saudação à esquerda e clique em Olá **GATEWAYS de dados** guia na parte superior da saudação.
3. Clique em **novo GATEWAY de dados** na parte inferior da saudação da tela hello.

    ![Novo Gateway de Dados](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Em Olá **novo gateway de dados** caixa de diálogo, digite Olá **nome do Gateway** e, opcionalmente, adicione um **descrição**. Clique em seta Olá Olá inferior direito toogo toohello próxima etapa da configuração de saudação.

    ![Insira o nome e a descrição do gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. No hello baixar e registrar a caixa de diálogo de gateway de dados, copiar Olá chave de registro de GATEWAY toohello da área de transferência.

    ![Baixar e registrar o gateway de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Se você ainda não baixou e instalou Olá Microsoft Data Management Gateway, clique em **gateway de gerenciamento de dados de Download**. Este usa toothe Microsoft Download Center onde você pode selecionar a versão do gateway Olá você necessário baixá-lo e instalá-lo. Você pode encontrar informações detalhadas sobre os pré-requisitos de instalação, as etapas de instalação e dicas de solução de problemas nas seções de início Olá artigo Olá [mover dados entre fontes locais e na nuvem com o Gateway de gerenciamento de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Depois de instalar o gateway hello, Olá Gerenciador de configuração de Gateway de gerenciamento de dados será aberto e Olá **registrar gateway** caixa de diálogo é exibida. Saudação de colar **chave de registro de Gateway** que você copiou na área de transferência toohello e clique em **registrar**.
8. Se você já tiver instalado um gateway, execute Olá Gerenciador de configuração de Gateway de gerenciamento de dados. Clique em **alterar a chave**, cole o **chave de registro de Gateway** que você copiou na área de transferência toohello na etapa anterior hello e clique em **Okey**.
9. Quando a saudação instalação for concluída, Olá **registrar gateway** para Microsoft Data Management Gateway Configuration Manager da caixa de diálogo é exibido. Cole Olá chave de registro de GATEWAY que você copiou para a área de transferência de saudação em uma etapa anterior e clique em **registrar**.

    ![Registrar gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Olá configuração do gateway é concluída quando Olá valores a seguir é definida no hello **início** guia no Microsoft Data Management Gateway Configuration Manager:

    * **Nome do gateway** e **nome de instância** são definidas toohello nome do gateway de saudação.
    * **Registro** está definido muito**registrado**.
    * **Status** está definido muito**iniciado**.
    * barra de status de saudação do hello inferior exibe **conectado tooData serviço de nuvem do Gateway de gerenciamento** junto com uma marca de seleção verde.

      ![Gerenciador do Gateway de Gerenciamento de Dados](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      O estúdio de aprendizado de máquina do Azure também é atualizado quando Olá registro é bem-sucedido.

    ![Registro de gateway concluído com êxito](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Em Olá **baixar e registrar o gateway de dados** caixa de diálogo, clique em instalação de saudação de toocomplete a marca de seleção. Olá **configurações** página exibe o status do gateway como "Online". No painel direito da saudação, você encontrará status e outras informações úteis.

    ![Configurações de gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Em Olá Gerenciador de configuração do Gateway de gerenciamento de dados Microsoft alternar toohello **certificado** certificado de Olá de guia especificado nessa guia é usada tooencrypt/descriptografar credenciais para armazenamento de dados do hello local que você especificar no portal de saudação. Esse certificado é um certificado padrão de saudação. A Microsoft recomenda alterar esse certificado próprio tooyour que você pode fazer backup em seu sistema de gerenciamento de certificado. Clique em **alteração** toouse seu próprio certificado em vez disso.

    ![Alterar o certificado de gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (opcional) Se você quiser tooenable log detalhado para solucionar problemas com o gateway hello, em Olá Gerenciador de configuração do Gateway de gerenciamento de dados Microsoft alternar toothe **diagnóstico** guia e verifique Olá **habilitar o registro detalhado para solução de problemas** opção. Olá informações de log podem ser encontradas no hello Visualizador de eventos do Windows em Olá **Applications and Services Logs**  - &gt; **Data Management Gateway** nó. Você também pode usar o hello **diagnóstico** guia tootest Olá conexão tooan na fonte de dados local usando o gateway de saudação.

    ![Habilitar registro em log detalhado](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Isso conclui o processo de instalação do gateway Olá no aprendizado de máquina do Azure.
Você está agora pronto toouse seus dados no local.

Você pode criar e configurar vários gateways no Studio de cada espaço de trabalho. Por exemplo, você pode ter um gateway que deseja tooconnect fontes de dados de teste de tooyour durante o desenvolvimento e um gateway diferente para suas fontes de dados de produção. O aprendizado de máquina do Azure fornece o tooset flexibilidade a vários gateways dependendo de seu ambiente corporativo. Atualmente, não é possível compartilhar um gateway entre espaços de trabalho e apenas um gateway pode ser instalado em um único computador. Para obter mais informações, confira [Mover dados entre fontes locais e na nuvem com o Gateway de Gerenciamento de Dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Etapa 2: Usar Olá gateway tooread dados de uma fonte de dados local
Depois de configurar o gateway hello, você pode adicionar uma **importar dados** módulo para um experimento que insere dados de saudação do banco de dados do SQL Server Olá no local.

1. No estúdio de aprendizado de máquina, selecione Olá **experiências** , clique em **+ novo** Olá canto inferior esquerdo e selecione **experiência em branco** (ou selecione uma das várias exemplo experiências disponíveis).
2. Localizar e arraste Olá **importar dados** toohello módulo experimentar a tela.
3. Clique em **Salvar como** abaixo tela hello. Digite "Azure Machine Learning local Tutorial do SQL Server" para o nome do teste hello, selecione o espaço de trabalho e clique Olá **Okey** marca de seleção.

   ![Salve o teste com um novo nome](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Clique Olá **importar dados** tooselect do módulo, em seguida, no **propriedades** toohello painel à direita da tela hello, selecione "Local SQL Database" hello **fonte de dados** lista suspensa.
5. Selecione Olá **gateway de dados** instalado e registrado. Você pode configurar outro gateway selecionando "(adicionar novo Gateway de Dados...)".

   ![Selecionar o gateway de dados para o módulo Importar Dados](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Digite hello SQL **nome do servidor de banco de dados** e **nome do banco de dados**, juntamente com hello SQL **consulta de banco de dados** deseja tooexecute.
7. Clique em **Inserir valores** em **Nome de usuário e senha** e insira suas credenciais de banco de dados. Você pode usar a Autenticação Integrada do Windows ou Autenticação do SQL Server dependendo de como o SQL Server local está configurado.

   ![Inserir as credenciais do banco de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   mensagem de saudação alterações "valores necessários" muito "valores conjunto" com uma marca de seleção verde. Você só precisa ter tooenter Olá credenciais uma vez, a menos que as informações do banco de dados de saudação ou senha for alterada. O aprendizado de máquina do Azure usa o certificado de saudação fornecida quando você instalou as credenciais do hello gateway tooencrypt Olá na nuvem hello. O Azure nunca armazena credenciais locais sem criptografia.

   ![Propriedades do módulo Importar Dados](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Clique em **executar** toorun experimento de saudação.

Depois que o teste Olá concluir a execução, é possível visualizar os dados de saudação importados do banco de dados de saudação clicando Olá a porta de saída de hello **importar dados** módulo e selecionando **visualizar**.

Depois de concluir o desenvolvimento de seu experimento, você poderá implantar e colocar o modelo em operação. Usando Olá serviço de execução de lote de dados de saudação dados do SQL Server local configurado no hello **importar dados** módulo será lido e usado para pontuação. Embora você possa usar Olá serviço de resposta de solicitação de pontuação de dados no local, a Microsoft recomenda usar o [do suplemento do Excel](machine-learning-excel-add-in-for-web-services.md) em vez disso. Atualmente, gravar tooan local banco de dados do SQL Server por meio de **exportar dados** não é serviços web com suporte ou em suas experiências ou publicado.
