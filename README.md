# 🖥️ Lab-suporte-infra | Infraestrutura On-Premise, AD DS, GPOs e POPs
#### Este repositório documenta a implementação prática de uma infraestrutura de rede corporativa *On-Premise* do zero. O objetivo deste laboratório é simular cenários reais de administração de servidores, gestão de identidades com Active Directory Domain Services (AD DS), aplicação de políticas de grupo (GPOs), elaboração de POPs (Procedimentos Operacionais Padrão) e resolução de incidentes (troubleshooting) de Suporte N1/N2.
---
## Base de conhecimentos aplicadas:
* Google It support 
* Fundamentos de active directory e redes
* Conhecimentos em PowerShell 
---
## 📝 Projetos
### [01. Etapas de Implementação AD DS](./01-etapas-ad-ds)
   * Configuração de servidor Active Directory, Unidades Organizacionais (OUs) no Windows Server.
### [02. Configurando serviços de rede DHCP, DNS e Servidor de arquivos NTFS](./02-rede-no-ad-dhcp-dns-ntfs)
   * Configuração de Servidor DHCP e Resolução Reversa DNS e implementação de File Server com Permissões Compartilhadas e NTFS.
### [03. Aplicação de políticas de grupo (GPO)](./03-aplicar-gpo)
   * Criando, aplicando e testando políticas de grupos básicas.
### [04. Procedimento Operacional Padrão (POP)](./04-aplicar-pop)
   * POP de Backup básico e Retenção de Dados (VSS & Cobian Reflector)
   * POP de Gestão de Print Server e Manutenção do Spooler de Impressão.
### [05. Resolução de incidentes (Troubleshooting)](./05-troubleshooting)
   * Knowledge Base Article (KBA)

---
## ⚠️ O que levar em consideração?
Este projeto é de evolução progressiva ele aborda e testa os conhecimentos práticos com suporte e infraestrutura. A formatação dele permite que aja interação com outros projetos do meu perfil afim de evitar redundâncias entre eles. 
* Esse Lab-suporte-infra está considerando a topologia e configurações de redes abordadas no sub-projeto específico do [Lab-redes/projetoTechCorp]( ) aonde eu explico melhor lá o escopo do projeto. 
Finalidade: simular um ambiente base dentro do nosso projeto de AD e evitando redundância.
* Esse Lab-suporte-infra está integrado ao [Lab-powershell-scripts]( ) aonde serão centralizados os scripts usados neste projeto. Finalidade: evitar redundância.
* Esse Lab-suporte-infra se estende de forma natural e progressiva com a integração do ambiente híbrido em cloud. 
Finalidade: adicionar a tecnologia do Azure e Entra ID dando sequência ao [Lab-infra-cloud]( ).




