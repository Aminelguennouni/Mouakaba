            --bg-light: #f8fafc;
            --white: #ffffff;
            --danger: #ef4444;
            --success: #10b981;
            --shadow: 0 10px 30px rgba(0,0,0,0.12);
        }

        * { box-sizing: border-box; font-family: 'Cairo', sans-serif; margin: 0; padding: 0; }
        
        body { background-color: var(--bg-light); display: flex; min-height: 100vh; overflow-x: hidden; }

        #menu-toggle {
            position: fixed; top: 20px; right: 20px; z-index: 2200;
            background: var(--primary); color: white; border: none;
            width: 45px; height: 45px; border-radius: 12px; cursor: pointer; font-size: 1.4rem;
            box-shadow: var(--shadow);
        }

        #sidebar {
            width: var(--sidebar-width); background: var(--white); height: 100vh;
            position: fixed; right: 0; top: 0; box-shadow: -5px 0 25px rgba(0,0,0,0.08);
            transition: 0.4s ease; z-index: 2100; padding: 20px; padding-top: 80px;
        }
        #sidebar.closed { transform: translateX(105%); }

        .sb-block { background: #f1f5f9; padding: 15px; border-radius: 15px; margin-bottom: 20px; border-right: 4px solid var(--primary); }
        .nav-menu a {
            display: flex; align-items: center; padding: 12px 15px; text-decoration: none;
            color: #475569; transition: 0.3s; border-radius: 12px; font-weight: 600; margin-bottom: 8px; cursor: pointer;
        }
        .nav-menu a:hover, .nav-menu a.active { background: var(--primary); color: white; }

        #login-page {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.95); backdrop-filter: blur(10px); z-index: 3000; justify-content: center; align-items: center;
        }
        .login-card { background: white; padding: 40px; border-radius: 24px; width: 380px; text-align: center; }

        main { flex: 1; margin-right: var(--sidebar-width); transition: 0.4s; position: relative; }
        main.expanded { margin-right: 0; }

        .section-view { display: none; padding: 0; animation: fadeIn 0.6s ease; }
        .section-view.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .hero-banner {
            position: relative; width: 100%; height: 500px;
            background-image: url('https://images.unsplash.com/photo-1524178232363-1fb2b075b655?q=80&w=2000&auto=format&fit=crop');
            background-size: cover; background-position: center;
            display: flex; align-items: center; justify-content: center; text-align: center;
        }
        .hero-overlay {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(135deg, rgba(37, 99, 235, 0.85), rgba(30, 58, 138, 0.9));
        }
        .hero-content { position: relative; z-index: 10; color: white; padding: 20px; }

        .dashboard-container { margin-top: -80px; padding: 0 40px 40px; position: relative; z-index: 20; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
        .stat-card { background: white; padding: 30px; border-radius: 20px; box-shadow: var(--shadow); text-align: center; border-bottom: 5px solid var(--primary); }
        .stat-card h3 { font-size: 2.5rem; margin-top: 10px; }

        .card-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; padding: 40px; }
        .item-card { background: white; border-radius: 25px; overflow: hidden; box-shadow: var(--shadow); cursor: pointer; transition: 0.3s; }
        .item-card:hover { transform: translateY(-5px); }
        .item-card img { width: 100%; height: 200px; object-fit: cover; }
        .item-body { padding: 25px; }
        .sub-details { max-height: 0; overflow: hidden; transition: 0.5s ease; background: #f8fafc; padding: 0 20px; border-radius: 0 0 25px 25px; }
        .item-card.active .sub-details { max-height: 500px; padding: 20px; border-top: 1px dashed var(--primary); }

        .table-panel { background: white; padding: 30px; border-radius: 25px; box-shadow: var(--shadow); margin: 40px; }
        .table-wrap { overflow-x: auto; margin-top: 25px; border-radius: 15px; border: 1px solid #eee; }
        table { width: 100%; border-collapse: collapse; }
        table th { background: #f8fafc; padding: 15px; text-align: right; color: #334155; }
        table td { padding: 12px 15px; border-top: 1px solid #f1f5f9; }

        .btn { padding: 12px 25px; border: none; border-radius: 12px; cursor: pointer; font-weight: bold; display: inline-flex; align-items: center; gap: 10px; transition: 0.3s; }
        .btn-primary { background: var(--primary); color: white; }
        .btn-excel { background: #166534; color: white; }
        .btn-word { background: #1e40af; color: white; }
        .btn-pdf { background: #b91c1c; color: white; }
        .btn:hover { filter: brightness(1.1); transform: scale(1.02); }

        input { width: 100%; padding: 14px; border: 1.5px solid #e2e8f0; border-radius: 12px; margin-bottom: 15px; outline: none; }
        footer { text-align: center; padding: 30px; color: #64748b; font-weight: 600; }
    </style>
</head>
<body>

    <div id="login-page">
        <div class="login-card">
            <h2 style="color: var(--primary);">🔐 دخول المسؤول</h2><br>
            <input type="text" placeholder="اسم المستخدم">
            <input type="password" placeholder="كلمة المرور">
            <button class="btn btn-primary" style="width: 100%; justify-content: center;" onclick="closeLogin()">تأكيد الدخول</button>
            <p onclick="closeLogin()" style="margin-top: 20px; cursor: pointer; color: #64748b;">رجوع</p>
        </div>
    </div>

    <button id="menu-toggle" onclick="toggleSidebar()">☰</button>

    <aside id="sidebar">
        <div class="sb-block">
            <h4 onclick="openLogin()">👤 تسجيل الدخول</h4>
        </div>
        <div class="sb-block">
            <input type="text" placeholder="بحث فوري..." onkeyup="globalSearch(this.value)">
        </div>
        <nav class="nav-menu">
            <a onclick="navigate('home-view')" id="nav-home" class="active">🏠 الرئيسية والإحصائيات</a>
            <a onclick="navigate('services-view')">🛠️ الخدمات التربوية</a>
            <a onclick="navigate('method-view')">📋 منهجية العمل</a>
            <a onclick="navigate('gallery-view')">🖼️ معرض الأنشطة</a>
            <a onclick="navigate('data-view')" id="nav-data">📊 معالجة وتصدير البيانات</a>
            <a onclick="resetApp()" style="color: var(--danger); margin-top: 20px; border-top: 1px solid #eee;">🗑️ مسح الذاكرة</a>
        </nav>
    </aside>

    <main id="main-content">
        <section id="home-view" class="section-view active">
            <div class="hero-banner">
                <div class="hero-overlay"></div>
                <div class="hero-content">
                    <h1 style="font-size: 3rem; font-weight: 800;">المنصة الرقمية للمواكبة التربوية</h1>
                    <p style="font-size: 1.3rem; margin-top: 15px; opacity: 0.9;">بوابة متكاملة لتحليل البيانات التعليمية وتجويد التعلمات</p>
                </div>
            </div>

            <div class="dashboard-container">
                <div class="stats-grid">
                    <div class="stat-card">
                        <p style="color: #64748b;">إجمالي التلاميذ</p>
                        <h3 id="total-val" style="color: var(--primary);">0</h3>
                    </div>
                    <div class="stat-card" style="border-bottom-color: var(--danger);">
                        <p style="color: #64748b;">حالات التعثر</p>
                        <h3 id="fail-val" style="color: var(--danger);">0</h3>
                    </div>
                    <div class="stat-card" style="border-bottom-color: var(--success);">
                        <p style="color: #64748b;">نسبة النجاح</p>
                        <h3 id="rate-val" style="color: var(--success);">0%</h3>
                    </div>
                </div>

                <div style="background: white; padding: 40px; border-radius: 25px; box-shadow: var(--shadow); margin-top: 40px; text-align: center;">
                    <h3>📊 التحليل البياني العام</h3>
                    <canvas id="homeChart" style="max-height: 350px; margin: 30px auto;"></canvas>
                </div>
            </div>
        </section>

        <section id="services-view" class="section-view">
            <h2 style="padding: 40px 40px 0; color: #1e293b;">الخدمات والوحدات الفرعية</h2>
            <div class="card-grid">
                <div class="item-card" onclick="this.classList.toggle('active')">
                    <img src="https://images.unsplash.com/photo-1516321318423-f06f85e504b3?q=80&w=500&auto=format&fit=crop">
                    <div class="item-body">
                        <strong>🔍 رصد وتتبع التعثرات</strong>
                        <p style="color: #64748b; font-size: 0.85rem; margin-top: 5px;">انقر لرؤية التفاصيل ↓</p>
                    </div>
                    <div class="sub-details">
                        <p>• تحليل نتائج الأسدس الأول والأسدس الثاني.</p>
                        <p>• جرد لائحة التلاميذ ذوي الصعوبات في المواد الأساسية.</p>
                        <p>• مقارنة تطور النتائج بين الأسدسين.</p>
                    </div>
                </div>
                <div class="item-card" onclick="this.classList.toggle('active')">
                    <img src="https://images.unsplash.com/photo-1552664730-d307ca884978?q=80&w=500&auto=format&fit=crop">
                    <div class="item-body">
                        <strong>🧠 الدعم التربوي المخصص</strong>
                        <p style="color: #64748b; font-size: 0.85rem; margin-top: 5px;">انقر لرؤية التفاصيل ↓</p>
                    </div>
                    <div class="sub-details">
                        <p>• بناء بروتوكولات المعالجة والدعم.</p>
                        <p>• تقارير بيداغوجية موجهة للآباء والمدرسين.</p>
                        <p>• تتبع التطور الفردي للمتعلم خلال الموسم الدراسي.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="method-view" class="section-view">
            <h2 style="padding: 40px 40px 0;">منهجية العمل والتحصيل</h2>
            <div class="card-grid">
                <div class="item-card">
                    <img src="https://images.unsplash.com/photo-1454165833767-027ffea9e77b?q=80&w=500&auto=format&fit=crop">
                    <div class="item-body"><h4>1. تجميع واستيراد البيانات</h4><p style="font-size: 0.9rem;">استقبال ملفات مسار (Excel) ومعالجتها برمجياً بدقة متناهية.</p></div>
                </div>
                <div class="item-card">
                    <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?q=80&w=500&auto=format&fit=crop">
                    <div class="item-body"><h4>2. المعالجة والتقارير</h4><p style="font-size: 0.9rem;">توليد تقارير إحصائية وبيانية قابلة للتحميل بصيغ Word و PDF.</p></div>
                </div>
            </div>
        </section>

        <section id="gallery-view" class="section-view">
            <h2 style="padding: 40px 40px 0;">🖼️ معرض الأنشطة والفعاليات</h2>
            <div class="card-grid" style="grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));">
                <img src="https://images.unsplash.com/photo-1509062522246-3755977927d7?q=80&w=400" style="border-radius:20px; width:100%;">
                <img src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=400" style="border-radius:20px; width:100%;">
                <img src="https://images.unsplash.com/photo-1427504494785-3a9ca7044f45?q=80&w=400" style="border-radius:20px; width:100%;">
            </div>
        </section>

        <section id="data-view" class="section-view">
            <div class="table-panel">
                <h2>📊 إدارة ومعالجة الملفات</h2><br>
                <div style="background: #f8fafc; padding: 30px; border-radius: 20px; border: 2px dashed #cbd5e1; text-align: center;">
                    <p style="font-weight: 700; margin-bottom: 15px;">رفع ملفات النتائج (Excel / CSV / Word / PDF)</p>
                    <input type="file" id="filePicker" accept=".xlsx, .csv, .doc, .docx, .pdf">
                    <button class="btn btn-primary" style="width: 100%; justify-content: center;" onclick="uploadFile()">بدء المعالجة الذكية</button>
                </div>

                <div class="table-wrap">
                    <table id="mainDataTable">
                        <thead></thead>
                        <tbody></tbody>
                    </table>
                </div>

                <div style="display: flex; gap: 15px; margin-top: 30px; justify-content: center; flex-wrap: wrap;">
                    <button class="btn btn-excel" onclick="exportExcel()">تصدير Excel</button>
                    <button class="btn btn-word" onclick="exportWord()">تصدير Word</button>
                    <button class="btn btn-pdf" onclick="exportPDF()">تصدير PDF</button>
                </div>
            </div>
        </section>

        <footer><p>© 2025 منصة المواكبة التربوية الرقمية | جميع الحقوق محفوظة</p></footer>
    </main>

    <script>
        let globalHeaders = JSON.parse(localStorage.getItem("h_v10")) || [];
        let globalRows = JSON.parse(localStorage.getItem("r_v10")) || [];
        let chartObj = null;

        function toggleSidebar() {
            document.getElementById('sidebar').classList.toggle('closed');
            document.getElementById('main-content').classList.toggle('expanded');
        }

        function navigate(id) {
            document.querySelectorAll('.section-view').forEach(v => v.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.querySelectorAll('.nav-menu a').forEach(a => a.classList.remove('active'));
            if(event && event.currentTarget.tagName === 'A') event.currentTarget.classList.add('active');
            if(window.innerWidth < 900) toggleSidebar();
        }

        function openLogin() { document.getElementById('login-page').style.display = 'flex'; }
        function closeLogin() { document.getElementById('login-page').style.display = 'none'; }

        function uploadFile() {
            const file = document.getElementById('filePicker').files[0];
            if(!file) return alert("يرجى اختيار ملف أولاً");
            const reader = new FileReader();
            reader.onload = (e) => {
                const data = new Uint8Array(e.target.result);
                const wb = XLSX.read(data, {type: 'array'});
                const json = XLSX.utils.sheet_to_json(wb.Sheets[wb.SheetNames[0]], {header: 1});
                globalHeaders = json[0];
                globalRows = json.slice(1).filter(r => r.length > 0);
                localStorage.setItem("h_v10", JSON.stringify(globalHeaders));
                localStorage.setItem("r_v10", JSON.stringify(globalRows));
                updateAll();
                alert("تم تحديث قاعدة البيانات بنجاح!");
            };
            reader.readAsArrayBuffer(file);
        }

        function updateAll() {
            renderTable();
            updateDashboard();
        }

        function updateDashboard() {
            const total = globalRows.length;
            const fail = globalRows.filter(r => parseFloat(r[1]) < 10).length;
            const success = total - fail;
            const rate = total > 0 ? Math.round((success / total) * 100) : 0;

            document.getElementById("total-val").innerText = total;
            document.getElementById("fail-val").innerText = fail;
            document.getElementById("rate-val").innerText = rate + "%";

            if(chartObj) chartObj.destroy();
            chartObj = new Chart(document.getElementById('homeChart'), {
                type: 'bar',
                data: {
                    labels: ['إجمالي المتعلمين', 'حالات التعثر', 'حالات النجاح'],
                    datasets: [{
                        label: 'العدد',
                        data: [total, fail, success],
                        backgroundColor: ['#2563eb', '#ef4444', '#10b981'],
                        borderRadius: 10
                    }]
                },
                options: { plugins: { legend: { display: false } } }
            });
        }

        function renderTable(search = "") {
            const thead = document.querySelector("#mainDataTable thead");
            const tbody = document.querySelector("#mainDataTable tbody");
            if(globalHeaders.length === 0) return;
            thead.innerHTML = `<tr>${globalHeaders.map(h => `<th>${h}</th>`).join("")}</tr>`;
            const filtered = globalRows.filter(r => r.some(c => String(c).toLowerCase().includes(search)));
            tbody.innerHTML = filtered.map(row => `<tr>${row.map(cell => `<td>${cell}</td>`).join("")}</tr>`).join("");
        }

        function globalSearch(v) {
            navigate('data-view');
            renderTable(v.toLowerCase());
        }

        function exportExcel() {
            const ws = XLSX.utils.aoa_to_sheet([globalHeaders, ...globalRows]);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "البيانات");
            XLSX.writeFile(wb, "تقرير_المواكبة_التربوية.xlsx");
        }

        function exportWord() {
            let h = `<html xmlns:w='urn:schemas-microsoft-com:office:word'><head><meta charset='utf-8'></head><body><h2 style='text-align:center'>تقرير التحصيل الدراسي</h2><table border='1'>`;
            h += `<tr>${globalHeaders.map(x => `<th>${x}</th>`).join("")}</tr>`;
            globalRows.forEach(r => h += `<tr>${r.map(c => `<td>${c}</td>`).join("")}</tr>`);
            h += `</table></body></html>`;
            saveAs(new Blob(['\ufeff', h], {type: 'application/msword'}), "تقرير_المواكبة.doc");
        }

        function exportPDF() {
            const element = document.getElementById("data-view");
            html2canvas(element, { 
                scale: 2,
                useCORS: true,
                allowTaint: true
            }).then(canvas => {
                const imgData = canvas.toDataURL('image/png');
                const pdf = new jspdf.jsPDF('p', 'mm', 'a4');
                const imgProps = pdf.getImageProperties(imgData);
                const pdfWidth = pdf.internal.pageSize.getWidth();
                const pdfHeight = (imgProps.height * pdfWidth) / imgProps.width;
                
                pdf.addImage(imgData, 'PNG', 0, 10, pdfWidth, pdfHeight);
                pdf.save("تقرير_المواكبة_التربوية.pdf");
            });
        }

        function resetApp() { if(confirm("حذف كافة البيانات المسجلة؟")) { localStorage.clear(); location.reload(); } }

        window.onload = () => { if(globalRows.length > 0) updateAll(); };
    </script>
</body>
</html>
