---
title: "aaaDeploy um serviço de divisão mesclagem | Microsoft Docs"
description: "Divisão e mesclagem com ferramenta de banco de dados elástico"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Implantar um serviço de divisão e mesclagem
ferramenta de mesclagem de divisão de saudação permite mover dados entre bancos de dados fragmentados. Veja [Mover dados entre bancos de dados na nuvem escalados horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Baixe os pacotes de divisão mesclagem Olá
1. Baixar a versão mais recente de NuGet saudação do [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Abra um prompt de comando e navegue toohello diretório onde você baixou o nuget.exe. download de saudação inclui commmands do PowerShell.
3. Baixe o pacote de mesclagem a divisão mais recente do hello no diretório atual de saudação com hello comando abaixo:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

Olá arquivos são colocados em um diretório chamado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** onde *x.x.xxx.x* reflete o número de versão de saudação. Localizar arquivos de serviço de divisão de mesclagem de Olá no hello **content\splitmerge\service** subdiretório e Olá scripts do PowerShell de divisão de mesclagem (e DLLs de cliente necessárias) em Olá **content\splitmerge\powershell** subdiretório.

## <a name="prerequisites"></a>Pré-requisitos
1. Crie um banco de dados do banco de dados de SQL do Azure que será usado como banco de dados de status de divisão mesclagem Olá. Vá toohello [portal do Azure](https://portal.azure.com). Crie um novo **banco de dados SQL**. Dê um nome de banco de dados de saudação e criar um novo administrador e uma senha. Ser-se de nome de saudação do toorecord e a senha para uso posterior.
2. Certifique-se de que o servidor de banco de dados de SQL do Azure permite que serviços do Azure tooconnect tooit. No portal de saudação em hello **as configurações do Firewall**, certifique-se de que Olá **permitir acesso a serviços tooAzure** configuração está definida muito**em**. Clique em hello "Salvar" ícone.
   
   ![Serviços permitidos][1]
3. Crie uma conta de Armazenamento do Azure que será usada para a saída de diagnóstico. Vá toohello Portal do Azure. Na barra de saudação à esquerda, clique em **novo**, clique em **dados + armazenamento**, em seguida, **armazenamento**.
4. Crie um Serviço de nuvem do Azure que conterá o seu serviço de Divisão-Mesclagem.  Vá toohello Portal do Azure. Na barra de saudação à esquerda, clique em **novo**, em seguida, **de computação**, **serviço de nuvem**, e **criar**. 

## <a name="configure-your-split-merge-service"></a>Configurar o serviço de divisão e mesclagem
### <a name="split-merge-service-configuration"></a>Configuração do serviço de Divisão-Mesclagem
1. Na pasta de saudação onde você baixou assemblies Olá direta de divisão, crie uma cópia da saudação **ServiceConfiguration.Template.cscfg** arquivo enviado junto com o **SplitMergeService.cspkg** e renomeá-lo **ServiceConfiguration**.
2. Abra **ServiceConfiguration** em um editor de texto como o Visual Studio valida entradas, como o formato de saudação de impressões digitais de certificado.
3. Criar um novo banco de dados ou escolha um tooserve existentes do banco de dados como banco de dados de status de saudação para operações de divisão de mesclagem e recuperar Olá cadeia de caracteres de conexão do banco de dados. 
   
   > [!IMPORTANT]
   > Neste momento, o banco de dados de status de saudação deve usar agrupamento latino hello (SQL\_latino1\_geral\_CP1\_CI\_AS). Para obter mais informações, consulte [Nome do agrupamento do Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Com o banco de dados de SQL do Azure, cadeia de caracteres de conexão Olá normalmente é de formulário de saudação:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Insira essa cadeia de caracteres de conexão no arquivo de cscfg Olá em ambos os Olá **SplitMergeWeb** e **SplitMergeWorker** seções de função na configuração de ElasticScaleMetadata hello.
5. Para Olá **SplitMergeWorker** função, digite um armazenamento de tooAzure de cadeia de caracteres de conexão válida para Olá **WorkerRoleSynchronizationStorageAccountConnectionString** configuração.

### <a name="configure-security"></a>Configurar a segurança
Para instruções detalhadas tooconfigure Olá a segurança do serviço de hello, consulte toohello [configuração de segurança de divisão mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md).

Para fins de saudação de uma implantação de teste simples para este tutorial, um conjunto mínimo de configuração etapas serão executadas tooget serviço de saudação em funcionamento. Essas etapas habilitam apenas Olá uma máquina/conta executá-los toocommunicate com o serviço de saudação.

### <a name="create-a-self-signed-certificate"></a>Crie um certificado autoassinado
Criar um novo diretório e de saudação de executar esse diretório usando o comando a seguir um [Prompt de comando do desenvolvedor para o Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) janela:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Você será solicitado para uma chave privada do tooprotect Olá de senha. Digite uma senha forte e confirme-a. Você será solicitado para Olá senha toobe usado mais uma vez depois disso. Clique em **Sim** em Olá final tooimport-toohello repositório de raiz de autoridades de certificação confiável.

### <a name="create-a-pfx-file"></a>Criar um arquivo PFX
Executar Olá após o comando Olá mesma janela onde makecert foi executado; Use Olá mesma senha que você toocreate usado Olá certificado:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Importe o certificado de cliente de saudação no repositório pessoal Olá
1. No Windows Explorer, clique duas vezes em **Mycert.pfx**.
2. Em Olá **Assistente de importação de certificado** selecione **usuário atual** e clique em **próximo**.
3. Verifique o caminho do arquivo hello e clique em **próximo**.
4. Senha do tipo hello, deixe **incluem todas as propriedades estendidas** marcada e clique em **próximo**.
5. Deixe **repositório de certificados automaticamente Olá [...]**  marcada e clique em **próximo**.
6. Clique em **Concluir** e em **OK**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Carregar o serviço de nuvem do hello PFX arquivo toohello
1. Vá toohello [Portal do Azure](https://portal.azure.com).
2. Selecione os **Serviços de nuvem**.
3. Selecione o serviço de nuvem de saudação criado anteriormente para o serviço de divisão/mesclagem hello.
4. Clique em **certificados** no menu superior hello.
5. Clique em **carregar** na barra inferior de saudação.
6. Selecione o arquivo PFX de saudação e digite Olá senha acima.
7. Depois de concluído, copie impressão digital do certificado Olá da nova entrada na lista de saudação de hello.

### <a name="update-hello-service-configuration-file"></a>Atualizar o arquivo de configuração de serviço Olá
Cole a impressão digital do certificado Olá copiado acima em seu atributo/valor de impressão digital Olá dessas configurações.
Olá função de trabalho:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Para função de web hello:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Observe que, para implantações de produção certificados separados devem ser usados para Olá autoridade de certificação para criptografia, Olá certificado de servidor e certificados de cliente. Para obter instruções detalhadas sobre isso, consulte a [Configuração de segurança](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Implantar o serviço
1. Vá toohello [portal do Azure](https://manage.windowsazure.com).
2. Clique em Olá **serviços de nuvem** Olá esquerda e selecione o serviço de nuvem Olá que você criou anteriormente.
3. Clique em **Painel**.
4. Escolha Olá ambiente de preparo, e clique em **carregar uma nova implantação de preparo**.
   
   ![Staging][3]
5. Na caixa de diálogo hello, digite um rótulo de implantação. Para 'Pacote' e 'Configuration', clique em 'Do Local' e escolha Olá **SplitMergeService.cspkg** de arquivo e o arquivo. cscfg configurados anteriormente.
6. Verifique se essa caixa de seleção Olá **implantar mesmo se uma ou mais funções contiverem uma única instância** é verificada.
7. Pressione o botão de escala de saudação na implantação de Olá Olá inferior direita toobegin. Espera que ele tootake toocomplete de alguns minutos.

   ![Carregar][4]

## <a name="troubleshoot-hello-deployment"></a>Solucionar problemas de implantação de saudação
Se sua função web falhar toocome on-line, provavelmente é um problema com a configuração de segurança hello. Verifique que Olá que SSL configurado conforme descrito acima.

Se sua função de trabalho falha toocome online, mas sua função web for bem-sucedida, provavelmente é um problema de conexão de banco de dados de status de toohello que você criou anteriormente.

* Certifique-se de que a cadeia de caracteres de conexão de saudação em seu. cscfg é precisa.
* Verificação de banco de dados e servidor de saudação existem e Olá identificação de usuário e senha estão corretos.
* Para o banco de dados de SQL do Azure, cadeia de caracteres de conexão Olá deve estar Olá formato:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Certifique-se de que esse nome de servidor de saudação não começa com **https://**.
* Certifique-se de que o servidor de banco de dados de SQL do Azure permite que serviços do Azure tooconnect tooit. toodo isso, abra https://manage.windowsazure.com, clique "Bancos de dados SQL" em saudação à esquerda, clique em "Servidores" na parte superior do hello e selecione o servidor. Clique em **configurar** em Olá principais e certifique-se de que Olá **serviços do Azure** configuração é definida muito "Sim". (Consulte os pré-requisitos de saudação seção na parte superior da saudação deste artigo).

## <a name="test-hello-service-deployment"></a>Testar a implantação do serviço Olá
### <a name="connect-with-a-web-browser"></a>Conectar-se com um navegador da Web
Determine o ponto de extremidade de web de saudação do seu serviço de divisão de mesclagem. Você pode encontrá-lo em Olá Portal clássico do Azure por vai toohello **painel** de seu serviço de nuvem e olhando na **URL do Site** Olá direita. Substituir **http://** com **https://** desde que as configurações de segurança de saudação desabilitar ponto de extremidade de saudação HTTP. Página de saudação de carga para esta URL no seu navegador.

### <a name="test-with-powershell-scripts"></a>Testes com scripts do PowerShell
implantação de saudação e seu ambiente podem ser testados executando scripts do PowerShell de exemplo hello incluído.

arquivos de script Hello incluídos são:

1. **SetupSampleSplitMergeEnvironment.ps1** - configura uma camada de dados de teste para Divisão/Mesclagem (consulte a tabela abaixo para uma descrição detalhada)
2. **ExecuteSampleSplitMerge.ps1** -executa operações de teste no teste de saudação da camada de dados (consulte a tabela abaixo para obter a descrição detalhada)
3. **GetMappings.ps1** - nível superior que imprime o estado atual de saudação do mapeamentos de fragmento Olá script de exemplo.
4. **ShardManagement.psm1** -script auxiliar que encapsula Olá ShardManagement API
5. **SqlDatabaseHelpers.psm1** – o script auxiliar para criar e gerenciar bancos de dados SQL
   
   <table style="width:100%">
     <tr>
       <th>Arquivo do PowerShell</th>
       <th>Etapas</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Cria um banco de dados do gerenciador de mapa do fragmento</td>
     </tr>
     <tr>
       <td>2.    Cria 2 bancos de dados do fragmento.
     </tr>
     <tr>
       <td>3.    Cria um mapa do fragmento para esses bancos de dados (exclui quaisquer mapas do fragmento existentes nesses bancos de dados). </td>
     </tr>
     <tr>
       <td>4.    Cria uma tabela de exemplo pequeno em ambos os fragmentos hello e preenche a tabela Olá em um dos fragmentos de saudação.</td>
     </tr>
     <tr>
       <td>5.    Declara hello SchemaInfo para a tabela fragmentada hello.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>Arquivo do PowerShell</th>
       <th>Etapas</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Envia um divisão solicitação toohello divisão mesclagem serviço web front-end, que divide os dados de saudação metade do segundo-fragmento primeiro toohello de fragmento hello.</td>
     </tr>
     <tr>
       <td>2.    Pesquisas Olá web front-end para Olá dividir o status da solicitação e aguarda até que a solicitação de saudação é concluída.</td>
     </tr>
     <tr>
       <td>3.    Envia um mesclagem solicitação toohello divisão mesclagem serviço web front-end, que move dados de saudação do primeiro-fragmento segundo toohello voltar de fragmento hello.</td>
     </tr>
     <tr>
       <td>4.    Olá sondagens web front-end para o status da solicitação de mesclagem hello e aguarda até que a solicitação de saudação é concluída.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Use o PowerShell tooverify sua implantação
1. Abra uma nova janela do PowerShell e navegue toohello diretório onde você baixou o pacote de divisão mesclagem hello e, em seguida, navegue até o diretório de "powershell" hello.
2. Criar um servidor de banco de dados do SQL Azure (ou escolha um servidor existente) onde Gerenciador do mapa de fragmentos hello e fragmentos serão criados.
   
   > [!NOTE]
   > Olá SetupSampleSplitMergeEnvironment.ps1 script cria esses bancos de dados em Olá mesmo servidor pelo script do hello tookeep padrão simple. Isso não é uma restrição de saudação serviço de divisão de mesclagem em si.
   >
   
   Um logon de autenticação do SQL com toohello de acesso de leitura/gravação, que bancos de dados serão necessários para hello toomove dados do serviço de divisão de mesclagem e o mapa de fragmento de saudação de atualização. Como Olá serviço de divisão de mesclagem é executado na nuvem Olá, ele não atualmente suporta autenticação integrada.
   
   Certifique-se de saudação do Azure SQL server está configurada tooallow acesso do endereço IP de saudação da máquina Olá execução desses scripts. Você pode encontrar essa configuração em um servidor do SQL Azure Olá / configuração / endereços IP permitidos.
3. Execute o ambiente de exemplo hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello.
   
   Executar esse script irá apagar os dados de gerenciamento de mapa de fragmento existentes estruturas no banco de dados do fragmento mapa manager hello e fragmentos de saudação. Talvez seja útil toorerun script de saudação se desejar que o mapa do fragmento Olá toore inicializar ou fragmentos.
   
   Linha de comando de exemplo:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Execute Olá Getmappings.ps1 tooview Olá mapeamentos de script que existem atualmente no ambiente de exemplo hello.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Execute Olá ExecuteSampleSplitMerge.ps1 script tooexecute uma operação de divisão (mover dados de saudação metade no segundo-fragmento primeiro toohello de fragmento Olá) e, em seguida, uma operação de mesclagem (movimentação de dados Olá novamente no fragmento primeiro Olá). Se você configurou o SSL e o ponto de extremidade http Olá esquerdo desabilitado, certifique-se de que você use o ponto de extremidade do hello https://.
   
   Linha de comando de exemplo:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Se você receber Olá erro abaixo, provavelmente é um problema com o certificado do ponto de extremidade seu Web. Tente conectar-se o ponto de extremidade de Web toohello com seu navegador favorito e verifique se há um erro de certificado.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Se tiver êxito, saída de hello deve ter a aparência Olá abaixo:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Experimente outros tipos de dados! Todos esses scripts levar um parâmetro - ShardKeyType opcional que permite que o tipo de chave de saudação do toospecify. padrão de saudação é Int32, mas você também pode especificar Int64, Guid ou Binary.

## <a name="create-requests"></a>Criar solicitações
serviço de saudação pode ser usado por meio da interface da web hello ou importando e usando o módulo de PowerShell SplitMerge.psm1 Olá que enviará solicitações por meio da função de web hello.

serviço de saudação pode mover dados em tabelas fragmentadas e tabelas de referência. Uma tabela fragmentada possui uma coluna de chave de fragmentação e tem diferentes dados de linha em cada fragmento. Uma tabela de referência não é fragmentada para que ele contém Olá mesmo linhas de dados em cada fragmento. Tabelas de referência são úteis para dados que não são alterados com frequência e tooJOIN usado com tabelas fragmentadas em consultas.

Em ordem tooperform uma operação de mesclagem de divisão, você deve declarar tabelas fragmentadas hello e tabelas de referência que você deseja toohave movido. Isso é feito com hello **SchemaInfo** API. Esta API está em Olá **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.

1. Para cada tabela fragmentada, crie um **ShardedTableInfo** que descreve o nome do esquema da tabela de saudação do pai do objeto (opcional, padrão é muito "dbo"), Olá nome da tabela e Olá nome da coluna na tabela que contém a chave de fragmentação hello.
2. Para cada tabela de referência, crie uma **ReferenceTableInfo** que descreve o nome do esquema da tabela de saudação do pai do objeto (opcional, padrão é muito "dbo") e o nome da tabela hello.
3. Adicionar Olá acima TableInfo objetos tooa novo **SchemaInfo** objeto.
4. Obter uma referência tooa **ShardMapManager** objeto e chame **GetSchemaInfoCollection**.
5. Adicionar Olá **SchemaInfo** toohello **SchemaInfoCollection**, fornecendo o nome do mapa de fragmentos hello.

Um exemplo disso pode ser visto no hello SetupSampleSplitMergeEnvironment.ps1 script.

Olá serviço de divisão de mesclagem não criar o banco de dados de destino hello (ou o esquema para todas as tabelas no banco de dados de saudação) para você. Eles devem ser pré-criados antes de enviar uma solicitação de serviço toohello.

## <a name="troubleshooting"></a>Solucionar problemas
Você pode ver Olá abaixo mensagem ao executar scripts do powershell de exemplo hello:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Esse erro significa que o certificado SSL não está corretamente configurado. Siga as instruções de saudação na seção 'Conectar-se com um navegador da web'.

Se não for possível enviar solicitações, você verá isso:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

Nesse caso, verifique o arquivo de configuração, na configuração de saudação específico para **WorkerRoleSynchronizationStorageAccountConnectionString**. Esse erro normalmente indica que essa função de trabalho Olá com êxito não foi possível inicializar banco de dados de metadados de saudação no primeiro uso. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

