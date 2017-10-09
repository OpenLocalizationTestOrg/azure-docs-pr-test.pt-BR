
* conversão Olá exige uma reinicialização do hello VM, portanto agendar migração Olá das suas máquinas virtuais durante uma janela de manutenção já existente. 

* Olá conversão não é reversível. 

* Ser-se de conversão de saudação do tootest. Migre uma máquina virtual de teste antes de executar a migração de saudação em produção.

* Durante a conversão de saudação, você desalocar Olá VM. Olá VM recebe um novo endereço IP quando é iniciado após a conversão de saudação. Se necessário, você pode [atribuir um endereço IP estático](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello VM.

* Olá VHDs originais e conta de armazenamento Olá usado pelo Olá VM antes da conversão não são excluídos. Eles continuam tooincur encargos. tooavoid sendo cobrado por esses artefatos, exclua os blobs VHD originais Olá depois de verificar que a conversão de saudação foi concluída.
