## <a name="next-steps"></a><span data-ttu-id="76460-101">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76460-101">Next steps</span></span>

<span data-ttu-id="76460-102">Depois de habilitar a integração do Cofre da Chave do Azure, você poderá habilitar a criptografia do SQL Server em sua VM do SQL.</span><span class="sxs-lookup"><span data-stu-id="76460-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="76460-103">Primeiro, você precisará criar uma chave assimétrica dentro de seu cofre de chave e uma chave simétrica no SQL Server em sua VM.</span><span class="sxs-lookup"><span data-stu-id="76460-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="76460-104">Em seguida, você poderá executar instruções T-SQL para habilitar a criptografia para seus bancos de dados e backups.</span><span class="sxs-lookup"><span data-stu-id="76460-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="76460-105">Há várias formas de criptografia das quais você pode tirar proveito:</span><span class="sxs-lookup"><span data-stu-id="76460-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="76460-106">Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="76460-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="76460-107">Backups criptografados</span><span class="sxs-lookup"><span data-stu-id="76460-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="76460-108">Criptografia de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="76460-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="76460-109">Os scripts Transact-SQL a seguir fornecem exemplos para cada uma dessas áreas.</span><span class="sxs-lookup"><span data-stu-id="76460-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="76460-110">Pré-requisitos para exemplos</span><span class="sxs-lookup"><span data-stu-id="76460-110">Prerequisites for examples</span></span>

<span data-ttu-id="76460-111">Cada exemplo tem base em dois pré-requisitos: uma chave assimétrica de seu cofre de chaves chamado **CONTOSO_KEY** e uma credencial criada pelo recurso de Integração de AKV chamada **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="76460-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="76460-112">Os comandos Transact-SQL a seguir configuram os pré-requisitos para executar os exemplos.</span><span class="sxs-lookup"><span data-stu-id="76460-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="76460-113">Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="76460-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="76460-114">Crie um logon do SQL Server que será usado pelo Mecanismo de banco de dados para TDE e adicione a credencial a ele.</span><span class="sxs-lookup"><span data-stu-id="76460-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="76460-115">Crie a chave de criptografia do banco de dados que será usada para a TDE.</span><span class="sxs-lookup"><span data-stu-id="76460-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="76460-116">Backups criptografados</span><span class="sxs-lookup"><span data-stu-id="76460-116">Encrypted backups</span></span>

1. <span data-ttu-id="76460-117">Crie um logon do SQL Server que será usado pelo Mecanismo de banco de dados para criptografia de backups e adicione a credencial a ele.</span><span class="sxs-lookup"><span data-stu-id="76460-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="76460-118">Faça o backup do banco de dados especificando a criptografia com a chave assimétrica armazenada no cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="76460-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="76460-119">Criptografia de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="76460-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="76460-120">Esse script cria uma chave simétrica protegida pela chave assimétrica no cofre de chave e usa a chave simétrica para criptografar dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76460-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="76460-121">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="76460-121">Additional resources</span></span>

<span data-ttu-id="76460-122">Para saber mais sobre como usar esses recursos de criptografia, consulte [Usando EKM com recursos de criptografia do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="76460-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="76460-123">Observe que as etapas neste artigo presumem que o SQL Server já está em execução em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="76460-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="76460-124">Se não estiver, confira [Provisionar uma máquina virtual do SQL Server no Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="76460-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="76460-125">Para obter orientação sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral sobre SQL Server em máquinas virtuais do Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76460-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>