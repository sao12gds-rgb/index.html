<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador Confirmação Azul Cargo WhatsApp</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; background: #f0f8ff; }
        .logo { text-align: center; margin-bottom: 20px; }
        .logo img { max-width: 250px; height: auto; }
        .form-group { margin-bottom: 15px; }
        label { display: block; font-weight: bold; margin-bottom: 5px; }
        input, textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 5px; box-sizing: border-box; }
        button { background: #007bff; color: white; padding: 12px 20px; border: none; border-radius: 5px; cursor: pointer; width: 100%; margin-bottom: 10px; font-size: 16px; }
        button:hover { background: #0056b3; }
        #preview { border: 1px solid #ddd; padding: 20px; margin-top: 20px; background: white; display: none; }
        #whatsapp-btn { background: #25D366; }
        #whatsapp-btn:hover { background: #128C7E; }
        #baixar-pack { background: #dc3545; font-size: 18px; }
        #baixar-pack:hover { background: #c82333; }
        #danfe-link { background: #28a745; }
    </style>
</head>
<body>
    <div class="logo">
        <img src="https://seeklogo.com/images/A/azul-cargo-express-logo-3B8A8A8A8A-seeklogo.com.png" alt="Azul Cargo Express ✈️" onerror="this.src='https://upload.wikimedia.org/wikipedia/commons/2/2d/Azul_Cargo_Express_logo.png';">
        <div style="font-size: 20px; color: #1e3a8a; margin-top: 10px;">CONFIRMAÇÃO DE ENTREGA</div>
    </div>
    
    <form id="generatorForm">
        <div class="form-group">
            <label>Telefone (5511999999999):</label>
            <input type="tel" id="telefone" placeholder="5511999999999" required>
        </div>
        
        <div class="form-group">
            <label>Nome Destinatário:</label>
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
            <label>Chave NF-e (44 dígitos):</label>
            <input type="text" id="chaveNFe" placeholder="43123456789012345678901234567890123456789012" maxlength="44" required>
        </div>
        
        <button type="button" onclick="gerarTudo()">🚀 Gerar Mensagem + Baixar PDFs NF + Confirmação</button>
    </form>
    
    <div id="preview" style="display:none;">
        <h3>✅ Mensagem WhatsApp (SEM chave):</h3>
        <textarea id="mensagemTexto" rows="8" readonly style="background: #e9ecef;"></textarea>
        <br>
        <button id="whatsapp-btn" onclick="enviarWhatsApp()">📱 Abrir WhatsApp Pronto</button>
    </div>

    <script>
        function gerarTudo() {
            const rastreio = document.getElementById('rastreio').value;
            const nome = document.getElementById('nome').value;
            const remetente = document.getElementById('remetente').value;
            const tel = document.getElementById('telefone').value;
            const chave = document.getElementById('chaveNFe').value;
            
            if (!tel || !chave || !rastreio) return alert('Preencha todos os campos!');
            
            // Mensagem SEM chave NF
            const mensagem = `Boa tarde, ${nome}

Falo da Azul Cargo Express ✈️

Solicitamos, por gentileza, a confirmação de recebimento da mercadoria referente ao rastreio ${rastreio}, remetente ${remetente} 
Pedimos que confirme por esta mensagem se a entrega foi realizada e se a mercadoria foi recebida em perfeitas condições.

Esta confirmação ficará registrada em sistema como evidência formal de entrega.

Agradecemos o retorno.`;
            
            document.getElementById('mensagemTexto').value = mensagem;
            document.getElementById('preview').style.display = 'block';
            
            // 1. Baixa PDF Confirmação
            setTimeout(() => baixarPDFConfirmacao(rastreio), 500);
            
            // 2. Abre MeuDanfe pra NF (usuário baixa manual)
            setTimeout(() => window.open(`https://meudanfe.com.br/?chave=${chave}`, '_blank'), 1000);
        }
        
        function baixarPDFConfirmacao(rastreio) {
            const element = document.getElementById('preview');
            html2pdf()
                .from(element)
                .set({ filename: `Confirmacao_AzulCargo_${rastreio}.pdf` })
                .save();
        }
        
        function enviarWhatsApp() {
            const tel = document.getElementById('telefone').value.replace(/[^0-9]/g, '');
            const mensagem = encodeURIComponent(document.getElementById('mensagemTexto').value);
            window.open(`https://wa.me/${tel}?text=${mensagem}`);
        }
    </script>
</body>
</html>

