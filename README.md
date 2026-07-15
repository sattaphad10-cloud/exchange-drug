<!DOCTYPE html>
<html lang="th">
<head>
    <!-- บังคับให้เบราว์เซอร์และระบบของ Tiiny.host อ่านรหัสภาษาไทยมาตรฐานทันที -->
    <meta charset="UTF-8">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <script>
        // โค้ดดักจับแก้ปัญหาภาษาต่างดาวจาก Iframe ของเว็บฝากไฟล์
        (function() {
            var meta = document.createElement('meta');
            meta.httpEquiv = "Content-Type";
            meta.content = "text/html; charset=utf-8";
            document.getElementsByTagName('head')[0].appendChild(meta);
        })();
    </script>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>รายการยาแลกเปลี่ยนหมดอายุ</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@400;700&display=swap');
        
        * { box-sizing: border-box; }
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 10px;
            color: #333;
        }
        .container {
            max-width: 800px;
            background: white;
            margin: 0 auto;
            padding: 15px;
            box-shadow: 0 0 10px rgba(0,0,0,0.05);
            border-radius: 8px;
        }
        h2 {
            text-align: center;
            font-size: 18px;
            margin-top: 10px;
            margin-bottom: 20px;
            font-weight: bold;
        }
        .section-title {
            font-size: 14px;
            font-weight: bold;
            margin-top: 25px;
            margin-bottom: 15px;
            background: #eaf5ec;
            padding: 10px;
            border-left: 4px solid #107c41;
            line-height: 1.4;
        }
        .item-card {
            border: 1px solid #e0e0e0;
            border-radius: 6px;
            padding: 12px;
            margin-bottom: 12px;
            background: #fff;
        }
        .item-number {
            font-weight: bold;
            color: #107c41;
            margin-bottom: 8px;
            font-size: 14px;
            border-bottom: 1px solid #eee;
            padding-bottom: 4px;
        }
        .form-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .form-group {
            display: flex;
            flex-direction: column;
            gap: 4px;
            width: 100%;
        }
        label {
            font-size: 13px;
            color: #666;
            font-weight: bold;
        }
        input[type="text"] {
            width: 100%;
            border: 1px solid #ccc;
            border-radius: 4px;
            padding: 8px 10px;
            font-family: 'Sarabun', sans-serif;
            font-size: 15px;
            background: #fff;
            outline: none;
        }
        .action-buttons {
            max-width: 800px;
            margin: 10px auto;
            display: flex;
            gap: 10px;
        }
        .btn {
            flex: 1;
            padding: 12px;
            font-family: 'Sarabun', sans-serif;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            border: none;
            border-radius: 6px;
            text-align: center;
        }
        .btn-print { background: #107c41; color: white; }
        .btn-clear { background: #e0e0e0; color: #333; }
        
        body.prepare-print { background: white !important; padding: 0 !important; }
        body.prepare-print .action-buttons { display: none !important; }
        body.prepare-print .container { box-shadow: none !important; padding: 0 !important; }
        body.prepare-print .item-card { border: none !important; padding: 0 !important; margin-bottom: 15px !important; }
        body.prepare-print .item-number { display: none !important; }
        body.prepare-print input[type="text"] {
            border: none !important;
            border-bottom: 1px dotted #000 !important;
            border-radius: 0 !important;
            padding: 2px !important;
            background: transparent !important;
        }
        body.prepare-print .section-title { background: transparent !important; border-left: none !important; padding: 0 !important; text-decoration: underline !important; }
        body.prepare-print .signature-section { border: none !important; background: transparent !important; padding: 0 !important; }

        .signature-section {
            margin-top: 30px;
            padding: 15px;
            background: #fdfdfd;
            border: 1px dashed #ccc;
            border-radius: 6px;
        }
        .signature-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 12px;
        }
        .signature-subtext {
            font-size: 12px;
            color: #666;
            margin-top: -4px;
            margin-bottom: 8px;
        }

        @media (min-width: 600px) {
            body { padding: 20px; }
            .container { padding: 30px; }
            .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
            .form-group { flex-direction: row; align-items: center; gap: 8px; }
            label { min-width: 60px; text-align: right; }
            .signature-section { max-width: 320px; margin-left: auto; }
            .action-buttons { justify-content: flex-end; }
            .btn { flex: none; padding: 10px 24px; }
        }

        @media print {
            body { background: white !important; padding: 0 !important; }
            .container { box-shadow: none !important; padding: 0 !important; margin: 0 !important; max-width: 100% !important; }
            .action-buttons { display: none !important; }
            .item-card { border: none !important; padding: 0 !important; margin-bottom: 15px !important; }
            .item-number { display: none !important; }
            .form-grid { display: grid !important; grid-template-columns: 1fr 1fr !important; gap: 8px !important; }
            .form-group { flex-direction: row !important; align-items: center !important; gap: 5px !important; }
            label { min-width: 50px !important; text-align: left !important; color: #000 !important; }
            input[type="text"] {
                border: none !important;
                border-bottom: 1px dotted #000 !important;
                border-radius: 0 !important;
                padding: 2px !important;
                background: transparent !important;
            }
            .section-title { background: transparent !important; border-left: none !important; padding: 0 !important; margin-top: 20px !important; text-decoration: underline !important; }
            .signature-section { border: none !important; background: transparent !important; padding: 0 !important; max-width: 300px !important; margin-left: auto !important; }
        }
    </style>
</head>
<body>

    <div class="action-buttons">
        <button class="btn btn-clear" onclick="clearForm()">ล้างข้อมูล</button>
        <button class="btn btn-print" onclick="smartPrint()">พิมพ์ฟอร์ม</button>
    </div>

    <div class="container">
        <h2>รายการยาแลกเปลี่ยนหมดอายุ</h2>

        <div class="section-title">รายการยาที่หมดอายุ (ชื่อยา/codeยา) จำนวน/ ราคาทุน(รวมภาษี)/มูลค่ารวม</div>
        
        <!-- รายการที่ 1 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 1</div>
            <div class="form-grid">
                <div class="form-group"><label>1.ชื่อยา</label><input type="text" id="exp_name_1"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exp_qty_1"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exp_pri_1"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exp_tot_1"></div>
            </div>
        </div>
        <!-- รายการที่ 2 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 2</div>
            <div class="form-grid">
                <div class="form-group"><label>2.ชื่อยา</label><input type="text" id="exp_name_2"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exp_qty_2"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exp_pri_2"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exp_tot_2"></div>
            </div>
        </div>
        <!-- รายการที่ 3 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 3</div>
            <div class="form-grid">
                <div class="form-group"><label>3.ชื่อยา</label><input type="text" id="exp_name_3"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exp_qty_3"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exp_pri_3"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exp_tot_3"></div>
            </div>
        </div>
        <!-- รายาการที่ 4 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 4</div>
            <div class="form-grid">
                <div class="form-group"><label>4.ชื่อยา</label><input type="text" id="exp_name_4"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exp_qty_4"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exp_pri_4"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exp_tot_4"></div>
            </div>
        </div>

        <div class="section-title">รายการที่แลกเปลี่ยน (ชื่อยา/codeยา) จำนวน/ ราคาทุน(รวมภาษี)/มูลค่ารวม</div>
        
        <!-- รายการที่ 1 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 1</div>
            <div class="form-grid">
                <div class="form-group"><label>1.ชื่อยา</label><input type="text" id="exc_name_1"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exc_qty_1"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exc_pri_1"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exc_tot_1"></div>
            </div>
        </div>
        <!-- รายการที่ 2 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 2</div>
            <div class="form-grid">
                <div class="form-group"><label>2.ชื่อยา</label><input type="text" id="exc_name_2"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exc_qty_2"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exc_pri_2"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exc_tot_2"></div>
            </div>
        </div>
        <!-- รายการที่ 3 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 3</div>
            <div class="form-grid">
                <div class="form-group"><label>3.ชื่อยา</label><input type="text" id="exc_name_3"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exc_qty_3"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exc_pri_3"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exc_tot_3"></div>
            </div>
        </div>
        <!-- รายการที่ 4 -->
        <div class="item-card">
            <div class="item-number">รายการที่ 4</div>
            <div class="form-grid">
                <div class="form-group"><label>4.ชื่อยา</label><input type="text" id="exc_name_4"></div>
                <div class="form-group"><label>จำนวน</label><input type="text" id="exc_qty_4"></div>
                <div class="form-group"><label>ราคาทุน</label><input type="text" id="exc_pri_4"></div>
                <div class="form-group"><label>มูลค่ารวม</label><input type="text" id="exc_tot_4"></div>
            </div>
        </div>

        <div class="signature-section">
            <div class="signature-group">
                <div class="form-group">
                    <label>ลงชื่อ</label>
                    <input type="text" id="sig_name">
                </div>
                <div class="signature-subtext" style="text-align: center; margin-left: 50px;">(ผู้แจ้งแลกเปลี่ยน)</div>
            </div>
            <div class="signature-group">
                <div class="form-group">
                    <label>วันที่แจ้ง</label>
                    <input type="text" id="sig_date">
                </div>
            </div>
        </div>
    </div>

    <script>
        const inputs = document.querySelectorAll('input[type="text"]');
        
        window.addEventListener('load', () => {
            inputs.forEach(input => {
                const savedValue = localStorage.getItem(input.id);
                if (savedValue) { input.value = savedValue; }
                input.addEventListener('input', () => {
                    localStorage.setItem(input.id, input.value);
                });
            });
        });

        function smartPrint() {
            window.print();
            document.body.classList.add('prepare-print');
            setTimeout(() => {
                alert('💡 แนะนำสำหรับมือถือ:\nหากหน้าต่างสั่งพิมพ์ไม่แสดงขึ้นมา ให้กดปุ่มแชร์/เมนูของเบราว์เซอร์ แล้วเลือกคำสั่ง "พิมพ์" (Print) ได้เลยครับ หน้าจอจะถูกจัดเป็นรูปแบบกระดาษไว้ให้แล้ว!');
            }, 300);
        }

        function clearForm() {
            if (confirm('คุณต้องการล้างข้อมูลทั้งหมดบนหน้าจอใช่หรือไม่?')) {
                inputs.forEach(input => {
                    input.value = '';
                    localStorage.removeItem(input.id);
                });
                document.body.classList.remove('prepare-print');
            }
        }
    </script>
</body>
</html>

