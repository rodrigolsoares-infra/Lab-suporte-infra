### 🚧 Status: Em desenvolvimento contínuo.

# Backup Corporativo e Retenção de Dados

## 🎯 Objetivo Geral
Garantir a continuidade de negócios e a proteção contra perda de dados no File Server corporativo, combinando recuperação instantânea via snapshots de volume (VSS) com rotinas automatizadas de backup incremental.

---

# 1 - Proteção de Dados com Volume Shadow Copy (VSS)

## 🎯 Objetivo
Implementar e configurar o serviço de Cópias de Sombra (VSS - Volume Shadow Copy) nos volumes de armazenamento do File Server, permitindo a recuperação rápida de arquivos corrompidos ou deletados acidentalmente pelos próprios usuários (self-service recovery) sem necessidade de intervenção do N2/N3.

---

## 🛠️ Recursos Utilizados
* **Tecnologia:** Windows Server Volume Shadow Copy Service (VSS)
* **Recursos Implementados:**
  * Agendamento automático de snapshots diários do volume de dados.
  * Habilitação da aba "Versões Anteriores" no Explorador de Arquivos para os clientes da rede.
  * Mitigação de chamados N1 relacionados à perda acidental de documentos.

---

## 🖼️ Evidências de Execução

### 1. Habilitação e Agendamento do VSS no Volume
![Configuração do VSS](imagens/09-vss-habilitado.png)

### 2. Validação da Restauração via Versões Anteriores
![Restauração de Arquivos](imagens/10-restauracao-versao-anterior.png)


--- 

# 2 - Rotina de Backup Corporativo Automatizado com Cobian Reflector

## 🎯 Objetivo
Configurar e automatizar rotinas de backup corporativo a nível de arquivos (File-Level) utilizando o **Cobian Reflector**, garantindo a redundância e integridade dos dados do File Server com agendamento periódico e estratégias de backup incremental.

---

## 🛠️ Recursos Utilizados
* **Ferramenta:** Cobian Reflector
* **Estratégia de Backup:** Backup Incremental da pasta crítica `C:\Empresa`
* **Recursos Implementados:**
  * Execução como Serviço do Windows (*Windows Service*) para operação em background.
  * Agendamento automatizado de rotinas diárias.
  * Separação rigorosa entre diretório de origem (Filesystem) e repositório de destino.

---

## 🖼️ Evidências de Execução

### 1. Configuração da Tarefa e Parâmetros de Backup
![Configuração do Cobian](imagens/11-cobian-tarefa-configurada.png)

### 2. Validação dos Logs de Execução com Sucesso
![Backup Concluído](imagens/12-cobian-backup-sucesso.png)

# Passo 05: Gestão de Impressão e Serviços de Rede

## 🎯 Objetivo Geral
Padronizar a gestão de dispositivos de impressão em ambiente corporativo, abrangendo o compartilhamento centralizado de recursos no servidor e a criação de automações para rápida resolução de incidentes de spooler travado.


# 1 - Implantação de Servidor de Impressão e Compartilhamento de Redes

## 🎯 Objetivo
Configurar o compartilhamento centralizado de recursos de impressão no servidor de domínio (`SRV-DC01`), padronizando nomes de fila, permissões de acesso e publicação no diretório corporativo.

---

## 🛠️ Recursos Utilizados
* **Recurso:** Windows Server Print Management
* **Recursos Implementados:**
  * Criação de fila de impressão compartilhada (`IMP-RH-CORP`).
  * Atribuição de nomenclatura padronizada e localização física para inventário.
  * Restrição de permissões de gerenciamento de documentos via grupos de segurança.

---

## 🖼️ Evidência de Execução

### Impressora Compartilhada no Servidor
![Impressora Compartilhada](imagens/13-impressora-compartilhada.png)

---
# 2 - Automação de Manutenção do Spooler de Impressão

## 🎯 Objetivo
Desenvolver e aplicar script de manutenção preventiva/corretiva para a resolução de travamentos na fila de impressão do Windows, automatizando a interrupção do serviço, expurgo de arquivos temporários corrompidos e reinicialização limpa do Spooler.

---

## 🛠️ Recursos Utilizados
* **Tecnologia:** PowerShell (`Stop-Service`, `Remove-Item`, `Start-Service`)
* **Fluxo de Atuação N1:**
  * Interrupção forçada do serviço `Spooler`.
  * Limpeza de buffer no diretório `C:\Windows\System32\spool\PRINTERS`.
  * Restabelecimento do serviço e validação de status ativo.

---

## 🖼️ Evidência de Execução

### Execução do Script de Reset do Spooler
![Reset do Spooler](imagens/14-reset-spooler-execucao.png)
---
