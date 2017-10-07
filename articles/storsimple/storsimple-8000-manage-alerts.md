---
title: "aaaView e gerenciar alertas para o dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Descreve as condições de alerta do StorSimple e severidade, como notificações de alerta tooconfigure e como Olá toouse Gerenciador de dispositivos de StorSimple toomanage alertas de serviço."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: fdd1a911ceff542bc6bdeae877e1f0fc381bf27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-storsimple-alerts"></a>Usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar alertas de StorSimple

## <a name="overview"></a>Visão geral

Olá **alertas** folha em Olá serviço do Gerenciador de dispositivos de StorSimple fornece uma maneira para você tooreview e apaga alertas relacionados ao dispositivo StorSimple em tempo real. Desta folha, você pode centralmente monitorar Olá problemas de integridade de seus dispositivos StorSimple e Olá solução geral do Microsoft Azure StorSimple.

Este tutorial descreve as condições de alerta comuns, níveis de severidade do alerta e como tooconfigure notificações de alerta. Além disso, ele inclui alerta referência rápida de localizar um alerta específico de tabelas, que permitem que você tooquickly e respondem adequadamente.

![Página de alertas](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="common-alert-conditions"></a>Condições comuns de alerta

Seu dispositivo StorSimple gera alertas em variedade de tooa de resposta de condições. Olá seguem tipos mais comuns de saudação das condições de alerta:

* **Problemas de hardware** – estes alertas informam sobre integridade de saudação do seu hardware. Eles permitem saber se as atualizações de firmware são necessárias, se uma interface de rede está com problemas ou se há um problema com uma de suas unidades de dados.
* **Problemas de conectividade** – esses alertas ocorrem quando há dificuldade na transferência de dados. Problemas de comunicação podem ocorrer durante a transferência de dados tooand de vencimento ou conta de armazenamento do Azure Olá toolack de conectividade entre os dispositivos de saudação e serviço de Gerenciador de dispositivos de StorSimple hello. Problemas de comunicação são alguns dos toofix mais difícil Olá porque há muitos pontos de falha. Sempre, primeiro você deve verificar se a conectividade de rede e acesso à Internet estão disponíveis antes de continuar toomore a solução de problemas avançada. Para obter ajuda com solução de problemas, vá muito[solução de problemas com o cmdlet Olá Conexão de teste](storsimple-troubleshoot-deployment.md).
* **Problemas de desempenho** – esses alertas são causados quando o sistema não estiver sendo executado corretamente, como quando ele está sob uma carga pesada.

Além disso, você pode ver toosecurity relacionados de alertas, atualizações ou falhas no trabalho.

## <a name="alert-severity-levels"></a>Níveis de severidade do alerta

Alertas têm diferentes níveis de severidade, dependendo do impacto Olá Olá situação de alerta terá e Olá a necessidade de um alerta de toohello de resposta. níveis de severidade de saudação são:

* **Crítico** – este alerta está em condição de tooa de resposta que está afetando o desempenho adequado de saudação do seu sistema. Ação é necessário tooensure que o serviço do StorSimple Olá não seja interrompido.
* **Aviso** – essa condição poderá se tornar crítica se não for resolvida. Você deve investigar a situação hello e tomar qualquer problema de saudação tooclear ação é necessária.
* **Informações** – esse alerta contém informações que podem ser úteis para controlar e gerenciar seu sistema.

## <a name="configure-alert-settings"></a>Definição de configurações de alerta

Você pode escolher se deseja toobe notificado por e-mail das condições de alerta para cada um dos seus dispositivos StorSimple. Além disso, você pode identificar outros destinatários de notificação de alerta, digitando seus endereços de email no hello **outros destinatários de email** caixa, separados por ponto e vírgula.

> [!NOTE]
> Você pode inserir um máximo de 20 endereços de email por dispositivo.

Depois de habilitar notificação por email para um dispositivo, os membros da lista de notificação de saudação receberão uma mensagem de email sempre que ocorrer um alerta crítico. mensagens de saudação serão enviadas por  *storsimple-alerts-noreply@mail.windowsazure.com*  e descreverão a condição de alerta de saudação. Destinatários podem clicar em **Unsubscribe** tooremove si na lista de notificação de email hello.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>tooenable notificação por email de alertas para um dispositivo
1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Na lista de saudação de dispositivos, selecione e clique em dispositivo Olá que você deseja tooconfigure.
2. Vá muito**configurações** > **geral** para dispositivo hello.

   ![Folha Alertas](./media/storsimple-8000-manage-alerts/configure-alerts-email2.png)
   
2. Em Olá **configurações gerais** folha, ir muito**configurações de alerta** e defina Olá seguinte:
   
   1. Em Olá **enviar notificação por email** campo, selecione **Sim**.
   2. Em Olá **administradores de serviço de Email** campo, selecione **Sim** toohave Olá administrador e serviço todos os administradores recebem notificações de alerta de saudação.
   3. Em Olá **outros destinatários de email** , digite os endereços de email de saudação de todos os outros destinatários que devem receber notificações de alerta de saudação. Insira os nomes no formato de saudação  *someone@somewhere.com* . Use endereços de email de saudação de tooseparate ponto e vírgula. Você pode configurar um máximo de 20 endereços de email por dispositivo. 
      
3. toosend uma notificação de email de teste, clique em **enviar email de teste**. saudação de serviço do Gerenciador de dispositivos de StorSimple exibirá mensagens de status conforme ele encaminha a notificação de teste de saudação.

    ![Configurações de alerta](./media/storsimple-8000-manage-alerts/configure-alerts-email3.png)

4. Você verá uma notificação quando o email de teste de saudação é enviado. 
   
    ![Email de notificação de teste de alertas enviado](./media/storsimple-8000-manage-alerts/configure-alerts-email4.png)
   
   > [!NOTE]
   > Se o teste de saudação mensagem de notificação não serão enviados, serviço de Gerenciador de dispositivos de StorSimple Olá exibirá uma mensagem de erro apropriado. Aguarde alguns minutos e, em seguida, tente toosend a mensagem de notificação de teste novamente. 

5. Depois que você concluiu a configuração de saudação, clique em **salvar**. Quando solicitado a confirmar, clique em **Sim**.

     ![Email de notificação de teste de alertas enviado](./media/storsimple-8000-manage-alerts/configure-alerts-email5.png)

## <a name="view-and-track-alerts"></a>Exibir e controlar os alertas

lâmina do resumo de serviço do Gerenciador de dispositivos do StorSimple Olá fornece uma visão geral rápida número Olá de alertas em seus dispositivos, organizados por nível de severidade.

![Painel de alertas](./media/storsimple-8000-manage-alerts/device-summary4.png)

Clicando em nível de severidade Olá abre Olá **alertas** folha. resultados da saudação incluem apenas os alertas de saudação que correspondem a esse nível de severidade.

Clicando em um alerta na lista de saudação fornece detalhes adicionais sobre o alerta de saudação, incluindo Olá último tempo Olá alerta foi relatado, número de saudação de ocorrências do alerta Olá no dispositivo hello e hello recomendado alerta de saudação tooresolve ação. Se um alerta de hardware, ele também identificará o componente de hardware hello.

![Exemplo de alerta de hardware](./media/storsimple-8000-manage-alerts/configure-alerts-email14.png)

Você pode copiar o arquivo de texto em tooa Olá detalhes do alerta se você precisar toosend Olá informações tooMicrosoft suporte. Após ter seguido recomendação Olá e resolver Olá condição de alerta local, você deve limpar o alerta de saudação do dispositivo de saudação selecionando alerta Olá no hello **alertas** folha e clicando em **limpar**. tooclear vários alertas, selecionadas cada alerta, clique em qualquer coluna exceto Olá **alerta** coluna e clique **limpar** após você ter selecionado todos Olá toobe alertas desmarcada. Observe que alguns alertas são desmarcadas automaticamente quando Olá problema for resolvido ou quando o sistema Olá atualiza o alerta de saudação com novas informações.

Quando você clica em **limpar**, você terá Olá oportunidade tooprovide comentar alerta hello e etapas de saudação que levou tooresolve Olá problema. Alguns eventos serão apagados pelo sistema Olá se outro evento for acionado com novas informações. Nesse caso, você verá o seguinte mensagem de saudação.

![Limpar mensagem de alerta](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Classificação e análise de alertas

Você pode achar mais eficientes relatórios toorun em alertas para que você pode revisar e limpá-los em grupos. Além disso, Olá **alertas** folha pode exibir os alertas de too250. Se você excedeu o número de alertas, nem todos os alertas serão exibidos no modo de exibição do saudação padrão. Você pode combinar Olá campos toocustomize quais alertas são exibidas a seguir:

* **Status** – Você pode exibir alertas **Ativos** ou **Removidos**. Alertas ativos ainda estão sendo acionados no seu sistema, enquanto os alertas apagados tenham sido apagadas manualmente por um administrador ou desmarcadas programaticamente porque sistema Olá atualizado condição de alerta de saudação com novas informações.
* **Severidade** – Você pode exibir alertas de todos os níveis de severidade (críticos, avisos, informações) ou apenas uma determinada severidade, como, por exemplo, somente alertas críticos.
* **Origem** – você pode exibir alertas de todas as fontes ou limitar Olá alertas toothose que vêm de serviço hello ou um ou todos os dispositivos de saudação.
* **Intervalo de tempo** – especificando Olá **de** e **para** datas e os carimbos de hora, você pode examinar alertas durante a saudação período de tempo que você está interessado.

![Lista Alertas](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="alerts-quick-reference"></a>Referência rápida de alertas

Olá tabelas a seguir lista alguns dos alertas do Microsoft Azure StorSimple Olá que você pode encontrar, bem como recomendações e informações adicionais quando disponíveis. Alertas do dispositivo StorSimple se encaixam em uma saudação categorias a seguir:

* [Alertas de conectividade de nuvem](#cloud-connectivity-alerts)
* [Alertas de cluster](#cluster-alerts)
* [Alertas de recuperação de desastres](#disaster-recovery-alerts)
* [Alertas de hardware](#hardware-alerts)
* [Alertas de falha nos trabalhos](#job-failure-alerts)
* [Alertas de volume fixado localmente](#locally-pinned-volume-alerts)
* [Alertas de rede](#networking-alerts)
* [Alertas de desempenho](#performance-alerts)
* [Alertas de segurança](#security-alerts)
* [Alertas do pacote de suporte](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertas de conectividade de nuvem

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Conectividade muito <*nome da credencial de nuvem*> não pode ser estabelecida. |Não é possível conectar-se a conta de armazenamento toohello. |Parece que pode haver um problema de conectividade com o seu dispositivo. Execute Olá `Test-HcsmConnection` cmdlet do hello Interface do Windows PowerShell para StorSimple em seu dispositivo tooidentify e corrigir o problema de saudação. Se Olá configurações estiverem corretas, problema de saudação pode ser com credenciais Olá Olá da conta de armazenamento para o qual o alerta de saudação foi gerado. Nesse caso, use Olá `Test-HcsStorageAccountCredential` toodetermine cmdlet se houver problemas que você possa resolver.<ul><li>Verifique as configurações de rede.</li><li>Verifique as credenciais da conta de armazenamento.</li></ul> |
| Não recebemos uma pulsação de seu dispositivo para Olá última <*número*> minutos. |Não é possível conectar-se toodevice. |Parece que há um problema de conectividade com o seu dispositivo. Use Olá `Test-HcsmConnection` cmdlet do hello Interface do Windows PowerShell para StorSimple em seu dispositivo tooidentify e corrigir o problema de saudação ou entre em contato com seu administrador de rede. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>Comportamento de StorSimple quando a conectividade de nuvem falha

O que acontece se a conectividade de nuvem falhar para o dispositivo StorSimple que está em execução na produção?

Se a falha de conectividade de nuvem em seu dispositivo de produção do StorSimple, em seguida, dependendo Olá estado do seu dispositivo, seguinte Olá pode ocorrer:

* **Para dados de local de saudação em seu dispositivo**: por algum tempo, haverá sem interromper e leituras continuarão toobe servido. No entanto, como número de saudação do IOs pendentes aumenta e excede um limite, Olá leituras podem iniciar toofail.

    Dependendo da quantidade de saudação de dados em seu dispositivo, Olá gravações também continuará toooccur para Olá primeiro algumas horas após a interrupção de saudação na conectividade de nuvem hello. Olá gravações irá reduzir a velocidade e eventualmente iniciar toofail se a conectividade de nuvem de saudação é interrompida por várias horas. (Há armazenamento temporário em dispositivo Olá para dados que são toobe enviada por push toohello nuvem. Essa área é liberada quando Olá dados são enviados. Se a falha de conectividade, dados nessa área de armazenamento não serão enviados toohello nuvem, e e/s falhará.)
* **Para dados de saudação na nuvem Olá**: para a maioria dos erros de conectividade de nuvem, um erro será retornado. Depois de saudação conectividade for restaurada, Olá IOs são reiniciados sem usuário Olá com volume de saudação toobring online. Em casos raros, a intervenção do usuário pode ser necessário toobring Olá back volume on-line de saudação portal do Azure.
* **Para instantâneos de nuvem em andamento**: Olá operação é repetida uma vez dentro de 4 a 5 horas e se a conectividade de saudação não for restaurada, instantâneos de nuvem Olá falhará.

### <a name="cluster-alerts"></a>Alertas de cluster

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Failover do dispositivo muito <*nome do dispositivo*>. |Dispositivo em modo de manutenção. |Dispositivo passou por failover de conclusão tooentering ou modo de manutenção existente. Isso é normal e nenhuma ação é necessária. Após a confirmação deste alerta, desmarque-a na página de alertas de saudação. |
| Failover do dispositivo muito <*nome do dispositivo*>. |Firmware ou software do dispositivo atualizado. |Houve um failover de cluster devido a atualização tooan. Isso é normal e nenhuma ação é necessária. Após a confirmação deste alerta, desmarque-a na página de alertas de saudação. |
| Failover do dispositivo muito <*nome do dispositivo*>. |Controlador desligado ou reiniciado. |Dispositivo passou por failover porque o controlador ativo Olá foi desligado ou reiniciado por um administrador. Nenhuma ação é necessária. Após a confirmação deste alerta, desmarque-a na página de alertas de saudação. |
| Failover do dispositivo muito <*nome do dispositivo*>. |Failover planejado. |Verifique se esse foi um failover planejado. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação. |
| Failover do dispositivo muito <*nome do dispositivo*>. |Failover não planejado. |StorSimple foi criado recuperar tooautomatically de failovers não planejados. Se você vir um grande número desses alertas, contate o Suporte da Microsoft. |
| Failover do dispositivo muito <*nome do dispositivo*>. |Outro/causa desconhecida. |Se você vir um grande número desses alertas, contate o Suporte da Microsoft. Depois de saudação problema for resolvido, desmarque este alerta da página de alertas de saudação. |
| O serviço de um dispositivo crítico informa o status de falha. |Falha no serviço de caminho de dados. |Contate o Suporte da Microsoft para obter assistência. |
| O endereço IP virtual da interface de rede <*DATA #*> informa o status de falha. |Outro/causa desconhecida. |Condições temporárias, às vezes, podem causar esses alertas. Se esse for o caso de Olá, em seguida, esse alerta será automaticamente excluído após algum tempo. Se Olá problema persistir, entre em contato com o Microsoft Support. |
| O endereço IP virtual da interface de rede <*DATA #*> informa o status de falha. |Nome da interface: <*dados #*> endereço IP <IP address> não pode ser colocado online porque um endereço IP duplicado foi detectado na rede de saudação. |Certifique-se de que o endereço IP duplicado de saudação é removido da rede hello, ou reconfigure interface Olá com um endereço IP diferente. |

### <a name="disaster-recovery-alerts"></a>Alertas de recuperação de desastres

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| As operações de recuperação não podem restaurar todas as configurações de saudação para este serviço. Os dados de configuração do dispositivo estão em um estado inconsistente para alguns dispositivos. |Inconsistência de dados detectada após a recuperação de desastres. |Os dados criptografados no serviço de saudação não estão sincronizados com o que dispositivo hello. Autorizar o dispositivo hello <*nome do dispositivo*> do processo de sincronização do Gerenciador de dispositivos de StorSimple toostart hello. Saudação de usar a Interface do Windows PowerShell para StorSimple toorun Olá `Restore-HcsmEncryptedServiceData` no dispositivo <*nome do dispositivo*> cmdlet, fornecendo a senha antiga hello como uma entrada toothis perfil de segurança do cmdlet toorestore hello. Em seguida, execute Olá `Invoke-HcsmServiceDataEncryptionKeyChange` chave de criptografia de dados de serviço do cmdlet tooupdate hello. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação. |

### <a name="hardware-alerts"></a>Alertas de hardware

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| O componente de hardware <*ID do componente*> relata o status como <*status*>. | |Condições temporárias, às vezes, podem causar esses alertas. Nesse caso, esse alerta será automaticamente removido após algum tempo. Se Olá problema persistir, entre em contato com o Microsoft Support. |
| Controlador passivo funcionando incorretamente. |controlador (secundário) passivo de saudação não está funcionando. |O dispositivo está funcionando, mas um dos controladores está funcionando incorretamente. Tente reiniciar o controlador em questão. Se o problema de saudação não for resolvido, entre em contato com o Microsoft Support. |

### <a name="job-failure-alerts"></a>Alertas de falha nos trabalhos

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| O backup de <*ID do grupo de volumes de origem*> falhou. |Falha no trabalho de backup. |Problemas de conectividade podem estar impedindo a operação de backup Olá seja concluída com êxito. Se não houver nenhum problema de conectividade, você pode atingiu Olá número máximo de backups. Exclua todos os backups que não são mais necessários e repita a operação de saudação. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação. |
| Clone <*IDs de elemento de backup de origem*> muito <*números de série do volume de destino*> falha. |Falha no trabalho de clone. |Atualização Olá lista backup tooverify que Olá backup ainda é válido. Olá backup for válido, é possível que problemas de conectividade de nuvem estejam impedindo a operação de clone de saudação conclusão com êxito. Se não houver nenhum problema de conectividade, talvez você tenha atingido o limite de armazenamento hello. Exclua todos os backups que não são mais necessários e repita a operação de saudação. Depois que você executou o problema de saudação tooresolve ação apropriada, desmarque este alerta da página de alertas de saudação. |
| A restauração de <*IDs de elemento de backup da fonte*> falhou. |Falha no trabalho de restauração. |Atualização Olá lista backup tooverify que Olá backup ainda é válido. Se Olá backup for válido, é possível que problemas de conectividade de nuvem estejam impedindo a operação de restauração de saudação seja concluída com êxito. Se não houver nenhum problema de conectividade, talvez você tenha atingido o limite de armazenamento hello. Exclua todos os backups que não são mais necessários e repita a operação de saudação. Depois que você executou o problema de saudação tooresolve ação apropriada, desmarque este alerta da página de alertas de saudação. |

### <a name="locally-pinned-volume-alerts"></a>Alertas de volume fixado localmente

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| A criação do volume local <*nome do volume*> falhou. |trabalho de criação de volume Olá falhou. <*Código de erro de falha de toohello correspondente de mensagem de erro*>. |Problemas de conectividade podem estar impedindo a operação de criação de espaço de saudação seja concluída com êxito. Volumes localmente afixados são muito provisionados e o processo de saudação de criar espaço envolve despejo de nuvem de toohello volumes em camadas. Se não houver nenhum problema de conectividade, você pode ter esgotado espaço local Olá dispositivo de saudação. Determine se o espaço existe no dispositivo de saudação antes de tentar essa operação. |
| A expansão do volume local <*nome do volume*> falhou. |trabalho de modificação do volume Olá falhou devido muito <*toohello correspondente de mensagem de erro Falha no código de erro*>. |Problemas de conectividade podem estar impedindo a operação de expansão de volume Olá seja concluída com êxito. Volumes localmente afixados são muito provisionados e o processo de saudação de estender espaço existente Olá envolve despejo de nuvem de toohello volumes em camadas. Se não houver nenhum problema de conectividade, você pode ter esgotado espaço local Olá dispositivo de saudação. Determine se o espaço existe no dispositivo de saudação antes de tentar essa operação. |
| A conversão do volume <*nome do volume*> falhou. |Olá volume trabalho tooconvert Olá volume tipo de conversão de tootiered localmente afixado falha. |Não foi possível concluir a conversão do volume de saudação do tipo localmente afixado tootiered. Certifique-se de que não há nenhum problema de conectividade impedindo Olá operação concluída com êxito. Para solucionar problemas de conectividade problemas passam muito[solução de problemas com o cmdlet Test-HcsmConnection da saudação](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volume localmente afixado Olá original agora foi marcada como um volume em camadas já que alguns dos dados de saudação do volume localmente afixada de saudação tem vazadas toohello nuvem durante a conversão de saudação. volume em camadas resultante de saudação ainda está ocupando espaço local no dispositivo Olá que não pode ser recuperado para futuras volumes locais.<br>Resolver quaisquer problemas de conectividade, limpe o alerta de saudação e converter esse volume toohello back original volume localmente afixado tipo tooensure todos os dados de saudação é disponibilizado localmente novamente. |
| A conversão do volume <*nome do volume*> falhou. |Olá conversão trabalho tooconvert Olá volume tipo de volume de em camadas toolocally fixado falha. |Não foi possível concluir a conversão do volume de saudação do tipo em camadas toolocally fixado. Certifique-se de que não há nenhum problema de conectividade impedindo Olá operação concluída com êxito. Para solucionar problemas de conectividade problemas passam muito[solução de problemas com o cmdlet Test-HcsmConnection da saudação](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>volume em camadas original Olá marcado como um volume localmente afixado como parte do processo de conversão de saudação continua toohave dados que residem na nuvem hello, enquanto Olá muito provisionados espaço no dispositivo Olá para este volume não pode ser recuperado para futuras local volumes.<br>Resolva quaisquer problemas de conectividade, alerta Olá limpar e converter esse volume toohello back original volume em camadas tipo tooensure local espaço muito provisionado no dispositivo Olá a ser recuperada. |
| Aproximando-se ao consumo de espaço local para instantâneos locais do <*nome do grupo de volume*> |Instantâneos locais para a política de backup Olá assim podem ficar sem espaço e ser invalidada tooavoid falhas de gravação do host. |Instantâneos locais frequentes junto com uma rotatividade alta de dados em volumes de Olá associados a esse grupo de política de backup estão causando o espaço local no hello dispositivo toobe consumido rapidamente. Exclua todos os instantâneos locais que não são mais necessários. Além disso, atualize suas agendas de instantâneo local para este tootake de política de backup menos instantâneos locais frequentes e certifique-se de que os instantâneos de nuvem são realizados regularmente. Se essas ações não são aplicadas, assim pode ser esgotado o espaço local para esses instantâneos e sistema hello serão automaticamente excluí-los tooensure gravações de host continuar toobe processada com êxito. |
| Os instantâneos locais para <*nome do grupo de volume*> foram invalidados. |Olá instantâneos locais para <*nome do grupo de volume*> foram invalidados e excluídos, em seguida, porque eles foram excedendo o espaço local de saudação no dispositivo de saudação. |tooensure que isso não aconteça novamente no hello futuro, examine os agendamentos de instantâneos locais Olá para esta política de backup e excluir todos os instantâneos locais que não são mais necessários. Instantâneos locais frequentes junto com uma rotatividade alta de dados em volumes de Olá associados a esse grupo de política de backup podem causar o espaço local no hello dispositivo toobe consumido rapidamente. |
| A restauração de <*IDs de elemento de backup da fonte*> falhou. |trabalho de restauração Olá falhou. |Se você tiver sido fixado localmente ou uma mistura de volumes localmente fixados e hierárquicos na política de backup, tooverify de lista de backup do hello atualização Olá backup ainda é válida. Se Olá backup for válido, é possível que problemas de conectividade de nuvem estejam impedindo a operação de restauração de saudação seja concluída com êxito. Olá localmente fixados volumes que estavam sendo restaurados como parte deste grupo de instantâneo não tem todos os seus dispositivos de toohello baixado de dados e, se você tiver uma mistura de volumes localmente afixados e hierárquicas neste grupo de instantâneo, eles não serão sincronizados com o outro. toosuccessfully concluir a operação de restauração hello, coloque os volumes de saudação neste grupo offline no host de saudação e repita a operação de restauração de saudação. Observe que quaisquer dados de volume toohello modificações que foram executados durante a saudação processo de restauração serão perdida. |

### <a name="networking-alerts"></a>Alertas de rede

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Não foi possível iniciar os serviços do StorSimple. |Erro de caminho de dados |Se Olá problema persistir, entre em contato com o Microsoft Support. |
| Endereço IP duplicado detectado para 'Data0'. | |sistema de saudação detectou um conflito de endereço IP '10.0.0.1'. Olá 'Data0' do recurso de rede no dispositivo Olá  *<device1>*  está offline. Verifique se esse endereço IP não está sendo usado por qualquer outra entidade nessa rede. problemas de rede tootroubleshoot, ir muito[solução de problemas com o cmdlet Get-NetAdapter de saudação](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Para ajudar a resolver esse problema, entre em contato com o administrador da rede. Se Olá problema persistir, entre em contato com o Microsoft Support. |
| O endereço IPv4 (ou IPv6) para 'Data0' está offline. | |recurso de rede de saudação 'Data0' com endereço IP '10.0.0.1'. e o prefixo de comprimento '22' no dispositivo de saudação  *<device1>*  está offline. Certifique-se de que toowhich de portas de comutador hello esta interface está conectada estão operacionais. problemas de rede tootroubleshoot, ir muito[solução de problemas com o cmdlet Get-NetAdapter de saudação](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |
| Não foi possível conectar o serviço de autenticação toohello. |Erro de caminho de dados |Olá URLthat usado tooauthenticate não está acessível. Certifique-se de que as regras de firewall incluem padrões de URL Olá especificados para o dispositivo StorSimple hello. Para obter mais informações sobre os padrões de URL no portal do Azure, acesse toohttps://aka.ms/ss-8000-network-reqs. Se usando a nuvem do governo do Azure, vá toohello padrões de URL no https://aka.ms/ss8000-gov-network-reqs.|

### <a name="performance-alerts"></a>Alertas de desempenho

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Olá carga de dispositivo foi excedido <*limite*>. |Mais lento do que os tempos de resposta esperados. |O dispositivo está relatando a utilização sob uma pesada carga de entrada/saída. Isso pode causar o trabalho de toonot do dispositivo, bem como deveria. Examine as cargas de trabalho de saudação que você já anexou toohello dispositivo e determinar se há alguma que possa ser movida tooanother dispositivo ou que não são mais necessários.| Não foi possível iniciar os serviços do StorSimple. |Erro de caminho de dados |Se Olá problema persistir, entre em contato com o Microsoft Support. |e Olá status atual, visite muito[Use Olá toomonitor de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Alertas de segurança

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Sessão do Suporte da Microsoft iniciada. |Terceiros acessaram a sessão de suporte. |Confirme se este acesso é autorizado. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação. |
| A senha para <*elemento*> expirará em <*período de tempo*>. |A expiração de senha está se aproximando. |Altere sua senha antes que ela expire. |
| Informações de configuração de segurança ausentes para <*ID do elemento*>. | |Olá volumes associados a esse contêiner de volume não pode ser usado tooreplicate a configuração do StorSimple. tooensure que seus dados são armazenados com segurança, recomendamos que você exclua o contêiner de volume hello e todos os volumes associados com o contêiner de volume Olá. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação. |
| <*número*> tentativas de logon falharam para <*ID do elemento*>. |Falha após várias tentativas de logon. |Seu dispositivo pode estar sendo atacado ou um usuário autorizado está tentando tooconnect com uma senha incorreta.<ul><li>Entre em contato com os usuários autorizados e verifique se essas tentativas foram de uma origem legítima. Se você continuar toosee grande número de tentativas de logon, considere desabilitar o gerenciamento remoto e entrar em contato com seu administrador de rede. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação.</li><li>Verifique se suas instâncias de Snapshot Manager estão configuradas com senha correta hello. Depois que você executou a ação apropriada, desmarque este alerta da página de alertas de saudação.</li></ul>Para obter mais informações, vá muito[alterar uma senha de dispositivo expirada](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Ocorreram uma ou mais falhas durante a alteração da chave de criptografia de dados de serviço de saudação. | |Houve erros durante a alteração da chave de criptografia de dados de serviço de saudação. Depois de resolver condições de erro hello, executar Olá `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet de saudação de Interface do Windows PowerShell para StorSimple em seu serviço de saudação do dispositivo tooupdate. Se o problema persistir, contate o Suporte da Microsoft. Depois de resolver o problema de hello, desmarque este alerta da página de alertas de saudação. |

### <a name="support-package-alerts"></a>Alertas do pacote de suporte

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Falha na criação do pacote de suporte. |StorSimple não pôde gerar um pacote de saudação. |Repita a operação. Se Olá problema persistir, entre em contato com o Microsoft Support. Depois que você tiver resolvido o problema hello, desmarque este alerta da página de alertas de saudação. |

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [Erros do StorSimple e solução de problemas de um dispositivo operacional](storsimple-troubleshoot-operational-device.md).

