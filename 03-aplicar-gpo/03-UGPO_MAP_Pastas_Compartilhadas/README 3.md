## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 3. `UGPO_MAP_Pastas_Compartilhadas`

- **Objetivo:** Mapear automaticamente unidades de rede de acordo com o departamento do usuário via Item-Level Targeting (ILT).
    
- **Link da OU:** `OU=Usuarios,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `User Configuration -> Preferences -> Windows Settings -> Drive Maps`
    
- **Passo a Passo:**
    
    1. Clicar com o botão direito -> _New_ -> _Mapped Drive_.
        
    2. Em _General_: Action = **Update**, Location = `\\DC01\RH_Docs`, Drive Letter = `H:`.
        
    3. Na aba _Common_: Marcar **Item-Level Targeting** -> Clicar em **Targeting...**
        
    4. Adicionar nova regra: `Security Group` IS `CORP\GRP_RH_Users`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Mapeamento ILT](.github/assets/gpo-ugpo-map-drive-ilt.png)
    ```
    
    _(Sugestão de print: Tela do Item-Level Targeting Editor configurada e janela do "Este Computador" mostrando o disco `H:`)_
    