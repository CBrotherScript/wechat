# wechat
这是一个用CBrother实现的微信后台开发的所有用到的消息加密算法,目前只实现了公众号后台加密算法，后续会提交微信小程序登录加密算法

对应了官方的这个页面的算法：https://developers.weixin.qq.com/doc/oplatform/Third-party_Platforms/2.0/api/Before_Develop/Technical_Plan.html

WXBizDataCrypt.cb为算法库，使用时候主要是包含这个文件

sample.cb完全模拟了官方提供的例子

wechat.cb提供了一个微信公众号后台开发的例子，实现了后台收到任何消息都返回 “收到了你发送的：+ 原消息内容”的效果

# 模拟官方的例子
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
