Ao adicionar discos de dados tooa VM do Linux, você poderá encontrar erros se um disco não existe no LUN 0. Se você estiver adicionando um disco manualmente usando Olá `azure vm disk attach-new` comando e especificar um LUN (`--lun`) em vez de permitir Olá toodetermine da plataforma Windows Azure Olá LUN apropriado, lembre-se que um disco já existe / existirão no LUN 0. 

Considere Olá seguinte exemplo mostra um trecho de código de saída de saudação do `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

discos de dados Olá dois existem na LUN 0 e 1 de LUN (primeira coluna Olá Olá `lsscsi` detalhes de saída `[host:channel:target:lun]`). Ambos os discos devem ser accessbile de dentro de saudação VM. Se manualmente especificadas Olá primeiro disco toobe adicionado no LUN 1 e o segundo disco Olá em LUN 2, você poderá consultar não discos Olá corretamente a partir de sua VM.

> [!NOTE]
> Hello Azure `host` valor seja 5 nestes exemplos, mas isso pode variar dependendo do tipo de saudação de armazenamento que você selecionar.
> 
> 

Esse comportamento de disco não é um problema do Azure, mas a maneira Olá quais Olá Linux kernel segue as especificações de SCSI hello. Quando o kernel do Linux Olá examina o barramento SCSI de saudação para dispositivos conectados, um dispositivo deve ser encontrado em LUN 0 para que Olá sistema toocontinue verificação de dispositivos adicionais. Assim:

* Examine a saída de saudação do `lsscsi` depois de adicionar um tooverify de disco de dados que você tenha um disco na LUN 0.
* Se o disco não aparecer corretamente para a VM, verifique se existe um disco no LUN 0.

