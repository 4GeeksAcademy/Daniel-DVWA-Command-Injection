# DVWA - Command Injection

Created: February 5, 2024 10:48 AM

## **Introdução à Injeção de Comandos**

- A injeção de comandos, em sua essência, consiste na inserção de um comando personalizado dentro de um comando já existente
- Em testes mais simples, é comum usar caracteres especiais para inserir nosso comando
- Para fazer esses testes precisamos conhecer os caracteres especiais que podem ser usados no Linux
- Caracteres Especiais
    - **&**
        - Exemplo: `ls & whoami`
        - Usado para encadear comandos
    
    ---
    
    - **;**
        - Exemplo: `ls; whoami`
        - Usado para separar comandos
    
    ---
    
    - **|**
        - Exemplo: `ls | whoami`
        - Usado para redirecionar a saída de um comando para a entrada de outro
    
    ---
    
    - **||**
        - Exemplo: `ls || whoami`
        - Usada como um operador lógico "OU”
    
    ---
    
    - **$()**
        - Exemplo: `echo $(whoami)`
        - Isso é conhecido como substituição de comando em shells Unix/Linux. O conteúdo entre os parênteses é executado como um comando, e a saída é substituída na linha de comando original.
    
    ---
    
    - **"`" (crase)**
        - Exemplo: `echo whoami`
        - Também conhecido como backtick, é semelhante a `$()`. Permite a execução de comandos dentro das crases, e o resultado é substituído na linha de comando original.
    
    ---
    
    - **%**
        - Exemplo: Se um aplicativo não valida adequadamente a entrada e permite algo como `ls%20-l`, isso pode ser explorado para codificar o espaço como `%20`, resultando na execução de `ls -l`.
    
    ---
    
    - **$(())**
        - Exemplo: `echo $((2+2))`
        - Se a entrada não for tratada corretamente, isso pode permitir a execução de expressões aritméticas.
    
    ---
    
    - **{}** ou **[]**
        - Exemplo: `ls {file.txt}`
        - Se o aplicativo não validar adequadamente a entrada, um atacante pode explorar isso para injetar comandos entre chaves.
    
    ---
    
    - ? * []
        - Exemplo: `cat /etc/passwd*`
        - Se a entrada não for tratada corretamente, caracteres curinga podem ser explorados para corresponder a vários arquivos.
    
    ---
    
    - **< >**
        - Exemplo: `cat < /etc/passwd`
        - Se a entrada não for validada, isso poderia permitir a leitura de arquivos sensíveis, como o `/etc/passwd`.
    
    ---
    
    - ("\")
        - Exemplo: `echo \$(whoami)`
        - Se a aplicação não escapar corretamente a entrada do usuário, um atacante pode usar a barra invertida para escapar o caractere `$` e realizar a substituição de comando.

---

## Testes

### low / medium

- Colocando o dns do google ele faz normalmente o ping
- Mas tentando colocar um comando a frente ou sozinho nada acontece
- Para solucionar isso, basta colocar um caracter especial que consiga adicionar um outro comando junto
- Vale lembrar que não é obrigatório colocar um ip antes do nosso comando para funcionar
- Caso o caracter especial que você usou não funcionar, use outros caracteres especiais
    
    ![Untitled](DVWA%20-%20Command%20Injection/Untitled.png)
    

### high

- Aqui nenhum caracter especial funciona
- A menos que você os envie de um jeito diferente
- Existem muitos meios de chegar no mesmo resultados fazendo coisas diferentes e enviando de jeitos diferentes
- Em resumo, o fato de o caractere "|" não ter funcionado em uma tentativa inicial não significa que ele não possa ser eficaz em outros contextos ou ser abordado de outros modos
- Mesmo você usando o comando colado no caracter ele vai funcionar, o Linux consegue entender e executar o comando
    
    ![Screenshot from 2024-02-05 12-31-21.png](DVWA%20-%20Command%20Injection/Screenshot_from_2024-02-05_12-31-21.png)
