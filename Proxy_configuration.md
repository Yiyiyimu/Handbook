## Github (解决国内下github速度慢)

git config --global http.proxy 'socks5://127.0.0.1:1080'

git config --global https.proxy 'socks5://127.0.0.1:1080'

**To Cancel:**

git config --global --unset http.proxy

git config --global --unset https.proxy


Reference：https://www.zhihu.com/question/27159393/answer/141047266

## cmd (解决国内挂vcpkg速度慢)

set http_proxy=http://127.0.0.1:1080

set https_proxy=http://127.0.0.1:1080

**For git-bash**

replace **set** with **export**

**To test:**

curl -vv google.com

**To cancel:**

set http_proxy=

set https_proxy=

Reference: https://zcdll.github.io/2018/01/27/proxy-on-windows-terminal
