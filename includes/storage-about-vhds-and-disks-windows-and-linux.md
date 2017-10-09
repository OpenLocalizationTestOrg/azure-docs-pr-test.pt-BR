
## <a name="about-vhds"></a>Sobre VHDs

Olá VHDs usados no Azure são arquivos. vhd armazenados como blobs de página em uma conta de armazenamento padrão ou premium no Azure. Para conhecer mais detalhes sobre os blobs, consulte [Noções Gerais sobre blobs de blocos e blobs de páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Para obter detalhes sobre o armazenamento premium, veja [Armazenamento premium de alto desempenho e máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md).

O Azure suporta Olá formato VHD de disco fixo. dispõe de formato Olá fixada Olá disco lógico linearmente no arquivo hello, portanto esse deslocamento X do disco é armazenado no deslocamento X do blob. Um pequeno rodapé no final de saudação do blob Olá descreve as propriedades de saudação do hello VHD. Geralmente, formato fixo Olá desperdiça espaço porque a maioria dos discos apresenta grandes intervalos não utilizados neles. No entanto, o Azure armazena arquivos. vhd em um formato esparso, para que você obtenha os benefícios de saudação de ambos os hello fixa e discos para discos dinâmicos em Olá mesmo tempo. Para obter mais detalhes, consulte [Introdução aos discos rígidos virtuais](https://technet.microsoft.com/library/dd979539.aspx).

Todos os arquivos. vhd no Azure que você deseja toouse como discos de toocreate uma fonte ou imagens são somente leitura. Quando você cria um disco ou uma imagem, o Azure faz cópias dos Olá arquivos. vhd. Essas cópias podem ser somente leitura ou leitura e gravação, dependendo de como usar o hello VHD.

Quando você cria uma máquina virtual a partir de uma imagem, o Azure cria um disco para a máquina virtual de saudação que é uma cópia do arquivo de VHD de origem hello. tooprotect contra exclusão acidental, o Azure posiciona uma concessão em qualquer arquivo. vhd de origem que usou toocreate uma imagem, um disco do sistema operacional ou um disco de dados.

Antes de excluir um arquivo. vhd de origem, você precisará de concessão de saudação tooremove excluindo Olá disco ou uma imagem. toodelete um arquivo. vhd que está sendo usado por uma máquina virtual como um disco do sistema operacional, você pode excluir máquina virtual de saudação, disco do sistema operacional hello e arquivo de VHD de origem Olá todos de uma vez excluindo a máquina virtual de saudação e excluindo todos os discos associados. No entanto, a exclusão de um arquivo .vhd que é uma origem de um disco de dados requer várias etapas em uma ordem definida. Primeiro desanexar o disco de saudação da máquina virtual de hello, então delete Olá disco e, em seguida, excluir o arquivo. vhd de saudação.

> [!WARNING]
> Se você excluir um arquivo .vhd de origem do armazenamento ou excluir sua conta de armazenamento, a Microsoft não poderá recuperar esses dados para você.
> 

## <a name="types-of-disks"></a>Tipos de discos 

Os Discos do Azure foram projetados para oferecer uma disponibilidade de 99,999%. Os Discos do Azure forneceram consistentemente a durabilidade no nível empresarial, com uma Taxa de Falha Anual de ZERO% líder do setor.

Há dois níveis de desempenho de armazenamento que você pode escolher ao criar seus discos – armazenamento Standard e Premium. Além disso, há dois tipos de discos--não gerenciado e gerenciado – e podem residir em qualquer nível de desempenho.


### <a name="standard-storage"></a>Armazenamento Standard 

Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz. Armazenamento padrão pode ser replicado localmente em um data center ou ser redundante geograficamente com centros de dados primários e secundários. Para saber mais sobre a replicação de armazenamento, veja [Replicação do Armazenamento do Azure](../articles/storage/common/storage-redundancy.md). 

Para saber mais sobre como usar o armazenamento Standard com discos de VM, veja [Armazenamento Standard e discos](../articles/storage/common/storage-standard-storage.md).

### <a name="premium-storage"></a>Armazenamento Premium 

O Armazenamento Premium tem o suporte de SSDs e oferece suporte de disco de alto desempenho e baixa latência para VMs executando cargas de trabalho intensivas para entradas e saídas. Você pode usar o Armazenamento Premium com DS, DSv2, GS, Ls ou FS as VMs do Azure da série. Para saber mais, veja [Armazenamento Premium](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Discos não gerenciados

Discos não gerenciados são tipo tradicional de saudação de discos que foram usados por máquinas virtuais. Com isso, você cria sua própria conta de armazenamento e especifique a conta de armazenamento ao criar o disco de saudação. Ter toomake se você não colocar muitos discos Olá a mesma conta de armazenamento, porque você poderá exceder Olá [metas de escalabilidade](../articles/storage/common/storage-scalability-targets.md) Olá da conta de armazenamento (20.000 IOPS, por exemplo), resultando em Olá VMs sendo limitadas. Com discos não gerenciados, você tem toofigure out como Olá toomaximize o uso de uma ou mais contas tooget Olá melhor desempenho de armazenamento fora de suas VMs.

### <a name="managed-disks"></a>Discos gerenciados 

Gerenciado identificadores de discos armazenamento Olá criação/gerenciamento no plano de fundo de saudação de conta para você e garante que você não tem tooworry sobre limites de escalabilidade Olá Olá da conta de armazenamento. Você simplesmente especifica o tamanho de disco hello e nível de desempenho de saudação (padrão/Premium), e o Azure cria e gerencia disco Olá para você. Mesmo que você adicione discos ou dimensionar Olá VM para cima e para baixo, você não tem tooworry sobre armazenamento hello está sendo usado. 

Você também pode gerenciar suas imagens personalizadas em uma conta de armazenamento por região do Azure e usá-los toocreate centenas de VMs em Olá mesma assinatura. Para obter mais informações sobre discos gerenciados, consulte Olá [visão geral de discos gerenciados](../articles/virtual-machines/windows/managed-disks-overview.md).

É recomendável que você use discos gerenciado do Azure para novas VMs e que você converta os discos de toomanaged de discos não gerenciado anterior, tootake aproveitar Olá muitos recursos disponíveis em discos gerenciado.

### <a name="disk-comparison"></a>Comparação de disco

Olá, a tabela a seguir fornece uma comparação do vs Premium padrão para não gerenciado e gerenciado toohelp de discos que você decidir quais toouse.

|    | Disco Premium do Azure | Disco padrão do Azure |
|--- | ------------------ | ------------------- |
| Tipo de disco | Unidades de Estado Sólido (SSD) | Unidades de Disco Rígido (HDD)  |
| Visão geral  | Suporte a disco com base em SSD de alto desempenho e baixa latência, para máquinas virtuais executando cargas de trabalho com uso intensivo de E/S ou hospedando ambiente de produção de missão crítica | Suporte a disco econômico com base em HDD para cenários de VM de desenvolvimento/teste |
| Cenário  | Cargas de trabalho confidenciais produção e desempenho | Desenvolvimento e teste, não-crítico, <br>Acesso infrequente |
| Tamanho do disco | P4: 32 GB (somente para discos gerenciados)<br>P6: 64 GB (somente para discos gerenciados)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: 2048 GB<br>P50: GB 4095 | Discos não Gerenciados: 1 GB a 4 TB (4095 GB) <br><br>Managed Disks:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>S50: GB 4095| 
| Taxa de Transferência Máxima por Disco | 250 MB/s | 60 MB/s | 
| IOPS Máxima por Disco | 7500 IOPS | 500 IOPS | 

