# Formacao Spark & Databricks

## Guia Passo a Passo: Instalando WSL2 e Ubuntu 24.04 LTS via PowerShell

Este guia irá te orientar na instalação do Subsistema Windows para Linux versão 2 (WSL2) e, em seguida, da distribuição Ubuntu 24.04 LTS utilizando o PowerShell no seu computador com Windows.

## ✅ Pré-requisitos

1. **Versão do Windows:** Você precisa do Windows 10 versão 1903 ou superior (Build 18362+), ou do Windows 11, para ter suporte ao WSL2.  
2. **Privilégios de Administrador:** Você deve executar o PowerShell como Administrador. Clique com o botão direito no ícone do PowerShell e selecione “Executar como administrador”.  
3. **Virtualização Ativada:** A virtualização por hardware deve estar ativada na BIOS/UEFI do seu computador.  
   - Caso encontre erros relacionados à virtualização, reinicie seu computador, entre na BIOS/UEFI (DEL, F2, F10 ou F12 durante o boot), e ative opções como:
     - "Virtualization Technology"
     - "VT-x"
     - "AMD-V"

---

## 🚀 Passo 1: Ativar o recurso do Subsistema Windows para Linux

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

## 🖥️ Passo 2: Ativar o recurso de Plataforma de Máquina Virtual

O WSL2 requer suporte à virtualização. Este comando ativa os componentes necessários:
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## 🔁 Passo 3: Reinicie o Computador

Uma reinicialização é necessária para aplicar as alterações dos passos anteriores.

Ação: Salve seu trabalho e reinicie o computador agora.

## ⚙️ Passo 4: Definir o WSL como versão 2 por padrão

Após reiniciar, abra novamente o PowerShell como Administrador. Execute o seguinte comando:
```powershell
wsl --set-default-version 2
```
_Nota: Caso apareça uma mensagem sobre atualização do kernel, veja o próximo passo._

## 📦 Passo 5: (Opcional, mas recomendado) Atualizar o Kernel do WSL

Para garantir compatibilidade e melhor desempenho, atualize o kernel do WSL:
```powershell
wsl --update
```
## 📥 Passo 6: Instalar o Ubuntu 24.04 LTS
Você pode listar distribuições disponíveis (opcional):
```powershell
wsl --list --online
```
E instalar o Ubuntu 24.04 LTS com:
```powershell
wsl --install -d Ubuntu-24.04
```
Nota: Esse processo pode levar alguns minutos, dependendo da sua conexão com a internet.

## 👤 Passo 7: Criar sua conta de usuário Linux
Após a instalação, a primeira execução do Ubuntu solicitará que você:

  - Crie um nome de usuário Linux
  - Defina uma senha para essa conta

Após isso, seu ambiente Ubuntu estará pronto para uso no WSL2!

## ✅ Conclusão
Parabéns! Agora você tem o WSL2 e o Ubuntu 24.04 LTS funcionando no seu Windows. Você pode abrir o `Ubuntu` digitando ubuntu no menu Iniciar ou usando o comando `wsl` no terminal.


```powershell

```







# EM INGLES 
markdown
# Step-by-Step Guide: Installing WSL2 and Ubuntu 24.04 LTS via PowerShell

This guide will walk you through installing the Windows Subsystem for Linux version 2 (WSL2) and then installing the Ubuntu 24.04 LTS distribution using PowerShell on your Windows machine.

**Prerequisites:**
1.  **Windows Version:** You need Windows 10 version 1903 or higher (Build 18362+) for WSL2 support, or Windows 11.
2.  **Administrator Privileges:** You must run PowerShell as an Administrator. Right-click the PowerShell icon and select "Run as administrator".
3.  **Virtualization Enabled:** Hardware virtualization must be enabled in your computer's BIOS/UEFI.
   - This is usually enabled by default on modern PCs, but if you encounter errors related to virtualization later, you may need to restart your computer, enter the BIOS/UEFI setup (often by pressing keys like DEL, F2, F10, or F12 during startup), and look for settings like
     - "Virtualization Technology",
     - "VT-x",
     - "AMD-V", or similar, and ensure they are enabled.

---

## Step 1: Enable the Windows Subsystem for Linux Feature

This command enables the core WSL feature required to run Linux distributions.
   - Enable the Windows Subsystem for Linux optional feature.
   -  dism.exe is the Deployment Image Servicing and Management tool used to modify Windows features.
   -  /online targets the running operating system.
   -  /enable-feature specifies you want to turn a feature on.
   -  /featurename:Microsoft-Windows-Subsystem-Linux is the specific feature we need.
   -  /all enables all parent features if required.
   -  /norestart prevents the system from automatically restarting immediately (we'll restart later).
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## Step 2: Enable the Virtual Machine Platform Feature

WSL2 requires virtualization support. This command enables the necessary platform components.

# Enable the Virtual Machine Platform optional feature.

# This is required for WSL2 to use virtualization for better performance and compatibility.

# Parameters are similar to the previous command, targeting a different feature.

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## Step 3: Restart Your Computer

A restart is required at this point for the changes made in the previous steps to take effect.

**Action:** Please save your work and restart your computer now.

## Step 4: Set WSL Default Version to 2

After restarting, open PowerShell as Administrator again. This command ensures that any future Linux distributions you install will use WSL2 by default.

# Set the default version of WSL to 2.

# The 'wsl' command is the primary tool for managing WSL.

# --set-default-version 2 tells WSL to use version 2 for any new installations.

```powershell
wsl --set-default-version 2
```

**Note:** You might see a message about the kernel being updated, or you might get an error if virtualization is not properly enabled in your BIOS/UEFI (see Prerequisites).

## Step 5: (Optional but Recommended) Update WSL Kernel

It's a good idea to ensure you have the latest WSL kernel components.

# Update the WSL Linux kernel to the latest version.

# This downloads and installs any available updates for the WSL components.

```powershell
wsl --update
```

## Step 6: Install Ubuntu 24.04 LTS

Now, you can install the specific Linux distribution. We'll use the wsl command to find and install Ubuntu 24.04 LTS.

First, optionally list available distributions to confirm the name:

# Optional: List available Linux distributions online to confirm the name.

# The '-l' or '--list' flag shows installed distributions.

# The '-o' or '--online' flag shows distributions available for installation.

# Look for the entry matching "Ubuntu-24.04".

```powershell
wsl --list --online
```

Then, install Ubuntu 24.04 LTS:

# Install Ubuntu 24.04 LTS.

# --install tells WSL to download and install a distribution.

# -d specifies the name of the distribution to install.

# 'Ubuntu-24.04' is the expected name for Ubuntu 24.04 LTS. (Verify with the list command if unsure).

```powershell
wsl --install -d Ubuntu-24.04
```

**Note:** This command will download the Ubuntu 24.04 LTS package and install it. This might take a few minutes depending on your internet speed.

## Step 7: Set Up Your Linux User Account

Once the installation is complete, the Ubuntu 24

```
```

