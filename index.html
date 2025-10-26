<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SNIP配置生成器</title>
<style>
/* ---------- 简化UI ---------- */
* { box-sizing: border-box; margin:0; padding:0; font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;}
body { background:#f0f2f5; color:#333; line-height:1.6; padding:20px; min-height:100vh;}
.container { max-width:900px; margin:0 auto; background:white; border-radius:10px; box-shadow:0 5px 20px rgba(0,0,0,0.1); padding:20px;}
header { text-align:center; margin-bottom:20px;}
h1 { font-size:2rem; color:#4a76a8; }
textarea { width:100%; min-height:120px; padding:10px; margin-bottom:10px; border-radius:5px; border:1px solid #ccc; font-family: monospace;}
button { padding:10px 15px; margin:5px 0; border:none; border-radius:5px; background:#4a76a8; color:white; cursor:pointer;}
button:hover { background:#3b5a80; }
.output { background:#222; color:#fff; padding:15px; border-radius:5px; font-family: monospace; max-height:400px; overflow:auto;}
.nav-links { display:flex; gap:10px; margin-bottom:20px; flex-wrap:wrap;}
.nav-links a, .nav-links button { text-decoration:none; color:white; background:#4a76a8; padding:8px 12px; border-radius:5px; }
.nav-links a:hover, .nav-links button:hover { background:#3b5a80; }
</style>
</head>
<body>
<div class="container">
<header>
<h1>SNIP配置生成器</h1>
</header>

<div class="nav-links">
    <button onclick="showPage('home')">首页</button>
    <button onclick="showPage('snipNode')">snip节点</button>
    <a href="https://cfxr.eu.org/sub-dev" target="_blank">获取白嫖哥snip</a>
    <a href="https://gist.github.com" target="_blank">Gist</a>
    <a href="https://sub.ikar.eu.org" target="_blank">soyo订阅转换</a>
</div>

<!-- 首页 -->
<div id="home">
    <label>配置文件开头:</label>
    <textarea id="configHeader">port: 7890
socks-port: 7891
allow-lan: true
mode: Rule
log-level: debug
external-controller: 127.0.0.1:9090
proxies:</textarea>

    <label>入口节点配置 (每行一个节点，多行可批量输入):</label>
    <div id="entryNodesContainer">
        <textarea class="entry-node" placeholder="请输入入口节点配置"></textarea>
    </div>
    <button id="addEntryNode">+ 添加入口节点输入框</button>

    <label>HTTPS节点配置 (每行一个节点，多行可批量输入，对应上面入口节点输入框):</label>
    <div id="httpsNodesContainer">
        <textarea class="https-node" placeholder="请输入HTTPS节点，每行一个"></textarea>
    </div>
    <button id="addHttpsNode">+ 添加HTTPS节点输入框</button>

    <button id="generateConfig">生成配置</button>
    <button id="copyConfig">一键复制</button>

    <div class="output"><pre id="output">生成结果将显示在这里...</pre></div>
</div>

<!-- snip节点页面 -->
<div id="snipNode" style="display:none;">
<h2>VLESS 批量转换为 Clash 配置</h2>
<label>输入多个 VLESS 链接（每行一个或 Base64 编码）:</label>
<textarea id="input" placeholder="vless://..."></textarea>
<button onclick="convert()">转换为 Clash 配置</button>
<button onclick="copyOutput()">复制结果</button>
<h3>转换结果：</h3>
<textarea id="outputNode" readonly></textarea>
</div>

<script>
function showPage(pageId){
    document.getElementById('home').style.display = pageId==='home' ? 'block' : 'none';
    document.getElementById('snipNode').style.display = pageId==='snipNode' ? 'block' : 'none';
}
showPage('home');

document.getElementById('addEntryNode').addEventListener('click',function(){
    const container=document.getElementById('entryNodesContainer');
    const newInput=document.createElement('textarea');
    newInput.className='entry-node';
    newInput.placeholder='请输入入口节点配置';
    container.appendChild(newInput);
});

document.getElementById('addHttpsNode').addEventListener('click',function(){
    const container=document.getElementById('httpsNodesContainer');
    const newInput=document.createElement('textarea');
    newInput.className='https-node';
    newInput.placeholder='请输入HTTPS节点，每行一个';
    container.appendChild(newInput);
});

const countryCodeMap = {US:'美国',HK:'香港',JP:'日本',TW:'台湾',SG:'新加坡',KR:'韩国',UK:'英国',DE:'德国',FR:'法国',CA:'加拿大',AU:'澳大利亚',RU:'俄罗斯',IN:'印度',BR:'巴西',MX:'墨西哥'};

function extractNameFromHttps(url){
    try{
        const hashIndex=url.indexOf('#');
        if(hashIndex===-1) return 'HTTPS节点';
        const hash=url.substring(hashIndex+1);
        for(const [code,name] of Object.entries(countryCodeMap)){
            if(hash.includes(`[${code}]`)||hash.includes(`_${code}_`)) return name;
        }
        if(hash.includes('中国_')){
            const parts=hash.split('_'); return parts[1]||'中国';
        }
        const parts=hash.split('_'); return parts[0]||'HTTPS节点';
    } catch{return 'HTTPS节点'; }
}

function cleanEntryNodeConfig(nodeConfig){
    return nodeConfig.replace(/^(\s*-\s*)/,'');
}

// 生成配置逻辑优化，HTTPS全局序号
document.getElementById('generateConfig').addEventListener('click',function(){
    let configHeader=document.getElementById('configHeader').value.trim();
    if(!configHeader) configHeader=`port: 7890
socks-port: 7891
allow-lan: true
mode: Rule
log-level: debug
external-controller: 127.0.0.1:9090
proxies:`;

    const entryNodesArray=Array.from(document.getElementsByClassName('entry-node')).map(t=>t.value.trim()).filter(Boolean);
    const httpsNodesArray=Array.from(document.getElementsByClassName('https-node')).map(t=>t.value.trim()).filter(Boolean);

    if(entryNodesArray.length===0 && httpsNodesArray.length===0){ alert('请至少输入一个节点配置！'); return; }

    let config=configHeader+'\n';

    // 添加入口节点
    entryNodesArray.forEach(enText=>{
        const lines=enText.split('\n').filter(Boolean);
        lines.forEach(l=>{ config+='  - '+cleanEntryNodeConfig(l)+'\n'; });
    });

    // HTTPS节点对应入口节点组合生成，序号全局累加
    let globalIndex = 1;
    httpsNodesArray.forEach((httpsText,index)=>{
        const httpsLines=httpsText.split('\n').filter(Boolean);
        const entryLines=(entryNodesArray[index]||'').split('\n').filter(Boolean);
        if(entryLines.length===0) return; // 没有对应入口节点则跳过
        httpsLines.forEach(httpsLine=>{
            entryLines.forEach(entryLine=>{
                try{
                    let server,port;
                    if(httpsLine.includes('://')){
                        const url=new URL(httpsLine);
                        server=url.hostname;
                        port=url.port||443;
                    } else{
                        const parts=httpsLine.split(':');
                        server=parts[0];
                        port=parts[1]||443;
                    }
                    const name=extractNameFromHttps(httpsLine)+'-'+globalIndex;
                    globalIndex++;
                    const dialerProxyMatch=entryLine.match(/name:\s*["']?([^'",}]+)["']?/);
                    const dialerProxy=dialerProxyMatch ? dialerProxyMatch[1] : 'snip';
                    config+=`  - name: "${name}"\n`;
                    config+=`    type: http\n`;
                    config+=`    server: ${server}\n`;
                    config+=`    port: ${port}\n`;
                    config+=`    tls: true\n`;
                    config+=`    skip-cert-verify: true\n`;
                    config+=`    dialer-proxy: "${dialerProxy}"\n\n`;
                } catch(e){ console.error('无效的HTTPS URL:',httpsLine,e); }
            });
        });
    });

    document.getElementById('output').textContent=config;
});

// 一键复制
document.getElementById('copyConfig').addEventListener('click',function(){
    const output=document.getElementById('output');
    if(!output.textContent || output.textContent==='生成结果将显示在这里...'){ alert('请先生成配置！'); return; }
    navigator.clipboard.writeText(output.textContent).then(()=>alert('配置已复制到剪贴板！')).catch(err=>console.error('复制失败:',err));
});

// ---------- snip节点页面不变 ----------
function tryDecodeBase64(text){
    try{ if(/^[A-Za-z0-9+/=\s]+$/.test(text)) return atob(text.replace(/\s+/g,'')); } catch(e){ console.warn('Base64 解码失败',e); }
    return text;
}
function convert(){
    let input=document.getElementById('input').value.trim();
    if(!input) return alert('请输入至少一个 VLESS 链接或 Base64 字符串');
    input=tryDecodeBase64(input);
    const lines=input.split('\n').map(l=>l.trim()).filter(Boolean);
    const result=[];
    lines.forEach((line,idx)=>{
        try{
            if(!line.startsWith('vless://')) throw new Error('无效 VLESS 链接');
            const [_,rest]=line.split('vless://');
            const [uuidAndServer,paramsAndName]=rest.split('?');
            const [uuid,serverPart]=uuidAndServer.split('@');
            const [server,portPart]=serverPart.split(':');
            const port=portPart?portPart.replace(/[^\d]/g,''):'';
            const [paramsStr,nameTag]=paramsAndName.split('#');
            const urlParams=new URLSearchParams(paramsStr);
            const rawNameTag=nameTag||'';
            let decodedNameTag='vless';
            if(rawNameTag){ try{ decodedNameTag=decodeURIComponent(rawNameTag); }catch(e){ decodedNameTag=rawNameTag; } }
            const name=`${decodedNameTag}${idx+1}`;
            const tls=urlParams.get('security')==='tls';
            const sni=urlParams.get('sni')||'';
            const fp=urlParams.get('fp')||'';
            const network=urlParams.get('type')||'ws';
            const host=urlParams.get('host')||sni;
            let path=decodeURIComponent(urlParams.get('path')||'/');
            if(!path.startsWith('/')) path='/'+path;
            result.push(`  - {name: ${name}, server: ${server}, port: ${port}, type: vless, uuid: ${uuid}, tls: ${tls}, tfo: false, skip-cert-verify: true, servername: ${sni}, client-fingerprint: ${fp}, network: ${network}, ws-opts: {path: "${path}", headers: {Host: ${host}}}}`);
        } catch(e){ result.push(`# 第 ${idx+1} 行解析失败：${line}`); }
    });
    document.getElementById('outputNode').value=result.join('\n');
}
function copyOutput(){
    const output=document.getElementById('outputNode');
    if(!output.value) return alert('没有内容可复制');
    output.select();
    document.execCommand('copy');
    alert('已复制到剪贴板！');
}
</script>
</body>
</html>
