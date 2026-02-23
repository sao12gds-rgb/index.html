<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>OCORRÊNCIA DE PONTO</title>
<style>
body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: auto;
}
h2 {
    text-align: center;
}
input, textarea {
    width: 100%;
    margin-bottom: 10px;
}
button {
    padding: 10px;
    cursor: pointer;
}
</style>
</head>
<body>

<h2>OCORRÊNCIA DE PONTO</h2>

<h4>DADOS DO EMPREGADOR</h4>
<p><strong>Razão Social:</strong> Gds Logística Ltda</p>
<p><strong>CNPJ:</strong> 16.637.947/0002-29</p>
<p><strong>Endereço:</strong> Rua Teodoro de Beaurepaire, 34 – Vila Dom Pedro I – São Paulo/SP</p>
<p><strong>CEP:</strong> 04279-030</p>

<hr>

<h4>DADOS DO TRABALHADOR</h4>

<label>Nome do Colaborador:</label>
<input type="text">

<label>Cargo:</label>
<input type="text">

<label>CPF:</label>
<input type="text">

<label>Data da Ocorrência:</label>
<input type="date">

<hr>

<h4>Registro não marcado</h4>
<input type="checkbox"> Entrada<br>
<input type="checkbox"> Saída Intervalo<br>
<input type="checkbox"> Retorno Intervalo<br>
<input type="checkbox"> Saída<br><br>

<label>Horário devido da marcação:</label>
<input type="time">

<hr>

<label>Justificativa:</label>
<textarea rows="4"></textarea>

<br><br>
<button onclick="window.print()">Gerar para impressão</button>

</body>
</html>
