# wechat-sdk-cb
这是一个用CBrother实现的微信后台开发中所用到的加密算法

# 微信公众号后台开发
【微信公众号】目录为微信公众号后台开发中收发消息时用到的算法

对应了官方的这个页面的算法：https://developers.weixin.qq.com/doc/oplatform/Third-party_Platforms/2.0/api/Before_Develop/Technical_Plan.html

WXBizMsgCrypt.cb为算法库，使用时候主要是包含这个文件

sample.cb完全模拟了官方提供的例子

wechat.cb提供了一个微信公众号后台开发的例子，实现了后台验证功能和收发消息功能，收到到任何文本消息都返回 “收到了你发送的：+ 原消息内容”的效果

## 模拟官方的例子
```javascript
import WXBizMsgCrypt

//微信公众号后台加解密
//对应官方https://developers.weixin.qq.com/doc/oplatform/Third-party_Platforms/2.0/api/Before_Develop/Technical_Plan.html的加解密算法

function main(parm)
{
	var sAppid = "wx2c2769f8efd9abc2";
	var sToken = "spamtest";
	var sEncodingAesKey = "abcdefghijklmnopqrstuvwxyz0123456789ABCDEFG";
	
	var oWXBizMsgCrypt = new WXBizMsgCrypt(sToken,sEncodingAesKey,sAppid);

	var sMsgSignature = "003fee52ecc56afb46c00b5c7721be87860ce785";
	var sTimestamp = "1410349438";
	var sNonce = "298025754";
	var sEncryptBase64 = "mfBCs65c67CeJw22u4VT2TD73q5H06+ocrAIxswCaeZ/d/Lw0msSZFHY0teqgSYiI1zR2gD2DKrB3TIrmX/liNSDrGqS8jSI/WPeKB5VPr7Ezr7gomZAyGCwJSgT1TRFWPfONGJMxuj2nk4faTuspAuVIFQ6SHwZuJBZC7mcJp7Cgr9cUhATQWDbOPaE7ukZBTV2YqyzH+UI2AK+J1S47cE79k1RX8t0hcTz/O0hlK8DGXKnvYv88qKQcI7z4iaajqHfRVZKBNyOODabs+It+ZfM3dWTeFcPgDbGtIEnpt/EDtuuA/zMvtkaKdHdswPnVZQ+xdwbYr3ldGvfT8HlEYEgkgKaThxTFobVlwzu2ZkXCjicbP3xdr15Iq48ObgzPpqYuZ3IEoyggZDKClquk0u0orMck4GTF/XyE8yGzc4=";

	var sPostData = "<xml><ToUserName><![CDATA[toUser]]></ToUserName><Encrypt><![CDATA[" + sEncryptBase64 + "]]></Encrypt></xml>";

	print oWXBizMsgCrypt.decryptMsg(sMsgSignature,sTimestamp,sNonce,sPostData);

	var sToXml = "<xml><ToUserName><![CDATA[oia2TjjewbmiOUlr6X-1crbLOvLw]]></ToUserName><FromUserName><![CDATA[gh_7f083739789a]]></FromUserName><CreateTime>1407743423</CreateTime><MsgType><![CDATA[video]]></MsgType><Video><MediaId><![CDATA[eYJ1MbwPRJtOvIEabaxHs7TX2D-HV71s79GUxqdUkjm6Gs2Ed1KF3ulAOA9H1xG0]]></MediaId><Title><![CDATA[testCallBackReplyVideo]]></Title><Description><![CDATA[testCallBackReplyVideo]]></Description></Video></xml>";
	print oWXBizMsgCrypt.encryptMsg(sToXml,sTimestamp,sNonce);
}
```
# 微信小程序开发
【微信小程序】目录为微信小程序开发中用到的算法

对应了官方的这个页面的算法：https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html

WXBizDataCrypt.cb为算法库，使用时候主要是包含这个文件

sample.cb完全模拟了官方提供的例子

wechatapp.cb提供了一个微信小程序登录的例子
## 模拟官方的例子
```javascript
import WXBizDataCrypt

//微信小程序加解密
//对应官方https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html的加解密算法

function main()
{
	var sAppid = "wx4f4bc4dec97d474b";
	var sSessionkey = "tiihtNczf5v6AKRyjwEUhQ==";
	var sEncryptedData = "CiyLU1Aw2KjvrjMdj8YKliAjtP4gsMZMQmRzooG2xrDcvSnxIMXFufNstNGTyaGS9uT5geRa0W4oTOb1WT7fJlAC+oNPdbB+3hVbJSRgv+4lGOETKUQz6OYStslQ142dNCuabNPGBzlooOmB231qMM85d2/fV6ChevvXvQP8Hkue1poOFtnEtpyxVLW1zAo6/1Xx1COxFvrc2d7UL/lmHInNlxuacJXwu0fjpXfz/YqYzBIBzD6WUfTIF9GRHpOn/Hz7saL8xz+W//FRAUid1OksQaQx4CMs8LOddcQhULW4ucetDf96JcR3g0gfRK4PC7E/r7Z6xNrXd2UIeorGj5Ef7b1pJAYB6Y5anaHqZ9J6nKEBvB4DnNLIVWSgARns/8wR2SiRS7MNACwTyrGvt9ts8p12PKFdlqYTopNHR1Vf7XjfhQlVsAJdNiKdYmYVoKlaRv85IfVunYzO0IKXsyl7JCUjCpoG20f0a04COwfneQAGGwd5oa+T8yO5hzuyDb/XcxxmK01EpqOyuxINew==";
	
	var sIv = "r7BXXKkLb8qrSNn05n0qiA==";

	var oWXBizDataCrypt = new WXBizDataCrypt(sAppid, sSessionkey);

	print "sEncryptBase64 size:" + strlen(sEncryptedData);
	print "sIv size:" + strlen(sIv);

	print oWXBizDataCrypt.decryptData(sEncryptedData,sIv);
}
```
