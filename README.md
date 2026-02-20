<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerador Confirmação Azul Cargo</title>
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
        #whatsapp-btn { background: #25D366; font-size: 18px; }
        #whatsapp-btn:hover { background: #128C7E; }
    </style>
</head>
<body>
    <div class="logo">
        <img src="https://seeklogo.com/images/A/azul-cargo-express-logo-3B8A8A8A8A-seeklogo.com.png" alt="Azul Cargo Express ✈️" 
             onerror="this.src='https://upload.wikimedia.org/wikipedia/commons/2/2d/Azul_Cargo_Express_logo.png';">
        <div style="font-size: 20px; color: #1e3a8a; margin-top: 10px;">CONFIRMAÇÃO DE ENTREGA</div>
    </div>
    
    <form id="generatorForm">
        <div class="form-group">
            <label>Telefone (5511974929028):</label>
            <input type="tel" id="telefone" value="5511974929028" required>
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
        <button type="button" onclick="gerarTudo()">🚀 GERAR Mensagem + PDF + MeuDanfe</button>
    </form>
    
    <div id="preview">
        <h3>✅ Mensagem WhatsApp PRONTA:</h3>
        <textarea id="mensagemTexto" rows="10" readonly style="background: #e9ecef; font-size: 14px;"></textarea>
        <button id="whatsapp-btn" onclick="enviarWhatsApp()">📱 ABRIR WHATSAPP COM MENSAGEM</button>
        <p><small>💡 Baixe PDF confirmação + NF MeuDanfe > anexe no WhatsApp</small></p>
    </div>

    <script>
        function gerarTudo() {
            const rastreio = document.getElementById('rastreio').value;
            const nome = document.getElementById('nome').value;
            const remetente = document.getElementById('remetente').value;
            const tel = document.getElementById('telefone').value;
            const chave = document.getElementById('chaveNFe').value;
            
            if (!tel || !chave || !rastreio) {
                return alert('❌ Preencha TELEFONE, CHAVE NF-e e AWB!');
            }
            
            const mensagem = `Boa tarde, ${nome}

Falo da Azul Cargo Express ✈️

Solicitamos, por gentileza, a confirmação de recebimento da mercadoria referente ao rastreio ${rastreio}, remetente ${remetente} 
Pedimos que confirme por esta mensagem se a entrega foi realizada e se a mercadoria foi recebida em perfeitas condições.

Esta confirmação ficará registrada em sistema como evidência formal de entrega.

Agradecemos o retorno.`;
            
            document.getElementById('mensagemTexto').value = mensagem;
            document.getElementById('preview').style.display = 'block';
            
            // Baixa PDF confirmação
            html2pdf()
                .from(document.getElementById('preview'))
                .set({
                    filename: `Confirmacao_AzulCargo_${rastreio}.pdf`,
                    margin: 1,
                    jsPDF: { unit: 'in', format: 'a4', orientation: 'portrait' }
                })
                .save();
            
            // Abre MeuDanfe pra baixar NF
            setTimeout(() => {
                window.open(`https://meudanfe.com.br/?chave=${chave}`, '_blank');
            }, 1000);
        }
        
        function enviarWhatsApp() {
            let tel = document.getElementById('telefone').value.replace(/[^0-9]/g, '');
            if (tel.length < 12) {
                return alert('❌ Telefone inválido! Use 5511XXXXXXXXX');
            }
            const msg = encodeURIComponent(document.getElementById('mensagemTexto').value);
            window.open(`https://wa.me/${tel}?text=${msg}`, '_blank');
        }
    </script>
</body>
</html>

