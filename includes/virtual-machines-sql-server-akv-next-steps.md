## <a name="next-steps"></a>Próximas etapas

Depois de habilitar a integração do Cofre da Chave do Azure, você poderá habilitar a criptografia do SQL Server em sua VM do SQL. Primeiro, você precisará toocreate uma chave assimétrica dentro de seu Cofre de chaves e uma chave simétrica no SQL Server na sua VM. Em seguida, será possível tooexecute T-SQL instruções tooenable a criptografia para seus bancos de dados e backups.

Há várias formas de criptografia das quais você pode tirar proveito:

* [Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Backups criptografados](https://msdn.microsoft.com/library/dn449489.aspx)
* [Criptografia de nível de coluna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Olá scripts Transact-SQL a seguir fornecem exemplos para cada uma dessas áreas.

### <a name="prerequisites-for-examples"></a>Pré-requisitos para exemplos

Cada exemplo é baseado em pré-requisitos Olá dois: uma chave assimétrica do Cofre de chaves chamado **CONTOSO_KEY** e uma credencial criados pelo recurso de integração de AKV Olá chamado **Azure_EKM_TDE_cred**. Olá, comandos Transact-SQL a seguir configurar esses pré-requisitos para executar os exemplos de saudação.

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

### <a name="transparent-data-encryption-tde"></a>Transparent Data Encryption (TDE)

1. Criar um toobe de logon do SQL Server usado pelo Olá mecanismo de banco de dados para TDE e adicione Olá credencial tooit.

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

1. Crie chave de criptografia de banco de dados de saudação que será usado para TDE.

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

### <a name="encrypted-backups"></a>Backups criptografados

1. Crie um toobe de logon do SQL Server usado pelo Olá mecanismo de banco de dados para criptografar backups e adicione Olá credencial tooit.

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

1. Banco de dados de backup Olá especificando a criptografia com a chave assimétrica Olá armazenada no cofre de chaves hello.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Criptografia de nível de coluna (CLE)

Esse script cria uma chave simétrica protegida pela chave assimétrica no cofre de chaves de saudação do hello e, em seguida, usa dados tooencrypt chave simétrica de saudação no banco de dados de saudação.

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

## <a name="additional-resources"></a>Recursos adicionais

Para obter mais informações sobre como toouse esses recursos de criptografia, consulte [usando EKM com recursos de criptografia do SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Observe que Olá etapas neste artigo presumem que você já ter o SQL Server em execução em uma máquina virtual do Azure. Se não estiver, confira [Provisionar uma máquina virtual do SQL Server no Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Para obter orientação sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral sobre SQL Server em máquinas virtuais do Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
