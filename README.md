<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador Confirmação Azul Cargo WhatsApp</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; background: #f0f8ff; }
        .form-group { margin-bottom: 15px; }
        label { display: block; font-weight: bold; margin-bottom: 5px; }
        input, textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 5px; box-sizing: border-box; }
        button { background: #007bff; color: white; padding: 12px 20px; border: none; border-radius: 5px; cursor: pointer; width: 100%; margin-bottom: 10px; font-size: 16px; }
        button:hover { background: #0056b3; }
        #preview { border: 1px solid #ddd; padding: 20px; margin-top: 20px; background: white; display: none; }
        .azul-logo { text-align: center; font-size: 24px; color: #1e3a8a; margin-bottom: 20px; }
        #whatsapp-btn { background: #25D366; }
        #whatsapp-btn:hover { background: #128C7E; }
        #danfe-link { background: #28a745; }
        #danfe-link:hover { background: #218838; }
    </style>
</head>
<body>
    <div class="azul-logo">Azul Cargo Express ✈️</div>
    
    <form id="generatorForm">
        <div class="form-group">
            <label>Número de Telefone (5511999999999):</label>
            <input type="tel" id="telefone" placeholder="5511999999999" required>
        </div>
        
        <div class="form-group">
            <label>Nome do Destinatário:</label>
            <input type="text" id="nome" value="Sr. GUILHERME CHAVES VAZ" required>
        </div>
        
        <div class="form-group">
            <label>Rastreio/AWB:</label>
            <input type="text" id="rastreio" value="02856680" required>
        </div>
        
        <div class="form-group">
            <label>Remetente:</label>
            <input type="text" id="remetente" value="LIVE ROUPAS ESPORTIVAS LTDA" required>
        </div>
        
        <div class="form-group">
            <label>Chave de Acesso NF-e (44 dígitos):</label>
            <input type="text" id="chaveNFe" placeholder="43123456789012345678901234567890123456789012" maxlength="44" required>
        </div>
        
        <button type="button" onclick="gerarPreview()">Gerar Mensagem + PDF</button>
    </form>
    
    <div id="preview">
        <h3>✅ Mensagem Pronta para WhatsApp:</h3>
        <textarea id="mensagemTexto" rows="10" readonly style="background: #e9ecef;"></textarea>
        <br>
        <button id="whatsapp-btn" onclick="enviarWhatsApp()">📱 Abrir WhatsApp (anexar PDFs)</button>
        <button onclick="baixarPDF()">🖨️ Baixar PDF Confirmação</button>
        <button id="danfe-link" onclick="consultarMeuDanfe()">📄 Gerar DANFE NF-e MeuDanfe (Grátis)</button>
    </div>

    <script>
        function gerarPreview() {
            const tel = document.getElementById('telefone').value;
            const nome = document.getElementById('nome').value;
            const rastreio = document.getElementById('rastreio').value;
            const remetente = document.getElementById('remetente').value;
            const chave = document.getElementById('chaveNFe').value;
            
            if (!tel || !chave) return alert('Preencha telefone e chave NF-e!');
            
            const mensagem = `Boa tarde, ${nome}

Falo da Azul Cargo Express ✈️

Solicitamos, por gentileza, a confirmação de recebimento da mercadoria referente ao rastreio ${rastreio}, remetente ${remetente} 
Pedimos que confirme por esta mensagem se a entrega foi realizada e se a mercadoria foi recebida em perfeitas condições.

Esta confirmação ficará registrada em sistema como evidência formal de entrega.

NF-e Chave: ${chave}

Agradecemos o retorno.`;
            
            document.getElementById('mensagemTexto').value = mensagem;
            document.getElementById('preview').style.display = 'block';
        }
        
        function enviarWhatsApp() {
            const tel = document.getElementById('telefone').value.replace(/[^0-9]/g, '');
            const mensagem = encodeURIComponent(document.getElementById('mensagemTexto').value);
            window.open(`https://wa.me/${tel}?text=${mensagem}`);
        }
        
        function baixarPDF() {
            const element = document.getElementById('preview');
            html2pdf().from(element).save(`Confirmacao_AzulCargo_${document.getElementById('rastreio').value}.pdf`);
        }
        
        function consultarMeuDanfe() {
            const chave = document.getElementById('chaveNFe').value;
            window.open(`https://meudanfe.com.br/?chave=${chave}`, '_blank');
        }
    </script>
</body>
</html>
