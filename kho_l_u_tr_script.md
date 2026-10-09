<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kho Lưu Trữ Script</title>
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --accent-color: #3b82f6;
            --accent-hover: #2563eb;
            --danger-color: #ef4444;
            --success-color: #10b981;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --code-bg: #090d16;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 2rem;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 2rem;
        }

        header h1 {
            font-size: 2.5rem;
            color: var(--accent-color);
            margin-bottom: 0.5rem;
        }

        header p {
            color: var(--text-muted);
        }

        .add-form-container {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.5rem;
            margin-bottom: 2rem;
        }

        .form-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .form-header h2 {
            font-size: 1.25rem;
            color: var(--accent-color);
        }

        .file-actions {
            display: flex;
            gap: 0.5rem;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-row {
            display: flex;
            gap: 1rem;
        }

        .form-row .form-group {
            flex: 1;
        }

        label {
            display: block;
            font-size: 0.875rem;
            color: var(--text-muted);
            margin-bottom: 0.4rem;
        }

        input[type="text"], select, textarea {
            width: 100%;
            padding: 0.75rem;
            border-radius: 8px;
            border: 1px solid var(--border-color);
            background-color: var(--bg-color);
            color: var(--text-main);
            font-size: 0.95rem;
            outline: none;
            transition: border-color 0.2s;
        }

        input[type="text"]:focus, select:focus, textarea:focus {
            border-color: var(--accent-color);
        }

        textarea {
            resize: vertical;
            min-height: 100px;
            font-family: monospace;
        }

        .controls {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            flex-wrap: wrap;
        }

        .search-box {
            flex: 1;
            min-width: 250px;
        }

        .script-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.5rem;
        }

        .script-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .script-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.75rem;
        }

        .script-title {
            font-size: 1.25rem;
            font-weight: 600;
        }

        .badge {
            background-color: rgba(59, 130, 246, 0.2);
            color: var(--accent-color);
            padding: 0.25rem 0.6rem;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: bold;
            text-transform: uppercase;
        }

        .script-desc {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-bottom: 1rem;
            line-height: 1.4;
        }

        .code-preview {
            background-color: var(--code-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 0.75rem;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.85rem;
            color: #a7f3d0;
            overflow-x: auto;
            margin-bottom: 1rem;
            max-height: 100px;
            white-space: pre-wrap;
            word-break: break-all;
        }

        .card-actions {
            display: flex;
            gap: 0.5rem;
        }

        .btn {
            padding: 0.6rem 1rem;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
            text-align: center;
            font-size: 0.875rem;
        }

        .btn-primary {
            background-color: var(--accent-color);
            color: white;
            flex: 1;
        }

        .btn-primary:hover {
            background-color: var(--accent-hover);
        }

        .btn-secondary {
            background-color: transparent;
            border: 1px solid var(--border-color);
            color: var(--text-main);
        }

        .btn-secondary:hover {
            background-color: var(--border-color);
        }

        .btn-danger {
            background-color: rgba(239, 68, 68, 0.2);
            color: var(--danger-color);
            border: 1px solid rgba(239, 68, 68, 0.4);
        }

        .btn-danger:hover {
            background-color: var(--danger-color);
            color: white;
        }

        .btn-success {
            background-color: rgba(16, 185, 129, 0.2);
            color: var(--success-color);
            border: 1px solid rgba(16, 185, 129, 0.4);
        }

        .btn-success:hover {
            background-color: var(--success-color);
            color: white;
        }

        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #10b981;
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            font-weight: 500;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.3s, transform 0.3s;
            pointer-events: none;
        }

        .toast.show {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Kho Lưu Trữ Script</h1>
            <p>Quản lý và sao lưu kho script của bạn dễ dàng</p>
        </header>

        <div class="add-form-container">
            <div class="form-header">
                <h2>➕ Thêm Script Mới</h2>
                <div class="file-actions">
                    <button class="btn btn-success" onclick="exportData()">📥 Xuất File Dữ Liệu</button>
                    <button class="btn btn-secondary" onclick="document.getElementById('importInput').click()">📤 Nhập File Dữ Liệu</button>
                    <input type="file" id="importInput" accept=".json" style="display: none;" onchange="importData(event)">
                </div>
            </div>

            <form id="scriptForm" onsubmit="addScript(event)">
                <div class="form-row">
                    <div class="form-group">
                        <label for="title">Tên Script</label>
                        <input type="text" id="title" placeholder="VD: Blox Fruits Auto Farm" required>
                    </div>
                    <div class="form-group">
                        <label for="category">Danh mục / Ngôn ngữ</label>
                        <select id="category" required>
                            <option value="roblox">Roblox Lua</option>
                            <option value="python">Python</option>
                            <option value="javascript">JavaScript</option>
                            <option value="shell">Shell / Bash</option>
                        </select>
                    </div>
                </div>
                <div class="form-group">
                    <label for="description">Mô tả ngắn</label>
                    <input type="text" id="description" placeholder="Mô tả công dụng của script..." required>
                </div>
                <div class="form-group">
                    <label for="code">Mã Script (Code)</label>
                    <textarea id="code" placeholder="Dán đoạn mã script vào đây..." required></textarea>
                </div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">Lưu Script Vào Kho</button>
            </form>
        </div>

        <div class="controls">
            <div class="search-box">
                <input type="text" id="searchInput" placeholder="Tìm kiếm script..." oninput="filterScripts()">
            </div>
            <select class="filter-select" id="categoryFilter" onchange="filterScripts()">
                <option value="all">Tất cả danh mục</option>
                <option value="roblox">Roblox Lua</option>
                <option value="python">Python</option>
                <option value="javascript">JavaScript</option>
                <option value="shell">Shell / Bash</option>
            </select>
        </div>

        <div class="script-grid" id="scriptGrid"></div>
    </div>

    <div id="toast" class="toast">Đã thực hiện thành công!</div>

    <script>
        let scriptsData = JSON.parse(localStorage.getItem("my_scripts")) || [
            {
                id: Date.now(),
                title: "Blox Fruits Auto Farm",
                category: "roblox",
                description: "Script tự động cày level, chest và farm boss.",
                code: 'loadstring(game:HttpGet("https://raw.githubusercontent.com/Example/BloxFruits/main/script.lua"))()'
            }
        ];

        function saveToLocalStorage() {
            localStorage.setItem("my_scripts", JSON.stringify(scriptsData));
        }

        function exportData() {
            if (scriptsData.length === 0) {
                showToast("Kho script đang trống, không thể xuất file!");
                return;
            }
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(scriptsData, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `scripts_backup_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast("Đã xuất file lưu trữ dữ liệu thành công!");
        }

        function importData(event) {
            const fileReader = new FileReader();
            fileReader.onload = function(e) {
                try {
                    const importedScripts = JSON.parse(e.target.result);
                    if (Array.isArray(importedScripts)) {
                        scriptsData = importedScripts;
                        saveToLocalStorage();
                        renderScripts(scriptsData);
                        showToast("Đã khôi phục dữ liệu từ file thành công!");
                    } else {
                        alert("File JSON không hợp lệ.");
                    }
                } catch (err) {
                    alert("Đã xảy ra lỗi khi đọc file JSON.");
                }
            };
            if (event.target.files[0]) {
                fileReader.readAsText(event.target.files[0]);
            }
        }

        function downloadSingleScript(id) {
            const script = scriptsData.find(item => item.id === id);
            if (!script) return;

            let ext = ".txt";
            if (script.category === "roblox") ext = ".lua";
            else if (script.category === "python") ext = ".py";
            else if (script.category === "javascript") ext = ".js";
            else if (script.category === "shell") ext = ".sh";

            const blob = new Blob([script.code], { type: "text/plain;charset=utf-8" });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = `${script.title.toLowerCase().replace(/\s+/g, '_')}${ext}`;
            link.click();
            URL.revokeObjectURL(link.href);
            showToast(`Đã tải file ${ext} về máy!`);
        }

        function addScript(event) {
            event.preventDefault();
            const title = document.getElementById("title").value;
            const category = document.getElementById("category").value;
            const description = document.getElementById("description").value;
            const code = document.getElementById("code").value;

            scriptsData.unshift({
                id: Date.now(),
                title,
                category,
                description,
                code
            });

            saveToLocalStorage();
            renderScripts(scriptsData);
            document.getElementById("scriptForm").reset();
            showToast("Đã thêm script mới!");
        }

        function deleteScript(id) {
            if (confirm("Bạn có chắc chắn muốn xóa script này?")) {
                scriptsData = scriptsData.filter(script => script.id !== id);
                saveToLocalStorage();
                filterScripts();
                showToast("Đã xóa script!");
            }
        }

        function renderScripts(scripts) {
            const grid = document.getElementById("scriptGrid");
            grid.innerHTML = "";

            if (scripts.length === 0) {
                grid.innerHTML = `<p style="grid-column: 1/-1; text-align: center; color: var(--text-muted);">Chưa có script nào.</p>`;
                return;
            }

            scripts.forEach(script => {
                const card = document.createElement("div");
                card.className = "script-card";
                card.innerHTML = `
                    <div>
                        <div class="card-header">
                            <h3 class="script-title">${escapeHtml(script.title)}</h3>
                            <span class="badge">${script.category}</span>
                        </div>
                        <p class="script-desc">${escapeHtml(script.description)}</p>
                        <pre class="code-preview"><code>${escapeHtml(script.code)}</code></pre>
                    </div>
                    <div class="card-actions">
                        <button class="btn btn-primary" onclick="copyCode(${script.id})">Sao Chép</button>
                        <button class="btn btn-secondary" onclick="downloadSingleScript(${script.id})">Tải File</button>
                        <button class="btn btn-danger" onclick="deleteScript(${script.id})">Xóa</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterScripts() {
            const searchValue = document.getElementById("searchInput").value.toLowerCase();
            const categoryValue = document.getElementById("categoryFilter").value;

            const filtered = scriptsData.filter(script => {
                const matchesSearch = script.title.toLowerCase().includes(searchValue) || 
                                      script.description.toLowerCase().includes(searchValue);
                const matchesCategory = categoryValue === "all" || script.category === categoryValue;
                return matchesSearch && matchesCategory;
            });

            renderScripts(filtered);
        }

        function copyCode(id) {
            const script = scriptsData.find(item => item.id === id);
            if (script) {
                navigator.clipboard.writeText(script.code).then(() => {
                    showToast("Đã sao chép script vào clipboard!");
                });
            }
        }

        function showToast(message) {
            const toast = document.getElementById("toast");
            toast.innerText = message;
            toast.classList.add("show");
            setTimeout(() => toast.classList.remove("show"), 2500);
        }

        function escapeHtml(text) {
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
        }

        renderScripts(scriptsData);
    </script>
</body>
</html>