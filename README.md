# gufengai.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI古风文章生成器</title>
    <style>
        *{
            margin:0;
            padding:0;
            box-sizing:border-box;
        }
        body{
            background-color: #f8f2e4;
            font-family: "宋体", "微软雅黑", serif;
            max-width: 850px;
            margin: 60px auto;
            padding: 0 20px;
        }
        h1{
            color: #7b241c;
            text-align: center;
            margin-bottom: 40px;
            font-size: 32px;
            letter-spacing: 4px;
        }
        .input-box{
            width: 100%;
            padding: 15px;
            font-size: 17px;
            border: 1px solid #c9b397;
            border-radius: 8px;
            background: #fffaf0;
        }
        .btn-generate{
            width: 100%;
            padding: 14px;
            margin: 20px 0;
            background-color: #7b241c;
            color: #fff;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            cursor: pointer;
            letter-spacing: 2px;
        }
        .result-box{
            width: 100%;
            height: 420px;
            padding: 15px;
            border: 1px solid #c9b397;
            border-radius: 8px;
            background: #fffaf0;
            font-size: 16px;
            line-height: 1.8;
            white-space: pre-wrap;
            color: #333;
        }
    </style>
</head>
<body>

    <h1>AI 古风文章生成器</h1>

    <input class="input-box" id="userInput" placeholder="请输入创作主题：如 江南烟雨、江湖侠义、边塞秋风、古风小说开篇">

    <button class="btn-generate" id="generateBtn">一键生成古风文章</button>

    <div class="result-box" id="resultBox"></div>

    <script>
        const btn = document.getElementById('generateBtn');
        const input = document.getElementById('userInput');
        const result = document.getElementById('resultBox');

        btn.addEventListener('click', async () => {
            let topic = input.value.trim();
            if(!topic){
                result.innerText = "请先输入创作主题再点击生成";
                return;
            }
            // 构造古风专用提示词
            let prompt = `请以纯正中国古风文笔创作一篇完整文章，文风典雅辞藻古雅，句式有古韵，不要现代口语，主题：${topic}`;
            try{
                result.innerText = "正在生成古风文章，请稍候...";
                let res = await fetch(`https://text.pollinations.ai/${encodeURIComponent(prompt)}`);
                let text = await res.text();
                result.innerText = text;
            }catch(err){
                result.innerText = "生成失败，请稍后重试";
            }
        });
    </script>

</body>
</html>
