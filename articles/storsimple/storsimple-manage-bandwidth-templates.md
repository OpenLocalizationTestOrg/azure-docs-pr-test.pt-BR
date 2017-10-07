---
title: aaaManage seus modelos de largura de banda de StorSimple | Microsoft Docs
description: "Descreve como os modelos de largura de banda StorSimple toomanage, que permitem que você toocontrol consumo de largura de banda."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a>Usar modelos de largura de banda Olá StorSimple Manager serviço toomanage StorSimple
## <a name="overview"></a>Visão geral
Os modelos de largura de banda permitem tooconfigure uso de largura de banda de rede em vários agendamentos de hora do dia tootier Olá data de saudação StorSimple dispositivo toohello nuvem.

Com agendas de limitação da largura de banda, você pode:

* Especifica agendas de largura de banda personalizada dependendo usos de rede de carga de trabalho de saudação.
* Centralizar o gerenciamento e reutilizar os agendamentos de saudação em vários dispositivos de uma maneira fácil e contínua.

> [!NOTE]
> Esse recurso está disponível somente para dispositivos físicos do StorSimple, e não para dispositivos virtuais.
> 
> 

Todos os modelos de largura de banda Olá para o serviço são exibidos em um formato tabular e contêm Olá informações a seguir:

* **Nome do** – modelo de largura de banda de toohello um nome exclusivo atribuído quando ele foi criado.
* **Agenda** – Olá número de agendamentos contidos em um modelo de determinada largura de banda.
* **Usado por** – Olá número de volumes usando modelos de largura de banda de saudação.

Usar o serviço StorSimple Manager Olá **configurar** página em modelos de largura de banda Olá toomanage de portal clássico do Azure.

Você também pode encontrar informações adicionais toohelp configurar modelos de largura de banda em:

* Perguntas e respostas sobre modelos de largura de banda
* Práticas recomendadas para modelos de largura de banda

## <a name="add-a-bandwidth-template"></a>Adicionar um modelo de largura de banda
Execute Olá seguindo as etapas toocreate um novo modelo de largura de banda.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd um modelo de largura de banda
1. Em Olá serviço StorSimple Manager **configurar** , clique em **Adicionar/Editar modelo de largura de banda**.
2. Em Olá **Adicionar/Editar modelo de largura de banda** caixa de diálogo:
   
   1. De saudação **modelo** lista suspensa, selecione **criar novo** tooadd um novo modelo de largura de banda.
   2. Especifique um nome exclusivo para o modelo de largura de banda.
3. Defina uma **Agenda de Largura de Banda**. toocreate uma agenda:
   
   1. Da lista suspensa de saudação, escolha dias Olá da agenda de saudação do hello semana é configurado para. Você pode selecionar vários dias, marcando caixas de seleção Olá localizadas antes do respectivos dias Olá na lista de saudação.
   2. Selecione Olá **dia inteiro** opção se a agenda de saudação é imposta para o dia inteiro hello. Quando essa opção é marcada, você não pode especificar uma **Hora de Início** ou uma **Hora de Término**. agenda de saudação é executada de 12:00 AM too11: 59 PM.
   3. Na lista suspensa de Olá, selecione um **Start Time**. Isso é quando o agendamento Olá começará.
   4. Na lista suspensa de Olá, selecione um **hora de término**. Isso é quando o agendamento de saudação irá parar.
      
      > [!NOTE]
      > Não há permissão para os agendamentos sobrepostos. Se hello horários de início e término resultarem em um agendamento sobreposto, você verá um efeito de toothat de mensagem de erro.
      > 
      > 
   5. Especifique a saudação **taxa de largura de banda**. Isso é Olá largura de banda em Megabits por segundo (Mbps) usada por seu dispositivo StorSimple em operações que envolvem a nuvem de saudação (carregamentos e downloads). Forneça um número entre 1 e 1.000 para esse campo.
   6. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). modelo Olá que você criou será adicionado toohello lista de modelos de largura de banda no serviço Olá **configurar** página.
      
      ![Criar novo modelo de largura de banda](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. Clique em **salvar** na parte inferior da saudação de página hello e clique **Sim** quando for solicitada a confirmação. Isso salvará as alterações de configuração de saudação que você fez.

## <a name="edit-a-bandwidth-template"></a>Editar um modelo de largura de banda
Execute Olá seguindo as etapas tooedit um modelo de largura de banda.

### <a name="tooedit-a-bandwidth-template"></a>tooedit um modelo de largura de banda
1. Clique em **adicionar/editar modelo de largura de banda**.
2. Em Olá **Adicionar/Editar modelo de largura de banda** caixa de diálogo:
   
   1. De saudação **modelo** lista suspensa, escolha uma largura de banda de modelo que você deseja toomodify.
   2. Conclua as alterações. (Você pode modificar qualquer uma das configurações existentes hello.)
   3. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Você verá Olá o modelo modificado na lista de saudação de modelos de largura de banda na página de configuração do serviço de saudação.
3. toosave suas alterações, clique em **salvar** final Olá Olá página. Clique em **Sim** quando solicitada a confirmação.

> [!NOTE]
> Você não poderá ser toosave agendar suas alterações se o agendamento editado Olá se sobrepõe a uma já existente no modelo de largura de banda de saudação que você está modificando.
> 
> 

## <a name="delete-a-bandwidth-template"></a>Excluir um modelo de largura de banda
Execute Olá seguindo as etapas toodelete um modelo de largura de banda.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete um modelo de largura de banda
1. Na lista tabular de saudação de modelos de largura de banda de saudação para seu serviço, selecione o modelo de Olá que você deseja toodelete. Um ícone de exclusão (**x**) será exibido toohello extrema direita do modelo selecionado hello. Clique em Olá **x** modelo de saudação do ícone toodelete.
2. Será solicitada a sua confirmação. Clique em **Okey** tooproceed.

Se o modelo de saudação está em uso por qualquer volume, você não poderá ser toodelete-lo. Você verá uma mensagem de erro indicando que esse modelo hello está em uso. Uma caixa de diálogo de mensagem de erro será exibida informando que todos os Olá referências toohello deve ser removido.

Você pode excluir todos os modelo de toohello de referências de saudação acessando Olá **contêineres de Volume** página e modificando os contêineres de volume Olá que usam esse modelo para que eles usem outro modelo ou usam uma largura de banda personalizada ou ilimitada configuração. Quando todas as referências de saudação foram removidas, você pode excluir o modelo de saudação.

## <a name="use-a-default-bandwidth-template"></a>Usar um modelo de largura de banda padrão
Um modelo de largura de banda padrão é fornecido e é usado pelos contêineres de volume por controles de largura de banda padrão tooenforce ao acessar a nuvem de saudação. modelo de padrão de saudação também serve como uma referência pronta para os usuários que criam seus próprios modelos. Olá detalhes desse modelo padrão são:

* **Nome** : noites e fins de semana ilimitados
* **Agenda** – um único agendamento de segunda-feira tooFriday que se aplica a uma taxa de largura de banda de 1 Mbps entre 8: 00 e 17: 00 horário do dispositivo. largura de banda de saudação é definida tooUnlimited restante de saudação da semana hello.

modelo de padrão de saudação pode ser editado. saudação de uso desse modelo (incluindo versões editadas) é rastreada.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Criar um modelo de largura de banda de dia inteiro que comece em uma hora especificada
Siga este procedimento toocreate uma agenda que inicia em um horário especificado e executa todos os dias. Exemplo hello, agenda Olá inicia às 9: 00 Olá manhã e é executada até Olá 9: 00 manhã seguinte. É importante toonote que Olá início e horários de término para uma determinada agenda devem ser incluídos na Olá mesmo 24 horas agendar e não pode abranger vários dias. Se você precisar tooset modelos de largura de banda que abrangem vários dias, você precisará toouse várias agendas (conforme mostrado no exemplo hello).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate um modelo de largura de banda de dia inteiro
1. Crie uma agenda que inicia às 9: 00 Olá manhã e é executado até meia-noite.
2. Adicione outra agenda. Configure Olá segundo agendamento toorun da meia-noite até 9: 00 Olá manhã.
3. Salve o modelo de largura de banda de saudação.

agendamento composto Olá será, em seguida, iniciar em um horário de sua escolha e executado o dia inteiro.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Perguntas e respostas sobre modelos de largura de banda
**P**. O que acontece toobandwidth controles quando está entre agendamentos Olá? (Uma agenda foi encerrada e outra ainda não foi iniciada.)

**R**. Nesses casos, nenhum controle de largura de banda será utilizado. Isso significa que o dispositivo Olá pode usar a largura de banda ilimitada quando camadas toohello de dados na nuvem.

**P**. Você pode modificar os modelos de largura de banda em um dispositivo offline?

**R**. Não será capaz de toomodify modelos de largura de banda em contêineres de volume se o dispositivo correspondente hello está offline.

**P**. Você pode editar um modelo de largura de banda associado a um contêiner de volume quando os volumes Olá associado estão offline?

**R**. Você pode modificar um modelo de largura de banda associado a um contêiner de volume cujos volumes estejam offline. Observe que, quando os volumes estão offline, nenhum dado será hierárquico de saudação dispositivo toohello nuvem.

**P**. Você pode excluir um modelo padrão?

**R**. Embora você pode excluir um modelo padrão, não é uma boa ideia toodo assim. saudação de uso de um modelo padrão, incluindo versões editadas, é rastreada. Olá, dados de rastreamento é analisado e decorrer Olá de tempo, é o modelo de padrão de saudação do tooimprove usado.

**P**. Como determinar seus modelos de largura de banda necessário toobe modificado?

**R**. Olá sinais de que você precisa de modelos de largura de banda de saudação toomodify é quando você iniciar vendo rede Olá lento ou ter interferências várias vezes em um dia. Se isso acontecer, monitore a rede de armazenamento e uso de saudação examinando os gráficos de desempenho de e/s e a taxa de transferência de rede hello.

De dados de taxa de transferência de rede hello, identifique o tempo de saudação do dia e Olá contêineres de volume no qual Olá afunilamento de rede ocorre. Se isso ocorrer quando os dados estão sendo toohello hierárquico nuvem (obtenha essas informações de desempenho de e/s para todos os contêineres de volume para o dispositivo toocloud), em seguida, você precisará de modelos de largura de banda de saudação toomodify associados aos seus contêineres de volume.

Após a modificação de saudação modelos estão em uso, você precisará rede de saudação toomonitor novamente quanto a latências significativas. Se elas ainda existirem, em seguida, você precisará toorevisit seus modelos de largura de banda.

**P**. O que acontece se vários contêineres de volume em meu dispositivo tiverem agendamentos sobrepostos, mas tooeach de aplicar limites diferentes?

**R**. Vamos supor que você tenha um dispositivo com 3 contêineres de volume. Olá agendamentos associados a esses contêineres completamente sobreponham. Para cada um desses contêineres, limites de largura de banda Olá usados são 5, 10 e 15 Mbps respectivamente. Quando a e/s estão ocorrendo em todos esses contêineres em Olá ao mesmo tempo, no mínimo, Olá Olá 3 limites de largura de banda pode ser aplicado: nesse caso, pois isso compartilhamento de solicitações de e/s de saída de 5 Mbps Olá mesma fila.

## <a name="best-practices-for-bandwidth-templates"></a>Práticas recomendadas para modelos de largura de banda
Siga estas práticas recomendadas para seu dispositivo StorSimple:

* Configure modelos de largura de banda em seu dispositivo tooenable limitação variável da taxa de transferência de rede Olá por dispositivo Olá em diferentes momentos do dia de saudação. Esses modelos de largura de banda quando usados com agendas de backup podem aproveitar eficientemente largura de banda de rede adicionais para operações de nuvem fora dos horários de pico.
* Calcule a largura de banda real Olá necessária para uma implantação específica com base no tamanho de saudação da implantação de saudação e objetivo de tempo de recuperação necessário hello (RTO).

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

