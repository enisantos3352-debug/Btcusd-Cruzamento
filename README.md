
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matrix - Relógio dos Cruzamentos & Tendência BTC</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0b0e11;
            color: #d1d4dc;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 520px;
            background: #1e222d;
            border: 1px solid #2a2e39;
            border-radius: 8px;
            padding: 20px;
            box-sizing: border-box;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
        }
        h2 {
            color: #3861fb;
            font-size: 15px;
            text-align: center;
            margin-top: 0;
            margin-bottom: 15px;
            letter-spacing: 1px;
        }
        .live-card {
            background: #131722;
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            margin-bottom: 12px;
            border: 1px solid #2a2e39;
        }
        .live-label {
            font-size: 11px;
            color: #848e9c;
            text-transform: uppercase;
        }
        .live-value {
            font-size: 22px;
            font-weight: bold;
            color: #f3ba2f;
            margin-top: 3px;
        }
        .grid-ma {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 1fr;
            gap: 6px;
            margin-bottom: 12px;
        }
        .ma-card {
            background: #131722;
            padding: 8px 4px;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #f3ba2f;
        }
        .ma-label { font-size: 9px; color: #f3ba2f; font-weight: bold; text-transform: uppercase; }
        .ma-value { font-size: 11px; font-weight: bold; color: #ffffff; margin-top: 4px; }

        .grid-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            margin-bottom: 12px;
        }
        .stat-box {
            background: #131722;
            padding: 10px;
            border-radius: 6px;
            text-align: center;
            border: 1px solid #2a2e39;
        }
        .stat-label {
            font-size: 10px;
            color: #848e9c;
            margin-bottom: 3px;
            text-transform: uppercase;
        }
        .stat-val-center { font-size: 14px; font-weight: bold; color: #3861fb; }
        .stat-val-max { font-size: 14px; font-weight: bold; color: #2ebd85; }
        .stat-val-min { font-size: 14px; font-weight: bold; color: #f6465d; }

        .signal-box {
            padding: 16px;
            border-radius: 6px;
            text-align: center;
            font-weight: bold;
            font-size: 14px;
            background: #131722;
            border: 2px solid #2a2e39;
            transition: all 0.3s ease;
        }
        .signal-buy { 
            background: rgba(0, 92, 41, 0.85); 
            color: #ffffff; 
            border-color: #2ebd85; 
            box-shadow: 0 0 15px rgba(46, 189, 133, 0.4);
        }
        .signal-sell { 
            background: rgba(122, 28, 42, 0.85); 
            color: #ffffff; 
            border-color: #f6465d; 
            box-shadow: 0 0 15px rgba(246, 70, 93, 0.4);
        }
        .signal-wait { 
            color: #848e9c; 
            border-color: #2a2e39;
        }

        /* Tela de Bloqueio com o Pix */
        #tela-bloqueio {
            display: none;
            background: #131722;
            border: 2px solid #f6465d;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
        }
        #tela-bloqueio h3 { color: #f6465d; margin-top: 0; }
        .pix-box {
            background: #1e222d;
            border: 1px dashed #2ebd85;
            padding: 12px;
            border-radius: 6px;
            margin: 12px 0;
        }
        .pix-chave {
            font-size: 16px;
            font-weight: bold;
            color: #2ebd85;
            margin-top: 5px;
            word-break: break-all;
        }
        .btn-whatsapp {
            display: inline-block;
            margin-top: 10px;
            background: #25d366;
            color: #fff;
            padding: 12px 18px;
            border-radius: 6px;
            text-decoration: none;
            font-weight: bold;
            font-size: 14px;
        }

        .footer-info {
            font-size: 10px;
            color: #787b86;
            text-align: center;
            margin-top: 12px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Matrix - Radar de Cruzamento dos Ponteiros</h2>
        
        <!-- PAINEL PRINCIPAL -->
        <div id="painel-principal">
            <div class="live-card">
                <div class="live-label">Preço Atual ao Vivo (BTC)</div>
                <div class="live-value" id="preco-atual">Carregando...</div>
            </div>

            <div class="grid-ma">
                <div class="ma-card">
                    <div class="ma-label">MÉD 9</div>
                    <div class="ma-value" id="ma-9">--</div>
                </div>
                <div class="ma-card">
                    <div class="ma-label">MÉD 21</div>
                    <div class="ma-value" id="ma-21">--</div>
                </div>
                <div class="ma-card">
                    <div class="ma-label">MÉD 50</div>
                    <div class="ma-value" id="ma-50">--</div>
                </div>
                <div class="ma-card">
                    <div class="ma-label">MÉD 200</div>
                    <div class="ma-value" id="ma-200">--</div>
                </div>
            </div>

            <div class="grid-stats">
                <div class="stat-box">
                    <div class="stat-label">Centro (Abertura 00h)</div>
                    <div class="stat-val-center" id="centro-00h">--</div>
                </div>
                <div class="stat-box">
                    <div class="stat-label">Próximo Cruzamento</div>
                    <div class="stat-val-center" id="proximo-cruzamento" style="color: #f3ba2f;">--</div>
                </div>
                <div class="stat-box">
                    <div class="stat-label">Teto Estimado (Máxima)</div>
                    <div class="stat-val-max" id="teto-max">--</div>
                </div>
                <div class="stat-box">
                    <div class="stat-label">Piso Estimado (Mínima)</div>
                    <div class="stat-val-min" id="piso-min">--</div>
                </div>
            </div>

            <div id="sinal-cruzamento" class="signal-box signal-wait">
                Escaneando o relógio e o alinhamento das médias...
            </div>
        </div>

        <!-- TELA DE BLOQUEIO COM PIX -->
        <div id="tela-bloqueio">
            <h3>⏰ Período de Teste Expirado!</h3>
            <p style="font-size: 13px; color: #d1d4dc;">Seu teste gratuito de 3 dias acabou. Para renovar por <strong>R$ 25/mês</strong>, faça o Pix para a chave abaixo:</p>
            
            <div class="pix-box">
                <div style="font-size: 11px; color: #848e9c; text-transform: uppercase;">Chave Pix (Telefone)</div>
                <div class="pix-chave">92985966939</div>
                <div style="font-size: 11px; color: #d1d4dc; margin-top: 5px;">Valor: <strong>R$ 25,00</strong></div>
            </div>

            <p style="font-size: 12px; color: #848e9c;">Assim que fizer o pagamento, mande o comprovante para o WhatsApp abaixo:</p>
            
            <a href="https://wa.me/5585992704001?text=Olá!%20Acabei%20de%20fazer%20o%20Pix%20de%20R$%2025%20para%20renovar%20o%20painel." target="_blank" class="btn-whatsapp">Mandar Comprovante no WhatsApp</a>
        </div>

        <div class="footer-info">Sistema de Teste Gratuito - 3 Dias</div>
    </div>

    <script>
        function verificarValidadeTeste() {
            const diasDeTeste = 3; 
            const msPorDia = 24 * 60 * 60 * 1000;
            let dataInicio = localStorage.getItem('matrix_inicio_teste_v17');
            if (!dataInicio) {
                dataInicio = new Date().getTime();
                localStorage.setItem('matrix_inicio_teste_v17', dataInicio);
            }
            let agora = new Date().getTime();
            if ((agora - parseInt(dataInicio)) > (diasDeTeste * msPorDia)) {
                document.getElementById('painel-principal').style.display = 'none';
                document.getElementById('tela-bloqueio').style.display = 'block';
                return false;
            }
            return true;
        }

        // Os 22 horários exatos de cruzamento dos ponteiros em segundos totais do dia
        const cruzamentosSegundos = [
            0,       // 00:00:00
            3927,    // 01:05:27
            7855,    // 02:10:55
            11782,   // 03:16:22
            15709,   // 04:21:49
            19636,   // 05:27:16
            23564,   // 06:32:44
            27491,   // 07:38:11
            31418,   // 08:43:38
            35345,   // 09:49:05
            39273,   // 10:54:33
            43200,   // 12:00:00
            47127,   // 13:05:27
            51055,   // 14:10:55
            54982,   // 15:16:22
            58909,   // 16:21:49
            62836,   // 17:27:16
            66764,   // 18:32:44
            70691,   // 19:38:11
            74618,   // 20:43:38
            78545,   // 21:49:05
            82473    // 22:54:33
        ];

        function formatarSegundosEmHora(segTotal) {
            let h = Math.floor(segTotal / 3600);
            let m = Math.floor((segTotal % 3600) / 60);
            let s = segTotal % 60;
            return String(h).padStart(2,'0') + ':' + String(m).padStart(2,'0') + ':' + String(s).padStart(2,'0');
        }

        let hist9 = JSON.parse(localStorage.getItem('matrix_hist_v17_9')) || [];
        let hist21 = JSON.parse(localStorage.getItem('matrix_hist_v17_21')) || [];
        let hist50 = JSON.parse(localStorage.getItem('matrix_hist_v17_50')) || [];
        let hist200 = JSON.parse(localStorage.getItem('matrix_hist_v17_200')) || [];

        async function carregarDadosRelogio() {
            if (!verificarValidadeTeste()) return;

            try {
                const resTicker = await fetch('https://api.binance.com/api/v3/ticker/24hr?symbol=BTCUSDT');
                const dataTicker = await resTicker.json();
                const precoAtual = parseFloat(dataTicker.lastPrice);

                const resKlines = await fetch('https://api.binance.com/api/v3/klines?symbol=BTCUSDT&interval=1h&limit=24');
                const klines = await resKlines.json();

                let abertura00h = precoAtual;
                klines.forEach(candle => {
                    let dataCandle = new Date(candle[0]);
                    if (dataCandle.getUTCHours() === 0) {
                        abertura00h = parseFloat(candle[1]);
                    }
                });

                // Descobrir o próximo cruzamento baseado no horário UTC atual
                let agora = new Date();
                let segundosAtuais = agora.getUTCHours() * 3600 + agora.getUTCMinutes() * 60 + agora.getSeconds();
                let proxSegundos = cruzamentosSegundos[0];
                
                for (let i = 0; i < cruzamentosSegundos.length; i++) {
                    if (cruzamentosSegundos[i] > segundosAtuais) {
                        proxSegundos = cruzamentosSegundos[i];
                        break;
                    }
                }

                // Cálculo das Médias (9, 21, 50, 200)
                function calcularMedia(hist, periodo, valorPadrao) {
                    hist.push(precoAtual);
                    if (hist.length > periodo) hist.shift();
                    let soma = hist.reduce((acc, val) => acc + val, 0);
                    let div = hist.length;
                    if (div < periodo) {
                        soma += (periodo - div) * valorPadrao;
                        div = periodo;
                    }
                    return soma / div;
                }

                let media9 = calcularMedia(hist9, 9, abertura00h);
                let media21 = calcularMedia(hist21, 21, abertura00h);
                let media50 = calcularMedia(hist50, 50, abertura00h);
                let media200 = calcularMedia(hist200, 200, abertura00h);

                localStorage.setItem('matrix_hist_v17_9', JSON.stringify(hist9));
                localStorage.setItem('matrix_hist_v17_21', JSON.stringify(hist21));
                localStorage.setItem('matrix_hist_v17_50', JSON.stringify(hist50));
                localStorage.setItem('matrix_hist_v17_200', JSON.stringify(hist200));

                // Máximas e Mínimas baseadas nos horários do relógio (projeção baseada na volatilidade diária)
                let tetoMax = abertura00h * 1.018;
                let pisoMin = abertura00h * 0.982;

                // Atualizando elementos visuais
                document.getElementById('preco-atual').innerText = `$ ${precoAtual.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('ma-9').innerText = `$ ${media9.toLocaleString('en-US', {minimumFractionDigits: 0, maximumFractionDigits: 0})}`;
                document.getElementById('ma-21').innerText = `$ ${media21.toLocaleString('en-US', {minimumFractionDigits: 0, maximumFractionDigits: 0})}`;
                document.getElementById('ma-50').innerText = `$ ${media50.toLocaleString('en-US', {minimumFractionDigits: 0, maximumFractionDigits: 0})}`;
                document.getElementById('ma-200').innerText = `$ ${media200.toLocaleString('en-US', {minimumFractionDigits: 0, maximumFractionDigits: 0})}`;

                document.getElementById('centro-00h').innerText = `$ ${abertura00h.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('proximo-cruzamento').innerText = formatarSegundosEmHora(proxSegundos);
                document.getElementById('teto-max').innerText = `$ ${tetoMax.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                document.getElementById('piso-min').innerText = `$ ${pisoMin.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;

                // --- SINAL DE ALTA (VERDE) E BAIXA (VERMELHO) ---
                let caixaSinal = document.getElementById('sinal-cruzamento');
                
                // Condição de Alta Perfeita (Leque alinhado + preço acima da abertura central)
                let tendenciaAlta = (precoAtual > media9) && (media9 > media21) && (media21 > media50) && (precoAtual > abertura00h);

                // Condição de Baixa Perfeita (Leque alinhado + preço abaixo da abertura central)
                let tendenciaBaixa = (precoAtual < media9) && (media9 < media21) && (media21 < media50) && (precoAtual < abertura00h);

                if (tendenciaAlta) {
                    caixaSinal.className = 'signal-box signal-buy';
                    caixaSinal.innerHTML = '🚀 TENDÊNCIA DE ALTA CONFIRMADA!<br><span style="font-size: 11px; font-weight: normal; color: #a3ffcb;">Cruzamento e leque de médias a favor da compra!</span>';
                } 
                else if (tendenciaBaixa) {
                    caixaSinal.className = 'signal-box signal-sell';
                    caixaSinal.innerHTML = '📉 TENDÊNCIA DE BAIXA CONFIRMADA!<br><span style="font-size: 11px; font-weight: normal; color: #ffb3bc;">Pressão vendedora nos suportes do relógio!</span>';
                } 
                else {
                    caixaSinal.className = 'signal-box signal-wait';
                    caixaSinal.innerHTML = '⚖️ AGUARDANDO ALINHAMENTO DOS PONTEIROS<br><span style="font-size: 11px; font-weight: normal;">Monitorando o próximo cruzamento do dia...</span>';
                }

            } catch (e) {
                console.error("Erro ao carregar dados do relógio:", e);
            }
        }

        if (verificarValidadeTeste()) {
            setInterval(carregarDadosRelogio, 2000);
            carregarDadosRelogio();
        }
    </script>

</body>
</html>
