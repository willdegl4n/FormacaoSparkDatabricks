![image](https://github.com/user-attachments/assets/427f5392-f127-4e32-987c-c3f73ece4230)
## Guia Passo a Passo: Instalando WSL2 e Ubuntu 24.04 LTS via PowerShell

Este guia irá te orientar na instalação do Subsistema Windows para Linux versão 2 (WSL2) e, em seguida, da distribuição Ubuntu 24.04 LTS utilizando o PowerShell no seu computador com Windows.

### ✅ Pré-requisitos

1. **Versão do Windows:** Você precisa do Windows 10 versão 1903 ou superior (Build 18362+), ou do Windows 11, para ter suporte ao WSL2.  
2. **Privilégios de Administrador:** Você deve executar o PowerShell como Administrador. Clique com o botão direito no ícone do PowerShell e selecione “Executar como administrador”.  
3. **Virtualização Ativada:** A virtualização por hardware deve estar ativada na BIOS/UEFI do seu computador.  
   - Caso encontre erros relacionados à virtualização, reinicie seu computador, entre na BIOS/UEFI (DEL, F2, F10 ou F12 durante o boot), e ative opções como:
     - "Virtualization Technology"
     - "VT-x"
     - "AMD-V"


### 🚀 Passo 1: Ativar o recurso do Subsistema Windows para Linux

Este comando ativa o recurso principal do WSL necessário para executar distribuições Linux:
   - Ativar o recurso opcional do Subsistema Windows para Linux.
   - dism.exe é a ferramenta de Gerenciamento e Manutenção de Imagens de Implantação usada para modificar recursos do Windows.
   - /online direciona o comando para o sistema operacional em execução.
   - /enable-feature especifica que você deseja ativar um recurso.
   - /featurename:Microsoft-Windows-Subsystem-Linux é o nome específico do recurso que precisamos ativar.
   - /all ativa todos os recursos pai necessários, se houver.
   - /norestart impede que o sistema reinicie automaticamente imediatamente (vamos reiniciar depois).

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

### 🖥️ Passo 2: Ativar o recurso de Plataforma de Máquina Virtual

O WSL2 requer suporte à virtualização. Este comando ativa os componentes necessários:
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### 🔁 Passo 3: Reinicie o Computador

Uma reinicialização é necessária para aplicar as alterações dos passos anteriores.

Ação: Salve seu trabalho e reinicie o computador agora.

### ⚙️ Passo 4: Definir o WSL como versão 2 por padrão

Após reiniciar, abra novamente o PowerShell como Administrador. Execute o seguinte comando:
```powershell
wsl --set-default-version 2
```
_Nota: Caso apareça uma mensagem sobre atualização do kernel, veja o próximo passo._

### 📦 Passo 5: (Opcional, mas recomendado) Atualizar o Kernel do WSL

Para garantir compatibilidade e melhor desempenho, atualize o kernel do WSL:
```powershell
wsl --update
```
### 📥 Passo 6: Instalar o Ubuntu 24.04 LTS
Você pode listar distribuições disponíveis (opcional):
```powershell
wsl --list --online
```
E instalar o Ubuntu 24.04 LTS com:
```powershell
wsl --install -d Ubuntu-24.04
```
Nota: Esse processo pode levar alguns minutos, dependendo da sua conexão com a internet.

### 👤 Passo 7: Criar sua conta de usuário Linux
Após a instalação, a primeira execução do Ubuntu solicitará que você:

  - Crie um nome de usuário Linux
  - Defina uma senha para essa conta

Após isso, seu ambiente Ubuntu estará pronto para uso no WSL2!

### ✅ Conclusão
Parabéns! Agora você tem o WSL2 e o Ubuntu 24.04 LTS funcionando no seu Windows. Você pode abrir o `Ubuntu` digitando ubuntu no menu Iniciar ou usando o comando `wsl` no terminal.


![image](https://github.com/user-attachments/assets/b151a951-94fb-444d-b9cc-64f2649ac57e)
------------------------------------------------------
## ⚙️ Etapas para configurar o Docker no WSL2 (Ubuntu)
vamos configurar o Docker dentro do WSL

### ✅ Passo 1: Atualizar os pacotes
Abra o terminal do Ubuntu e execute:
```bash
sudo apt update && sudo apt upgrade -y
```

### ✅ Passo 2: Instalar dependências necessárias
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common lsb-release -y
```

### ✅ Passo 3: Adicionar a chave GPG oficial do Docker
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### ✅ Passo 4: Adicionar o repositório do Docker
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### ✅ Passo 5: Instalar o Docker Engine
```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

### ✅ Passo 6: Habilitar o Docker para uso sem sudo (opcional, mas prático)
```bash
sudo usermod -aG docker ${USER}
su - ${USER}
```
⚠️ Importante: depois desse comando, você precisa fechar o terminal e abrir de novo (ou executar newgrp docker) para a permissão surtir efeito.


### ✅ Passo 7: Testar o Docker
```bash
docker run hello-world
```
⚠️ Importante: Tambem pode ser verificado a instalação com os comandos 
```bash
sudo systemctl status docker
```
```bash
docker --version
```
