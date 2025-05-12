addEventListener('scheduled', event => event.waitUntil(handleScheduled()));

// 配合甬哥的 serv00 SSH 脚本 / Github / VPS / 软路由脚本，生成保活网页与重启网页
// 每个保活 /up 网页或每个重启 /re 网页之间用空格、逗号或其他间隔符，网页前需带 http://
const urlString = 'http://保活或重启网页1 http://保活或重启网页2 http://保活或重启网页3 ………';
const urls = urlString.split(/[\s,，]+/);
const TIMEOUT = 5000;

async function fetchWithTimeout(url) {
  const controller = new AbortController();
  const timeout = setTimeout(() => controller.abort(), TIMEOUT);
  try {
    await fetch(url, { signal: controller.signal });
    console.log(`✅ 成功: ${url}`);
  } catch (error) {
    console.warn(`❌ 访问失败: ${url}, 错误: ${error.message}`);
  } finally {
    clearTimeout(timeout);
  }
}

async function handleScheduled() {
  console.log('⏳ 任务开始');
  await Promise.all(urls.map(fetchWithTimeout));
  console.log('📊 任务结束');
}
