<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>文件分享站</title>
    <style>
        body { font-family: Arial; padding: 30px; }
        h1 { color: #333; }
        a { display: block; margin: 10px 0; font-size: 18px; }
    </style>
</head>
<body>
    <h1>文件分享站</h1>
    <p>点击以下文件下载：</p>

    <div id="file-list"></div>

    <script>
        // 自动列出文件（GitHub Pages 必须使用库内容 API）
        fetch('https://api.github.com/repos/USERNAME/REPO/contents')
            .then(r => r.json())
            .then(files => {
                const list = document.getElementById("file-list");
                files
                    .filter(f => f.type === "file" && f.name !== "index.html")
                    .forEach(f => {
                        const a = document.createElement("a");
                        a.href = f.download_url;
                        a.innerText = f.name;
                        list.appendChild(a);
                    });
            });
    </script>

</body>
</html>
