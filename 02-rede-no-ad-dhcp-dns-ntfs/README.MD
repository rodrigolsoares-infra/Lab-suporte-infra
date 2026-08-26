### 🚧 Status: Em desenvolvimento contínuo.

# Implementação de Serviços Essenciais de Rede (DHCP e DNS)

## 🎯 Objetivo
Configurar e validar a distribuição automática de endereçamento de rede via protocolo DHCP no Windows Server 2022, garantindo integração nativa com o Active Directory DS e resolução de nomes via DNS (Zonas Direta e Reversa).

---

## ⚙️ Especificações do Escopo DHCP (`Escopo_TechCorp_LAN`)
* **Rede/Sub-rede:** `192.168.10.0/24`
* **Intervalo de Distribuição:** `192.168.10.100` até `192.168.10.200`
* **Máscara de Sub-rede:** `255.255.255.0`
* **Gateway Padrão (Router):** `192.168.10.10`
* **Servidor DNS Principal:** `192.168.10.10` (`SRV-DC01`)
* **Nome do Domínio:** `techcorp.local`

---

## 🖼️ Evidências de Validação

### 1. Concessões Ativas no Console DHCP (`SRV-DC01`)
![Concessoes Ativas DHCP](imagens/05-dhcp-concessoes.png)

### 2. Endereço IP e Opções de Rede Recebidas no Cliente (`CLI-TI-01`)
![IP Configurado via DHCP no Cliente](imagens/06-cliente-ip-dhcp.png)

---
---

# Implementação de File Server com Permissões Compartilhadas e NTFS

## 🎯 Objetivo
Configurar um Servidor de Arquivos (File Server) corporativo no Windows Server 2022, implementando o princípio do menor privilégio (PoLP) através do controle de acesso baseado em funções (RBAC), combinando permissões de Compartilhamento SMB e Segurança NTFS.

---

## 📁 Estrutura de Pastas e Matriz de Acesso

| Pasta | Caminho Local | Grupo com Acesso | Nível de Permissão (NTFS) |
| :--- | :--- | :--- | :--- |
| `Empresa` | `C:\Empresa` | `Todos` (Everyone) | Read/List (Compartilhamento SMB) |
| `TI` | `C:\Empresa\TI` | `GRP_TI_Admins` | Controle Total |
| `Financeiro` | `C:\Empresa\Financeiro` | `GRP_Financeiro_RW` | Modificar / Leitura e Escrita |
| `RH` | `C:\Empresa\RH` | `GRP_RH_RW` | Modificar / Leitura e Escrita |
| `Vendas` | `C:\Empresa\Vendas` | `GRP_Vendas_RW` | Modificar / Leitura e Escrita |

---

## 🖼️ Evidências de Validação

### 1. Configuração de Permissões Avançadas NTFS (`SRV-DC01`)
![Permissoes NTFS](imagens/07-permissoes-ntfs.png)

### 2. Validação de Controle de Acesso no Cliente (`CLI-TI-01`)
![Acesso Negado e Mapeamento](imagens/08-acesso-negado-cliente.png)
