---
title: "soluções pré-configuradas de aaaGet iniciado com | Microsoft Docs"
description: "Siga este tutorial toolearn como toodeploy um Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Introdução ao soluções Olá pré-configurado

Azure IoT Suite [soluções pré-configuradas] [ lnk-preconfigured-solutions] combinar várias IoT do Azure services toodeliver ponta a ponta soluções que implementam cenários comuns de negócios de IoT. Olá *monitoramento remoto* solução pré-configurada conecta tooand monitora seus dispositivos. Você pode usar o fluxo de saudação do hello solução tooanalyze de dados de seus dispositivos e os resultados dos negócios tooimprove fazendo processos responder automaticamente toothat o fluxo de dados.

Este tutorial mostra como o monitoramento remoto tooprovision Olá pré-configurado solução. Ele também orienta você por meio de recursos básicos de saudação da solução Olá pré-configurado. Você pode acessar muitos desses recursos de solução de saudação *painel* que implanta como parte da solução Olá pré-configurados:

![Painel de solução pré-configurada de monitoramento remoto][img-dashboard]

toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.

> [!NOTE]
> Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Visão geral do cenário

Quando você implanta Olá solução pré-configurada de monitoramento remoto, ele será preenchido com recursos que permitem que você toostep por meio de um cenário comum de monitoramento remoto. Nesse cenário, solução de toohello conectado vários dispositivos estão relatando os valores de temperatura inesperado. Olá seções a seguir mostram como para:

* Identificar os dispositivos de saudação enviar valores de temperatura inesperado.
* Configurar esses dispositivos toosend mais detalhadas da telemetria.
* Corrigi o problema de saudação pela atualização do firmware Olá nesses dispositivos.
* Verifique se que a ação resolveu o problema de saudação.

Um recurso principal deste cenário é que você pode executar todas essas ações remotamente no painel de solução de saudação. Dispositivos de toohello acesso físico não é necessário.

## <a name="view-hello-solution-dashboard"></a>Painel de solução de saudação de View

Painel de solução de saudação permite toomanage solução de saudação implantada. Por exemplo, você pode exibir telemetria, adicionar dispositivos e configurar regras.

1. Quando Olá provisionamento for concluído e lado a lado para sua solução pré-configurada Olá indica **pronto**, escolha **iniciar** tooopen seu portal de solução de monitoramento remoto em uma nova guia.

    ![Iniciar a solução de saudação pré-configurado][img-launch-solution]

1. Por padrão, o portal de solução Olá mostra Olá *painel*. Você pode navegar tooother áreas do portal de solução hello usando o menu de saudação no lado esquerdo de saudação da página de saudação.

    ![Painel de solução pré-configurada de monitoramento remoto][img-menu]

Painel de saudação exibe Olá informações a seguir:

* Um mapa que exibe o local de saudação de cada dispositivo conectado toohello solução. Quando você executa solução hello, há 25 dispositivos simulados. Hello simulados dispositivos são implementados como WebJobs do Azure, e solução de saudação usa as informações de tooplot de API do Bing Maps de Olá no mapa de saudação. Consulte Olá [perguntas frequentes sobre] [ lnk-faq] toolearn como toomake Olá mapa dinâmico.
* Um painel **Histórico de Telemetria** que plota telemetria de umidade e temperatura de um dispositivo selecionado em tempo quase real e exibe dados de agregação, como umidade média, mínima e máxima.
* Um painel **Histórico de Alarme** que mostra eventos recentes de alarme quando um valor de telemetria excedeu um limite. Você pode definir seus próprios alarmes nos exemplos de toohello adição criados pela solução Olá pré-configurado.
* Um painel **Trabalhos** que exibe informações sobre os trabalhos agendados. Você pode agendar seus próprios trabalhos na página **Trabalhos de gerenciamento**.

## <a name="view-alarms"></a>Exibir alarmes

Painel de histórico de alarme Olá mostra que cinco dispositivos estão se comunicando maior do que os valores esperados de telemetria.

![Histórico de alarme de tarefas no painel de solução de saudação][img-alarms]

> [!NOTE]
> Esses alarmes são gerados por uma regra que está incluída na solução Olá pré-configurado. Essa regra gera um alerta quando o valor de temperatura Olá enviado por um dispositivo excede 60. Você pode definir suas próprias regras e ações escolhendo [regras](#add-a-rule) e [ações](#add-an-action) no menu esquerdo hello.

## <a name="view-devices"></a>Exibir dispositivos

Olá *dispositivos* lista mostra todos os dispositivos de saudação registrado na solução de saudação. Na lista de dispositivos Olá você pode exibir e editar os metadados do dispositivo, adicionar ou remover dispositivos e chamar métodos em dispositivos. Você pode filtrar e classificar lista Olá de dispositivos na lista de dispositivos de saudação. Você também pode personalizar as colunas de Olá mostradas na lista de dispositivos de saudação.

1. Escolha **dispositivos** tooshow lista de dispositivos Olá para esta solução.

   ![Lista de dispositivos de saudação de exibição no portal de solução de saudação][img-devicelist]

1. lista de dispositivos Olá inicialmente mostra 25 dispositivos simulados criados pelo processo de provisionamento de saudação. Você pode adicionar a solução de toohello de dispositivos adicionais simulada e físico.

1. detalhes de saudação tooview de um dispositivo, escolha um dispositivo na lista de dispositivos de saudação.

   ![Exibir detalhes do dispositivo Olá no portal de solução de saudação][img-devicedetails]

Olá **detalhes do dispositivo** painel contém seis seções:

* Uma coleção de links que permitem a você toocustomize Olá ícone do dispositivo, desativar dispositivo hello, adicionar uma regra, invocar um método ou enviar um comando. Para ter uma comparação de comandos (mensagens do dispositivo para nuvem) e métodos (métodos diretos), consulte [Orientação para comunicações entre o dispositivo e a nuvem][lnk-c2d-guidance].
* Olá **dispositivo duas - marcas** seção permite que você tooedit valores de marca para dispositivo hello. Você pode exibir valores de marca na lista de dispositivos de saudação e usar a lista de dispositivos marca valores toofilter hello.
* Olá **dispositivo duas - propriedades desejado** seção permite que você tooset propriedade valores toobe enviado toohello dispositivo.
* Olá **dispositivo duas - propriedades relatadas** seção mostra os valores de propriedade enviados do dispositivo de saudação.
* Olá **propriedades do dispositivo** seção mostra informações de registro de identidade hello como dispositivo Olá chaves de identificação e autenticação.
* Olá **trabalhos recentes** seção mostra informações sobre todos os trabalhos que têm recentemente esse dispositivo de destino.

## <a name="filter-hello-device-list"></a>Lista de dispositivos de saudação do filtro

Você pode usar um filtro toodisplay apenas os dispositivos que estão enviando valores de temperatura inesperado. Olá solução pré-configurada de monitoramento remoto inclui Olá **dispositivos não íntegro** filtrar tooshow dispositivos com um valor de temperatura média maior que 60. Você também pode [criar seus próprios filtros](#add-a-filter).

1. Escolha **abrir salvos filtro** toodisplay uma lista de filtros disponíveis. Em seguida, escolha **dispositivos não íntegro** filtro de saudação tooapply:

    ![Exibir a lista de saudação de filtros][img-unhealthy-filter]

1. lista de dispositivos Olá agora mostra somente os dispositivos com um valor de temperatura média maior que 60.

    ![Exibir lista de dispositivo filtrado Olá mostrando dispositivos não íntegro][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Atualizar as propriedades desejadas

Você identificou agora um conjunto de dispositivos que precisam de correção. No entanto, você decidir que a frequência de dados de saudação de 15 segundos não é suficiente para um diagnóstico claro do problema de saudação. Com mais toobetter de pontos de dados alterando Olá telemetria frequência toofive segundos tooprovide diagnostica o problema de saudação. Você pode enviar por push dispositivos remotos do alteração tooyour essa configuração do portal de solução de saudação. Você pode fazer a alteração de saudação uma vez, avaliar o impacto de Olá e, em seguida, atuar em resultados de saudação.

Siga essas etapas toorun um trabalho que altera a saudação **TelemetryInterval** propriedade para dispositivos Olá afetado desejada. Quando dispositivos Olá recebem Olá novo **TelemetryInterval** valor da propriedade, eles mudam seu telemetria de toosend configuração cada cinco segundos, em vez da cada 15 segundos:

1. Enquanto você estiver mostrando a lista de Olá de dispositivos não íntegro na lista de dispositivos de saudação, escolha **Agendador de trabalhos**, em seguida, **Editar dispositivo duas**.

1. Chamar trabalho Olá **intervalo de alteração de telemetria**.

1. Alterar valor Olá Olá **propriedade desejada** nome **desejado. Config.TelemetryInterval** toofive segundos.

1. Escolha **Agenda**.

    ![Alterar Olá TelemetryInterval propriedade toofive segundos][img-change-interval]

1. Você pode monitorar o andamento de saudação do trabalho Olá Olá **gerenciamento trabalhos** página no portal de saudação.

> [!NOTE]
> Se você quiser toochange um valor de propriedade desejada para um dispositivo individual, use Olá **propriedades desejadas** seção Olá **detalhes do dispositivo** painel em vez de executar um trabalho.

Esse trabalho define o valor de saudação do hello **TelemetryInterval** desejado de propriedade em duas de dispositivo Olá para todos os dispositivos selecionados pelo filtro de saudação de hello. dispositivos de saudação recuperar esse valor de duas de dispositivo hello e atualizar seu comportamento. Quando um dispositivo recupera e processa uma propriedade desejada de duas um dispositivo, ele define a propriedade de valor relatado correspondente do hello.

## <a name="invoke-methods"></a>Invocar métodos

Enquanto o trabalho Olá é executado, você observe na lista de saudação de dispositivos não íntegro todos esses dispositivos têm firmware antigo (menor que a versão 1.6) versões.

![Saudação de exibição relatados versão do firmware para dispositivos não íntegro Olá][img-old-firmware]

Esta versão do firmware pode ser a causa raiz Olá Olá inesperado temperatura valores porque você sabe que outros dispositivos íntegros foram atualizado recentemente tooversion 2.0. É possível usar Olá interno **dispositivos antigos do firmware** filtrar tooidentify quaisquer dispositivos com versões antigas do firmware. No portal de saudação, você poderá remotamente atualizar todos os dispositivos de saudação ainda executando versões antigas do firmware:

1. Escolha **abrir salvos filtro** toodisplay uma lista de filtros disponíveis. Em seguida, escolha **dispositivos antigos do firmware** filtro de saudação tooapply:

    ![Exibir a lista de saudação de filtros][img-old-filter]

1. lista de dispositivos Olá agora mostra somente os dispositivos com versões antigas do firmware. Essa lista inclui cinco dispositivos de saudação identificados pelo Olá **dispositivos não íntegro** filtro e três dispositivos adicionais:

    ![Exibir lista de dispositivo filtrado Olá mostrando dispositivos antigos][img-filtered-old-list]

1. Escolha **Agendador de Trabalho** e, em seguida, **Chamar o Método**.

1. Definir **nome do trabalho** muito**tooversion de atualização de Firmware 2.0**.

1. Escolha **InitiateFirmwareUpdate** como Olá **método**.

1. Saudação de conjunto **FwPackageUri** parâmetro muito**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Escolha **Agenda**. saudação padrão é Olá trabalho toorun agora.

    ![Criar trabalho tooupdate Olá firmware dispositivos Olá selecionado][img-method-update]

> [!NOTE]
> Se você quiser tooinvoke um método em um dispositivo individual, escolha **métodos** em Olá **detalhes do dispositivo** painel em vez de executar um trabalho.

Esse trabalho invoca Olá **InitiateFirmwareUpdate** método direto em todos os dispositivos de saudação selecionados pelo filtro de saudação. Dispositivos respondem imediatamente tooIoT Hub e iniciam o processo de atualização de firmware Olá assincronamente. dispositivos de saudação fornecem informações de status sobre o processo de atualização de firmware Olá por meio de valores de propriedade relatado, conforme mostrado no hello capturas de tela a seguir. Escolha Olá **atualização** informações de saudação tooupdate ícone em listas de trabalho e dispositivo hello:

![Lista de trabalhos, mostrando a execução de lista de atualização de firmware Olá][img-update-1]
![lista de dispositivos, mostrando o status de atualização de firmware][img-update-2]
![trabalho mostrando Olá firmware atualização lista completa][img-update-3]

> [!NOTE]
> Em um ambiente de produção, você pode agendar trabalhos toorun durante uma janela de manutenção designado.

## <a name="scenario-review"></a>Análise do cenário

Nesse cenário, você identificou um problema potencial com alguns de seus dispositivos remotos usando o histórico de alarme Olá no painel hello e um filtro. Você então filtro Olá usado e tooremotely um trabalho configurar Olá dispositivos tooprovide toohelp de informações mais diagnosticar o problema de saudação. Finalmente, você usou um filtro e manutenção de tooschedule um trabalho em dispositivos Olá afetado. Se você retornar toohello painel, você pode verificar que não existem mais qualquer alarmes provenientes de dispositivos em sua solução. Você pode usar um filtro tooverify que Olá firmware está atualizado em todos os dispositivos de saudação em sua solução e que não há mais nenhum íntegros dispositivos:

![Filtro mostrando que todos os dispositivos têm um firmware atualizado][img-updated]

![Filtro mostrando que todos os dispositivos estão íntegros][img-healthy]

## <a name="other-features"></a>Outros recursos

Olá seções a seguir descrevem alguns recursos adicionais de saudação solução pré-configurada de monitoramento remoto que não são descritos como parte do cenário anterior hello.

### <a name="customize-columns"></a>Personalizar colunas

Você pode personalizar as informações de saudação mostradas na lista de dispositivos Olá escolhendo **editor coluna**. Você pode adicionar e remover as colunas que exibem os valores de propriedade e marcação relatados. Também pode reorganizar e renomear as colunas:

   ![Lista de dispositivos coluna editor ion Olá][img-columneditor]

### <a name="customize-hello-device-icon"></a>Personalizar o ícone do dispositivo Olá

Você pode personalizar o ícone do dispositivo Olá exibido na lista de dispositivos de saudação do hello **detalhes do dispositivo** painel da seguinte maneira:

1. Escolha Olá Olá de tooopen do ícone de lápis **Editar imagem** painel para um dispositivo:

   ![Abrir o editor de imagens do dispositivo][img-startimageedit]

1. Carregar uma nova imagem ou usar uma das imagens existentes hello e, em seguida, escolha **salvar**:

   ![Editar o editor de imagens do dispositivo][img-imageedit]

1. Olá imagem selecionada agora exibe em Olá **ícone** coluna para o dispositivo de saudação.

> [!NOTE]
> Olá imagem está armazenada no armazenamento de blob. Uma marca em duas de dispositivo Olá contém uma imagem de toohello link no armazenamento de blob.

### <a name="add-a-device"></a>Adicionar um dispositivo

Quando você implanta a solução Olá pré-configurados, você provisiona automaticamente 25 dispositivos de exemplo que você pode ver na lista de dispositivos de saudação. Esses dispositivos são *dispositivos simulados* em execução em um Trabalho Web do Azure. Dispositivos simulados tornam mais fácil para você tooexperiment com solução Olá pré-configurado sem Olá necessidade toodeploy real, físico dispositivos. Se você quiser tooconnect uma solução de toohello dispositivo real, consulte Olá [conectar sua solução pré-configurada de monitoramento remoto de toohello dispositivo] [ lnk-connect-rm] tutorial.

Olá etapas a seguir mostram como tooadd uma solução do dispositivo simulado toohello:

1. Navegue back toohello lista de dispositivos.

1. tooadd um dispositivo, escolha **+ adicionar um dispositivo** no canto do hello inferior esquerdo.

   ![Adicionar uma solução de toohello pré-configurado do dispositivo][img-adddevice]

1. Escolha **adicionar novo** em Olá **dispositivo simulado** lado a lado.

   ![Definir novos detalhes do dispositivo no painel][img-addnew]

   Em adição toocreating um novo dispositivo simulado, você também pode adicionar um dispositivo físico se você escolher toocreate um **dispositivo personalizado**. toolearn mais sobre como se conectar a solução de toohello de dispositivos físicos, consulte [conectar seu toohello de dispositivo IoT Suite solução pré-configurada de monitoramento remoto][lnk-connect-rm].

1. Selecione **Deixe-me definir minha própria ID** de dispositivo e adicione um nome de ID de dispositivo exclusivo, como **mydevice_01**.

1. Escolha **Criar**.

   ![Salvar um novo dispositivo][img-definedevice]

1. Na etapa 3 do **adicionar um dispositivo simulado**, escolha **feito** lista de dispositivos de toohello tooreturn.

1. Você pode exibir seu dispositivo **executando** na lista de dispositivos de saudação.

    ![Exibir novo dispositivo na lista de dispositivos][img-runningnew]

1. Você também pode exibir hello simulados telemetria do seu dispositivo novo painel hello:

    ![Exibir telemetria do novo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Desabilitar e excluir um dispositivo

Você pode desabilitar um dispositivo e depois que ele for desabilitado, poderá removê-lo:

![Desabilitar e remover um dispositivo][img-disable]

### <a name="add-a-rule"></a>Adicionar uma regra

Existem regras para o novo dispositivo de saudação recém-adicionado. Nesta seção, você deve adicionar uma regra que dispara um alarme quando temperatura Olá relatado pelo Olá novo dispositivo excede 47 graus. Antes de começar, observe que o histórico de telemetria Olá para novo dispositivo de saudação no painel de saudação mostra a temperatura do dispositivo Olá nunca exceda 45 graus.

1. Navegue back toohello lista de dispositivos.

1. tooadd uma regra para dispositivo hello, selecione o novo dispositivo no hello **lista de dispositivos**e, em seguida, escolha **Adicionar regra**.

1. Criar uma regra que usa **temperatura** como campo de dados hello e usa **AlarmTemp** como hello quando temperatura Olá excede 47 graus de saída:

    ![Adicionar uma regra de dispositivo][img-adddevicerule]

1. toosave as alterações, escolha **salvar e exibir regras**.

1. Escolha **comandos** no painel de detalhes de dispositivo Olá para o novo dispositivo de saudação.

    ![Adicionar uma regra de dispositivo][img-adddevicerule2]

1. Selecione **ChangeSetPointTemp** da lista de comandos hello e defina **SetPointTemp** too45. Escolha **Enviar Comando**:

    ![Adicionar uma regra de dispositivo][img-adddevicerule3]

1. Navegue painel traseiro toohello. Após um curto período de tempo, você verá uma nova entrada no hello **histórico de alarme** painel quando a temperatura Olá relatado pelo seu novo dispositivo excede o limite de grau 47 hello:

    ![Adicionar uma regra de dispositivo][img-adddevicerule4]

1. Você pode revisar e editar todas as regras em Olá **regras** página do painel de saudação:

    ![Listar regras de dispositivo][img-rules]

1. Você pode revisar e editar todas as ações de saudação que podem ser executadas na regra de tooa de resposta em Olá **ações** página do painel de saudação:

    ![Listar ações de dispositivo][img-actions]

> [!NOTE]
> É possível toodefine ações que podem enviar uma mensagem de email ou SMS na resposta tooa regra ou integrar com um sistema de linha de negócios por meio de um [aplicativo lógico][lnk-logic-apps]. Para obter mais informações, consulte Olá [tooyour conexão lógica aplicativo monitoramento remoto do Azure IoT Suite pré-configurado solução][lnk-logicapptutorial].

### <a name="manage-filters"></a>Gerenciar filtros

Na lista de dispositivos hello, criar, salvar e recarregar filtros toodisplay uma lista personalizada de hub de tooyour conectado de dispositivos. toocreate um filtro:

1. Escolha o ícone de filtro de edição Olá acima da lista de saudação de dispositivos:

    ![Editor de filtro Olá aberto][img-editfiltericon]

1. Em Olá **editor de filtro**, adicionar campos hello, operadores e lista de dispositivos valores toofilter hello. Você pode adicionar vários toorefine de cláusulas seu filtro. Escolha **filtro** filtro de saudação tooapply:

    ![Crie um filtro][img-filtereditor]

1. Neste exemplo, a lista de saudação é filtrada por fabricante e modelo:

    ![Lista filtrada][img-filterelist]

1. toosave o filtro com um nome personalizado, escolha Olá **Salvar como** ícone:

    ![Salvar um filtro][img-savefilter]

1. tooreapply um filtro que você salvou anteriormente, escolha Olá **abrir salvos filtro** ícone:

    ![Abrir um filtro][img-openfilter]

Você pode criar filtros com base na id do dispositivo, estado do dispositivo, propriedades desejadas, propriedades relatadas e marcações. Adicionar seu próprio dispositivo tooa de marcas personalizadas no hello **marcas** seção Olá **detalhes do dispositivo** painel ou executar um trabalho tooupdate tags em vários dispositivos.

> [!NOTE]
> Em Olá **editor de filtro**, você pode usar o hello **exibição avançada** tooedit Olá texto da consulta diretamente.

### <a name="commands"></a>Comandos

De saudação **detalhes do dispositivo** painel, você pode enviar o dispositivo de toohello de comandos. Quando um dispositivo é iniciado, ele envia informações sobre Olá comandos dá suporte à solução toohello. Para obter uma discussão das diferenças de saudação entre os métodos e comandos, consulte [opções de nuvem para dispositivo do Azure IoT Hub][lnk-c2d-guidance].

1. Escolha **comandos** em Olá **detalhes do dispositivo** painel para o dispositivo selecionado hello:

   ![Comandos de dispositivo no painel][img-devicecommands]

1. Selecione **PingDevice** da lista de comandos de saudação.

1. Escolha **Enviar Comando**.

1. Você pode ver o status de saudação do comando Olá no histórico de comandos de saudação.

   ![Status do comando no painel][img-pingcommand]

solução de saudação rastreia o status de saudação de cada comando envia. Inicialmente é o resultado de saudação **pendente**. Quando o dispositivo Olá relata que ele executou o comando hello, Olá é conjunto de resultados muito**sucesso**.

## <a name="behind-hello-scenes"></a>Em segundo plano da saudação

Quando você implanta uma solução pré-configurada, o processo de implantação de saudação cria vários recursos no hello assinatura do Azure que você selecionou. Você pode exibir esses recursos no hello Azure [portal][lnk-portal]. o processo de implantação Olá cria um **grupo de recursos** com um nome baseado no nome hello escolhido para sua solução pré-configurada:

![Solução pré-configurada em Olá portal do Azure][img-portal]

Você pode exibir configurações de saudação de cada recurso, selecionando-o na lista de saudação de recursos no grupo de recursos de saudação.

Você também pode exibir o código-fonte Olá para solução de saudação pré-configurado. Olá código-fonte solução pré-configurada de monitoramento remoto está em Olá [azure-iot-monitoramento remoto] [ lnk-rmgithub] repositório GitHub:

* Olá **DeviceAdministration** pasta contém o código-fonte para o painel Olá Olá.
* Olá **simulador** pasta contém o código-fonte para o dispositivo simulado Olá Olá.
* Olá **EventProcessor** pasta contém o código-fonte Olá para o processo de back-end de saudação que manipula a telemetria de entrada hello.

Quando você terminar, você pode excluir solução Olá pré-configurado de sua assinatura do Azure em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site. Este site permite que você exclua tooeasily que todos os recursos que foram provisionados quando você criou a solução Olá pré-configurado de hello.

> [!NOTE]
> tooensure excluir tudo relacionados à solução toohello pré-configurado, excluí-la em Olá [azureiotsuite.com] [ lnk-azureiotsuite] do site e não exclua o grupo de recursos de saudação no portal de saudação.

## <a name="next-steps"></a>Próximas etapas

Agora que você implantou uma solução de trabalho pré-configurados, você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:

* [Passo a passo da solução pré-configurada de monitoramento remoto][lnk-rm-walkthrough]
* [Conecte-se a sua solução pré-configurada de monitoramento remoto de toohello de dispositivo][lnk-connect-rm]
* [Permissões no site de azureiotsuite.com Olá][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md