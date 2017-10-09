---
title: 'Always Encrypted: Banco de Dados SQL - Azure Key Vault | Microsoft Docs'
description: "Este artigo mostra como os dados confidenciais no banco de dados SQL com o uso de criptografia de dados toosecure Olá Assistente do sempre criptografado no SQL Server Management Studio. Ele também inclui instruções que lhe mostrará como toostore cada chave de criptografia no cofre de chaves do Azure."
keywords: criptografia de dados, chave de criptografia, criptografia de nuvem
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Always Encrypted: proteger dados confidenciais no Banco de Dados SQL e armazenar suas chaves de criptografia no Cofre de Chaves do Azure

Este artigo mostra como os dados confidenciais em um SQL toosecure banco de dados com a criptografia de dados usando Olá [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) na [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Ele também inclui instruções que lhe mostrará como toostore cada chave de criptografia no cofre de chaves do Azure.

Sempre criptografado é uma nova tecnologia de criptografia de dados no banco de dados do SQL Azure e SQL Server que ajuda a proteger dados confidenciais em repouso no servidor de saudação, durante a movimentação entre cliente e servidor e, enquanto dados saudação estão em uso. Sempre criptografado garante que os dados confidenciais nunca seja exibida como texto sem formatação no sistema de banco de dados de saudação. Depois de configurar a criptografia de dados, somente os aplicativos cliente ou servidores de aplicativos que têm acesso toohello chaves podem acessar dados de texto sem formatação. Para obter informações detalhadas, consulte [Always Encrypted (Mecanismo do Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx).

Depois de configurar Olá toouse de banco de dados sempre criptografado, você criará um aplicativo cliente em c# com Visual Studio toowork com dados criptografado de saudação.

Siga as etapas de saudação neste artigo e saiba como tooset o sempre criptografado para um banco de dados do SQL Azure. Neste artigo, você aprenderá como Olá tooperform seguintes tarefas:

* Assistente de sempre criptografado Olá Use no SSMS toocreate [chaves Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Crie uma [CMK (Chave Mestra da Coluna)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Crie uma [CEK (Chave de Criptografia da Coluna)](https://msdn.microsoft.com/library/mt146372.aspx).
* Criar uma tabela de banco de dados e criptografar colunas.
* Crie um aplicativo que insere, seleciona e exibe dados de colunas Olá criptografado.

## <a name="prerequisites"></a>Pré-requisitos
Para este tutorial, será necessário:

* Uma conta e uma assinatura do Azure. Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versão 13.0.700.242 ou posterior.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou posterior (no computador do cliente de saudação).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [Azure PowerShell](/powershell/azure/overview), versão 1.0 ou posterior. Tipo **(Get-Module azure - ListAvailable). Versão** toosee qual versão do PowerShell que você está executando.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Habilitar o serviço de banco de dados SQL de saudação do cliente aplicativo tooaccess
Você deve habilitar seu serviço de banco de dados do SQL cliente aplicativo tooaccess Olá Configurando a autenticação necessária hello e hello aquisição *ClientId* e *segredo* que você precisará tooauthenticate seu aplicativo no hello código a seguir.

1. Olá abrir [portal clássico do Azure](http://manage.windowsazure.com).
2. Selecione **do Active Directory** e clique em instância do Active Directory Olá que seu aplicativo usará.
3. Clique em **Aplicativos** e, em seguida, clique em **ADICIONAR**.
4. Digite um nome para seu aplicativo (por exemplo: *myClientApp*), selecione **aplicativo WEB**e clique em Olá seta toocontinue.
5. Para Olá **URL de logon** e **URI da ID do aplicativo** você pode digitar uma URL válida (por exemplo, *http://myClientApp*) e continuar.
6. Clique em **CONFIGURAR**.
7. Copie a **ID DO CLIENTE**. (Posteriormente você precisará desse valor no código)
8. Em Olá **chaves** seção, selecione **1 ano** de saudação **selecionar duração** lista suspensa. (Você copiará chave Olá depois de salvar a etapa 13.)
9. Role para baixo e clique em **Adicionar aplicativo**.
10. Deixe **Mostrar** definido muito**Microsoft Apps** e selecione **API de gerenciamento de serviços do Microsoft Azure**. Clique em Olá toocontinue de marca de seleção.
11. Selecione **acessar o gerenciamento de serviços do Azure...**  de saudação **permissões delegadas** lista suspensa.
12. Clique em **SALVAR**.
13. Após Olá salvar for concluída, copie o valor da chave Olá no hello **chaves** seção. (Posteriormente você precisará desse valor no código)

## <a name="create-a-key-vault-toostore-your-keys"></a>Criar um cofre de chaves toostore suas chaves
Agora que o aplicativo cliente está configurado e você tem a ID do cliente, é hora toocreate um cofre de chaves e configurar sua política de acesso para que você e seu aplicativo podem acessar os segredos do cofre da saudação (chaves Always Encrypted Olá). Olá *criar*, *obter*, *lista*, *sinal*, *verificar*, *wrapKey*, e *unwrapKey* permissões são necessárias para criar uma nova chave mestra de coluna e para configurar a criptografia com o SQL Server Management Studio.

Você pode criar rapidamente um cofre de chaves executando Olá script a seguir. Para obter uma explicação detalhada sobre esses cmdlets e obter mais informações sobre como criar e configurar um cofre de chaves, veja [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md).

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>Criar um banco de dados SQL em branco
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Vá muito**novo** > **dados + armazenamento** > **banco de dados SQL**.
3. Crie um banco de dados **Em branco** chamado **Clínica** em um servidor novo ou existente. Para obter instruções detalhadas sobre como toocreate um banco de dados Olá portal do Azure, consulte [seu primeiro banco de dados do SQL Azure](sql-database-get-started-portal.md).
   
    ![Criar um banco de dados vazio](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Você será necessário Olá cadeia de caracteres de conexão mais tarde no tutorial Olá, assim depois de criar o banco de dados Olá, procurar toohello nova clínica banco de dados e copiar Olá conexão cadeia de caracteres. Você pode obter a cadeia de caracteres de conexão Olá a qualquer momento, mas é fácil toocopy no hello portal do Azure.

1. Vá muito**bancos de dados SQL** > **clínica** > **Mostrar cadeias de conexão de banco de dados**.
2. Copie a cadeia de caracteres de conexão de saudação para **ADO.NET**.
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Conectar-se o banco de dados toohello com SSMS
Abra o SSMS e conecte o servidor de toohello com o banco de dados do hello clínica.

1. Abra o SSMS. (Ir muito**conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela se ele não estiver aberto.)
2. Insira o nome do servidor e credenciais. nome do servidor de saudação pode ser encontrada na folha de banco de dados SQL hello e na cadeia de caracteres de conexão Olá copiados anteriormente. Nome de servidor completo do tipo hello, incluindo *t*.
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Se hello **nova regra de Firewall** abre a janela, entrar tooAzure e permitem SSMS criar uma nova regra de firewall para você.

## <a name="create-a-table"></a>Criar uma tabela
Nesta seção, você criará um dados dos pacientes toohold da tabela. Ele não é inicialmente criptografado - você irá configurar a criptografia na próxima seção, Olá.

1. Expanda **Bancos de Dados**.
2. Saudação de atalho **clínica** de banco de dados e clique em **nova consulta**.
3. Saudação de colar Transact-SQL (T-SQL) a seguir na nova janela de consulta hello e **Execute** -lo.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>Criptografar colunas (configurar o Always Encrypted)
SSMS fornece um assistente que ajuda você a configurar facilmente sempre criptografado por configuração Olá chave mestra da coluna, chave de criptografia de coluna e colunas criptografadas para você.

1. Expandaa **Bancos de Dados** > **Clínica** > **Tabelas**.
2. Atalho Olá **pacientes** de tabela e selecione **criptografar colunas** Assistente de sempre criptografado Olá tooopen:
   
    ![Criptografar Colunas](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Assistente de sempre criptografado Hello inclui Olá seções a seguir: **seleção de coluna**, **configuração da chave mestra**, **validação**, e **resumo** .

### <a name="column-selection"></a>Seleção de coluna
Clique em **próximo** em Olá **Introdução** Olá de tooopen página **seleção de coluna** página. Nessa página, você seleciona as colunas que você deseja tooencrypt, [Olá tipo de criptografia e qual chave de criptografia de coluna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Criptografe as informações de **SSN** e **BirthDate** de cada paciente. coluna de SSN Olá usará criptografia determinística, que dá suporte a pesquisas de igualdade, junções e group by. coluna de data de nascimento Olá usará criptografia aleatória, que não oferece suporte a operações.

Saudação de conjunto **tipo de criptografia** coluna Olá SSN muito**determinística** e Olá coluna BirthDate muito**aleatória**. Clique em **Avançar**.

![Criptografar Colunas](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Configuração da Chave Mestra
Olá **configuração da chave mestra** página é onde você configurar a CMK e provedor de repositório de chaves hello selecione onde hello CMK será armazenado. No momento, você pode armazenar uma CMK no repositório de certificados do Windows hello, o Cofre de chaves do Azure ou um módulo de segurança de hardware (HSM).

Este tutorial mostra como toostore as chaves no cofre de chaves do Azure.

1. Selecione **Cofre de Chaves do Azure**.
2. Selecione o Cofre de chave desejado Olá da lista suspensa de saudação.
3. Clique em **Avançar**.

![Configuração da Chave Mestra](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Validação
Você pode criptografar colunas Olá agora ou salvar um toorun de script do PowerShell mais tarde. Para este tutorial, selecione **continuar toofinish agora** e clique em **próximo**.

### <a name="summary"></a>Resumo
Verifique se as configurações de saudação estão corretas e clique em **concluir** toocomplete o programa de instalação de saudação do sempre criptografado.

![Resumo](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Verifique se ações do assistente Olá
Concluído o Assistente de saudação, seu banco de dados está configurado para sempre criptografado. Olá Olá de assistente executado ações a seguir:

* Criação de uma chave mestra de coluna e armazenamento no Cofre de Chaves do Azure.
* Criação de uma chave de criptografia de coluna e armazenamento no Cofre de Chaves do Azure.
* Saudação configurado selecionado colunas para criptografia. tabela de pacientes Olá atualmente não tem dados, mas os dados existentes nas colunas de saudação selecionada agora são criptografados.

Verificar a criação de saudação de chaves Olá no SSMS expandindo **clínica** > **segurança** > **chaves Always Encrypted**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Criar um aplicativo cliente que funciona com dados saudação criptografado
Agora que sempre criptografado estiver configurado, você pode criar um aplicativo que realiza *insere* e *seleciona* em Olá colunas criptografadas.  

> [!IMPORTANT]
> O aplicativo deve usar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos ao passar o servidor de toohello de dados de texto sem formatação com colunas sempre criptografadas. A passagem de valores literais sem usar objetos SqlParameter resultará em uma exceção.
> 
> 

1. Abra o Visual Studio e crie um novo **Aplicativo de Console** do C# (Visual Studio 2015 e anterior) ou **Aplicativo de Console (.NET Framework)** (Visual Studio 2017 e posterior). Verifique se seu projeto está definido muito**do .NET Framework 4.6** ou posterior.
2. Projeto de saudação do nome **AlwaysEncryptedConsoleAKVApp** e clique em **Okey**.
3. Instalar Olá seguintes pacotes do NuGet indo muito**ferramentas** > **NuGet Package Manager** > **Package Manager Console**.

Execute estas duas linhas de código em Olá Package Manager Console.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modificar sua tooenable de cadeia de caracteres de conexão sempre criptografado
Esta seção explica como tooenable sempre criptografados em sua cadeia de conexão do banco de dados.

tooenable sempre criptografado, você precisa Olá tooadd **Column Encryption Setting** conexão de tooyour de palavra-chave da cadeia de caracteres e defini-lo muito**habilitado**.

Você pode definir isso diretamente na cadeia de caracteres de conexão hello, ou pode defini-lo usando [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). aplicativo de exemplo Hello em Olá próxima seção mostra como toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Habilitar o sempre criptografado na cadeia de caracteres de conexão Olá
Adicione Olá cadeia de caracteres de conexão de tooyour palavra-chave a seguir.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Habilitar o Always Encrypted com SqlConnectionStringBuilder
Olá mostrado no código a seguir como tooenable sempre criptografado, definindo [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) muito[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Registrar provedor do Azure Key Vault Olá
Olá código a seguir mostra como tooregister Olá provedor de Cofre de chaves do Azure com o driver do ADO.NET hello.

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>Aplicativo de console de exemplo do Always Encrypted
Este exemplo demonstra como:

* Modifique seu tooenable de cadeia de caracteres de conexão sempre criptografado.
* Registre o Cofre de chaves do Azure como Olá provedor de repositório de chaves do aplicativo.  
* Inserir dados nas colunas de saudação criptografada.
* Selecionar um registro por filtragem para um valor específico em uma coluna criptografada.

Substitua o conteúdo de saudação do **Program.cs** com hello código a seguir. Substitua a cadeia de caracteres de conexão de saudação para a variável de connectionString global Olá na linha de saudação que precede diretamente o método Main de saudação com a cadeia de conexão válida do hello portal do Azure. Essa é Olá alteração só é necessário toomake toothis código.

Execute Olá aplicativo toosee sempre criptografado em ação.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a>Verificar se os dados de saudação foi criptografados
Você pode verificar rapidamente que dados reais de saudação no servidor de saudação são criptografados consultando dados de pacientes saudação com o SSMS (usando sua conexão atual onde **Column Encryption Setting** ainda não foi habilitado).

Execute Olá consulta a seguir no banco de dados de clínica hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Você pode ver que colunas Olá criptografado não contêm nenhum dado de texto sem formatação.

   ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess Olá dados de texto sem formatação, você pode adicionar Olá *Column Encryption Setting = habilitado* conexão de toohello do parâmetro.

1. No SSMS, clique com o botão direito do mouse em seu servidor no **Pesquisador de Objetos** e escolha **Desconectar**.
2. Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela e clique em **opções**.
3. Clique em **Parâmetros Adicionais de Conexão** e digite **Column Encryption Setting=enabled**.
   
    ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Execute Olá consulta a seguir no banco de dados de clínica hello.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Agora você pode ver os dados de texto sem formatação de saudação em colunas criptografada de saudação.

    ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Próximas etapas
Depois de criar um banco de dados que usa o sempre criptografado, você poderá desejar a seguir Olá toodo:

* [Girar e limpar suas chaves](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrar dados que já foram criptografados com o Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>Informações relacionadas
* [Always Encrypted (Desenvolvimento Cliente)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx)
* [Criptografia do SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog do Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

