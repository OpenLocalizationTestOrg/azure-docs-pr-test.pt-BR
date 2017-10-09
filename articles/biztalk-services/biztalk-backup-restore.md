---
title: "aaaCreate e restaurar um backup nos Serviços BizTalk | Microsoft Docs"
description: "Os serviços BizTalk incluem backup e restauração. Saiba como toocreate e restaurar um backup e determinar o que foi feito backup. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>Serviços BizTalk: backup e restauração

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Os Serviços BizTalk do Azure incluem recursos de backup e restauração. Este tópico descreve como toobackup e restauração de serviços do BizTalk usando Olá portal clássico do Azure.

Você também pode fazer backup de serviços do BizTalk usando Olá [API REST dos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Conexões híbridas não estão incluídas no backup independentemente Olá Edition. Você deve recriar suas conexões híbridas.


## <a name="before-you-begin"></a>Antes de começar
* É possível que o backup e a restauração não estejam disponíveis para todas as edições. Consulte [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md).
* Usando Olá portal clássico do Azure, você pode criar um backup sob demanda ou criar um backup agendado. 
* Conteúdo de backup pode ser restaurado toohello mesmo BizTalk Service ou tooa novo BizTalk Service. toorestore Olá BizTalk Service usando Olá Olá existente BizTalk Service de mesmo nome deve ser excluído e Olá nome deve estar disponível. Depois de excluir um BizTalk Service, pode levar mais tempo do que desejar para Olá mesmo nome toobe disponível. Se você não puder esperar pela Olá mesmo nome toobe disponível, em seguida, restaure tooa novo BizTalk Service.
* Os serviços do BizTalk pode ser restaurado toohello mesma edição ou uma edição superior. Restauração de Serviços BizTalk tooa edição inferior, quando foi feito o backup de hello, não há suporte.
  
    Por exemplo, um backup usando Olá que edição Basic pode ser restaurado toohello edição Premium. Um backup usando Olá que Premium Edition não pode ser restaurado toohello Standard Edition.
* números de controle de EDI Olá backup toomaintain continuidade de números de controle de saudação. Se as mensagens são processadas após o último backup de hello, restaurar o conteúdo de backup pode causar números de controle duplicados.
* Se um lote de mensagens ativas processar em lotes de saudação **antes de** executar um backup. Ao criar um backup (conforme necessário ou agendado), as mensagens em lotes nunca são armazenadas. 
  
    **Se um backup for feito com mensagens ativas em um lote, o backup dessas mensagens não será feito e, portanto, elas serão perdidas.**
* Opcional: Olá Portal de Serviços BizTalk, pare de quaisquer operações de gerenciamento.

## <a name="create-a-backup"></a>Criar um backup
Um backup pode ser obtido a qualquer momento e é totalmente controlado por você. Esta seção lista os backups de toocreate etapas Olá Olá clássico do Azure usando o portal, incluindo:

[Backup sob demanda](#backupnow)

[Agendar um backup](#backupschedule)

#### <a name="backupnow"></a>Backup sob demanda
1. No portal clássico do Azure do hello, selecione **Serviços BizTalk**, e, em seguida, selecione Olá BizTalk Service toobackup desejado.
2. Em Olá **painel** guia, selecione **backup** final Olá Olá página.
3. Insira um nome de backup. Por exemplo, digite *meuServiçoBizTalk*BU*Data*.
4. Escolha uma conta de armazenamento de blob e backup de Olá Olá selecione marca de seleção toostart.

Após a conclusão do backup hello, um contêiner com o nome do backup Olá que você inserir é criado na conta de armazenamento hello. Esse contêiner contém a configuração de backup do Serviço do BizTalk.

#### <a name="backupschedule"></a>Agendar um backup
1. No portal clássico do Azure do hello, selecione **Serviços BizTalk**, selecione Olá nome BizTalk Service deseja tooschedule Olá backup e, em seguida, selecione Olá **configurar** guia.
2. Saudação de conjunto **Status de Backup** muito**automática**. 
3. Selecione Olá **conta de armazenamento** toostore Olá backup, digite Olá **frequência** toocreate Olá backups e quanto tempo tookeep hello (**dias de retenção**):
   
    ![][AutomaticBU]
   
    **Observações**     
   
   * Em **dias de retenção**, período de retenção Olá deve ser maior que a frequência de backup hello.
   * Selecione **sempre manter pelo menos um backup**, mesmo se ele for após o período de retenção de saudação.
4. Selecione **Salvar**.

Quando um trabalho de backup agendado é executado, ele cria um contêiner (dados de backup toostore) na conta de armazenamento Olá inserido. nome de saudação do contêiner de saudação é nomeada *BizTalk Service nome-data-hora*. 

Se Olá painel do BizTalk Service mostra um **falha** status:

![Último status do backup agendado][BackupStatus] 

Olá link abre o hello Logs de operação de serviços de gerenciamento toohelp solucionar problemas. Consulte [Serviços BizTalk: solução de problemas usando logs de operação](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Restaurar
Você pode restaurar backups de saudação portal clássico do Azure ou de saudação [restaurar API de REST de Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582). Esta seção lista Olá etapas toorestore usando o portal clássico do hello.

#### <a name="before-restoring-a-backup"></a>Antes de restaurar um backup
* Os novos armazenamentos de acompanhamento, arquivamento e monitoramento podem ser especificados durante a restauração de um Serviço BizTalk.
* Olá mesmos dados de tempo de execução de EDI são restaurados. backup de tempo de execução de EDI Olá armazena números de controle de saudação. Olá restaurado números de controle estão em sequência de tempo de saudação do backup hello. Se as mensagens são processadas após o último backup de hello, restaurar o conteúdo de backup pode causar números de controle duplicados.

#### <a name="restore-a-backup"></a>Restaurar um backup
1. No portal clássico do Azure do hello, selecione **novo** > **serviços de aplicativos** > **BizTalk Service** > **restaurar** :
   
    ![Restaurar um backup][Restore]
2. Em **Backup URL**, selecione o ícone de pasta hello e expanda a conta de armazenamento do Azure Olá repositórios Olá backup de configuração do BizTalk Service. Expanda o contêiner de saudação e no painel direito da saudação, selecione Olá correspondente backup de arquivo. txt. 
   <br/><br/>
   Selecione **Abrir**.
3. Em Olá **serviço de restauração do BizTalk** , insira um **nome do serviço BizTalk** e verifique se Olá **URL do domínio**, **edição**e **Região** para Olá restaurado BizTalk Service. **Criar uma nova instância de banco de dados SQL** para Olá banco de dados de rastreamento:
   
    ![][RestoreBizTalkService]
   
    Selecione a seta Avançar hello.
4. Verificar Olá nome do banco de dados do SQL hello, insira o servidor físico hello, onde o banco de dados SQL Olá será criado e uma nome de usuário/senha para o servidor.

    Se você desejar a edição de banco de dados SQL tooconfigure hello, tamanho e outras propriedades, selecione **definir configurações avançadas do banco de dados**. 

    Selecione a seta Avançar hello.

1. Criar uma nova conta de armazenamento ou insira uma conta de armazenamento existente para Olá BizTalk Service.
2. Selecione a restauração de Olá Olá marca de seleção toostart.

Depois que a restauração de saudação for concluído com êxito, um BizTalk Service novo é listado em um estado suspenso na página de Serviços BizTalk Olá no hello portal clássico do Azure.

### <a name="postrestore"></a>Depois de restaurar um backup
Olá BizTalk Service sempre é restaurado em um **suspenso** estado. Nesse estado, você pode fazer alterações de configuração antes que o novo ambiente do hello está funcionando, incluindo:

* Se você criar aplicativos do BizTalk Service usando Olá SDK dos Serviços BizTalk do Azure, talvez seja necessário credenciais de controle de acesso (ACS) Olá tootooupdate em toowork esses aplicativos com o ambiente de saudação restaurada.
* Restaurar um tooreplicate BizTalk Service um ambiente existente do BizTalk Service. Nessa situação, se houver contratos configurados no portal de Serviços BizTalk original Olá que usam uma pasta de origem FTP, talvez seja necessário tooupdate contratos Olá Olá recém restaurado ambiente toouse uma pasta FTP de origem diferente. Caso contrário, pode haver dois contratos diferentes tentar toopull Olá a mesma mensagem.
* Se você restaurou toohave vários ambientes de BizTalk Service, certifique-se de que ambiente correto de saudação em aplicativos do Visual Studio hello, cmdlets do PowerShell, APIs REST ou APIs de OM de gerenciamento de parceiros comerciais de destino.
* É um backup de tooconfigure automatizada prática recomendada no ambiente do serviço BizTalk Olá recentemente restaurado.

Olá toostart BizTalk Service em Olá portal clássico do Azure, selecione Olá restaurado BizTalk Service e selecione **retomar** na barra de tarefas de saudação. 

## <a name="what-gets-backed-up"></a>Do que é feito backup
Quando um backup é criado, hello itens a seguir são feitos:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Itens do backup</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portal de Serviços BizTalk do Azure</strong></td>
</tr> 
<tr>
<td>Configuração e tempo de execução</td> 
<td>
<ul>
<li>Detalhes e perfil do parceiro</li>
<li>Contratos de parceiro</li>
<li>Assemblies personalizados implantados</li>
<li>Pontes implantadas</li>
<li>Certificados</li>
<li>Transformações implantadas</li>
<li>Pipelines</li>
<li>Modelos criados e salvos em Olá Portal de Serviços BizTalk</li>
<li>Mapeamentos de X12 ST01 e GS01</li>
<li>Números de controle (EDI)</li>
<li>Valores de MIC de mensagens AS2</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Serviço BizTalk do Azure</strong></td>
</tr> 
<tr>
<td>Certificado SSL</td> 
<td>
<ul>
<li>Dados do certificado SSL</li>
<li>Senha do certificado SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Configurações do Serviço do BizTalk</td> 
<td>
<ul>
<li>Contagem de unidades da escala</li>
<li>Edição</li>
<li>Versão do produto</li>
<li>Região/Datacenter</li>
<li>O namespace e a chave do ACS (Serviço de Controle de Acesso)</li>
<li>Cadeia de conexão do banco de dados de acompanhamento</li>
<li>Cadeia de conexão da conta de armazenamento de arquivamento</li>
<li>Cadeia de conexão da conta de armazenamento de monitoramento</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Itens Adicionais</strong></td>
</tr> 
<tr>
<td>Banco de Dados de Acompanhamento</td> 
<td>Quando Olá BizTalk Service é criado, detalhes do banco de dados de rastreamento de saudação são inseridos, incluindo hello servidor de banco de dados do SQL Azure e o nome de banco de dados de rastreamento de saudação. Olá banco de dados de rastreamento não é automaticamente backup.
<br/><br/>
<strong>Importante</strong><br/>
Se Olá banco de dados de rastreamento é excluído e Olá necessidades de banco de dados recuperadas, deve existir um backup anterior. Se não existir um backup, a saudação banco de dados de controle e seus dados não são recuperáveis. Nessa situação, crie um novo banco de dados de rastreamento com hello mesmo nome de banco de dados. A Replicação Geográfica é recomendada.</td>
</tr> 
</table>

## <a name="next"></a>Avançar
Serviços de BizTalk do Azure toocreate em hello Azure clássico, acesse muito[Serviços BizTalk: provisionamento usando o portal do Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart criação de aplicativos, vá muito[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Consulte também
* [Fazer o backup do Serviço BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restaurar o Serviço BizTalk do backup](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Serviços BizTalk: provisionamento usando o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Serviços BizTalk: gráfico do status do provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Serviços BizTalk: guias Painel, Monitor e Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Serviços BizTalk: limitação](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Serviços BizTalk: nome e chave do emissor](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

