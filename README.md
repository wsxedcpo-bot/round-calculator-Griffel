[Расчет круглых коробок.html](https://github.com/user-attachments/files/25280065/default.html)
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GriffelBox — калькулятор коробок</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --puder: #f9f1f0;
            --puder-medium: #f0e4e1;
            --puder-dark: #d9c2be;
            --accent: #ff7e8f;
            --accent-hover: #e5677a;
            --text: #4e3e3a;
            --text-light: #7a6a66;
            --white: #ffffff;
            --shadow: rgba(0,0,0,0.03);
            --border-radius: 16px;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--puder);
            color: var(--text);
            line-height: 1.5;
            padding: 30px 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
        }

        .wrapper {
            max-width: 1440px;
            width: 100%;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }
        .logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            margin-bottom: 10px;
        }
        .logo-icon {
            font-size: 42px;
            line-height: 1;
        }
        h1 {
            font-size: 44px;
            font-weight: 700;
            letter-spacing: -0.02em;
            color: var(--text);
        }
        .subhead {
            font-size: 16px;
            font-weight: 400;
            color: var(--text-light);
            margin-bottom: 6px;
        }
        .copyright {
            font-size: 12px;
            color: var(--text-light);
            opacity: 0.8;
            font-style: italic;
            margin-top: 8px;
        }

        .input-card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            padding: 32px;
            box-shadow: 0 12px 28px var(--shadow);
            margin-bottom: 32px;
        }
        .input-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 28px;
            margin-bottom: 28px;
        }
        .input-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        .input-group label {
            font-size: 13px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: var(--text-light);
        }
        .input-group input {
            padding: 16px 18px;
            border: 2px solid var(--puder-medium);
            border-radius: 12px;
            font-size: 18px;
            font-weight: 500;
            color: var(--text);
            transition: 0.2s;
            font-family: 'Inter', sans-serif;
        }
        .input-group input:focus {
            border-color: var(--accent);
            outline: none;
            box-shadow: 0 0 0 3px rgba(255,126,143,0.1);
        }

        .radio-row {
            display: flex;
            gap: 16px;
            margin-top: 4px;
        }
        .radio-item {
            flex: 1;
        }
        .radio-item input {
            display: none;
        }
        .radio-item label {
            display: block;
            padding: 16px 20px;
            background-color: var(--puder);
            border: 2px solid var(--puder-medium);
            border-radius: 12px;
            text-align: center;
            font-weight: 600;
            font-size: 16px;
            color: var(--text);
            cursor: pointer;
            transition: 0.2s;
        }
        .radio-item input:checked + label {
            background-color: var(--accent);
            border-color: var(--accent);
            color: white;
        }
        .radio-item label:hover {
            border-color: var(--accent);
        }

        .btn-calc {
            width: 100%;
            padding: 18px;
            background-color: var(--accent);
            border: none;
            border-radius: 14px;
            font-size: 18px;
            font-weight: 700;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            font-family: 'Inter', sans-serif;
            letter-spacing: 0.5px;
            box-shadow: 0 6px 0 #b35f6b;
            margin-top: 8px;
        }
        .btn-calc:hover {
            background-color: var(--accent-hover);
            transform: translateY(-3px);
            box-shadow: 0 9px 0 #b35f6b;
        }
        .btn-calc:active {
            transform: translateY(2px);
            box-shadow: 0 4px 0 #b35f6b;
        }

        .result-grid {
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 32px;
            align-items: start;
        }
        @media (max-width: 1000px) {
            .result-grid {
                grid-template-columns: 1fr;
            }
        }

        .result-card {
            background-color: var(--white);
            border-radius: var(--border-radius);
            padding: 24px;
            box-shadow: 0 8px 20px var(--shadow);
        }
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            padding-bottom: 16px;
            border-bottom: 2px solid var(--puder-medium);
        }
        .card-header h2 {
            font-size: 22px;
            font-weight: 600;
        }
        .box-badge {
            background-color: var(--accent);
            color: white;
            padding: 6px 18px;
            border-radius: 40px;
            font-weight: 600;
            font-size: 15px;
        }

        .table-responsive {
            overflow-x: auto;
        }
        .comp-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 15px;
        }
        .comp-table th {
            background-color: var(--puder-medium);
            padding: 16px 12px;
            text-align: left;
            font-weight: 600;
            color: var(--text);
            border-bottom: 2px solid var(--puder-dark);
        }
        .comp-table td {
            padding: 16px 12px;
            border-bottom: 1px solid var(--puder-medium);
        }
        .comp-table tr:last-child td {
            border-bottom: none;
        }
        .comp-table tr:nth-child(even) {
            background-color: #fffbfb;
        }
        .dimension-badge {
            display: inline-block;
            background-color: rgba(255,126,143,0.12);
            color: var(--accent-hover);
            font-weight: 700;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 15px;
            font-family: 'Inter', monospace;
        }

        .btn-excel {
            background-color: #2c3e50;
            color: white;
            border: none;
            border-radius: 10px;
            padding: 14px 24px;
            font-weight: 600;
            font-size: 15px;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 20px;
        }
        .btn-excel:hover {
            background-color: #1e2b37;
        }

        .cutting-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
            border: 1px solid var(--puder-dark);
            border-radius: 12px;
            overflow: hidden;
        }
        .cutting-table th {
            background-color: #7ea8ff;
            color: white;
            padding: 12px 6px;
            font-weight: 600;
            border-right: 1px solid rgba(255,255,255,0.2);
            text-align: center;
        }
        .cutting-table td {
            padding: 12px 6px;
            border: 1px solid var(--puder-medium);
            text-align: center;
            vertical-align: middle;
        }
        .cutting-table .count-main {
            font-weight: 700;
            color: var(--accent);
            font-size: 16px;
        }
        .cutting-table .fraction {
            font-size: 12px;
            color: var(--text-light);
            margin-top: 4px;
        }
        .btn-visual {
            background-color: var(--accent);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-visual:hover {
            background-color: var(--accent-hover);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.5);
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        }
        .modal-content {
            background-color: white;
            border-radius: 20px;
            max-width: 1100px;
            width: 100%;
            max-height: 90vh;
            overflow: auto;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }
        .modal-header {
            padding: 20px 24px;
            border-bottom: 1px solid #e0e0e0;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #f7f7f7;
        }
        .modal-header h3 {
            font-weight: 600;
            color: #333;
        }
        .close-btn {
            background: none;
            border: none;
            font-size: 28px;
            cursor: pointer;
            color: #666;
            line-height: 1;
        }
        .modal-body {
            padding: 24px;
        }

        .excel-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
            border: 1px solid #a0a0a0;
        }
        .excel-table th {
            background-color: #e8e8e8;
            color: #000;
            padding: 8px 10px;
            border: 1px solid #aaa;
            font-weight: 600;
        }
        .excel-table td {
            padding: 6px 10px;
            border: 1px solid #ccc;
            color: #222;
        }
        .excel-table .mono {
            font-family: 'Courier New', monospace;
            font-weight: 600;
        }

        .sheet-container {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            justify-content: center;
            margin-top: 20px;
        }
        .sheet-item {
            text-align: center;
        }
        .sheet-canvas-box {
            position: relative;
            width: 300px;
            height: 200px;
            border: 2px solid #333;
            background-color: #fafafa;
            margin: 10px auto;
        }
        .element-rect {
            position: absolute;
            border: 1px solid var(--accent);
            background-color: rgba(255,126,143,0.15);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            font-weight: 600;
            color: #333;
        }

        .footer-note {
            margin-top: 30px;
            font-size: 13px;
            text-align: center;
            color: var(--text-light);
        }
    </style>
</head>
<body>
    <div class="wrapper">
        <div class="header">
            <div class="logo">
                <span class="logo-icon">📦</span>
                <h1>GriffelBox</h1>
            </div>
            <div class="subhead">точный расчёт компонентов упаковки</div>
            <div class="copyright">© Все расчёты — интеллектуальная собственность GriffelBox. Копирование запрещено.</div>
        </div>

        <div class="input-card">
            <div class="input-grid">
                <div class="input-group">
                    <label>Диаметр коробки, см</label>
                    <input type="number" id="diameter" min="1" step="0.1" value="10">
                </div>
                <div class="input-group">
                    <label>Высота коробки, см</label>
                    <input type="number" id="height" min="1" step="0.1" value="10">
                </div>
                <div class="input-group">
                    <label>Тип коробки</label>
                    <div class="radio-row">
                        <div class="radio-item">
                            <input type="radio" name="lid" id="withLid" checked>
                            <label for="withLid">С крышкой</label>
                        </div>
                        <div class="radio-item">
                            <input type="radio" name="lid" id="withoutLid">
                            <label for="withoutLid">Без крышки</label>
                        </div>
                    </div>
                </div>
            </div>
            <button class="btn-calc" id="calculateBtn">Рассчитать</button>
        </div>

        <div class="result-grid">
            <div class="result-card">
                <div class="card-header">
                    <h2>Компоненты коробки</h2>
                    <div class="box-badge" id="boxLabel">10×10 см</div>
                </div>
                <div class="table-responsive">
                    <table class="comp-table" id="componentTable">
                        <thead><tr><th>Компонент</th><th>Развёртка, мм</th></tr></thead>
                        <tbody id="componentBody"></tbody>
                    </table>
                </div>
                <button class="btn-excel" id="excelBtn">
                    <span>📊</span> Экспорт в Excel‑формат (ЧБ)
                </button>
            </div>

            <div class="result-card">
                <div class="card-header">
                    <h2>Раскрой листа</h2>
                    <div class="box-badge">кол-во / 1/кол-во</div>
                </div>
                <div class="table-responsive">
                    <table class="cutting-table" id="cuttingTable">
                        <thead id="cuttingHeader"></thead>
                        <tbody id="cuttingBody"></tbody>
                    </table>
                </div>
                <div class="footer-note">
                    * Нажмите «Показать» для визуализации оптимального размещения.
                </div>
            </div>
        </div>
    </div>

    <div id="excelModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>📋 GriffelBox — таблица компонентов (черно‑белая, Excel‑стиль)</h3>
                <button class="close-btn" id="closeExcelModal">&times;</button>
            </div>
            <div class="modal-body" id="excelBody"></div>
        </div>
    </div>

    <div id="cuttingModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 id="visualTitle">Визуализация раскроя</h3>
                <button class="close-btn" id="closeCuttingModal">&times;</button>
            </div>
            <div class="modal-body" id="visualBody"></div>
        </div>
    </div>

    <script>
        (function() {
            "use strict";

            const SHEETS = [
                { w: 1020, h: 720, name: '1020×720' },
                { w: 1020, h: 700, name: '1020×700' },
                { w: 1000, h: 700, name: '1000×700' },
                { w: 900,  h: 640, name: '900×640' }
            ];

            const CUTTING_POSITIONS = ['Лайнер крышки', 'Лайнер', 'Цветное дно', 'Лайнер борта крышки'];

            // ----- Функции расчёта -----
            function getSleeveLength(diameter) {
                if (diameter === 10) return 700;
                if (diameter === 18) return 2000;
                if (diameter >= 25) return 3000;
                return 1000;
            }

            function getLidRingHeight(boxHeight) {
                if (boxHeight < 25) return 30;
                if (boxHeight >= 29 && boxHeight <= 40) return 40;
                return 30;   // для 25-28 и >40
            }

            function roundToTenSpecial(val, diameter) {
                if (diameter === 10) {
                    return Math.ceil(val / 10) * 10;
                }
                return Math.round(val / 10) * 10;
            }

            function getLinerAddition(diameter) {
                if (diameter === 10 || diameter === 23) return 20;
                if (diameter === 15) return 10;
                return 30;
            }

            // ----- Главный расчёт -----
            function calculateAll() {
                const diameter = parseFloat(document.getElementById('diameter').value) || 0;
                const height = parseFloat(document.getElementById('height').value) || 0;
                const withLid = document.getElementById('withLid').checked;

                if (diameter <= 0 || height <= 0) {
                    document.getElementById('componentBody').innerHTML = '<tr><td colspan="2" style="padding:40px;text-align:center;">Введите корректные размеры</td></tr>';
                    document.getElementById('cuttingBody').innerHTML = '';
                    return;
                }

                const diamMm = diameter * 10;
                const heightMm = height * 10;

                const components = [];

                // 1. Гильза/хром-эрзац – ВАЖНО: первое число = высота коробки в мм, второе = фиксированная длина
                const sleeveLen = getSleeveLength(diameter);
                components.push({
                    name: 'Гильза/хром-эрзац',
                    size: `${heightMm} × ${sleeveLen}`,    // высота × длина
                    w: sleeveLen,
                    h: heightMm
                });

                // 2. Лайнер
                const linerCirc = Math.PI * diamMm;
                const rounded = roundToTenSpecial(linerCirc, diameter);
                const linerAdd = getLinerAddition(diameter);
                const linerW = rounded + linerAdd;
                const linerH = heightMm + 30;
                components.push({
                    name: 'Лайнер',
                    size: `${linerW} × ${linerH}`,
                    w: linerW,
                    h: linerH
                });

                // 3. Цветное дно
                const bottom = diamMm + 20;
                components.push({
                    name: 'Цветное дно',
                    size: `${bottom} × ${bottom}`,
                    w: bottom,
                    h: bottom
                });

                if (withLid) {
                    // 4. Кольцо крышки/хром-эрзац – высота кольца × фиксированная длина
                    const ringH = getLidRingHeight(height);
                    const ringLen = getSleeveLength(diameter);
                    components.push({
                        name: 'Кольцо крышки/хром-эрзац',
                        size: `${ringH} × ${ringLen}`,
                        w: ringLen,
                        h: ringH
                    });

                    // 5. Лайнер борта крышки – (высота кольца+10) × (длина лайнера+10)
                    const brimH = ringH + 10;
                    const brimW = linerW + 10;
                    components.push({
                        name: 'Лайнер борта крышки',
                        size: `${brimH} × ${brimW}`,
                        w: brimW,
                        h: brimH
                    });

                    // 6. Лайнер крышки – (диаметр+30) квадрат
                    const lidLiner = diamMm + 30;
                    components.push({
                        name: 'Лайнер крышки',
                        size: `${lidLiner} × ${lidLiner}`,
                        w: lidLiner,
                        h: lidLiner
                    });
                }

                // Отрисовка таблицы компонентов
                let compHtml = '';
                components.forEach(c => {
                    compHtml += `<tr><td>${c.name}</td><td><span class="dimension-badge">${c.size}</span></td></tr>`;
                });
                document.getElementById('componentBody').innerHTML = compHtml;
                document.getElementById('boxLabel').innerHTML = `${diameter}×${height} см ${withLid ? '🔵' : '⚪'}`;

                // Раскрой только для нужных позиций
                const cuttingComponents = components.filter(c => CUTTING_POSITIONS.includes(c.name));
                renderCuttingTable(cuttingComponents);

                // Сохраняем данные для модалок
                window.__lastComponents = components;
                window.__lastDiameter = diameter;
                window.__lastHeight = height;
                window.__lastWithLid = withLid;
                window.__lastCutting = cuttingComponents;
            }

            // ----- Оптимальное количество на листе (с учётом поворота) -----
            function calcOptimalCount(elW, elH, sheetW, sheetH) {
                const cntNormal = Math.floor(sheetW / elW) * Math.floor(sheetH / elH);
                const cntRotated = Math.floor(sheetW / elH) * Math.floor(sheetH / elW);
                if (cntNormal >= cntRotated) {
                    return {
                        count: cntNormal,
                        cols: Math.floor(sheetW / elW),
                        rows: Math.floor(sheetH / elH),
                        rotated: false
                    };
                } else {
                    return {
                        count: cntRotated,
                        cols: Math.floor(sheetW / elH),
                        rows: Math.floor(sheetH / elW),
                        rotated: true
                    };
                }
            }

            // ----- Таблица раскроя -----
            function renderCuttingTable(elements) {
                const thead = document.getElementById('cuttingHeader');
                const tbody = document.getElementById('cuttingBody');

                let headHtml = `<tr><th rowspan="2">Элемент</th>`;
                SHEETS.forEach(s => {
                    headHtml += `<th colspan="2">${s.name} мм</th>`;
                });
                headHtml += `<th rowspan="2">Виз.</th></tr><tr>`;
                SHEETS.forEach(() => {
                    headHtml += `<th>шт</th><th>1/шт</th>`;
                });
                headHtml += `</tr>`;
                thead.innerHTML = headHtml;

                if (!elements || elements.length === 0) {
                    tbody.innerHTML = '<tr><td colspan="'+(SHEETS.length*2+2)+'">Нет элементов для раскроя</td></tr>';
                    return;
                }

                let bodyHtml = '';
                elements.forEach((el, idx) => {
                    bodyHtml += `<tr><td style="font-weight:600; text-align:left;">${el.name}</td>`;
                    SHEETS.forEach(sheet => {
                        const opt = calcOptimalCount(el.w, el.h, sheet.w, sheet.h);
                        const count = opt.count;
                        const fraction = count ? (1/count).toFixed(3) : '0';
                        bodyHtml += `<td><span class="count-main">${count}</span></td>`;
                        bodyHtml += `<td class="fraction">${fraction}</td>`;
                    });
                    bodyHtml += `<td><button class="btn-visual" onclick="showVisualization(${idx})">Показать</button></td>`;
                    bodyHtml += `</tr>`;
                });
                tbody.innerHTML = bodyHtml;
                window.__cuttingElements = elements;
            }

            // ----- Визуализация раскроя (глобальная функция) -----
            window.showVisualization = function(elementIndex) {
                const el = window.__cuttingElements[elementIndex];
                if (!el) return;

                const title = `Раскрой: ${el.name} (${el.w}×${el.h} мм)`;
                document.getElementById('visualTitle').innerText = title;

                let visualHtml = `<div style="display:flex; flex-wrap:wrap; gap:30px; justify-content:center;">`;

                SHEETS.forEach((sheet, sidx) => {
                    const opt = calcOptimalCount(el.w, el.h, sheet.w, sheet.h);
                    if (opt.count === 0) return;
                    const cellW = opt.rotated ? el.h : el.w;
                    const cellH = opt.rotated ? el.w : el.h;

                    visualHtml += `<div class="sheet-item">
                        <div style="font-weight:600; margin-bottom:8px;">${sheet.name}</div>
                        <div class="sheet-canvas-box" id="canvas-${elementIndex}-${sidx}" style="position:relative; width:300px; height:200px; border:2px solid #333;"></div>
                        <div style="margin-top:6px; font-size:13px;">
                            <span>${opt.cols}×${opt.rows} = ${opt.count} шт.</span>
                            ${opt.rotated ? '<span style="color:gray;"> (поворот)</span>' : ''}
                        </div>
                    </div>`;
                });
                visualHtml += `</div>`;

                document.getElementById('visualBody').innerHTML = visualHtml;
                document.getElementById('cuttingModal').style.display = 'flex';

                setTimeout(() => {
                    SHEETS.forEach((sheet, sidx) => {
                        const opt = calcOptimalCount(el.w, el.h, sheet.w, sheet.h);
                        if (opt.count === 0) return;
                        const canvasDiv = document.getElementById(`canvas-${elementIndex}-${sidx}`);
                        if (!canvasDiv) return;

                        const cellW = opt.rotated ? el.h : el.w;
                        const cellH = opt.rotated ? el.w : el.h;

                        const scale = Math.min(
                            (canvasDiv.clientWidth - 10) / (opt.cols * cellW),
                            (canvasDiv.clientHeight - 10) / (opt.rows * cellH)
                        ) * 0.9;

                        const offsetX = (canvasDiv.clientWidth - opt.cols * cellW * scale) / 2;
                        const offsetY = (canvasDiv.clientHeight - opt.rows * cellH * scale) / 2;

                        for (let row = 0; row < opt.rows; row++) {
                            for (let col = 0; col < opt.cols; col++) {
                                const rect = document.createElement('div');
                                rect.className = 'element-rect';
                                rect.style.width = `${cellW * scale}px`;
                                rect.style.height = `${cellH * scale}px`;
                                rect.style.left = `${offsetX + col * cellW * scale}px`;
                                rect.style.top = `${offsetY + row * cellH * scale}px`;
                                rect.style.display = 'flex';
                                rect.style.alignItems = 'center';
                                rect.style.justifyContent = 'center';
                                rect.style.fontSize = '10px';
                                rect.innerText = `${row*opt.cols+col+1}`;
                                rect.title = `${opt.rotated ? el.h+'×'+el.w : el.w+'×'+el.h} мм`;
                                canvasDiv.appendChild(rect);
                            }
                        }
                    });
                }, 30);
            };

            // ----- Excel модалка (ЧБ, Excel-стиль) -----
            function openExcelModal() {
                const comps = window.__lastComponents;
                if (!comps) return;

                let excelHtml = `<table class="excel-table">
                    <thead>
                        <tr>
                            <th>№</th>
                            <th>Компонент</th>
                            <th>Развёртка (мм)</th>
                            <th>Ширина</th>
                            <th>Высота</th>
                            <th>Примечание</th>
                        </tr>
                    </thead>
                    <tbody>`;
                comps.forEach((c, i) => {
                    const [w, h] = c.size.split(' × ').map(Number);
                    excelHtml += `<tr>
                        <td>${i+1}</td>
                        <td>${c.name}</td>
                        <td class="mono">${c.size}</td>
                        <td>${w}</td>
                        <td>${h}</td>
                        <td>${getNote(c.name)}</td>
                    </tr>`;
                });
                excelHtml += `</tbody></table>
                <div style="margin-top:24px; font-size:12px; border-top:1px solid #aaa; padding-top:16px;">
                    <strong>Методика расчёта:</strong> по формулам GriffelBox.<br>
                    Дата: ${new Date().toLocaleString('ru-RU')}<br>
                    Параметры: Ø ${window.__lastDiameter} см, H ${window.__lastHeight} см, ${window.__lastWithLid ? 'крышка' : 'без крышки'}<br>
                    <span style="color:#666;">© Интеллектуальная собственность GriffelBox</span>
                </div>`;
                document.getElementById('excelBody').innerHTML = excelHtml;
                document.getElementById('excelModal').style.display = 'flex';
            }

            function getNote(name) {
                if (name.includes('Гильза')) return 'основа коробки';
                if (name.includes('Кольцо крышки')) return 'бортик крышки';
                if (name.includes('Лайнер') && name.includes('борта')) return 'внутр. облицовка борта';
                if (name.includes('Лайнер') && name.includes('крышки')) return 'внутр. облицовка крышки';
                if (name.includes('Лайнер')) return 'внутр. облицовка';
                if (name.includes('Цветное дно')) return 'дно с цветным покрытием';
                return '';
            }

            // ----- Закрытие модалок -----
            function closeModal(modalId) {
                document.getElementById(modalId).style.display = 'none';
            }

            // ----- Привязка событий -----
            document.getElementById('calculateBtn').addEventListener('click', calculateAll);
            document.getElementById('diameter').addEventListener('input', calculateAll);
            document.getElementById('height').addEventListener('input', calculateAll);
            document.getElementById('withLid').addEventListener('change', calculateAll);
            document.getElementById('withoutLid').addEventListener('change', calculateAll);
            document.getElementById('excelBtn').addEventListener('click', openExcelModal);

            document.getElementById('closeExcelModal').addEventListener('click', () => closeModal('excelModal'));
            document.getElementById('closeCuttingModal').addEventListener('click', () => closeModal('cuttingModal'));

            window.addEventListener('click', (e) => {
                if (e.target.classList.contains('modal')) {
                    e.target.style.display = 'none';
                }
            });

            // Стартовый расчёт
            calculateAll();
        })();
    </script>
</body>
</html>
