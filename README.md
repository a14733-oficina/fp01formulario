Análise Técnica do Projeto - FP01

📝 Descrição do Projeto

Este projeto demonstra a interação fundamental entre um formulário de registo simples em HTML e um script de processamento em PHP. O objetivo é recolher dados básicos do utilizador (Nome, Idade, Senha) e, no lado do servidor (PHP), processar esses dados para:

1.
Classificar a idade do utilizador (Criança, Adolescente, Adulto).

2.
Avaliar a força da senha com base no seu comprimento.

3.
Apresentar uma mensagem de boas-vindas e os resultados da análise.

🛠️ Tecnologias Utilizadas

Tecnologia
Propósito
HTML5
Criação do formulário de registo.
PHP
Processamento dos dados submetidos, lógica condicional e apresentação de resultados.


📂 Estrutura de Ficheiros

O projeto é composto por dois ficheiros principais:

Plain Text


/
├── form.html      (Formulário de entrada de dados)
├── processa.php   (Script PHP de processamento e saída)


💻 Análise Detalhada do Código

1. HTML (form.html)

O ficheiro form.html é um formulário simples e direto, focado na recolha de três tipos de dados.

Elemento
Atributo name
Tipo de Campo
Observações
Nome
nome
text
Campo de texto simples.
Idade
idade
number
Utiliza type="number" com min="1" e max="120", fornecendo uma validação client-side básica para garantir que a idade é um número razoável.
Password
senha
password
O type="password" oculta a entrada do utilizador, uma boa prática de segurança.
Formulário
N/A
N/A
Utiliza method="POST" para submeter os dados de forma segura (não visível no URL) para o script processa.php.


2. PHP (processa.php)

O ficheiro processa.php contém toda a lógica de backend e a apresentação dos resultados.

2.1. Receção e Processamento de Dados

Linhas
Código PHP
Descrição
2-4
$nome=$_POST["nome"]; ...
Receção de Dados: Recolhe os valores submetidos do formulário através do array superglobal $_POST.
5
$tamanho = strlen($senha);
Função PHP: Utiliza a função nativa strlen() para calcular o comprimento da string da senha, essencial para a lógica de avaliação de força.


2.2. Lógica Condicional (Classificação de Idade)

O script utiliza uma estrutura if/elseif/else para classificar a idade recebida:

PHP


if($idade > 18){
    $idadeTexto = "adulto👴";
} elseif ($idade < 12) {
    $idadeTexto = "criança👶";
}else{
    $idadeTexto = "adolescente🧑";
}


•
Análise: A lógica é clara e funcional, definindo três categorias de idade.

2.3. Lógica Condicional (Avaliação de Senha)

Uma segunda estrutura if/elseif/else é usada para avaliar a força da senha com base no seu comprimento:

PHP


if($tamanho > 8){
    // ... Password forte
}elseif($tamanho < 5){
    // ... Password fraca
}else{
    // ... Password media
}


•
Análise: Esta é uma implementação básica de avaliação de força. O código utiliza tags <span> com estilos inline (style='color: ...') para colorir o resultado, o que demonstra a mistura de PHP e HTML/CSS para saída dinâmica.

2.4. Saída (Output)

O script utiliza a função echo para gerar a saída HTML diretamente:

PHP


echo "Ola $nome,bem vindo!  
";
echo "$nome tu és $idadeTexto!  
";
// ... (saída da avaliação da senha)


•
Análise: O PHP está a gerar o HTML de forma direta. Embora funcional, esta abordagem não é ideal para projetos maiores, pois mistura a lógica de programação com a estrutura de apresentação.

💡 Sugestões de Melhoria e Refatoração

1. Separação de Responsabilidades (PHP e HTML)

A principal melhoria técnica seria separar a lógica de processamento da apresentação.

•
Problema Atual: O processa.php gera o HTML diretamente com echo.

•
Recomendação: O PHP deve apenas calcular $idadeTexto e $forcaSenhaTexto. O HTML deve ser escrito de forma estruturada, e o PHP deve ser usado apenas para "imprimir" as variáveis nos locais apropriados.

Exemplo de Refatoração:

PHP


<?php
// Lógica de Processamento (no topo do ficheiro)
// ... (cálculo de $idadeTexto e $forcaSenhaTexto)
?>
<!DOCTYPE html>
<html>
<head>
    <title>Resultado do Processamento</title>
    <style>
        .forte { color: green; }
        .fraca { color: red; }
        .media { color: orange; }
    </style>
</head>
<body>
    <h1>Resultado da Análise</h1>
    <p>Olá **<?php echo $nome; ?>**, bem-vindo!</p>
    <p>Tu és **<?php echo $idadeTexto; ?>**.</p>
    <p>A tua senha é classificada como: <span class="<?php echo $classeCSS; ?>"><?php echo $forcaSenhaTexto; ?></span></p>
</body>
</html>


2. Validação de Dados em PHP

O script assume que todos os dados foram submetidos corretamente.

•
Recomendação: Adicionar validação para garantir que os campos não estão vazios e que a idade é um número inteiro válido, utilizando funções como isset() e filter_var().

3. Melhoria na Avaliação de Senha

A avaliação de senha é muito básica.

•
Recomendação: Para uma avaliação mais robusta, considerar a inclusão de requisitos como a presença de letras maiúsculas, minúsculas, números e símbolos, em vez de apenas o comprimento.

4. Uso de CSS Externo

O estilo inline para a cor da senha deve ser evitado.

•
Recomendação: Mover os estilos de cor para um ficheiro CSS externo ou para a tag <style> no <head> do documento, e usar classes CSS (como .forte, .fraca, .media) no PHP.

