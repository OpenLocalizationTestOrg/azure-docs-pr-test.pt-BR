---
title: "aaaCreate Serviços BizTalk do Azure no portal do Azure de saudação | Microsoft Docs"
description: "Saiba como tooprovision ou criar serviços BizTalk do Azure no hello portal do Azure; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Criar serviços do BizTalk usando Olá portal do Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign em toohello portal do Azure, você precisa de uma conta do Azure e a assinatura do Azure. Se você não tiver uma conta, será possível criar uma conta de avaliação gratuita em questão de minutos. Consulte [Avaliação gratuita do Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Criar um Serviço do BizTalk
Dependendo da saudação edição que você escolher, nem todas as configurações do BizTalk Service podem estar disponíveis.

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação inferior hello, selecione **novo**:  
   ![Selecione o botão novo Olá][NEWButton]
3. Selecione **SERVIÇOS DE APLICATIVOS** > **SERVIÇO BIZTALK** > **CRIAÇÃO PERSONALIZADA**:  
   ![Selecionar Serviço BizTalk e Criação Personalizada][NewBizTalkService]
4. Insira as configurações do serviço BizTalk hello:
   
    <table border="1">
    <tr>
    <td><strong>Nome do Serviço BizTalk</strong></td>
    <td>Você pode inserir qualquer nome, mas seja específico. Alguns exemplos incluem:<br/><br/>
    <em>mycompany</em>.biztalk.windows.net<br/>
    <em>mycompanymyapplication</em>.biztalk.windows.net<br/>
    <em>myapplication</em>.biztalk.windows.net<br/><br/>". <yourbiztalkservicename>.BizTalk.Windows.NET" é automaticamente adicionado toohello nome digitado. Isso cria uma URL que é usado tooaccess o BizTalk de serviço, como <strong>https://<em>myapplication</em>. <yourbiztalkservicename>.BizTalk.Windows.NET</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Edição</strong></td>
    <td>Se você estiver na fase de teste/desenvolvimento hello, escolha <strong>desenvolvedor</strong>. Se você estiver na fase de produção de hello, use Olá <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Serviços BizTalk: gráfico de edições</a> toodetermine se <strong>Premium</strong>, <strong>padrão</strong>, ou <strong>Basic</strong>é Olá a opção correta para seu cenário de negócios.
    </td>
    </tr>
    <tr>
    <td><strong>Região</strong></td>
    <td>Selecione Olá região geográfica toohost o BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>URL do Domínio</strong></td>
    <td><strong>Opcional</strong>. Por padrão, a URL do domínio Olá é <em>Nomedeseuserviçobiztalk</em>. <yourbiztalkservicename>.BizTalk.Windows.NET. Um domínio personalizado também pode ser inserido. Por exemplo, se seu domínio for <em>contoso</em>, insira: <br/><br/>
    <em>MyCompany</em>.contoso.com<br/>
    <em>MyCompanyMyApplication</em>.contoso.com<br/>
    <em>MyApplication</em>.contoso.com<br/>
    <em>YourBizTalkServiceName</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Selecione a seta Avançar hello.
5. Digite hello armazenamento e as configurações de banco de dados:  <table border="1">
    <tr>
    <td><strong>Conta de armazenamento de Monitoramento/Arquivamento</strong></td>
    <td>Selecione uma conta de armazenamento existente ou crie uma nova. <br/><br/>Se você criar uma nova conta de armazenamento, digite Olá <strong>nome da conta de armazenamento</strong>.</td>
    </tr>
    <tr>
    <td><strong>Acompanhamento de banco de dados</strong></td>
    <td>Se você usar um banco de dados SQL do Azure, não poderá ser usado por outro Serviço do BizTalk. É necessário o nome de logon de saudação e a senha inserida quando esse servidor de banco de dados do SQL Azure foi criada.<br/><br/><strong>Dica</strong> criar banco de dados de rastreamento de saudação e conta de armazenamento de monitoramento/arquivamento em Olá mesma região como Olá BizTalk Service.</td>
    </tr>
    </table>
Selecione a seta Avançar hello.
6. Insira as configurações de banco de dados de saudação:  <table border="1">
    <tr>
    <td><strong>Nome</strong></td>
    <td>Disponível quando <strong>criar uma nova instância de banco de dados SQL</strong> está selecionado na tela anterior hello.
    <br/><br/>
Insira um toobe de nome de banco de dados SQL usado pelo seu BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Servidor</strong></td>
    <td>Disponível quando <strong>criar uma nova instância de banco de dados SQL</strong> está selecionado na tela anterior hello.
    <br/><br/>
Selecione um Servidor de Banco de Dados SQL ou crie um novo servidor de Banco de Dados SQL.</td>
    </tr>
    <tr>
    <td><strong>Nome de logon do servidor</strong></td>
    <td>Digite o nome de usuário de logon de saudação.</td>
    </tr>
    <tr>
    <td><strong>Senha de logon do servidor</strong></td>
    <td>Insira a senha de logon de saudação.</td>
    </tr>
    <tr>
    <td><strong>Região</strong></td>
    <td>Disponível quando a opção <strong>Criar uma nova instância do Banco de Dados SQL</strong> é selecionada. Selecione Olá região geográfica toohost seu banco de dados SQL.</td>
    </tr>
    </table>

Selecione Olá marca de seleção toocomplete Olá assistente. Olá progresso ícone será exibido:  
![O ícone de progresso é exibido após a conclusão][ProgressComplete]

Ao concluir, Olá serviço BizTalk do Azure é criado e está pronto para seus aplicativos. as configurações padrão de saudação são suficientes. Se quiser que as configurações padrão de saudação toochange, selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione o BizTalk Service. Configurações adicionais são exibidas em Olá [guias painel, monitorar e escala](biztalk-dashboard-monitor-scale-tabs.md) na parte superior da saudação.

Dependendo do estado de saudação do hello BizTalk Service, existem algumas operações que não podem ser concluídas. Para obter uma lista dessas operações, vá muito[gráfico de estado dos serviços do BizTalk](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Etapas pós-provisionamento
* [Instalar o certificado de saudação em um computador local](#InstallCert)
* [Adicionar um certificado pronto para produção](#AddCert)
* [Obter o namespace do Access Control Olá](#ACS)

#### <a name="InstallCert"></a>Instalar o certificado de saudação em um computador local
Como parte do provisionamento do Serviço do BizTalk, um certificado autoassinado é criado e associado com a assinatura do seu serviço do BizTalk. Você deve baixar o certificado e instalá-lo em computadores em que você implante aplicativos do BizTalk Service ou envia mensagens tooa ponto de extremidade do BizTalk Service.

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione sua assinatura do BizTalk Service.
3. Selecione Olá **painel** guia.
4. Selecione **Baixar Certificado SSL**:  
   ![Modificar certificado SSL][QuickGlance]
5. Clique duas vezes no certificado hello e execute através do certificado de Olá Olá Assistente tooinstall. Verifique se você instalou o certificado de saudação sob Olá **autoridades de certificação raiz confiáveis** armazenar.

#### <a name="AddCert"></a>Adicionar um certificado pronto para produção
certificado autoassinado Olá que é criado automaticamente quando a criação de Serviços BizTalk é destinado ao uso em ambientes de desenvolvimento somente. Para cenários de produção, substitua-o por um certificado pronto para produção.

1. Em Olá **painel** guia, selecione **certificado de SSL da atualização**.
2. Procurar o certificado SSL privado tooyour (*CertificateName*. pfx) que inclui o nome do BizTalk Service, digite a senha de saudação e clique em marca de seleção de saudação.

#### <a name="ACS"></a>Obter o namespace do Access Control Olá
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione o BizTalk Service.
3. Na barra de tarefas hello, selecione **informações de Conexão**:  
   ![Selecionar Informações de conexão][ACSConnectInfo]
4. Copie os valores de controle de acesso de saudação.

Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso. Olá namespace de controle de acesso é automaticamente criado para o BizTalk Service.

valores de controle de acesso de saudação podem ser usados com qualquer aplicativo. Quando os Serviços BizTalk do Azure é criado, esse namespace de controle de acesso controla autenticação Olá com a implantação do BizTalk Service. Se você quiser toochange Olá assinatura ou gerenciar namespace hello, selecione **do ACTIVE DIRECTORY** Olá painel de navegação esquerdo e, em seguida, selecione seu namespace. barra de tarefas Olá lista as opções.

Clicando em **gerenciar** abre Olá Portal de gerenciamento de controle de acesso. No Portal de gerenciamento de controle de acesso do hello, Olá usa o BizTalk Service **identidades de serviço**:  
![Identidades de serviço do ACS no Portal de gerenciamento de controle de acesso de saudação][ACSServiceIdentities]

Olá identidade de serviço de controle de acesso é um conjunto de credenciais que permitem que aplicativos ou clientes tooauthenticate diretamente com o controle de acesso e receber um token.

> [!IMPORTANT]
> Olá BizTalk Service usa **proprietário** para identidade de serviço padrão hello e hello **senha** valor. Se você usar o valor de chave simétrica de saudação em vez da saudação valor da senha, hello seguinte erro poderá ocorrer.<br/><br/>*Não foi possível conectar a conta de serviço de gerenciamento de controle de acesso de toohello com hello especificado credenciais*
> 
> 

[Gerenciando o namespace de seu ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) lista algumas diretrizes e recomendações.

## <a name="requirements-explained"></a>Requisitos explicados
Esses requisitos não se aplicam a toohello edição gratuita.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>O que você precisa</strong></td>
        <td><strong>Por que você precisa disto</strong></td>
</tr>
<tr>
<td>Assinatura do Azure</td>
<td>assinatura de saudação determina quem pode entrar toohello portal do Azure. proprietário de conta Olá cria a assinatura de saudação em <a HREF="https://account.windowsazure.com/Subscriptions"> assinaturas do Azure</a>.
<br/><br/>
Olá conta do Azure pode ter várias assinaturas e pode ser gerenciada por qualquer pessoa que é permitido. Por exemplo, o proprietário de conta do Azure cria uma assinatura chamada <em>BizTalkServiceSubscription</em> e fornece Olá administradores do BizTalk dentro da sua empresa (por exemplo, ContosoBTSAdmins@live.com) toothis assinatura de acesso. Nesse cenário, administradores do BizTalk Olá entrar toohello portal do Azure e ter serviços completos de administrador direitos tooall Olá hospedado na assinatura de hello, incluindo Serviços BizTalk do Azure. Administradores do BizTalk Olá não são proprietários da conta do Azure de saudação e, portanto, não tem acesso tooany as informações de cobrança.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gerenciar assinaturas e contas de armazenamento no portal do Azure de saudação</a> fornece mais informações.
</td>
</tr>
<tr>
<td>Banco de Dados SQL do Azure</td>
<td>Armazena Olá tabelas, exibições e procedimentos armazenados usados pelo Olá BizTalk Service, incluindo dados de controle de saudação.
<br/><br/>
Ao criar um Serviço BizTalk, você pode usar um SQL Server do Azure ou um Banco de Dados SQL do Azure ou criar automaticamente um novo servidor ou banco de dados.
<br/><br/>
Olá escala de banco de dados SQL é configurado automaticamente. Normalmente, a escala do saudação padrão é suficiente para um BizTalk Service. Escala de saudação alteração afeta o preço. Confira <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Contas e faturamento no banco de dados SQL do Azure</a>
<br/><br/>
<strong>Observações</strong>
<br/>
<ul>
<li> Quando você criar um novo SQL Server e Banco de Dados do Azure, os Serviços do Azure são habilitados automaticamente. Olá BizTalk Service requer os serviços do Azure ser habilitado.</li>
<li>Se você criar um novo banco de dados SQL em um servidor existente do SQL Azure, Olá regras de firewall do hello Server não são alterados. Como resultado, é possível de que outros serviços do Azure não são permitidos para bancos de dados do servidor de acesso toohello.</li>
</ul>
</td>
</tr>
<tr>
<td>Namespace do Controle de Acesso do Azure</td>
<td>Autenticados com os Serviços do BizTalk do Azure. Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso. Quando você cria um BizTalk Service, Olá namespace de controle de acesso é criado automaticamente.</td>
</tr>

<tr>
<td>Conta de Armazenamento do Azure</td>
<td>Fornece acesso tootables, blobs e filas usadas pelo seu seguinte de saudação do BizTalk Service toosave:

<ul>
<li>Os arquivos de log que Olá monitor BizTalk Service. Olá monitoramento saída também é exibida no hello **monitoramento** guia Olá portal do Azure.</li>
<li>Ao criar um X12 ou AS2 acordo entre parceiros, você pode habilitar as propriedades de mensagem do hello arquivamento recurso toostore. Esses dados são salvos no hello conta de armazenamento.</li>
</ul>
<br/>
Ao criar um Serviço BizTalk, você pode usar uma conta de Armazenamento existente ou criar automaticamente uma nova conta de Armazenamento.
<br/><br/>
configurações de armazenamento saudação padrão são suficientes para um BizTalk Service.
<br/><br/>
Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente. Essas chaves controlam acesso tooyour conta de armazenamento. Olá BizTalk Service usa automaticamente Olá chave primária.
<br/><br/>
Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Armazenamento</a> para obter mais informações.
</td>
</tr>

<tr>
<td>Certificado SSL privado</td>
<td>
Quando um Serviço do BizTalk do Azure for criado, uma URL HTTPS que inclui o nome do seu Serviço do BizTalk também é criado. Essa URL é toouse configurada automaticamente um certificado autoassinado somente para desenvolvimento. Para produção, você necessita um certificado SSL privado.
<br/><br/>
<strong>Informações importantes sobre o Certificado SSL</strong>

<ul>
<li>Data de validade do certificado Olá deve ser inferior a 5 anos.</li>
<li>Todos os certificados privados exigem uma senha. Saiba essa senha e, como uma prática recomendada, compartilhe essa senha com seus administradores.</li>
<li>Os certificados autoassinados são usados em um ambientes de desenvolvimento/teste. Ao usar certificados autoassinados, importar o repositório de certificados pessoais do hello certificado tooyour e Olá repositório de certificados de autoridades de certificação raiz confiáveis.</li>
</ul>
<br/>Ao enviar a autoridade de certificação tooyour do solicitação de certificado de produção hello, dar Olá propriedades do certificado a seguir:
<br/>

<ul>
<li><strong>Uso avançado de chave</strong>: no mínimo, os Serviços BizTalk do Azure exigem a Autenticação de Servidor.</li>
<li><strong>Nome comum</strong>: insira o nome de domínio totalmente qualificado (FQDN) Olá de sua URL do serviço BizTalk do Azure. Veja <a HREF="#CreateService">Criar um Serviço BizTalk</a> neste artigo.</li>
</ul>
<br/>
Pode ser adicionado a um certificado novo ou diferente depois Olá BizTalk Service é criado.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>Conexões Híbridas
Quando você cria um serviço de BizTalk do Azure, Olá **conexões híbridas** guia está disponível:

![Guia de Conexões Híbridas][HybridConnectionTab]

Conexões híbridas são usada tooconnect do Azure site ou serviço móvel do Azure tooany local recursos que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP, os serviços móveis e a maioria dos serviços da Web personalizados.  Conexões híbridas e hello serviço de adaptador do BizTalk são diferentes. Olá serviço de adaptador BizTalk é usado tooconnect Serviços BizTalk do Azure tooan no sistema local da linha de negócios (LOB).

 Consulte [conexões híbridas](integration-hybrid-connection-overview.md) toolearn mais, incluindo a criação e gerenciamento de conexões híbridas.

## <a name="next-steps"></a>Próximas etapas
Agora que um BizTalk Service foi criada, você se familiarizar com hello diferente [Serviços BizTalk: guias painel, monitorar e escala](biztalk-dashboard-monitor-scale-tabs.md). Seu Serviço BizTalk está pronto para os seus aplicativos. toostart criação de aplicativos, vá muito[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Consulte também
* [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md)<br/>
* [Serviços BizTalk: gráfico de estado](biztalk-service-state-chart.md)<br/>
* [Serviços BizTalk: backup e restauração](biztalk-backup-restore.md)<br/>
* [Serviços BizTalk: limitação](biztalk-throttling-thresholds.md)<br/>
* [Serviços BizTalk: nome e chave do emissor](biztalk-issuer-name-issuer-key.md)<br/>
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Conexões híbridas](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
