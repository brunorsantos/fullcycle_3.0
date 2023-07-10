Idempotencia é muito importante no terraform, para evitar a criacao de recursos em duplicidade

O codigo do Terraform é de forma declarativa, isto é mostrando o que é desejado como resultado final. Caso esse resultado final seja o mesmo que o já existente ele nao fará nada.

## Terraform x Ansible

Terraform é melhor para criar estruturas (novo cluster, criar um recurso na nuvem) enquando o ansible é melhor para gerenciar configurações (liberar ips, redirecionamento de portas para todas as maquinas, etc)

## Estado

O terraform grava um arquivo de estado, para comparar ao executar novamente. Caso esse arquivo nao exista, sera um problema para criar.

É possivel configurar um arquivo online (bucket s3) para o trabalho em conjunto.
