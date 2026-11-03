# 中国电信 Egern 小组件（待真机联调）

提供小、中、大号和锁屏组件，显示流量余量、已用/总量、剩余语音、余额和当天记录的余量变化。沿用用户提供的联通版布局，浅色白底、深色自适应。未获得的短信、本月消费、结转等数据不会编造。

## 安装

1. 在 Egern 中添加远程模块：
   https://raw.githubusercontent.com/Wyatt323/Egern/main/ChinaTelecom/ChinaTelecom.yaml
2. 启用模块及 HTTPS 解密，并按 Egern 指引安装、信任解密证书。
3. 在经 Egern 代理的 Safari 中打开 https://e.189.cn/index.do ，登录后进入套餐余量/余额页面。捕获成功后刷新小组件。
4. 添加 Egern 小组件，选择 `china-telecom`。

不要把捕获到的 Cookie 上传至仓库。

## 兼容边界

- 使用公开脚本记录的 `e.189.cn/store/user/package_detail.do` 和 `balance_new.do` 接口，只捕获这两个路径。尚未使用真实电信账号验证接口当前可用性、省份兼容性、登录跳转和 Egern 真机显示。
- 不承诺支持电信 App 或微信小程序；如网页不再调用这两个接口，需要依据实际响应适配。可提供脱敏后的接口域名、路径和响应字段，务必去掉 Cookie、Token、手机号及身份信息。
- 余额按分转元；流量按 KB 转 MB/GB。优先使用接口汇总字段；汇总不可用时累加 `unitTypeId=3` 且 `offerType!=19` 的明细。不同套餐的汇总口径可能包含定向流量，尚不提供通用/定向切换。无限量/特殊单位套餐需要进一步适配。
- Cookie 仅存 Egern 本地存储，用于同域查询。过期后重新登录；失败保留缓存并显示缓存标记。余额与余量可能来自不同时间，更新时间采用较早的一项。
- 当天用量是当天首次记录至今的余量差，不是运营商自然日账单；赠包、套餐变更、月初重置会影响估算。
- 切换号码前应清理此脚本存储，避免不同号码历史混合。

## 来源

UI 改编自 https://github.com/moyuzaime/egern/blob/main/ChinaUnicom/ChinaUnicom_Widget.js 。
电信接口及单位参考 https://github.com/dompling/Scriptable/blob/master/Scripts/ChinaTelecom.js 。
公开发布或分发前请核对上游许可和署名要求。
