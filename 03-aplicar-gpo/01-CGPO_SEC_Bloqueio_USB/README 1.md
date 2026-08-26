## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 1. `CGPO_SEC_Bloqueio_USB`

- **Objetivo:** Impedir o uso de pendrives ou HDs externos para prevenir vazamento de dados e malwares.
    
- **Link da OU:** `OU=Computadores,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `Computer Configuration -> Policies -> Administrative Templates -> System -> Removable Storage Access`
    
- **Passo a Passo:**
    
    1. Localizar a diretiva `All Removable Storage classes: Deny all access`.
        
    2. Alterar o estado para **Enabled**.
        
    3. Executar `gpupdate /force` na máquina cliente.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Acesso Negado USB](.github/assets/gpo-cgpo-sec-bloqueio-usb-denied.png)
    ```
    
    _(Sugestão de print: Janela do Windows Explorer tentando abrir a unidade `E:` exibindo o alerta "Acesso Negado")_