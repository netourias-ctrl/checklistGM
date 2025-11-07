<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Check List de Inspeção - Bases / Racks / Carrinhos</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#f6f8fb;
      --card:#ffffff;
      --accent:#0f62fe;
      --muted:#6b7280;
      --ok:#16a34a;
      --nok:#dc2626;
      --na:#9ca3af;
      --shadow: 0 6px 18px rgba(15,22,39,0.08);
      font-family: 'Inter', system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    html,body{height:100%}
    body{
      margin:0;
      background:linear-gradient(180deg,var(--bg),#eef2ff 60%);
      padding:28px;
      color:#0b1220;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    .container{
      max-width:900px;
      margin:0 auto;
    }

    header.card{
      background:var(--card);
      border-radius:12px;
      padding:18px 20px;
      box-shadow:var(--shadow);
      display:flex;
      gap:16px;
      align-items:center;
      margin-bottom:18px;
    }
    .brand{
      width:64px;
      height:64px;
      border-radius:10px;
      background:linear-gradient(135deg,var(--accent),#5b21b6);
      color:white;
      display:flex;
      align-items:center;
      justify-content:center;
      font-weight:700;
      font-size:20px;
    }
    header h1{
      margin:0;
      font-size:18px;
    }
    header p{margin:2px 0 0;color:var(--muted);font-size:13px}

    .card{
      background:var(--card);
      border-radius:12px;
      padding:18px;
      box-shadow:var(--shadow);
      margin-bottom:18px;
    }

    .meta{
      display:grid;
      grid-template-columns: 1fr 1fr 1fr;
      gap:12px;
      align-items:center;
    }

    label.small{font-size:12px;color:var(--muted);display:block;margin-bottom:6px}
    input[type="text"], input[type="date"], input[type="number"], textarea, select{
      width:100%;
      padding:10px 12px;
      border-radius:8px;
      border:1px solid #e6e9ef;
      font-size:14px;
      background:#fff;
      box-sizing:border-box;
    }
    textarea{min-height:60px;resize:vertical}

    h2.section-title{
      margin:0 0 12px;
      display:flex;
      align-items:center;
      gap:10px;
      font-size:15px;
    }

    /* checklist grid */
    .grid-check{
      display:grid;
      grid-template-columns: 1fr 120px 120px 120px;
      gap:10px;
      align-items:center;
    }
    .item{
      padding:10px;
      border-radius:8px;
      display:flex;
      align-items:center;
      gap:12px;
    }
    .item strong{display:block}
    .status-group{
      display:flex;
      gap:8px;
      align-items:center;
      justify-content:flex-start;
    }
    .status-group label{
      display:inline-flex;
      align-items:center;
      gap:6px;
      background:#fbfdff;
      border:1px solid #eef2ff;
      padding:6px 8px;
      border-radius:8px;
      font-size:13px;
      cursor:pointer;
      user-select:none;
    }
    .status-group input{accent-color:var(--accent)}

    /* Repair section */
    .repairs{
      display:grid;
      grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
      gap:12px;
    }
    .repairs .field{background:#fbfdff;padding:10px;border-radius:8px;border:1px solid #eef2ff}
    .sig{
      display:flex;
      gap:12px;
      align-items:center;
      margin-top:10px;
    }
    .sig canvas{border:1px solid #e6e9ef;border-radius:6px;background:white}
    .buttons{
      display:flex;
      gap:10px;
      justify-content:flex-end;
      margin-top:12px;
    }
    button{
      padding:10px 14px;
      border-radius:8px;
      border:0;
      cursor:pointer;
      font-weight:600;
    }
    .btn-primary{background:var(--accent);color:white}
    .btn-outline{background:transparent;border:1px solid #dbe5ff;color:var(--accent)}
    .small{font-size:13px;padding:8px 10px}

    footer.note{font-size:12px;color:var(--muted);margin-top:8px;text-align:center}

    /* print-friendly */
    @media print{
      body{background:white;padding:0}
      .buttons, header .brand{display:none}
      header.card, .card{box-shadow:none;border-radius:0}
    }

    /* responsive */
    @media (max-width:720px){
      .meta{grid-template-columns: 1fr;}
      .grid-check{grid-template-columns: 1fr 1fr;}
    }

  </style>
</head>
<body>
  <div class="container">

    <header class="card" role="banner">
      <div class="brand">CHK</div>
      <div>
        <h1>Check List de Inspeção de Bases / Racks / Carrinhos</h1>
        <p>Versão moderna do formulário — preencha e imprima/exporte em PDF</p>
      </div>
      <div style="margin-left:auto;text-align:right">
        <div style="font-size:12px;color:var(--muted)">Data</div>
        <div id="display-date" style="font-weight:600"></div>
      </div>
    </header>

    <form id="checklistForm" class="card" autocomplete="off">
      <div class="meta" aria-label="Informações do equipamento">
        <div>
          <label class="small" for="nome">Nome</label>
          <input id="nome" name="nome" type="text" placeholder="Nome do local / equipamento">
        </div>
        <div>
          <label class="small" for="tipo">Tipo do equipamento</label>
          <input id="tipo" name="tipo" type="text" placeholder="Ex: Base sobre rodas">
        </div>
        <div>
          <label class="small" for="numero">Nº / O.S.</label>
          <input id="numero" name="numero" type="text" placeholder="Ex: 0096">
        </div>
      </div>
    </form>

    <section class="card" aria-labelledby="condicoes">
      <h2 id="condicoes" class="section-title">1 — Condições Gerais</h2>

      <div style="display:flex;gap:12px;flex-direction:column">
        <div class="grid-check" aria-hidden="false" role="list">
          <!-- Column headings (visually implicit) -->
          <div style="font-weight:600">Item</div>
          <div style="font-weight:600">OK</div>
          <div style="font-weight:600">NOK</div>
          <div style="font-weight:600">N/A</div>

          <!-- Items list -->
          <!-- repeated structure -->
          <template id="item-template">
            <div class="item" role="listitem"><strong class="label"></strong></div>
            <div class="status-group">
              <label><input type="radio" name="" value="ok"> OK</label>
            </div>
            <div class="status-group">
              <label><input type="radio" name="" value="nok"> NOK</label>
            </div>
            <div class="status-group">
              <label><input type="radio" name="" value="na"> N/A</label>
            </div>
          </template>

        </div>

        <script>
          // JS will render the checklist items
        </script>
      </div>
    </section>

    <section class="card" aria-labelledby="reparo">
      <h2 id="reparo" class="section-title">2 — Reparo Realizado</h2>
      <div class="repairs" id="repairsGrid">
        <!-- Editable repair fields -->
        <div class="field">
          <label class="small">Solda</label>
          <input type="text" id="reparo_solda" placeholder="Descrição / Peças trocadas">
        </div>
        <div class="field">
          <label class="small">Engate</label>
          <input type="text" id="reparo_engate" placeholder="Descrição / Ajuste">
        </div>
        <div class="field">
          <label class="small">Travas</label>
          <input type="text" id="reparo_travas" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Manipulo</label>
          <input type="text" id="reparo_manipulo" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Caixa de roda</label>
          <input type="text" id="reparo_caixa" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Rodízio</label>
          <input type="text" id="reparo_rodizio" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Policarbonato</label>
          <input type="text" id="reparo_policarb" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Amortecedores</label>
          <input type="text" id="reparo_amort" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Lona</label>
          <input type="text" id="reparo_lona" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Brush Bar</label>
          <input type="text" id="reparo_brush" placeholder="Descrição">
        </div>
        <div class="field">
          <label class="small">Carpete</label>
          <input type="text" id="reparo_carpete" placeholder="Descrição">
        </div>
      </div>

      <div style="margin-top:12px">
        <label class="small">Observações</label>
        <textarea id="observacoes" placeholder="Observações gerais sobre a inspeção"></textarea>
      </div>

      <div class="sig">
        <div style="flex:1">
          <label class="small">Nome do serralheiro / ajudante</label>
          <input type="text" id="nome_serralheiro" placeholder="Nome">
        </div>
        <div>
          <label class="small">Assinatura (clicar para assinar)</label><br>
          <canvas id="signature" width="320" height="70" aria-label="Área de assinatura"></canvas>
          <div style="margin-top:6px">
            <button type="button" class="small btn-outline" id="clearSig">Limpar</button>
          </div>
        </div>
      </div>

      <div class="buttons">
        <button type="button" class="btn-outline small" id="resetBtn">Limpar Formulário</button>
        <button type="button" class="btn-primary small" id="printBtn">Exportar / Imprimir</button>
      </div>

    </section>

    <footer class="note">Checklist gerado por sistema — verifique e assine antes de imprimir.</footer>

  </div>

  <script>
    // set date
    const displayDate = document.getElementById('display-date');
    const today = new Date();
    displayDate.textContent = today.toLocaleDateString('pt-BR');

    // checklist items (baseados no formulário da imagem)
    const items = [
      "Soldas",
      "Engates",
      "Travas",
      "Manipulo",
      "Caixa de roda",
      "Rodízio",
      "Policarbonato",
      "Amortecedores",
      "Brush Bar",
      "Lona",
      "Carpete"
    ];

    // render items into the grid-check area
    const grid = document.querySelector('.grid-check');
    const template = document.getElementById('item-template');

    items.forEach((labelText, idx) => {
      // clone nodes
      const tpl = template.content.cloneNode(true);
      const labelNode = tpl.querySelector('.label') || tpl.querySelector('strong');
      labelNode.textContent = labelText;

      // we need to set radio names to group by item
      const radios = tpl.querySelectorAll('input[type="radio"]');
      radios.forEach(r => {
        r.name = 'item_' + idx;
      });

      grid.appendChild(tpl);
    });

    // signature canvas simple drawing
    const canvas = document.getElementById('signature');
    const ctx = canvas.getContext('2d');
    let drawing = false;
    let last = {x:0,y:0};

    function pointerDown(e){
      drawing = true;
      const rect = canvas.getBoundingClientRect();
      last.x = (e.touches ? e.touches[0].clientX : e.clientX) - rect.left;
      last.y = (e.touches ? e.touches[0].clientY : e.clientY) - rect.top;
    }
    function pointerMove(e){
      if(!drawing) return;
      const rect = canvas.getBoundingClientRect();
      const x = (e.touches ? e.touches[0].clientX : e.clientX) - rect.left;
      const y = (e.touches ? e.touches[0].clientY : e.clientY) - rect.top;
      ctx.lineJoin = 'round';
      ctx.lineCap = 'round';
      ctx.strokeStyle = '#0b1220';
      ctx.lineWidth = 2;
      ctx.beginPath();
      ctx.moveTo(last.x, last.y);
      ctx.lineTo(x, y);
      ctx.stroke();
      last.x = x; last.y = y;
    }
    function pointerUp(){drawing = false;}
    canvas.addEventListener('mousedown', pointerDown);
    canvas.addEventListener('mousemove', pointerMove);
    document.addEventListener('mouseup', pointerUp);
    // touch
    canvas.addEventListener('touchstart', (e)=>{ e.preventDefault(); pointerDown(e); });
    canvas.addEventListener('touchmove', (e)=>{ e.preventDefault(); pointerMove(e); });
    canvas.addEventListener('touchend', (e)=>{ pointerUp(); });

    document.getElementById('clearSig').addEventListener('click', ()=>{
      ctx.clearRect(0,0,canvas.width,canvas.height);
    });

    // reset form
    document.getElementById('resetBtn').addEventListener('click', ()=>{
      if (!confirm('Limpar todo o formulário?')) return;
      document.getElementById('checklistForm').reset();
      document.querySelectorAll('.repairs input, textarea').forEach(i=>i.value='');
      document.querySelectorAll('input[type=radio]').forEach(r=>r.checked=false);
      ctx.clearRect(0,0,canvas.width,canvas.height);
      document.getElementById('nome_serralheiro').value='';
      document.getElementById('observacoes').value='';
    });

    // print/export
    document.getElementById('printBtn').addEventListener('click', ()=>{
      // before printing, inline-populate some fields into the printable area if needed
      window.print();
    });

    // accessibility: allow keyboard tabbing on radio labels
    document.querySelectorAll('.status-group label').forEach(l=>{
      l.tabIndex = 0;
      l.addEventListener('keypress', (e)=>{
        if(e.key === 'Enter' || e.key === ' '){
          e.preventDefault();
          const input = l.querySelector('input');
          if(input) input.checked = true;
        }
      });
    });
  </script>
</body>
</html>
