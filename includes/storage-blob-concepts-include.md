## <a name="what-is-blob-storage"></a>O que é Armazenamento de Blob?
Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados de objeto não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Você pode usar dados de tooexpose de armazenamento de Blob publicamente toohello mundo ou toostore dados de aplicativo em particular.

Usos comuns de armazenamento de Blob incluem:

* Serviço de imagens e documentos diretamente tooa navegador
* Armazenar arquivos para acesso distribuído
* Transmitir por streaming áudio e vídeo
* Armazenamento de dados de backup e restauração, recuperação de desastres e arquivamento
* Armazenando dados para análise por um serviço local ou hospedado do Azure

## <a name="blob-service-concepts"></a>Conceitos do Serviço Blob
Olá serviço Blob contém Olá componentes a seguir:

![Arquitetura de blob](./media/storage-blob-concepts-include/blob1.png)

* **Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Essa conta de armazenamento pode ser uma **conta de armazenamento** de uso geral ou uma **conta de Armazenamento de Blobs**, que é especializada em armazenar objetos/blobs. Consulte [Sobre as contas de armazenamento do Azure](../articles/storage/common/storage-create-storage-account.md) para obter mais informações.
* **Contêiner:** um contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem ter um contêiner. Uma conta pode conter um número ilimitado de contêineres. Um contêiner pode armazenar um número ilimitado de blobs. Observe que esse nome de contêiner Olá deve estar em minúscula.
* **Blob:** um arquivo de qualquer tipo e tamanho. O armazenamento do Azure oferece três tipos de blobs: blob de blocos, blob de páginas e blob de anexo.
  
    *Blobs de blocos* são ideais para armazenar arquivos de texto ou binários, como documentos e arquivos de mídia. *Blobs de acréscimo* são semelhantes blobs de tooblock em que eles são compostos de blocos, mas eles são otimizados para operações de acréscimo, para que sejam úteis para cenários de registro em log. Um blob de bloco único pode conter o too50, 000 blocos de too100 MB cada, para um tamanho total de um pouco mais de 4,75 TB (100 MB X 50.000). Um blob de acréscimo único pode conter o too50, 000 blocos de too4 MB cada, para um tamanho total de um pouco mais de 195 GB (4 MB X 50.000).
  
    *Blobs de página* pode ser até too1 TB de tamanho e são mais eficientes para operações de leitura/gravação frequentes. Máquinas virtuais do Azure usam blobs de páginas como sistema operacional e discos de dados.
  
    Para obter detalhes sobre como nomear contêineres e blobs, confira [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

