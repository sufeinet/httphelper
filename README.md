C#HttpHelper实现了C#HttpWebRequest抓取时无视编码，无视证书，无视Cookie，并且实现的代理的功能，使用它您可以进行Get和Post请求，可以很方便 的设置Cookie，证书，代理，编码问题您不用管，因为类会自动为您识别网页的编码。
       这个类是我以前写百度，Google，Soso，Sogou等网络蜘蛛时使用的，经过上千万个网站的测试，上万个网站抓取的例子总结出来的，中间的方法也是我实验了很久之后方案，所以大家可以放心使用。
       get,post
HttpHelper http = new HttpHelper();
           HttpItem item = new HttpItem()
           {
               URL = "http://www.sufeinet.com",//URL这里都是测试     必需项
               Method = "get",//URL     可选项 默认为Get
           };
           //得到HTML代码
           HttpResult result = http.GetHtml(item);
           item = new HttpItem()
          {
              URL = "http://tool.sufeinet.com",//URL这里都是测试URl   必需项
              Encoding = null,//编码格式（utf-8,gb2312,gbk）     可选项 默认类会自动识别
              //Encoding = Encoding.Default,
              Method = "post",//URL     可选项 默认为Get
              Postdata = "user=123123&pwd=1231313"
          };
           //得到新的HTML代码
           result = http.GetHtml(item);
           
           
           HttpHelper http = new HttpHelper();
          HttpItem item = new HttpItem()
          {
              URL = "http://www.sufeinet.com",//URL     必需项
              Encoding = null,//编码格式（utf-8,gb2312,gbk）     可选项 默认类会自动识别
               //Encoding = Encoding.Default,
              Method = "get",//URL     可选项 默认为Get
          };
          item.Header.Add("测试Key1", "测试Value1");
          item.Header.Add("测试Key2", "测试Value2");
          //得到HTML代码
          HttpResult result = http.GetHtml(item);
          //取出返回的Cookie
          string cookie = result.Cookie;
          //返回的Html内容
          string html = result.Html;
          if (result.StatusCode == System.Net.HttpStatusCode.OK)
          {
              //表示访问成功，具体的大家就参考HttpStatusCode类
          }
          //表示StatusCode的文字说明与描述
          string statusCodeDescription = result.StatusDescription;
          
          HttpHelper http = new HttpHelper();
          HttpItem item = new HttpItem()
          {
              URL = "http://www.sufeinet.com",//URL     必需项
              Encoding = null,//编码格式（utf-8,gb2312,gbk）     可选项 默认类会自动识别
              //Encoding = Encoding.Default,
              ResultType = ResultType.Byte
          };
          //得到HTML代码
          HttpResult result = http.GetHtml(item);
          if (result.StatusCode == System.Net.HttpStatusCode.OK)
          {
              //表示访问成功，具体的大家就参考HttpStatusCode类
          }
          //表示StatusCode的文字说明与描述
          string statusCodeDescription = result.StatusDescription;
          //把得到的Byte转成图片
          Image img = byteArrayToImage(result.ResultByte);
      }
 
      /// <summary>
      /// 字节数组生成图片
      /// </summary>
      /// <param name="Bytes">字节数组</param>
      /// <returns>图片</returns>
      private Image byteArrayToImage(byte[] Bytes)
      {
              MemoryStream ms = new MemoryStream(Bytes);
              Image outputImg = Image.FromStream(ms);
              return outputImg;
      }
           
           
           
