Zabbix 繁體中文前端頁面翻譯


步驟(部分需 sudo)：

1.確認有安裝繁體中文語系
localectl list-locales

2.下載中文字體(這裡使用 NotoSansTC)
curl -o /usr/share/zabbix/assets/fonts/NotoSansTC[wght].ttf https://raw.githubusercontent.com/google/fonts/main/ofl/notosanstc/NotoSansTC%5Bwght%5D.ttf

3.修改設定檔 locales.inc.php，找到 function getLocales() 啟用繁體中文選項(false => true)
nano /usr/share/zabbix/include/locales.inc.php

4.修改設定檔 defines.inc.php，找到 'ZBX_GRAPH_FONT_NAME' 修改字體為剛下載的
nano /usr/share/zabbix/include/defines.inc.php

5.備份原檔(操作錯誤還原用)
cp /usr/share/zabbix/locale/zh_TW/LC_MESSAGES/frontend.mo /usr/share/zabbix/locale/zh_TW/LC_MESSAGES/frontend.mo.bak

6.下載 frontend.po 後編譯翻譯檔
msgfmt frontend.po -ofrontend.mo

7.取代原本翻譯檔
cp frontend.mo /usr/share/zabbix/locale/zh_TW/LC_MESSAGES/frontend.mo

8.重啟網頁服務
systemctl restart httpd

完成！！

(更改字體也可解決 zabbix 中文亂碼問題)
