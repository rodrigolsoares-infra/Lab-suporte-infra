## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 4. `CGPO_SYS_WSUS_Config`

- **Objetivo:** Direcionar as estações para baixar atualizações do servidor WSUS local.
    
- **Link da OU:** `OU=Computadores,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `Computer Configuration -> Policies -> Administrative Templates -> Windows Components -> Windows Update`
    
- **Passo a Passo:**
    
    1. Habilitar `Specify intranet Microsoft update service location` -> Inserir `[http://wsus.corp.local:8530](http://wsus.corp.local:8530)` nos campos de serviço.
        
    2. Habilitar `Configure Automatic Updates` -> Selecionar a opção `4 - Auto download and schedule the install`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Cliente WSUS](.github/assets/gpo-cgpo-sys-wsus-client.png)
    ```
    
    *(Sugestão de print: Painel de configurações do Windows Update mostrando o aviso _"Algumas configurações são geridas pela sua organização"_)