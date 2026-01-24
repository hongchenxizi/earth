<div align="center">

* PaaS 平台设置的环境变量
  | 变量名        | 是否必须 | 默认值 | 备注 |
  | ------------ | ------ | ------ | ------ |
  | UUID         | 否 |5efabea4-f6d4-91fd-b8f0-17e004c89c60| 开启了哪吒v1,请修改UUID|
  | PORT         | 否 |  3000  |  监听端口                    |
  | NAME         | 否 |        | 节点名称前缀，例如：Glitch |
  | DOMAIN       | 是 |        | 项目分配的域名或已反代的域名，不包括https://前缀  |
  | SUB_PATH     | 否 |  sub   | 订阅路径   |
  | AUTO_ACCESS  | 否 |  false | 是否开启自动访问保活,false为关闭,true为开启,需同时填写DOMAIN变量 |

```
export default {
    async fetch(request, env) {
        let url = new URL(request.url);
        if (url.pathname.startsWith('/')) {
            var arrStr = [
                'change.your.domain', // 此处单引号里填写你的节点伪装域名
            ];
            url.protocol = 'https:'
            url.hostname = getRandomArray(arrStr)
            let new_request = new Request(url, request);
            return fetch(new_request);
        }
        return env.ASSETS.fetch(request);
    },
};
function getRandomArray(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

