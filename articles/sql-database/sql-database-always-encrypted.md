---
title: 'Always Encrypted: Banco de Dados SQL do Azure - armazenamento de certificados do Windows | Microsoft Docs'
description: "Este artigo mostra como os dados confidenciais no banco de dados SQL com criptografia de banco de dados usando toosecure Olá Assistente do sempre criptografado no SQL Server Management Studio (SSMS). Ele também mostra como toostore suas chaves de criptografia no certificado do Windows hello armazenam."
keywords: criptografar dados, criptografia do sql, criptografia de banco de dados, dados confidenciais, sempre criptografados
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Sempre criptografado: Proteger dados confidenciais no banco de dados SQL e armazenar as chaves de criptografia no repositório de certificados do Windows hello

Este artigo mostra como os dados confidenciais em um SQL toosecure banco de dados com criptografia de banco de dados usando Olá [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) na [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Ele também mostra como toostore suas chaves de criptografia no certificado do Windows hello armazenam.

Sempre criptografado é uma nova tecnologia de criptografia de dados no banco de dados do SQL Azure e SQL Server que ajuda a proteger dados confidenciais em repouso no servidor de saudação, durante a movimentação entre cliente e servidor e enquanto dados saudação estão em uso, garantir que os dados confidenciais nunca aparece como texto sem formatação no sistema de banco de dados de saudação. Depois de criptografar dados, somente os aplicativos cliente ou servidores de aplicativos que têm acesso toohello chaves podem acessar dados de texto sem formatação. Para obter informações detalhadas, consulte [Always Encrypted (Mecanismo do Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx).

Depois de configurar Olá toouse de banco de dados sempre criptografado, você criará um aplicativo cliente em c# com Visual Studio toowork com dados criptografado de saudação.

Siga etapas Olá toolearn este artigo como tooset o sempre criptografado para um banco de dados do SQL Azure. Neste artigo, você aprenderá como Olá tooperform seguintes tarefas:

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

## <a name="create-a-blank-sql-database"></a>Criar um banco de dados SQL em branco
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **Novo** > **Dados + Armazenamento** > **Banco de Dados SQL**.
3. Crie um banco de dados **Em branco** chamado **Clínica** em um servidor novo ou existente. Para obter instruções detalhadas sobre como criar um banco de dados no hello portal do Azure, consulte [seu primeiro banco de dados do SQL Azure](sql-database-get-started-portal.md).
   
    ![Criar um banco de dados vazio](./media/sql-database-always-encrypted/create-database.png)

Você precisará de cadeia de caracteres de conexão Olá posteriormente no tutorial de saudação. Após a criação do banco de dados hello, vá toohello nova clínica banco de dados e copiar Olá conexão cadeia de caracteres. Você pode obter a cadeia de caracteres de conexão Olá a qualquer momento, mas é fácil toocopy, quando você está no hello portal do Azure.

1. Clique em **Bancos de dados SQL** > **Clínica** > **Mostrar cadeias de conexão do banco de dados**.
2. Copie a cadeia de caracteres de conexão de saudação para **ADO.NET**.
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Conectar-se o banco de dados toohello com SSMS
Abra o SSMS e conecte o servidor de toohello com o banco de dados do hello clínica.

1. Abra o SSMS. (Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela se não estiver aberto).
2. Insira o nome do servidor e credenciais. nome do servidor de saudação pode ser encontrada na folha de banco de dados SQL hello e na cadeia de caracteres de conexão Olá copiados anteriormente. Incluindo do nome completo do servidor do tipo Olá *t*.
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted/ssms-connect.png)

Se hello **nova regra de Firewall** abre a janela, entrar tooAzure e permitem SSMS criar uma nova regra de firewall para você.

## <a name="create-a-table"></a>Criar uma tabela
Nesta seção, você criará um dados dos pacientes toohold da tabela. Isso será uma tabela normal inicialmente – você irá configurar a criptografia na próxima seção, Olá.

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
SSMS fornece um assistente tooeasily configurar o Always Encrypted Configurando Olá CMK, CEK e colunas criptografadas para você.

1. Expandaa **Bancos de Dados** > **Clínica** > **Tabelas**.
2. Atalho Olá **pacientes** de tabela e selecione **criptografar colunas** Assistente de sempre criptografado Olá tooopen:
   
    ![Criptografar Colunas](./media/sql-database-always-encrypted/encrypt-columns.png)

Assistente de sempre criptografado Hello inclui Olá seções a seguir: **seleção de coluna**, **configuração da chave mestra** (CMK) **validação**, e  **Resumo**.

### <a name="column-selection"></a>Seleção de coluna
Clique em **próximo** em Olá **Introdução** Olá de tooopen página **seleção de coluna** página. Nessa página, você seleciona as colunas que você deseja tooencrypt, [Olá tipo de criptografia e qual chave de criptografia de coluna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Criptografe as informações de **SSN** e **BirthDate** de cada paciente. Olá **SSN** coluna usará criptografia determinística, que dá suporte a pesquisas de igualdade, junções e group by. Olá **BirthDate** coluna usará criptografia aleatória, que não oferece suporte a operações.

Saudação de conjunto **tipo de criptografia** para Olá **SSN** coluna muito**determinística** e hello **BirthDate** coluna muito **Aleatória**. Clique em **Avançar**.

![Criptografar Colunas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configuração da Chave Mestra
Olá **configuração da chave mestra** página é onde você configurar a CMK e provedor de repositório de chaves hello selecione onde hello CMK será armazenado. No momento, você pode armazenar uma CMK no repositório de certificados do Windows hello, o Cofre de chaves do Azure ou um módulo de segurança de hardware (HSM). Este tutorial mostra como toostore suas chaves de certificado do Windows hello armazenam.

Verifique se **Repositório de certificados do Windows** está marcado e clique em **Avançar**.

![Configuração da Chave Mestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Validação
Você pode criptografar colunas Olá agora ou salvar um toorun de script do PowerShell mais tarde. Para este tutorial, selecione **continuar toofinish agora** e clique em **próximo**.

### <a name="summary"></a>Resumo
Verifique se as configurações de saudação estão corretas e clique em **concluir** toocomplete o programa de instalação de saudação do sempre criptografado.

![Resumo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Verifique se ações do assistente Olá
Concluído o Assistente de saudação, seu banco de dados está configurado para sempre criptografado. Olá Olá de assistente executado ações a seguir:

* Criou uma CMK.
* Criou uma CEK.
* Saudação configurado selecionado colunas para criptografia. O **pacientes** tabela atualmente não tem dados, mas os dados existentes nas colunas de saudação selecionada agora são criptografados.

Verificar a criação de saudação de chaves Olá no SSMS indo muito**clínica** > **segurança** > **chaves Always Encrypted**. Agora você pode ver Olá novas chaves Olá assistente gerado para você.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Criar um aplicativo cliente que funciona com dados saudação criptografado
Agora que sempre criptografado estiver configurado, você pode criar um aplicativo que realiza *insere* e *seleciona* em Olá colunas criptografadas. toosuccessfully executar o aplicativo de exemplo hello, você deve executá-lo em Olá mesmo computador em que você executou o Assistente de sempre criptografado hello. aplicativo de hello toorun em outro computador, você deve implantar o sempre criptografado certificados toohello computador executando o aplicativo cliente de saudação.  

> [!IMPORTANT]
> O aplicativo deve usar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos ao passar o servidor de toohello de dados de texto sem formatação com colunas sempre criptografadas. A passagem de valores literais sem usar objetos SqlParameter resultará em uma exceção.
> 
> 

1. Abra o Visual Studio e crie um novo aplicativo de console em C#. Verifique se seu projeto está definido muito**do .NET Framework 4.6** ou posterior.
2. Projeto de saudação do nome **AlwaysEncryptedConsoleApp** e clique em **Okey**.

![Novo aplicativo de console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modificar sua tooenable de cadeia de caracteres de conexão sempre criptografado
Esta seção explica como tooenable sempre criptografados em sua cadeia de conexão do banco de dados. Você modificará o aplicativo de console Olá que você acabou de criar na próxima seção hello, "Sempre criptografados exemplo de aplicativo de console."

tooenable sempre criptografado, você precisa Olá tooadd **Column Encryption Setting** conexão de tooyour de palavra-chave da cadeia de caracteres e defini-lo muito**habilitado**.

Você pode definir isso diretamente na cadeia de caracteres de conexão hello, ou pode defini-lo usando um [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). aplicativo de exemplo Hello em Olá próxima seção mostra como toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Isso é Olá alteração somente necessária em um cliente aplicativo específico tooAlways criptografado. Se você tiver um aplicativo existente que armazena sua cadeia de conexão externamente (isto é, em um arquivo de configuração), você pode ser capaz de tooenable sempre criptografado sem alterar nenhum código.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Habilitar o sempre criptografado na cadeia de caracteres de conexão Olá
Adicione Olá cadeia de caracteres de conexão de tooyour palavra-chave a seguir:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Habilitar o Always Encrypted com um SqlConnectionStringBuilder
Olá código a seguir mostra como tooenable sempre criptografado, definindo Olá [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) muito[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Aplicativo de console de exemplo do Always Encrypted
Este exemplo demonstra como:

* Modifique seu tooenable de cadeia de caracteres de conexão sempre criptografado.
* Inserir dados nas colunas de saudação criptografada.
* Selecionar um registro por filtragem para um valor específico em uma coluna criptografada.

Substitua o conteúdo de saudação do **Program.cs** com hello código a seguir. Substitua a cadeia de caracteres de conexão de saudação para a variável de connectionString global Olá na linha de saudação diretamente acima Olá método Main com a cadeia de conexão válida do hello portal do Azure. Essa é Olá alteração só é necessário toomake toothis código.

Execute Olá aplicativo toosee sempre criptografado em ação.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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
Você pode verificar rapidamente que os dados reais de Olá no servidor de saudação é criptografados consultando Olá **pacientes** dados com o SSMS. (Use a conexão atual qual configuração de criptografia de coluna Olá ainda não está habilitada.)

Execute Olá consulta a seguir no banco de dados de clínica hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Você pode ver que colunas Olá criptografado não contêm nenhum dado de texto sem formatação.

   ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess Olá dados de texto sem formatação, você pode adicionar Olá **Column Encryption Setting = habilitado** conexão de toohello do parâmetro.

1. No SSMS, clique com o botão direito do mouse no seu servidor em **Pesquisador de Objetos** e clique em **Desconectar**.
2. Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela e clique **opções**.
3. Clique em **Parâmetros Adicionais de Conexão** e digite **Column Encryption Setting=enabled**.
   
    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Execução hello seguinte consulta no hello **clínica** banco de dados.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Agora você pode ver os dados de texto sem formatação de saudação em colunas criptografada de saudação.

    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Se você se conectar com o SSMS (ou qualquer cliente) em um computador diferente, ele não terá acesso chaves de criptografia de toohello e não será capaz de toodecrypt dados de saudação.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Depois de criar um banco de dados que usa o sempre criptografado, você poderá desejar a seguir Olá toodo:

* Executar esse exemplo de um computador diferente. Ele não terá acesso chaves de criptografia toohello, para que ele não terá dados do access toohello em texto sem formatação e não será executado com êxito.
* [Girar e limpar suas chaves](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrar dados que já foram criptografados com o Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).
* [Implantar o sempre criptografado máquinas de clientes de tooother certificados](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (consulte a seção de "Fazer tooApplications de certificados disponíveis e os usuários" hello).

## <a name="related-information"></a>Informações relacionadas
* [Always Encrypted (desenvolvimento de cliente)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx)
* [Criptografia do SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog do Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

