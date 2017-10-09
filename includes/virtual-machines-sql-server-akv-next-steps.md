## <a name="next-steps"></a><span data-ttu-id="33528-101">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33528-101">Next steps</span></span>

<span data-ttu-id="33528-102">Depois de habilitar a integração do Cofre da Chave do Azure, você poderá habilitar a criptografia do SQL Server em sua VM do SQL.</span><span class="sxs-lookup"><span data-stu-id="33528-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="33528-103">Primeiro, você precisará toocreate uma chave assimétrica dentro de seu Cofre de chaves e uma chave simétrica no SQL Server na sua VM.</span><span class="sxs-lookup"><span data-stu-id="33528-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="33528-104">Em seguida, será possível tooexecute T-SQL instruções tooenable a criptografia para seus bancos de dados e backups.</span><span class="sxs-lookup"><span data-stu-id="33528-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="33528-105">Há várias formas de criptografia das quais você pode tirar proveito:</span><span class="sxs-lookup"><span data-stu-id="33528-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="33528-106">Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="33528-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="33528-107">Backups criptografados</span><span class="sxs-lookup"><span data-stu-id="33528-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="33528-108">Criptografia de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="33528-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="33528-109">Olá scripts Transact-SQL a seguir fornecem exemplos para cada uma dessas áreas.</span><span class="sxs-lookup"><span data-stu-id="33528-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="33528-110">Pré-requisitos para exemplos</span><span class="sxs-lookup"><span data-stu-id="33528-110">Prerequisites for examples</span></span>

<span data-ttu-id="33528-111">Cada exemplo é baseado em pré-requisitos Olá dois: uma chave assimétrica do Cofre de chaves chamado **CONTOSO_KEY** e uma credencial criados pelo recurso de integração de AKV Olá chamado **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="33528-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="33528-112">Olá, comandos Transact-SQL a seguir configurar esses pré-requisitos para executar os exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="33528-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="33528-113">Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="33528-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="33528-114">Criar um toobe de logon do SQL Server usado pelo Olá mecanismo de banco de dados para TDE e adicione Olá credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="33528-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="33528-115">Crie chave de criptografia de banco de dados de saudação que será usado para TDE.</span><span class="sxs-lookup"><span data-stu-id="33528-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="33528-116">Backups criptografados</span><span class="sxs-lookup"><span data-stu-id="33528-116">Encrypted backups</span></span>

1. <span data-ttu-id="33528-117">Crie um toobe de logon do SQL Server usado pelo Olá mecanismo de banco de dados para criptografar backups e adicione Olá credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="33528-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="33528-118">Banco de dados de backup Olá especificando a criptografia com a chave assimétrica Olá armazenada no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="33528-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="33528-119">Criptografia de nível de coluna (CLE)</span><span class="sxs-lookup"><span data-stu-id="33528-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="33528-120">Esse script cria uma chave simétrica protegida pela chave assimétrica no cofre de chaves de saudação do hello e, em seguida, usa dados tooencrypt chave simétrica de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="33528-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="33528-121">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="33528-121">Additional resources</span></span>

<span data-ttu-id="33528-122">Para obter mais informações sobre como toouse esses recursos de criptografia, consulte [usando EKM com recursos de criptografia do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="33528-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="33528-123">Observe que Olá etapas neste artigo presumem que você já ter o SQL Server em execução em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="33528-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="33528-124">Se não estiver, confira [Provisionar uma máquina virtual do SQL Server no Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="33528-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="33528-125">Para obter orientação sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral sobre SQL Server em máquinas virtuais do Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33528-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
