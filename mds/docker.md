# Docker

**Docker** é uma plataforma de virtualização de containers que permite empacotar, distribuir e executar aplicações de forma isolada e consistente. Diferente das máquinas virtuais tradicionais, containers Docker compartilham o kernel do sistema operacional host, tornando-os mais leves e eficientes.

### Principais benefícios do Docker

- Isolamento: Cada container roda de forma isolada, com seus próprios processos, redes e sistemas de arquivos
- Portabilidade: "Build once, run anywhere" - containers podem ser executados em qualquer ambiente que tenha Docker instalado
- Eficiência: Containers são mais leves que VMs tradicionais e iniciam mais rapidamente
- Escalabilidade: Facilita a criação e gerenciamento de múltiplas instâncias da aplicação

### Dockerfile

**Dockerfile** é um arquivo de texto que contém todas as instruções necessárias para criar uma imagem Docker. 

- A imagem base a ser utilizada
- Comandos a serem executados durante a construção
- Arquivos a serem copiados para dentro da imagem
- Portas a serem expostas
- Comando padrão a ser executado quando o container iniciar
